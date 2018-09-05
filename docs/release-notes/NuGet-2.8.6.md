---
title: Informacje o wersji NuGet 2.8.6
description: Informacje o wersji programu NuGet 2.8.6 tym — znane problemy, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d57c658999ed3c79b962de84fd973276833ef3fd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546494"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="323c5-103">Informacje o wersji NuGet 2.8.6</span><span class="sxs-lookup"><span data-stu-id="323c5-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="323c5-104">[Informacje o wersji NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [informacjach o wersji NuGet 2.8.7](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="323c5-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="323c5-105">NuGet 2.8.6 został wydany 20 lipca 2015 roku jako aktualizację pomocniczą do naszych 2.8.5 VSIX z niektórymi docelowe poprawek i udoskonaleń do obsługi pakietów, które mogą być dostarczane z obsługą model programowania platformy uniwersalnej systemu Windows do systemu Windows 10.</span><span class="sxs-lookup"><span data-stu-id="323c5-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="323c5-106">Ta wersja rozszerzenia Menedżera pakietów NuGet zapewniają obsługę programu Visual Studio 2013 tylko.</span><span class="sxs-lookup"><span data-stu-id="323c5-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="323c5-107">W tej wersji okno Menedżera pakietów NuGet nie dodano dla pomocy technicznej:</span><span class="sxs-lookup"><span data-stu-id="323c5-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="323c5-108">Wprowadzono UAP krótką nazwę platformy docelowej do obsługi systemu Windows 10 dla deweloperów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="323c5-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="323c5-109">Punkty końcowe programu NuGet protocol w wersji 3</span><span class="sxs-lookup"><span data-stu-id="323c5-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="323c5-110">Obsługa [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) właściwość protocolVersion atrybutu w źródłach repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="323c5-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="323c5-111">Wartość domyślna to "2"</span><span class="sxs-lookup"><span data-stu-id="323c5-111">Default value is "2"</span></span>
* <span data-ttu-id="323c5-112">Nastąpi powrót do repozytorium zdalnego, jeśli wersja wymagany pakiet nie jest dostępna w lokalnej pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="323c5-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>