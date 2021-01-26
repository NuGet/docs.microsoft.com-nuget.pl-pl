---
title: Informacje o wersji narzędzia NuGet 3,0 RC2
description: Informacje o wersji programu NuGet 3,0 RC2, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 355c200481f4acba9931dc3bcd85e99c5ffbf224
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780280"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="a99f6-103">Informacje o wersji narzędzia NuGet 3,0 RC2</span><span class="sxs-lookup"><span data-stu-id="a99f6-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="a99f6-104">Informacje o wersji narzędzia [NuGet 3,0 RC](../release-notes/nuget-3.0-RC.md)  |  [Informacje o wersji narzędzia NuGet 3,0](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="a99f6-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="a99f6-105">Pakiet NuGet 3,0 RC2 został opublikowany od 3 czerwca 2015 jako tymczasowe wydanie dostępne z galerii rozszerzeń programu Visual Studio 2015 i [CodePlex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="a99f6-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="a99f6-106">W tej wersji wprowadzono wiele ważnych poprawek i ulepszeń wydajności, które były ważne do wydania przed ukończeniem pełnej wersji programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="a99f6-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="a99f6-107">Ta wersja rozszerzenia NuGet jest dostępna tylko dla programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="a99f6-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="a99f6-108">W sumie zostały zamknięte 158 problemów w tej wersji i można zapoznać się z [pełną listą problemów w witrynie GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="a99f6-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="a99f6-109">Podsumowanie najważniejszych problemów rozwiązanych</span><span class="sxs-lookup"><span data-stu-id="a99f6-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="a99f6-110">Częste wywołania aktualizacji sieci podczas odświeżania okna Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="a99f6-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="a99f6-111">Opóźnione przewijanie podczas zmiany widoku na zainstalowany w Menedżerze pakietów</span><span class="sxs-lookup"><span data-stu-id="a99f6-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="a99f6-112">Wywołania sieciowe powinny być uruchamiane w wątku w tle</span><span class="sxs-lookup"><span data-stu-id="a99f6-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="a99f6-113">Dodano pole wyboru "nie pokazuj okna podglądu"</span><span class="sxs-lookup"><span data-stu-id="a99f6-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="a99f6-114">Dodano ograniczanie procesów w celu zmniejszenia użycia procesora</span><span class="sxs-lookup"><span data-stu-id="a99f6-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="a99f6-115">Ulepszona obsługa odwołań do biblioteki klas przenośnych</span><span class="sxs-lookup"><span data-stu-id="a99f6-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="a99f6-116">W usłudze autouzupełniania była rozróżniana wielkość liter</span><span class="sxs-lookup"><span data-stu-id="a99f6-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="a99f6-117">Aktualizuj, aby wprowadzić poświadczenia uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="a99f6-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="a99f6-118">Ulepszone rejestrowanie błędów</span><span class="sxs-lookup"><span data-stu-id="a99f6-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="a99f6-119">Ulepszone komunikaty o błędach programu PowerShell podczas wywoływania polecenia Update-Package</span><span class="sxs-lookup"><span data-stu-id="a99f6-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="a99f6-120">Pobierz tę [aktualizację do rozszerzenia NuGet](https://nuget.codeplex.com/releases/view/615507) z CodePlex [, aby uzyskać więcej informacji o](http://blog.nuget.org) postępie i anonsach dla programu NuGet 3,0!.</span><span class="sxs-lookup"><span data-stu-id="a99f6-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>