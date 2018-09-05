---
title: Informacje o wersji 2.1 NuGet
description: Informacje o wersji programu NuGet 2.1, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fd6dadc7968991c77c1b06a6a261415355b2fd73
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548600"
---
# <a name="nuget-21-release-notes"></a>Informacje o wersji 2.1 NuGet

[Informacje o wersji NuGet w wersji 2.0](../release-notes/nuget-2.0.md) | [informacjach o wersji NuGet 2.2](../release-notes/nuget-2.2.md)

NuGet 2.1 został wydany 4 października 2012.

## <a name="hierarchical-nugetconfig"></a>Hierarchiczna pliku Nuget.Config.

NuGet 2.1 zapewnia większą elastyczność w kontrolowaniu ustawienia NuGet za pomocą rekursywnie zalet się strukturę folderów, wyszukiwanie `NuGet.Config` plików, a następnie kompilując konfiguracji z zestawu wszystkich znalezionych plików.  Na przykład Rozważmy scenariusz, w którym zespół ma repozytorium wewnętrznego pakietów dla kompilacji ciągłej integracji innych zależności wewnętrzne. Struktura folderów dla pojedynczego projektu może wyglądać następująco:

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

Ponadto jeśli przywracania pakietów jest włączone dla rozwiązania, również będzie istnieć następujący folder:

    C:\myteam\solution1\.nuget

Aby mogła mieć repozytorium pakietów wewnętrznego zespołu jest dostępne dla wszystkich projektów, które zespół nad nimi pracuje jednocześnie nie dostępne dla każdego projektu na komputerze, możemy utworzyć nowy plik Nuget.Config i umieść go w folderze c:\myteam. Nie ma możliwości występowaniem do folderu pakietów na projekt.

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

Teraz widać, czy źródłowy został dodany, uruchamiając polecenie "nuget.exe źródła" z dowolnego folderu poniżej c:\myteam jak pokazano poniżej:

![Źródła pakietu z konfiguracji nuget nadrzędnej](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` pliki są wyszukiwane w następującej kolejności:

1. `.nuget\Nuget.Config`
2. Cykliczne zapoznaj się z folderu projektu do katalogu głównego
3. Globalne `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)

Konfiguracje są niż stosowane *odwrócić kolejność*, co oznacza, że w oparciu o kolejność powyżej, globalnego pliku Nuget.Config może być stosowane w pierwszej kolejności, następuje odnalezione pliku Nuget.Config pliki z katalogu głównego do folderu projektu, a następnie przez `.nuget\Nuget.Config`.  Jest to szczególnie ważne, jeśli używasz `<clear/>` elementu do usunięcia jest zestaw elementów z konfiguracji.

## <a name="specify-packages-folder-location"></a>Określ "pakietami" Lokalizacja folderu

W przeszłości NuGet zarządzane pakietów rozwiązań z folderu znanych pakietów znaleziono poniżej folderu głównego rozwiązania.  Dla zespołów deweloperskich, które mają wiele różnych rozwiązań, które zostały zainstalowane pakiety NuGet może to spowodować tego samego pakietu instalowany w wielu różnych miejscach w systemie plików.

NuGet 2.1 zapewnia bardziej precyzyjną kontrolę nad lokalizacji folderu pakietów za pomocą `repositoryPath` element `NuGet.Config` pliku.  Opierając się na poprzednim przykładzie hierarchiczne obsługę pliku Nuget.Config, przyjęto założenie, firma Microsoft chce mieć wszystkie projekty w ramach C:\myteam\ udział w tym samym folderze pakietów.  W tym celu po prostu dodaj następujący wpis do `c:\myteam\Nuget.Config`.

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

W tym przykładzie wspólnie `Nuget.Config` plik Określa folder udostępnionych pakietów dla każdego projektu, który jest tworzony poniżej C:\myteam, niezależnie od głębokości. Uwaga: Jeśli masz istniejący folder packages poniżej główny rozwiązania, należy go usunąć przed NuGet spowoduje umieszczenie pakietów w nowej lokalizacji.

## <a name="support-for-portable-libraries"></a>Obsługa bibliotek przenośnych

[Przenośne biblioteki](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) to funkcja wprowadzona przy użyciu .NET 4, która umożliwia tworzenie zestawów, które mogą działać bez żadnych modyfikacji na różnych platformach firmy Microsoft, z wersji środowiska.NET Framework do programu Silverlight, Windows Phone i Xbox nawet 360 (choć w tej chwili NuGet nie obsługuje docelowej przenośnej biblioteki Xbox).  Rozszerzając [pakietu konwencje](../create-packages/supporting-multiple-target-frameworks.md) profilów i framework w wersji NuGet 2.1 obsługuje obecnie przenośnych bibliotek, umożliwiając tworzenie pakietów, które mają złożone framework i profil docelowy `lib` folderów.

Na przykład należy wziąć pod uwagę następujące biblioteki klas przenośnych dostępnych platform.

![Okno dialogowe tworzenia bibliotek przenośnych](./media/releasenotes-21-plib.png)

Po utworzeniu biblioteki oraz polecenie `nuget.exe pack MyPortableProject.csproj` jest uruchamiana, nowy komputer przenośny widać strukturę folderu pakietu biblioteki, sprawdzając zawartość wygenerowany pakiet NuGet.

![Układ pakietu przenośnej biblioteki](./media/releasenotes-21-plib-layout.png)

Jak widać, Konwencji nazwy folderu przenośnej biblioteki jest zgodny ze wzorcem "przenośnych — {struktury 1} + {framework n}" gdzie identyfikatory framework postępuj zgodnie z istniejącą [konwencje nazwa i wersja framework](../reference/target-frameworks.md). Jedynym wyjątkiem Konwencji nazwy i wersji można znaleźć w identyfikatora struktury, używane dla Windows Phone.  Tej krótkiej nazwy powinny używać nazwy framework "wp" (wp7, wp71 lub wp8). Na przykład za pomocą "wp7 silverlight", spowoduje wystąpienie błędu.

Podczas instalowania pakietu, który jest utworzony na podstawie tej struktury folderów, NuGet teraz je zastosować regułach framework i profile do wielu celów, jak określono w nazwie folderu.  Za reguł dopasowania NuGet jest zasada "bardziej szczegółowe" elementy docelowe mają pierwszeństwo przed tymi "specyficzne dla języka less".  Oznacza to, że monikerów przeznaczonych dla określonej platformy będzie zawsze preferowany nad tymi przenośne jeśli są zgodne z projektem.  Ponadto jeśli wiele elementów docelowych przenośnych są zgodne z projektem, NuGet zostanie Preferuj jeden, gdzie zestaw obsługiwane platformy to "najbliższy" do projektu odwołanie do pakietu.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Określania wartości docelowej systemu Windows 8 i Windows Phone 8 projektów

Oprócz dodania obsługi przyjmowania jako celu projektów bibliotek przenośnych, NuGet 2.1 udostępnia nowe monikerów framework dla projektów systemu Windows 8 Store i Windows Phone 8, a także niektóre nowe ogólne monikery dla Windows Store i projektów Windows Phone, które będą znajdować się łatwiejsze zarządzanie w przyszłych wersjach odpowiednich platform.

W przypadku aplikacji systemu Windows 8 Store identyfikatory wyglądać następująco:

| NuGet 2.0 i starszych | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45, .NETCore45 | Windows, Windows8, win, win8 |

<br/>
W przypadku projektów Windows Phone identyfikatory wyglądać następująco:

| System operacyjny telefonu | NuGet 2.0 i starszych | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3-wp | WP-WindowsPhone7 wp7, WindowsPhone, |
| Windows Phone 7.5 (Mango) | silverlight4 wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | (nieobsługiwane) | wp8, WindowsPhone8 |

<br/>
We wszystkich powyższych zmian starych nazw framework będzie można w pełni obsługiwane przez NuGet 2.1.  Przenoszenie do przodu, nowych nazw należy używać jak będą bardziej stabilne w przyszłych wersjach odpowiednich platform. Nowe nazwy będą *nie* jest obsługiwana w wersji pakietu nuget przed 2.1, jednak tak właściwie przypadku przełączenia.

## <a name="improved-search-in-package-manager-dialog"></a>Udoskonalonej funkcji wyszukiwania w oknie dialogowym Menedżer pakietów

W ciągu ostatnich kilku iteracji zmiany zostały wprowadzone do galerii pakietów NuGet, który znacznie poprawia szybkość i istotność pakietu wyszukiwania.  Jednak te ulepszenia zostały ograniczone do witryny sieci Web w witrynie nuget.org.  NuGet 2.1 udostępnia ulepszone wyszukiwanie środowisko w oknie dialogowym Menedżer pakietów NuGet.  Na przykład Wyobraź sobie chciała pakietu Windows Azure buforowania w wersji zapoznawczej.  Zapytanie wyszukiwania uzasadnione dla tego pakietu może być "Pamięć podręczna systemu Azure".  W poprzednich wersjach okno Menedżera pakietów żądanego pakietu nie będzie jeszcze widoczna na pierwszej stronie wyników.  Jednak w NuGet 2.1 żądanego pakietu teraz wyświetlane u góry strony wyników wyszukiwania.

![Wyszukiwania okno Menedżera pakietów](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>Wymusić aktualizację pakietu

Przed NuGet 2.1 NuGet może pominąć aktualizowanie pakietu podczas nie jest liczbą wysokiej wersji.  Ogranicz liczbę problemów w przypadku niektórych scenariuszy — szczególnie w przypadku kompilacji lub scenariuszach ciągłej integracji, w których zespół nie chciały zwiększ numer kompilacji każdej wersji pakietu to wprowadzona.  Żądane zachowanie było wymusić aktualizację bez względu na to.  NuGet 2.1 rozwiązuje ten problem z flagą "Zainstaluj ponownie".  Na przykład poprzednich wersji programu NuGet spowoduje następujące podczas próby zaktualizowania pakietu, który nie ma nowszą wersję pakietu:

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

Przy użyciu flagi zainstaluj pakiet zostanie zaktualizowany niezależnie od tego, czy dostępna jest nowsza wersja.

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

Inny scenariusz, w których flaga reinstall okaże się korzystne jest framework ponownego określenia wartości docelowej. Po zmianie platformy docelowej projektu (na przykład z .NET 4 .NET 4.5), pakiet aktualizacji-Zainstaluj ponownie można zaktualizować odwołania do zestawów prawidłowe dla wszystkich pakietów NuGet zainstalowana w projekcie.

## <a name="edit-package-sources-within-visual-studio"></a>Edytowanie źródła pakietów w programie Visual Studio

W poprzednich wersjach programu NuGet aktualizowania źródła pakietu z poziomu okna dialogowego Opcje programu Visual Studio wymagane usunięcie i ponowne dodanie źródła pakietu.  NuGet 2.1 zwiększa ten przepływ pracy dzięki obsłudze aktualizacji jako funkcje pierwszej klasy interfejsu użytkownika konfiguracji.

![Okno dialogowe konfiguracji Menedżera pakietów](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Poprawki błędów

NuGet 2.1 obejmuje wiele poprawek błędów. Aby uzyskać pełną listę prac elementy rozwiązane w NuGet w wersji 2.0, widok [NuGet narzędzie do śledzenia problemów w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
