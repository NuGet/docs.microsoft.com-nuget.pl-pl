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
# <a name="nuget-21-release-notes"></a><span data-ttu-id="64d54-103">Informacje o wersji 2.1 NuGet</span><span class="sxs-lookup"><span data-stu-id="64d54-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="64d54-104">[Informacje o wersji NuGet w wersji 2.0](../release-notes/nuget-2.0.md) | [informacjach o wersji NuGet 2.2](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="64d54-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="64d54-105">NuGet 2.1 został wydany 4 października 2012.</span><span class="sxs-lookup"><span data-stu-id="64d54-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="64d54-106">Hierarchiczna pliku Nuget.Config.</span><span class="sxs-lookup"><span data-stu-id="64d54-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="64d54-107">NuGet 2.1 zapewnia większą elastyczność w kontrolowaniu ustawienia NuGet za pomocą rekursywnie zalet się strukturę folderów, wyszukiwanie `NuGet.Config` plików, a następnie kompilując konfiguracji z zestawu wszystkich znalezionych plików.</span><span class="sxs-lookup"><span data-stu-id="64d54-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="64d54-108">Na przykład Rozważmy scenariusz, w którym zespół ma repozytorium wewnętrznego pakietów dla kompilacji ciągłej integracji innych zależności wewnętrzne.</span><span class="sxs-lookup"><span data-stu-id="64d54-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="64d54-109">Struktura folderów dla pojedynczego projektu może wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="64d54-109">The folder structure for an individual project might look like the following:</span></span>

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

<span data-ttu-id="64d54-110">Ponadto jeśli przywracania pakietów jest włączone dla rozwiązania, również będzie istnieć następujący folder:</span><span class="sxs-lookup"><span data-stu-id="64d54-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

    C:\myteam\solution1\.nuget

<span data-ttu-id="64d54-111">Aby mogła mieć repozytorium pakietów wewnętrznego zespołu jest dostępne dla wszystkich projektów, które zespół nad nimi pracuje jednocześnie nie dostępne dla każdego projektu na komputerze, możemy utworzyć nowy plik Nuget.Config i umieść go w folderze c:\myteam.</span><span class="sxs-lookup"><span data-stu-id="64d54-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="64d54-112">Nie ma możliwości występowaniem do folderu pakietów na projekt.</span><span class="sxs-lookup"><span data-stu-id="64d54-112">There is no way to specificy a packages folder per project.</span></span>

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

<span data-ttu-id="64d54-113">Teraz widać, czy źródłowy został dodany, uruchamiając polecenie "nuget.exe źródła" z dowolnego folderu poniżej c:\myteam jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="64d54-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![Źródła pakietu z konfiguracji nuget nadrzędnej](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="64d54-115">`NuGet.Config` pliki są wyszukiwane w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="64d54-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="64d54-116">Cykliczne zapoznaj się z folderu projektu do katalogu głównego</span><span class="sxs-lookup"><span data-stu-id="64d54-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="64d54-117">Globalne `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span><span class="sxs-lookup"><span data-stu-id="64d54-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="64d54-118">Konfiguracje są niż stosowane *odwrócić kolejność*, co oznacza, że w oparciu o kolejność powyżej, globalnego pliku Nuget.Config może być stosowane w pierwszej kolejności, następuje odnalezione pliku Nuget.Config pliki z katalogu głównego do folderu projektu, a następnie przez `.nuget\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="64d54-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="64d54-119">Jest to szczególnie ważne, jeśli używasz `<clear/>` elementu do usunięcia jest zestaw elementów z konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="64d54-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="64d54-120">Określ "pakietami" Lokalizacja folderu</span><span class="sxs-lookup"><span data-stu-id="64d54-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="64d54-121">W przeszłości NuGet zarządzane pakietów rozwiązań z folderu znanych pakietów znaleziono poniżej folderu głównego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="64d54-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="64d54-122">Dla zespołów deweloperskich, które mają wiele różnych rozwiązań, które zostały zainstalowane pakiety NuGet może to spowodować tego samego pakietu instalowany w wielu różnych miejscach w systemie plików.</span><span class="sxs-lookup"><span data-stu-id="64d54-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="64d54-123">NuGet 2.1 zapewnia bardziej precyzyjną kontrolę nad lokalizacji folderu pakietów za pomocą `repositoryPath` element `NuGet.Config` pliku.</span><span class="sxs-lookup"><span data-stu-id="64d54-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="64d54-124">Opierając się na poprzednim przykładzie hierarchiczne obsługę pliku Nuget.Config, przyjęto założenie, firma Microsoft chce mieć wszystkie projekty w ramach C:\myteam\ udział w tym samym folderze pakietów.</span><span class="sxs-lookup"><span data-stu-id="64d54-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="64d54-125">W tym celu po prostu dodaj następujący wpis do `c:\myteam\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="64d54-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="64d54-126">W tym przykładzie wspólnie `Nuget.Config` plik Określa folder udostępnionych pakietów dla każdego projektu, który jest tworzony poniżej C:\myteam, niezależnie od głębokości.</span><span class="sxs-lookup"><span data-stu-id="64d54-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="64d54-127">Uwaga: Jeśli masz istniejący folder packages poniżej główny rozwiązania, należy go usunąć przed NuGet spowoduje umieszczenie pakietów w nowej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="64d54-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="64d54-128">Obsługa bibliotek przenośnych</span><span class="sxs-lookup"><span data-stu-id="64d54-128">Support for Portable Libraries</span></span>

<span data-ttu-id="64d54-129">[Przenośne biblioteki](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) to funkcja wprowadzona przy użyciu .NET 4, która umożliwia tworzenie zestawów, które mogą działać bez żadnych modyfikacji na różnych platformach firmy Microsoft, z wersji środowiska.NET Framework do programu Silverlight, Windows Phone i Xbox nawet 360 (choć w tej chwili NuGet nie obsługuje docelowej przenośnej biblioteki Xbox).</span><span class="sxs-lookup"><span data-stu-id="64d54-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="64d54-130">Rozszerzając [pakietu konwencje](../create-packages/supporting-multiple-target-frameworks.md) profilów i framework w wersji NuGet 2.1 obsługuje obecnie przenośnych bibliotek, umożliwiając tworzenie pakietów, które mają złożone framework i profil docelowy `lib` folderów.</span><span class="sxs-lookup"><span data-stu-id="64d54-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="64d54-131">Na przykład należy wziąć pod uwagę następujące biblioteki klas przenośnych dostępnych platform.</span><span class="sxs-lookup"><span data-stu-id="64d54-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![Okno dialogowe tworzenia bibliotek przenośnych](./media/releasenotes-21-plib.png)

<span data-ttu-id="64d54-133">Po utworzeniu biblioteki oraz polecenie `nuget.exe pack MyPortableProject.csproj` jest uruchamiana, nowy komputer przenośny widać strukturę folderu pakietu biblioteki, sprawdzając zawartość wygenerowany pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="64d54-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![Układ pakietu przenośnej biblioteki](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="64d54-135">Jak widać, Konwencji nazwy folderu przenośnej biblioteki jest zgodny ze wzorcem "przenośnych — {struktury 1} + {framework n}" gdzie identyfikatory framework postępuj zgodnie z istniejącą [konwencje nazwa i wersja framework](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="64d54-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="64d54-136">Jedynym wyjątkiem Konwencji nazwy i wersji można znaleźć w identyfikatora struktury, używane dla Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="64d54-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="64d54-137">Tej krótkiej nazwy powinny używać nazwy framework "wp" (wp7, wp71 lub wp8).</span><span class="sxs-lookup"><span data-stu-id="64d54-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="64d54-138">Na przykład za pomocą "wp7 silverlight", spowoduje wystąpienie błędu.</span><span class="sxs-lookup"><span data-stu-id="64d54-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="64d54-139">Podczas instalowania pakietu, który jest utworzony na podstawie tej struktury folderów, NuGet teraz je zastosować regułach framework i profile do wielu celów, jak określono w nazwie folderu.</span><span class="sxs-lookup"><span data-stu-id="64d54-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="64d54-140">Za reguł dopasowania NuGet jest zasada "bardziej szczegółowe" elementy docelowe mają pierwszeństwo przed tymi "specyficzne dla języka less".</span><span class="sxs-lookup"><span data-stu-id="64d54-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="64d54-141">Oznacza to, że monikerów przeznaczonych dla określonej platformy będzie zawsze preferowany nad tymi przenośne jeśli są zgodne z projektem.</span><span class="sxs-lookup"><span data-stu-id="64d54-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="64d54-142">Ponadto jeśli wiele elementów docelowych przenośnych są zgodne z projektem, NuGet zostanie Preferuj jeden, gdzie zestaw obsługiwane platformy to "najbliższy" do projektu odwołanie do pakietu.</span><span class="sxs-lookup"><span data-stu-id="64d54-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="64d54-143">Określania wartości docelowej systemu Windows 8 i Windows Phone 8 projektów</span><span class="sxs-lookup"><span data-stu-id="64d54-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="64d54-144">Oprócz dodania obsługi przyjmowania jako celu projektów bibliotek przenośnych, NuGet 2.1 udostępnia nowe monikerów framework dla projektów systemu Windows 8 Store i Windows Phone 8, a także niektóre nowe ogólne monikery dla Windows Store i projektów Windows Phone, które będą znajdować się łatwiejsze zarządzanie w przyszłych wersjach odpowiednich platform.</span><span class="sxs-lookup"><span data-stu-id="64d54-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="64d54-145">W przypadku aplikacji systemu Windows 8 Store identyfikatory wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="64d54-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="64d54-146">NuGet 2.0 i starszych</span><span class="sxs-lookup"><span data-stu-id="64d54-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="64d54-147">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="64d54-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="64d54-148">winRT45, .NETCore45</span><span class="sxs-lookup"><span data-stu-id="64d54-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="64d54-149">Windows, Windows8, win, win8</span><span class="sxs-lookup"><span data-stu-id="64d54-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="64d54-150">W przypadku projektów Windows Phone identyfikatory wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="64d54-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="64d54-151">System operacyjny telefonu</span><span class="sxs-lookup"><span data-stu-id="64d54-151">Phone OS</span></span> | <span data-ttu-id="64d54-152">NuGet 2.0 i starszych</span><span class="sxs-lookup"><span data-stu-id="64d54-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="64d54-153">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="64d54-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="64d54-154">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="64d54-154">Windows Phone 7</span></span> | <span data-ttu-id="64d54-155">silverlight3-wp</span><span class="sxs-lookup"><span data-stu-id="64d54-155">silverlight3-wp</span></span> | <span data-ttu-id="64d54-156">WP-WindowsPhone7 wp7, WindowsPhone,</span><span class="sxs-lookup"><span data-stu-id="64d54-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="64d54-157">Windows Phone 7.5 (Mango)</span><span class="sxs-lookup"><span data-stu-id="64d54-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="64d54-158">silverlight4 wp71</span><span class="sxs-lookup"><span data-stu-id="64d54-158">silverlight4-wp71</span></span> | <span data-ttu-id="64d54-159">wp71, WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="64d54-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="64d54-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="64d54-160">Windows Phone 8</span></span> | <span data-ttu-id="64d54-161">(nieobsługiwane)</span><span class="sxs-lookup"><span data-stu-id="64d54-161">(not supported)</span></span> | <span data-ttu-id="64d54-162">wp8, WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="64d54-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="64d54-163">We wszystkich powyższych zmian starych nazw framework będzie można w pełni obsługiwane przez NuGet 2.1.</span><span class="sxs-lookup"><span data-stu-id="64d54-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="64d54-164">Przenoszenie do przodu, nowych nazw należy używać jak będą bardziej stabilne w przyszłych wersjach odpowiednich platform.</span><span class="sxs-lookup"><span data-stu-id="64d54-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="64d54-165">Nowe nazwy będą *nie* jest obsługiwana w wersji pakietu nuget przed 2.1, jednak tak właściwie przypadku przełączenia.</span><span class="sxs-lookup"><span data-stu-id="64d54-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="64d54-166">Udoskonalonej funkcji wyszukiwania w oknie dialogowym Menedżer pakietów</span><span class="sxs-lookup"><span data-stu-id="64d54-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="64d54-167">W ciągu ostatnich kilku iteracji zmiany zostały wprowadzone do galerii pakietów NuGet, który znacznie poprawia szybkość i istotność pakietu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="64d54-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="64d54-168">Jednak te ulepszenia zostały ograniczone do witryny sieci Web w witrynie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="64d54-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="64d54-169">NuGet 2.1 udostępnia ulepszone wyszukiwanie środowisko w oknie dialogowym Menedżer pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="64d54-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="64d54-170">Na przykład Wyobraź sobie chciała pakietu Windows Azure buforowania w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="64d54-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="64d54-171">Zapytanie wyszukiwania uzasadnione dla tego pakietu może być "Pamięć podręczna systemu Azure".</span><span class="sxs-lookup"><span data-stu-id="64d54-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="64d54-172">W poprzednich wersjach okno Menedżera pakietów żądanego pakietu nie będzie jeszcze widoczna na pierwszej stronie wyników.</span><span class="sxs-lookup"><span data-stu-id="64d54-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="64d54-173">Jednak w NuGet 2.1 żądanego pakietu teraz wyświetlane u góry strony wyników wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="64d54-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![Wyszukiwania okno Menedżera pakietów](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="64d54-175">Wymusić aktualizację pakietu</span><span class="sxs-lookup"><span data-stu-id="64d54-175">Force Package Update</span></span>

<span data-ttu-id="64d54-176">Przed NuGet 2.1 NuGet może pominąć aktualizowanie pakietu podczas nie jest liczbą wysokiej wersji.</span><span class="sxs-lookup"><span data-stu-id="64d54-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="64d54-177">Ogranicz liczbę problemów w przypadku niektórych scenariuszy — szczególnie w przypadku kompilacji lub scenariuszach ciągłej integracji, w których zespół nie chciały zwiększ numer kompilacji każdej wersji pakietu to wprowadzona.</span><span class="sxs-lookup"><span data-stu-id="64d54-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="64d54-178">Żądane zachowanie było wymusić aktualizację bez względu na to.</span><span class="sxs-lookup"><span data-stu-id="64d54-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="64d54-179">NuGet 2.1 rozwiązuje ten problem z flagą "Zainstaluj ponownie".</span><span class="sxs-lookup"><span data-stu-id="64d54-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="64d54-180">Na przykład poprzednich wersji programu NuGet spowoduje następujące podczas próby zaktualizowania pakietu, który nie ma nowszą wersję pakietu:</span><span class="sxs-lookup"><span data-stu-id="64d54-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

<span data-ttu-id="64d54-181">Przy użyciu flagi zainstaluj pakiet zostanie zaktualizowany niezależnie od tego, czy dostępna jest nowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="64d54-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

<span data-ttu-id="64d54-182">Inny scenariusz, w których flaga reinstall okaże się korzystne jest framework ponownego określenia wartości docelowej.</span><span class="sxs-lookup"><span data-stu-id="64d54-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="64d54-183">Po zmianie platformy docelowej projektu (na przykład z .NET 4 .NET 4.5), pakiet aktualizacji-Zainstaluj ponownie można zaktualizować odwołania do zestawów prawidłowe dla wszystkich pakietów NuGet zainstalowana w projekcie.</span><span class="sxs-lookup"><span data-stu-id="64d54-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="64d54-184">Edytowanie źródła pakietów w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="64d54-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="64d54-185">W poprzednich wersjach programu NuGet aktualizowania źródła pakietu z poziomu okna dialogowego Opcje programu Visual Studio wymagane usunięcie i ponowne dodanie źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="64d54-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="64d54-186">NuGet 2.1 zwiększa ten przepływ pracy dzięki obsłudze aktualizacji jako funkcje pierwszej klasy interfejsu użytkownika konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="64d54-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![Okno dialogowe konfiguracji Menedżera pakietów](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="64d54-188">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="64d54-188">Bug Fixes</span></span>

<span data-ttu-id="64d54-189">NuGet 2.1 obejmuje wiele poprawek błędów.</span><span class="sxs-lookup"><span data-stu-id="64d54-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="64d54-190">Aby uzyskać pełną listę prac elementy rozwiązane w NuGet w wersji 2.0, widok [NuGet narzędzie do śledzenia problemów w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="64d54-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
