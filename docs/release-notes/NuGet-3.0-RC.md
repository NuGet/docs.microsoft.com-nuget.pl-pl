---
title: Informacje o wersji narzędzia NuGet 3,0 RC
description: Informacje o wersji programu NuGet 3,0 RC, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 19bc51a278425295811db253ca3f4ba4366ccf49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776573"
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="7175b-103">Informacje o wersji narzędzia NuGet 3,0 RC</span><span class="sxs-lookup"><span data-stu-id="7175b-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="7175b-104">Informacje o wersji programu [NuGet 3,0 beta](../release-notes/nuget-3.0-beta.md)  |  [Informacje o wersji narzędzia NuGet 3,0 RC2](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="7175b-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="7175b-105">Pakiet NuGet 3,0 RC został zwolniony 29 kwietnia 2015 z wersją Visual Studio 2015 RC.</span><span class="sxs-lookup"><span data-stu-id="7175b-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="7175b-106">W tej wersji wprowadzono wiele ważnych poprawek usterek, ulepszeń wydajności i aktualizacji w celu obsługi nowych platform.</span><span class="sxs-lookup"><span data-stu-id="7175b-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="7175b-107">Jest on dostępny tylko dla programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="7175b-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="7175b-108">Dalsze koncentracje na wydajności</span><span class="sxs-lookup"><span data-stu-id="7175b-108">Continued Focus on Performance</span></span>

<span data-ttu-id="7175b-109">Stabilność i wydajność zapytań NuGet nadal jest aktywnym tematem, na którym koncentrujemy się.</span><span class="sxs-lookup"><span data-stu-id="7175b-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="7175b-110">W tej wersji należy zacząć wyświetlać bardzo szybkie operacje wyszukiwania w interfejsie użytkownika i witrynie programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="7175b-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="7175b-111">Monitorujemy usługę i używamy usługi, aby można było dalej dostroić te operacje.</span><span class="sxs-lookup"><span data-stu-id="7175b-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="7175b-112">Znaczne problemy rozwiązane</span><span class="sxs-lookup"><span data-stu-id="7175b-112">Significant Issues Resolved</span></span>

<span data-ttu-id="7175b-113">Aby zapewnić stabilizację klientów programu NuGet, firma Microsoft rozwiązała wiele problemów w ramach tej wersji.</span><span class="sxs-lookup"><span data-stu-id="7175b-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="7175b-114">Poniżej przedstawiono krótką listę niektórych ważniejszych problemów, które zostały rozwiązane:</span><span class="sxs-lookup"><span data-stu-id="7175b-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="7175b-115">W ramach zmiany nazwy platformy K dla ASP.NET 5, monikery struktury zostały zaktualizowane w celu obsługi [linku](https://github.com/NuGet/Home/issues/215) środowiska DNX i dnxcore</span><span class="sxs-lookup"><span data-stu-id="7175b-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="7175b-116">Dodano dokumentację pomocy z linków w [linku](https://github.com/NuGet/Home/issues/232) interfejsu użytkownika programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7175b-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="7175b-117">Ulepszona obsługa złożonych odwołań w `.nuspec` połączeniu z odwołaniami do struktury rozdzielonych przecinkami [](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="7175b-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="7175b-118">Stała obsługa [łącza](https://github.com/NuGet/Home/issues/253) dla kultur japońskich</span><span class="sxs-lookup"><span data-stu-id="7175b-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="7175b-119">Zaktualizowano klienta, aby zezwolić na używanie przez ASP.NET 5 projektów [nowych punktów](https://github.com/NuGet/Home/issues/219) końcowych v3</span><span class="sxs-lookup"><span data-stu-id="7175b-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="7175b-120">Zaktualizowano w celu lepszego obsługi folderu pakietów z [linkiem](https://github.com/NuGet/Home/issues/56) kontroli źródła</span><span class="sxs-lookup"><span data-stu-id="7175b-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="7175b-121">Stałe wsparcie dla [linku](https://github.com/NuGet/Home/issues/17) pakietów satelitarnych</span><span class="sxs-lookup"><span data-stu-id="7175b-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="7175b-122">Poprawiono obsługę [linku](https://github.com/NuGet/Home/issues/18) do plików zawartości specyficznej dla platformy</span><span class="sxs-lookup"><span data-stu-id="7175b-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="7175b-123">Remonty obecności usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="7175b-123">GitHub presence overhaul</span></span>

<span data-ttu-id="7175b-124">Wprowadziliśmy pewne zmiany w [repozytoriach kodu źródłowego w serwisie GitHub](http://github.com/nuget/home).</span><span class="sxs-lookup"><span data-stu-id="7175b-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="7175b-125">Jeśli masz problemy z klientem programu Visual Studio NuGet, poleceniami programu PowerShell lub wykonywalnym wierszem polecenia, można rejestrować te problemy i monitorować ich postęp na naszej [liście problemów z repozytorium głównym usługi GitHub](http://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="7175b-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="7175b-126">Śledzimy problemy z galerią w naszym [repozytorium GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="7175b-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="7175b-127">Bądź na bieżąco</span><span class="sxs-lookup"><span data-stu-id="7175b-127">Stay Tuned</span></span>

<span data-ttu-id="7175b-128">Obserwuj [nasz blog](http://blog.nuget.org) , aby uzyskać więcej informacji na temat postępu i anonsów dla programu NuGet 3,0!</span><span class="sxs-lookup"><span data-stu-id="7175b-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>