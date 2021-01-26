---
title: Informacje o wersji narzędzia NuGet 2.8.1
description: Informacje o wersji programu NuGet 2.8.1, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4dcd8ab140026c39345f850ac00a7a5f26a0e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776764"
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="8ae08-103">Informacje o wersji narzędzia NuGet 2.8.1</span><span class="sxs-lookup"><span data-stu-id="8ae08-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="8ae08-104">Informacje o wersji narzędzia [NuGet 2,8](../release-notes/nuget-2.8.md)  |  [Informacje o wersji narzędzia NuGet 2.8.2](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="8ae08-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="8ae08-105">Pakiet NuGet 2.8.1 został opublikowany 2 kwietnia 2014.</span><span class="sxs-lookup"><span data-stu-id="8ae08-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="8ae08-106">Istotne funkcje w wersji</span><span class="sxs-lookup"><span data-stu-id="8ae08-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="8ae08-107">Obsługa projektów Windows Phone 8,1</span><span class="sxs-lookup"><span data-stu-id="8ae08-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="8ae08-108">Ta wersja obsługuje teraz następujące nowe monikery platformy docelowej, które mogą być używane do celów projektów Windows Phone 8,1:</span><span class="sxs-lookup"><span data-stu-id="8ae08-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="8ae08-109">WindowsPhone81/WP81 (dla projektów Windows Phone opartych na programie Silverlight)</span><span class="sxs-lookup"><span data-stu-id="8ae08-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="8ae08-110">WindowsPhoneApp81/WPA81 (dla projektów aplikacji Windows Phone opartych na WinRT)</span><span class="sxs-lookup"><span data-stu-id="8ae08-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="8ae08-111">Aktualizacja rozszerzenia WebMatrix narzędzia NuGet</span><span class="sxs-lookup"><span data-stu-id="8ae08-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="8ae08-112">W tej wersji zostanie zaktualizowany klient NuGet znaleziony w programie WebMatrix do [NuGet. Core.](https://www.nuget.org/packages/Nuget.Core/2.6.1)</span><span class="sxs-lookup"><span data-stu-id="8ae08-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="8ae08-113">Co ważniejsze, aktualizacja "ACS Core" umożliwia klientowi WebMatrix zainstalowanie pakietów NuGet, które zawierają nowsze wersje `.nuspec` schematu, w tym pakiety nuget ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8ae08-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="8ae08-114">Aby uzyskać więcej informacji na temat aktualizacji rozszerzenia WebMatrix, zobacz te szczegółowe informacje o [wersji](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span><span class="sxs-lookup"><span data-stu-id="8ae08-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="8ae08-115">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="8ae08-115">Bug Fixes</span></span>
<span data-ttu-id="8ae08-116">Oprócz tych funkcji Ta wersja programu NuGet zawiera inne poprawki błędów.</span><span class="sxs-lookup"><span data-stu-id="8ae08-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="8ae08-117">Wystąpiło 16 łącznych problemów rozwiązanych w wydaniu.</span><span class="sxs-lookup"><span data-stu-id="8ae08-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="8ae08-118">Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 2.8.1, zobacz [Śledzenie problemów NuGet dla tej wersji](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="8ae08-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="8ae08-119">Wysyłka przy użyciu programu Visual Studio "14" CTP</span><span class="sxs-lookup"><span data-stu-id="8ae08-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="8ae08-120">W programie Visual Studio "14" CTP wydanej 3 czerwca 2014, pakiet NuGet 2.8.1 jest dostarczany w tym polu.</span><span class="sxs-lookup"><span data-stu-id="8ae08-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="8ae08-121">Funkcje, które obsługuje, pozostają w wartości nominalnej z innymi 2.8.1 VSIX, takimi jak jeden dla Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="8ae08-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
