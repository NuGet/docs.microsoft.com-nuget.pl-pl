---
title: Informacje o wersji 3.1 NuGet
description: Informacje o wersji programu NuGet 3.1, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 779567d94a5a9a1b3eacddaa4c882201a446cb4b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545350"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="e39a9-103">Informacje o wersji 3.1 NuGet</span><span class="sxs-lookup"><span data-stu-id="e39a9-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="e39a9-104">[Informacje o wersji NuGet 3.0](../release-notes/nuget-3.0.0.md) | [informacjach o wersji NuGet 3.1.1](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="e39a9-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="e39a9-105">NuGet 3.1 została wydana 27 lipca 2015 r. jako powiązane rozszerzenie do zestawu Universal Windows Platform SDK dla programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="e39a9-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="e39a9-106">Dostarczona przez nas tej wersji przy użyciu zestawu SDK platformy Windows tak, aby środowisko programistyczne Windows można korzystać z zalet pracy dla wielu platform NuGet, który zostało wcześniej uruchomione.</span><span class="sxs-lookup"><span data-stu-id="e39a9-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="e39a9-107">Ta wersja rozszerzenia NuGet jest dostępna tylko dla programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="e39a9-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="e39a9-108">Firma Microsoft zaleca tych deweloperów, które mają dostęp do aktualizacji galerii programu Visual Studio do najnowszej wersji, która jest dostępna, ponieważ obecnie publikujemy zawsze aktualizacji za pomocą poprawki i nowe funkcje.</span><span class="sxs-lookup"><span data-stu-id="e39a9-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="e39a9-109">Rozszerzenie programu NuGet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e39a9-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="e39a9-110">Problemy i funkcje w tej wersji są oznaczone w serwisie GitHub przy użyciu [punktu kontrolnego "3.1 platformy uniwersalnej systemu Windows w wersji RTM przechodnie support"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) ogółem, firma Microsoft zamknięte 67 problemy w wersji 3.1.</span><span class="sxs-lookup"><span data-stu-id="e39a9-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="e39a9-111">Nowe funkcje</span><span class="sxs-lookup"><span data-stu-id="e39a9-111">New Features</span></span>

* <span data-ttu-id="e39a9-112">`project.json` Obsługa pomocy technicznej Windows platformy uniwersalnej systemu Windows i program ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="e39a9-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="e39a9-113">Instalacja pakietów przechodnich</span><span class="sxs-lookup"><span data-stu-id="e39a9-113">Transitive package installation</span></span>

<span data-ttu-id="e39a9-114">Opis i definicji tych funkcji można znaleźć innym miejscu, w dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="e39a9-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="e39a9-115">przestarzałe</span><span class="sxs-lookup"><span data-stu-id="e39a9-115">Deprecated</span></span>

<span data-ttu-id="e39a9-116">Następujące funkcje nie są już dostępne dla programu Visual Studio 2015:</span><span class="sxs-lookup"><span data-stu-id="e39a9-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="e39a9-117">Nie można zainstalować pakietów poziomu rozwiązania</span><span class="sxs-lookup"><span data-stu-id="e39a9-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="e39a9-118">Następujące funkcje nie są już dostępne dla programu Visual Studio 2015 i projekty, które używają `project.json` specyfikacji</span><span class="sxs-lookup"><span data-stu-id="e39a9-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="e39a9-119">`install.ps1` i `uninstall.ps1` — te skrypty będą ignorowane podczas instalowania pakietu, przywracanie, aktualizacji i Odinstaluj</span><span class="sxs-lookup"><span data-stu-id="e39a9-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="e39a9-120">Transformacje konfiguracji zostaną zignorowane.</span><span class="sxs-lookup"><span data-stu-id="e39a9-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="e39a9-121">Zawartość zostanie przekazane, ale nie są kopiowane do projektu.</span><span class="sxs-lookup"><span data-stu-id="e39a9-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="e39a9-122">Zespół dokłada starań, aby ponownie zaimplementować tę funkcję, Śledź dyskusję i postęp na: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="e39a9-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="e39a9-123">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="e39a9-123">Known Issues</span></span>

<span data-ttu-id="e39a9-124">Wystąpiły szereg znanych problemów dostarczone w tej wersji.</span><span class="sxs-lookup"><span data-stu-id="e39a9-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="e39a9-125">Instalacji w wersji 3.1 za pomocą zestawu Windows 10 SDK spowoduje obniżenia poziomu dowolnej wersji rozszerzenia NuGet, który został wcześniej zainstalowany</span><span class="sxs-lookup"><span data-stu-id="e39a9-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="e39a9-126">Wiersza polecenia NuGet</span><span class="sxs-lookup"><span data-stu-id="e39a9-126">NuGet Command-line</span></span>

<span data-ttu-id="e39a9-127">Plik wykonywalny wiersza polecenia NuGet został zaktualizowany i przeniesione do nowej lokalizacji dystrybucyjny wersji historycznych tego nuget.exe mogą w dalszym ciągu być udostępniane.</span><span class="sxs-lookup"><span data-stu-id="e39a9-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="e39a9-128">Można pobrać wersji 3.1 beta nuget.exe dla Windows na: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="e39a9-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="e39a9-129">Nowa lokalizacja dystrybucyjny znajduje się na hoście dist.nuget.org przy użyciu struktury folderów, który następuje po ten szablon:</span><span class="sxs-lookup"><span data-stu-id="e39a9-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a><span data-ttu-id="e39a9-130">Nowe funkcje</span><span class="sxs-lookup"><span data-stu-id="e39a9-130">New Features</span></span>

* <span data-ttu-id="e39a9-131">nuget.exe można przywrócić i zainstaluj pakiety do projektów, które używają `project.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="e39a9-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="e39a9-132">nuget.exe mogą połączyć się i wykorzystywać protokołu NuGet w wersji 3 na: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="e39a9-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="e39a9-133">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="e39a9-133">Known Issues</span></span> ##

1.    <span data-ttu-id="e39a9-134">Nie można wykonać pakiet względem `project.json` pliku — [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="e39a9-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="e39a9-135">Nie jest obsługiwana w Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="e39a9-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="e39a9-136">Element nie jest lokalizowany - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="e39a9-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="e39a9-137">Nie jest podpisany, podobnie jak istniejące http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="e39a9-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
