---
title: Informacje o wersji NuGet 2.0 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 51c7e94f-0084-4c62-bfba-7dfd81675361
description: "Informacje o wersji dotyczące tym znanych problemów, poprawki, dodatkowe funkcje i dcr NuGet w wersji 2.0."
keywords: NuGet 2.0 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 41eed1a7c6ad91d63813fb74986aa498765f3dea
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="59cf0-104">Informacje o wersji 2.0 NuGet</span><span class="sxs-lookup"><span data-stu-id="59cf0-104">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="59cf0-105">[Informacje o wersji NuGet 1.8](../release-notes/nuget-1.8.md) | [NuGet 2.1 informacje o wersji](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="59cf0-105">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="59cf0-106">19 czerwca 2012 został wydany NuGet 2.0.</span><span class="sxs-lookup"><span data-stu-id="59cf0-106">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="59cf0-107">Znane problem</span><span class="sxs-lookup"><span data-stu-id="59cf0-107">Known Installation Issue</span></span>
<span data-ttu-id="59cf0-108">Jeśli korzystasz z VS 2010 z dodatkiem SP1, możesz napotkać błąd instalacji podczas próby uaktualnienia NuGet, jeśli masz starszą wersję zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="59cf0-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="59cf0-109">Obejście jest po prostu odinstalować NuGet, a następnie zainstaluj go z galerii rozszerzeń programu VS.</span><span class="sxs-lookup"><span data-stu-id="59cf0-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="59cf0-110">Zobacz [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) uzyskać więcej informacji, lub [przejdź bezpośrednio do poprawki VS](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="59cf0-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="59cf0-111">Uwaga: Jeśli program Visual Studio nie pozwalają na odinstalować rozszerzenia (przycisk Odinstaluj jest wyłączony), następnie prawdopodobnie konieczne ponowne uruchomienie programu Visual Studio za pomocą polecenia "Uruchom jako Administrator".</span><span class="sxs-lookup"><span data-stu-id="59cf0-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="59cf0-112">Jest teraz aktywny zgody przywracania pakietu</span><span class="sxs-lookup"><span data-stu-id="59cf0-112">Package restore consent is now active</span></span>

<span data-ttu-id="59cf0-113">Zgodnie z opisem w tym [post na zgody przywracania pakietu](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 będzie teraz wymagać o wyrażenie zgody umożliwiające przywracanie pakietów przejść do trybu online i pobrać pakietów.</span><span class="sxs-lookup"><span data-stu-id="59cf0-113">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="59cf0-114">Upewnij się, że podanych zgody za pomocą okna dialogowego konfiguracji Menedżera pakietów lub zmiennej środowiskowej EnableNuGetPackageRestore.</span><span class="sxs-lookup"><span data-stu-id="59cf0-114">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="59cf0-115">Zależności grupy według platform docelowych</span><span class="sxs-lookup"><span data-stu-id="59cf0-115">Group dependencies by target frameworks</span></span>

<span data-ttu-id="59cf0-116">Począwszy od wersji 2.0, pakiet, który może różnić się zależności oparte na profil platformy docelowej projektu.</span><span class="sxs-lookup"><span data-stu-id="59cf0-116">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="59cf0-117">Odbywa się przy użyciu zaktualizowanych `.nuspec` schematu.</span><span class="sxs-lookup"><span data-stu-id="59cf0-117">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="59cf0-118">`<dependencies>` Element teraz może zawierać zestaw `<group>` elementów.</span><span class="sxs-lookup"><span data-stu-id="59cf0-118">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="59cf0-119">Każda grupa zawiera zero lub więcej `<dependency>` elementów i `targetFramework` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="59cf0-119">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="59cf0-120">Wszystkie zależności w grupie są zainstalowane jednocześnie, jeśli platforma docelowa jest zgodna z profil platformy docelowej projektu.</span><span class="sxs-lookup"><span data-stu-id="59cf0-120">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="59cf0-121">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="59cf0-121">For example:</span></span>

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

<span data-ttu-id="59cf0-122">Należy pamiętać, że grupa może zawierać **zero** zależności.</span><span class="sxs-lookup"><span data-stu-id="59cf0-122">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="59cf0-123">W powyższym przykładzie Jeśli pakiet jest zainstalowany w projekcie, którego celem Silverlight 3.0 lub nowszej, zależności nie zostanie zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="59cf0-123">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="59cf0-124">Jeśli pakiet jest zainstalowany w projekcie, przeznaczonego dla programu .NET 4.0 lub nowszy, dwie zależności, jQuery i WebActivator, zostanie zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="59cf0-124">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="59cf0-125">Po zainstalowaniu pakietu do projektu przeznaczonego dla tych platform 2 lub innych framework wcześniejszą wersję RouteMagic 1.1.0 zostanie zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="59cf0-125">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="59cf0-126">Nie istnieje żadne dziedziczenia między grupami.</span><span class="sxs-lookup"><span data-stu-id="59cf0-126">There is no inheritance between groups.</span></span> <span data-ttu-id="59cf0-127">Jeśli platforma docelowa projektu odpowiada `targetFramework` atrybutu grupy, tylko zależności w ramach tej grupy zostaną zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="59cf0-127">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="59cf0-128">Pakiet można określić zależności pakietów w jednym z dwóch formatów: starym formacie płaska lista `<dependency>` elementy lub grup.</span><span class="sxs-lookup"><span data-stu-id="59cf0-128">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="59cf0-129">Jeśli `<group>` format jest używany, nie można zainstalować pakietu, w wersjach starszych niż 2.0 programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="59cf0-129">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="59cf0-130">Należy pamiętać, że mieszanie dwa formaty jest niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="59cf0-130">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="59cf0-131">Na przykład poniższy fragment kodu jest **nieprawidłowy** i zostanie odrzucony przez narzędzie NuGet.</span><span class="sxs-lookup"><span data-stu-id="59cf0-131">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="59cf0-132">Pliki zawartości i skryptów programu PowerShell są grupowane według platformy docelowej</span><span class="sxs-lookup"><span data-stu-id="59cf0-132">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="59cf0-133">Oprócz odwołania do zestawów pliki zawartości i skryptów programu PowerShell również można przedstawić w rozbiciu platformy docelowej.</span><span class="sxs-lookup"><span data-stu-id="59cf0-133">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="59cf0-134">Znaleziono taką samą strukturę folderów w `lib` folder służący do określania platformy docelowej teraz mogą być stosowane w taki sam sposób, aby `content` i `tools` folderów.</span><span class="sxs-lookup"><span data-stu-id="59cf0-134">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="59cf0-135">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="59cf0-135">For example:</span></span>

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

<span data-ttu-id="59cf0-136">**Uwaga**: ponieważ `init.ps1` jest wykonywane na poziomie rozwiązania i jest niezależne od dowolnego pojedynczego projektu, musi on być umieszczony bezpośrednio pod `tools` folderu.</span><span class="sxs-lookup"><span data-stu-id="59cf0-136">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="59cf0-137">Umieszczony w folderze określonej struktury, będą ignorowane.</span><span class="sxs-lookup"><span data-stu-id="59cf0-137">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="59cf0-138">Nową funkcją w NuGet 2.0 jest również można folderze struktury *pusty*, w którym to przypadku NuGet zostanie nie dodać odwołania do zestawów, dodać pliki zawartości lub uruchamiać skrypty programu PowerShell dla konkretnego framework w wersji.</span><span class="sxs-lookup"><span data-stu-id="59cf0-138">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="59cf0-139">W przykładzie powyżej folderu `content\net40` jest pusta.</span><span class="sxs-lookup"><span data-stu-id="59cf0-139">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="59cf0-140">Ulepszone kartę ukończenia wydajności</span><span class="sxs-lookup"><span data-stu-id="59cf0-140">Improved tab completion performance</span></span>
<span data-ttu-id="59cf0-141">Karta funkcję uzupełniania w konsoli Menedżera pakietów NuGet została zaktualizowana do znacznie poprawić wydajność.</span><span class="sxs-lookup"><span data-stu-id="59cf0-141">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="59cf0-142">Będzie znacznie mniej opóźnienia od momentu, gdy zostanie naciśnięty klawisz tab, aż pojawi się lista rozwijana uwag.</span><span class="sxs-lookup"><span data-stu-id="59cf0-142">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="59cf0-143">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="59cf0-143">Bug Fixes</span></span>
<span data-ttu-id="59cf0-144">NuGet 2.0 zawiera wiele poprawek usterek, ze szczególnym uwzględnieniem zgody przywracania pakietu i wydajność.</span><span class="sxs-lookup"><span data-stu-id="59cf0-144">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="59cf0-145">Pełną listę prac elementów usunięto w wersji NuGet 2.0, sprawdź widok [NuGet Tracker problem w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="59cf0-145">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
