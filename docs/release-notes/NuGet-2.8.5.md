---
title: Informacje o wersji narzędzia NuGet 2.8.5
description: Informacje o wersji programu NuGet 2.8.5, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f729092bc964b286a007564bd3bbd8c79bc895c9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780360"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="8cfe6-103">Informacje o wersji narzędzia NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="8cfe6-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="8cfe6-104">Informacje o wersji narzędzia [NuGet 2.8.3](../release-notes/nuget-2.8.3.md)  |  [Informacje o wersji narzędzia NuGet 2.8.6](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="8cfe6-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="8cfe6-105">2.8.5 NuGet wydano 30 marca 2015.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="8cfe6-106">Jest to drobna aktualizacja naszego 2.8.3 VSIX z niektórymi poprawkami.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="8cfe6-107">W tej wersji dodano okno dialogowe obsługa Menedżera pakietów NuGet dla [monikerów platformy docelowej środowiska DNX](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="8cfe6-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="8cfe6-108">Te nowe monikery struktury, które są obsługiwane, obejmują:</span><span class="sxs-lookup"><span data-stu-id="8cfe6-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="8cfe6-109">**core50** — moniker platformy docelowej "Base" (TFM), który jest zgodny z rdzeniem CLR.</span><span class="sxs-lookup"><span data-stu-id="8cfe6-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="8cfe6-110">**dnx452** -A TFM specyficzne dla aplikacji opartych na środowiska dnxch przy użyciu pełnej wersji 4.5.2 platformy</span><span class="sxs-lookup"><span data-stu-id="8cfe6-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="8cfe6-111">**dnx46** -A TFM specyficzne dla aplikacji opartych na środowiska dnxach przy użyciu pełnej wersji 4,6 platformy</span><span class="sxs-lookup"><span data-stu-id="8cfe6-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="8cfe6-112">**dnxcore50** -A TFM specyficzne dla aplikacji opartych na środowiska DNX przy użyciu podstawowej wersji 5,0 platformy</span><span class="sxs-lookup"><span data-stu-id="8cfe6-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="8cfe6-113">Rozwiązano problem polegający na tym, że uniemożliwiło zainstalowanie pakietów w projektach FSharp:</span><span class="sxs-lookup"><span data-stu-id="8cfe6-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400