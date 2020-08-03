---
title: Znajdowanie i wybieranie pakietów NuGet
description: Omówienie sposobu znajdowania i wybierania najlepszych pakietów NuGet dla projektu, w tym szczegółowych informacji o składni wyszukiwania NuGet.
author: karann-msft
ms.author: karann
ms.date: 06/04/2018
ms.topic: conceptual
ms.openlocfilehash: 45928e60033959bc8b4f43d1ef3e4c943e7ec057
ms.sourcegitcommit: e02482e15c0cef63153086ed50d14f5b2a38f598
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/31/2020
ms.locfileid: "87473887"
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a>Znajdowanie i ocenianie pakietów NuGet dla projektu

Podczas uruchamiania dowolnego projektu .NET lub przy każdej identyfikacji potrzeby funkcjonalnej aplikacji lub usługi możesz zaoszczędzić wiele czasu i problemów, korzystając z istniejących pakietów NuGet, które spełniają te wymagania. Te pakiety mogą pochodzić z publicznej kolekcji [NuGet.org](https://www.nuget.org/packages/)lub prywatnego źródła, które jest udostępniane przez organizację lub inną osobę trzecią.

## <a name="finding-packages"></a>Znajdowanie pakietów

Po odwiedzeniu nuget.org lub otwarciu interfejsu użytkownika Menedżera pakietów w programie Visual Studio zostanie wyświetlona lista pakietów posortowanych według dokładność. Pokazuje to najczęściej używane pakiety we wszystkich projektach platformy .NET. Istnieje dobry szansa, że niektóre z tych pakietów mogą być przydatne dla własnych projektów.

![Widok domyślny nuget.org/packages pokazujący najpopularniejsze pakiety](media/Finding-01-Popularity.png)

W witrynie nuget.org Zwróć uwagę na przycisk **Filtr** w prawym górnym rogu strony. Po kliknięciu panel wyszukiwania zaawansowanego zostanie rozwinięty, aby przedstawić opcje sortowania i filtrowania.

![Wyniki wyszukiwania dla elementu "JSON" w nuget.org](media/Finding-02-SearchResults.png)

Aby wyświetlić pakiety określonego typu, można użyć filtru **typu pakietu** :
- **`All types`**: Jest to zachowanie domyślne. Pokazuje wszystkie pakiety niezależnie od ich typu.
- **`Dependency`**: Regularne pakiety NuGet, które można zainstalować w projekcie.
- **`.NET tool`**: Te filtry do [narzędzi platformy .NET](/dotnet/core/tools/global-tools), pakiet NuGet zawierający aplikację konsolową.
- **`Template`**: Te filtry do [szablonów platformy .NET](/dotnet/core/install/templates), których można użyć do tworzenia nowych projektów przy użyciu [`dotnet new`](/dotnet/core/tools/dotnet-new) polecenia.

Możesz użyć opcji **Sortuj według** , aby posortować wyniki wyszukiwania:
- **`Relevance`**: Jest to zachowanie domyślne. Sortuje wyniki zgodnie z wewnętrznym algorytmem oceniania.
- **`Downloads`**: Sortuje wyniki wyszukiwania według łącznej liczby pobrań w kolejności malejącej.
- **`Recently updated`**: Sortuje wyniki wyszukiwania według daty utworzenia najnowszej wersji, w kolejności malejącej chronologicznej.

W sekcji **Opcje** można znaleźć **`Include prerelease`** pole wyboru.
Po zaznaczeniu tej opcji nuget.org wyświetla wszystkie wersje pakietów, w tym wstępne wydania. Aby wyświetlić tylko stabilne wersje, usuń zaznaczenie tej opcji.

Aby zastosować filtry wyszukiwania, kliknij **`Apply`** przycisk. Zawsze możesz wrócić do zachowania domyślnego, klikając **`Reset`** przycisk.

Można również użyć [składni wyszukiwania](#search-syntax) do filtrowania tagów, właścicieli i identyfikatorów pakietów.

### <a name="does-the-package-support-my-projects-target-framework"></a>Czy pakiet obsługuje platformę docelową mojego projektu?

NuGet instaluje pakiet do projektu tylko wtedy, gdy obsługiwane struktury tego pakietu obejmują platformę docelową projektu. Jeśli pakiet nie jest zgodny, narzędzie NuGet wystawia błąd.

Niektóre pakiety mają listę obsługiwanych struktur bezpośrednio w galerii nuget.org, ale ponieważ takie dane nie są wymagane, wiele pakietów nie zawiera tej listy. Obecnie nie ma możliwości wyszukiwania nuget.org dla pakietów, które obsługują konkretną platformę docelową (Ta funkcja jest rozważana, zobacz problem z pakietem [nuget 2936](https://github.com/NuGet/NuGetGallery/issues/2936)).

Na szczęście można określić obsługiwane platformy, korzystając z dwóch innych metod:

1. Spróbuj zainstalować pakiet w projekcie za pomocą [`Install-Package`](../reference/ps-reference/ps-ref-install-package.md) polecenia w konsoli Menedżera pakietów NuGet. Jeśli pakiet jest niezgodny, to polecenie pokazuje obsługiwane platformy pakietu.

1. Pobierz pakiet z jego strony na nuget.org przy użyciu linku **pobierania ręcznego** w obszarze **informacje**. Zmień rozszerzenie z `.nupkg` na `.zip` , a następnie otwórz plik, aby przejrzeć zawartość jego `lib` folderu. Dla każdej obsługiwanej platformy widoczne są podfoldery, gdzie każdy podfolder ma nazwę z monikerem platformy docelowej (TFM; zobacz [Platformy docelowe](../reference/target-frameworks.md)). Jeśli w obszarze `lib` i tylko jednej bibliotece DLL nie ma podfolderów, należy spróbować zainstalować pakiet w projekcie w celu odnalezienia jego zgodności.

## <a name="pre-release-packages"></a>Pakiety wersji wstępnej

Wielu autorów pakietów udostępnia wersje zapoznawcze i beta, ponieważ kontynuują ulepszanie i wyszukiwanie najnowszych poprawek.

Domyślnie nuget.org wyświetla pakiety wersji wstępnej w wynikach wyszukiwania. Aby wyszukać tylko stabilne wersje, wyczyść opcję **Uwzględnij wersję wstępną** w panelu wyszukiwania zaawansowanego dostępnym z poziomu przycisku **filtru** w prawym górnym rogu strony.

![Pole wyboru Uwzględnij wersję wstępną w programie nuget.org](media/Finding-06-include-prerelease.png)

W programie Visual Studio i w przypadku korzystania z narzędzi NuGet i interfejsu wiersza polecenia programu dotnet pakiet NuGet domyślnie nie zawiera wersji wstępnej. Aby zmienić to zachowanie, wykonaj następujące czynności:

- **Interfejs użytkownika Menedżera pakietów w programie Visual Studio**: w interfejsie użytkownika **Zarządzanie pakietami NuGet** Ustaw pole **Uwzględnij wersję wstępną** . Ustawienie lub wyczyszczenie tego pola powoduje odświeżenie interfejsu użytkownika Menedżera pakietów oraz listę dostępnych wersji, które można zainstalować.

    ![Pole wyboru Uwzględnij wersję wstępną w programie Visual Studio](media/Prerelease_02-CheckPrerelease.png)

- **Konsola Menedżera pakietów**: Użyj `-IncludePrerelease` przełącznika z `Find-Package` poleceniami,,, `Get-Package` `Install-Package` `Sync-Package` i `Update-Package` . Zapoznaj się z dokumentacją [programu PowerShell](../reference/powershell-reference.md).

- **Interfejs wiersza polecenianuget.exe**: Użyj `-prerelease` przełącznika z `install` poleceniem, `update` , `delete` i `mirror` . Zapoznaj się z dokumentacją [interfejsu wiersza polecenia NuGet](../reference/nuget-exe-cli-reference.md)

- **Interfejs wiersza poleceniadotnet.exe**: Określ dokładną wersję wstępną za pomocą `-v` argumentu. Zapoznaj się z informacjami dotyczącymi [dodawania pakietu dotnet](/dotnet/core/tools/dotnet-add-package).

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a>Natywne pakiety języka C++

Pakiet NuGet obsługuje natywne pakiety języka C++, które mogą być używane w projektach C++ w programie Visual Studio. Umożliwia to menu kontekstowe **Zarządzanie pakietami NuGet** dla projektów, wprowadza `native` platformę docelową i zapewnia integrację z programem MSBuild.

Aby znaleźć natywne pakiety w [NuGet.org](https://www.nuget.org/packages), Wyszukaj za pomocą `tag:native` . Takie pakiety zazwyczaj udostępniają `.targets` i `.props` pliki, które NuGet są importowane automatycznie podczas dodawania pakietu do projektu.

## <a name="evaluating-packages"></a>Ocenianie pakietów

Najlepszym sposobem na ocenę użyteczności pakietu jest pobranie go i wypróbowanie go w kodzie (wszystkie pakiety na nuget.org są rutynowo skanowane pod kątem wirusów, w drodze). Każdy wysoce popularny pakiet został uruchomiony tylko przez kilku deweloperów korzystających z niego i może być jednym z wczesnych użytkowników.

W tym samym czasie używanie pakietu NuGet oznacza jego zależność, dlatego należy upewnić się, że jest to niezawodne i niezawodne. Ponieważ Instalowanie i bezpośrednie Testowanie pakietu jest czasochłonne, można także uzyskać informacje o jakości pakietu, korzystając z informacji na stronie z listą pakietu:

- *Pobieranie statystyk*: na stronie pakiet w witrynie NuGet.org sekcja **statystyki** zawiera łączne pliki do pobrania, pliki do pobrania najnowszej wersji i średnie pobieranie na dzień. Większa liczba wskazuje, że wielu innych deweloperów pobrało zależność od pakietu, co oznacza, że sama sprawdzona.

    ![Pobierz statystyki na stronie z listą pakietu](media/Finding-03-Downloads.png)

- *Użycie usługi GitHub*: na stronie Package (pakiet) sekcja **użycie usługi GitHub** zawiera listę publicznych repozytoriów GitHub, które są zależne od tego pakietu i o dużej liczbie gwiazdek w witrynie GitHub. Liczba gwiazdek repozytorium GitHub zazwyczaj wskazuje, jak popularne jest repozytorium z użytkownikami usługi GitHub (zazwyczaj jest to bardziej popularne). Odwiedź [stronę wprowadzenie witryny GitHub](https://help.github.com/en/github/getting-started-with-github/saving-repositories-with-stars#about-stars) , aby uzyskać więcej informacji o systemie klasyfikacji i repozytorium usługi GitHub.

    ![Użycie usługi GitHub](media/GitHub-Usage.png)

    > [!Note]
    > Sekcja użycie usługi GitHub pakietu jest generowana automatycznie, bez sprawdzenia przez człowieka indywidualnych repozytoriów i wyłącznie do celów informacyjnych w celu pokazania repozytoriów GitHub, które są zależne od pakietu i które są popularne z użytkownikami usługi GitHub.

- *Historia wersji*: na stronie pakiet zapoznaj się z **informacjami** dotyczącymi daty ostatniej aktualizacji i sprawdź **historię wersji**. Dobrze obsługiwany pakiet zawiera najnowsze aktualizacje i zaawansowaną historię wersji. Zaniedbane pakiety mają kilka aktualizacji i często nie zostały zaktualizowane w pewnym czasie.

    ![Historia wersji na stronie z listą pakietu](media/Finding-04-VersionHistory.png)

- *Ostatnie instalacje*: na stronie pakiet w obszarze **Statystyka**wybierz pozycję **Wyświetl pełne statystyki**. Na stronie pełne statystyki zostanie wyświetlony pakiet instalowany w ciągu ostatnich sześciu tygodni według numeru wersji. Pakiet, do którego aktywnie korzysta inni deweloperzy, jest zazwyczaj lepszym wyborem niż ten, który nie jest.

- *Obsługa*: na stronie pakiet w obszarze **informacje**wybierz pozycję **Witryna projektu** (jeśli jest dostępna), aby zobaczyć opcje pomocy technicznej udostępniane przez autora. Projekt z dedykowaną lokacją jest ogólnie lepszy.

- *Historia deweloperów*: na stronie pakiet w obszarze **właściciele**wybierz właściciela, aby zobaczyć, jakie inne pakiety zostały opublikowane. Te z wieloma pakietami mogą nadal obsługiwać swoją pracę w przyszłości.

- *Wkłady typu open source*: wiele pakietów jest przechowywanych w repozytoriach typu "open source", dzięki czemu deweloperzy mogą w zależności od nich bezpośrednio współtworzyć poprawki błędów i ulepszenia funkcji. Historia udziału danego pakietu jest również dobrym wskaźnikiem liczby aktywnie używanych deweloperów.

- Przeprowadzenie *rozmowy kwalifikacyjnej z właścicielami*: Nowi deweloperzy mogą na pewno być zaangażowani w tworzenie doskonałych pakietów do użycia i dobrym rozwiązaniem jest nadanie im nowego ekosystemu NuGet. Pamiętając o tym, aby skontaktować się bezpośrednio z deweloperami pakietu za pomocą opcji **właściciele kontaktu** w obszarze **informacje** na stronie z listą. Z tego strony będą mieć szczęście, aby móc korzystać z Twoich potrzeb.

- *Prefiksy identyfikatorów pakietów zarezerwowanych*: wiele właścicieli pakietów ma zastosowanych do i ma przypisany [prefiks identyfikatora pakietu zastrzeżonego](../nuget-org/id-prefix-reservation.md). Gdy zobaczysz znacznik wyboru obok identyfikatora pakietu na [NuGet.org](https://www.nuget.org/)lub w programie Visual Studio, oznacza to, że właściciel pakietu spełnił [kryteria](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria) rezerwacji prefiksów identyfikatorów. Oznacza to, że właściciel pakietu jest czyszczony na identyfikowaniu siebie i ich pakiecie.

> [!Note]
> Zawsze pamiętaj o postanowień licencyjnych dotyczących pakietu, które możesz zobaczyć, wybierając pozycję **Informacje o licencji** na stronie z listą pakietów w witrynie NuGet.org. Jeśli pakiet nie określa postanowień licencyjnych, skontaktuj się z właścicielem pakietu bezpośrednio, korzystając z linku **właściciele kontaktu** na stronie pakiet. Firma Microsoft nie udziela licencji jakiejkolwiek własności intelektualnej od dostawców pakietów innych firm i nie ponosi odpowiedzialności za informacje udostępniane przez strony trzecie.

## <a name="license-url-deprecation"></a>Przestarzały adres URL licencji
Po przejściu z [licenseUrl](../reference/nuspec.md#licenseurl) na [licencję](../reference/nuspec.md#license)niektórzy klienci NuGet i źródła danych NuGet mogą nie mieć jeszcze możliwości podawania informacji licencyjnych. Aby zachować zgodność z poprzednimi wersjami, adres URL licencji wskazuje ten dokument zawierający informacje o sposobie pobierania informacji o licencji w takich przypadkach.

Jeśli klikniesz adres URL licencji dla pakietu przeniesiesz do tej strony, oznacza to, że pakiet zawiera plik licencji i
* Nawiązano połączenie ze źródłem danych, które nie wie, jak interpretować i przedstawić nowe informacje o licencji na kliencie **lub**
* Używasz klienta, który jeszcze nie wie, jak interpretować i odczytać nowe informacje o licencji, które są potencjalnie dostępne w kanale informacyjnym **lub**
* Kombinacja obu bram

Oto jak można odczytać informacje zawarte w pliku licencji w pakiecie:
1. Pobierz pakiet NuGet i rozpakuj jego zawartość do folderu.
1. Otwórz `.nuspec` plik, który będzie znajdować się w katalogu głównym tego folderu.
1. Powinien mieć tag podobny do tego `<license type="file">license\license.txt</license>` . Oznacza to, że plik licencji ma nazwę `license.txt` i znajduje się w folderze o nazwie, `license` który również znajduje się w katalogu głównym tego folderu.
1. Przejdź do `license` folderu i Otwórz `license.txt` plik.

W przypadku programu MSBuild równoważnego ustawieniu licencji w programie zapoznaj się z tematem `.nuspec` [pakowanie wyrażenia licencji lub pliku licencji](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).

## <a name="search-syntax"></a>Składnia wyszukiwania

Wyszukiwanie pakietów NuGet działa tak samo na nuget.org, w interfejsie wiersza polecenia NuGet i w rozszerzeniu Menedżera pakietów NuGet w programie Visual Studio. Ogólnie rzecz biorąc, wyszukiwanie jest stosowane do słów kluczowych, a także opisów pakietów.

- **Filtrowanie**: możesz zastosować termin wyszukiwania do konkretnej właściwości przy użyciu składni `<property>:<term>` , gdzie (bez `<property>` uwzględniania wielkości liter) może być,,,,,,, `id` `packageid` `version` `title` `tags` `author` `description` `summary` , i `owner` . Można wyszukiwać wiele właściwości jednocześnie. Wyszukiwania na `id` właściwości są dopasowaniami podciągów, podczas gdy `packageid` i `owner` używa dokładnego dopasowania bez uwzględniania wielkości liter. Przykłady:

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
