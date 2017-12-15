---
title: Informacje o wersji NuGet 3.4.2 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: b514da09-da1f-416b-9bfc-692f08fb6957
description: "Informacje o wersji programu NuGet 3.4.2 tym — znane problemy, poprawki, dodatkowe funkcje i dcr."
keywords: NuGet 3.4.2 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6761c59b6dc85b9a8503041928c2707549006d9c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="a2502-104">Informacje o wersji NuGet 3.4.2</span><span class="sxs-lookup"><span data-stu-id="a2502-104">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="a2502-105">[Informacje o wersji NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 informacje o wersji](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="a2502-105">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="a2502-106">NuGet 3.4.2 został wydany 8 kwietnia 2016, aby rozwiązać pewne problemy, które zostały zidentyfikowane w wersji 3.4 i 3.4.1 wersji.</span><span class="sxs-lookup"><span data-stu-id="a2502-106">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="a2502-107">RC nuget.exe 3.4.2 jest teraz dostępna</span><span class="sxs-lookup"><span data-stu-id="a2502-107">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="a2502-108">Można pobrać wersji release candidate nuget.exe 3.4.2 [tutaj](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="a2502-108">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="a2502-109">Aktualizacje i usprawnienia</span><span class="sxs-lookup"><span data-stu-id="a2502-109">Updates and Improvements</span></span>

* <span data-ttu-id="a2502-110">Firma Microsoft ma znaczne zwiększenie wydajności aktualizacji w konkretnych sytuacji, gdy aktualizacje dla pakietów wykresami zależności bezpośrednich przez bardzo długi czas i zawiesił Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a2502-110">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="a2502-111">Przywracanie nuget bez ruch sieciowy jest 2,5 x – 3 x szybsze w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a2502-111">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="a2502-112">Oprócz tej zmiany został rozwiązany problem gdzie możemy zostały naciśnięcie sieci dwa razy, gdy liczba pobierania aktualizacji w Interfejsie użytkownika programu VS.</span><span class="sxs-lookup"><span data-stu-id="a2502-112">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="a2502-113">To jest częściowo odpowiedzialny za niektórzy klienci problemów limitu czasu w wersji 3.4/3.4.1.</span><span class="sxs-lookup"><span data-stu-id="a2502-113">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="a2502-114">Dodano obsługę ustawienie no_proxy</span><span class="sxs-lookup"><span data-stu-id="a2502-114">Added support for no_proxy setting</span></span>

##<a name="fixes"></a><span data-ttu-id="a2502-115">Poprawki</span><span class="sxs-lookup"><span data-stu-id="a2502-115">Fixes</span></span>

* <span data-ttu-id="a2502-116">Rozwiązano problem, na którym nuget.org źródła brakowało w ustawieniach NuGet lub konfiguracji po zaktualizowaniu do 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="a2502-116">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="a2502-117">Rozwiązano problem, w którym zmiany wielkości liter FindPackagesById w 3.4.1 dzieli Artifactory.</span><span class="sxs-lookup"><span data-stu-id="a2502-117">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="a2502-118">Rozwiązany problem z FIPS powodujący błędy z Przywracanie NuGet z nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="a2502-118">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="a2502-119">Stała awarii podczas przeglądania źródła z ikoną nieprawidłowy adres URL.</span><span class="sxs-lookup"><span data-stu-id="a2502-119">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="a2502-120">Rozwiązane problemy z scalania wersji i pozycje "Wszystkie źródła".</span><span class="sxs-lookup"><span data-stu-id="a2502-120">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="a2502-121">Znane problemy w 3.4.2 wiersza polecenia systemu Windows x86 (RC)</span><span class="sxs-lookup"><span data-stu-id="a2502-121">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="a2502-122">Wczesne następnym tygodniu przed możemy trafień RTM będzie rozwiązać te problemy.</span><span class="sxs-lookup"><span data-stu-id="a2502-122">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="a2502-123">Uruchomione Przywracanie nuget dla rozwiązania zakończy się niepowodzeniem, jeśli plik rozwiązania znajduje się w hierarchii folderów niższe niż pliki projektu.</span><span class="sxs-lookup"><span data-stu-id="a2502-123">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="a2502-124">Polecenia usuwania nuget na pakiet za pomocą kanału informacyjnego V2 zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="a2502-124">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="a2502-125">Zamiast tego użyj V3 źródła danych.</span><span class="sxs-lookup"><span data-stu-id="a2502-125">Use V3 feed instead.</span></span>


<span data-ttu-id="a2502-126">Aby uzyskać pełną listę poprawek i ulepszenia w tej wersji, zapoznaj się z listy problemów dotyczących [tutaj](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="a2502-126">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>