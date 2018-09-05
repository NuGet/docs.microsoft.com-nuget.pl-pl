---
title: Informacje o wersji NuGet 2.8.2
description: Informacje o wersji programu NuGet 2.8.2 tym — znane problemy, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ed22aef6766bbe8e4b688e0587304a18eaeb8895
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551151"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="0e984-103">Informacje o wersji NuGet 2.8.2</span><span class="sxs-lookup"><span data-stu-id="0e984-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="0e984-104">[Informacje o wersji NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [informacje o wersji programu NuGet 2.8.3](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="0e984-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="0e984-105">NuGet 2.8.2 została wydana 22 maja 2014 r.</span><span class="sxs-lookup"><span data-stu-id="0e984-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="0e984-106">W tej wersji uwzględnione tylko zmiany wiersza polecenia nuget.exe, pakiet NuGet.Server i inne pakiety NuGet.</span><span class="sxs-lookup"><span data-stu-id="0e984-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="0e984-107">Wersja nie zawiera rozszerzenia programu WebMatrix lub zaktualizowane rozszerzenie programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0e984-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="0e984-108">Znaczące zmiany</span><span class="sxs-lookup"><span data-stu-id="0e984-108">Notable Updates</span></span>

<span data-ttu-id="0e984-109">Najbardziej znaczące zmiany były związane z wiersza polecenia nuget.exe oraz pakiet NuGet.Server (na potrzeby samodzielnie hostowane kanały informacyjne NuGet).</span><span class="sxs-lookup"><span data-stu-id="0e984-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="0e984-110">Nuget.exe ważne poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="0e984-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="0e984-111">nuget.exe wypychania nie powiedzie się i utrzymuje ponawianie próby</span><span class="sxs-lookup"><span data-stu-id="0e984-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="0e984-112">nuget.exe wypychania nie wysyła poprawne poświadczenia uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="0e984-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="0e984-113">nuget.exe wypychania nie wykonaj przekierowania tymczasowego</span><span class="sxs-lookup"><span data-stu-id="0e984-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="0e984-114">Naprawienie usterki NuGet.Server ważne</span><span class="sxs-lookup"><span data-stu-id="0e984-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="0e984-115">Nieprawidłowa wartość zwrócona przez NuGet.Server IsAbsoluteLatestVersion</span><span class="sxs-lookup"><span data-stu-id="0e984-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="0e984-116">Zaktualizowano pakiety</span><span class="sxs-lookup"><span data-stu-id="0e984-116">Packages Updated</span></span>

<span data-ttu-id="0e984-117">Wiersza polecenia nuget.exe oraz NuGet.Server poprawki są dostarczane jako aktualizacje pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="0e984-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="0e984-118">Wystąpiły inne pakiety aktualizowane przy użyciu 2.8.2 także.</span><span class="sxs-lookup"><span data-stu-id="0e984-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="0e984-119">Poniżej przedstawiono listę zaktualizowanych pakietów:</span><span class="sxs-lookup"><span data-stu-id="0e984-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="0e984-120">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="0e984-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="0e984-121">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="0e984-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="0e984-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="0e984-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="0e984-123">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="0e984-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="0e984-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (pakiet, nie rozszerzenia)</span><span class="sxs-lookup"><span data-stu-id="0e984-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="0e984-125">Wszystkie zmiany</span><span class="sxs-lookup"><span data-stu-id="0e984-125">All Changes</span></span>
<span data-ttu-id="0e984-126">Wystąpiły problemy 10, które zostały rozwiązane w wydaniu.</span><span class="sxs-lookup"><span data-stu-id="0e984-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="0e984-127">Pełną listę prac elementy rozwiązane w NuGet 2.8.2, sprawdź widok [NuGet narzędzie do śledzenia problemów w tej wersji](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="0e984-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
