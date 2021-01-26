---
title: Informacje o wersji narzędzia NuGet 2,1
description: Informacje o wersji programu NuGet 2,1, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777031"
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="ed032-103">Informacje o wersji narzędzia NuGet 2,1</span><span class="sxs-lookup"><span data-stu-id="ed032-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="ed032-104">Informacje o wersji narzędzia [NuGet 2,0](../release-notes/nuget-2.0.md)  |  [Informacje o wersji narzędzia NuGet 2,2](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="ed032-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="ed032-105">Pakiet NuGet 2,1 został wydaną 4 października 2012.</span><span class="sxs-lookup"><span data-stu-id="ed032-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="ed032-106">Nuget.Config hierarchiczne</span><span class="sxs-lookup"><span data-stu-id="ed032-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="ed032-107">Pakiet NuGet 2,1 zapewnia większą elastyczność kontrolowania ustawień NuGet w drodze cyklicznego powiększania struktury folderów szukających `NuGet.Config` plików, a następnie tworzenia konfiguracji z zestawu wszystkich odnalezionych plików.</span><span class="sxs-lookup"><span data-stu-id="ed032-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="ed032-108">Przykładowo Rozważmy scenariusz, w którym zespół ma wewnętrzne repozytorium pakietów dla kompilacji CI innych zależności wewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="ed032-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="ed032-109">Struktura folderów dla pojedynczego projektu może wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="ed032-109">The folder structure for an individual project might look like the following:</span></span>

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

<span data-ttu-id="ed032-110">Ponadto jeśli dla rozwiązania włączono funkcję przywracania pakietów, istnieje również następujący folder:</span><span class="sxs-lookup"><span data-stu-id="ed032-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

```
C:\myteam\solution1\.nuget
```

<span data-ttu-id="ed032-111">Aby można było udostępnić wewnętrzne repozytorium pakietów dla wszystkich projektów, na których pracuje zespół, bez udostępniania go dla każdego projektu na komputerze, możemy utworzyć nowy plik Nuget.Config i umieścić go w folderze c:\myteam.</span><span class="sxs-lookup"><span data-stu-id="ed032-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="ed032-112">Nie istnieje sposób, aby określony folder pakietów dla projektu.</span><span class="sxs-lookup"><span data-stu-id="ed032-112">There is no way to specificy a packages folder per project.</span></span>

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

<span data-ttu-id="ed032-113">Teraz możemy zobaczyć, że źródło zostało dodane przez uruchomienie polecenia "nuget.exe sources" z dowolnego folderu poniżej c:\myteam, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="ed032-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![Źródła pakietów z konfiguracji nadrzędnej programu NuGet](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="ed032-115">`NuGet.Config` pliki są wyszukiwane w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="ed032-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="ed032-116">Przechodzenie cykliczne z folderu projektu do katalogu głównego</span><span class="sxs-lookup"><span data-stu-id="ed032-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="ed032-117">Global `Nuget.Config` ( `%appdata%\NuGet\Nuget.Config` )</span><span class="sxs-lookup"><span data-stu-id="ed032-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="ed032-118">Konfiguracje są stosowane w *odwrotnej kolejności*, co oznacza, że na podstawie powyższego porządku zostanie najpierw zastosowana globalna Nuget.Config, a następnie odnalezione pliki Nuget.Config z katalogu głównego do folderu projektu, a następnie `.nuget\Nuget.Config` .</span><span class="sxs-lookup"><span data-stu-id="ed032-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="ed032-119">Jest to szczególnie ważne, jeśli używasz `<clear/>` elementu do usuwania zestawu elementów z konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ed032-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="ed032-120">Określ lokalizację folderu "Packages"</span><span class="sxs-lookup"><span data-stu-id="ed032-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="ed032-121">W przeszłości program NuGet zarządzał pakietami rozwiązań z znanego folderu "Packages" znajdującego się pod folderem głównym rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ed032-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="ed032-122">W przypadku zespołów programistycznych, które mają wiele różnych rozwiązań z zainstalowanymi pakietami NuGet, może to spowodować zainstalowanie tego samego pakietu w wielu różnych miejscach w systemie plików.</span><span class="sxs-lookup"><span data-stu-id="ed032-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="ed032-123">Program NuGet 2,1 zapewnia bardziej szczegółową kontrolę nad lokalizacją folderu Packages za pośrednictwem `repositoryPath` elementu w `NuGet.Config` pliku.</span><span class="sxs-lookup"><span data-stu-id="ed032-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="ed032-124">Korzystając z powyższego przykładu wsparcia Nuget.Config hierarchicznego, założono, że wszystkie projekty w obszarze C:\myteam\ korzystają z tego samego folderu Packages.</span><span class="sxs-lookup"><span data-stu-id="ed032-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="ed032-125">Aby to osiągnąć, po prostu Dodaj następujący wpis do `c:\myteam\Nuget.Config` .</span><span class="sxs-lookup"><span data-stu-id="ed032-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="ed032-126">W tym przykładzie udostępniony `Nuget.Config` plik określa folder pakietów udostępnionych dla każdego projektu, który jest tworzony pod C:\myteam, bez względu na głębokość.</span><span class="sxs-lookup"><span data-stu-id="ed032-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="ed032-127">Należy pamiętać, że jeśli masz folder pakietów znajdujący się pod elementem głównym rozwiązania, musisz go usunąć, zanim pakiet NuGet umieści pakiety w nowej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="ed032-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="ed032-128">Obsługa bibliotek przenośnych</span><span class="sxs-lookup"><span data-stu-id="ed032-128">Support for Portable Libraries</span></span>

<span data-ttu-id="ed032-129">[Biblioteki przenośne](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) to funkcja, która została wprowadzona najpierw z platformą .NET 4, która umożliwia tworzenie zestawów, które mogą współdziałać bez modyfikacji na różnych platformach firmy Microsoft, od wersji The.NET Framework do Silverlight do Windows Phone i nawet dla konsoli Xbox 360</span><span class="sxs-lookup"><span data-stu-id="ed032-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="ed032-130">Rozszerzając [konwencje pakietu](../create-packages/supporting-multiple-target-frameworks.md) dla wersji i profilów struktury, program NuGet 2,1 obsługuje teraz przenośne biblioteki, umożliwiając tworzenie pakietów, które mają foldery programu złożonej struktury i profil docelowy `lib` .</span><span class="sxs-lookup"><span data-stu-id="ed032-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="ed032-131">Rozważmy na przykład następujące Platformy docelowe dostępne w bibliotece klas przenośnych.</span><span class="sxs-lookup"><span data-stu-id="ed032-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![Okno dialogowe tworzenia biblioteki przenośnej](./media/releasenotes-21-plib.png)

<span data-ttu-id="ed032-133">Po skompilowaniu biblioteki i `nuget.exe pack MyPortableProject.csproj` uruchomieniu polecenia można zobaczyć nową strukturę folderu przenośnego pakietu biblioteki, sprawdzając zawartość wygenerowanego pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="ed032-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![Układ pakietu biblioteki przenośnej](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="ed032-135">Jak widać, konwencja nazw folderu biblioteki przenośnej jest zgodna ze wzorcem "Portable-{Framework 1} + {Framework n}", w której identyfikatory struktury są zgodne z istniejącymi [nazwami i konwencjami dotyczącymi wersji platformy](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="ed032-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="ed032-136">Jeden wyjątek od konwencji nazw i wersji znajduje się w identyfikatorze platformy używanym do Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="ed032-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="ed032-137">Moniker powinien używać nazwy platformy "wp" (WP7, wp71 lub WP8).</span><span class="sxs-lookup"><span data-stu-id="ed032-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="ed032-138">Na przykład przy użyciu polecenia "Silverlight-WP7" spowoduje to wystąpienie błędu.</span><span class="sxs-lookup"><span data-stu-id="ed032-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="ed032-139">Podczas instalowania pakietu, który jest tworzony na podstawie tej struktury folderów, pakiet NuGet może teraz zastosować jego strukturę i reguły profilu do wielu obiektów docelowych, jak określono w nazwie folderu.</span><span class="sxs-lookup"><span data-stu-id="ed032-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="ed032-140">Za reguły dopasowywania narzędzia NuGet jest zasada, że "bardziej specyficzne" cel będzie miał pierwszeństwo przed "mniej konkretnymi".</span><span class="sxs-lookup"><span data-stu-id="ed032-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="ed032-141">Oznacza to, że monikere ukierunkowane na konkretną platformę zawsze są preferowane w przypadku urządzeń przenośnych, jeśli są one zgodne z projektem.</span><span class="sxs-lookup"><span data-stu-id="ed032-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="ed032-142">Ponadto jeśli wiele przenośnych obiektów docelowych jest zgodnych z projektem, pakiet NuGet woli, że zestaw obsługiwanych platform jest "najbliższy" w projekcie odwołującym się do pakietu.</span><span class="sxs-lookup"><span data-stu-id="ed032-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="ed032-143">Ukierunkowane projekty systemu Windows 8 i Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="ed032-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="ed032-144">Oprócz dodawania obsługi docelowych projektów bibliotek, program NuGet 2,1 udostępnia nowe monikery struktury dla projektów systemu Windows 8 i Windows Phone 8, a także kilka nowych ogólnych monikerów dla projektów sklepu Windows i Windows Phone, które będą łatwiejsze do zarządzania w przyszłych wersjach odpowiednich platform.</span><span class="sxs-lookup"><span data-stu-id="ed032-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="ed032-145">W przypadku aplikacji ze sklepu Windows 8 identyfikatory wyglądają następująco:</span><span class="sxs-lookup"><span data-stu-id="ed032-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="ed032-146">Pakiet NuGet 2,0 i wcześniejsze</span><span class="sxs-lookup"><span data-stu-id="ed032-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="ed032-147">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="ed032-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="ed032-148">winRT45, . NETCore45</span><span class="sxs-lookup"><span data-stu-id="ed032-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="ed032-149">Windows, Windows8, win, Win8</span><span class="sxs-lookup"><span data-stu-id="ed032-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="ed032-150">W przypadku projektów Windows Phone identyfikatory wyglądają następująco:</span><span class="sxs-lookup"><span data-stu-id="ed032-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="ed032-151">Telefon SYSTEMowy</span><span class="sxs-lookup"><span data-stu-id="ed032-151">Phone OS</span></span> | <span data-ttu-id="ed032-152">Pakiet NuGet 2,0 i wcześniejsze</span><span class="sxs-lookup"><span data-stu-id="ed032-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="ed032-153">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="ed032-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed032-154">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="ed032-154">Windows Phone 7</span></span> | <span data-ttu-id="ed032-155">silverlight3-WP</span><span class="sxs-lookup"><span data-stu-id="ed032-155">silverlight3-wp</span></span> | <span data-ttu-id="ed032-156">WP, WP7, WindowsPhone, WindowsPhone7</span><span class="sxs-lookup"><span data-stu-id="ed032-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="ed032-157">Windows Phone 7,5 (mango)</span><span class="sxs-lookup"><span data-stu-id="ed032-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="ed032-158">silverlight4-wp71</span><span class="sxs-lookup"><span data-stu-id="ed032-158">silverlight4-wp71</span></span> | <span data-ttu-id="ed032-159">wp71, WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="ed032-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="ed032-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="ed032-160">Windows Phone 8</span></span> | <span data-ttu-id="ed032-161">(nieobsługiwane)</span><span class="sxs-lookup"><span data-stu-id="ed032-161">(not supported)</span></span> | <span data-ttu-id="ed032-162">WP8, WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="ed032-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="ed032-163">We wszystkich powyższych zmianach nazwy starych struktur będą nadal w pełni obsługiwane przez program NuGet 2,1.</span><span class="sxs-lookup"><span data-stu-id="ed032-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="ed032-164">Po przeniesieniu do przodu nowe nazwy powinny być używane, ponieważ będą bardziej stabilne w przyszłych wersjach odpowiednich platform.</span><span class="sxs-lookup"><span data-stu-id="ed032-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="ed032-165">Nowe nazwy *nie* będą obsługiwane w wersjach programu NuGet wcześniejszych niż 2,1, dlatego należy zaplanować odpowiednie dla momentu przełączenia.</span><span class="sxs-lookup"><span data-stu-id="ed032-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="ed032-166">Ulepszone wyszukiwanie w oknie dialogowym Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="ed032-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="ed032-167">W ciągu ostatnich kilku iteracji wprowadzono zmiany w galerii NuGet, które znacznie poprawiły szybkość i przydatność wyszukiwania pakietów.</span><span class="sxs-lookup"><span data-stu-id="ed032-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="ed032-168">Jednak te ulepszenia zostały ograniczone do witryny sieci Web nuget.org.</span><span class="sxs-lookup"><span data-stu-id="ed032-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="ed032-169">Pakiet NuGet 2,1 zapewnia udoskonalone środowisko wyszukiwania dostępne za pomocą okna dialogowego Menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="ed032-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="ed032-170">Załóżmy na przykład, że chcesz znaleźć pakiet zapoznawczy usługi Windows Azure w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="ed032-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="ed032-171">Odpowiednie zapytanie wyszukiwania dla tego pakietu może być "Azure cache".</span><span class="sxs-lookup"><span data-stu-id="ed032-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="ed032-172">W poprzednich wersjach okna dialogowego Menedżera pakietów żądany pakiet nie będzie nawet wyświetlany na pierwszej stronie wyników.</span><span class="sxs-lookup"><span data-stu-id="ed032-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="ed032-173">Jednak w programie NuGet 2,1 żądany pakiet jest teraz wyświetlany w górnej części wyników wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="ed032-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![Wyszukiwanie okna dialogowego Menedżera pakietów](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="ed032-175">Wymuś aktualizację pakietu</span><span class="sxs-lookup"><span data-stu-id="ed032-175">Force Package Update</span></span>

<span data-ttu-id="ed032-176">Przed pakietem NuGet 2,1, pakiet NuGet pominie aktualizację pakietu, gdy nie jest dostępny żaden wysoki numer wersji.</span><span class="sxs-lookup"><span data-stu-id="ed032-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="ed032-177">W przypadku niektórych scenariuszy — w szczególności w przypadku scenariuszy kompilacji lub tworzenia, w których zespół nie chce zwiększyć numeru wersji pakietu przy każdej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="ed032-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="ed032-178">Odpowiednie zachowanie miało wymusić aktualizację bez względu na to, co.</span><span class="sxs-lookup"><span data-stu-id="ed032-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="ed032-179">Pakiet NuGet 2,1 dotyczy tej flagi z flagą "Zainstaluj ponownie".</span><span class="sxs-lookup"><span data-stu-id="ed032-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="ed032-180">Na przykład poprzednie wersje programu NuGet spowodują następujące próby zaktualizowania pakietu, który nie miał nowszej wersji pakietu:</span><span class="sxs-lookup"><span data-stu-id="ed032-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

<span data-ttu-id="ed032-181">Przy użyciu flagi reinstall pakiet zostanie zaktualizowany niezależnie od tego, czy jest dostępna nowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="ed032-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

<span data-ttu-id="ed032-182">Innym scenariuszem, w którym flaga ponownej instalacji udowadnia korzystne znaczenie, jest zmiana struktury.</span><span class="sxs-lookup"><span data-stu-id="ed032-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="ed032-183">W przypadku zmiany platformy docelowej projektu (na przykład z programu .NET 4 do programu .NET 4,5) Update-Package-reinstall można zaktualizować odwołania do odpowiednich zestawów dla wszystkich pakietów NuGet zainstalowanych w projekcie.</span><span class="sxs-lookup"><span data-stu-id="ed032-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="ed032-184">Edytowanie źródeł pakietów w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ed032-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="ed032-185">W poprzednich wersjach programu NuGet aktualizowanie źródła pakietu z poziomu okna dialogowego Opcje programu Visual Studio wymagało usunięcia i ponownego dodania źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="ed032-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="ed032-186">Pakiet NuGet 2,1 usprawnia ten przepływ pracy, obsługując aktualizację jako pierwszą funkcję klasy interfejsu użytkownika konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ed032-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![Okno dialogowe konfiguracji Menedżera pakietów](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="ed032-188">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="ed032-188">Bug Fixes</span></span>

<span data-ttu-id="ed032-189">Pakiet NuGet 2,1 zawiera wiele poprawek błędów.</span><span class="sxs-lookup"><span data-stu-id="ed032-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="ed032-190">Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 2,0, zobacz [Śledzenie problemów NuGet dla tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="ed032-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
