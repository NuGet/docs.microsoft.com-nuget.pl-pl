---
title: Informacje o wersji NuGet 2.8.5
description: Informacje o wersji programu NuGet 2.8.5 tym — znane problemy, poprawki, dodatkowe funkcje i dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 40557035e445d07e7acf301e34b750b329ba9990
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820082"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="ec268-103">Informacje o wersji NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="ec268-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="ec268-104">[Informacje o wersji NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 informacje o wersji](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="ec268-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="ec268-105">NuGet 2.8.5 wydanej w dniu 30 marca 2015 roku.</span><span class="sxs-lookup"><span data-stu-id="ec268-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="ec268-106">Jest to aktualizacja pomocnicza do naszej 2.8.3 VSIX niektóre docelowe poprawki.</span><span class="sxs-lookup"><span data-stu-id="ec268-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="ec268-107">W tej wersji dodano obsługę dla okna dialogowego Menedżer pakietów NuGet [DNX docelowej Framework monikerów](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="ec268-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="ec268-108">Te nowe monikerów framework, które są obsługiwane następujące:</span><span class="sxs-lookup"><span data-stu-id="ec268-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="ec268-109">**core50** — "base" target framework moniker (TFM) zgodny z Core CLR.</span><span class="sxs-lookup"><span data-stu-id="ec268-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="ec268-110">**dnx452** — A TFM aplikacji określonym na podstawie DNX przy użyciu 4.5.2 pełnej wersji platformy</span><span class="sxs-lookup"><span data-stu-id="ec268-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="ec268-111">**dnx46** — A TFM aplikacji określonym na podstawie DNX przy użyciu 4.6 pełnej wersji platformy</span><span class="sxs-lookup"><span data-stu-id="ec268-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="ec268-112">**dnxcore50** — A TFM aplikacji określonym na podstawie środowiska DNX za pomocą wersji Core 5.0 Framework</span><span class="sxs-lookup"><span data-stu-id="ec268-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="ec268-113">Jeden błąd został rozwiązany tego uniemożliwił pakietów instalacji do projektów języka FSharp prawidłowo:</span><span class="sxs-lookup"><span data-stu-id="ec268-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400