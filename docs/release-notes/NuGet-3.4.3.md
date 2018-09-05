---
title: Informacje o wersji narzędzia NuGet 3.4.3
description: Informacje o wersji NuGet 3.4.3, w tym — znane problemy, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6ee4ecc06eb5119e24108d1cd6d2050254c45817
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549168"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="55c38-103">Informacje o wersji narzędzia NuGet 3.4.3</span><span class="sxs-lookup"><span data-stu-id="55c38-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="55c38-104">[Informacje o wersji NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [informacjach o wersji NuGet 3.4.4](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="55c38-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="55c38-105">Narzędzia NuGet 3.4.3 została wydana 22 kwietnia 2016 r. Aby rozwiązać wiele problemów, które zostały zidentyfikowane w wersji 3.4 i kolejnych.</span><span class="sxs-lookup"><span data-stu-id="55c38-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="55c38-106">Możesz pobrać VSIX i nuget.exe [tutaj](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="55c38-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="55c38-107">Aktualizacje i ulepszenia</span><span class="sxs-lookup"><span data-stu-id="55c38-107">Updates and Improvements</span></span>

* <span data-ttu-id="55c38-108">Poprawiono niezawodność programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="55c38-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="55c38-109">Usunęliśmy kilka problemów w pakiecie NuGet, który spowodował awarię w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="55c38-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="55c38-110">Poprawki</span><span class="sxs-lookup"><span data-stu-id="55c38-110">Fixes</span></span>

* <span data-ttu-id="55c38-111">Rozwiązano niektóre problemy z autoryzacją nuget prywatny chroniony hasłem, źródła danych.</span><span class="sxs-lookup"><span data-stu-id="55c38-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="55c38-112">Rozwiązano problem wokół nie będzie w stanie przywracania PCL z `project.json` za pomocą środowiska uruchomieniowe określona.</span><span class="sxs-lookup"><span data-stu-id="55c38-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="55c38-113">Niektórzy klienci zostały przekroczone sporadycznych błędów podczas instalowania pakietów.</span><span class="sxs-lookup"><span data-stu-id="55c38-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="55c38-114">To teraz został rozwiązany w tej wersji.</span><span class="sxs-lookup"><span data-stu-id="55c38-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="55c38-115">Rozwiązano problem powodujący niepowodzenia przywracania w języku C + +/ CLI projekty przy użyciu `project.json`.</span><span class="sxs-lookup"><span data-stu-id="55c38-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="55c38-116">Niektóre pakiety (np. ModernHttpClient) gdzie brakiem rozpakowano poprawnie zastosowania nuget w rozwiązaniu mono.</span><span class="sxs-lookup"><span data-stu-id="55c38-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="55c38-117">To teraz został rozwiązany w tej wersji.</span><span class="sxs-lookup"><span data-stu-id="55c38-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="55c38-118">Aby uzyskać pełną listę poprawek i udoskonaleń w tej wersji, zapoznaj się z listy problemów dotyczących [tutaj](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="55c38-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>