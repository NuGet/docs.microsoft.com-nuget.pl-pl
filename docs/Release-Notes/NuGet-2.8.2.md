---
title: Informacje o wersji NuGet 2.8.2
description: Informacje o wersji programu NuGet 2.8.2 tym — znane problemy, poprawki, dodatkowe funkcje i dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a004c250d60a4ed1ca8dede1e83b2a68e10299bf
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="1ae6a-103">Informacje o wersji NuGet 2.8.2</span><span class="sxs-lookup"><span data-stu-id="1ae6a-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="1ae6a-104">[Informacje o wersji NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 informacje o wersji](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="1ae6a-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="1ae6a-105">NuGet 2.8.2 wydanej w dniu 22 maja 2014.</span><span class="sxs-lookup"><span data-stu-id="1ae6a-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="1ae6a-106">Ta wersja uwzględnione tylko zmiany nuget.exe wiersza polecenia, pakiet NuGet.Server i inne pakiety NuGet.</span><span class="sxs-lookup"><span data-stu-id="1ae6a-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="1ae6a-107">Wersja nie zawiera zaktualizowane rozszerzenie programu Visual Studio lub rozszerzenia programu WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="1ae6a-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="1ae6a-108">Ważne aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="1ae6a-108">Notable Updates</span></span>

<span data-ttu-id="1ae6a-109">Najbardziej znaczące aktualizacje zostały nuget.exe wiersza polecenia i pakietu NuGet.Server (dla siebie źródeł danych NuGet).</span><span class="sxs-lookup"><span data-stu-id="1ae6a-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="1ae6a-110">Nuget.exe ważne poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="1ae6a-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="1ae6a-111">nuget.exe wypychania nie powiedzie się i przechowuje ponawianie próby</span><span class="sxs-lookup"><span data-stu-id="1ae6a-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="1ae6a-112">nuget.exe wypychania nie wysyła poprawnie poświadczenia uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="1ae6a-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="1ae6a-113">nuget.exe wypychania nie wykonaj Przekierowanie tymczasowe</span><span class="sxs-lookup"><span data-stu-id="1ae6a-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="1ae6a-114">Poprawka błędu NuGet.Server ważne</span><span class="sxs-lookup"><span data-stu-id="1ae6a-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="1ae6a-115">Niewłaściwą wartość zwrócona przez NuGet.Server IsAbsoluteLatestVersion</span><span class="sxs-lookup"><span data-stu-id="1ae6a-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="1ae6a-116">Pakiety aktualizacji</span><span class="sxs-lookup"><span data-stu-id="1ae6a-116">Packages Updated</span></span>

<span data-ttu-id="1ae6a-117">Nuget.exe wiersza polecenia i NuGet.Server poprawki są dostarczane jako aktualizacji pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="1ae6a-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="1ae6a-118">Brak innych pakietów, zaktualizowane 2.8.2 również.</span><span class="sxs-lookup"><span data-stu-id="1ae6a-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="1ae6a-119">Poniżej przedstawiono listę zaktualizowanych pakietów:</span><span class="sxs-lookup"><span data-stu-id="1ae6a-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="1ae6a-120">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="1ae6a-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="1ae6a-121">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="1ae6a-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="1ae6a-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="1ae6a-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="1ae6a-123">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="1ae6a-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="1ae6a-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (pakietu, nie rozszerzenia)</span><span class="sxs-lookup"><span data-stu-id="1ae6a-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="1ae6a-125">Wszystkie zmiany</span><span class="sxs-lookup"><span data-stu-id="1ae6a-125">All Changes</span></span>
<span data-ttu-id="1ae6a-126">Wystąpiły problemy 10 w wersji.</span><span class="sxs-lookup"><span data-stu-id="1ae6a-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="1ae6a-127">Pełną listę prac elementów usunięto w wersji NuGet 2.8.2, sprawdź widok [NuGet Tracker problem w tej wersji](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="1ae6a-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
