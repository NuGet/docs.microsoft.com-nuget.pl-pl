---
title: Informacje o wersji NuGet 3.4.2
description: Informacje o wersji programu NuGet 3.4.2 tym — znane problemy, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4c8aa75df822ca5b2f1c4bd274272218f16ad917
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549154"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="ded05-103">Informacje o wersji NuGet 3.4.2</span><span class="sxs-lookup"><span data-stu-id="ded05-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="ded05-104">[Informacje o wersji NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [informacjach o wersji NuGet 3.4.3](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="ded05-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="ded05-105">NuGet 3.4.2 została wydana 8 kwietnia 2016, aby rozwiązać wiele problemów, które zostały zidentyfikowane w 3.4 i 3.4.1 wydania.</span><span class="sxs-lookup"><span data-stu-id="ded05-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="ded05-106">nuget.exe 3.4.2 RC jest teraz dostępna</span><span class="sxs-lookup"><span data-stu-id="ded05-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="ded05-107">Możesz pobrać wersję Release candidate programu nuget.exe 3.4.2 [tutaj](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="ded05-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="ded05-108">Aktualizacje i ulepszenia</span><span class="sxs-lookup"><span data-stu-id="ded05-108">Updates and Improvements</span></span>

* <span data-ttu-id="ded05-109">Znacznie ulepszyliśmy wydajności aktualizacji konkretnego scenariusza, w którym aktualizacje w pakietach za pomocą wykresów zależności głębokiego bardzo dużo czasu i nieuruchamianie programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ded05-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="ded05-110">Przywracanie pakietów nuget bez ruch sieciowy jest 2,5 x — 3 x szybciej w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ded05-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="ded05-111">Poza tą zmianą usunęliśmy problem gdzie możemy zostały osiągnięcia sieci dwa razy, gdy jest to pobieranie aktualizacji licznik w Interfejsie użytkownika programu VS.</span><span class="sxs-lookup"><span data-stu-id="ded05-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="ded05-112">Taka konfiguracja była częściowo odpowiada dla niektórych klientów problemy dotyczące limitu czasu w 3.4/3.4.1.</span><span class="sxs-lookup"><span data-stu-id="ded05-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="ded05-113">Dodano obsługę ustawienia no_proxy</span><span class="sxs-lookup"><span data-stu-id="ded05-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="ded05-114">Poprawki</span><span class="sxs-lookup"><span data-stu-id="ded05-114">Fixes</span></span>

* <span data-ttu-id="ded05-115">Rozwiązano problem, w którym źródło nuget.org brakowało w NuGet ustawienia lub konfiguracji po aktualizacji do 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="ded05-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="ded05-116">Rozwiązano problem, w którym zmiany wielkości liter do FindPackagesById 3.4.1 przerywa Artifactory.</span><span class="sxs-lookup"><span data-stu-id="ded05-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="ded05-117">Rozwiązany problem z trybem FIPS powodującą błędy dzięki funkcji przywracania NuGet za pomocą nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="ded05-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="ded05-118">Naprawiono awarię podczas przeglądania źródła za pomocą adresu URL nieprawidłowa ikona.</span><span class="sxs-lookup"><span data-stu-id="ded05-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="ded05-119">Rozwiązane problemy ze scalaniem wersje i wpisy z "Wszystkie źródła".</span><span class="sxs-lookup"><span data-stu-id="ded05-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="ded05-120">Znane problemy w 3.4.2 Windows x86 wiersza polecenia (RC)</span><span class="sxs-lookup"><span data-stu-id="ded05-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="ded05-121">Te problemy zostaną naprawione wczesne Następny tydzień przed osiągnęliśmy RTM.</span><span class="sxs-lookup"><span data-stu-id="ded05-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="ded05-122">Uruchomione Przywracanie nuget dla rozwiązania zakończy się niepowodzeniem, jeśli plik rozwiązania jest umieszczany w hierarchię folderów niższe niż pliki projektu.</span><span class="sxs-lookup"><span data-stu-id="ded05-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="ded05-123">Uruchomienie polecenia delete nuget na pakiet przy użyciu źródła danych w wersji 2 nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="ded05-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="ded05-124">Zamiast tego użyj wersji 3 źródła danych.</span><span class="sxs-lookup"><span data-stu-id="ded05-124">Use V3 feed instead.</span></span>


<span data-ttu-id="ded05-125">Aby uzyskać pełną listę poprawek i udoskonaleń w tej wersji, zapoznaj się z listy problemów dotyczących [tutaj](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="ded05-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>