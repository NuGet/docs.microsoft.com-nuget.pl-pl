---
title: "Rozpoznawanie zależności pakietu NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 1d530a72-3486-4a0d-b6fb-017524616f91
description: "Szczegółowe informacje na temat procesu za pomocą którego rozwiązany i zainstalowane w obu NuGet zależności pakietu NuGet 2.x i NuGet 3.x+."
keywords: "Zależności pakietów NuGet, przechowywanie wersji NuGet, wersje zależności, wykres wersji, rozdzielczość wersji, przechodnie przywracania"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 251ae6944cc0010f596c9b3daf95c318595a5c4d
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/05/2018
---
# <a name="how-nuget-resolves-package-dependencies"></a>Jak NuGet jest rozpoznawany jako zależności pakietów

Dowolnej chwili pakiet jest zainstalowany lub ponownej instalacji, w tym instalowane jako część [przywrócić](../consume-packages/package-restore.md) procesu NuGet instaluje wszystkie dodatkowe pakiety, od których zależy ten pierwszy pakietu.

Te zależności natychmiastowego następnie również zainstalować zależności na ich własnych, które mogą w dalszym dowolnego głębokość. Daje to tak zwany *wykresu zależności* , który opisuje relacje między pakietami są wszystkie poziomy.

Jeśli tego samego zależności wielu pakietów, następnie ten sam identyfikator pakietu może występować na wykresie wiele razy potencjalnie z ograniczeniami innej wersji. Jednak tylko jedna wersja danego pakietu może służyć w projekcie, dlatego należy wybrać NuGet, która wersja jest można użyć. Dokładne proces zależy od używany format odwołanie do pakietu.

W tym temacie:
- [Rozpoznawanie zależności z PackageReference i project.json](#dependency-resolution-with-packagereference-and-projectjson)
- [Rozpoznawanie zależności z pliku packages.config](#dependency-resolution-with-packagesconfig)
- [Z wyjątkiem odwołania](#excluding-references), jest to konieczne, jeśli występuje konflikt między zależność określonych w jednym projekcie i zestawu, który jest tworzony przez inny.
- [Instalowanie aktualizacji zależności w pakiecie](#dependency-updates-during-package-install)
- [Rozwiązywanie błędów niezgodne pakietu](#resolving-incompatible-package-errors)

## <a name="dependency-resolution-with-packagereference-and-projectjson"></a>Rozpoznawanie zależności z PackageReference i project.json

Podczas instalowania pakietów do projektów przy użyciu PackageReference lub `project.json` formatów, NuGet dodaje odwołania do wykres prostych pakietu odpowiedniego pliku i pozwala rozwiązać konflikty wcześniejsze. Ten proces jest nazywany *przechodnie przywracania*. Ponowne zainstalowanie lub przywracanie pakietów następnie jest procesem pobierania pakietów wymienionych na wykresie, co powoduje szybsze i bardziej przewidywalne kompilacji. Można również wykorzystać (przestawne) wersji symboli wieloznacznych, takich jak 2.8. \*, unikając kosztowne i błąd wywołania podatne `nuget update` na komputerach klienckich i serwerach kompilacji.

Po uruchomieniu procesu przywracania NuGet przed kompilacji go najpierw rozpoznaje zależności w pamięci, a następnie zapisuje wynikowego wykresu w pliku o nazwie `project.assets.json` w `obj` folderu projektu przy użyciu PackageReference lub w pliku o nazwie `project.lock.json` obok `project.json`. Następnie MSBuild odczytuje ten plik i przekształca ją w zestawie folderów, gdzie można znaleźć potencjalnych odwołania, a następnie dodanie ich do drzewa projektu w pamięci.

Plik blokady jest tymczasowe i nie powinno być dodane do kontroli źródła. Ta opcja jest wyświetlana domyślnie zarówno `.gitignore` i `.tfignore`. Zobacz [pakietów i kontroli źródła](Packages-and-Source-Control.md).

### <a name="dependency-resolution-rules"></a>Zasady rozpoznawania zależności

Przywracanie przechodnie stosuje cztery główne zasady można rozpoznać zależności: najniższa odpowiedniej wersji, wersje przestawne najbliższej wins i cousin zależności.

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a>Najniższa wersja dotyczy

Najniższa reguła dotyczy wersji przywraca Najniższa wersja możliwe pakietu zgodnie z jego zależności. Ma również zastosowanie do zależności w bibliotece klas programu lub aplikacji, chyba że zadeklarowany jako [przestawne](#floating-versions).

Na poniższej ilustracji na przykład 1.0 beta jest uznawane za niższa niż 1.0, wybierze NuGet w wersji 1.0:

![Wybieranie Najniższa wersja dotyczy](media/projectJson-dependency-1.png)

W następnej ilustracji wersji 2.1 nie jest dostępne w źródle danych, ale ponieważ jest ograniczenie wersji > = Dalej Najniższa wersja, można go znaleźć, w tym przypadku 2.2 2.1 pobrania NuGet:

![Wybór następnego Najniższa wersja dostępne w źródle danych](media/projectJson-dependency-2.png)

Aplikacja określa numer wersji dokładne, takie jak 1.2, który nie jest dostępne w źródle danych, NuGet nie powiedzie się z powodu błędu podczas próby zainstalowania lub przywracanie pakietu:

![NuGet generuje błąd, gdy nie będzie dostępna wersja pakietu dokładnego](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-wildcard-versions"></a>Liczby zmiennoprzecinkowe (symbol wieloznaczny) wersji

Wersja zależności zmiennoprzecinkową lub symbol wieloznaczny jest określany za pomocą \* symbolu wieloznacznego w wersji 6.0.\*. Ta wersja specyfikacji mówi, "Korzystanie z najnowszej wersji 6.0.x;" 4.\* oznacza "używać najnowszej wersji 4.x." Przy użyciu symboli wieloznacznych umożliwia pakiet zależności, aby kontynuować, zmieniające się bez konieczności zmiany aplikacja odbierająca komunikaty (lub pakietu).

Korzystając z symbolem wieloznacznym, NuGet rozpoznaje najwyższa wersja pakietu, która odpowiada wzorcowi wersji, na przykład w wersji 6.0. \* pobiera najwyższa wersja pakietu, który rozpoczyna się od 6.0:

![Wybieranie wersji 6.0.1 podczas przestawne w wersji 6.0. * jest wymagane](media/projectJson-dependency-4.png)

> [!Note]
> Aby uzyskać informacje na zachowanie symboli wieloznacznych i wersje wstępne, zobacz [wersji pakietu](../reference/package-versioning.md#version-ranges-and-wildcards).


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a>Najbliższej wins

Gdy wykres pakietu dla aplikacji zawiera różne wersje tego samego pakietu, NuGet wybiera pakiet, który jest najbardziej zbliżony do aplikacji na wykresie i ignoruje wszystkie pozostałe. To zachowanie umożliwia zastąpienie dowolnej wersji pakietu z określonego na wykresie zależności aplikacji.

W poniższym przykładzie jest zależna aplikacja, bezpośrednio na B pakietu z ograniczenie wersji > = 2.0. Aplikacja zależy również od pakietu A, który z kolei również zależy od pakietu B, ale z > = 1.0 ograniczenia. Zależność od pakietu B 2.0 jest względem aplikacji na wykresie, zostanie użyta ta wersja:

![Aplikacji przy użyciu reguły najbliższej Wins](media/projectJson-dependency-5.png)

>[!Warning]
> Reguła najbliższej Wins może spowodować obniżenie wersji pakietu, w związku z tym potencjalnie fundamentalne innych zależności na wykresie. Dlatego ta reguła jest stosowana z ostrzeżeniem, aby ostrzec użytkownika.

Ta zasada powoduje również w większą wydajność o na wykresie zależności duże (takich jak z pakietami BCL) ponieważ po danym zależności jest ignorowana, NuGet również ignoruje wszystkie pozostałe zależności w oddziale wykresu. Na poniższym diagramie na przykład, ponieważ pakiet C 2.0 jest używana, NuGet ignoruje odgałęzień na wykresie, które odwołują się do starszej wersji pakietu c:

![NuGet ignoruje pakietu na wykresie, ignoruje całą gałąź](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a>Cousin zależności

W przypadku pakietu różne wersje są określane w tej samej odległości na wykresie z aplikacji, NuGet korzysta z Najniższa wersja, która spełnia wszystkie wymagania dotyczące wersji (jak [Najniższa wersja dotyczy](#lowest-applicable-version) i [ liczby zmiennoprzecinkowe wersji](#floating-versions) zasady). Na poniższej ilustracji, na przykład w wersji 2.0 z pakietu B spełnia innych > = 1.0 ograniczenia i jest używany w związku z tym:

![Rozpoznawanie zależności cousin przy użyciu starszej wersji, która spełnia wszystkie ograniczenia](media/projectJson-dependency-7.png)

W niektórych przypadkach nie jest możliwe spełnia wszystkie wymagania dotyczące wersji. Jak pokazano poniżej, jeśli pakiet A wymaga dokładnie pakietu B 1.0, a pakiet C pakietu B > = 2.0, a następnie NuGet nie można rozpoznać zależności i zwraca błąd.

![Nierozpoznane zależności ze względu na to wymaganie dotyczące dokładnej wersji](media/projectJson-dependency-8.png)

W takich przypadkach najwyższego poziomu konsumenta (aplikacją lub pakietem) należy dodać bezpośrednie zależności pakietu B, aby [najbliższej Wins](#nearest-wins) reguła ma zastosowanie.

## <a name="dependency-resolution-with-packagesconfig"></a>Rozpoznawanie zależności z pliku packages.config

Z `packages.config`, zależności projektu są zapisywane w `packages.config` jako płaska lista. Wszystkie zależności są pakiety również są zapisywane w tej samej listy. Po zainstalowaniu pakietów NuGet może także modyfikować `.csproj` pliku `app.config`, `web.config`i inne poszczególnych plików.

Z `packages.config`, próbuje rozwiązywania konfliktów zależności podczas instalacji każdego poszczególnych pakietu NuGet. Oznacza to, że jeśli pakiet A jest instalowany i jest zależna od pakietu B i B pakietu jest już na liście `packages.config` jako zależność z innego elementu NuGet porównuje wersje pakietu B żądanej i próbuje odnaleźć wersji, która spełnia wszystkie wersji ograniczenia. W szczególności NuGet wybierze niższą *major.minor* wersji, która spełnia zależności.

Domyślnie NuGet 2.7 i starszych jest rozpoznawana jako najwyższe *poprawki* wersji (za pomocą *major.minor.patch.build* Konwencji). [NuGet 2,8 i wyższych](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies) zmienia to zachowanie, aby wyszukać Najniższa wersja poprawki domyślnie. Można kontrolować, to ustawienie za pomocą `DependencyVersion` atrybutu w `Nuget.Config` i `-DependencyVersion` przełącznik w wierszu polecenia.  

`packages.config` Przetworzyć dla rozpoznawania zależności pobiera skomplikowane dla większych wykresy zależności. Każda nowa instalacja pakietu wymaga przechodzenie całego grafu i zwiększa prawdopodobieństwo wystąpienia konfliktów wersji. Gdy wystąpi konflikt, instalacja zostanie zatrzymana, pozostawiając projektu w stanie nieokreślonym, szczególnie w przypadku potencjalnych zmiany w samym pliku projektu. To nie jest problem, korzystając z innych formatów odwołanie do pakietu.


## <a name="managing-dependency-assets"></a>Zarządzanie zasobami zależności

Korzystając z `project.json` lub PackageReference formatów, można kontrolować, które zasoby z przepływu zależności w projekcie najwyższego poziomu. Aby uzyskać więcej informacji, zobacz [project.json](../Schema/project-json.md) i [pakietu odwołań w plikach projektu](Package-References-in-Project-Files.md#controlling-dependency-assets).

Gdy najwyższego poziomu projektu jest pakietem, również mają kontrolę nad tym przepływu za pomocą `include` i `exclude` atrybutów na liście zależności `.nuspec` pliku. Zobacz [.nuspec — odwołanie do zależności](../Schema/nuspec.md#dependencies).

## <a name="excluding-references"></a>Z wyjątkiem odwołania

Istnieją scenariusze, w których zestawów o tej samej nazwie może być więcej niż jedno odwołanie w projekcie zwracające błędy czasu projektowania i czas kompilacji. Należy wziąć pod uwagę projekt, który zawiera niestandardową wersję `C.dll`i odwołuje się C pakietu, który zawiera także `C.dll`. W tym samym czasie, projekt zależy również od B pakietu, który również jest zależny od pakietu C i `C.dll`. W związku z tym NuGet nie może określić, które `C.dll` do użycia, ale po prostu nie można usunąć zależności projektu C pakietu, ponieważ pakiet B również zależy od niego.

Aby rozwiązać ten problem, należy bezpośrednio odwoływać `C.dll` mają (lub użyj innego pakietu, który odwołuje się do właściwego), a następnie dodać zależność C pakietu, który wyklucza wszystkie jego zasoby. W zależności od formatu używanego odwołanie do pakietu odbywa się w następujący sposób:

- [PackageReference](../consume-packages/package-references-in-project-files.md): Dodaj `Exclude="All"` w zależności:

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" Exclude="All" />
    ```

- `packages.config`: Usuń odwołanie do PackageC z `.csproj` plików w celu odwołuje się tylko wersję `C.dll` żądany.
    
- `project.json`: Dodaj `"exclude" : "all"` w zależność PackageC:

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="dependency-updates-during-package-install"></a>Instalowanie aktualizacji zależności w pakiecie 

Nuget 2.4.x i wcześniej, po zainstalowaniu pakietu zależności, których już istnieje w projekcie zależności zostanie zaktualizowana do najnowszej wersji spełniającego ograniczenia wersji, nawet jeśli istniejąca wersja także spełnia te ograniczenia. 

Rozważmy na przykład pakiet A jest zależny od pakietu B, który określa 1.0 numeru wersji. Repozytorium źródłowe zawiera zarówno wersji 1.0, 1.1 i 1.2 pakietu B. Jeśli A jest zainstalowany w projekcie, która zawiera już B w wersji 1.0, B zostało zaktualizowane do wersji 1.2. 

Z NuGet 2.5 i później Jeśli spełniony jest już wersję zależności, zależność nie zostały zaktualizowane podczas inne instalacje pakietu. 

W tym samym przykładzie powyżej instalowania pakietu, który A do projektu z NuGet 2.5 i nowsze pozostawia pakiet B 1.0 w projekcie, ponieważ już spełnia ograniczenie wersji. Jednak jeśli pakietu A były żądania w wersji 1.1 lub nowszej b, następnie B 1.2 będzie zainstalowany. 

## <a name="resolving-incompatible-package-errors"></a>Rozwiązywanie błędów niezgodne pakietu

Podczas pakietu operację przywracania, może zostać wyświetlony błąd "co najmniej jednego pakietu nie są zgodne..." lub pakietu "nie jest zgodny" z platformy docelowej projektu.

Ten błąd występuje, gdy jeden lub więcej pakietów, do którego odwołuje się projekt nie wskazują obsługują platformy docelowej projektu; oznacza to, że pakiet nie zawiera odpowiedniej biblioteki DLL w jego `lib` folderu dla struktury docelowej, która jest zgodna z projektem. (Zobacz [platform docelowych](../Schema/Target-Frameworks.md) listę.) 

Na przykład, jeśli projekt przeznaczony `netstandard1.6` i spróbujesz zainstalować pakiet, który zawiera pliki DLL tylko `lib\net20` i `\lib\net45` foldery, możesz wyświetlone komunikaty podobnie do następującej dla pakietu i jego zależności:

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

- Przekieruj z projektem, aby platforma, która jest obsługiwana przez pakiety, które chcesz użyć.
- Skontaktuj się z autorem pakietów i pracować z nimi, aby dodać obsługę z wybranym framework. Każdy pakiet wyświetlania strony na [nuget.org](https://www.nuget.org/) ma **właścicieli skontaktuj się z** łącza do tego celu.
- **Nie zaleca się**: jako rozwiązanie tymczasowe podczas pracy z autorem pakietu, projektów przeznaczonych dla `netcore`, `netstandard`, i `netcoreapp` są oznaczane innych platform, jako niezgodna, umożliwiając pakietów przeznaczonych dla tych innych platform, które mają być używane. Zobacz [importuje project.json](../Schema/project-json.md#imports) i [docelowy programu MSBuild przywracania PackageTargetFallback](../Schema/msbuild-targets.md#packagetargetfallback). Może to spowodować nieoczekiwane wyniki, więc ponownie najlepiej rozwiązać niezgodności pakietu przy pracy z autorem pakietu podczas aktualizacji.
