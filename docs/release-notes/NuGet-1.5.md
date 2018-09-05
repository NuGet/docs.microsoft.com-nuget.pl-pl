---
title: 1,5 raza więcej wersji NuGet
description: Informacje o wersji programu NuGet 1.5, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c2b549f65e675e5fde9ae1dfea3f44f7d691a86b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548728"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="409ba-103">1,5 raza więcej wersji NuGet</span><span class="sxs-lookup"><span data-stu-id="409ba-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="409ba-104">[Informacje o wersji NuGet 1.4](../release-notes/nuget-1.4.md) | [informacjach o wersji NuGet w wersji 1.6](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="409ba-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="409ba-105">NuGet w wersji 1.5 został wydany 30 sierpnia 2011 r.</span><span class="sxs-lookup"><span data-stu-id="409ba-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="409ba-106">Funkcje</span><span class="sxs-lookup"><span data-stu-id="409ba-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="409ba-107">Szablony projektów za pomocą pakietów NuGet wstępnie zainstalowane</span><span class="sxs-lookup"><span data-stu-id="409ba-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="409ba-108">Podczas tworzenia nowego szablonu projektu ASP.NET MVC 3, biblioteki skryptów jQuery zawarty w projekcie faktycznie umieszczone tam przez instalowanie pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="409ba-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="409ba-109">Szablon projektu platformy ASP.NET MVC 3 zawiera zestaw pakietów NuGet, które mają zostać zainstalowane podczas wywoływania szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="409ba-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="409ba-110">Ta możliwość uwzględnienia pakietów NuGet za pomocą szablonu projektu jest teraz funkcją NuGet, _wszelkie_ szablonu projektu mogą teraz korzystać z.</span><span class="sxs-lookup"><span data-stu-id="409ba-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="409ba-111">Aby uzyskać więcej informacji na temat tej funkcji, przeczytaj ten [wpis na blogu autorstwa dla deweloperów funkcji](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span><span class="sxs-lookup"><span data-stu-id="409ba-111">For more details about this feature, read this [blog post by the developer of the feature](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="409ba-112">Odwołania do zestawów jawne</span><span class="sxs-lookup"><span data-stu-id="409ba-112">Explicit Assembly References</span></span>

<span data-ttu-id="409ba-113">Dodano nową `<references />` element używany jawnie określić zestawy, które w ramach pakietu powinny istnieć odwołania.</span><span class="sxs-lookup"><span data-stu-id="409ba-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="409ba-114">Jeśli na przykład dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="409ba-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="409ba-115">A następnie tylko `xunit.dll` i `xunit.extensions.dll` będzie odwoływać się z odpowiednią [podfolder framework/profile](../reference/nuspec.md#explicit-assembly-references) z `lib` folderu nawet wtedy, gdy istnieją inne zestawy w folderze.</span><span class="sxs-lookup"><span data-stu-id="409ba-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="409ba-116">Jeśli ten element zostanie pominięty, a następnie stosuje zwykłe zachowanie stosowane, czyli odwołać się do każdego zestawu w `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="409ba-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="409ba-117">__Do czego służy ta funkcja?__</span><span class="sxs-lookup"><span data-stu-id="409ba-117">__What is this feature used for?__</span></span>

<span data-ttu-id="409ba-118">Ta funkcja obsługuje tylko zestawy czasu projektowania.</span><span class="sxs-lookup"><span data-stu-id="409ba-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="409ba-119">Na przykład korzystając z kontraktów kodu, zestawów umowy muszą być obok zestawów środowiska uruchomieniowego, które mogą rozszerzyć, aby je znaleźć programu Visual Studio, ale zestawy kontraktu nie powinien rzeczywiście odwoływać się do projektu i nie powinien być skopiowany do `bin` folderu.</span><span class="sxs-lookup"><span data-stu-id="409ba-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="409ba-120">Podobnie funkcja może służyć do dla struktur testów jednostek, takich jak XUnit, które należy jego zestawy narzędzi do znajdujące się obok zestawów środowiska uruchomieniowego, ale wyłączone z odwołaniami do projektów.</span><span class="sxs-lookup"><span data-stu-id="409ba-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="409ba-121">Dodano możliwość Wyklucz pliki zawarte w .nuspec</span><span class="sxs-lookup"><span data-stu-id="409ba-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="409ba-122">`<file>` Elemencie `.nuspec` pliku może służyć do określonego pliku lub zestawu plików przy użyciu symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="409ba-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="409ba-123">Korzystając z symbolem wieloznacznym, nie istnieje żaden sposób, aby wykluczyć określony podzbiór dołączone pliki.</span><span class="sxs-lookup"><span data-stu-id="409ba-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="409ba-124">Na przykład załóżmy, że chcesz, aby wszystkie pliki tekstowe, w folderze, z wyjątkiem jeden z nich.</span><span class="sxs-lookup"><span data-stu-id="409ba-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="409ba-125">Użyj średników do określenia wielu plików.</span><span class="sxs-lookup"><span data-stu-id="409ba-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="409ba-126">Lub użyj symbolu wieloznacznego, aby wykluczyć zestaw plików, takich jak wszystkie pliki kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="409ba-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="409ba-127">Usuwanie pakietów, korzystając z okna dialogowego monituje o usunięcie zależności</span><span class="sxs-lookup"><span data-stu-id="409ba-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="409ba-128">Podczas odinstalowywania pakietu z zależnościami, wyświetli NuGet, dzięki czemu usuwanie zależności pakietu wraz z pakietu.</span><span class="sxs-lookup"><span data-stu-id="409ba-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Usuwanie pakietów zależnych](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="409ba-130">`Get-Package` polecenie poprawy</span><span class="sxs-lookup"><span data-stu-id="409ba-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="409ba-131">`Get-Package` Polecenie obsługuje teraz `-ProjectName` parametru.</span><span class="sxs-lookup"><span data-stu-id="409ba-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="409ba-132">To polecenie</span><span class="sxs-lookup"><span data-stu-id="409ba-132">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="409ba-133">zostanie wyświetlona lista wszystkich pakietów zainstalowany w projekcie A.</span><span class="sxs-lookup"><span data-stu-id="409ba-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="409ba-134">Obsługa serwerów proxy, które wymagają uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="409ba-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="409ba-135">Gdy za pomocą narzędzia NuGet za serwerem proxy, który wymaga uwierzytelniania, NuGet będzie teraz powodować wyświetlenie monitu o poświadczenia serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="409ba-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="409ba-136">Wprowadzanie poświadczeń umożliwia rozszerzenie NuGet, aby nawiązać połączenie z repozytorium zdalnego.</span><span class="sxs-lookup"><span data-stu-id="409ba-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="409ba-137">Obsługa repozytoria, które wymagają uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="409ba-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="409ba-138">Pakiet NuGet obsługuje obecnie nawiązywania połączenia z [repozytoriów prywatnych](../hosting-packages/local-feeds.md) wymagające basic lub uwierzytelnianie NTLM.</span><span class="sxs-lookup"><span data-stu-id="409ba-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="409ba-139">Obsługa uwierzytelniania szyfrowanego zostanie dodana w przyszłej wersji.</span><span class="sxs-lookup"><span data-stu-id="409ba-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="409ba-140">Ulepszenia wydajności w repozytorium nuget.org</span><span class="sxs-lookup"><span data-stu-id="409ba-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="409ba-141">Wprowadziliśmy kilka ulepszeń wydajności do galerii nuget.org, aby utworzyć pakiet sporządzanie list i szybsze wyszukiwanie.</span><span class="sxs-lookup"><span data-stu-id="409ba-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="409ba-142">Filtrowanie projektu okna dialogowego rozwiązań</span><span class="sxs-lookup"><span data-stu-id="409ba-142">Solution dialog project filtering</span></span>
<span data-ttu-id="409ba-143">W poziomie rozwiązania okna dialogowego, monitując o jakie projektów zainstalować możemy wyświetlić tylko projekty, które są zgodne z wybranym pakietem.</span><span class="sxs-lookup"><span data-stu-id="409ba-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="409ba-144">Informacje o wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="409ba-144">Package Release Notes</span></span>
<span data-ttu-id="409ba-145">Pakiety NuGet teraz obejmują wsparcie dla wersji.</span><span class="sxs-lookup"><span data-stu-id="409ba-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="409ba-146">Informacje o wersji przedstawiać tylko się podczas wyświetlania _aktualizacje_ pakietu, więc nie ma sensu je dodać do swojej pierwszej wersji.</span><span class="sxs-lookup"><span data-stu-id="409ba-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Informacje o wersji na karcie Aktualizacje](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="409ba-148">Aby dodać informacje o wersji do pakietu, należy użyć nowego `<releaseNotes />` elementu metadanych w pliku NuSpec.</span><span class="sxs-lookup"><span data-stu-id="409ba-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="409ba-149">.nuspec & ltfiles /&gt; poprawy</span><span class="sxs-lookup"><span data-stu-id="409ba-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="409ba-150">`.nuspec` Pliku teraz umożliwia pusty `<files />` element, który informuje nuget.exe Aby nie zawiera plików w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="409ba-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="409ba-151">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="409ba-151">Bug Fixes</span></span>
<span data-ttu-id="409ba-152">NuGet w wersji 1.5 miał daje w sumie 107 stałej elementów roboczych.</span><span class="sxs-lookup"><span data-stu-id="409ba-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="409ba-153">103 te zostały oznaczone jako błędy.</span><span class="sxs-lookup"><span data-stu-id="409ba-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="409ba-154">Aby uzyskać pełną listę prac elementy rozwiązane w NuGet w wersji 1.5, widok [NuGet narzędzie do śledzenia problemów w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="409ba-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="409ba-155">Poprawki błędów warte odnotowania:</span><span class="sxs-lookup"><span data-stu-id="409ba-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="409ba-156">[Problem 1273](http://nuget.codeplex.com/workitem/1273): wprowadzone `packages.config` większą kontrolę wersji, przyjazne sortowanie alfabetyczne pakietów i usuwając dodatkowych spacji.</span><span class="sxs-lookup"><span data-stu-id="409ba-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="409ba-157">[Problem 844](http://nuget.codeplex.com/workitem/844): numery wersji są teraz znormalizowane tak, aby `Install-Package 1.0` działa na pakiet z wersją `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="409ba-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="409ba-158">[Problem 1060](http://nuget.codeplex.com/workitem/1060): podczas tworzenia pakietu przy użyciu nuget.exe, `-Version` Flaga zastąpienia `<version />` elementu.</span><span class="sxs-lookup"><span data-stu-id="409ba-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
