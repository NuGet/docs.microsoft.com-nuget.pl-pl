---
title: Informacje o wersji NuGet 2.1 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informacje o wersji programu NuGet 2.1 tym znanych problemów, poprawki, dodatkowe funkcje i dcr."
keywords: NuGet 2.1 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 05cdb898cc674ac7eadb238d41896638d8e3488c
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-21-release-notes"></a>Informacje o wersji 2.1 NuGet

[Informacje o wersji NuGet 2.0](../release-notes/nuget-2.0.md) | [NuGet 2.2 informacje o wersji](../release-notes/nuget-2.2.md)

NuGet 2.1 został wydany 4 października 2012.

## <a name="hierarchical-nugetconfig"></a>Hierarchiczna pliku Nuget.Config.
NuGet 2.1 zapewnia większą elastyczność w kontrolowanie ustawień NuGet i rekursywnie przejście zapasowej struktury folderów wyszukiwania `NuGet.Config` plików i następnie budowanie konfiguracji z zestawu wszystkich znalezionych plików.  Na przykład Rozważmy scenariusz, w którym zespół ma z repozytorium pakietów wewnętrzny dla elementu konfiguracji kompilacji innych zależności wewnętrzne. Struktura folderów dla pojedynczego projektu może wyglądać następująco:

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

Ponadto jeśli Przywracanie pakietów jest włączone dla rozwiązania, również będą istnieć następujący folder:

    C:\myteam\solution1\.nuget

Aby przypisać repozytorium pakietów wewnętrznego zespołu dostępne dla wszystkich projektów, które zespół pracuje podczas nie czym będzie dostępna dla każdego projektu na komputerze, firma Microsoft Utwórz nowy plik Nuget.Config i umieść go w folderze c:\myteam. Nie istnieje sposób zdefiniuj do folderu pakietów dla projektu.

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

Możemy teraz sprawdzić, czy źródło zostało dodane, uruchamiając polecenie "nuget.exe źródła" z dowolnego folderu poniżej c:\myteam w sposób przedstawiony poniżej:

![Źródła pakietów z konfiguracji nadrzędnej nuget](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config`pliki są wyszukiwane w następującej kolejności:

1. `.nuget\Nuget.Config`
2. Cykliczne zaprezentuje z folderu projektu z katalogiem głównym
3. Globalne `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)

Konfiguracje są niż stosowane w *odwracania kolejności*, oznacza to, że zgodne z kolejnością powyżej, globalnego pliku Nuget.Config czy być zastosowana jako pierwsza, następuje odnalezionych plików pliku Nuget.Config z głównym folderze projektu, a następnie przez `.nuget\Nuget.Config`.  Jest to szczególnie ważne, jeśli używasz `<clear/>` elementu do usunięcia zbiór elementów na podstawie konfiguracji.

## <a name="specify-packages-folder-location"></a>Określ lokalizację folderu "packages"
W przeszłości NuGet zarządza pakietów rozwiązania z folderu znane pakietów znaleziono poniżej folderu głównego rozwiązania.  Dla zespoły deweloperów, które mają wiele różnych rozwiązań, które zostały zainstalowane pakiety NuGet może to spowodować tego samego pakietu instalowany w wielu różnych miejscach w systemie plików.

NuGet 2.1 zapewnia większą kontrolę nad lokalizację folderu pakietów za pomocą `repositoryPath` element `NuGet.Config` pliku.  Opierając się na poprzedni przykład hierarchiczna Nuget.Config pomocy technicznej, Przykładowa firma Microsoft chcesz, aby wszystkie projekty w obszarze C:\myteam\ udział w tym samym folderze pakietów.  W tym celu po prostu dodaj następujący wpis do `c:\myteam\Nuget.Config`.

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

W tym przykładzie udostępnionego `Nuget.Config` pliku Określa folder udostępniony pakietów dla każdego projektu, który jest tworzony poniżej C:\myteam, niezależnie od głębokość. Uwaga: Jeśli masz istniejący folder pakietów poniżej katalogu głównym rozwiązanie będzie należy go usunąć przed NuGet spowoduje umieszczenie pakietów w nowej lokalizacji.

## <a name="support-for-portable-libraries"></a>Obsługa bibliotek przenośnych
[Przenośnych bibliotek](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) to funkcja wprowadzona z .NET 4, który umożliwia tworzenie zestawów, które mogą pracować bez żadnych modyfikacji na różnych platformach firmy Microsoft, z wersji środowiska.NET Framework do Silverlight Windows Phone i nawet Xbox 360 (chociaż w tej chwili NuGet nie obsługują elementu docelowego przenośnej biblioteki konsoli Xbox).  Rozszerzając [pakietu konwencje](../create-packages/supporting-multiple-target-frameworks.md) profilów i framework w wersji NuGet 2.1 obsługuje teraz bibliotek przenośnych dzięki umożliwieniu tworzenia pakietów, które framework złożone i cel profilu `lib` folderów.

Na przykład należy wziąć pod uwagę następujące biblioteki klas przenośnych dostępnych platform.

![Okno dialogowe Tworzenie przenośnej biblioteki](./media/releasenotes-21-plib.png)

Po utworzeniu biblioteki i polecenia `nuget.exe pack MyPortableProject.csproj` jest uruchamiana, nowy komputer przenośny struktury folderu pakietu biblioteki można wyświetlić, sprawdzając zawartość wygenerowany pakiet NuGet.

![Biblioteka przenośna układ pakietu](./media/releasenotes-21-plib-layout.png)

Jak widać, Konwencji nazwa folderu przenośnej biblioteki zgodny ze wzorcem "portable {platformy 1} + {framework n}", gdzie identyfikatory framework postępuj zgodnie z istniejącą [konwencje nazwa i wersja framework](../schema/target-frameworks.md). Jedynym wyjątkiem konwencje nazwa i wersja znajduje się w identyfikator platformy używany dla Windows Phone.  Moniker tej należy używać nazwy platformy "wp" (wp7, wp71 lub wp8). Za pomocą "wp7 silverlight", na przykład spowoduje błąd.

Podczas instalowania pakietu, który został utworzony na podstawie tej struktury folderów, NuGet teraz reguły można stosować jej framework i profilu do wielu elementów docelowych, jak określono w nazwie folderu.  Za regułami dopasowywania NuGet jest zasada "dokładniej" elementy docelowe mają pierwszeństwo przed "mniej" precyzyjnych.  Oznacza to, że monikerów przeznaczonych dla określonej platformy będzie zawsze preferowany nad przenośne te jeśli są zgodne z projektem.  Ponadto jeśli wiele elementów docelowych przenośnych są zgodne z projektem, NuGet preferowane jeden zestaw platformach obsługiwanych w przypadku "najbliższy" do projektu odwołanie do pakietu.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Skierowane do systemu Windows 8 i Windows Phone 8 projektów
Oprócz dodawania obsługi przeznaczonych dla projektów bibliotek przenośnych, NuGet 2.1 udostępnia nowe monikerów framework dla projektów zarówno Sklepu Windows 8 i Windows Phone 8, a także niektóre nowe monikerów ogólne dla Sklepu Windows i Windows Phone projektów, które będą łatwiejsze zarządzanie w przyszłych wersjach odpowiednich platform.

Dla aplikacji ze Sklepu Windows 8 identyfikatory wyglądać w następujący sposób:

|NuGet 2.0 i starsze wersje|NuGet 2.1|
|----------------|-----------|
|winRT45, .NETCore45|Systemu Windows, Windows8, Windows, Windows 8|

<br/>
W przypadku projektów Windows Phone identyfikatory wyglądać w następujący sposób:

|Phone OS|NuGet 2.0 i starsze wersje|NuGet 2.1
|----------------|-----------|-----------|
|Windows Phone 7|silverlight3-wp|wp, wp7, WindowsPhone, WindowsPhone7|
|Windows Phone (Mango) w wersji 7.5|silverilght4-wp71|wp71, WindowsPhone71|
|Windows Phone 8|(nieobsługiwane)|wp8, WindowsPhone8|
<br/>
We wszystkich powyższych zmian stare nazwy framework będzie można w pełni obsługiwane przez NuGet 2.1.  Przenoszenie do przodu, nowych nazw należy używać jak będą bardziej stabilne w przyszłych wersjach odpowiednich platform. Nowe nazwy zostanie *nie* być obsługiwana w wersji NuGet przed 2.1, jednak, dlatego należy planować odpowiednio dla, kiedy należy utworzyć przełącznik.

## <a name="improved-search-in-package-manager-dialog"></a>Udoskonalonej funkcji wyszukiwania w oknie dialogowym Menedżera pakietów
W ciągu ostatnich kilku iteracji zmiany zostały wprowadzone do galerii NuGet, który znacznie ulepszona szybkość i przydatności wyszukiwania pakietu.  Jednak te ulepszenia były ograniczone do witryny sieci Web nuget.org.  NuGet 2.1 udostępnia wyszukiwania udoskonalone środowisko w oknie dialogowym Menedżer pakietów NuGet.  Na przykład załóżmy chcieli pakietu Windows Azure buforowanie w wersji zapoznawczej.  Zapytania wyszukiwania uzasadnione dla tego pakietu może być "Pamięć podręczna Azure".  W poprzednich wersjach okno dialogowe Menedżera pakietów żądanego pakietu nie będzie nawet widoczna na pierwszej stronie wyników.  Jednak w NuGet 2.1 żądany pakiet teraz zostaną wyświetlone u góry wyników wyszukiwania.

![Wyszukiwanie okna dialogowego Menedżera pakietów](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>Wymuszanie pakietu aktualizacji
Przed NuGet 2.1 NuGet może pominąć aktualizowanie pakietu, gdy wystąpił nie numer wersji wysoki.  To wprowadzone tarcia w niektórych scenariuszach — szczególnie w przypadku kompilacji lub CI scenariuszy, w miejsce zespołu nie chcesz zwiększyć numer wersji pakietu liczba dla każdej kompilacji.  Zachowanie było wymusić aktualizację bez względu na to.  NuGet 2.1 rozwiązuje ten problem z flagą "ponownie".  Na przykład poprzednie wersje programu NuGet spowoduje następujące podczas próby aktualizacji pakietu, który nie ma nowszą wersję pakietu:

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

Przy użyciu flagi ponownie zainstaluj pakiet zostanie zaktualizowany niezależnie od tego, czy dostępna jest nowsza wersja.

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

Inny scenariusz, w których flagi reinstall okaże się korzystne jest framework ponownie docelowych. Po zmianie platformy docelowej projektu (na przykład z 4 .NET 4.5 .NET), pakiet aktualizacji-Zainstaluj ponownie można zaktualizować odwołania do poprawne zestawów dla wszystkich pakietów NuGet zainstalowanych w projekcie.

## <a name="edit-package-sources-within-visual-studio"></a>Edycja źródła pakietów w programie Visual Studio
W poprzednich wersjach programu NuGet aktualizowanie źródła pakietu z wewnątrz okno dialogowe Opcje programu Visual Studio wymagane usunięcie i ponowne dodanie źródła pakietu.  NuGet 2.1 poprawia ten przepływ pracy dzięki obsłudze aktualizacji w pierwszej klasie funkcji interfejsu użytkownika konfiguracji.

![Okno dialogowe konfiguracji Menedżera pakietów](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Poprawki błędów
NuGet 2.1 zawiera wiele poprawek usterek. Pełną listę prac elementów usunięto w wersji NuGet 2.0, sprawdź widok [NuGet Tracker problem w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
