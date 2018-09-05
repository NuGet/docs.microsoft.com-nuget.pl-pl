---
title: Informacje o wersji NuGet 3.2.1
description: Informacje o wersji programu NuGet 3.2.1 tym — znane problemy, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5ddbb8aa52ef85c823404364a3aca79fd16f3b1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548193"
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="4c4d5-103">Informacje o wersji NuGet 3.2.1</span><span class="sxs-lookup"><span data-stu-id="4c4d5-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="4c4d5-104">[Informacje o wersji NuGet 3.2](../release-notes/nuget-3.2.md) | [informacjach o wersji NuGet 3.3](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="4c4d5-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="4c4d5-105">Rozwiązanie NuGet 3.2.1 dla wiersza polecenia został wydany 12 października 2015 za pomocą kliku optymalizacji i poprawek w wersji 3.2 i jest dostępny w [dist.nuget.org](http://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="4c4d5-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="4c4d5-106">Ulepszenia</span><span class="sxs-lookup"><span data-stu-id="4c4d5-106">Improvements</span></span>

* <span data-ttu-id="4c4d5-107">NuGet teraz używa pliku konfiguracji z oryginalnego wielkość liter w wyrazie `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="4c4d5-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="4c4d5-108">Jest to ważne w systemach operacyjnych z uwzględnieniem wielkości liter [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="4c4d5-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="4c4d5-109">Przywracanie pakietów NuGet teraz będzie ignorować projektami środowiska dnx (`*.xproj`) powinny zostać przetworzone za pomocą `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="4c4d5-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="4c4d5-110">Zoptymalizowane pod kątem wykorzystania sieci, podczas pracy z `index.json` i utworzyć pakiet danych rejestracyjnych [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="4c4d5-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="4c4d5-111">Pobieranie zasobów ulepszone obsługi się bardziej niezawodne usługi w wersji 2 [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="4c4d5-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="4c4d5-112">Poprawki</span><span class="sxs-lookup"><span data-stu-id="4c4d5-112">Fixes</span></span>

* <span data-ttu-id="4c4d5-113">Aktualizacja NuGet poprawnie aktualizacji `.csproj` / `.vcxproj` odwołania [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="4c4d5-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="4c4d5-114">Teraz uniemożliwia folderem lokalnym .nuget tworzone podczas SpecialFolders.UserProfile nie można odnaleźć [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="4c4d5-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="4c4d5-115">Ulepszona obsługa pakietów w lokalnej pamięci podręcznej, które są uszkodzone podczas pobierania [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="4c4d5-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="4c4d5-116">Pełną listę problemów rozwiązanych dla rozszerzenia programu wiersza polecenia i programu Visual Studio można znaleźć w witrynie NuGet GitHub [3.2.1 punkt kontrolny](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="4c4d5-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="4c4d5-117">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="4c4d5-117">Known Issues</span></span>

<span data-ttu-id="4c4d5-118">W dalszym ciągu śledzenia problemów na naszej liście problemów GitHub, który znajduje się w temacie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="4c4d5-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>