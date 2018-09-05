---
title: Rozpoznawanie zależności pakietu NuGet
description: Szczegółowe informacje na temat procesu za pomocą którego zależności pakietu NuGet są rozwiązane i zainstalowane w obu NuGet 2.x i NuGet 3.x+.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: cdbe13df04bb27091b684a4ae27b0e751da1098f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549037"
---
# <a name="how-nuget-resolves-package-dependencies"></a>Jak NuGet jest rozpoznawana jako zależności pakietów

Ilekroć pakiet jest zainstalowany lub ponownej instalacji, w tym instalowany jako część [przywrócić](../consume-packages/package-restore.md) procesu NuGet instaluje również wszelkich dodatkowych pakietów, od których zależy ten pakiet pierwszy.

Te zależności natychmiastowe następnie może również są zależne od własnych, wciąż mogą dowolnego głębi. Tworzy to, co jest nazywane *wykres zależności* , który opisuje relacje między pakietami na wszystkich poziomach.

Gdy wiele pakietów mają ten sam zależność, następnie ten sam identyfikator pakietu może znajdować się na wykresie wielokrotnie, potencjalnie z ograniczeniami w innej wersji. Jednak tylko jedną wersję dany pakiet może służyć w projekcie, więc NuGet należy wybrać, która wersja jest używana. Dokładne proces zależy od formatu zarządzania pakietów, które są używane.

## <a name="dependency-resolution-with-packagereference"></a>Rozpoznawanie zależności za pomocą funkcji PackageReference

Podczas instalowania pakietów do projektów przy użyciu formatu PackageReference, NuGet dodaje odwołania do pakietu prostego wykresu w pliku odpowiednią i rozwiązywania konfliktów wcześniej. Ten proces jest nazywany *przechodnie przywracania*. Ponowne zainstalowanie lub Trwa przywracanie pakietów następnie proces pobierania pakietów wymienionych na wykresie skutkuje szybszy i bardziej przewidywalne kompilacje. Możesz również korzystać z zalet symbolu wieloznacznego (zmiennoprzecinkowego) wersji, takich jak 2.8. \*, unikanie kosztownych i błąd wywołania podatne `nuget update` na maszynach klienckich i serwerach kompilacji.

Podczas procesu przywracania NuGet przed kompilacji go najpierw rozpoznaje zależności w pamięci, a następnie zapisuje wynikowy wykres w pliku o nazwie `project.assets.json` w `obj` folderu projektu przy użyciu funkcji PackageReference. Program MSBuild następnie odczytuje ten plik i przekształca je w zestawie folderów, gdzie można znaleźć potencjalnych odwołania, a następnie dodanie ich do drzewa projektu w pamięci.

Plik blokady są tymczasowe i nie należy dodawać do kontroli źródła. Ta opcja jest wyświetlana domyślnie w obu `.gitignore` i `.tfignore`. Zobacz [pakiety i kontrola źródła](packages-and-source-control.md).

### <a name="dependency-resolution-rules"></a>Zasad rozpoznawania zależności

Przywracanie przechodnie stosuje cztery główne zasady, aby rozpoznać zależności: najniższy odpowiednią wersję, zmiennoprzecinkowy wersje, najbliższego serwera wins i cousin zależności.

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a>Najtańsza odpowiednią wersję

Najniższy reguły odpowiednią wersję przywraca najniższy wersję pakietu, zgodnie z jego zależności. Ma również zastosowanie do zależności od aplikacji lub biblioteki klas o ile nie jest zadeklarowany jako [zmiennoprzecinkowy](#floating-versions).

Na poniższej ilustracji na przykład 1.0 beta jest uważana za niższa niż 1.0 tak NuGet wybiera wersję 1.0:

![Wybór najtańsza odpowiednią wersję](media/projectJson-dependency-1.png)

Na poniższej ilustracji, wersja 2.1 nie jest dostępna w źródle danych, ale ponieważ jest ograniczenie wersji > = następnej wersji najniższy, można go znaleźć, w tym przypadku 2.2 2.1 pobrań NuGet:

![Wybór następnego Najniższa wersja dostępne w źródle danych](media/projectJson-dependency-2.png)

Aplikacja określa numer wersji dokładnie, takie jak 1.2, który nie jest dostępna w źródle danych, NuGet nie powiedzie się z powodu błędu podczas próby zainstalowania lub przywracanie pakietu:

![NuGet generuje błąd, gdy wersja pakietu dokładnie nie jest dostępna](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-wildcard-versions"></a>Wersje (symbol wieloznaczny)

Wersja zależności liczb zmiennoprzecinkowych lub symbol wieloznaczny jest określony za pomocą \* symbole wieloznaczne, podobnie jak w wersji 6.0.\*. Ta specyfikacja wersji jest wyświetlany komunikat "Użyj najnowszej wersji 6.0.x;" 4.\* oznacza, że "Użyj najnowszej wersji 4.x." Użycie symbolu wieloznacznego umożliwia pakiet zależności, aby kontynuować, zmieniające się bez konieczności zmiany aplikacja odbierająca komunikaty (lub pakietu).

Korzystając z symbolem wieloznacznym, NuGet jest rozpoznawany jako najwyższa wersja pakietu, który pasuje do wzorca wersji, na przykład 6.0. \* pobiera najwyższej wersji pakietu, który rozpoczyna się od 6.0:

![Wybieranie wersji 6.0.1 podczas przestawne w wersji 6.0. * żądania](media/projectJson-dependency-4.png)

> [!Note]
> Aby uzyskać informacje na zachowaniu symbole wieloznaczne i wersje wstępne, zobacz [przechowywanie wersji pakietów](../reference/package-versioning.md#version-ranges-and-wildcards).


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a>Najbliższy serwer wins

Jeśli wykres pakietu dla aplikacji zawiera różne wersje tego samego pakietu, NuGet wybiera pakiet, który jest najbardziej zbliżony do aplikacji na wykresie i ignoruje wszystkie inne. To zachowanie umożliwia aplikacji zastąpienie dowolnej wersji danego pakietu w wykresie zależności.

W poniższym przykładzie jest zależna aplikacja bezpośrednio na pakiet B z ograniczenie wersji > = w wersji 2.0. Aplikacja zależy również od pakietu element, który z kolei również jest zależny pakiet b, ale z > = 1,0 ograniczenia. Zależność od pakietu B w wersji 2.0 jest bliżej aplikacji na wykresie, zostanie użyta tej wersji:

![Aplikacji przy użyciu reguły najbliższej Wins](media/projectJson-dependency-5.png)

>[!Warning]
> Reguła najbliższej Wins może spowodować obniżenie wersji pakietu, w związku z tym potencjalnie istotne innych zależności na wykresie. Dlatego ta reguła jest stosowana z ostrzeżeniem, aby ostrzec użytkownika.

Ta zasada również wyników w większej wydajności za pomocą wykresu zależności dużych (takich jak za pomocą pakietów BCL), ponieważ po danym zależności jest ignorowany, NuGet ignoruje także wszystkich zależności pozostałych w tej gałęzi wykresu. Na poniższym diagramie na przykład, ponieważ jest używany pakiet języka C w wersji 2.0, NuGet ignoruje żadnych gałęzi na wykresie, które odwołują się do starszej wersji pakietu C:

![Gdy NuGet ignoruje pakietu na wykresie, powoduje ignorowanie tego całą gałąź](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a>Cousin zależności

Gdy inny pakiet wersje są określane w tej samej odległości na wykresie z aplikacji, NuGet używa Najniższa wersja, która spełnia wszystkie wymagania dotyczące wersji (podobnie jak w przypadku [najniższy odpowiednią wersję](#lowest-applicable-version) i [ wersje](#floating-versions) zasady). Na poniższej ilustracji, na przykład wersji 2.0 pakiet B spełnia innych > = ograniczenie wersji 1.0, a ten sposób jest używany:

![Rozpoznawanie zależności cousin przy użyciu starszej wersji, który spełnia wszystkie ograniczenia](media/projectJson-dependency-7.png)

W niektórych przypadkach nie jest możliwe spełnić wszystkie wymagania dotyczące wersji. Jak pokazano poniżej, jeśli pakiet A wymaga dokładnie pakiet B 1.0, a pakiet C pakiet B > = 2.0, wówczas nie można rozpoznać zależności i powoduje błąd NuGet.

![Nierozpoznane zależności ze względu na to wymaganie dotyczące dokładna wersja](media/projectJson-dependency-8.png)

W takich przypadkach konsument najwyższego poziomu (aplikacją lub pakietem) należy dodać bezpośredniej zależności pakiet B tak, aby [najbliższej Wins](#nearest-wins) reguła ma zastosowanie.

## <a name="dependency-resolution-with-packagesconfig"></a>Rozpoznawanie zależności z pliku packages.config

Za pomocą `packages.config`, zależności projektu są zapisywane w `packages.config` jako płaska lista. Wszelkie zależności te pakiety są również zapisane na tej samej liście. Po zainstalowaniu pakietów NuGet może także modyfikować `.csproj` pliku `app.config`, `web.config`oraz inne poszczególne pliki.

Za pomocą `packages.config`, próbuje rozwiązać konflikty zależności podczas instalacji poszczególnych poszczególnych pakietów NuGet. Oznacza to, jeśli pakiet A jest w trakcie instalacji i jest zależny od pakietu B i B pakiet jest już na liście `packages.config` jako zależność coś innego, porównuje wersje pakietu B żądanej i próbuje odnaleźć wersję, która spełnia wszystkie wersje NuGet ograniczenia. W szczególności NuGet wybiera niższym *major.minor* wersji, który spełnia zależności.

Domyślnie program NuGet 2.8 szuka Najniższa wersja poprawki (zobacz [informacje o wersji NuGet 2.8](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)). Można kontrolować tego ustawienia za pomocą `DependencyVersion` atrybutu w `Nuget.Config` i `-DependencyVersion` Przejdź w wierszu polecenia.  

`packages.config` Przetwarzania dla rozpoznawania zależności pobiera skomplikowane dla większych wykresów zależności. Każda nowa instalacja pakietu wymaga przechodzenia całego wykresu i zgłasza prawdopodobieństwo wystąpienia konfliktów wersji. Gdy wystąpi konflikt, instalacja zostanie zatrzymana, pozostawiając projektu w stanie nieokreślonym, szczególnie w przypadku potencjalne zmiany w samym pliku projektu. Nie jest to problem, korzystając z formatów pakietu zarządzania.

## <a name="managing-dependency-assets"></a>Zarządzanie zasobami zależności

Korzystając z formatu PackageReference, można kontrolować trwałe, które z przepływu zależności do najwyższego poziomu projektu. Aby uzyskać więcej informacji, zobacz [PackageReference](package-references-in-project-files.md#controlling-dependency-assets).

Gdy najwyższego poziomu projektu jest to pakiet, jednocześnie masz kontrolę nad ten przepływ przy użyciu `include` i `exclude` atrybutów ze składników zależnych wymienionych w `.nuspec` pliku. Zobacz [odwołanie .nuspec — zależności](../reference/nuspec.md#dependencies).

## <a name="excluding-references"></a>Z wyjątkiem odwołania

Istnieją scenariusze, w których zestawów o takiej samej nazwie może występować odwołanie do więcej niż jeden raz w projekcie, tworzenie błędy w czasie projektowania i w czasie kompilacji. Należy wziąć pod uwagę projekt, który zawiera niestandardową wersję `C.dll`i zawiera odwołania do pakietu języka C, który zawiera także `C.dll`. W tym samym czasie projekt zależy również od B pakiet, który również jest zależny od pakietu C i `C.dll`. W rezultacie NuGet nie można określić, które `C.dll` do użycia, ale po prostu nie można usunąć projektu zależności pakietu języka C, ponieważ pakiet B również zależy od niego.

Aby rozwiązać ten problem, należy bezpośrednio odwoływać się `C.dll` mają (lub użyj innego pakietu, który odwołuje się do właściwy), a następnie dodać zależność od pakietu języka C, która wyklucza wszystkie jej zasoby. W zależności od formatu używanego pakietu zarządzania odbywa się w następujący sposób:

- [PackageReference](../consume-packages/package-references-in-project-files.md): Dodaj `Exclude="All"` w zależności:

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" Exclude="All" />
    ```

- `packages.config`: Usuń odwołanie do PackageC z `.csproj` plików tak, aby odwoływał się tylko wersję `C.dll` przewidzianą.
    
## <a name="dependency-updates-during-package-install"></a>Instalowanie aktualizacji zależność w pakiecie 

Jeśli wersja zależności jest już spełniany, zależność nie zostały zaktualizowane podczas inne instalacje pakietu. Na przykład rozważmy element jest zależny od pakietu B, która określa 1.0, aby uzyskać numer wersji pakietu. Repozytorium źródłowe zawiera wersji 1.0, 1.1 i 1.2, pakiet B. Jeśli element jest zainstalowany w projekcie, który zawiera już B w wersji 1.0, B 1.0 pozostaje wówczas w użyciu, ponieważ spełnia ograniczenie wersji. Jednakże jeśli pakiet A żądań w wersji 1.1 lub nowszej b, następnie B 1.2 zostanie zainstalowany. 

## <a name="resolving-incompatible-package-errors"></a>Rozwiązywanie błędów pakietu niezgodne

Operacja przywracania podczas pakietu, może zostać wyświetlony błąd "co najmniej jednego pakietu nie są zgodne...", lub pakietu "nie jest zgodny" przy użyciu platformy docelowej projektu.

Ten błąd występuje, gdy jeden lub więcej pakietów, do którego odwołuje się projekt wskazuje, czy obsługują one platforma docelowa projektu; oznacza to, że pakiet nie zawiera odpowiedniej biblioteki DLL w jego `lib` folder dla platformy docelowej, który jest zgodny z projektem. (Zobacz [ustalać platformy docelowe](../reference/target-frameworks.md) dla listy.) 

Na przykład, jeśli projekt jest ukierunkowany `netstandard1.6` i spróbujesz zainstalować pakiet zawierający pliki DLL tylko `lib\net20` i `\lib\net45` folderów, możesz wyświetlić komunikaty następujący pakiet i prawdopodobnie jej zależności:

```output
Restoring packages for myproject.csproj...
Package ContosoUtilities 2.1.2.3 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoUtilities 2.1.2.3 supports:
  - net20 (.NETFramework,Version=v2.0)
  - net45 (.NETFramework,Version=v4.5)
Package ContosoCore 0.86.0 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoCore 0.86.0 supports:
  - 11 (11,Version=v0.0)
  - net20 (.NETFramework,Version=v2.0)
  - sl3 (Silverlight,Version=v3.0)
  - sl4 (Silverlight,Version=v4.0)
One or more packages are incompatible with .NETStandard,Version=v1.6.
Package restore failed. Rolling back package changes for 'MyProject'.
```

Aby rozwiązać niezgodności, wykonaj jedną z następujących czynności:

- Zmień platformę docelową projektu Framework, który jest obsługiwany przez pakiety, które chcesz użyć.
- Skontaktuj się z autorem pakietów i pracować z nimi, aby dodać obsługę używanej platformy wybrany. Każdy pakiet stronie listy na [nuget.org](https://www.nuget.org/) ma **skontaktuj się z właścicielami** łącze do tego celu.

