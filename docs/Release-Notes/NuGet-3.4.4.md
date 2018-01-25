---
title: Informacje o wersji NuGet 3.4.4 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informacje o wersji programu NuGet 3.4.4 tym — znane problemy, poprawki, dodatkowe funkcje i dcr."
keywords: NuGet 3.4.4 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fabc10ae5c8e0bd43581f85c7763eb23e9483aaf
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="1cdaf-104">Informacje o wersji NuGet 3.4.4</span><span class="sxs-lookup"><span data-stu-id="1cdaf-104">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="1cdaf-105">[Informacje o wersji NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [informacje o wersji 3.5 Beta NuGet](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="1cdaf-105">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="1cdaf-106">Głównym celem tej wersji zostało ulepszenia jakości 3.4.3 wersji nuget.exe kilka poprawki z rozszerzeniem programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1cdaf-106">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="1cdaf-107">Możesz pobrać zarówno VSIX, jak i nuget.exe [tutaj](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="1cdaf-107">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="1cdaf-108">[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="1cdaf-108">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="1cdaf-109">Pełny wykaz zmian</span><span class="sxs-lookup"><span data-stu-id="1cdaf-109">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="1cdaf-110">Lista problemów</span><span class="sxs-lookup"><span data-stu-id="1cdaf-110">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="1cdaf-111">Zmiany</span><span class="sxs-lookup"><span data-stu-id="1cdaf-111">Changes</span></span>

- <span data-ttu-id="1cdaf-112">Ulepszenia pakietu: Ulepszenia pakowanie symboli, pakowanie z `project.json` i więcej [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="1cdaf-112">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="1cdaf-113">Wyświetlanie wyjątku po awarii, znajdowanie projekty w poleceniu aktualizacji [\#605] (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="1cdaf-113">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="1cdaf-114">Typ pakietu do odczytu z wejścia `.nuspec` i `project.json` podczas pakowania [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="1cdaf-114">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="1cdaf-115">Należy NuGet.Shared nie w projekcie.</span><span class="sxs-lookup"><span data-stu-id="1cdaf-115">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="1cdaf-116">\#602</span><span class="sxs-lookup"><span data-stu-id="1cdaf-116">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="1cdaf-117">Użyj limit wypychania jako limitu czasu odpowiedzi HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="1cdaf-117">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="1cdaf-118">Nie ma plików pakietu wraz z czasem przyszłych ich przypadków użycia [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="1cdaf-118">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="1cdaf-119">Aktualizowanie `NuGet.Core.dll` wersji 2.12.0, aby rozwiązać problem XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="1cdaf-119">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="1cdaf-120">Obsługuje./NuGet.CommandLine.XPlat - v \<szczegółowości\> \<tryb\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="1cdaf-120">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="1cdaf-121">Wyświetl wystąpił błąd podczas przywracania bez `project.json` lub `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="1cdaf-121">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="1cdaf-122">Ustalenie wersje zależności wymagane wersje różnią się [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="1cdaf-122">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>