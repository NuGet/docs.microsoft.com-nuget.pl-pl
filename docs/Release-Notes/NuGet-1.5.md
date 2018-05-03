---
title: Informacje o wersji 1.5 NuGet
description: Informacje o wersji dla tym znanych problemów, poprawki, dodatkowe funkcje i dcr NuGet w wersji 1.5.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1f2f7ebe718ce943faa31b7e19395eead8726648
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="5b4ae-103">Informacje o wersji 1.5 NuGet</span><span class="sxs-lookup"><span data-stu-id="5b4ae-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="5b4ae-104">[Informacje o wersji NuGet 1.4](../release-notes/nuget-1.4.md) | [NuGet w wersji 1.6 informacje o wersji](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="5b4ae-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="5b4ae-105">NuGet w wersji 1.5 został wydany 30 sierpnia 2011.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="5b4ae-106">Funkcje</span><span class="sxs-lookup"><span data-stu-id="5b4ae-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="5b4ae-107">Szablony projektu z pakietami NuGet preinstalowane</span><span class="sxs-lookup"><span data-stu-id="5b4ae-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="5b4ae-108">Podczas tworzenia nowego szablonu projektu programu ASP.NET MVC 3, biblioteki skryptów jQuery zawarty w projekcie faktycznie umieszczone w nim przez instalowanie pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="5b4ae-109">Szablon projektu programu ASP.NET MVC 3 zawiera zestaw pakietów NuGet, które zainstalowane po wywołaniu szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="5b4ae-110">Ta możliwość uwzględnienia pakietów NuGet z szablonem projektu jest teraz funkcją NuGet który _żadnych_ szablonu projektu można teraz korzystać z.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="5b4ae-111">Aby uzyskać więcej informacji na temat tej funkcji przeczytaj [wpis w blogu przez dewelopera funkcji](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b4ae-111">For more details about this feature, read this [blog post by the developer of the feature](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="5b4ae-112">Odwołania do zestawów jawne</span><span class="sxs-lookup"><span data-stu-id="5b4ae-112">Explicit Assembly References</span></span>

<span data-ttu-id="5b4ae-113">Dodano nową `<references />` element używany do określenia jawnie zestawy, które w pakiecie ma być utworzone odwołanie.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="5b4ae-114">Jeśli na przykład dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="5b4ae-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="5b4ae-115">Następnie tylko `xunit.dll` i `xunit.extensions.dll` zostanie dodane odwołanie z wykorzystaniem odpowiedniej [podfolder, w ramach profilu](../reference/nuspec.md#explicit-assembly-references) z `lib` folderu, nawet jeśli istnieją innych zestawów w folderze.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="5b4ae-116">Jeśli ten element zostanie pominięty, a następnie stosuje zwykłe zachowanie, czyli odwołać się do każdego zestawu w `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="5b4ae-117">__Do czego służy ta funkcja?__</span><span class="sxs-lookup"><span data-stu-id="5b4ae-117">__What is this feature used for?__</span></span>

<span data-ttu-id="5b4ae-118">Ta funkcja obsługuje tylko zestawy czasu projektowania.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="5b4ae-119">Na przykład używając kontraktów kodu zestawów kontraktu musi być obok zestawy środowiska wykonawczego, do których one rozszerzyć, aby można je znaleźć Visual Studio, ale zestawów kontraktu powinien nie faktycznie można odwołuje się projekt i nie powinny być kopiowane do `bin` folderu.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="5b4ae-120">Podobnie funkcja może być używana do dla platform testów jednostkowych, takich jak XUnit, którą musi jego zestawów narzędzia znajdujące się obok zestawy środowiska wykonawczego, ale wyłączone z odwołań do projektu.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="5b4ae-121">Dodano możliwość Wyklucz pliki zawarte w .nuspec</span><span class="sxs-lookup"><span data-stu-id="5b4ae-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="5b4ae-122">`<file>` w elemencie `.nuspec` plików może służyć do uwzględnienia określonego pliku lub zestawu plików przy użyciu symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="5b4ae-123">Podczas korzystania z symbolem wieloznacznym, nie istnieje sposób wykluczenia konkretnego podzestawu dołączonych plików.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="5b4ae-124">Na przykład załóżmy, że chcesz, aby wszystkie pliki tekstowe, w folderze z wyjątkiem określonych.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="5b4ae-125">Użyj średników do określenia wielu plików.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="5b4ae-126">Lub użyj symbolu wieloznacznego, aby wykluczyć zestaw plików, na przykład wszystkie pliki kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="5b4ae-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="5b4ae-127">Usuwanie pakietów, korzystając z okna dialogowego monituje o usunięcie zależności</span><span class="sxs-lookup"><span data-stu-id="5b4ae-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="5b4ae-128">Podczas odinstalowywania pakietu z zależnościami, wyświetli NuGet, co pozwala na usunięcie zależności pakietów wraz z pakietem.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Usuwanie pakietów zależnych](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="5b4ae-130">`Get-Package` polecenie poprawy</span><span class="sxs-lookup"><span data-stu-id="5b4ae-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="5b4ae-131">`Get-Package` Polecenia obsługuje teraz `-ProjectName` parametru.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="5b4ae-132">To polecenie</span><span class="sxs-lookup"><span data-stu-id="5b4ae-132">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="5b4ae-133">Wyświetla wszystkie pakiety zainstalowane w projekcie A.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="5b4ae-134">Obsługa serwerów proxy, które wymagają uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="5b4ae-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="5b4ae-135">Gdy używasz serwera proxy wymagającego uwierzytelniania przy użyciu narzędzia NuGet, NuGet teraz wyświetli monit o podanie poświadczeń serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="5b4ae-136">Wprowadzanie poświadczeń umożliwia NuGet do nawiązania połączenia ze zdalnego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="5b4ae-137">Obsługa repozytoriów, które wymagają uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="5b4ae-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="5b4ae-138">NuGet obsługuje teraz nawiązywania [prywatne repozytoria](../hosting-packages/local-feeds.md) wymagające basic lub uwierzytelniania NTLM.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="5b4ae-139">Obsługa do uwierzytelnienia szyfrowanego zostanie dodana w przyszłej wersji.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="5b4ae-140">Ulepszenia wydajności umożliwiające repozytorium nuget.org</span><span class="sxs-lookup"><span data-stu-id="5b4ae-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="5b4ae-141">Poprawiono kilka wydajności do galerii nuget.org, aby utworzyć pakiet wyświetlania i szybsze wyszukiwanie.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="5b4ae-142">Filtrowanie projektu okna dialogowego rozwiązania</span><span class="sxs-lookup"><span data-stu-id="5b4ae-142">Solution dialog project filtering</span></span>
<span data-ttu-id="5b4ae-143">W oknie rozwiązanie na poziomie monitując o jakie projekty do zainstalowania możemy Pokaż tylko projekty, które są zgodne z wybranego pakietu.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="5b4ae-144">Informacje o wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="5b4ae-144">Package Release Notes</span></span>
<span data-ttu-id="5b4ae-145">Pakiety NuGet teraz obejmuje obsługę wersji.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="5b4ae-146">Informacje o wersji Pokazuj tylko się podczas wyświetlania _aktualizacje_ dla pakietu, więc go nie ma sensu je dodać do Twojego pierwszego wydania.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Informacje o wersji w karcie Aktualizacje](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="5b4ae-148">Aby dodać informacje o wersji do pakietu, należy użyć nowego `<releaseNotes />` metadane elementu w pliku NuSpec.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="5b4ae-149">.nuspec & ltfiles /&gt; poprawy jakości</span><span class="sxs-lookup"><span data-stu-id="5b4ae-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="5b4ae-150">`.nuspec` Pliku umożliwia teraz pusty `<files />` element, który informuje nuget.exe pozwalające nie zawiera plików w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="5b4ae-151">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="5b4ae-151">Bug Fixes</span></span>
<span data-ttu-id="5b4ae-152">NuGet w wersji 1.5 było łącznie 107 stałej elementów roboczych.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="5b4ae-153">103 tych zostały oznaczone jako usterki.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="5b4ae-154">Pełną listę prac elementów usunięto w wersji NuGet w wersji 1.5, sprawdź widok [NuGet Tracker problem w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="5b4ae-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="5b4ae-155">Warto zauważyć, poprawki:</span><span class="sxs-lookup"><span data-stu-id="5b4ae-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="5b4ae-156">[Problem 1273](http://nuget.codeplex.com/workitem/1273): wprowadzone `packages.config` przyjazną alfabetycznie sortowanie pakietów i usunięcia spacji dodatkowe więcej kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="5b4ae-157">[Problem 844](http://nuget.codeplex.com/workitem/844): numery wersji są teraz znormalizowany, aby `Install-Package 1.0` działa na pakiet z wersją `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="5b4ae-158">[Problem 1060](http://nuget.codeplex.com/workitem/1060): podczas tworzenia pakietu przy użyciu nuget.exe, `-Version` Flaga zastąpienia `<version />` elementu.</span><span class="sxs-lookup"><span data-stu-id="5b4ae-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
