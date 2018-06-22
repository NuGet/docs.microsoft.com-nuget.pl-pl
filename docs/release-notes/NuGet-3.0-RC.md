---
title: Informacje o wersji RC NuGet 3.0
description: Informacje o wersji programu NuGet 3.0 RC tym znanych problemów, poprawki, dodatkowe funkcje i dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 28ac49d9e9071d16d20b24808abb0acaab214ffd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819601"
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="587d2-103">Informacje o wersji RC NuGet 3.0</span><span class="sxs-lookup"><span data-stu-id="587d2-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="587d2-104">[Informacje o wersji Beta NuGet 3.0](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 informacje o wersji](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="587d2-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="587d2-105">Począwszy od wersji programu Visual Studio 2015 RC z NuGet 3.0 RC został wydany 29 kwietnia 2015 r.</span><span class="sxs-lookup"><span data-stu-id="587d2-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="587d2-106">Ta wersja zawiera szereg ważnych poprawek, wydajności i aktualizacji do obsługi nowej struktury.</span><span class="sxs-lookup"><span data-stu-id="587d2-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="587d2-107">Jest on dostępny tylko dla programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="587d2-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="587d2-108">Kontynuacja fokus na wydajność</span><span class="sxs-lookup"><span data-stu-id="587d2-108">Continued Focus on Performance</span></span>

<span data-ttu-id="587d2-109">Stabilność i wydajność kwerend NuGet nadal będą dostępne na temat dynamicznej.</span><span class="sxs-lookup"><span data-stu-id="587d2-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="587d2-110">W tej wersji należy zacząć wyświetlić operacje bardzo szybkiego wyszukiwania w NuGet interfejsu użytkownika i witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="587d2-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="587d2-111">Firma Microsoft jest monitorowanie usługi i sposobie korzystania z usługi tak, aby móc dalej dostosować te operacje.</span><span class="sxs-lookup"><span data-stu-id="587d2-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="587d2-112">Istotne problemy rozwiązane</span><span class="sxs-lookup"><span data-stu-id="587d2-112">Significant Issues Resolved</span></span>

<span data-ttu-id="587d2-113">Aby ustabilizowania klientów NuGet, możemy rozpoznać wiele problemów w ramach tej wersji.</span><span class="sxs-lookup"><span data-stu-id="587d2-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="587d2-114">Poniżej przedstawiono tylko krótki listę niektórych ważniejsze rozwiązaniu problemów:</span><span class="sxs-lookup"><span data-stu-id="587d2-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="587d2-115">W ramach zmiany nazwy K framework dla platformy ASP.NET 5, monikerów framework zostały zaktualizowane do obsługi środowiska dnx i dnxcore [łącza](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="587d2-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="587d2-116">Dodane w dokumentacji pomocy z łącza w interfejsie użytkownika programu Visual Studio [łącza](https://github.com/NuGet/Home/issues/232)</span><span class="sxs-lookup"><span data-stu-id="587d2-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="587d2-117">Lepszą obsługę złożonych odwołań w `.nuspec` z odwołaniami rozdzielana przecinkami framework [łącza](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="587d2-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="587d2-118">Stałe obsługę japońskiego kultur [łącza](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="587d2-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="587d2-119">Zaktualizowanego klienta umożliwiają projektów ASP.NET 5 nowe punkty końcowe v3 [łącza](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="587d2-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="587d2-120">Zaktualizowano w celu lepszej obsługi pakietów folder z kontrolą źródła [łącza](https://github.com/NuGet/Home/issues/56)</span><span class="sxs-lookup"><span data-stu-id="587d2-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="587d2-121">Stałe obsługi pakietów satelity [łącza](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="587d2-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="587d2-122">Poprawiona obsługa plików zawartości określonej struktury [łącza](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="587d2-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="587d2-123">Naprawy głównej obecności GitHub</span><span class="sxs-lookup"><span data-stu-id="587d2-123">GitHub presence overhaul</span></span>

<span data-ttu-id="587d2-124">Wprowadziliśmy pewne zmiany do naszej [źródła repozytoria kodu w witrynie GitHub](http://github.com/nuget/home).</span><span class="sxs-lookup"><span data-stu-id="587d2-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="587d2-125">Jeśli masz problemy z klienta NuGet programu Visual Studio, poleceń programu Powershell lub wiersza polecenia pliku wykonywalnego możesz zalogować tych problemów i monitorować ich postęp na naszych [listę problemów repozytorium GitHub głównej](http://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="587d2-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="587d2-126">Śledzimy problemy z galerii w naszym [repozytorium GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="587d2-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="587d2-127">Wkrótce</span><span class="sxs-lookup"><span data-stu-id="587d2-127">Stay Tuned</span></span>

<span data-ttu-id="587d2-128">Można śledzić na [naszym blogu](http://blog.nuget.org) więcej i powiadomień dla NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="587d2-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>