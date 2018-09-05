---
title: Informacje o wersji programu NuGet 3.0 RC
description: Informacje o wersji programu NuGet 3.0 RC obejmuje znane problemy, poprawki błędów, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0575cb1598f259a1cf1597f67123b644d67c31b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551722"
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="61bc1-103">Informacje o wersji programu NuGet 3.0 RC</span><span class="sxs-lookup"><span data-stu-id="61bc1-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="61bc1-104">[Informacje o wersji programu NuGet 3.0 Beta](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 — informacje o wersji](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="61bc1-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="61bc1-105">NuGet 3.0 RC został wydany 29 kwietnia 2015 w wersji Visual Studio 2015 RC.</span><span class="sxs-lookup"><span data-stu-id="61bc1-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="61bc1-106">Ta wersja ma wiele ważnych poprawek błędów, ulepszeń wydajności i aktualizacji do obsługi nowych platform.</span><span class="sxs-lookup"><span data-stu-id="61bc1-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="61bc1-107">Jest on dostępny tylko dla programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="61bc1-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="61bc1-108">Ciągłe dążenie do wydajności</span><span class="sxs-lookup"><span data-stu-id="61bc1-108">Continued Focus on Performance</span></span>

<span data-ttu-id="61bc1-109">Stabilności i wydajności kwerend NuGet nadal aktualnie gorący temat wśród, koncentrujemy się na.</span><span class="sxs-lookup"><span data-stu-id="61bc1-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="61bc1-110">W tej wersji należy zacząć wyświetlić operacje bardzo szybkie wyszukiwanie w NuGet interfejsu użytkownika i witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="61bc1-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="61bc1-111">Firma Microsoft monitorowania usługi i sposobie korzystania z usługi tak, aby umożliwić nam dostosować te operacje.</span><span class="sxs-lookup"><span data-stu-id="61bc1-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="61bc1-112">Istotne problemy rozwiązane</span><span class="sxs-lookup"><span data-stu-id="61bc1-112">Significant Issues Resolved</span></span>

<span data-ttu-id="61bc1-113">W celu stabilizacji klientom programu NuGet, rozwiązaliśmy wiele problemów w ramach tej wersji.</span><span class="sxs-lookup"><span data-stu-id="61bc1-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="61bc1-114">Poniżej przedstawiono tylko krótkie listami niektóre najważniejsze zagadnienia, które są rozwiązane:</span><span class="sxs-lookup"><span data-stu-id="61bc1-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="61bc1-115">W ramach zmiany nazwy K framework programu ASP.NET 5, monikerów framework zostały zaktualizowane do obsługi środowiska dnx i dnxcore [łącza](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="61bc1-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="61bc1-116">Dodano dokumentacji pomocy z poziomu linków w interfejsie użytkownika programu Visual Studio [łącza](https://github.com/NuGet/Home/issues/232)</span><span class="sxs-lookup"><span data-stu-id="61bc1-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="61bc1-117">Lepiej obsługi złożonych odwołań w `.nuspec` za pomocą odwołania rozdzielonych przecinkami [łącza](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="61bc1-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="61bc1-118">Naprawiono obsługę japoński kultur [łącza](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="61bc1-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="61bc1-119">Zaktualizowanego klienta, aby umożliwić projektów ASP.NET 5, aby używać nowych v3 punktów końcowych [łącza](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="61bc1-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="61bc1-120">Zaktualizowano w celu lepszego uchwyt folder packages z kontrolą źródła [łącza](https://github.com/NuGet/Home/issues/56)</span><span class="sxs-lookup"><span data-stu-id="61bc1-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="61bc1-121">Naprawiono obsługę satelitarnej pakietów [łącza](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="61bc1-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="61bc1-122">Poprawiona obsługa dla określonej platformy, pliki zawartości [łącza](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="61bc1-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="61bc1-123">Kontrolę obecności usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="61bc1-123">GitHub presence overhaul</span></span>

<span data-ttu-id="61bc1-124">Wprowadziliśmy pewne zmiany do naszych [źródła repozytoriów w serwisie GitHub](http://github.com/nuget/home).</span><span class="sxs-lookup"><span data-stu-id="61bc1-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="61bc1-125">Jeśli masz problemy z klienta programu NuGet w programie Visual Studio, poleceń programu Powershell lub wiersza polecenia pliku wykonywalnego można rejestrować tych problemów i monitorować ich postęp na naszych [listę problemów w repozytorium GitHub głównej](http://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="61bc1-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="61bc1-126">Śledzimy problemy z galerii w naszym [repozytorium GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="61bc1-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="61bc1-127">Obserwuj na bieżąco</span><span class="sxs-lookup"><span data-stu-id="61bc1-127">Stay Tuned</span></span>

<span data-ttu-id="61bc1-128">Można nadzorować [naszym blogu](http://blog.nuget.org) więcej postępu i anonsów dla pakietów NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="61bc1-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>