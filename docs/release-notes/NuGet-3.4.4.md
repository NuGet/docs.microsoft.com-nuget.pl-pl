---
title: Informacje o wersji narzędzia NuGet 3.4.4
description: Informacje o wersji programu NuGet 3.4.4, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4e5e635432147afba4809562035bc8c762d31af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780222"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="2b12c-103">Informacje o wersji narzędzia NuGet 3.4.4</span><span class="sxs-lookup"><span data-stu-id="2b12c-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="2b12c-104">Informacje o wersji narzędzia [NuGet 3.4.3](../release-notes/nuget-3.4.3.md)  |  [NuGet 3,5 — informacje o wersji beta](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="2b12c-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="2b12c-105">Głównym celem tej wersji była poprawa jakości 3.4.3 wersji nuget.exe z kilkoma poprawkami do rozszerzenia programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2b12c-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="2b12c-106">W [tym miejscu](https://dist.nuget.org/index.html)możesz pobrać zarówno VSIX, jak i nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="2b12c-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtm-2016-05-19"></a><span data-ttu-id="2b12c-107">[3.4.4 — RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="2b12c-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="2b12c-108">Pełny dziennik zmian</span><span class="sxs-lookup"><span data-stu-id="2b12c-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="2b12c-109">Lista problemów</span><span class="sxs-lookup"><span data-stu-id="2b12c-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="2b12c-110">Zmiany</span><span class="sxs-lookup"><span data-stu-id="2b12c-110">Changes</span></span>

- <span data-ttu-id="2b12c-111">Udoskonalenia pakietu: ulepszenia symboli pakowania, pakowanie z `project.json` i więcej [ \# 606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="2b12c-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="2b12c-112">Wyświetl wyjątek, jeśli wystąpił błąd podczas znajdowania projektów w poleceniu Update [ \# 605] (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="2b12c-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="2b12c-113">Odczytaj typ pakietu z danych wejściowych `.nuspec` i `project.json` przy pakowaniu [ \# 603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="2b12c-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="2b12c-114">Utwórz pakiet NuGet. Udostępnianie nie jest projektem.</span><span class="sxs-lookup"><span data-stu-id="2b12c-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="2b12c-115">\#602</span><span class="sxs-lookup"><span data-stu-id="2b12c-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="2b12c-116">Użyj limitu czasu wypychania jako limitu czasu odpowiedzi HTTP [ \# 599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="2b12c-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="2b12c-117">Pliki pakietu z przyszłymi czasami nie będą używane [ \# 597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="2b12c-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="2b12c-118">Aktualizowanie `NuGet.Core.dll` wersji do 2.12.0 w celu naprawienia problemu XML [ \# 594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="2b12c-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="2b12c-119">Support./NuGet.commandline.XPlat-v \<verbosity\> \<mode\> [ \# 593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="2b12c-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="2b12c-120">Wyświetl błąd przywracania bez `project.json` lub `packages.config` [ \# 590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="2b12c-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="2b12c-121">Naprawianie wersji zależności, gdy wymagane są różne wersje [ \# 559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="2b12c-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>