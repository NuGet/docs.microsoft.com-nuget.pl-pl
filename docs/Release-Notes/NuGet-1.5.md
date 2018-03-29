---
title: Informacje o wersji NuGet w wersji 1.5 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Informacje o wersji dla tym znanych problemów, poprawki, dodatkowe funkcje i dcr NuGet w wersji 1.5.
keywords: NuGet w wersji 1.5 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: abb044bab5fdc8748b529a2f0072a7271a3674dd
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="18b50-104">Informacje o wersji 1.5 NuGet</span><span class="sxs-lookup"><span data-stu-id="18b50-104">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="18b50-105">[Informacje o wersji NuGet 1.4](../release-notes/nuget-1.4.md) | [NuGet w wersji 1.6 informacje o wersji](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="18b50-105">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="18b50-106">NuGet w wersji 1.5 został wydany 30 sierpnia 2011.</span><span class="sxs-lookup"><span data-stu-id="18b50-106">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="18b50-107">Funkcje</span><span class="sxs-lookup"><span data-stu-id="18b50-107">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="18b50-108">Szablony projektu z pakietami NuGet preinstalowane</span><span class="sxs-lookup"><span data-stu-id="18b50-108">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="18b50-109">Podczas tworzenia nowego szablonu projektu programu ASP.NET MVC 3, biblioteki skryptów jQuery zawarty w projekcie faktycznie umieszczone w nim przez instalowanie pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="18b50-109">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="18b50-110">Szablon projektu programu ASP.NET MVC 3 zawiera zestaw pakietów NuGet, które zainstalowane po wywołaniu szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="18b50-110">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="18b50-111">Ta możliwość uwzględnienia pakietów NuGet z szablonem projektu jest teraz funkcją NuGet który _żadnych_ szablonu projektu można teraz korzystać z.</span><span class="sxs-lookup"><span data-stu-id="18b50-111">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="18b50-112">Aby uzyskać więcej informacji na temat tej funkcji przeczytaj [wpis w blogu przez dewelopera funkcji](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span><span class="sxs-lookup"><span data-stu-id="18b50-112">For more details about this feature, read this [blog post by the developer of the feature](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="18b50-113">Odwołania do zestawów jawne</span><span class="sxs-lookup"><span data-stu-id="18b50-113">Explicit Assembly References</span></span>

<span data-ttu-id="18b50-114">Dodano nową `<references />` element używany do określenia jawnie zestawy, które w pakiecie ma być utworzone odwołanie.</span><span class="sxs-lookup"><span data-stu-id="18b50-114">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="18b50-115">Jeśli na przykład dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="18b50-115">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="18b50-116">Następnie tylko `xunit.dll` i `xunit.extensions.dll` zostanie dodane odwołanie z wykorzystaniem odpowiedniej [podfolder, w ramach profilu](../reference/nuspec.md#explicit-assembly-references) z `lib` folderu, nawet jeśli istnieją innych zestawów w folderze.</span><span class="sxs-lookup"><span data-stu-id="18b50-116">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="18b50-117">Jeśli ten element zostanie pominięty, a następnie stosuje zwykłe zachowanie, czyli odwołać się do każdego zestawu w `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="18b50-117">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="18b50-118">__Do czego służy ta funkcja?__</span><span class="sxs-lookup"><span data-stu-id="18b50-118">__What is this feature used for?__</span></span>

<span data-ttu-id="18b50-119">Ta funkcja obsługuje tylko zestawy czasu projektowania.</span><span class="sxs-lookup"><span data-stu-id="18b50-119">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="18b50-120">Na przykład używając kontraktów kodu zestawów kontraktu musi być obok zestawy środowiska wykonawczego, do których one rozszerzyć, aby można je znaleźć Visual Studio, ale zestawów kontraktu powinien nie faktycznie można odwołuje się projekt i nie powinny być kopiowane do `bin` folderu.</span><span class="sxs-lookup"><span data-stu-id="18b50-120">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="18b50-121">Podobnie funkcja może być używana do dla platform testów jednostkowych, takich jak XUnit, którą musi jego zestawów narzędzia znajdujące się obok zestawy środowiska wykonawczego, ale wyłączone z odwołań do projektu.</span><span class="sxs-lookup"><span data-stu-id="18b50-121">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="18b50-122">Dodano możliwość Wyklucz pliki zawarte w .nuspec</span><span class="sxs-lookup"><span data-stu-id="18b50-122">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="18b50-123">`<file>` w elemencie `.nuspec` plików może służyć do uwzględnienia określonego pliku lub zestawu plików przy użyciu symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="18b50-123">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="18b50-124">Podczas korzystania z symbolem wieloznacznym, nie istnieje sposób wykluczenia konkretnego podzestawu dołączonych plików.</span><span class="sxs-lookup"><span data-stu-id="18b50-124">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="18b50-125">Na przykład załóżmy, że chcesz, aby wszystkie pliki tekstowe, w folderze z wyjątkiem określonych.</span><span class="sxs-lookup"><span data-stu-id="18b50-125">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="18b50-126">Użyj średników do określenia wielu plików.</span><span class="sxs-lookup"><span data-stu-id="18b50-126">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="18b50-127">Lub użyj symbolu wieloznacznego, aby wykluczyć zestaw plików, na przykład wszystkie pliki kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="18b50-127">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="18b50-128">Usuwanie pakietów, korzystając z okna dialogowego monituje o usunięcie zależności</span><span class="sxs-lookup"><span data-stu-id="18b50-128">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="18b50-129">Podczas odinstalowywania pakietu z zależnościami, wyświetli NuGet, co pozwala na usunięcie zależności pakietów wraz z pakietem.</span><span class="sxs-lookup"><span data-stu-id="18b50-129">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Usuwanie pakietów zależnych](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="18b50-131">`Get-Package` polecenie poprawy</span><span class="sxs-lookup"><span data-stu-id="18b50-131">`Get-Package` command improvement</span></span>
<span data-ttu-id="18b50-132">`Get-Package` Polecenia obsługuje teraz `-ProjectName` parametru.</span><span class="sxs-lookup"><span data-stu-id="18b50-132">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="18b50-133">To polecenie</span><span class="sxs-lookup"><span data-stu-id="18b50-133">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="18b50-134">Wyświetla wszystkie pakiety zainstalowane w projekcie A.</span><span class="sxs-lookup"><span data-stu-id="18b50-134">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="18b50-135">Obsługa serwerów proxy, które wymagają uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="18b50-135">Support for Proxies that require authentication</span></span>
<span data-ttu-id="18b50-136">Gdy używasz serwera proxy wymagającego uwierzytelniania przy użyciu narzędzia NuGet, NuGet teraz wyświetli monit o podanie poświadczeń serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="18b50-136">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="18b50-137">Wprowadzanie poświadczeń umożliwia NuGet do nawiązania połączenia ze zdalnego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="18b50-137">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="18b50-138">Obsługa repozytoriów, które wymagają uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="18b50-138">Support for Repositories that require authentication</span></span>
<span data-ttu-id="18b50-139">NuGet obsługuje teraz nawiązywania [prywatne repozytoria](../hosting-packages/local-feeds.md) wymagające basic lub uwierzytelniania NTLM.</span><span class="sxs-lookup"><span data-stu-id="18b50-139">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="18b50-140">Obsługa do uwierzytelnienia szyfrowanego zostanie dodana w przyszłej wersji.</span><span class="sxs-lookup"><span data-stu-id="18b50-140">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="18b50-141">Ulepszenia wydajności umożliwiające repozytorium nuget.org</span><span class="sxs-lookup"><span data-stu-id="18b50-141">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="18b50-142">Poprawiono kilka wydajności do galerii nuget.org, aby utworzyć pakiet wyświetlania i szybsze wyszukiwanie.</span><span class="sxs-lookup"><span data-stu-id="18b50-142">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="18b50-143">Filtrowanie projektu okna dialogowego rozwiązania</span><span class="sxs-lookup"><span data-stu-id="18b50-143">Solution dialog project filtering</span></span>
<span data-ttu-id="18b50-144">W oknie rozwiązanie na poziomie monitując o jakie projekty do zainstalowania możemy Pokaż tylko projekty, które są zgodne z wybranego pakietu.</span><span class="sxs-lookup"><span data-stu-id="18b50-144">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="18b50-145">Informacje o wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="18b50-145">Package Release Notes</span></span>
<span data-ttu-id="18b50-146">Pakiety NuGet teraz obejmuje obsługę wersji.</span><span class="sxs-lookup"><span data-stu-id="18b50-146">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="18b50-147">Informacje o wersji Pokazuj tylko się podczas wyświetlania _aktualizacje_ dla pakietu, więc go nie ma sensu je dodać do Twojego pierwszego wydania.</span><span class="sxs-lookup"><span data-stu-id="18b50-147">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Informacje o wersji w karcie Aktualizacje](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="18b50-149">Aby dodać informacje o wersji do pakietu, należy użyć nowego `<releaseNotes />` metadane elementu w pliku NuSpec.</span><span class="sxs-lookup"><span data-stu-id="18b50-149">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="18b50-150">.nuspec & ltfiles /&gt; poprawy jakości</span><span class="sxs-lookup"><span data-stu-id="18b50-150">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="18b50-151">`.nuspec` Pliku umożliwia teraz pusty `<files />` element, który informuje nuget.exe pozwalające nie zawiera plików w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="18b50-151">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="18b50-152">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="18b50-152">Bug Fixes</span></span>
<span data-ttu-id="18b50-153">NuGet w wersji 1.5 było łącznie 107 stałej elementów roboczych.</span><span class="sxs-lookup"><span data-stu-id="18b50-153">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="18b50-154">103 tych zostały oznaczone jako usterki.</span><span class="sxs-lookup"><span data-stu-id="18b50-154">103 of those were marked as bugs.</span></span>

<span data-ttu-id="18b50-155">Pełną listę prac elementów usunięto w wersji NuGet w wersji 1.5, sprawdź widok [NuGet Tracker problem w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="18b50-155">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="18b50-156">Warto zauważyć, poprawki:</span><span class="sxs-lookup"><span data-stu-id="18b50-156">Bug fixes worth noting:</span></span>

* <span data-ttu-id="18b50-157">[Problem 1273](http://nuget.codeplex.com/workitem/1273): wprowadzone `packages.config` przyjazną alfabetycznie sortowanie pakietów i usunięcia spacji dodatkowe więcej kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="18b50-157">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="18b50-158">[Problem 844](http://nuget.codeplex.com/workitem/844): numery wersji są teraz znormalizowany, aby `Install-Package 1.0` działa na pakiet z wersją `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="18b50-158">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="18b50-159">[Problem 1060](http://nuget.codeplex.com/workitem/1060): podczas tworzenia pakietu przy użyciu nuget.exe, `-Version` Flaga zastąpienia `<version />` elementu.</span><span class="sxs-lookup"><span data-stu-id="18b50-159">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
