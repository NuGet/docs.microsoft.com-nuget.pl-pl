---
title: Informacje o wersji pakietu NuGet 3.2.1
description: Informacje o wersji programu NuGet 3.2.1, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cbbef3517122ceda91cb4b4463fe8be43d204db4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776522"
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="90c1b-103">Informacje o wersji pakietu NuGet 3.2.1</span><span class="sxs-lookup"><span data-stu-id="90c1b-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="90c1b-104">Informacje o wersji narzędzia [NuGet 3,2](../release-notes/nuget-3.2.md)  |  [Informacje o wersji narzędzia NuGet 3,3](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="90c1b-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="90c1b-105">Program NuGet 3.2.1 dla wiersza polecenia został zwolniony 12 października 2015 z kilkuą optymalizacji i poprawek dla wersji 3,2 i jest dostępny z [dist.NuGet.org](http://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="90c1b-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="90c1b-106">Ulepszenia</span><span class="sxs-lookup"><span data-stu-id="90c1b-106">Improvements</span></span>

* <span data-ttu-id="90c1b-107">Pakiet NuGet używa teraz pliku konfiguracji z oryginalną wielkością liter `NuGet.Config` .</span><span class="sxs-lookup"><span data-stu-id="90c1b-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="90c1b-108">Jest to ważne w przypadku systemów operacyjnych z uwzględnieniem wielkości liter [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="90c1b-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="90c1b-109">Przywracanie NuGet zignoruje teraz środowiska DNX projekty ( `*.xproj` ), które powinny być przetwarzane przy użyciu `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="90c1b-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="90c1b-110">Zoptymalizowane wykorzystanie sieci podczas pracy z `index.json` danymi rejestracji pakietu i ich pakietów [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="90c1b-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="90c1b-111">Ulepszona obsługa pobierania zasobów jest bardziej niezawodna w przypadku usług w wersji 2 [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="90c1b-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="90c1b-112">Poprawki</span><span class="sxs-lookup"><span data-stu-id="90c1b-112">Fixes</span></span>

* <span data-ttu-id="90c1b-113">Aktualizacja NuGet prawidłowo aktualizuje `.csproj` / `.vcxproj` odwołania [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="90c1b-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="90c1b-114">Teraz uniemożliwiamy utworzenie lokalnego folderu. NuGet, gdy nie można zlokalizować SpecialFolders. UserProfile [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="90c1b-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="90c1b-115">Ulepszona obsługa pakietów w lokalnej pamięci podręcznej, które są uszkodzone podczas pobierania [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="90c1b-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="90c1b-116">Pełna lista problemów rozwiązanych w przypadku rozszerzenia wiersza polecenia i programu Visual Studio znajduje się w obszarze [kontrolnym](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed) NuGet GitHub 3.2.1</span><span class="sxs-lookup"><span data-stu-id="90c1b-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="90c1b-117">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="90c1b-117">Known Issues</span></span>

<span data-ttu-id="90c1b-118">Będziemy nadal śledzić problemy na naszej liście problemów usługi GitHub, którą można znaleźć w witrynie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="90c1b-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>