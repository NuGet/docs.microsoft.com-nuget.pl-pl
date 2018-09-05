---
title: Znajdowanie i Wybieranie pakietów NuGet
description: Przegląd jak znaleźć i wybrać najlepsze pakietów NuGet dla projektu, w tym szczegółowe informacje na temat składni wyszukiwania NuGet.
author: karann-msft
ms.author: karann
ms.date: 06/04/2018
ms.topic: conceptual
ms.openlocfilehash: 81672abf0362e053da2b71c8bd39bd7f96ddf73b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549418"
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a>Znajdowanie i ocena pakietów NuGet w projekcie

Podczas uruchamiania każdego projektu .NET lub po każdym zidentyfikować funkcjonalności potrzeby swojej aplikacji lub usługi, można zapisać samodzielnie mnóstwo czasu i problemy przy użyciu istniejących pakietów NuGet, które spełniają te potrzeby. Te pakiety mogą pochodzić z publicznych kolekcji [nuget.org](http://www.nuget.org/packages/), lub prywatnych źródła, które jest udostępniane przez organizację użytkownika lub innej.

## <a name="finding-packages"></a>Wyszukuje pakietów

Gdy można znaleźć w witrynie nuget.org, lub otworzyć Interfejs użytkownika Menedżera pakietów w programie Visual Studio, zobaczysz listę pakietów, posortowane według łączna liczba plików do pobrania. To od razu dowiesz się pakietów najbardziej powszechnie używany w milionach projektów .NET. Jest dobrym pomysłem, a następnie, że co najmniej niektórych pakietów wymienionych na pierwsze kilka stron będą użyteczne w swoich projektach.

![Domyślny widok nuget.org/packages przedstawiający najbardziej popularnymi pakietami](media/Finding-01-Popularity.png)

Zwróć uwagę **Uwzględnij wersję wstępną** opcji w prawym górnym rogu strony. Po wybraniu nuget.org pokazuje wszystkie wersje pakietów, łącznie z wersji beta i innych Wczesne wersje. Aby pokazać tylko stabilne zwolnione, wyczyść pole wyboru.

Zależności od określonych potrzeb wyszukiwanie według tagów (Menedżera pakietów w Visual Studio lub w portalu, np. nuget.org) to najczęściej oznacza, że odnajdowania odpowiedniego pakietu. Na przykład wyszukiwanie "json" zawiera listę wszystkich pakietów NuGet, które są oznaczane za pomocą tego słowa kluczowego i dlatego mają niektóre relacji do formatu danych JSON.

![Wyniki wyszukiwania dla "json" w witrynie nuget.org](media/Finding-02-SearchResults.png)

Można także przeszukać przy użyciu Identyfikatora pakietu, jeśli je znasz. Zobacz [wyszukiwanie składni](#search-syntax) poniżej.

W tej chwili wyniki wyszukiwania są sortowane tylko według istotności, więc zazwyczaj chcesz przeszukać co najmniej pierwsze kilka stron wyników dla pakietów, które odpowiadają potrzebom użytkownika lub dostosować terminy wyszukiwania, aby dokładniej.

### <a name="does-the-package-support-my-projects-target-framework"></a>Pakiet obsługuje platformę docelową mój projekt?

NuGet instaluje pakiet do projektu tylko wtedy, gdy ten pakiet obsługiwanych platform obejmują platformę docelową projektu. Jeśli pakiet nie jest zgodny, NuGet generuje błąd.

Niektóre pakiety listy ich obsługiwanych platform, bezpośrednio w galerii nuget.org, ale takich danych nie jest wymagane, wiele pakietów nie dołączaj tej listy. Obecnie nie istnieje sposób wyszukiwania nuget.org pakietów, obsługujące platformę określony element docelowy (Ta funkcja jest pod uwagę, zobacz [2936 problem NuGet](https://github.com/NuGet/NuGetGallery/issues/2936)).

Na szczęście można określić obsługiwanych platform za pomocą dwóch innych środków:

1. Próba zainstalowania pakietu do projektu przy użyciu [ `Install-Package` ](../tools/ps-ref-install-package.md) polecenia w konsoli Menedżera pakietów NuGet. Jeśli pakiet jest niezgodna, to polecenie wyświetla pakietu obsługiwanych platform.

1. Pobierz pakiet z jego strony w witrynie nuget.org przy użyciu **ręcznego pobrania** łącze w obszarze **informacje**. Zmień rozszerzenie z `.nupkg` do `.zip`, a następnie otwórz plik, aby zbadać zawartość jego `lib` folderu. Widzisz podfoldery dla każdego z obsługiwanych platform, gdzie każdy podfolder nosi nazwę z monikerem platformy docelowej (TFM; zobacz [platform docelowych](../reference/target-frameworks.md)). Jeśli zostanie wyświetlony bez podfolderów w obszarze `lib` i tylko pojedynczego pliku DLL, należy należy próbować zainstalować pakiet w projekcie w celu odnalezienia swojej zgodności.

## <a name="pre-release-packages"></a>Pakiety w wersji wstępnej

Wiele autorom pakietów upewnij (wersja zapoznawcza), a dostępne wydań beta, jako że nadal wprowadzić ulepszenia i wyszukiwanie informacji zwrotnych o ich najnowsze poprawki.

Domyślnie nuget.org zawiera pakiety w wersji wstępnej w wynikach wyszukiwania. Aby wyszukać tylko stabilne wersje, wyczyść **Uwzględnij wersję wstępną** opcji w prawym górnym rogu strony

![Obejmują wstępnej pole wyboru w witrynie nuget.org](media/Finding-06-include-prerelease.png)

W programie Visual Studio, a podczas korzystania z narzędzi interfejsu wiersza polecenia platformy dotnet i NuGet NuGet nie zawiera wersji wstępnych domyślnie. Aby zmienić to zachowanie, wykonaj następujące czynności:

- **Interfejs użytkownika Menedżera pakietów w programie Visual Studio**: W **Zarządzaj pakietami NuGet** interfejsu użytkownika, ustaw **Uwzględnij wersję wstępną** pole. Ustawienie lub usunięcie zaznaczenia tego pola odświeża interfejs użytkownika Menedżera pakietów i listę dostępnych wersji, które można zainstalować.

    ![Wstępna pola wyboru Dołącz w programie Visual Studio](media/Prerelease_02-CheckPrerelease.png)

- **Konsola Menedżera pakietów**: Użyj `-IncludePrerelease` przełącznik z `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, i `Update-Package` poleceń. Zapoznaj się [dokumentacja programu PowerShell](../tools/powershell-reference.md).

- **Interfejs wiersza polecenia nuget.exe**: Użyj `-prerelease` przełącznik z `install`, `update`, `delete`, i `mirror` poleceń. Zapoznaj się [dokumentacja interfejsu wiersza polecenia NuGet](../tools/nuget-exe-cli-reference.md)

- **DotNet.exe interfejsu wiersza polecenia**: Określ dokładnie wersji wstępnej, za pomocą `-v` argumentu. Zapoznaj się [dotnet Dodawanie odwołania do pakietu](/dotnet/core/tools/dotnet-add-package).

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a>Pakiety natywne C++

NuGet obsługuje pakiety natywne C++ może używane w projektach C++ w programie Visual Studio. Dzięki temu **Zarządzaj pakietami NuGet** polecenia menu kontekstowe dla projektów, wprowadza `native` docelowy framework i zapewnia integrację programu MSBuild.

Aby znaleźć pakiety natywne na [nuget.org](https://www.nuget.org/packages), Wyszukaj przy użyciu `tag:native`. Takie pakiety zwykle zapewniają `.targets` i `.props` pliki, które NuGet importuje automatycznie, gdy pakiet zostanie dodany do projektu.

## <a name="evaluating-packages"></a>Ocena pakietów

Najlepszym sposobem, aby ocenić przydatność pakietu jest ją pobrać i wypróbować tę funkcję w kodzie (wszystkie pakiety w witrynie nuget.org są regularnie skanowane pod kątem wirusów, przy okazji). Co bardzo popularnego pakietu uruchomiono usługę za pomocą tylko kilku deweloperzy korzystający z jego i może być jednym z pierwszych!

W tym samym czasie przy użyciu pakietu NuGet oznacza, że jest zależna od, tak aby upewnić się, że w niezawodnym i solidnym. Ponieważ instalowania i testowania bezpośrednio pakietu jest czasochłonne, możesz także dowiedzieć się znacznie jakości pakietu, korzystając z informacji na stronie listy pakiet:

- *Pobiera statystyki*: na stronie pakiet w witrynie nuget.org, **statystyki** sekcji przedstawiono całkowitą pliki do pobrania, pobieranie najnowszej wersji i średnia pobiera dziennie. Większą liczbą wskazują, że wielu innych deweloperów miały zależność od pakietu, co oznacza, że jej okazał się.

    ![Pobierz statystyki na stronie listy pakietów](media/Finding-03-Downloads.png)

- *Historia wersji*: na stronie pakiet, sprawdź w obszarze **informacje** daty ostatniego aktualizacji i sprawdź **historię wersji**. Dobrze obsługiwanych pakietów zawiera najnowsze aktualizacje i historię wersji sformatowanego. Zaniedbany pakiety mają kilka aktualizacji i często nie były aktualizowane za jakiś czas.

    ![Historia wersji na stronie listy pakietów](media/Finding-04-VersionHistory.png)

- *Instaluje najnowsze*: na stronie pakiet w obszarze **statystyki**, wybierz opcję **Wyświetl pełne statystyki**. Strony pełne statystyki pokazuje, że pakiet instaluje się w ciągu ostatnich sześciu tygodni za pomocą numeru wersji. Pakiet, który aktywnie korzystającą z innymi deweloperami zwykle jest lepszym rozwiązaniem niż ta, która nie jest.

- *Obsługuje*: na stronie pakiet w obszarze **informacje**, wybierz opcję **witryny projektu** (jeśli jest dostępny) aby sprawdzić, jaka pomoc techniczna opcje Autor zawiera. Projekt z witryną dedykowaną zazwyczaj lepiej jest obsługiwane.

- *Historia dewelopera*: na stronie pakiet w obszarze **właścicieli**, wybierz tego właściciela, aby zobaczyć, jakie inne pakiety zostały one opublikowane. Za pomocą wielu pakietów są bardziej prawdopodobne, kontynuowanie obsługi swoją pracę w przyszłości.

- *Otwórz źródło wkładów*: wiele pakietów są obsługiwane w przypadku repozytoriów typu open-source umożliwieniem deweloperom w zależności od ich bezpośrednio współtworzyć poprawki błędów i ulepszenia funkcji. Historia wkład dowolnego danego pakietu jest również dobry wskaźnik ile deweloperzy mają aktywnego udziału użytkownika.

- *Wywiad właściciele*: nowych deweloperów na pewno może być równie wszelkich starań, aby tworzyć wspaniałe pakietów do użycia i dobrze dać im możliwość dostosowania coś nowego do ekosystemu NuGet. Pamiętając o tym, skontaktuj się bezpośrednio do deweloperów pakietu za pomocą **skontaktuj się z właścicielami** opcji w obszarze **informacje** na stronie listy. To, będziesz mieć chętnie z Tobą, aby spełniały Twoje potrzeby!

- *Zastrzeżone prefiksy identyfikator pakietu*: zostały zastosowane do wielu właścicieli pakietu i zostały przyznane [pakietu zastrzeżony prefiks Identyfikatora](../reference/id-prefix-reservation.md). Po wyświetleniu visual znacznik wyboru obok Identyfikatora pakietu na [nuget.org](https://www.nuget.org/), lub w programie Visual Studio, oznacza to spełnienie właścicielem pakietu i naszych [kryteria](../reference/id-prefix-reservation.md#id-prefix-reservation-criteria) dla Identyfikatora prefiksu rezerwacji. Oznacza to, że właściciel pakietu jest jasne na identyfikowaniu same, jak i ich pakietu.

> [!Note]
> Zawsze mieć je na uwadze postanowień licencyjnych pakietu, które można wyświetlić, wybierając **informacji o licencji** na stronie listy pakietów w witrynie nuget.org. Jeśli pakiet nie określa postanowienia licencyjne, skontaktuj się z właścicielem pakietu bezpośrednio przy użyciu **skontaktuj się z właścicielami** łącze na stronie pakiet. Microsoft nie licencji jakiejkolwiek własności intelektualnej dla Ciebie od dostawców pakietów innych firm, a nie jest odpowiedzialny za otrzymane od innych firm.

## <a name="search-syntax"></a>Składnia wyszukiwania

Wyszukaj pakiet NuGet działa tak samo w witrynie nuget.org, interfejs wiersza polecenia NuGet, a także wewnątrz rozszerzenia Menedżera pakietów NuGet w programie Visual Studio. Ogólnie rzecz biorąc zastosowano wyszukiwania słów kluczowych, a także opis pakietu.

- **Słowa kluczowe**: wyszukiwania wyszukuje odpowiednie pakiety, które zawierają dowolne z podanych słów kluczowych. Przykład: `modern UI`. Aby wyszukać pakietów, które zawierają wszystkie podanych słów kluczowych, użyj "+" między warunkami, takich jak `modern+UI`.
- **Zwroty**: wprowadzania terminów w cudzysłowach szuka dokładne dopasowania bez uwzględniania wielkości liter w tych warunkach. Przykład: `"modern UI" package`
- **Filtrowanie**: termin wyszukiwania można zastosować do konkretnej właściwości, za pomocą składni `<property>:<term>` gdzie `<property>` (bez uwzględniania wielkości liter) może być `id`, `packageid`, `version`, `title`, `tags`, `author`, `description`, `summary`, i `owner`. Warunki mogą być zawarte w cudzysłowie, jeśli to konieczne, i można wyszukiwać wiele właściwości, w tym samym czasie. Ponadto wyszukuje `id` właściwości są dopasowań podciągów, podczas gdy `packageid` używa dokładnego dopasowania. Przykłady:

    ```
    id:NuGet.Core                # Match any part of the id property
    Id:"Nuget.Core"
    ID:jQuery
    title:jquery                 # Searches title as shown on the package listing
    PackageId:jquery             # Match the package id exactly
    id:jquery id:ui              # Search for multiple terms in the id
    id:jquery tags:validation    # Search multiple properties
    id:"jquery.ui"               # Phrase search
    invalid:jquery ui            # Unsupported properties are ignored, so this
                                 # is the same as searching on jquery ui
    ```
