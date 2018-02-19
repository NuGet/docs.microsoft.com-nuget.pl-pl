---
title: Informacje o wersji NuGet 3.0 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informacje o wersji programu NuGet 3.0.0 tym — znane problemy, poprawki, dodatkowe funkcje i dcr."
keywords: NuGet 3.0.0 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 65251b28093d2ac275053b8bfef6620e16e3fb4a
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="4260b-104">Informacje o wersji 3.0 NuGet</span><span class="sxs-lookup"><span data-stu-id="4260b-104">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="4260b-105">[Informacje o wersji NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 informacje o wersji](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="4260b-105">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="4260b-106">NuGet 3.0 został wydany 20 lipca 2015 roku jako rozszerzenie pakietu programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="4260b-106">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="4260b-107">Firma Microsoft przypisany do dostarczania tej wersji w programie Visual Studio, dzięki czemu kompleksowe środowisko NuGet 3.0 zaktualizowane będzie dostępna dla nowych użytkowników programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4260b-107">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="4260b-108">Ta wersja rozszerzenia NuGet jest dostępna tylko dla programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="4260b-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="4260b-109">Firma Microsoft zaleca tych projektantów, którzy mają dostęp do galerii Visual Studio aktualizacji do najnowszej wersji, która jest dostępna, ponieważ będziemy publikowania aktualizacji wkrótce po wydaniu programu Visual Studio 2015, który zawiera obsługę programowania Windows 10.</span><span class="sxs-lookup"><span data-stu-id="4260b-109">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="4260b-110">Łącznie, możemy zamknięte 240 problemów w wersji 3.0 i możesz przejrzeć [pełną listę problemów w serwisie GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="4260b-110">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="4260b-111">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="4260b-111">Known Issues</span></span>

<span data-ttu-id="4260b-112">Wiele znanych problemów dostarczone w tej wersji, a wszystkie te elementy zostały usunięte w naszym zaplanowane wersji 3.1 się z wersji systemu Windows 10 w lipcu 29.</span><span class="sxs-lookup"><span data-stu-id="4260b-112">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="4260b-113">Jesteś w stanie zaktualizować rozszerzenia programu Visual Studio z galerii na lub po tym dniu, aby rozwiązać te znane problemy.</span><span class="sxs-lookup"><span data-stu-id="4260b-113">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="4260b-114">Nie podano tłumaczenia etykiety "Nie pokazuj ponownie" w oknie Podgląd i etykiety "Autorzy" w oknie Opis pakietu.</span><span class="sxs-lookup"><span data-stu-id="4260b-114">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="4260b-115">Gdy pracę nad projektem za pomocą TFS kontroli źródła, NuGet nie może przedstawić Menedżera pakietów interfejsu użytkownika, jeśli plik Nuget.Config jest oznaczony jako tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="4260b-115">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="4260b-116">**Obejście** wyewidencjonować plik z TFS.</span><span class="sxs-lookup"><span data-stu-id="4260b-116">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="4260b-117">Tekst w żółty "pasek ponowne uruchomienie" w oknie programu NuGet Powershell nie jest widoczny, gdy używasz ciemny motyw programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4260b-117">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="4260b-118">**Obejście** Użyj motywu jasny Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4260b-118">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="4260b-119">Podsumowanie Najważniejsze problemy rozwiązane</span><span class="sxs-lookup"><span data-stu-id="4260b-119">Summary of top issues resolved</span></span>

* [<span data-ttu-id="4260b-120">Wywołuje zaktualizować częste sieci, gdy odświeża okno Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="4260b-120">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="4260b-121">Opóźnienie przewijania zainstalowanym zmiana na widok w Menedżerze pakietów</span><span class="sxs-lookup"><span data-stu-id="4260b-121">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="4260b-122">Wywołania sieci powinny być uruchamiane w wątku w tle</span><span class="sxs-lookup"><span data-stu-id="4260b-122">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="4260b-123">Dodano pola wyboru "Nie pokazuj okna podglądu"</span><span class="sxs-lookup"><span data-stu-id="4260b-123">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="4260b-124">Dodano procesu ograniczania przepustowości, aby zmniejszyć obciążenie procesora</span><span class="sxs-lookup"><span data-stu-id="4260b-124">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="4260b-125">Ulepszona obsługa odwołania portable klasy biblioteki</span><span class="sxs-lookup"><span data-stu-id="4260b-125">Improved portable-class-library reference handling</span></span>
    * [<span data-ttu-id="4260b-126">https://github.com/NuGet/Home/issues/562</span><span class="sxs-lookup"><span data-stu-id="4260b-126">https://github.com/NuGet/Home/issues/562</span></span>](https://github.com/NuGet/Home/issues/562)
    * [<span data-ttu-id="4260b-127">https://github.com/NuGet/Home/issues/454</span><span class="sxs-lookup"><span data-stu-id="4260b-127">https://github.com/NuGet/Home/issues/454</span></span>](https://github.com/NuGet/Home/issues/454)
    * [<span data-ttu-id="4260b-128">https://github.com/NuGet/Home/issues/440</span><span class="sxs-lookup"><span data-stu-id="4260b-128">https://github.com/NuGet/Home/issues/440</span></span>](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="4260b-129">Funkcji AutoComplete usługa została z uwzględnieniem wielkości liter</span><span class="sxs-lookup"><span data-stu-id="4260b-129">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="4260b-130">Aktualizacja ponowne wprowadzenie poświadczeń uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="4260b-130">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="4260b-131">Rejestrowanie udoskonalone błędów</span><span class="sxs-lookup"><span data-stu-id="4260b-131">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="4260b-132">Ulepszone środowiska powershell komunikaty o błędach podczas wywoływania metody pakietu aktualizacji</span><span class="sxs-lookup"><span data-stu-id="4260b-132">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="4260b-133">Stałe link "Dowiedz się więcej na temat opcji", aby uniknąć awarii w systemie Windows 10</span><span class="sxs-lookup"><span data-stu-id="4260b-133">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="4260b-134">Pamiętaj ustawienie pola wyboru wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="4260b-134">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="4260b-135">Ulepszone zbieranie wydajności przez buforowanie wyników wielu projektów w rozwiązaniu</span><span class="sxs-lookup"><span data-stu-id="4260b-135">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="4260b-136">Można zbierać równolegle wielu pakietów</span><span class="sxs-lookup"><span data-stu-id="4260b-136">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="4260b-137">Usunięte install-package-force polecenia</span><span class="sxs-lookup"><span data-stu-id="4260b-137">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="4260b-138">Można śledzić na [naszym blogu](http://blog.nuget.org) więcej i anonsów uzyskując gotowy do świadczenia pomocy technicznej do tworzenia aplikacji systemu Windows 10.</span><span class="sxs-lookup"><span data-stu-id="4260b-138">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>