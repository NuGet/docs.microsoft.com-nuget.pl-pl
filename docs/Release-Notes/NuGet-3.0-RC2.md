---
title: Informacje o wersji NuGet 3.0 RC2 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 20f9b360-2d78-4676-a803-e86996eb2f10
description: "Informacje o wersji programu NuGet 3.0 RC2 tym znanych problemów, poprawki, dodatkowe funkcje i dcr."
keywords: NuGet 3.0 RC2 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2a708babf200a650a0faffc704235d3c142f510f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="6b186-104">Informacje o wersji NuGet 3.0 RC2</span><span class="sxs-lookup"><span data-stu-id="6b186-104">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="6b186-105">[Informacje o wersji RC NuGet 3.0](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 informacje o wersji](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="6b186-105">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="6b186-106">NuGet 3.0 RC2 został wydany 3 czerwcu 2015 roku jako tymczasowy wersji dostępne w galerii programu Visual Studio 2015 rozszerzenia i [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="6b186-106">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="6b186-107">Ta wersja zawiera kilka ważnych poprawek i ulepszenia wydajności, które firma Microsoft mieli świadomość były ważne Zwolnij przed ukończone wersji programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="6b186-107">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="6b186-108">Ta wersja rozszerzenia NuGet jest dostępna tylko dla programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="6b186-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="6b186-109">Łącznie, możemy zamknąć 158 problemów dotyczących tej wersji i możesz przejrzeć [pełną listę problemów w serwisie GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="6b186-109">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="6b186-110">Podsumowanie Najważniejsze problemy rozwiązane</span><span class="sxs-lookup"><span data-stu-id="6b186-110">Summary of top issues resolved</span></span>

* [<span data-ttu-id="6b186-111">Wywołuje zaktualizować częste sieci, gdy odświeża okno Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="6b186-111">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="6b186-112">Opóźnienie przewijania zainstalowanym zmiana na widok w Menedżerze pakietów</span><span class="sxs-lookup"><span data-stu-id="6b186-112">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="6b186-113">Wywołania sieci powinny być uruchamiane w wątku w tle</span><span class="sxs-lookup"><span data-stu-id="6b186-113">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="6b186-114">Dodano pola wyboru "Nie pokazuj okna podglądu"</span><span class="sxs-lookup"><span data-stu-id="6b186-114">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="6b186-115">Dodano procesu ograniczania przepustowości, aby zmniejszyć obciążenie procesora</span><span class="sxs-lookup"><span data-stu-id="6b186-115">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="6b186-116">Ulepszona obsługa odwołania portable klasy biblioteki</span><span class="sxs-lookup"><span data-stu-id="6b186-116">Improved portable-class-library reference handling</span></span>
    * [<span data-ttu-id="6b186-117">https://github.com/NuGet/Home/issues/562</span><span class="sxs-lookup"><span data-stu-id="6b186-117">https://github.com/NuGet/Home/issues/562</span></span>](https://github.com/NuGet/Home/issues/562)
    * [<span data-ttu-id="6b186-118">https://github.com/NuGet/Home/issues/454</span><span class="sxs-lookup"><span data-stu-id="6b186-118">https://github.com/NuGet/Home/issues/454</span></span>](https://github.com/NuGet/Home/issues/454)
    * [<span data-ttu-id="6b186-119">https://github.com/NuGet/Home/issues/440</span><span class="sxs-lookup"><span data-stu-id="6b186-119">https://github.com/NuGet/Home/issues/440</span></span>](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="6b186-120">Funkcji AutoComplete usługa została z uwzględnieniem wielkości liter</span><span class="sxs-lookup"><span data-stu-id="6b186-120">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="6b186-121">Aktualizacja ponowne wprowadzenie poświadczeń uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="6b186-121">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="6b186-122">Rejestrowanie udoskonalone błędów</span><span class="sxs-lookup"><span data-stu-id="6b186-122">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="6b186-123">Ulepszone środowiska powershell komunikaty o błędach podczas wywoływania metody pakietu aktualizacji</span><span class="sxs-lookup"><span data-stu-id="6b186-123">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="6b186-124">Pobierz to [aktualizacji do rozszerzenia NuGet](https://nuget.codeplex.com/releases/view/615507) w witrynie Codeplex i można śledzić na [naszym blogu](http://blog.nuget.org) więcej i powiadomień dla NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="6b186-124">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>