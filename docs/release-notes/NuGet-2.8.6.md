---
title: Informacje o wersji NuGet 2.8.6
description: Informacje o wersji programu NuGet 2.8.6 tym — znane problemy, poprawki, dodatkowe funkcje i dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ee801a0edfe22888d65506cea557fd9c79dcf7bd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819721"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="4cb0a-103">Informacje o wersji NuGet 2.8.6</span><span class="sxs-lookup"><span data-stu-id="4cb0a-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="4cb0a-104">[Informacje o wersji NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 informacje o wersji](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="4cb0a-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="4cb0a-105">Została wydana NuGet 2.8.6 20 lipca 2015 roku jako pomocnicza aktualizacji do naszej 2.8.5 VSIX niektóre docelowe poprawki i ulepszenia umożliwiające obsługę pakietów, które mogą być dostarczone z obsługą modelu programowania platformy uniwersalnej systemu Windows do systemu Windows 10.</span><span class="sxs-lookup"><span data-stu-id="4cb0a-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="4cb0a-106">Ta wersja rozszerzenia Menedżera pakietów NuGet zapewnia obsługę programu Visual Studio 2013 tylko.</span><span class="sxs-lookup"><span data-stu-id="4cb0a-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="4cb0a-107">W tej wersji okno dialogowe Menedżer pakietów NuGet nie dodano obsługę:</span><span class="sxs-lookup"><span data-stu-id="4cb0a-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="4cb0a-108">Wprowadzono Moniker platformy docelowej UAP do obsługi systemu Windows 10 dla deweloperów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4cb0a-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="4cb0a-109">Punkty końcowe w wersji 3 protokołu NuGet</span><span class="sxs-lookup"><span data-stu-id="4cb0a-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="4cb0a-110">Obsługa [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) atrybut właściwość protocolVersion w źródłach repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="4cb0a-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="4cb0a-111">Wartość domyślna to "2"</span><span class="sxs-lookup"><span data-stu-id="4cb0a-111">Default value is "2"</span></span>
* <span data-ttu-id="4cb0a-112">Nastąpi powrót do zdalnego repozytorium, jeśli wersja wymagany pakiet nie jest dostępny w lokalnej pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="4cb0a-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>