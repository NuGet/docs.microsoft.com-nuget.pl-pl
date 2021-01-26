---
title: Informacje o wersji narzędzia NuGet 3.4.3
description: Informacje o wersji programu NuGet 3.4.3, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f0d9740aaf0a82b9e4023b5e4990c8f4adbea63c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776463"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="fa574-103">Informacje o wersji narzędzia NuGet 3.4.3</span><span class="sxs-lookup"><span data-stu-id="fa574-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="fa574-104">Informacje o wersji narzędzia [NuGet 3.4.2](../release-notes/nuget-3.4.2.md)  |  [Informacje o wersji narzędzia NuGet 3.4.4](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="fa574-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="fa574-105">3.4.3 NuGet została wydana 22 kwietnia 2016, aby rozwiązać kilka problemów, które zostały zidentyfikowane w 3,4 i kolejnych wersjach.</span><span class="sxs-lookup"><span data-stu-id="fa574-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="fa574-106">W [tym miejscu](https://dist.nuget.org/index.html)możesz pobrać zarówno VSIX, jak i nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="fa574-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="fa574-107">Aktualizacje i ulepszenia</span><span class="sxs-lookup"><span data-stu-id="fa574-107">Updates and Improvements</span></span>

* <span data-ttu-id="fa574-108">Ulepszona niezawodność programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fa574-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="fa574-109">W programie NuGet rozwiązano pewne problemy, które spowodowały awarie w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fa574-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="fa574-110">Poprawki</span><span class="sxs-lookup"><span data-stu-id="fa574-110">Fixes</span></span>

* <span data-ttu-id="fa574-111">Rozwiązano pewne problemy z autoryzacją za pomocą prywatnych źródeł danych NuGet chronionych hasłem.</span><span class="sxs-lookup"><span data-stu-id="fa574-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="fa574-112">Rozwiązano problem polegający na tym, że nie można przywrócić programu PCL z programu `project.json` przy użyciu określonych środowisk uruchomieniowych.</span><span class="sxs-lookup"><span data-stu-id="fa574-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="fa574-113">Niektórzy klienci byli w nieprzerwanych awariach podczas instalowania pakietów.</span><span class="sxs-lookup"><span data-stu-id="fa574-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="fa574-114">Ten problem został rozwiązany w tej wersji.</span><span class="sxs-lookup"><span data-stu-id="fa574-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="fa574-115">Rozwiązano problem, który spowodował błędy przywracania w projektach C++/CLI z `project.json` .</span><span class="sxs-lookup"><span data-stu-id="fa574-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="fa574-116">Niektóre pakiety (np. ModernHttpClient), które nie są rozpakowane prawidłowo w przypadku używania NuGet w programie mono.</span><span class="sxs-lookup"><span data-stu-id="fa574-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="fa574-117">Ten problem został rozwiązany w tej wersji.</span><span class="sxs-lookup"><span data-stu-id="fa574-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="fa574-118">Aby zapoznać się z pełną listą poprawek i ulepszeń w tej wersji, zapoznaj się z listą problemów w [tym miejscu](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="fa574-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>