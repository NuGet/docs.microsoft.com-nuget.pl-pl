---
title: NuGet 3.0 RC2 — informacje o wersji
description: Informacje o wersji programu NuGet 3.0 w wersji RC2 tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 863e48e632387b768a43530b987683605baf6db7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545824"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="6d770-103">NuGet 3.0 RC2 — informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="6d770-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="6d770-104">[Informacje o wersji programu NuGet 3.0 RC](../release-notes/nuget-3.0-RC.md) | [informacjach o wersji NuGet 3.0](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="6d770-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="6d770-105">NuGet 3.0 w wersji RC2 został wydany 3 czerwca 2015 jako tymczasowy wydania dostępne z w galerii Visual Studio 2015 rozszerzenia i [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="6d770-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="6d770-106">Ta wersja ma kilka ważnych poprawek błędów i ulepszenia wydajności, które będziemy mieli świadomość były ważne, aby zwolnić przed ukończone wersji programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="6d770-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="6d770-107">Ta wersja rozszerzenia NuGet jest dostępna tylko dla programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="6d770-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="6d770-108">W sumie możemy zamknięcia 158 problemów w tej wersji, i możesz przejrzeć [pełną listę problemów w usłudze GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="6d770-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="6d770-109">Podsumowanie Najważniejsze problemy rozwiązane</span><span class="sxs-lookup"><span data-stu-id="6d770-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="6d770-110">Aktualizacja sieci częste wywołania podczas odświeżania okno Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="6d770-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="6d770-111">Opóźnione przewijania zainstalowanym zmiana na widok w Menedżerze pakietów</span><span class="sxs-lookup"><span data-stu-id="6d770-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="6d770-112">Wywołania sieciowe powinien zostać uruchomiony na wątku w tle</span><span class="sxs-lookup"><span data-stu-id="6d770-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="6d770-113">Dodano pole wyboru "Nie pokazuj okna (wersja zapoznawcza)"</span><span class="sxs-lookup"><span data-stu-id="6d770-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="6d770-114">Dodano proces ograniczania przepustowości, aby zmniejszyć obciążenie procesora</span><span class="sxs-lookup"><span data-stu-id="6d770-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="6d770-115">Ulepszona obsługa odwołanie do biblioteki w przypadku klas przenośna</span><span class="sxs-lookup"><span data-stu-id="6d770-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="6d770-116">Usługa autouzupełniania była uwzględniana wielkość liter</span><span class="sxs-lookup"><span data-stu-id="6d770-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="6d770-117">Aktualizacja ponownie wprowadzić poświadczenia uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="6d770-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="6d770-118">Rejestrowanie udoskonalone błędów</span><span class="sxs-lookup"><span data-stu-id="6d770-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="6d770-119">Powershell Ulepszone komunikaty o błędach podczas wywoływania pakiet aktualizacji</span><span class="sxs-lookup"><span data-stu-id="6d770-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="6d770-120">Pobierz ten [aktualizacji do rozszerzenie NuGet](https://nuget.codeplex.com/releases/view/615507) z witryny Codeplex i można nadzorować [naszym blogu](http://blog.nuget.org) więcej postępu i anonsów dla pakietów NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="6d770-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>