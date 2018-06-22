---
title: Informacje o wersji 1.3 NuGet
description: Informacje o wersji programu NuGet 1.3 tym znanych problemów, poprawki, dodatkowe funkcje i dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c0284fe0afb11bf6465897132cccd160674ea3e1
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821151"
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="dccc2-103">Informacje o wersji 1.3 NuGet</span><span class="sxs-lookup"><span data-stu-id="dccc2-103">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="dccc2-104">[Informacje o wersji NuGet 1.2](../release-notes/nuget-1.2.md) | [NuGet 1.4 informacje o wersji](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="dccc2-104">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="dccc2-105">NuGet 1.3 został wydany 25 kwietnia 2011.</span><span class="sxs-lookup"><span data-stu-id="dccc2-105">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="dccc2-106">Nowe funkcje</span><span class="sxs-lookup"><span data-stu-id="dccc2-106">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="dccc2-107">Prostsze tworzenie pakietu z integracją serwera symboli</span><span class="sxs-lookup"><span data-stu-id="dccc2-107">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="dccc2-108">Zespół NuGet we współpracy z pracowników w [SymbolSource.org](http://www.symbolsource.org/) oferowanie naprawdę prosty sposób publikowania źródeł, a w pliku PDB wraz z pakietem.</span><span class="sxs-lookup"><span data-stu-id="dccc2-108">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="dccc2-109">Umożliwia klientom pakietu krok do źródła pakietu w debugerze.</span><span class="sxs-lookup"><span data-stu-id="dccc2-109">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="dccc2-110">Aby uzyskać więcej informacji, przeczytaj [tworzenie i publikowanie pakietu symboli](../create-packages/symbol-packages.md) łatwy sposób, aby opublikować pakiety NuGet ze źródła.</span><span class="sxs-lookup"><span data-stu-id="dccc2-110">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="dccc2-111">Można również obejrzeć na żywo pokaz tej funkcji jako część programu NuGet szczegółowo porozmawiać na Mix11.</span><span class="sxs-lookup"><span data-stu-id="dccc2-111">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="dccc2-112">Ta funkcja jest pełni wykazać, zaczynając od znaku 20 minut wideo.</span><span class="sxs-lookup"><span data-stu-id="dccc2-112">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="dccc2-113">`Open-PackagePage` polecenie</span><span class="sxs-lookup"><span data-stu-id="dccc2-113">`Open-PackagePage` Command</span></span>

<span data-ttu-id="dccc2-114">Tego polecenia można łatwo uzyskać dostęp do strony projektu dla pakietu z poziomu konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="dccc2-114">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="dccc2-115">Umożliwia także opcje, aby otworzyć adres URL licencji i na stronie nadużycia raportów dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="dccc2-115">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="dccc2-116">Składnia polecenia jest następująca:</span><span class="sxs-lookup"><span data-stu-id="dccc2-116">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="dccc2-117">`-PassThru` Opcja służy do zwracania wartości określonego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="dccc2-117">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="dccc2-118">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="dccc2-118">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="dccc2-119">Otwiera w przeglądarce adres URL projektu określony w pakiecie Ninject.</span><span class="sxs-lookup"><span data-stu-id="dccc2-119">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="dccc2-120">Otwiera w przeglądarce adres URL licencji określony w pakiecie Ninject.</span><span class="sxs-lookup"><span data-stu-id="dccc2-120">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="dccc2-121">Otwiera w przeglądarce adres URL w bieżącym źródle pakietów używane do zgłaszania nadużyć dla określonego pakietu.</span><span class="sxs-lookup"><span data-stu-id="dccc2-121">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="dccc2-122">Przypisuje adres URL licencji do zmiennej $url bez otwierania adresu URL w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="dccc2-122">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="dccc2-123">Usprawnienia wydajności</span><span class="sxs-lookup"><span data-stu-id="dccc2-123">Performance Improvements</span></span>

<span data-ttu-id="dccc2-124">NuGet 1.3 wprowadzono wiele ulepszeń wydajności.</span><span class="sxs-lookup"><span data-stu-id="dccc2-124">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="dccc2-125">NuGet 1.3 pozwala uniknąć pobierania tej samej wersji pakietu wiele razy przy tym pamięci podręcznej użytkownika lokalnego.</span><span class="sxs-lookup"><span data-stu-id="dccc2-125">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="dccc2-126">Można uzyskać dostępu do pamięci podręcznej i wyczyszczone za pomocą okna dialogowego Ustawienia Menedżera pakietów:</span><span class="sxs-lookup"><span data-stu-id="dccc2-126">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![Okno dialogowe Opcje NuGet z ustawień pamięci podręcznej pakietu](./media/nuget-options.png)

<span data-ttu-id="dccc2-128">Inne ulepszenia wydajności obejmują dodawanie obsługi kompresji HTTP i poprawy szybkości instalacji pakietu w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dccc2-128">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="dccc2-129">Visual Studio i nuget.exe korzysta z tej samej listy źródeł pakietu</span><span class="sxs-lookup"><span data-stu-id="dccc2-129">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="dccc2-130">Przed NuGet 1.3 lista źródeł pakietów używane przez nuget.exe i NuGet programu Visual Studio dodatku nie były przechowywane w tym samym miejscu.</span><span class="sxs-lookup"><span data-stu-id="dccc2-130">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="dccc2-131">NuGet 1.3 obecnie korzysta z tej samej listy w obu miejscach.</span><span class="sxs-lookup"><span data-stu-id="dccc2-131">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="dccc2-132">Listy są przechowywane w `NuGet.Config` i przechowywane w folderze AppData.</span><span class="sxs-lookup"><span data-stu-id="dccc2-132">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="dccc2-133">nuget.exe ignoruje pliki i foldery, które zaczynają się "." domyślnie</span><span class="sxs-lookup"><span data-stu-id="dccc2-133">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="dccc2-134">W celu NuGet działają prawidłowo w przypadku systemów kontroli źródła, takie Podwersją i Mercurial, nuget.exe ignoruje folderów i plików, które zaczynają się '.' znaków, podczas tworzenia pakietów.</span><span class="sxs-lookup"><span data-stu-id="dccc2-134">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="dccc2-135">Tę wartość można zastąpić przy użyciu dwóch nowych flag:</span><span class="sxs-lookup"><span data-stu-id="dccc2-135">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="dccc2-136">__-NoDefaultExcludes__ służy do zastąpienia tego ustawienia i obejmują wszystkie pliki.</span><span class="sxs-lookup"><span data-stu-id="dccc2-136">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="dccc2-137">__— Wyklucz__ służy do dodawania inne pliki/foldery do wykluczenia, za pomocą wzorca.</span><span class="sxs-lookup"><span data-stu-id="dccc2-137">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="dccc2-138">Na przykład, aby wykluczyć wszystkie pliki z rozszerzeniem "bak"</span><span class="sxs-lookup"><span data-stu-id="dccc2-138">For example, to exclude all files with the '.bak' file extension</span></span>

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="dccc2-139">_Uwaga: wzorzec nie jest cykliczne domyślnie._</span><span class="sxs-lookup"><span data-stu-id="dccc2-139">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="dccc2-140">Wsparcie dla projektów WiX i .NET Micro Framework</span><span class="sxs-lookup"><span data-stu-id="dccc2-140">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="dccc2-141">Dzięki użyciu społeczność NuGet obsługuje WiX typów projektów, a także Micro .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="dccc2-141">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="dccc2-142">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="dccc2-142">Bug Fixes</span></span>

<span data-ttu-id="dccc2-143">Aby zapoznać się z pełną listą poprawki, Wyświetl [NuGet Tracker problem w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="dccc2-143">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="dccc2-144">Poprawki błędów warto zauważyć</span><span class="sxs-lookup"><span data-stu-id="dccc2-144">Bug fixes worth noting</span></span>

* <span data-ttu-id="dccc2-145">Pakiety z plikami źródłowymi działa w obu witryn sieci Web i projekty aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="dccc2-145">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="dccc2-146">Dla witryn sieci Web, pliki źródłowe zostają skopiowane do `App_Code` folderu</span><span class="sxs-lookup"><span data-stu-id="dccc2-146">For Websites, source files are copied into the `App_Code` folder</span></span>
