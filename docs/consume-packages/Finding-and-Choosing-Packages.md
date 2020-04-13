---
title: Znajdowanie i wybieranie pakietów NuGet
description: Omówienie sposobu znajdowania i wybierania najlepszych pakietów NuGet dla projektu, w tym szczegółowe informacje na temat składni wyszukiwania NuGet.
author: karann-msft
ms.author: karann
ms.date: 06/04/2018
ms.topic: conceptual
ms.openlocfilehash: 9f427005251bc2bf7a8a79285e39b4bd49062dbf
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428857"
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a>Znajdowanie i ocena pakietów NuGet dla twojego projektu

Podczas uruchamiania dowolnego projektu platformy .NET lub za każdym razem, gdy identyfikujesz funkcjonalną potrzebę aplikacji lub usługi, możesz zaoszczędzić sobie dużo czasu i problemów, używając istniejących pakietów NuGet, które spełniają tę potrzebę. Pakiety te mogą pochodzić z kolekcji publicznej w [nuget.org](https://www.nuget.org/packages/)lub z prywatnego źródła dostarczonego przez organizację lub inną stronę trzecią.

## <a name="finding-packages"></a>Znajdowanie pakietów

Podczas odwiedzania nuget.org lub otwierania interfejsu użytkownika Menedżera pakietów w programie Visual Studio, zobaczysz listę pakietów posortowanych według całkowitych pobrań. To natychmiast pokazuje najczęściej używane pakiety w milionach projektów platformy .NET. Istnieje więc duża szansa, że przynajmniej niektóre pakiety wymienione na pierwszych stronach będą przydatne w twoich projektach.

![Domyślny widok nuget.org/packages pokazujący najpopularniejsze pakiety](media/Finding-01-Popularity.png)

Zwróć uwagę na opcję **Dołącz wydanie wstępne** w prawym górnym rogu strony. Po wybraniu tej opcji nuget.org wyświetla wszystkie wersje pakietów, w tym wersje beta i inne wczesne wersje. Aby wyświetlić tylko stabilne zwolnione, wyczyść opcję.

W przypadku określonych potrzeb wyszukiwanie według tagów (w menedżerze pakietów programu Visual Studio lub w portalu, takim jak nuget.org) jest najczęstszym sposobem odnajdywania odpowiedniego pakietu. Na przykład wyszukiwanie na "json" wyświetla listę wszystkich pakietów NuGet, które są oznaczone tym słowem kluczowym i w związku z tym mają pewne relacje z formatem danych JSON.

![Wyniki wyszukiwania dla 'json' w nuget.org](media/Finding-02-SearchResults.png)

Możesz również wyszukiwać przy użyciu identyfikatora pakietu, jeśli go znasz. Zobacz [składnię wyszukiwania](#search-syntax) poniżej.

W tej chwili wyniki wyszukiwania są sortowane tylko według trafności, więc zazwyczaj chcesz przeglądać co najmniej kilka pierwszych stron wyników dla pakietów, które odpowiadają Twoim potrzebom, lub zawęzić wyszukiwane terminy, aby były bardziej szczegółowe.

### <a name="does-the-package-support-my-projects-target-framework"></a>Czy pakiet obsługuje docelową strukturę mojego projektu?

NuGet instaluje pakiet w projekcie tylko wtedy, gdy obsługiwane struktury tego pakietu obejmują platformę docelową projektu. Jeśli pakiet nie jest zgodny, NuGet wystawia błąd.

Niektóre pakiety wymieniają obsługiwane struktury bezpośrednio w galerii nuget.org, ale ponieważ takie dane nie są wymagane, wiele pakietów nie zawiera tej listy. Obecnie nie ma środków do wyszukiwania nuget.org dla pakietów, które obsługują określonej struktury docelowej (funkcja jest rozważana, zobacz [NuGet Issue 2936](https://github.com/NuGet/NuGetGallery/issues/2936)).

Na szczęście można określić obsługiwane struktury za pomocą dwóch innych środków:

1. Spróbuj zainstalować pakiet w projekcie [`Install-Package`](../reference/ps-reference/ps-ref-install-package.md) za pomocą polecenia w konsoli Menedżera pakietów NuGet. Jeśli pakiet jest niezgodny, to polecenie pokazuje obsługiwane struktury pakietu.

1. Pobierz pakiet ze swojej strony na nuget.org za pomocą linku **Do pobrania Ręczne** w obszarze **Informacje**. Zmień rozszerzenie `.nupkg` z `.zip`na program i otwórz plik, `lib` aby sprawdzić zawartość jego folderu. Tam są widoczne podfoldery dla każdej z obsługiwanych struktur, gdzie każdy podfolder jest nazwany z monikerem struktury docelowej (TFM; zobacz [Struktury docelowe).](../reference/target-frameworks.md) Jeśli nie widzisz żadnych `lib` podfolderów w obszarze i tylko jedną bibliotekę DLL, należy podjąć próbę zainstalowania pakietu w projekcie, aby odkryć jego zgodność.

## <a name="pre-release-packages"></a>Pakiety w wersji wstępnej

Wielu autorów pakietów udostępnia wersje zapoznawczye i beta, ponieważ nadal wprowadzać ulepszenia i zasięgać opinii na temat swoich najnowszych wersji.

Domyślnie nuget.org pokazuje pakiety wersji wstępnej w wynikach wyszukiwania. Aby wyszukać tylko **stabilne** wersje, wyczyść opcję Dołącz wydanie wstępne w prawym górnym rogu strony

![Uwzględnij pole wyboru wstępnej wersji programu nuget.org](media/Finding-06-include-prerelease.png)

W programie Visual Studio i podczas korzystania z narzędzi NuGet i dotnet interfejsu wiersza polecenia NuGet nie zawiera wersji wstępnych domyślnie. Aby zmienić to zachowanie, wykonaj następujące czynności:

- **Interfejs użytkownika Menedżera pakietów w programie Visual Studio:** W interfejsie użytkownika **zarządzania pakietami NuGet** ustaw pole **Dołącz zawartość wstępną.** Ustawienie lub wyczyszczenie tego pola powoduje odświeżenie interfejsu użytkownika Menedżera pakietów i listy dostępnych wersji, które można zainstalować.

    ![Pole wyboru Uwzględnij wydanie wstępne w programie Visual Studio](media/Prerelease_02-CheckPrerelease.png)

- **Konsola Menedżera pakietów:** Użyj przełącznika `-IncludePrerelease` z poleceniami `Find-Package`, `Get-Package` `Install-Package`, `Sync-Package`, i. `Update-Package` Zapoznaj się z [odwołaniem programu PowerShell](../reference/powershell-reference.md).

- **nuget.exe CLI:** `-prerelease` Użyj przełącznika `update` `delete`z `mirror` poleceniami `install`, , i . Zapoznaj się z [odwołaniem nuget cli](../reference/nuget-exe-cli-reference.md)

- **dotnet.exe CLI**: Określ dokładną `-v` wersję wstępną za pomocą argumentu. Zapoznaj się z [odwołaniem do dotnet add package](/dotnet/core/tools/dotnet-add-package).

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a>Natywne pakiety C++

NuGet obsługuje natywne pakiety C++, które mogą być używane w projektach języka C++ w programie Visual Studio. Dzięki temu **zarządzanie pakietami NuGet** menu kontekstowe `native` polecenia dla projektów, wprowadza platformę docelową i zapewnia integrację MSBuild.

Aby znaleźć pakiety macierzyste w `tag:native` [nuget.org](https://www.nuget.org/packages), wyszukaj za pomocą . Takie pakiety `.targets` zazwyczaj `.props` zapewniają i pliki, które NuGet importuje automatycznie, gdy pakiet jest dodawany do projektu.

## <a name="evaluating-packages"></a>Ocena pakietów

Najlepszym sposobem oceny przydatności pakietu jest pobranie go i wypróbowanie go w kodzie (wszystkie pakiety na nuget.org są rutynowo skanowane w poszukiwaniu wirusów, nawiasem mówiąc). Po tym wszystkim, każdy bardzo popularny pakiet rozpoczął się tylko kilku programistów korzystających z niego, i może być jednym z pierwszych użytkowników!

W tym samym czasie przy użyciu pakietu NuGet oznacza biorąc zależność od niego, więc chcesz upewnić się, że jest niezawodny i niezawodny. Ponieważ instalowanie i bezpośrednie testowanie pakietu jest czasochłonne, można również dowiedzieć się wiele o jakości pakietu, korzystając z informacji na stronie listy pakietu:

- *Statystyki pobierania*: na stronie pakietu w nuget.org sekcja **Statystyki** pokazuje łączną liczbę pobrań, pobrań najnowszej wersji i średnie pobrań dziennie. Większe liczby wskazują, że wielu innych deweloperów miały zależność od pakietu, co oznacza, że sprawdził się.

    ![Pobieranie statystyk na stronie aukcji pakietu](media/Finding-03-Downloads.png)

- *Użycie gitHub:* na stronie pakietu sekcja **Użycie GitHub** zawiera listę publicznych repozytoriów GitHub, które zależą od tego pakietu i które mają dużą liczbę gwiazdek w usłudze GitHub. Liczba gwiazdek repozytorium GitHub zazwyczaj wskazuje, jak popularne jest to repozytorium wśród użytkowników GitHub (więcej gwiazdek zwykle oznacza większą popularność). Więcej informacji na temat systemu rankingowego GitHub w zakresie gwiazd i repozytorium można znaleźć na stronie Wprowadzenie [do gitHub.](https://help.github.com/en/github/getting-started-with-github/saving-repositories-with-stars#about-stars)

    ![Użycie githubu](media/GitHub-Usage.png)

    > [!Note]
    > Sekcja GitHub Usage pakietu jest generowana automatycznie, okresowo, bez przeglądu poszczególnych repozytoriów przez człowieka i wyłącznie w celach informacyjnych w celu wyświetlenia repozytoriów GitHub, które zależą od pakietu i które są popularne wśród użytkowników GitHub.

- *Historia wersji*: na stronie pakietu poszukaj w obszarze **Informacje** daty ostatniej aktualizacji i sprawdź **historię wersji**. Dobrze utrzymany pakiet zawiera najnowsze aktualizacje i bogatą historię wersji. Zaniedbane pakiety mają kilka aktualizacji i często nie zostały zaktualizowane w pewnym czasie.

    ![Historia wersji na stronie aukcji pakietu](media/Finding-04-VersionHistory.png)

- *Ostatnie instalacje:* na stronie pakietu w obszarze **Statystyki**wybierz **pozycję Wyświetl pełne statystyki**. Pełna strona statystyk pokazuje pakiet instalowany w ciągu ostatnich sześciu tygodni według numeru wersji. Pakiet, który inni deweloperzy są aktywnie przy użyciu jest zazwyczaj lepszym wyborem niż taki, który nie jest.

- *Pomoc techniczna:* na stronie pakietu w obszarze **Informacje**wybierz **pozycję Witryna projektu** (jeśli jest dostępna), aby zobaczyć, jakie opcje pomocy technicznej zapewnia autor. Projekt z dedykowaną witryną jest na ogół lepiej obsługiwany.

- *Historia deweloperów*: na stronie pakietu w obszarze **Właściciele**wybierz właściciela, aby zobaczyć, jakie inne pakiety opublikowali. Osoby z wieloma pakietami są bardziej prawdopodobne, aby kontynuować wspieranie ich pracy w przyszłości.

- *Wkład open source:* wiele pakietów jest utrzymywanych w repozytoriach open source, dzięki czemu deweloperzy mogą w zależności od nich bezpośrednio wnosić poprawki błędów i ulepszenia funkcji. Historia wkładu danego pakietu jest również dobrym wskaźnikiem tego, ilu programistów jest aktywnie zaangażowanych.

- *Wywiad z właścicielami*: nowi deweloperzy z pewnością mogą być równie zaangażowani w produkcję świetnych pakietów do wykorzystania, i dobrze jest dać im szansę wnieść coś nowego do ekosystemu NuGet. Mając to na uwadze, skontaktuj się bezpośrednio z deweloperami pakietów za pomocą opcji **Skontaktuj się z właścicielami** w obszarze **Informacje** na stronie aukcji. Są szanse, że chętnie będą współpracować z Tobą, aby zaspokoić Twoje potrzeby!

- *Prefiksy zastrzeżonego identyfikatora pakietu:* wielu właścicieli pakietów złożyło wniosek o [wydanie zastrzeżonego prefiksu identyfikatora pakietu.](../nuget-org/id-prefix-reservation.md) Gdy zobaczysz znacznik wyboru wizualnego obok identyfikatora pakietu w [nuget.org](https://www.nuget.org/)lub w programie Visual Studio, oznacza to, że właściciel pakietu spełnił nasze [kryteria](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria) rezerwacji prefiksu identyfikatora. Oznacza to, że właściciel pakietu jest jasne, na identyfikacji siebie i ich pakiet.

> [!Note]
> Zawsze należy pamiętać o postanowieniach licencyjnych pakietu, które można zobaczyć, wybierając **informacje o licencji** na stronie aukcji pakietu w nuget.org. Jeśli pakiet nie określa postanowień licencyjnych, skontaktuj się z właścicielem pakietu bezpośrednio za pomocą łącza **Skontaktuj się z właścicielami** na stronie pakietu. Firma Microsoft nie udziela licencji na żadne prawa własności intelektualnej od zewnętrznych dostawców pakietów i nie ponosi odpowiedzialności za informacje dostarczone przez osoby trzecie.

## <a name="license-url-deprecation"></a>Deprecation adresów URL licencji
W miarę przechodzenia z [licenseUrl](../reference/nuspec.md#licenseurl) do [licencji,](../reference/nuspec.md#license)niektórzy klienci NuGet i źródła danych NuGet mogą jeszcze nie mieć możliwości tworzenia informacji o licencjonowaniu w niektórych przypadkach. Aby zachować zgodność z powrotem, adres URL licencji wskazuje ten dokument, który mówi o tym, jak pobrać informacje o licencji w takich przypadkach.

Kliknięcie adresu URL licencji dla pakietu, który został przeniesiony na tę stronę, oznacza to, że pakiet zawiera plik licencji i
* Jesteś połączony z kanałem, który nie wie jeszcze, jak interpretować i powierzchni nowych informacji licencyjnych do klienta **LUB**
* Korzystasz z klienta, który nie wie jeszcze, jak interpretować i odczytywać nowe informacje o licencji, które są potencjalnie dostarczane przez kanał **LUB**
* Kombinacja obu bram

Oto jak można odczytać informacje zawarte w pliku licencji wewnątrz pakietu:
1. Pobierz pakiet NuGet i rozpaj jego zawartość do folderu.
1. Otwórz `.nuspec` plik, który byłby w katalogu głównym tego folderu.
1. Powinien mieć tag `<license type="file">license\license.txt</license>`jak . Oznacza to, że plik `license.txt` licencji jest nazwany `license` i znajduje się wewnątrz folderu o nazwie, który również znajduje się w katalogu głównym tego folderu.
1. Przejdź do `license` folderu `license.txt` i otwórz plik.

Dla MSBuild równoważne ustawienie licencji `.nuspec`w , spójrz na [Pakowanie wyrażenia licencji lub pliku licencji](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).

## <a name="search-syntax"></a>Szukaj składni

Wyszukiwanie pakietów NuGet działa tak samo na nuget.org, z interfejsu wiersza polecenia NuGet i w ramach rozszerzenia Menedżera pakietów NuGet w programie Visual Studio. Ogólnie rzecz biorąc, wyszukiwanie jest stosowane do słów kluczowych, a także opisów pakietów.

- **Filtrowanie:** Wyszukiwany termin można zastosować do określonej właściwości `<property>:<term>` `<property>` przy użyciu składni, w której `id` `packageid`(bez `title` `tags`uwzględniania wielkości `owner`liter) mogą być , , `version`, , , `author`, `description`, `summary`, , i . Można wyszukiwać wiele właściwości w tym samym czasie. Wyszukiwania we `id` właściwości są dopasowania podciągów, natomiast `packageid` i `owner` używa dokładne, niewrażliwe dopasowanie. Przykłady:

```
PackageId:jquery             # Match the package ID in an exact, case-insensitive manner

owner:microsoft              # Match the owner in an exact, case-insensitive manner

id:NuGet.Core                # Match any part of the ID property
Id:"Nuget.Core"
ID:jQuery
id:jquery id:ui              # Search for multiple terms in the ID
id:jquery tags:validation    # Search multiple properties

invalid:jquery ui            # Unsupported properties are ignored, so this
                             # is the same as searching on ui
```
