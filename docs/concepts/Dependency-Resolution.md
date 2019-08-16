---
title: Rozpoznawanie zależności pakietu NuGet
description: Szczegółowe informacje na temat procesu, za pomocą którego zależności pakietu NuGet są rozwiązywane i instalowane zarówno w programie NuGet 2. x, jak i NuGet 3. x +.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 8bd1d473a69d769f3d9204188f3130578af78797
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/15/2019
ms.locfileid: "69520580"
---
# <a name="how-nuget-resolves-package-dependencies"></a>Jak narzędzie NuGet rozpoznaje zależności pakietów

Za każdym razem, gdy pakiet zostanie zainstalowany lub ponownie zainstalowany, który obejmuje instalację w ramach procesu [przywracania](../consume-packages/package-restore.md) , program NuGet zainstaluje także wszystkie dodatkowe pakiety, od których zależy pierwszy pakiet.

Te bezpośrednie zależności mogą również mieć własne zależności, które mogą przejść do dowolnej głębokości. Powoduje to utworzenie *grafu zależności* opisującego relacje między pakietami na wszystkich poziomach.

Gdy wiele pakietów ma tę samą zależność, ten sam identyfikator pakietu może być wyświetlany na wykresie wiele razy, potencjalnie z innymi ograniczeniami wersji. Jednak w projekcie można używać tylko jednej wersji danego pakietu, więc pakiet NuGet musi wybrać używaną wersję. Dokładny proces zależy od używanego formatu zarządzania pakietami.

## <a name="dependency-resolution-with-packagereference"></a>Rozpoznawanie zależności z PackageReference

W przypadku instalowania pakietów do projektów przy użyciu formatu PackageReference, NuGet dodaje odwołania do wykresu prostego pakietu w odpowiednim pliku i rozwiązuje konflikty przed czasem. Ten proces jest nazywany przywracaniem *przechodnim*. Ponowne instalowanie lub przywracanie pakietów jest procesem pobierania pakietów wymienionych na grafie, co powoduje szybsze i bardziej przewidywalne kompilacje. Możesz również korzystać z symboli wieloznacznych (zmiennoprzecinkowych), takich jak 2,8. Unikanie kosztownych i podatnych na błędy `nuget update` wywołań na komputerach klienckich i serwerach kompilacji. \*

Gdy proces przywracania NuGet zostanie uruchomiony przed kompilacją, rozpoznaje zależności jako pierwsze w pamięci, a następnie zapisuje wykres wyjściowy do pliku o nazwie `project.assets.json`. Zapisuje także rozwiązane zależności do pliku blokady o nazwie `packages.lock.json`, jeśli [jest włączona funkcja blokowania plików](https://docs.microsoft.com/en-us/nuget/consume-packages/package-references-in-project-files#locking-dependencies).
Plik zasobów znajduje się w lokalizacji `MSBuildProjectExtensionsPath`, która domyślnie jest folderem "obj" projektu. Program MSBuild odczytuje następnie ten plik i tłumaczy go na zestaw folderów, w których można znaleźć potencjalne odwołania, a następnie dodaje je do drzewa projektu w pamięci.

`project.assets.json` Plik jest tymczasowy i nie należy go dodawać do kontroli źródła. Jest on wyświetlany domyślnie w obu `.gitignore` i. `.tfignore` Zobacz [pakiety i kontrola źródła](../consume-packages/packages-and-source-control.md).

### <a name="dependency-resolution-rules"></a>Reguły rozpoznawania zależności

Przywracanie przechodnie stosuje cztery główne reguły do rozwiązywania zależności: najniższa odpowiednia wersja, liczba zmiennoprzecinkowa, najbliższy serwer WINS i zależności Cousin.

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a>Najniższa odpowiednia wersja

Najniższa odpowiednia reguła wersji przywraca najmniejszą możliwą wersję pakietu określoną przez jego zależności. Dotyczy to również zależności aplikacji lub biblioteki klas, chyba że jest zadeklarowana jako [zmienna](#floating-versions).

Na poniższej ilustracji na przykład 1,0-beta jest uważana za mniej niż 1,0, więc pakiet NuGet wybiera wersję 1,0:

![Wybieranie najniższej odpowiedniej wersji](media/projectJson-dependency-1.png)

Na następnym rysunku wersja 2,1 nie jest dostępna w kanale informacyjnym, ale ponieważ ograniczenie wersji jest > = 2,1 pakiet NuGet wybiera następną najniższą wersję, którą może znaleźć w tym przypadku 2,2:

![Wybieranie następnej najniższej wersji dostępnej w kanale informacyjnym](media/projectJson-dependency-2.png)

Gdy aplikacja określa dokładny numer wersji, na przykład 1,2, który nie jest dostępny w kanale informacyjnym, pakiet NuGet kończy się niepowodzeniem z powodu błędu podczas próby zainstalowania lub przywrócenia pakietu:

![Pakiet NuGet generuje błąd w przypadku niedostępności dokładnej wersji pakietu](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-wildcard-versions"></a>Wersje zmiennoprzecinkowe (symbol wieloznaczny)

Do \* symbolu wieloznacznego jest określana wersja zależności zmiennoprzecinkowa lub z symbolem\*wieloznacznym, podobnie jak w przypadku 6,0. W tej specyfikacji wersji znajduje się komunikat "Użyj najnowszej wersji programu 6.0. x"; 4.\* oznacza "Użyj najnowszej wersji 4. x". Użycie symbolu wieloznacznego pozwala pakietowi zależności kontynuować rozwijanie bez konieczności wprowadzania zmian w aplikacji zużywanej przez program (lub pakiet).

W przypadku korzystania z symbolu wieloznacznego NuGet rozpoznaje najwyższą wersję pakietu, która pasuje do wzorca wersji, na przykład 6,0. \* pobiera najwyższą wersję pakietu rozpoczynającą się od 6,0:

![Wybieranie wersji 6.0.1 w przypadku żądania zmiennoprzecinkowej wersji 6,0. *](media/projectJson-dependency-4.png)

> [!Note]
> Aby uzyskać informacje o zachowaniu symboli wieloznacznych i wersjach wstępnych, zobacz [wersja pakietu](package-versioning.md#version-ranges-and-wildcards).


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a>Najbliższy serwer WINS

Gdy Graf pakietu dla aplikacji zawiera różne wersje tego samego pakietu, NuGet wybiera pakiet, który znajduje się najbliżej aplikacji na grafie i ignoruje wszystkie pozostałe. Takie zachowanie umożliwia aplikacji przesłonięcie dowolnej konkretnej wersji pakietu na wykresie zależności.

W poniższym przykładzie aplikacja zależy bezpośrednio od pakietu B z ograniczeniem wersji > = 2.0. Aplikacja zależy również od pakietu, który z kolei zależy również od pakietu B, ale z ograniczeniem > = 1.0. Ponieważ zależność od pakietu B 2,0 jest bliska aplikacji na grafie, używana jest ta wersja:

![Aplikacja przy użyciu najbliższej reguły WINS](media/projectJson-dependency-5.png)

>[!Warning]
> Najbliższa reguła WINS może spowodować obniżenie wersji pakietu, co może spowodować zakłócenie innych zależności w grafie. W związku z tym ta reguła jest stosowana z ostrzeżeniem dotyczącym alertu użytkownika.

Ta zasada powoduje również zwiększenie wydajności przy użyciu wykresu z dużą zależnością (na przykład z pakietami BCL), ponieważ po zignorowaniu danej zależności, NuGet ignoruje także wszystkie pozostałe zależności z tej gałęzi wykresu. Na poniższym diagramie, na przykład, ponieważ używany jest pakiet C 2,0, NuGet ignoruje wszystkie gałęzie na grafie odwołujące się do starszej wersji pakietu C:

![Gdy NuGet zignoruje pakiet na grafie, ignoruje całą gałąź](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a>Cousin zależności

Gdy różne wersje pakietów są określone w tej samej odległości na wykresie z aplikacji, pakiet NuGet używa najniższej wersji, która spełnia wszystkie wymagania dotyczące wersji (tak jak w przypadku najniższych [odpowiednich wersji](#lowest-applicable-version) i reguł [wersji zmiennoprzecinkowych](#floating-versions) ). Na przykład na poniższym obrazie wersja 2,0 pakietu B spełnia pozostałe ograniczenia > = 1.0 i jest w ten sposób używana:

![Rozpoznawanie zależności Cousin przy użyciu niższej wersji, która spełnia wszystkie ograniczenia](media/projectJson-dependency-7.png)

W niektórych przypadkach nie jest możliwe spełnienie wszystkich wymagań dotyczących wersji. Jak pokazano poniżej, jeśli pakiet A wymaga dokładnie pakietu B 1,0, a pakiet C wymaga pakietu B > = 2.0, program NuGet nie może rozpoznać zależności i nadaje błędu.

![Nierozpoznawalne zależności z powodu dokładnego wymagania wersji](media/projectJson-dependency-8.png)

W takich sytuacjach konsument najwyższego poziomu (aplikacja lub pakiet) powinien dodać własną bezpośrednią zależność od pakietu B w celu zastosowania najbliższej reguły [usługi WINS](#nearest-wins) .

## <a name="dependency-resolution-with-packagesconfig"></a>Rozpoznawanie zależności z pakietem. config

W `packages.config`programie zależności projektu są `packages.config` zapisywane jako płaska lista. Wszystkie zależności tych pakietów są również zapisywane na tej samej liście. Po zainstalowaniu pakietów NuGet może także zmodyfikować `.csproj` plik `web.config`, `app.config`, i inne poszczególne pliki.

W `packages.config`programie NuGet próbuje rozwiązać konflikty zależności podczas instalacji poszczególnych pakietów. Oznacza to, że jeśli pakiet a jest instalowany i zależy od pakietu b, a pakiet b jest już wymieniony w `packages.config` zależności od czegoś innego, NuGet porównuje wersje żądanego pakietu b i próbuje znaleźć wersję, która spełnia wymagania dotyczące całej wersji powiązanych. Pakiet NuGet wybiera niższą wersję *główną. pomocniczą* , która spełnia zależności.

Domyślnie program NuGet 2,8 szuka najniższej wersji poprawki (zobacz [Informacje o wersji programu nuget 2,8](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)). To ustawienie można kontrolować za pomocą `DependencyVersion` atrybutu w `Nuget.Config` i `-DependencyVersion` przełącznika w wierszu polecenia.  

Proces `packages.config` rozpoznawania zależności jest skomplikowany dla większych wykresów zależności. Każdy nowy pakiet instalacji wymaga przechodzenia do całego wykresu i podnosi ryzyko wystąpienia konfliktów wersji. Po wystąpieniu konfliktu instalacja zostaje zatrzymana, pozostawiając projekt w nieokreślonym stanie, szczególnie z potencjalnymi modyfikacjami samego pliku projektu. Nie jest to problem występujący w przypadku używania innych formatów zarządzania pakietami.

## <a name="managing-dependency-assets"></a>Zarządzanie zasobami zależności

W przypadku korzystania z formatu PackageReference można kontrolować, które zasoby z zależności są przepływem do projektu najwyższego poziomu. Aby uzyskać szczegółowe informacje, zobacz [PackageReference](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

Gdy projekt najwyższego poziomu jest samym pakietem, masz również kontrolę nad tym przepływem przy użyciu `include` atrybutów i `exclude` `.nuspec` z zależnościami wymienionymi w pliku. Zobacz [. nuspec — zależności](../reference/nuspec.md#dependencies).

## <a name="excluding-references"></a>Wykluczanie odwołań

Istnieją scenariusze, w których zestawy o tej samej nazwie mogą być przywoływane więcej niż raz w projekcie, generowanie błędów czasu projektowania i czasu kompilacji. Rozważmy projekt, który zawiera niestandardową `C.dll`wersję programu, i odwołuje się do `C.dll`niego pakiet C, który również zawiera. W tym samym czasie projekt zależy również od pakietu B, który również jest zależny od pakietu C i `C.dll`. W związku z tym nie można określić, `C.dll` który z nich ma być używany, ale nie można usunąć zależności projektu w pakiecie C, ponieważ pakiet B również zależy od niego.

Aby rozwiązać ten problem, należy bezpośrednio odwołać `C.dll` się do żądanego elementu (lub użyć innego pakietu, który odwołuje się do niego), a następnie dodać zależność od pakietu C, który wyklucza wszystkie jego zasoby. Jest to wykonywane w zależności od używanego formatu zarządzania pakietami:

- [PackageReference](../consume-packages/package-references-in-project-files.md): Dodaj `ExcludeAssets="All"` w zależności:

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" ExcludeAssets="All" />
    ```

- `packages.config`: Usuń odwołanie do PackageC z `.csproj` pliku, aby odwoływać się tylko do żądanej `C.dll` wersji.
    
## <a name="dependency-updates-during-package-install"></a>Aktualizacje zależności podczas instalacji pakietu 

Jeśli poprzednia wersja zależności jest już spełniona, zależność nie jest aktualizowana podczas innych instalacji pakietu. Rozważmy na przykład pakiet A, który zależy od pakietu B i określa 1,0 dla numeru wersji. Repozytorium źródłowe zawiera wersje 1,0, 1,1 i 1,2 pakietu B. Jeśli jest zainstalowany w projekcie, który zawiera już B w wersji 1,0, wówczas B 1,0 nadal jest używany, ponieważ spełnia ograniczenie wersji. Jeśli jednak pakiet A ma żądania w wersji 1,1 lub nowszej B, wówczas zostanie zainstalowana B 1,2. 

## <a name="resolving-incompatible-package-errors"></a>Rozwiązywanie niezgodnych błędów pakietów

Podczas operacji przywracania pakietu może zostać wyświetlony komunikat o błędzie "co najmniej jeden pakiet nie jest zgodny. lub że pakiet "jest niezgodny" z platformą docelową projektu.

Ten błąd występuje, gdy jeden lub więcej pakietów, do których odwołuje się projekt, nie wskazuje, że obsługują platformę docelową projektu; oznacza to, że pakiet nie zawiera odpowiedniej biblioteki DLL w jej `lib` folderze dla platformy docelowej, która jest zgodna z projektem. (Zobacz [Platformy docelowe](../reference/target-frameworks.md) dla listy). 

Na przykład jeśli projekt jest obiektem `netstandard1.6` docelowym i podjęto próbę zainstalowania pakietu zawierającego biblioteki DLL `lib\net20` tylko w folderach `\lib\net45` i, zobaczysz komunikaty podobne do następujących dla pakietu i prawdopodobnie jego zależności:

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

- Przekieruj projekt do struktury, która jest obsługiwana przez pakiety, których chcesz użyć.
- Skontaktuj się z autorem pakietów i pracuj z nimi, aby dodać obsługę wybranej platformy. Każda Strona z listą pakietów w witrynie [NuGet.org](https://www.nuget.org/) ma link **Contact Owners** do tego celu.

