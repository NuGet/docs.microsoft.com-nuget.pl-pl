---
title: Informacje o wersji narzędzia NuGet 3.4.2
description: Informacje o wersji programu NuGet 3.4.2, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6e6aa174582d059faa5bef9469cd83b19da51cf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780258"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="7e86f-103">Informacje o wersji narzędzia NuGet 3.4.2</span><span class="sxs-lookup"><span data-stu-id="7e86f-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="7e86f-104">Informacje o wersji pakietu [NuGet](../release-notes/nuget-3.4.1.md)  |  [Informacje o wersji narzędzia NuGet 3.4.3](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="7e86f-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="7e86f-105">Program NuGet 3.4.2 został zwolniony 8 kwietnia 2016, aby rozwiązać kilka problemów, które zostały zidentyfikowane w wersji 3,4 i.</span><span class="sxs-lookup"><span data-stu-id="7e86f-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="7e86f-106">nuget.exe 3.4.2 RC jest teraz dostępny</span><span class="sxs-lookup"><span data-stu-id="7e86f-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="7e86f-107">W [tym miejscu](https://dist.nuget.org/index.html)możesz pobrać wersję release candidate nuget.exe 3.4.2.</span><span class="sxs-lookup"><span data-stu-id="7e86f-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="7e86f-108">Aktualizacje i ulepszenia</span><span class="sxs-lookup"><span data-stu-id="7e86f-108">Updates and Improvements</span></span>

* <span data-ttu-id="7e86f-109">Znacznie Ulepszono wydajność aktualizacji w konkretnym scenariuszu, w przypadku których aktualizacje na pakietach ze szczegółowymi wykresami zależności zajęły dużo czasu i zawiesiły program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7e86f-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="7e86f-110">Przywracanie NuGet bez ruchu sieciowego to 2,5 x – trzykrotnie w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7e86f-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="7e86f-111">Oprócz tej zmiany Rozwiązano problem polegający na tym, że po pobraniu liczby aktualizacji w interfejsie użytkownika programu VS nastąpiło dwukrotne naciśnięcie sieci.</span><span class="sxs-lookup"><span data-stu-id="7e86f-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="7e86f-112">Było to częściowo odpowiedzialne za niektóre problemy z limitem czasu w przypadku klientów w wersji 3.4/Object.</span><span class="sxs-lookup"><span data-stu-id="7e86f-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="7e86f-113">Dodano obsługę ustawienia no_proxy</span><span class="sxs-lookup"><span data-stu-id="7e86f-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="7e86f-114">Poprawki</span><span class="sxs-lookup"><span data-stu-id="7e86f-114">Fixes</span></span>

* <span data-ttu-id="7e86f-115">Rozwiązano problem polegający na tym, że brak źródła nuget.org w ustawieniach lub konfiguracji NuGet po uaktualnieniu do programu.</span><span class="sxs-lookup"><span data-stu-id="7e86f-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="7e86f-116">Rozwiązano problem polegający na tym, że wielkość liter zmieni się na FindPackagesById w Artifactoryach.</span><span class="sxs-lookup"><span data-stu-id="7e86f-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="7e86f-117">Rozwiązano problem związany z standardem FIPS, który spowodował błędy przywracania NuGet z nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="7e86f-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="7e86f-118">Naprawiono awarię podczas przeglądania źródeł z nieprawidłowym adresem URL ikony.</span><span class="sxs-lookup"><span data-stu-id="7e86f-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="7e86f-119">Rozwiązano problemy z scalaniem wersji i wpisów ze wszystkich źródeł.</span><span class="sxs-lookup"><span data-stu-id="7e86f-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="7e86f-120">Znane problemy w programie 3.4.2 Windows x86 — wiersz polecenia (RC)</span><span class="sxs-lookup"><span data-stu-id="7e86f-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="7e86f-121">Te problemy zostaną rozwiązane na wczesny tydzień przed osiągnięciem wersji RTM.</span><span class="sxs-lookup"><span data-stu-id="7e86f-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="7e86f-122">Uruchomienie przywracania NuGet w rozwiązaniu zakończy się niepowodzeniem, jeśli plik rozwiązania zostanie umieszczony w niższej hierarchii folderów niż pliki projektu.</span><span class="sxs-lookup"><span data-stu-id="7e86f-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="7e86f-123">Uruchamianie polecenia usuwania NuGet w pakiecie przy użyciu źródła danych v2 zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="7e86f-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="7e86f-124">Zamiast tego należy użyć kanału informacyjnego v3.</span><span class="sxs-lookup"><span data-stu-id="7e86f-124">Use V3 feed instead.</span></span>


<span data-ttu-id="7e86f-125">Aby zapoznać się z pełną listą poprawek i ulepszeń w tej wersji, zapoznaj się z listą problemów w [tym miejscu](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="7e86f-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>