---
title: Informacje o wersji NuGet 3.4.3 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informacje o wersji programu NuGet 3.4.3 tym — znane problemy, poprawki, dodatkowe funkcje i dcr."
keywords: NuGet 3.4.3 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 68aab607659d15f96aefeab7bb90afc787710824
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="7b725-104">Informacje o wersji NuGet 3.4.3</span><span class="sxs-lookup"><span data-stu-id="7b725-104">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="7b725-105">[Informacje o wersji NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 informacje o wersji](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="7b725-105">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="7b725-106">NuGet 3.4.3 został wydany 22 kwietnia 2016 r., aby rozwiązać pewne problemy, które zostały zidentyfikowane w 3.4 i późniejszych wersjach.</span><span class="sxs-lookup"><span data-stu-id="7b725-106">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="7b725-107">Możesz pobrać zarówno VSIX, jak i nuget.exe [tutaj](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="7b725-107">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="7b725-108">Aktualizacje i usprawnienia</span><span class="sxs-lookup"><span data-stu-id="7b725-108">Updates and Improvements</span></span>

* <span data-ttu-id="7b725-109">Większą niezawodność programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b725-109">Improved Visual Studio reliability.</span></span> <span data-ttu-id="7b725-110">Naprawiono problemy w NuGet, który spowodował awarię programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b725-110">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="7b725-111">Poprawki</span><span class="sxs-lookup"><span data-stu-id="7b725-111">Fixes</span></span>

* <span data-ttu-id="7b725-112">Usunięto niektóre problemy z autoryzacją nuget prywatny chroniony hasłem źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="7b725-112">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="7b725-113">Rozwiązano problem wokół nie będą mogli przywrócić PCL z `project.json` z określonych środowisk uruchomieniowych.</span><span class="sxs-lookup"><span data-stu-id="7b725-113">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="7b725-114">Niektórzy klienci były uruchomione w sporadycznych błędów podczas instalowania pakietów.</span><span class="sxs-lookup"><span data-stu-id="7b725-114">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="7b725-115">Teraz, ten problem został naprawiony w tej wersji.</span><span class="sxs-lookup"><span data-stu-id="7b725-115">This has now been fixed in this release.</span></span>
* <span data-ttu-id="7b725-116">Rozwiązano problem powodujący błędy przywracania w języku C + +/ CLI projektów z `project.json`.</span><span class="sxs-lookup"><span data-stu-id="7b725-116">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="7b725-117">Niektóre pakiety (np. ModernHttpClient) gdy nie jest rozpakowane poprawnie Jeśli używasz nuget mono.</span><span class="sxs-lookup"><span data-stu-id="7b725-117">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="7b725-118">Teraz, ten problem został naprawiony w tej wersji.</span><span class="sxs-lookup"><span data-stu-id="7b725-118">This has now been fixed in this release.</span></span>

<span data-ttu-id="7b725-119">Aby uzyskać pełną listę poprawek i ulepszenia w tej wersji, zapoznaj się z listy problemów dotyczących [tutaj](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="7b725-119">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>