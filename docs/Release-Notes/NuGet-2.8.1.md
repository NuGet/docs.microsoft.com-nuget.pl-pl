---
title: Informacje o wersji NuGet 2.8.1 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informacje o wersji programu NuGet 2.8.1 tym — znane problemy, poprawki, dodatkowe funkcje i dcr."
keywords: NuGet 2.8.1 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 99dd050eb06024972132d5b0dcc9f97f965adc12
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="4bb93-104">Informacje o wersji 2.8.1 NuGet</span><span class="sxs-lookup"><span data-stu-id="4bb93-104">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="4bb93-105">[Informacje o wersji NuGet 2.8](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 informacje o wersji](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="4bb93-105">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="4bb93-106">NuGet 2.8.1 został wydany 2 kwietnia 2014 r.</span><span class="sxs-lookup"><span data-stu-id="4bb93-106">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="4bb93-107">Ważne funkcje w wersji</span><span class="sxs-lookup"><span data-stu-id="4bb93-107">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="4bb93-108">Obsługa systemu Windows Phone 8.1 projektów</span><span class="sxs-lookup"><span data-stu-id="4bb93-108">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="4bb93-109">Ta wersja obsługuje teraz następujące nowe docelowej framework monikerów które mogą być używane do projektów docelowych systemu Windows Phone 8.1:</span><span class="sxs-lookup"><span data-stu-id="4bb93-109">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="4bb93-110">WindowsPhone81 / WP81 (dla projektów Silverlight systemem Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="4bb93-110">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="4bb93-111">WindowsPhoneApp81 / WPA81 (dla projektów opartych na WinRT aplikacji Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="4bb93-111">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="4bb93-112">Aktualizowanie NuGet rozszerzenia programu WebMatrix</span><span class="sxs-lookup"><span data-stu-id="4bb93-112">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="4bb93-113">Ta wersja aktualizacji klienta NuGet w program WebMatrix w celu [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1, a z funkcji takich jak XDT przekształcenia.</span><span class="sxs-lookup"><span data-stu-id="4bb93-113">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="4bb93-114">Co więcej, 2.6.1 aktualizacja core umożliwia klienta programu WebMatrix można zainstalować pakietów NuGet, które znajdują się nowsze wersje `.nuspec` schemat, który zawiera pakiety ASP.NET NuGet.</span><span class="sxs-lookup"><span data-stu-id="4bb93-114">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="4bb93-115">Aby uzyskać więcej informacji na temat aktualizacji rozszerzenia programu WebMatrix, zobacz te określone [informacje o wersji](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span><span class="sxs-lookup"><span data-stu-id="4bb93-115">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="4bb93-116">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="4bb93-116">Bug Fixes</span></span>
<span data-ttu-id="4bb93-117">Oprócz tych funkcji ta wersja programu NuGet zawiera inne poprawki błędów.</span><span class="sxs-lookup"><span data-stu-id="4bb93-117">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="4bb93-118">Znaleziono 16 całkowita problemy rozwiązane w wersji.</span><span class="sxs-lookup"><span data-stu-id="4bb93-118">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="4bb93-119">Pełną listę prac elementów usunięto w wersji NuGet 2.8.1, sprawdź widok [NuGet Tracker problem w tej wersji](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="4bb93-119">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="4bb93-120">Reshipping z programem Visual Studio "14" CTP</span><span class="sxs-lookup"><span data-stu-id="4bb93-120">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="4bb93-121">W wersji CTP programu Visual Studio "14" wydanej w dniu 2014 3 czerwca NuGet 2.8.1 jest dostarczany w polu.</span><span class="sxs-lookup"><span data-stu-id="4bb93-121">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="4bb93-122">Funkcje, obsługuje on pozostają w par z innych 2.8.1 VSIXes, takich jak dla programu Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="4bb93-122">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
