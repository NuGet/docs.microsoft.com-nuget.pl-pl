---
title: Informacje o wersji NuGet 2.8.1
description: Informacje o wersji programu NuGet 2.8.1 tym — znane problemy, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39fb7db00e18e32eef15adc11764a122c97ddfd5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545242"
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="a6b47-103">Informacje o wersji NuGet 2.8.1</span><span class="sxs-lookup"><span data-stu-id="a6b47-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="a6b47-104">[Informacje o wersji NuGet 2.8](../release-notes/nuget-2.8.md) | [informacjach o wersji NuGet 2.8.2](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="a6b47-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="a6b47-105">NuGet 2.8.1 został wydany 2 kwietnia 2014 r.</span><span class="sxs-lookup"><span data-stu-id="a6b47-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="a6b47-106">Ważne funkcje w wersji</span><span class="sxs-lookup"><span data-stu-id="a6b47-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="a6b47-107">Obsługa systemu Windows Phone 8.1 projektów</span><span class="sxs-lookup"><span data-stu-id="a6b47-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="a6b47-108">Ta wersja obsługuje teraz następujące nowe target framework monikerów, które może służyć do projektów docelowych Windows Phone 8.1:</span><span class="sxs-lookup"><span data-stu-id="a6b47-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="a6b47-109">WindowsPhone81 / WP81 (dla projektów Windows Phone opartych na technologii Silverlight)</span><span class="sxs-lookup"><span data-stu-id="a6b47-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="a6b47-110">WindowsPhoneApp81 / WPA81 (w przypadku projektów opartych na WinRT aplikacji Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="a6b47-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="a6b47-111">Aktualizuj rozszerzenie NuGet w programie WebMatrix</span><span class="sxs-lookup"><span data-stu-id="a6b47-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="a6b47-112">W tej wersji aktualizacji klienta programu NuGet w programie WebMatrix można [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 i wiąże z funkcji takich jak XDT przekształcenia.</span><span class="sxs-lookup"><span data-stu-id="a6b47-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="a6b47-113">Co ważniejsze, 2.6.1 aktualizacja core umożliwia instalowanie pakietów NuGet, które znajdują się nowsze wersje klienta programu WebMatrix `.nuspec` schemat, który zawiera pakiety ASP.NET NuGet.</span><span class="sxs-lookup"><span data-stu-id="a6b47-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="a6b47-114">Aby uzyskać więcej informacji na temat aktualizacji rozszerzenia programu WebMatrix, zobacz te, które są określone [informacje o wersji](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span><span class="sxs-lookup"><span data-stu-id="a6b47-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="a6b47-115">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="a6b47-115">Bug Fixes</span></span>
<span data-ttu-id="a6b47-116">Poza tymi funkcjami w tej wersji programu NuGet zawiera inne poprawki błędów.</span><span class="sxs-lookup"><span data-stu-id="a6b47-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="a6b47-117">Wystąpiły 16 Suma problemów, które zostały rozwiązane w wydaniu.</span><span class="sxs-lookup"><span data-stu-id="a6b47-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="a6b47-118">Pełną listę prac elementy rozwiązane w NuGet 2.8.1, sprawdź widok [NuGet narzędzie do śledzenia problemów w tej wersji](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="a6b47-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="a6b47-119">Reshipping z programem Visual Studio "14" CTP</span><span class="sxs-lookup"><span data-stu-id="a6b47-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="a6b47-120">W wersji CTP programu Visual Studio "14" wydana w czerwcu 2014 3rd NuGet 2.8.1 jest dostarczany w polu.</span><span class="sxs-lookup"><span data-stu-id="a6b47-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="a6b47-121">Funkcje, ale obsługuje pozostają w par przy użyciu innych 2.8.1 VSIXes, takiego jak Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="a6b47-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
