---
title: Rozwiązanie zależności pakietu NuGet
description: Szczegółowe informacje na temat procesu, za pomocą którego zależności pakietu NuGet są rozwiązywane i instalowane zarówno w pakiecie NuGet 2.x, jak i NuGet 3.x+.
author: JonDouglas
ms.author: jodou
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 69adbbad20debf2e53f247e85d638b3226c0491d
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323755"
---
# <a name="how-nuget-resolves-package-dependencies"></a>Jak pakiet NuGet rozwiązuje zależności pakietów

Za każdym razem, gdy pakiet jest instalowany lub [](../consume-packages/package-restore.md) ponownie instalowany, co obejmuje instalację w ramach procesu przywracania, pakiet NuGet instaluje również wszelkie dodatkowe pakiety, od których zależy pierwszy pakiet.

Te bezpośrednie zależności mogą również mieć zależności samodzielnie, co może nadal mieć dowolną głębokość. W ten sposób powstaje tzw. wykres *zależności* opisujący relacje między pakietami na wszystkich poziomach.

Jeśli wiele pakietów ma tę samą zależność, ten sam identyfikator pakietu może pojawić się na wykresie wiele razy, potencjalnie z różnymi ograniczeniami wersji. Jednak w projekcie można używać tylko jednej wersji danego pakietu, więc nuGet musi wybrać wersję, która jest używana. Dokładny proces zależy od używanego formatu zarządzania pakietami.

## <a name="dependency-resolution-with-packagereference"></a>Rozwiązanie zależności za pomocą packageReference

Podczas instalowania pakietów w projektach przy użyciu formatu PackageReference pakiet NuGet dodaje odwołania do płaskiego grafu pakietu w odpowiednim pliku i z wyprzedzeniem rozwiązuje konflikty. Ten proces jest określany jako przywracanie *przechodnie.* Ponowne instalowanie lub przywracanie pakietów to proces pobierania pakietów wymienionych na grafie, co spowoduje szybsze i bardziej przewidywalne kompilacje. Można również korzystać z wersji zmiennoprzecinkowych, takich jak 2.8. , aby uniknąć modyfikowania projektu w celu używania najnowszej \* wersji pakietu.

Gdy proces przywracania NuGet jest uruchamiany przed kompilacją, najpierw rozwiązuje zależności w pamięci, a następnie zapisuje wynikowy graf do pliku o nazwie `project.assets.json` . Ponadto zapisuje rozpoznane zależności w pliku blokady o nazwie , jeśli włączono funkcję `packages.lock.json` [pliku blokady](../consume-packages/package-references-in-project-files.md#locking-dependencies).
Plik assets znajduje się w folderze , który domyślnie jest `MSBuildProjectExtensionsPath` folderem "obj" projektu. Następnie program MSBuild odczytuje ten plik i tłumaczy go na zestaw folderów, w których można znaleźć potencjalne odwołania, a następnie dodaje je do drzewa projektów w pamięci.

Plik `project.assets.json` jest tymczasowy i nie powinien być dodawany do kontroli źródła. Jest ona domyślnie wymieniona zarówno w wartościach , `.gitignore` jak i `.tfignore` . Zobacz [Pakiety i kontrola źródła](../consume-packages/packages-and-source-control.md).

### <a name="dependency-resolution-rules"></a>Reguły rozwiązywania zależności

Przywracanie przechodnie stosuje cztery główne reguły rozwiązywania zależności: najniższą dostępną wersję, wersje zmiennoprzecincze, najbliższą wins i zależności zależność zależność zależności.

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a>Najniższa wersja, która ma zastosowanie

Najniższa obowiązująca reguła wersji przywraca najniższą możliwą wersję pakietu zdefiniowaną przez jego zależności. Dotyczy to również zależności aplikacji lub biblioteki klas, chyba że jest zadeklarowana jako [zmiennoprzecinkowa](#floating-versions).

Na przykład na poniższej ilustracji wersja 1.0-beta jest uznawana za niższą niż 1.0, więc nuGet wybiera wersję 1.0:

![Wybieranie najniższej odpowiedniej wersji](media/projectJson-dependency-1.png)

Na następnej ilustracji wersja 2.1 nie jest dostępna w kanale informacyjnym, ale ponieważ ograniczenie wersji to >= 2.1 NuGet wybiera następną najniższą możliwą wersję, w tym przypadku 2.2:

![Wybieranie następnej najniższej wersji dostępnej w kanale informacyjnym](media/projectJson-dependency-2.png)

Gdy aplikacja określa dokładny numer wersji, taki jak 1.2, który nie jest dostępny w kanale informacyjnym, program NuGet kończy się niepowodzeniem z błędem podczas próby zainstalowania lub przywrócenia pakietu:

![Program NuGet generuje błąd, gdy dokładna wersja pakietu jest niedostępny](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-versions"></a>Wersje zmiennoprzecinowe

Zmiennoprzecinkową wersję zależności określa się za pomocą \* znaku . Na przykład `6.0.*`. Ta specyfikacja wersji zawiera "użyj najnowszej wersji 6.0.x"; `4.*` oznacza "użyj najnowszej wersji 4.x". Użycie wersji zmiennej zmniejsza liczbę zmian w pliku projektu, jednocześnie zapewniając użycie zawsze najnowszej wersji zależności.

W przypadku korzystania z wersji zmiennoprzecinków NuGet rozpozna najwyższą wersję pakietu, która pasuje do wzorca wersji, na przykład pobiera najwyższą wersję pakietu, która rozpoczyna się od `6.0.*` wersji 6.0:

![Wybieranie wersji 6.0.1, gdy żądana jest zmiennoprzecinkowa wersja 6.0.*](media/projectJson-dependency-4.png)

> [!Note]
> Aby uzyskać informacje na temat zachowania wersji zmiennoprzecinkowych i wersji wstępnych, zobacz [Package versioning (Wersjowanie pakietów).](package-versioning.md#version-ranges)


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a>Najbliższa wins

Gdy wykres pakietu dla aplikacji zawiera różne wersje tego samego pakietu, nuGet wybiera pakiet, który znajduje się najbliżej aplikacji na wykresie, i ignoruje wszystkie inne. To zachowanie umożliwia aplikacji zastąpienie dowolnej konkretnej wersji pakietu na wykresie zależności.

W poniższym przykładzie aplikacja zależy bezpośrednio od pakietu B z ograniczeniem wersji >=2.0. Aplikacja zależy również od pakietu A, który z kolei zależy również od pakietu B, ale z >=1.0. Ponieważ zależność od pakietu B 2.0 jest bliżej aplikacji na wykresie, używana jest ta wersja:

![Aplikacja używająca reguły najbliższego wins](media/projectJson-dependency-5.png)

>[!Warning]
> Reguła Najbliższe wins może spowodować obniżenie wersji pakietu, co może potencjalnie spowodować przerwanie innych zależności na wykresie. W związku z tym ta reguła jest stosowana z ostrzeżeniem ostrzegawczym użytkownika.

Ta reguła powoduje również zwiększenie wydajności przy użyciu dużego grafu zależności (na przykład tych z pakietami BCL), ponieważ po zignorowania danej zależności nuGet ignoruje również wszystkie pozostałe zależności w tej gałęzi grafu. Na przykład na poniższym diagramie, ponieważ jest używany pakiet C 2.0, nuGet ignoruje wszystkie gałęzie grafu odwołujące się do starszej wersji pakietu C:

![Gdy program NuGet ignoruje pakiet w grafie, ignoruje tę całą gałąź](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a>Zależności z 2018 r.

Gdy różne wersje pakietów są określane w tej samej odległości na grafie od aplikacji, program NuGet [](#lowest-applicable-version) używa najniższej wersji, która spełnia wszystkie wymagania dotyczące wersji (tak jak w przypadku reguł o najniższej obowiązującej wersji i wersjach zmiennoprzecinków). [](#floating-versions) Na przykład na poniższej ilustracji wersja 2.0 pakietu B spełnia inne ograniczenie >=1.0 i dlatego jest używana:

![Rozwiązywanie zależności zależności przy użyciu niższej wersji, która spełnia wszystkie ograniczenia](media/projectJson-dependency-7.png)

W niektórych przypadkach nie jest możliwe spełnienie wszystkich wymagań dotyczących wersji. Jak pokazano poniżej, jeśli pakiet A wymaga dokładnie pakietu B 1.0, a pakiet C wymaga pakietu B >=2.0, wówczas nuGet nie może rozpoznać zależności i wyświetla błąd.

![Nierozpoznane zależności ze względu na dokładne wymaganie dotyczące wersji](media/projectJson-dependency-8.png)

W takich sytuacjach konsument najwyższego poziomu (aplikacja lub pakiet) powinien dodać własną bezpośrednią [](#nearest-wins) zależność od pakietu B, aby miała zastosowanie reguła Najbliższe wins.

## <a name="dependency-resolution-with-packagesconfig"></a>Rozwiązanie zależności za pomocą packages.config

W przypadku programu zależności projektu są zapisywane w `packages.config` `packages.config` programie jako płaska lista. Wszelkie zależności tych pakietów są również zapisywane na tej samej liście. Po zainstalowaniu pakietów pakiet NuGet może również modyfikować `.csproj` plik , i inne pojedyncze `app.config` `web.config` pliki.

W `packages.config` programie nuGet próbuje rozwiązać konflikty zależności podczas instalacji poszczególnych pakietów. Oznacza to, że jeśli pakiet A jest instalowany i zależy od pakietu B, a pakiet B jest już wymieniony jako zależność innego pakietu, NuGet porównuje żądane wersje pakietu B i próbuje znaleźć wersję, która spełnia wszystkie ograniczenia `packages.config` wersji. W szczególności nuGet wybiera niższą *wersję główną.pomocniczą,* która spełnia zależności.

Domyślnie program NuGet 2.8 szuka najniższej wersji poprawki (zobacz Informacje o wersji [nuGet 2.8).](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies) To ustawienie można kontrolować za pomocą `DependencyVersion` atrybutu w pliku `NuGet.Config` i `-DependencyVersion` przełącznika w wierszu polecenia.  

Proces `packages.config` rozwiązywania zależności jest skomplikowany w przypadku większych grafów zależności. Każda nowa instalacja pakietu wymaga przechodzenia całego grafu i zwiększa prawdopodobieństwo konfliktów wersji. Gdy wystąpi konflikt, instalacja jest zatrzymywana, pozostawiając projekt w stanie nieokreślonym, szczególnie w przypadku potencjalnych modyfikacji samego pliku projektu. Nie jest to problem w przypadku korzystania z innych formatów zarządzania pakietami.

## <a name="managing-dependency-assets"></a>Zarządzanie zasobami zależności

W przypadku korzystania z formatu PackageReference można kontrolować, które zasoby z zależności przepływają do projektu najwyższego poziomu. Aby uzyskać szczegółowe informacje, zobacz [PackageReference](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

Gdy projekt najwyższego poziomu jest samym pakietem, masz również kontrolę nad tym przepływem przy użyciu atrybutów i z zależnościami wymienionymi `include` `exclude` w pliku `.nuspec` . Zobacz [.nuspec Reference - Dependencies (Odwołanie do nuspec — zależności).](../reference/nuspec.md#dependencies)

## <a name="excluding-references"></a>Wykluczanie odwołań

Istnieją scenariusze, w których zestawy o tej samej nazwie mogą być przywołyowane w projekcie więcej niż raz, co tworzy błędy czasu projektowania i kompilacji. Rozważmy projekt, który zawiera niestandardową wersję i odwołuje `C.dll` się do pakietu C, który również zawiera . `C.dll` W tym samym czasie projekt zależy również od pakietu B, który zależy również od pakietu C i `C.dll` . W związku z tym nuGet nie może określić, którego pakietu użyć, ale nie można po prostu usunąć zależności projektu od pakietu C, ponieważ pakiet B również od niego `C.dll` zależy.

Aby rozwiązać ten problem, należy bezpośrednio odwoływać się do odpowiedniego pakietu (lub użyć innego pakietu, który odwołuje się do odpowiedniego pakietu), a następnie dodać zależność od pakietu C, która wyklucza wszystkie jego `C.dll` zasoby. Odbywa się to w następujący sposób w zależności od formatu zarządzania pakietami w użyciu:

- [PackageReference](../consume-packages/package-references-in-project-files.md): `ExcludeAssets="All"` dodaj w zależności:

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" ExcludeAssets="All" />
    ```

- `packages.config`: usuń z pliku odwołanie do packagec, aby odwołyło `.csproj` się tylko do `C.dll` wersji, której potrzebujesz.
    
## <a name="dependency-updates-during-package-install"></a>Aktualizacje zależności podczas instalowania pakietu 

Jeśli wersja zależności jest już spełniona, zależność nie jest aktualizowana podczas innych instalacji pakietów. Rozważmy na przykład pakiet A, który zależy od pakietu B i określa 1.0 jako numer wersji. Repozytorium źródłowe zawiera wersje 1.0, 1.1 i 1.2 pakietu B. Jeśli A jest zainstalowany w projekcie, który zawiera już wersję B 1.0, wersja B 1.0 pozostaje w użyciu, ponieważ spełnia ograniczenie wersji. Jeśli jednak pakiet A zawierał żądania w wersji 1.1 lub wyższej od wersji B, zostanie zainstalowana wersja B 1.2. 

## <a name="resolving-incompatible-package-errors"></a>Rozwiązywanie problemów z niezgodnymi pakietami

Podczas operacji przywracania pakietu może zostać wyświetlony błąd "Co najmniej jeden pakiet nie jest zgodny..." lub że pakiet "nie jest zgodny" z platformą docelową projektu.

Ten błąd występuje, gdy co najmniej jeden pakiet przywołyowany w projekcie nie wskazuje, że obsługuje platformę docelową projektu; oznacza to, że pakiet nie zawiera odpowiedniej biblioteki DLL w folderze dla docelowej `lib` struktury, która jest zgodna z projektem. (Aby uzyskać [listę,](../reference/target-frameworks.md) zobacz Platforme docelowe). 

Jeśli na przykład projekt jest przeznaczony i próbujesz zainstalować pakiet zawierający biblioteki DLL tylko w folderach i , zobaczysz komunikaty podobne do następujących dla pakietu i prawdopodobnie `netstandard1.6` `lib\net20` jego `\lib\net45` zależności:

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

Aby rozwiązać problemy z niezgodnościami, wykonaj jedną z następujących czynności:

- Przekieruj projekt do struktury, która jest obsługiwana przez pakiety, których chcesz użyć.
- Skontaktuj się z autorem pakietów i skontaktuj się z nimi, aby dodać obsługę wybranej struktury. Każda strona listy pakietów w [nuget.org](https://www.nuget.org/) ma **w** tym celu link Kontakt z właścicielami.
