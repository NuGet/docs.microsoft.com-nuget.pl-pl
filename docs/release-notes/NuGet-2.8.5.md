---
title: Informacje o wersji NuGet 2.8.5
description: Informacje o wersji programu NuGet 2.8.5 tym — znane problemy, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa03b00a0043a4805f33900124c13b0777c2b7a3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548628"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="8eff9-103">Informacje o wersji NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="8eff9-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="8eff9-104">[Informacje o wersji programu NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [informacjach o wersji NuGet 2.8.6](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="8eff9-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="8eff9-105">NuGet 2.8.5 został wydany 30 marca 2015 r.</span><span class="sxs-lookup"><span data-stu-id="8eff9-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="8eff9-106">Jest aktualizację pomocniczą do naszych wersji 2.8.3 VSIX z niektórymi docelowe poprawki.</span><span class="sxs-lookup"><span data-stu-id="8eff9-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="8eff9-107">W tej wersji dodano obsługę dla okna dialogowego Menedżer pakietów NuGet [środowiska DNX Target Framework monikerów](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="8eff9-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="8eff9-108">Te nowe krótkie nazwy framework, które są obsługiwane, obejmują:</span><span class="sxs-lookup"><span data-stu-id="8eff9-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="8eff9-109">**core50** — "base" docelowe moniker struktury (TFM), która jest zgodna z Core CLR.</span><span class="sxs-lookup"><span data-stu-id="8eff9-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="8eff9-110">**dnx452** — TFM specyficzne dla środowiska DNX na podstawie używających 4.5.2 pełną wersję platformy</span><span class="sxs-lookup"><span data-stu-id="8eff9-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="8eff9-111">**dnx46** — TFM specyficzne dla środowiska DNX na podstawie używających 4.6 pełną wersję platformy</span><span class="sxs-lookup"><span data-stu-id="8eff9-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="8eff9-112">**dnxcore50** — TFM: specyficzne dla środowiska DNX na podstawie aplikacji przy użyciu wersji Core 5.0 framework</span><span class="sxs-lookup"><span data-stu-id="8eff9-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="8eff9-113">Jeden błąd został naprawiony tego uniemożliwił pakietów instalacji do projektów języka FSharp prawidłowo:</span><span class="sxs-lookup"><span data-stu-id="8eff9-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400