---
title: Informacje o wersji narzędzia NuGet 2.8.2
description: Informacje o wersji programu NuGet 2.8.2, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780372"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="04fb5-103">Informacje o wersji narzędzia NuGet 2.8.2</span><span class="sxs-lookup"><span data-stu-id="04fb5-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="04fb5-104">Informacje o wersji narzędzia [NuGet 2.8.1](../release-notes/nuget-2.8.1.md)  |  [Informacje o wersji narzędzia NuGet 2.8.3](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="04fb5-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="04fb5-105">Pakiet NuGet 2.8.2 został opublikowany w dniu 22 maja 2014.</span><span class="sxs-lookup"><span data-stu-id="04fb5-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="04fb5-106">W tej wersji uwzględniono tylko zmiany w nuget.exe wierszu polecenia, pakiet NuGet. Server i inne pakiety NuGet.</span><span class="sxs-lookup"><span data-stu-id="04fb5-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="04fb5-107">Wydanie nie zawiera zaktualizowanego rozszerzenia programu Visual Studio lub rozszerzenia WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="04fb5-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="04fb5-108">Ważne aktualizacje</span><span class="sxs-lookup"><span data-stu-id="04fb5-108">Notable Updates</span></span>

<span data-ttu-id="04fb5-109">Najbardziej ważne aktualizacje zostały nuget.exe w wierszu polecenia i pakiecie NuGet. Server (dla własnych źródeł NuGet).</span><span class="sxs-lookup"><span data-stu-id="04fb5-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="04fb5-110">Ważne poprawki nuget.exe błędów</span><span class="sxs-lookup"><span data-stu-id="04fb5-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="04fb5-111">nuget.exe wypychanie nie powiedzie się i kontynuuje ponawianie próby</span><span class="sxs-lookup"><span data-stu-id="04fb5-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="04fb5-112">nuget.exe push nie wysyła prawidłowo poświadczeń uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="04fb5-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="04fb5-113"> Wypychanienuget.exe nie będzie podążać za przekierowaniem tymczasowym</span><span class="sxs-lookup"><span data-stu-id="04fb5-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="04fb5-114">Ważna Poprawka błędu NuGet. serwer</span><span class="sxs-lookup"><span data-stu-id="04fb5-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="04fb5-115">Niepoprawna wartość IsAbsoluteLatestVersion zwrócona przez NuGet. serwer</span><span class="sxs-lookup"><span data-stu-id="04fb5-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="04fb5-116">Zaktualizowano pakiety</span><span class="sxs-lookup"><span data-stu-id="04fb5-116">Packages Updated</span></span>

<span data-ttu-id="04fb5-117">nuget.exe wiersza polecenia i NuGet. poprawki serwera są dostarczane jako aktualizacje pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="04fb5-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="04fb5-118">Dodano również inne pakiety z 2.8.2.</span><span class="sxs-lookup"><span data-stu-id="04fb5-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="04fb5-119">Oto lista zaktualizowanych pakietów:</span><span class="sxs-lookup"><span data-stu-id="04fb5-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="04fb5-120">NuGet. Core</span><span class="sxs-lookup"><span data-stu-id="04fb5-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="04fb5-121">NuGet. CommandLine</span><span class="sxs-lookup"><span data-stu-id="04fb5-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="04fb5-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="04fb5-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="04fb5-123">NuGet. Build</span><span class="sxs-lookup"><span data-stu-id="04fb5-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="04fb5-124">[NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (pakiet, a nie rozszerzenie)</span><span class="sxs-lookup"><span data-stu-id="04fb5-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="04fb5-125">Wszystkie zmiany</span><span class="sxs-lookup"><span data-stu-id="04fb5-125">All Changes</span></span>
<span data-ttu-id="04fb5-126">Wystąpiły 10 problemów rozwiązanych w wydaniu.</span><span class="sxs-lookup"><span data-stu-id="04fb5-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="04fb5-127">Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 2.8.2, zobacz [Śledzenie problemów NuGet dla tej wersji](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="04fb5-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
