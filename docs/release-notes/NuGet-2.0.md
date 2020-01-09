---
title: Informacje o wersji narzędzia NuGet 2,0
description: Informacje o wersji programu NuGet 2,0, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 01fdbfafcaea009cf119dfa880b2b16539c9b088
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383070"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="e6cb7-103">Informacje o wersji narzędzia NuGet 2,0</span><span class="sxs-lookup"><span data-stu-id="e6cb7-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="e6cb7-104">[Informacje o wersji pakietu nuget 1,8](../release-notes/nuget-1.8.md) | [Informacje o wersji narzędzia NuGet 2,1](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="e6cb7-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="e6cb7-105">Pakiet NuGet 2,0 został wydaną 19 czerwca 2012.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="e6cb7-106">Znany problem z instalacją</span><span class="sxs-lookup"><span data-stu-id="e6cb7-106">Known Installation Issue</span></span>
<span data-ttu-id="e6cb7-107">W przypadku korzystania z programu VS 2010 z dodatkiem SP1 można napotkać błąd instalacji podczas próby uaktualnienia narzędzia NuGet, jeśli jest zainstalowana starsza wersja.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="e6cb7-108">Obejście polega na prostu odinstalować pakiet NuGet, a następnie zainstalować go z galerii rozszerzeń programu VS.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="e6cb7-109">Aby uzyskać więcej informacji, zobacz <https://support.microsoft.com/kb/2581019> lub [Przejdź bezpośrednio do poprawki programu vs](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="e6cb7-109">See <https://support.microsoft.com/kb/2581019> for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="e6cb7-110">Uwaga: Jeśli program Visual Studio nie zezwoli na odinstalowanie rozszerzenia (przycisk Odinstaluj jest wyłączony), prawdopodobnie trzeba będzie ponownie uruchomić program Visual Studio za pomocą polecenia "Uruchom jako administrator".</span><span class="sxs-lookup"><span data-stu-id="e6cb7-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="e6cb7-111">Wyrażanie zgody na przywracanie pakietu jest teraz aktywne</span><span class="sxs-lookup"><span data-stu-id="e6cb7-111">Package restore consent is now active</span></span>

<span data-ttu-id="e6cb7-112">Zgodnie z opisem w tym [wpisie dotyczącym przywracania pakietów pakiet](http://blog.nuget.org/20120518/package-restore-and-consent.html)NuGet 2,0 będzie teraz wymagał zgody, aby umożliwić przywracanie pakietów w trybie online i pobrać pakiety.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="e6cb7-113">Upewnij się, że podano zgodę za pośrednictwem okna dialogowego konfiguracji Menedżera pakietów lub zmiennej środowiskowej EnableNuGetPackageRestore.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="e6cb7-114">Grupuj zależności według platform docelowych</span><span class="sxs-lookup"><span data-stu-id="e6cb7-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="e6cb7-115">Począwszy od wersji 2,0, zależności pakietów mogą się różnić w zależności od profilu struktury projektu docelowego.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="e6cb7-116">Jest to realizowane przy użyciu zaktualizowanego schematu `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="e6cb7-117">Element `<dependencies>` może teraz zawierać zestaw `<group>` elementów.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="e6cb7-118">Każda grupa zawiera zero lub więcej elementów `<dependency>` i atrybut `targetFramework`.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="e6cb7-119">Wszystkie zależności wewnątrz grupy są instalowane razem, jeśli struktura docelowa jest zgodna z docelowym profilem platformy projektu.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="e6cb7-120">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e6cb7-120">For example:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<span data-ttu-id="e6cb7-121">Należy zauważyć, że grupa może zawierać **zero** zależności.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="e6cb7-122">W powyższym przykładzie, jeśli pakiet jest zainstalowany w projekcie, który jest przeznaczony dla programu Silverlight 3,0 lub nowszego, nie zostaną zainstalowane żadne zależności.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="e6cb7-123">Jeśli pakiet jest zainstalowany w projekcie przeznaczonym dla programu .NET 4,0 lub nowszego, zostaną zainstalowane dwie zależności, jQuery i webaktywator.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="e6cb7-124">Jeśli pakiet jest instalowany w projekcie, który jest przeznaczony dla wczesnej wersji tych 2 platform lub innych platform, RouteMagic 1.1.0 zostanie zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="e6cb7-125">Nie ma żadnego dziedziczenia między grupami.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-125">There is no inheritance between groups.</span></span> <span data-ttu-id="e6cb7-126">Jeśli platforma docelowa projektu jest zgodna z atrybutem `targetFramework` grupy, zostaną zainstalowane tylko zależności w ramach tej grupy.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="e6cb7-127">Pakiet może określać zależności pakietu w dowolnym z dwóch formatów: starym formacie płaskiej listy elementów `<dependency>` lub grup.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="e6cb7-128">Jeśli jest używany format `<group>`, nie można zainstalować pakietu w wersjach programu NuGet wcześniejszych niż 2,0.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="e6cb7-129">Należy zauważyć, że mieszanie dwóch formatów jest niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="e6cb7-130">Na przykład poniższy fragment kodu jest **nieprawidłowy** i zostanie odrzucony przez pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="e6cb7-131">Grupowanie plików zawartości i skryptów programu PowerShell według platformy docelowej</span><span class="sxs-lookup"><span data-stu-id="e6cb7-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="e6cb7-132">Oprócz odwołań do zestawów, pliki zawartości i skrypty programu PowerShell mogą być również pogrupowane według platformy docelowej.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="e6cb7-133">Ta sama struktura folderów znaleziona w folderze `lib` do określania platformy docelowej można teraz zastosować w taki sam sposób, jak foldery `content` i `tools`.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="e6cb7-134">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e6cb7-134">For example:</span></span>

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

<span data-ttu-id="e6cb7-135">**Uwaga**: ponieważ `init.ps1` jest wykonywany na poziomie rozwiązania i nie zależy od żadnego pojedynczego projektu, musi być umieszczony bezpośrednio pod folderem `tools`.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="e6cb7-136">Jeśli zostanie umieszczony w folderze specyficznym dla platformy, zostanie zignorowany.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="e6cb7-137">Ponadto nową funkcją w programie NuGet 2,0 jest to, że folder struktury może być *pusty*, w takim przypadku pakiet NuGet nie dodaje odwołań do zestawów, nie dodaje plików zawartości ani nie uruchamia skryptów programu PowerShell dla konkretnej wersji platformy.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="e6cb7-138">W powyższym przykładzie folder `content\net40` jest pusty.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="e6cb7-139">Ulepszona wydajność kończenia karty</span><span class="sxs-lookup"><span data-stu-id="e6cb7-139">Improved tab completion performance</span></span>
<span data-ttu-id="e6cb7-140">Funkcja uzupełniania tabulatorów w konsoli Menedżera pakietów NuGet została zaktualizowana w celu znacznego zwiększenia wydajności.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="e6cb7-141">Nastąpi znacznie mniej opóźnienia od momentu naciśnięcia klawisza Tab do momentu wyświetlenia listy rozwijanej sugestii.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="e6cb7-142">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="e6cb7-142">Bug Fixes</span></span>
<span data-ttu-id="e6cb7-143">Pakiet NuGet 2,0 zawiera wiele poprawek błędów z naciskiem na zgodę i wydajność przywracania pakietu.</span><span class="sxs-lookup"><span data-stu-id="e6cb7-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="e6cb7-144">Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 2,0, zobacz [Śledzenie problemów NuGet dla tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="e6cb7-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
