---
title: Informacje o wersji NuGet 2.8.5 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informacje o wersji programu NuGet 2.8.5 tym — znane problemy, poprawki, dodatkowe funkcje i dcr."
keywords: NuGet 2.8.5 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ace56284e56f24394d49c0598ec3604b62caaf67
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="1f2c6-104">Informacje o wersji NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="1f2c6-104">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="1f2c6-105">[Informacje o wersji NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 informacje o wersji](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="1f2c6-105">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="1f2c6-106">NuGet 2.8.5 wydanej w dniu 30 marca 2015 roku.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-106">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="1f2c6-107">Jest to aktualizacja pomocnicza do naszej 2.8.3 VSIX niektóre docelowe poprawki.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-107">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="1f2c6-108">W tej wersji dodano obsługę dla okna dialogowego Menedżer pakietów NuGet [DNX docelowej Framework monikerów](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="1f2c6-108">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="1f2c6-109">Te nowe monikerów framework, które są obsługiwane następujące:</span><span class="sxs-lookup"><span data-stu-id="1f2c6-109">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="1f2c6-110">**core50** — "base" target framework moniker (TFM) zgodny z Core CLR.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-110">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="1f2c6-111">**dnx452** — A TFM aplikacji określonym na podstawie DNX przy użyciu 4.5.2 pełnej wersji platformy</span><span class="sxs-lookup"><span data-stu-id="1f2c6-111">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="1f2c6-112">**dnx46** — A TFM aplikacji określonym na podstawie DNX przy użyciu 4.6 pełnej wersji platformy</span><span class="sxs-lookup"><span data-stu-id="1f2c6-112">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="1f2c6-113">**dnxcore50** — A TFM aplikacji określonym na podstawie środowiska DNX za pomocą wersji Core 5.0 Framework</span><span class="sxs-lookup"><span data-stu-id="1f2c6-113">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="1f2c6-114">Jeden błąd został rozwiązany tego uniemożliwił pakietów instalacji do projektów języka FSharp prawidłowo:</span><span class="sxs-lookup"><span data-stu-id="1f2c6-114">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

<span data-ttu-id="1f2c6-115">https://nuget.codeplex.com/workitem/4400</span><span class="sxs-lookup"><span data-stu-id="1f2c6-115">https://nuget.codeplex.com/workitem/4400</span></span>