---
title: Informacje o wersji narzędzia NuGet 3,1
description: Informacje o wersji programu NuGet 3,1, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776530"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="4de9a-103">Informacje o wersji narzędzia NuGet 3,1</span><span class="sxs-lookup"><span data-stu-id="4de9a-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="4de9a-104">Informacje o wersji narzędzia [NuGet 3,0](../release-notes/nuget-3.0.0.md)  |  [Informacje o wersji NuGet 3.1.1](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="4de9a-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="4de9a-105">Pakiet NuGet 3,1 został opublikowany w dniu 27 lipca 2015 jako dołączone rozszerzenie zestawu SDK platforma uniwersalna systemu Windows dla programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="4de9a-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="4de9a-106">Ta wersja została dostarczona z zestawem SDK platformy Windows, aby środowisko programistyczne dla systemu Windows mogło korzystać z pracy międzyplatformowej NuGet, która została wcześniej uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="4de9a-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="4de9a-107">Ta wersja rozszerzenia NuGet jest dostępna tylko dla programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="4de9a-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="4de9a-108">Zalecamy, aby Ci deweloperzy mieli dostęp do aktualizacji galerii programu Visual Studio do najnowszej dostępnej wersji, ponieważ zawsze są publikowane aktualizacje z poprawkami błędów i nowymi funkcjami.</span><span class="sxs-lookup"><span data-stu-id="4de9a-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="4de9a-109">Rozszerzenie NuGet programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4de9a-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="4de9a-110">Problemy i funkcje w tej wersji są otagowane w witrynie GitHub z punktem 3,1 67 [kontrolnym "3,1 RTM platformy uwpe"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  .</span><span class="sxs-lookup"><span data-stu-id="4de9a-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="4de9a-111">Nowe funkcje</span><span class="sxs-lookup"><span data-stu-id="4de9a-111">New Features</span></span>

* <span data-ttu-id="4de9a-112">`project.json` Obsługa systemów Windows platformy UWP i ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="4de9a-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="4de9a-113">Instalacja pakietu przechodniego</span><span class="sxs-lookup"><span data-stu-id="4de9a-113">Transitive package installation</span></span>

<span data-ttu-id="4de9a-114">Opisy i definicje tych funkcji można znaleźć w innym miejscu w dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="4de9a-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="4de9a-115">Przestarzałe</span><span class="sxs-lookup"><span data-stu-id="4de9a-115">Deprecated</span></span>

<span data-ttu-id="4de9a-116">Następujące funkcje nie są już dostępne dla programu Visual Studio 2015:</span><span class="sxs-lookup"><span data-stu-id="4de9a-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="4de9a-117">Nie można już zainstalować pakietów na poziomie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="4de9a-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="4de9a-118">Następujące funkcje nie są już dostępne dla programu Visual Studio 2015 i projektów korzystających ze `project.json` specyfikacji</span><span class="sxs-lookup"><span data-stu-id="4de9a-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="4de9a-119">`install.ps1` i `uninstall.ps1` — te skrypty zostaną zignorowane podczas instalowania pakietu, przywracania, aktualizowania i odinstalowywania</span><span class="sxs-lookup"><span data-stu-id="4de9a-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="4de9a-120">Przekształcenia konfiguracji zostaną zignorowane</span><span class="sxs-lookup"><span data-stu-id="4de9a-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="4de9a-121">Zawartość zostanie przeniesiona, ale nie zostanie skopiowana do projektu.</span><span class="sxs-lookup"><span data-stu-id="4de9a-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="4de9a-122">Zespół pracuje nad ponowną implementacją tej funkcji, postępuj zgodnie z dyskusjami i postępem: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="4de9a-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="4de9a-123">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="4de9a-123">Known Issues</span></span>

<span data-ttu-id="4de9a-124">Wykryto kilka znanych problemów z tą wersją.</span><span class="sxs-lookup"><span data-stu-id="4de9a-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="4de9a-125">Instalacja wersji 3,1 z zestawem SDK systemu Windows 10 spowoduje obniżenie wersji rozszerzenia NuGet, która została wcześniej zainstalowana</span><span class="sxs-lookup"><span data-stu-id="4de9a-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="4de9a-126">Wiersz polecenia NuGet</span><span class="sxs-lookup"><span data-stu-id="4de9a-126">NuGet Command-line</span></span>

<span data-ttu-id="4de9a-127">Plik wykonywalny wiersza polecenia NuGet został zaktualizowany i przeniesiony do nowej lokalizacji dystrybucyjnej, aby można było dalej udostępnić historyczne wersje nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="4de9a-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="4de9a-128">Wersję 3,1 dla systemu Windows w nuget.exe wersji beta można pobrać pod adresem: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="4de9a-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="4de9a-129">Nowa lokalizacja dystrybucji znajduje się na hoście dist.nuget.org z strukturą folderów, która jest zgodna z tym szablonem:</span><span class="sxs-lookup"><span data-stu-id="4de9a-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a><span data-ttu-id="4de9a-130">Nowe funkcje</span><span class="sxs-lookup"><span data-stu-id="4de9a-130">New Features</span></span>

* <span data-ttu-id="4de9a-131">nuget.exe może przywrócić i zainstalować pakiety w projektach korzystających z `project.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="4de9a-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="4de9a-132">nuget.exe może nawiązać połączenie z protokołem NuGet v3 i korzystać z niego w: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="4de9a-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="4de9a-133">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="4de9a-133">Known Issues</span></span> ##

1.    <span data-ttu-id="4de9a-134">Nie można wykonać pakietu dla `project.json` pliku- [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="4de9a-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="4de9a-135">Nie jest obsługiwane w przypadku mono- [1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="4de9a-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="4de9a-136">Nie jest zlokalizowany- [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="4de9a-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="4de9a-137">Nie jest podpisany, podobnie jak istniejący http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="4de9a-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
