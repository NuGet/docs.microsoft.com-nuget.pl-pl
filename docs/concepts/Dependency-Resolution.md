---
title: Rozpoznawanie zależności pakietu NuGet
description: Szczegóły dotyczące procesu, za pośrednictwem którego zależności pakietu NuGet są rozpoznawane i instalowane w nuget 2.x i NuGet 3.x+.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 4b95251e4b055523a9533b4125589b2650be932d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428829"
---
# <a name="how-nuget-resolves-package-dependencies"></a>Jak NuGet rozwiązuje zależności pakietów

Za każdym razem, gdy pakiet jest zainstalowany lub ponownie zainstalowany, co obejmuje instalowanie w ramach procesu [przywracania,](../consume-packages/package-restore.md) NuGet instaluje również wszelkie dodatkowe pakiety, od których zależy ten pierwszy pakiet.

Te bezpośrednie zależności mogą mieć również zależności na własną rękę, które mogą nadal dowolnie głębokość. Powoduje to, co nazywa się *wykres zależności,* który opisuje relacje między pakietami na wszystkich poziomach.

Gdy wiele pakietów mają taką samą zależność, a następnie ten sam identyfikator pakietu może pojawić się na wykresie wiele razy, potencjalnie z różnych ograniczeń wersji. Jednak tylko jedna wersja danego pakietu może służyć w projekcie, więc NuGet musi wybrać, która wersja jest używana. Dokładny proces zależy od używanego formatu zarządzania pakietami.

## <a name="dependency-resolution-with-packagereference"></a>Rozpoznawanie zależności za pomocą packagereference

Podczas instalowania pakietów w projektach przy użyciu formatu PackageReference, NuGet dodaje odwołania do wykresu pakietu płaskiego w odpowiednim pliku i rozwiązuje konflikty z wyprzedzeniem. Proces ten jest określany jako *przywracanie przechodnie*. Ponowne instalowanie lub przywracanie pakietów jest następnie procesem pobierania pakietów wymienionych na wykresie, co powoduje szybsze i bardziej przewidywalne kompilacje. Można również skorzystać z wersji przestawnych, takich jak 2.8. \*, aby uniknąć modyfikowania projektu w celu użycia najnowszej wersji pakietu.

Gdy proces przywracania NuGet jest uruchamiany przed kompilacją, najpierw rozpoznaje zależności w pamięci, `project.assets.json`a następnie zapisuje wynikowy wykres do pliku o nazwie . Zapisuje również rozpoznane zależności do pliku `packages.lock.json`blokady o nazwie , jeśli [funkcja pliku blokady jest włączona](../consume-packages/package-references-in-project-files.md#locking-dependencies).
Plik zasobów znajduje się `MSBuildProjectExtensionsPath`w , który domyślnie do projektu "obj" folderu. MSBuild następnie odczytuje ten plik i tłumaczy go na zestaw folderów, w których można znaleźć potencjalne odwołania, a następnie dodaje je do drzewa projektu w pamięci.

Plik `project.assets.json` jest tymczasowy i nie należy go dodawać do kontroli źródła. Jest domyślnie wymieniony w `.gitignore` `.tfignore`obu i . Zobacz [Pakiety i kontrola źródła](../consume-packages/packages-and-source-control.md).

### <a name="dependency-resolution-rules"></a>Reguły rozpoznawania zależności

Przywracanie przechodnie stosuje cztery główne reguły w celu rozwiązania zależności: najniższa obowiązująca wersja, wersje przestawne, najbliższe wygrane i zależności kuzyna.

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a>Najniższa obowiązująca wersja

Reguła najniższej odpowiedniej wersji przywraca najniższą możliwą wersję pakietu zdefiniowaną przez jego zależności. Dotyczy to również zależności od aplikacji lub biblioteki klas, chyba że zadeklarowane jako [pływające](#floating-versions).

Na poniższej ilustracji, na przykład 1.0-beta jest uważany za niższy niż 1.0 więc NuGet wybiera wersję 1.0:

![Wybór najniższej odpowiedniej wersji](media/projectJson-dependency-1.png)

Na następnym rysunku wersja 2.1 nie jest dostępna w kanale informacyjnym, ale ponieważ ograniczenie wersji jest >= 2.1 NuGet wybiera następną najniższą wersję, która może znaleźć, w tym przypadku 2.2:

![Wybór następnej najniższej dostępnej wersji w kanale informacyjnym](media/projectJson-dependency-2.png)

Gdy aplikacja określa dokładny numer wersji, takich jak 1.2, który nie jest dostępny w kanale informacyjnym, NuGet kończy się niepowodzeniem z błędem podczas próby zainstalowania lub przywrócenia pakietu:

![NuGet generuje błąd, gdy dokładna wersja pakietu nie jest dostępna](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-versions"></a>Wersje pływające

Zmienna wersja zależności jest \* określona ze znakiem. Na przykład `6.0.*`. Ta specyfikacja wersji mówi "użyj najnowszej wersji 6.0.x"; `4.*` oznacza "użyj najnowszej wersji 4.x". Przy użyciu wersji przestawnej zmniejsza zmiany w pliku projektu, jednocześnie aktualizując z najnowszej wersji zależności.

Podczas korzystania z wersji przestawnej NuGet rozwiązuje najwyższą wersję pakietu, `6.0.*` który pasuje do wzorca wersji, na przykład pobiera najwyższą wersję pakietu, który rozpoczyna się od 6.0:

![Wybór wersji 6.0.1, gdy wymagana jest zmienna wersja 6.0.*](media/projectJson-dependency-4.png)

> [!Note]
> Aby uzyskać informacje na temat zachowania wersji przestawnych i wersji wstępnych, zobacz [Przechowywanie wersji pakietu](package-versioning.md#version-ranges).


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a>Najbliższe wygrane

Gdy wykres pakietu dla aplikacji zawiera różne wersje tego samego pakietu, NuGet wybiera pakiet, który jest najbliżej aplikacji na wykresie i ignoruje wszystkie inne. To zachowanie umożliwia aplikacji zastąpić dowolną wersję określonego pakietu na wykresie zależności.

W poniższym przykładzie aplikacja zależy bezpośrednio od pakietu B z ograniczeniem wersji >=2.0. Aplikacja zależy również od pakietu A, który z kolei zależy również od pakietu B, ale z ograniczeniem >= 1.0. Ponieważ zależność od pakietu B 2.0 jest bliżej aplikacji na wykresie, ta wersja jest używana:

![Aplikacja używająca reguły Najbliższe wygrane](media/projectJson-dependency-5.png)

>[!Warning]
> Reguła Najbliższe wins może spowodować obniżenie wersji pakietu, co może spowodować przerwanie innych zależności na wykresie. W związku z tym ta reguła jest stosowana z ostrzeżeniem, aby ostrzec użytkownika.

Ta reguła powoduje również większą wydajność z wykresu dużej zależności (takich jak te z pakietami BCL), ponieważ po zignorowaniu danej zależności NuGet ignoruje również wszystkie pozostałe zależności na tej gałęzi wykresu. Na poniższym diagramie, na przykład, ponieważ pakiet C 2.0 jest używany, NuGet ignoruje wszelkie gałęzie na wykresie, które odwołują się do starszej wersji pakietu C:

![Gdy NuGet ignoruje pakiet na wykresie, ignoruje całą gałąź](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a>Zależności kuzyna

Gdy różne wersje pakietu są określane w tej samej odległości na wykresie z aplikacji, NuGet używa najniższej wersji, która spełnia wszystkie wymagania dotyczące wersji (jak w [przypadku najniższej odpowiedniej wersji](#lowest-applicable-version) i [zmiennych reguł wersji).](#floating-versions) Na poniższej ilustracji, na przykład wersja 2.0 pakietu B spełnia pozostałe >= 1,0 ograniczenia i dlatego jest używana:

![Rozwiązywanie zależności kuzyna przy użyciu niższej wersji, która spełnia wszystkie ograniczenia](media/projectJson-dependency-7.png)

W niektórych przypadkach nie jest możliwe spełnienie wszystkich wymagań dotyczących wersji. Jak pokazano poniżej, jeśli pakiet A wymaga dokładnie pakiet B 1.0 i pakiet C wymaga pakietu B >= 2.0, a następnie NuGet nie może rozwiązać zależności i daje błąd.

![Nierozwiązywalne zależności z powodu dokładnego wymagania dotyczące wersji](media/projectJson-dependency-8.png)

W takich sytuacjach konsument najwyższego poziomu (aplikacja lub pakiet) należy dodać własną bezpośrednią zależność od pakietu B, tak aby obowiązuje [reguła Najbliższe umowy wins.](#nearest-wins)

## <a name="dependency-resolution-with-packagesconfig"></a>Rozpoznawanie zależności za pomocą pliku packages.config

Z `packages.config`, zależności projektu są zapisywane `packages.config` jako płaska lista. Wszelkie zależności tych pakietów są również zapisywane na tej samej liście. Po zainstalowaniu pakietów NuGet `.csproj` może `app.config`również `web.config`zmodyfikować plik, i inne pojedyncze pliki.

Z `packages.config`, NuGet próbuje rozwiązać konflikty zależności podczas instalacji każdego pojedynczego pakietu. Oznacza to, że jeśli pakiet A jest instalowany i zależy `packages.config` od pakietu B, a pakiet B jest już wymieniony jako zależność czegoś innego, NuGet porównuje wersje pakietu B żądane i próbuje znaleźć wersję, która spełnia wszystkie ograniczenia wersji. W szczególności NuGet wybiera niższą wersję *major.minor,* która spełnia zależności.

Domyślnie NuGet 2.8 szuka najniższej wersji poprawki (zobacz [NuGet 2.8 release notes](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)). To ustawienie można sterować za pomocą atrybutu `DependencyVersion` in i przełącznika `Nuget.Config` `-DependencyVersion` w wierszu polecenia.  

Proces `packages.config` rozwiązywania zależności komplikuje się dla większych wykresów zależności. Każda nowa instalacja pakietu wymaga przechodzenia przez cały wykres i zwiększa szansę na konflikty wersji. W przypadku wystąpienia konfliktu instalacja jest zatrzymywany, pozostawiając projekt w stanie nieokreślonym, szczególnie z potencjalnymi modyfikacjami samego pliku projektu. Nie jest to problem podczas korzystania z innych formatów zarządzania pakietami.

## <a name="managing-dependency-assets"></a>Zarządzanie zasobami zależności

Korzystając z formatu PackageReference, można kontrolować, które zasoby z zależności przepływu do projektu najwyższego poziomu. Aby uzyskać szczegółowe informacje, zobacz [PackageReference](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

Gdy projekt najwyższego poziomu jest sam pakiet, masz również kontrolę `include` `exclude` nad tym przepływem `.nuspec` przy użyciu i atrybuty z zależnościami wymienionych w pliku. Zobacz [.nuspec Reference - Zależności](../reference/nuspec.md#dependencies).

## <a name="excluding-references"></a>Z wyłączeniem odniesień

Istnieją scenariusze, w których zestawy o tej samej nazwie mogą być odwoływane więcej niż raz w projekcie, powodując błędy czasu projektowania i czasu kompilacji. Należy wziąć pod uwagę projekt, który zawiera niestandardową wersję `C.dll`programu , i odwołuje się do pakietu C, który również zawiera `C.dll`. Jednocześnie projekt zależy również od pakietu B, który również `C.dll`zależy od pakietu C i . W rezultacie NuGet nie można `C.dll` określić, którego do użycia, ale nie można po prostu usunąć zależności projektu na pakiet C, ponieważ pakiet B również zależy od niego.

Aby rozwiązać ten problem, należy `C.dll` bezpośrednio odwołać się do żądanego (lub użyć innego pakietu, który odwołuje się do właściwego), a następnie dodać zależność od pakietu C, który wyklucza wszystkie jego zasoby. Odbywa się to w następujący sposób w zależności od używanego formatu zarządzania pakietami:

- [PackageReference](../consume-packages/package-references-in-project-files.md): `ExcludeAssets="All"` dodaj w zależności:

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" ExcludeAssets="All" />
    ```

- `packages.config`: usuń odwołanie do PackageC z `.csproj` pliku, tak aby `C.dll` odwoływał się tylko do wersji, którą chcesz.
    
## <a name="dependency-updates-during-package-install"></a>Aktualizacje zależności podczas instalowania pakietu 

Jeśli wersja zależności jest już spełniona, zależność nie jest aktualizowana podczas innych instalacji pakietu. Rozważmy na przykład pakiet A, który zależy od pakietu B i określa 1.0 dla numeru wersji. Repozytorium źródłowe zawiera wersje 1.0, 1.1 i 1.2 pakietu B. Jeśli A jest zainstalowany w projekcie, który zawiera już B w wersji 1.0, a następnie B 1.0 pozostaje w użyciu, ponieważ spełnia ograniczenia wersji. Jednak jeśli pakiet A miał żądania w wersji 1.1 lub wyższej b, a następnie B 1.2 zostanie zainstalowany. 

## <a name="resolving-incompatible-package-errors"></a>Rozwiązywanie błędów niezgodnego pakietu

Podczas operacji przywracania pakietu może zostać wyświetlony błąd "Co najmniej jeden pakiet nie jest zgodny..." lub że pakiet "nie jest zgodny" z ramami docelowymi projektu.

Ten błąd występuje, gdy jeden lub więcej pakietów, do których odwołuje się w projekcie nie wskazują, że obsługują one platformę docelową projektu; oznacza to, że pakiet nie zawiera odpowiedniej `lib` biblioteki DLL w swoim folderze dla struktury docelowej, która jest zgodna z projektem. (Zobacz [struktury docelowe](../reference/target-frameworks.md) dla listy.) 

Na przykład jeśli obiekt `netstandard1.6` docelowy projektu i spróbujesz zainstalować pakiet `lib\net20` `\lib\net45` zawierający biblioteki DLL tylko w folderach i folderach, zobaczysz komunikaty podobne do następujących dla pakietu i ewentualnie jego utrzymaniu:

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

- Przekierować projekt do struktury, która jest obsługiwana przez pakiety, których chcesz użyć.
- Skontaktuj się z autorem pakietów i pracuj z nimi, aby dodać obsługę wybranej struktury. Każda strona z listą pakietów na [nuget.org](https://www.nuget.org/) ma w tym celu łącze **Skontaktuj się z właścicielami.**
