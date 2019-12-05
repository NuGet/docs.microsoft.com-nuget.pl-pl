---
title: Informacje o wersji narzędzia NuGet 1,3
description: Informacje o wersji programu NuGet 1,3, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 45d5caa46d532670e370b81f675663b3c5aaaa95
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825265"
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="cbb52-103">Informacje o wersji narzędzia NuGet 1,3</span><span class="sxs-lookup"><span data-stu-id="cbb52-103">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="cbb52-104">[Informacje o wersji pakietu nuget 1,2](../release-notes/nuget-1.2.md) | [Informacje o wersji narzędzia NuGet 1,4](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="cbb52-104">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="cbb52-105">Pakiet NuGet 1,3 został wydaną 25 kwietnia 2011.</span><span class="sxs-lookup"><span data-stu-id="cbb52-105">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="cbb52-106">Nowe funkcje</span><span class="sxs-lookup"><span data-stu-id="cbb52-106">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="cbb52-107">Usprawnione Tworzenie pakietów z integracją z serwerem symboli</span><span class="sxs-lookup"><span data-stu-id="cbb52-107">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="cbb52-108">Zespół NuGet współpracujący z osób na [SymbolSource.org](http://www.symbolsource.org/) , aby zaoferować naprawdę prosty sposób publikowania źródeł i plików PDB wraz z pakietem.</span><span class="sxs-lookup"><span data-stu-id="cbb52-108">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="cbb52-109">Dzięki temu klienci pakietu mogą przechodzić do źródła pakietu w debugerze.</span><span class="sxs-lookup"><span data-stu-id="cbb52-109">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="cbb52-110">Aby uzyskać więcej informacji, przeczytaj artykuł [Tworzenie i publikowanie pakietu symboli](../create-packages/symbol-packages.md) w łatwy sposób publikowania pakietów NuGet ze źródłami.</span><span class="sxs-lookup"><span data-stu-id="cbb52-110">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="cbb52-111">Możesz również obejrzeć prezentację na żywo tej funkcji jako część pakietu NuGet, z głębokości Porozmawiaj pod adresem Mix11.</span><span class="sxs-lookup"><span data-stu-id="cbb52-111">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="cbb52-112">Ta funkcja jest w pełni zademonstrowana, zaczynając od 20-minutowego znaku wideo.</span><span class="sxs-lookup"><span data-stu-id="cbb52-112">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="cbb52-113">Polecenie `Open-PackagePage`</span><span class="sxs-lookup"><span data-stu-id="cbb52-113">`Open-PackagePage` Command</span></span>

<span data-ttu-id="cbb52-114">To polecenie ułatwia dostęp do strony projektu dla pakietu z poziomu konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="cbb52-114">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="cbb52-115">Dostępne są również opcje umożliwiające otwarcie adresu URL licencji i strony Zgłoś nadużycie dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="cbb52-115">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="cbb52-116">Składnia polecenia jest następująca:</span><span class="sxs-lookup"><span data-stu-id="cbb52-116">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="cbb52-117">Opcja `-PassThru` służy do zwracania wartości określonego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="cbb52-117">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="cbb52-118">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="cbb52-118">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="cbb52-119">Otwiera przeglądarkę do adresu URL projektu określonego w pakiecie Ninject.</span><span class="sxs-lookup"><span data-stu-id="cbb52-119">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="cbb52-120">Otwiera przeglądarkę do adresu URL licencji określonego w pakiecie Ninject.</span><span class="sxs-lookup"><span data-stu-id="cbb52-120">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="cbb52-121">Otwiera przeglądarkę do adresu URL w bieżącym źródle pakietu używanym do zgłaszania nadużycia dla określonego pakietu.</span><span class="sxs-lookup"><span data-stu-id="cbb52-121">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="cbb52-122">Przypisuje adres URL licencji do zmiennej, $url bez otwierania adresu URL w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="cbb52-122">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="cbb52-123">Usprawnienia wydajności</span><span class="sxs-lookup"><span data-stu-id="cbb52-123">Performance Improvements</span></span>

<span data-ttu-id="cbb52-124">W programie NuGet 1,3 wprowadzono wiele ulepszeń wydajności.</span><span class="sxs-lookup"><span data-stu-id="cbb52-124">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="cbb52-125">Pakiet NuGet 1,3 pozwala uniknąć pobierania tej samej wersji pakietu wielokrotnie przez uwzględnienie lokalnej pamięci podręcznej dla poszczególnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="cbb52-125">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="cbb52-126">Dostęp do pamięci podręcznej można uzyskać i wyczyścić za pomocą okna dialogowego ustawień Menedżera pakietów:</span><span class="sxs-lookup"><span data-stu-id="cbb52-126">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![Okno dialogowe Opcje NuGet z ustawieniami pamięci podręcznej pakietów](./media/nuget-options.png)

<span data-ttu-id="cbb52-128">Inne ulepszenia wydajności obejmują dodawanie obsługi kompresji HTTP i zwiększanie szybkości instalacji pakietów w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cbb52-128">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="cbb52-129">Programy Visual Studio i NuGet. exe używają tej samej listy źródeł pakietów</span><span class="sxs-lookup"><span data-stu-id="cbb52-129">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="cbb52-130">Przed pakietem NuGet 1,3 Lista źródeł pakietów używanych przez narzędzia NuGet. exe i dodatek NuGet Visual Studio nie zostały zapisane w tym samym miejscu.</span><span class="sxs-lookup"><span data-stu-id="cbb52-130">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="cbb52-131">Pakiet NuGet 1,3 używa teraz tej samej listy w obu miejscach.</span><span class="sxs-lookup"><span data-stu-id="cbb52-131">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="cbb52-132">Lista jest przechowywana w `NuGet.Config` i przechowywana w folderze AppData.</span><span class="sxs-lookup"><span data-stu-id="cbb52-132">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="cbb52-133">NuGet. exe domyślnie ignoruje pliki i foldery, które zaczynają się od "."</span><span class="sxs-lookup"><span data-stu-id="cbb52-133">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="cbb52-134">Aby program NuGet działał poprawnie z systemami kontroli źródła, takimi jak Subversion i Mercurial, NuGet. exe ignoruje foldery i pliki, które zaczynają się od znaku "." podczas tworzenia pakietów.</span><span class="sxs-lookup"><span data-stu-id="cbb52-134">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="cbb52-135">Można to zastąpić przy użyciu dwóch nowych flag:</span><span class="sxs-lookup"><span data-stu-id="cbb52-135">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="cbb52-136">__-NoDefaultExcludes__ służy do przesłonięcia tego ustawienia i uwzględnienia wszystkich plików.</span><span class="sxs-lookup"><span data-stu-id="cbb52-136">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="cbb52-137">__-Exclude__ służy do dodawania innych plików/folderów do wykluczenia przy użyciu wzorca.</span><span class="sxs-lookup"><span data-stu-id="cbb52-137">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="cbb52-138">Na przykład, aby wykluczyć wszystkie pliki z rozszerzeniem. bak.</span><span class="sxs-lookup"><span data-stu-id="cbb52-138">For example, to exclude all files with the '.bak' file extension</span></span>

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="cbb52-139">_Uwaga: wzorzec nie jest domyślnie cykliczny._</span><span class="sxs-lookup"><span data-stu-id="cbb52-139">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="cbb52-140">Obsługa projektów WiX i .NET Micro Framework</span><span class="sxs-lookup"><span data-stu-id="cbb52-140">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="cbb52-141">Dzięki wkładom społecznościowym pakiet NuGet obejmuje obsługę typów projektów WiX oraz .NET Micro Framework.</span><span class="sxs-lookup"><span data-stu-id="cbb52-141">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="cbb52-142">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="cbb52-142">Bug Fixes</span></span>

<span data-ttu-id="cbb52-143">Aby zapoznać się z pełną listą poprawek błędów, przejrzyj [Narzędzie śledzenia problemów NuGet dla tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="cbb52-143">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="cbb52-144">Poprawki błędów warto zauważyć</span><span class="sxs-lookup"><span data-stu-id="cbb52-144">Bug fixes worth noting</span></span>

* <span data-ttu-id="cbb52-145">Pakiety z plikami źródłowymi działają zarówno w witrynach internetowych, jak i w projektach aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="cbb52-145">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="cbb52-146">W przypadku witryn sieci Web pliki źródłowe są kopiowane do folderu `App_Code`</span><span class="sxs-lookup"><span data-stu-id="cbb52-146">For Websites, source files are copied into the `App_Code` folder</span></span>
