---
title: Informacje o wersji 2.0 programu NuGet
description: Informacje o wersji programu NuGet w tym znanych problemów, poprawki, funkcje dodane i DCRs w wersji 2.0.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f32eea9260ce7e307ff56b7f3e6b48c6d98e6c90
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547578"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="50325-103">Informacje o wersji 2.0 programu NuGet</span><span class="sxs-lookup"><span data-stu-id="50325-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="50325-104">[Informacje o wersji NuGet 1.8](../release-notes/nuget-1.8.md) | [informacjach o wersji NuGet 2.1](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="50325-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="50325-105">NuGet w wersji 2.0 została wydana 19 czerwca 2012 r.</span><span class="sxs-lookup"><span data-stu-id="50325-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="50325-106">Problem z instalacją znane</span><span class="sxs-lookup"><span data-stu-id="50325-106">Known Installation Issue</span></span>
<span data-ttu-id="50325-107">Jeśli używasz programu VS 2010 z dodatkiem SP1, możesz napotkać błąd instalacji podczas próby uaktualnienia NuGet, jeśli masz starszą wersję zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="50325-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="50325-108">Obejście polega na po prostu Odinstaluj NuGet, a następnie zainstalować go z galerii rozszerzeń programu VS.</span><span class="sxs-lookup"><span data-stu-id="50325-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="50325-109">Zobacz [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) uzyskać więcej informacji, lub [przejdź bezpośrednio do poprawki programu VS](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="50325-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="50325-110">Uwaga: Jeśli program Visual Studio nie pozwalają na odinstalować rozszerzenie (przycisk Odinstaluj jest wyłączony), prawdopodobnie musisz ponownie program Visual Studio za pomocą polecenia "Uruchom jako Administrator".</span><span class="sxs-lookup"><span data-stu-id="50325-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="50325-111">Pakiet przywracania zgody jest teraz aktywna</span><span class="sxs-lookup"><span data-stu-id="50325-111">Package restore consent is now active</span></span>

<span data-ttu-id="50325-112">Zgodnie z opisem w tym [publikować zgody przywracania pakietu](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet w wersji 2.0 będzie wymagać teraz od o wyrażenie zgody umożliwiające przywracanie pakietu przejdź do trybu online i pobierania pakietów.</span><span class="sxs-lookup"><span data-stu-id="50325-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="50325-113">Upewnij się, czy podane zgodę za pomocą okna dialogowego konfiguracji dla Menedżera pakietów lub zmiennej środowiskowej EnableNuGetPackageRestore.</span><span class="sxs-lookup"><span data-stu-id="50325-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="50325-114">Grupa zależności według platform docelowych</span><span class="sxs-lookup"><span data-stu-id="50325-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="50325-115">Począwszy od wersji 2.0, pakietów, które mogą się różnić w zależności oparte na profilu framework projektu docelowego.</span><span class="sxs-lookup"><span data-stu-id="50325-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="50325-116">Jest to realizowane przy użyciu zaktualizowanych `.nuspec` schematu.</span><span class="sxs-lookup"><span data-stu-id="50325-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="50325-117">`<dependencies>` Elementu może teraz zawierać zestaw `<group>` elementów.</span><span class="sxs-lookup"><span data-stu-id="50325-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="50325-118">Każda grupa zawiera zero lub więcej `<dependency>` elementy i `targetFramework` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="50325-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="50325-119">Wszystkie zależności wewnątrz grupy są instalowane razem, gdy platforma docelowa jest zgodny z profil platformy docelowej projektu.</span><span class="sxs-lookup"><span data-stu-id="50325-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="50325-120">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="50325-120">For example:</span></span>

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

<span data-ttu-id="50325-121">Należy zauważyć, że grupa może zawierać **zero** zależności.</span><span class="sxs-lookup"><span data-stu-id="50325-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="50325-122">W powyższym przykładzie Jeśli pakiet jest zainstalowany w projekcie, który jest przeznaczony dla programu Silverlight 3.0 lub nowszej, żadne zależności zostanie zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="50325-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="50325-123">Jeśli pakiet jest zainstalowany w projekcie, który jest przeznaczony dla programu .NET 4.0 lub nowszy, dwie zależności, jQuery i WebActivator, zostanie zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="50325-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="50325-124">Jeśli pakiet jest zainstalowany w projekcie, który jest przeznaczony dla starszej wersji tych struktur 2 lub innych framework, zostanie zainstalowana RouteMagic 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="50325-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="50325-125">Brak nie dziedziczenia między grupami.</span><span class="sxs-lookup"><span data-stu-id="50325-125">There is no inheritance between groups.</span></span> <span data-ttu-id="50325-126">Jeśli platforma docelowa projektu odpowiada `targetFramework` atrybut grupy, tylko zależności w ramach tej grupy zostaną zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="50325-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="50325-127">Pakiet można określić zależności pakietów w jednym z dwóch formatów: stary format płaską listę `<dependency>` elementów lub grup.</span><span class="sxs-lookup"><span data-stu-id="50325-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="50325-128">Jeśli `<group>` jest używany format, nie można zainstalować pakietu do pakietu nuget w wersji wcześniejszej niż w wersji 2.0.</span><span class="sxs-lookup"><span data-stu-id="50325-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="50325-129">Należy pamiętać, że mieszanie dwa formaty jest niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="50325-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="50325-130">Na przykład poniższy fragment kodu jest **nieprawidłowy** i zostanie odrzucony przez NuGet.</span><span class="sxs-lookup"><span data-stu-id="50325-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="50325-131">Pliki zawartości i skryptów programu PowerShell są grupowane według platformy docelowej</span><span class="sxs-lookup"><span data-stu-id="50325-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="50325-132">Oprócz odwołania do zestawów pliki zawartości i skryptów programu PowerShell także można grupować według wartości docelowej.</span><span class="sxs-lookup"><span data-stu-id="50325-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="50325-133">Tę samą strukturę folderów znaleziony w `lib` folderu do określania wartości docelowej można teraz stosować w taki sam sposób, aby `content` i `tools` folderów.</span><span class="sxs-lookup"><span data-stu-id="50325-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="50325-134">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="50325-134">For example:</span></span>

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

<span data-ttu-id="50325-135">**Uwaga**: ponieważ `init.ps1` jest wykonywane na poziomie rozwiązania i jest nie jest ona zależna od dowolnego pojedynczego projektu, musi zostać umieszczony bezpośrednio pod `tools` folderu.</span><span class="sxs-lookup"><span data-stu-id="50325-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="50325-136">Umieszczony w folderze określonej platformy, zostaną zignorowane.</span><span class="sxs-lookup"><span data-stu-id="50325-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="50325-137">Ponadto jest nowa funkcja NuGet w wersji 2.0, że folder struktury może być *pusty*, w którym to przypadku NuGet zostanie nie Dodawanie odwołania do zestawów, dodać pliki zawartości lub Uruchamiaj skrypty programu PowerShell dla konkretnego framework w wersji.</span><span class="sxs-lookup"><span data-stu-id="50325-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="50325-138">W przykładzie powyżej folderu `content\net40` jest pusty.</span><span class="sxs-lookup"><span data-stu-id="50325-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="50325-139">Wydajność uzupełniania ulepszone karty</span><span class="sxs-lookup"><span data-stu-id="50325-139">Improved tab completion performance</span></span>
<span data-ttu-id="50325-140">Funkcję uzupełniania kartę w konsoli Menedżera pakietów NuGet został zaktualizowany w celu znacznego podniesienia wydajności.</span><span class="sxs-lookup"><span data-stu-id="50325-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="50325-141">Będzie znacznie mniejsze opóźnienie od chwili, gdy naciskania klawisza tab, aż pojawi się lista rozwijana sugestii.</span><span class="sxs-lookup"><span data-stu-id="50325-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="50325-142">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="50325-142">Bug Fixes</span></span>
<span data-ttu-id="50325-143">NuGet w wersji 2.0 obejmuje wiele poprawek błędów, z naciskiem na wydajność i zgody przywracania pakietu.</span><span class="sxs-lookup"><span data-stu-id="50325-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="50325-144">Aby uzyskać pełną listę prac elementy rozwiązane w NuGet w wersji 2.0, widok [NuGet narzędzie do śledzenia problemów w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="50325-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
