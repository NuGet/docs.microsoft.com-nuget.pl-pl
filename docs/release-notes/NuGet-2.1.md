---
title: Informacje o wersji 2.1 NuGet
description: Informacje o wersji programu NuGet 2.1 tym znanych problemów, poprawki, dodatkowe funkcje i dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3b7a000098a7362f4b1c2c4072c6cd1468baf9b5
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2018
ms.locfileid: "32044811"
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="20871-103">Informacje o wersji 2.1 NuGet</span><span class="sxs-lookup"><span data-stu-id="20871-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="20871-104">[Informacje o wersji NuGet 2.0](../release-notes/nuget-2.0.md) | [NuGet 2.2 informacje o wersji](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="20871-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="20871-105">NuGet 2.1 został wydany 4 października 2012.</span><span class="sxs-lookup"><span data-stu-id="20871-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="20871-106">Hierarchiczna pliku Nuget.Config.</span><span class="sxs-lookup"><span data-stu-id="20871-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="20871-107">NuGet 2.1 zapewnia większą elastyczność w kontrolowanie ustawień NuGet i rekursywnie przejście zapasowej struktury folderów wyszukiwania `NuGet.Config` plików i następnie budowanie konfiguracji z zestawu wszystkich znalezionych plików.</span><span class="sxs-lookup"><span data-stu-id="20871-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="20871-108">Na przykład Rozważmy scenariusz, w którym zespół ma z repozytorium pakietów wewnętrzny dla elementu konfiguracji kompilacji innych zależności wewnętrzne.</span><span class="sxs-lookup"><span data-stu-id="20871-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="20871-109">Struktura folderów dla pojedynczego projektu może wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="20871-109">The folder structure for an individual project might look like the following:</span></span>

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

<span data-ttu-id="20871-110">Ponadto jeśli Przywracanie pakietów jest włączone dla rozwiązania, również będą istnieć następujący folder:</span><span class="sxs-lookup"><span data-stu-id="20871-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

    C:\myteam\solution1\.nuget

<span data-ttu-id="20871-111">Aby przypisać repozytorium pakietów wewnętrznego zespołu dostępne dla wszystkich projektów, które zespół pracuje podczas nie czym będzie dostępna dla każdego projektu na komputerze, firma Microsoft Utwórz nowy plik Nuget.Config i umieść go w folderze c:\myteam.</span><span class="sxs-lookup"><span data-stu-id="20871-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="20871-112">Nie istnieje sposób zdefiniuj do folderu pakietów dla projektu.</span><span class="sxs-lookup"><span data-stu-id="20871-112">There is no way to specificy a packages folder per project.</span></span>

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

<span data-ttu-id="20871-113">Możemy teraz sprawdzić, czy źródło zostało dodane, uruchamiając polecenie "nuget.exe źródła" z dowolnego folderu poniżej c:\myteam w sposób przedstawiony poniżej:</span><span class="sxs-lookup"><span data-stu-id="20871-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![Źródła pakietów z konfiguracji nadrzędnej nuget](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="20871-115">`NuGet.Config` pliki są wyszukiwane w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="20871-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="20871-116">Cykliczne zaprezentuje z folderu projektu z katalogiem głównym</span><span class="sxs-lookup"><span data-stu-id="20871-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="20871-117">Globalne `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span><span class="sxs-lookup"><span data-stu-id="20871-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="20871-118">Konfiguracje są niż stosowane w *odwracania kolejności*, oznacza to, że zgodne z kolejnością powyżej, globalnego pliku Nuget.Config czy być zastosowana jako pierwsza, następuje odnalezionych plików pliku Nuget.Config z głównym folderze projektu, a następnie przez `.nuget\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="20871-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="20871-119">Jest to szczególnie ważne, jeśli używasz `<clear/>` elementu do usunięcia zbiór elementów na podstawie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="20871-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="20871-120">Określ lokalizację folderu "packages"</span><span class="sxs-lookup"><span data-stu-id="20871-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="20871-121">W przeszłości NuGet zarządza pakietów rozwiązania z folderu znane pakietów znaleziono poniżej folderu głównego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="20871-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="20871-122">Dla zespoły deweloperów, które mają wiele różnych rozwiązań, które zostały zainstalowane pakiety NuGet może to spowodować tego samego pakietu instalowany w wielu różnych miejscach w systemie plików.</span><span class="sxs-lookup"><span data-stu-id="20871-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="20871-123">NuGet 2.1 zapewnia większą kontrolę nad lokalizację folderu pakietów za pomocą `repositoryPath` element `NuGet.Config` pliku.</span><span class="sxs-lookup"><span data-stu-id="20871-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="20871-124">Opierając się na poprzedni przykład hierarchiczna Nuget.Config pomocy technicznej, Przykładowa firma Microsoft chcesz, aby wszystkie projekty w obszarze C:\myteam\ udział w tym samym folderze pakietów.</span><span class="sxs-lookup"><span data-stu-id="20871-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="20871-125">W tym celu po prostu dodaj następujący wpis do `c:\myteam\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="20871-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="20871-126">W tym przykładzie udostępnionego `Nuget.Config` pliku Określa folder udostępniony pakietów dla każdego projektu, który jest tworzony poniżej C:\myteam, niezależnie od głębokość.</span><span class="sxs-lookup"><span data-stu-id="20871-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="20871-127">Uwaga: Jeśli masz istniejący folder pakietów poniżej katalogu głównym rozwiązanie, należy go usunąć przed NuGet spowoduje umieszczenie pakietów w nowej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="20871-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="20871-128">Obsługa bibliotek przenośnych</span><span class="sxs-lookup"><span data-stu-id="20871-128">Support for Portable Libraries</span></span>

<span data-ttu-id="20871-129">[Przenośnych bibliotek](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) to funkcja wprowadzona z .NET 4, który umożliwia tworzenie zestawów, które mogą pracować bez żadnych modyfikacji na różnych platformach firmy Microsoft, z wersji środowiska.NET Framework do Silverlight Windows Phone i nawet Xbox 360 (chociaż w tej chwili NuGet nie obsługują elementu docelowego przenośnej biblioteki konsoli Xbox).</span><span class="sxs-lookup"><span data-stu-id="20871-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="20871-130">Rozszerzając [pakietu konwencje](../create-packages/supporting-multiple-target-frameworks.md) profilów i framework w wersji NuGet 2.1 obsługuje teraz bibliotek przenośnych dzięki umożliwieniu tworzenia pakietów, które framework złożone i cel profilu `lib` folderów.</span><span class="sxs-lookup"><span data-stu-id="20871-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="20871-131">Na przykład należy wziąć pod uwagę następujące biblioteki klas przenośnych dostępnych platform.</span><span class="sxs-lookup"><span data-stu-id="20871-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![Okno dialogowe Tworzenie przenośnej biblioteki](./media/releasenotes-21-plib.png)

<span data-ttu-id="20871-133">Po utworzeniu biblioteki i polecenia `nuget.exe pack MyPortableProject.csproj` jest uruchamiana, nowy komputer przenośny struktury folderu pakietu biblioteki można wyświetlić, sprawdzając zawartość wygenerowany pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="20871-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![Biblioteka przenośna układ pakietu](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="20871-135">Jak widać, Konwencji nazwa folderu przenośnej biblioteki zgodny ze wzorcem "portable {platformy 1} + {framework n}", gdzie identyfikatory framework postępuj zgodnie z istniejącą [konwencje nazwa i wersja framework](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="20871-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="20871-136">Jedynym wyjątkiem konwencje nazwa i wersja znajduje się w identyfikator platformy używany dla Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="20871-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="20871-137">Moniker tej należy używać nazwy platformy "wp" (wp7, wp71 lub wp8).</span><span class="sxs-lookup"><span data-stu-id="20871-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="20871-138">Za pomocą "wp7 silverlight", na przykład spowoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="20871-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="20871-139">Podczas instalowania pakietu, który został utworzony na podstawie tej struktury folderów, NuGet teraz reguły można stosować jej framework i profilu do wielu elementów docelowych, jak określono w nazwie folderu.</span><span class="sxs-lookup"><span data-stu-id="20871-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="20871-140">Za regułami dopasowywania NuGet jest zasada "dokładniej" elementy docelowe mają pierwszeństwo przed "mniej" precyzyjnych.</span><span class="sxs-lookup"><span data-stu-id="20871-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="20871-141">Oznacza to, że monikerów przeznaczonych dla określonej platformy będzie zawsze preferowany nad przenośne te jeśli są zgodne z projektem.</span><span class="sxs-lookup"><span data-stu-id="20871-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="20871-142">Ponadto jeśli wiele elementów docelowych przenośnych są zgodne z projektem, NuGet preferowane jeden zestaw platformach obsługiwanych w przypadku "najbliższy" do projektu odwołanie do pakietu.</span><span class="sxs-lookup"><span data-stu-id="20871-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="20871-143">Skierowane do systemu Windows 8 i Windows Phone 8 projektów</span><span class="sxs-lookup"><span data-stu-id="20871-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="20871-144">Oprócz dodawania obsługi przeznaczonych dla projektów bibliotek przenośnych, NuGet 2.1 udostępnia nowe monikerów framework dla projektów zarówno Sklepu Windows 8 i Windows Phone 8, a także niektóre nowe monikerów ogólne dla Sklepu Windows i Windows Phone projektów, które będą łatwiejsze zarządzanie w przyszłych wersjach odpowiednich platform.</span><span class="sxs-lookup"><span data-stu-id="20871-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="20871-145">Dla aplikacji ze Sklepu Windows 8 identyfikatory wyglądać w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="20871-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="20871-146">NuGet 2.0 i starsze wersje</span><span class="sxs-lookup"><span data-stu-id="20871-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="20871-147">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="20871-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="20871-148">winRT45, .NETCore45</span><span class="sxs-lookup"><span data-stu-id="20871-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="20871-149">Systemu Windows, Windows8, Windows, Windows 8</span><span class="sxs-lookup"><span data-stu-id="20871-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="20871-150">W przypadku projektów Windows Phone identyfikatory wyglądać w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="20871-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="20871-151">Phone OS</span><span class="sxs-lookup"><span data-stu-id="20871-151">Phone OS</span></span> | <span data-ttu-id="20871-152">NuGet 2.0 i starsze wersje</span><span class="sxs-lookup"><span data-stu-id="20871-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="20871-153">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="20871-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="20871-154">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="20871-154">Windows Phone 7</span></span> | <span data-ttu-id="20871-155">silverlight3-wp</span><span class="sxs-lookup"><span data-stu-id="20871-155">silverlight3-wp</span></span> | <span data-ttu-id="20871-156">WP, WindowsPhone7 wp7, WindowsPhone,</span><span class="sxs-lookup"><span data-stu-id="20871-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="20871-157">Windows Phone (Mango) w wersji 7.5</span><span class="sxs-lookup"><span data-stu-id="20871-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="20871-158">silverlight4 wp71</span><span class="sxs-lookup"><span data-stu-id="20871-158">silverlight4-wp71</span></span> | <span data-ttu-id="20871-159">wp71, WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="20871-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="20871-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="20871-160">Windows Phone 8</span></span> | <span data-ttu-id="20871-161">(nieobsługiwane)</span><span class="sxs-lookup"><span data-stu-id="20871-161">(not supported)</span></span> | <span data-ttu-id="20871-162">wp8, WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="20871-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="20871-163">We wszystkich powyższych zmian stare nazwy framework będzie można w pełni obsługiwane przez NuGet 2.1.</span><span class="sxs-lookup"><span data-stu-id="20871-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="20871-164">Przenoszenie do przodu, nowych nazw należy używać jak będą bardziej stabilne w przyszłych wersjach odpowiednich platform.</span><span class="sxs-lookup"><span data-stu-id="20871-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="20871-165">Nowe nazwy zostanie *nie* być obsługiwana w wersji NuGet przed 2.1, jednak, dlatego należy planować odpowiednio dla, kiedy należy utworzyć przełącznik.</span><span class="sxs-lookup"><span data-stu-id="20871-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="20871-166">Udoskonalonej funkcji wyszukiwania w oknie dialogowym Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="20871-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="20871-167">W ciągu ostatnich kilku iteracji zmiany zostały wprowadzone do galerii NuGet, który znacznie ulepszona szybkość i przydatności wyszukiwania pakietu.</span><span class="sxs-lookup"><span data-stu-id="20871-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="20871-168">Jednak te ulepszenia były ograniczone do witryny sieci Web nuget.org.</span><span class="sxs-lookup"><span data-stu-id="20871-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="20871-169">NuGet 2.1 udostępnia wyszukiwania udoskonalone środowisko w oknie dialogowym Menedżer pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="20871-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="20871-170">Na przykład załóżmy chcieli pakietu Windows Azure buforowanie w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="20871-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="20871-171">Zapytania wyszukiwania uzasadnione dla tego pakietu może być "Pamięć podręczna Azure".</span><span class="sxs-lookup"><span data-stu-id="20871-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="20871-172">W poprzednich wersjach okno dialogowe Menedżera pakietów żądanego pakietu nie będzie nawet widoczna na pierwszej stronie wyników.</span><span class="sxs-lookup"><span data-stu-id="20871-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="20871-173">Jednak w NuGet 2.1 żądany pakiet teraz zostaną wyświetlone u góry wyników wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="20871-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![Wyszukiwanie okna dialogowego Menedżera pakietów](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="20871-175">Wymuszanie pakietu aktualizacji</span><span class="sxs-lookup"><span data-stu-id="20871-175">Force Package Update</span></span>

<span data-ttu-id="20871-176">Przed NuGet 2.1 NuGet może pominąć aktualizowanie pakietu, gdy wystąpił nie numer wersji wysoki.</span><span class="sxs-lookup"><span data-stu-id="20871-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="20871-177">To wprowadzone tarcia w niektórych scenariuszach — szczególnie w przypadku kompilacji lub CI scenariuszy, w miejsce zespołu nie chcesz zwiększyć numer wersji pakietu liczba dla każdej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="20871-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="20871-178">Zachowanie było wymusić aktualizację bez względu na to.</span><span class="sxs-lookup"><span data-stu-id="20871-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="20871-179">NuGet 2.1 rozwiązuje ten problem z flagą "ponownie".</span><span class="sxs-lookup"><span data-stu-id="20871-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="20871-180">Na przykład poprzednie wersje programu NuGet spowoduje następujące podczas próby aktualizacji pakietu, który nie ma nowszą wersję pakietu:</span><span class="sxs-lookup"><span data-stu-id="20871-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

<span data-ttu-id="20871-181">Przy użyciu flagi ponownie zainstaluj pakiet zostanie zaktualizowany niezależnie od tego, czy dostępna jest nowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="20871-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

<span data-ttu-id="20871-182">Inny scenariusz, w których flagi reinstall okaże się korzystne jest framework ponownie docelowych.</span><span class="sxs-lookup"><span data-stu-id="20871-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="20871-183">Po zmianie platformy docelowej projektu (na przykład z 4 .NET 4.5 .NET), pakiet aktualizacji-Zainstaluj ponownie można zaktualizować odwołania do poprawne zestawów dla wszystkich pakietów NuGet zainstalowanych w projekcie.</span><span class="sxs-lookup"><span data-stu-id="20871-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="20871-184">Edycja źródła pakietów w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="20871-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="20871-185">W poprzednich wersjach programu NuGet aktualizowanie źródła pakietu z wewnątrz okno dialogowe Opcje programu Visual Studio wymagane usunięcie i ponowne dodanie źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="20871-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="20871-186">NuGet 2.1 poprawia ten przepływ pracy dzięki obsłudze aktualizacji w pierwszej klasie funkcji interfejsu użytkownika konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="20871-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![Okno dialogowe konfiguracji Menedżera pakietów](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="20871-188">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="20871-188">Bug Fixes</span></span>

<span data-ttu-id="20871-189">NuGet 2.1 zawiera wiele poprawek usterek.</span><span class="sxs-lookup"><span data-stu-id="20871-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="20871-190">Pełną listę prac elementów usunięto w wersji NuGet 2.0, sprawdź widok [NuGet Tracker problem w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="20871-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
