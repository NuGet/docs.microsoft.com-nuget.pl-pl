---
title: Informacje o wersji NuGet 3.4.2
description: Informacje o wersji programu NuGet 3.4.2 tym — znane problemy, poprawki, dodatkowe funkcje i dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 88d29a84e280433663ab6c1c04ae16e1329420f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819669"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="60072-103">Informacje o wersji NuGet 3.4.2</span><span class="sxs-lookup"><span data-stu-id="60072-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="60072-104">[Informacje o wersji NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 informacje o wersji](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="60072-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="60072-105">NuGet 3.4.2 został wydany 8 kwietnia 2016, aby rozwiązać pewne problemy, które zostały zidentyfikowane w wersji 3.4 i 3.4.1 wersji.</span><span class="sxs-lookup"><span data-stu-id="60072-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="60072-106">RC nuget.exe 3.4.2 jest teraz dostępna</span><span class="sxs-lookup"><span data-stu-id="60072-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="60072-107">Można pobrać wersji release candidate nuget.exe 3.4.2 [tutaj](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="60072-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="60072-108">Aktualizacje i usprawnienia</span><span class="sxs-lookup"><span data-stu-id="60072-108">Updates and Improvements</span></span>

* <span data-ttu-id="60072-109">Firma Microsoft ma znaczne zwiększenie wydajności aktualizacji w konkretnych sytuacji, gdy aktualizacje dla pakietów wykresami zależności bezpośrednich przez bardzo długi czas i zawiesił Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="60072-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="60072-110">Przywracanie nuget bez ruch sieciowy jest 2,5 x – 3 x szybsze w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="60072-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="60072-111">Oprócz tej zmiany został rozwiązany problem gdzie możemy zostały naciśnięcie sieci dwa razy, gdy liczba pobierania aktualizacji w Interfejsie użytkownika programu VS.</span><span class="sxs-lookup"><span data-stu-id="60072-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="60072-112">To jest częściowo odpowiedzialny za niektórzy klienci problemów limitu czasu w wersji 3.4/3.4.1.</span><span class="sxs-lookup"><span data-stu-id="60072-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="60072-113">Dodano obsługę ustawienie no_proxy</span><span class="sxs-lookup"><span data-stu-id="60072-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="60072-114">Poprawki</span><span class="sxs-lookup"><span data-stu-id="60072-114">Fixes</span></span>

* <span data-ttu-id="60072-115">Rozwiązano problem, na którym nuget.org źródła brakowało w ustawieniach NuGet lub konfiguracji po zaktualizowaniu do 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="60072-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="60072-116">Rozwiązano problem, w którym zmiany wielkości liter FindPackagesById w 3.4.1 dzieli Artifactory.</span><span class="sxs-lookup"><span data-stu-id="60072-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="60072-117">Rozwiązany problem z FIPS powodujący błędy z Przywracanie NuGet z nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="60072-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="60072-118">Stała awarii podczas przeglądania źródła z ikoną nieprawidłowy adres URL.</span><span class="sxs-lookup"><span data-stu-id="60072-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="60072-119">Rozwiązane problemy z scalania wersji i pozycje "Wszystkie źródła".</span><span class="sxs-lookup"><span data-stu-id="60072-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="60072-120">Znane problemy w 3.4.2 wiersza polecenia systemu Windows x86 (RC)</span><span class="sxs-lookup"><span data-stu-id="60072-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="60072-121">Wczesne następnym tygodniu przed możemy trafień RTM będzie rozwiązać te problemy.</span><span class="sxs-lookup"><span data-stu-id="60072-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="60072-122">Uruchomione Przywracanie nuget dla rozwiązania zakończy się niepowodzeniem, jeśli plik rozwiązania znajduje się w hierarchii folderów niższe niż pliki projektu.</span><span class="sxs-lookup"><span data-stu-id="60072-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="60072-123">Polecenia usuwania nuget na pakiet za pomocą kanału informacyjnego V2 zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="60072-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="60072-124">Zamiast tego użyj V3 źródła danych.</span><span class="sxs-lookup"><span data-stu-id="60072-124">Use V3 feed instead.</span></span>


<span data-ttu-id="60072-125">Aby uzyskać pełną listę poprawek i ulepszenia w tej wersji, zapoznaj się z listy problemów dotyczących [tutaj](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="60072-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>