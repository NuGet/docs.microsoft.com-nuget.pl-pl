---
title: Informacje o wersji 3.1 NuGet
description: Informacje o wersji dla tym znanych problemów, poprawki, dodatkowe funkcje i dcr 3.1 NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d14455da6f8af4db92f7105ea1b0e88eb9e71600
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820880"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="96c75-103">Informacje o wersji 3.1 NuGet</span><span class="sxs-lookup"><span data-stu-id="96c75-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="96c75-104">[Informacje o wersji NuGet 3.0](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 informacje o wersji](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="96c75-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="96c75-105">NuGet 3.1 został wydany w dniu 27 lipca 2015 roku jako rozszerzenie powiązane do uniwersalnego zestawu SDK platformy Windows dla programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="96c75-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="96c75-106">Dostarczana tej wersji przy użyciu zestawu SDK platformy systemu Windows tak, aby środowisko programistyczne systemu Windows można wykorzystać do pracy i platform NuGet, które zostało wcześniej uruchomione.</span><span class="sxs-lookup"><span data-stu-id="96c75-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="96c75-107">Ta wersja rozszerzenia NuGet jest dostępna tylko dla programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="96c75-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="96c75-108">Firma Microsoft zaleca tych projektantów, którzy mają dostęp do galerii Visual Studio aktualizacji do najnowszej wersji, która jest dostępna, ponieważ firma Microsoft zawsze publikują aktualizacji za pomocą poprawki i nowe funkcje.</span><span class="sxs-lookup"><span data-stu-id="96c75-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="96c75-109">Rozszerzenie programu NuGet dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="96c75-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="96c75-110">Problemy i funkcji w tej wersji są oznaczone w serwisie GitHub z [punkt kontrolny "3.1 Obsługa przechodnie RTM platformy uniwersalnej systemu Windows"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) w całości, możemy zamknięte 67 problemów w wersji 3.1.</span><span class="sxs-lookup"><span data-stu-id="96c75-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="96c75-111">Nowe funkcje</span><span class="sxs-lookup"><span data-stu-id="96c75-111">New Features</span></span>

* <span data-ttu-id="96c75-112">`project.json` Obsługa pomocy technicznej systemu Windows i programu ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="96c75-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="96c75-113">Instalacja pakietu przechodnie</span><span class="sxs-lookup"><span data-stu-id="96c75-113">Transitive package installation</span></span>

<span data-ttu-id="96c75-114">Opis i definicji pojęć dotyczących tych funkcji można znaleźć w innym miejscu, w dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="96c75-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="96c75-115">Przestarzałe</span><span class="sxs-lookup"><span data-stu-id="96c75-115">Deprecated</span></span>

<span data-ttu-id="96c75-116">Następujące funkcje nie są już dostępne dla programu Visual Studio 2015:</span><span class="sxs-lookup"><span data-stu-id="96c75-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="96c75-117">Nie można zainstalować pakietów poziomu rozwiązania</span><span class="sxs-lookup"><span data-stu-id="96c75-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="96c75-118">Następujące funkcje nie są już dostępne dla programu Visual Studio 2015 i projekty, które używają `project.json` specyfikacji</span><span class="sxs-lookup"><span data-stu-id="96c75-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="96c75-119">`install.ps1` i `uninstall.ps1` -te skrypty zostaną zignorowane podczas instalacji pakietu, przywracania, aktualizacji i odinstalowywania</span><span class="sxs-lookup"><span data-stu-id="96c75-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="96c75-120">Transformacje konfiguracji zostaną zignorowane.</span><span class="sxs-lookup"><span data-stu-id="96c75-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="96c75-121">Zawartość będzie wykonywane, ale nie został skopiowany do projektu.</span><span class="sxs-lookup"><span data-stu-id="96c75-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="96c75-122">Zespół pracuje nad ponownie zaimplementować tę funkcję, wykonaj dyskusji i postępu na: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="96c75-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="96c75-123">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="96c75-123">Known Issues</span></span>

<span data-ttu-id="96c75-124">Wystąpiły znane problemy występujące w dostarczone w tej wersji.</span><span class="sxs-lookup"><span data-stu-id="96c75-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="96c75-125">Instalacja wersji 3.1 z zestawu Windows 10 SDK będzie obniżyć dowolnej wersji rozszerzenia NuGet, który został wcześniej zainstalowany</span><span class="sxs-lookup"><span data-stu-id="96c75-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="96c75-126">NuGet wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="96c75-126">NuGet Command-line</span></span>

<span data-ttu-id="96c75-127">Plik wykonywalny wiersza polecenia NuGet został zaktualizowany i przeniesione do nowej lokalizacji dystrybucyjnego historię wersji nuget.exe mogą w dalszym ciągu udostępnione.</span><span class="sxs-lookup"><span data-stu-id="96c75-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="96c75-128">Można pobrać wersji 3.1 beta nuget.exe dla systemu Windows na: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="96c75-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="96c75-129">Nową lokalizację dystrybucyjnego znajduje się na tym hoście dist.nuget.org ze strukturą folder znajdujący się tego szablonu:</span><span class="sxs-lookup"><span data-stu-id="96c75-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a><span data-ttu-id="96c75-130">Nowe funkcje</span><span class="sxs-lookup"><span data-stu-id="96c75-130">New Features</span></span>

* <span data-ttu-id="96c75-131">nuget.exe można przywrócić i zainstalować pakiety w projektach, które używają `project.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="96c75-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="96c75-132">nuget.exe łączyć się i korzystać z protokołu NuGet w wersji 3 w: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="96c75-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="96c75-133">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="96c75-133">Known Issues</span></span> ##

1.    <span data-ttu-id="96c75-134">Nie można wykonać pakiet przed `project.json` pliku - [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="96c75-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="96c75-135">Nie jest obsługiwany w jedno - [1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="96c75-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="96c75-136">Nie jest lokalizowany - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="96c75-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="96c75-137">Nie jest podpisany, podobnie jak istniejące http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="96c75-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
