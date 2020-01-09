---
title: Informacje o wersji narzędzia NuGet 1,5
description: Informacje o wersji programu NuGet 1,5, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940a19cdc485d611d03b52ee3102bc95a78a36bb
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383352"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="04fe9-103">Informacje o wersji narzędzia NuGet 1,5</span><span class="sxs-lookup"><span data-stu-id="04fe9-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="04fe9-104">[Informacje o wersji pakietu nuget 1,4](../release-notes/nuget-1.4.md) | [Informacje o wersji narzędzia NuGet 1,6](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="04fe9-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="04fe9-105">Pakiet NuGet 1,5 został wydaną 30 sierpnia 2011.</span><span class="sxs-lookup"><span data-stu-id="04fe9-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="04fe9-106">Funkcje</span><span class="sxs-lookup"><span data-stu-id="04fe9-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="04fe9-107">Szablony projektów ze wstępnie zainstalowanymi pakietami NuGet</span><span class="sxs-lookup"><span data-stu-id="04fe9-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="04fe9-108">Podczas tworzenia nowego szablonu projektu ASP.NET MVC 3, biblioteki skryptów jQuery zawarte w projekcie są w rzeczywistości umieszczane w tym miejscu przez zainstalowanie pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="04fe9-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="04fe9-109">Szablon projektu ASP.NET MVC 3 zawiera zestaw pakietów NuGet, które są instalowane podczas wywoływania szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="04fe9-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="04fe9-110">Ta możliwość dołączania pakietów NuGet z szablonem projektu to teraz funkcja NuGet, którą _każdy_ szablon projektu może teraz korzystać z programu.</span><span class="sxs-lookup"><span data-stu-id="04fe9-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="04fe9-111">Aby uzyskać więcej informacji na temat tej funkcji, przeczytaj ten [wpis w blogu przez dewelopera tej funkcji](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span><span class="sxs-lookup"><span data-stu-id="04fe9-111">For more details about this feature, read this [blog post by the developer of the feature](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="04fe9-112">Jawne odwołania do zestawów</span><span class="sxs-lookup"><span data-stu-id="04fe9-112">Explicit Assembly References</span></span>

<span data-ttu-id="04fe9-113">Dodano nowy element `<references />` używany do jawnego określania zestawów, do których należy odwoływać się w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="04fe9-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="04fe9-114">Na przykład, jeśli dodasz następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="04fe9-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="04fe9-115">Następnie tylko `xunit.dll` i `xunit.extensions.dll` będą przywoływane z odpowiedniego [podfolderu Framework/profile](../reference/nuspec.md#explicit-assembly-references) folderu `lib`, nawet jeśli istnieją inne zestawy w folderze.</span><span class="sxs-lookup"><span data-stu-id="04fe9-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="04fe9-116">W przypadku pominięcia tego elementu stosowane jest zwykłe zachowanie, które polega na odwoływaniu się do każdego zestawu w folderze `lib`.</span><span class="sxs-lookup"><span data-stu-id="04fe9-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="04fe9-117">__Do czego służy ta funkcja?__</span><span class="sxs-lookup"><span data-stu-id="04fe9-117">__What is this feature used for?__</span></span>

<span data-ttu-id="04fe9-118">Ta funkcja obsługuje tylko zestawy w czasie projektowania.</span><span class="sxs-lookup"><span data-stu-id="04fe9-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="04fe9-119">Na przykład w przypadku korzystania z kontraktów kodu zestawy kontraktu muszą znajdować się obok zestawów środowiska uruchomieniowego, które rozszerzają się, aby program Visual Studio mógł je znaleźć, ale w przypadku zestawów kontraktu nie należy odwoływać się do tego projektu i nie należy go kopiować do folderu `bin`.</span><span class="sxs-lookup"><span data-stu-id="04fe9-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="04fe9-120">Podobnie funkcja może być używana do dla platform testów jednostkowych, takich jak XUnit, które wymagają, aby zestawy narzędzi były zlokalizowane obok zestawów środowiska uruchomieniowego, ale nie zostały wykluczone z odwołań do projektu.</span><span class="sxs-lookup"><span data-stu-id="04fe9-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="04fe9-121">Dodano możliwość wykluczania plików z pliku. nuspec</span><span class="sxs-lookup"><span data-stu-id="04fe9-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="04fe9-122">Element `<file>` w pliku `.nuspec` może służyć do dołączania określonego pliku lub zestawu plików przy użyciu symbolu wieloznacznego.</span><span class="sxs-lookup"><span data-stu-id="04fe9-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="04fe9-123">Gdy jest używany symbol wieloznaczny, nie ma możliwości wykluczenia określonego podzestawu dołączonych plików.</span><span class="sxs-lookup"><span data-stu-id="04fe9-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="04fe9-124">Załóżmy na przykład, że chcesz, aby wszystkie pliki tekstowe w folderze z wyjątkiem określonego.</span><span class="sxs-lookup"><span data-stu-id="04fe9-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="04fe9-125">Użyj średników do określenia wielu plików.</span><span class="sxs-lookup"><span data-stu-id="04fe9-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="04fe9-126">Lub Użyj symbolu wieloznacznego, aby wykluczyć zestaw plików, takich jak wszystkie pliki kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="04fe9-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="04fe9-127">Usuwanie pakietów przy użyciu okna dialogowego z komunikatem o usunięciu zależności</span><span class="sxs-lookup"><span data-stu-id="04fe9-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="04fe9-128">Podczas odinstalowywania pakietu z zależnościami program NuGet monituje o usunięcie zależności pakietu wraz z pakietem.</span><span class="sxs-lookup"><span data-stu-id="04fe9-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Usuwanie pakietów zależnych](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="04fe9-130">udoskonalenie polecenia `Get-Package`</span><span class="sxs-lookup"><span data-stu-id="04fe9-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="04fe9-131">Polecenie `Get-Package` obsługuje teraz parametr `-ProjectName`.</span><span class="sxs-lookup"><span data-stu-id="04fe9-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="04fe9-132">Więc polecenie</span><span class="sxs-lookup"><span data-stu-id="04fe9-132">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="04fe9-133">wyświetli listę wszystkich pakietów zainstalowanych w projekcie A.</span><span class="sxs-lookup"><span data-stu-id="04fe9-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="04fe9-134">Obsługa serwerów proxy, które wymagają uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="04fe9-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="04fe9-135">W przypadku korzystania z programu NuGet za serwerem proxy wymagającym uwierzytelniania pakiet NuGet będzie teraz monitował o poświadczenia serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="04fe9-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="04fe9-136">Wprowadzenie poświadczeń umożliwia NuGet łączenie się ze zdalnym repozytorium.</span><span class="sxs-lookup"><span data-stu-id="04fe9-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="04fe9-137">Obsługa repozytoriów wymagających uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="04fe9-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="04fe9-138">Pakiet NuGet obsługuje teraz łączenie z [repozytoriami prywatnymi](../hosting-packages/local-feeds.md) , które wymagają uwierzytelniania podstawowego lub NTLM.</span><span class="sxs-lookup"><span data-stu-id="04fe9-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="04fe9-139">Obsługa uwierzytelniania szyfrowanego zostanie dodana w przyszłym wydaniu.</span><span class="sxs-lookup"><span data-stu-id="04fe9-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="04fe9-140">Udoskonalenia wydajności repozytorium nuget.org</span><span class="sxs-lookup"><span data-stu-id="04fe9-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="04fe9-141">Wprowadziliśmy kilka ulepszeń wydajności w galerii nuget.org, aby przyspieszyć tworzenie i wyszukiwanie pakietów.</span><span class="sxs-lookup"><span data-stu-id="04fe9-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="04fe9-142">Filtrowanie projektu okna dialogowego rozwiązania</span><span class="sxs-lookup"><span data-stu-id="04fe9-142">Solution dialog project filtering</span></span>
<span data-ttu-id="04fe9-143">W oknie dialogowym na poziomie rozwiązania po wyświetleniu monitu o projekty, które mają zostać zainstalowane, wyświetlane są tylko projekty zgodne z wybranym pakietem.</span><span class="sxs-lookup"><span data-stu-id="04fe9-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="04fe9-144">Informacje o wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="04fe9-144">Package Release Notes</span></span>
<span data-ttu-id="04fe9-145">Pakiety NuGet zawierają teraz obsługę informacji o wersji.</span><span class="sxs-lookup"><span data-stu-id="04fe9-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="04fe9-146">Informacje o wersji są wyświetlane tylko podczas wyświetlania _aktualizacji_ pakietu, więc nie ma sensu, aby dodać je do swojej pierwszej wersji.</span><span class="sxs-lookup"><span data-stu-id="04fe9-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Informacje o wersji na karcie Aktualizacje](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="04fe9-148">Aby dodać informacje o wersji do pakietu, Użyj nowego elementu `<releaseNotes />` Metadata w pliku NuSpec.</span><span class="sxs-lookup"><span data-stu-id="04fe9-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="04fe9-149">nuspec & ltfiles/&gt;</span><span class="sxs-lookup"><span data-stu-id="04fe9-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="04fe9-150">Plik `.nuspec` teraz zezwala na pusty element `<files />`, który informuje plik NuGet. exe, aby nie dołączać żadnego pliku w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="04fe9-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="04fe9-151">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="04fe9-151">Bug Fixes</span></span>
<span data-ttu-id="04fe9-152">Pakiet NuGet 1,5 zawiera łącznie 107 elementów roboczych.</span><span class="sxs-lookup"><span data-stu-id="04fe9-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="04fe9-153">103 z tych elementów zostało oznaczonych jako błędy.</span><span class="sxs-lookup"><span data-stu-id="04fe9-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="04fe9-154">Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 1,5, zobacz [Śledzenie problemów NuGet dla tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="04fe9-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="04fe9-155">Poprawki błędów warto zauważyć:</span><span class="sxs-lookup"><span data-stu-id="04fe9-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="04fe9-156">[Problem 1273](http://nuget.codeplex.com/workitem/1273): `packages.config` większą liczbę kontroli wersji, sortując pakiety alfabetycznie i usuwając dodatkowe odstępy.</span><span class="sxs-lookup"><span data-stu-id="04fe9-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="04fe9-157">[Problem 844](http://nuget.codeplex.com/workitem/844): numery wersji są teraz znormalizowane, tak aby `Install-Package 1.0` działały w pakiecie z wersją `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="04fe9-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="04fe9-158">[Problem 1060](http://nuget.codeplex.com/workitem/1060): podczas tworzenia pakietu przy użyciu NuGet. exe flaga `-Version` zastępuje element `<version />`.</span><span class="sxs-lookup"><span data-stu-id="04fe9-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
