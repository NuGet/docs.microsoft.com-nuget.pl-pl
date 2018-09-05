---
title: Informacje o wersji 3.0 NuGet
description: Informacje o wersji programu NuGet 3.0.0 tym — znane problemy, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1ade2b5b5ff7d57d756829c1c1853b5573c17d6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551866"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="3fd6e-103">Informacje o wersji 3.0 NuGet</span><span class="sxs-lookup"><span data-stu-id="3fd6e-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="3fd6e-104">[Informacje o wersji programu NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [informacjach o wersji NuGet 3.1](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="3fd6e-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="3fd6e-105">NuGet 3.0 został wydany 20 lipca 2015 roku jako rozszerzenie pakietu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="3fd6e-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="3fd6e-106">Przeprowadziliśmy się do świadczenia tej wersji programu Visual Studio, tak aby pełnego środowiska pracy zaktualizowanych pakietów NuGet 3.0 będą dostępne dla nowych użytkowników programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3fd6e-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="3fd6e-107">Ta wersja rozszerzenia NuGet jest dostępna tylko dla programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="3fd6e-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="3fd6e-108">Firma Microsoft zaleca tych deweloperów, które mają dostęp do aktualizacji galerii programu Visual Studio do najnowszej wersji, która jest dostępna, ponieważ obecnie publikujemy aktualizacji wkrótce po wydaniu programu Visual Studio 2015, który zawiera obsługę programowania aplikacji dla systemu Windows 10.</span><span class="sxs-lookup"><span data-stu-id="3fd6e-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="3fd6e-109">W sumie możemy zamknięte 240 problemy w wersji 3.0 i możesz przejrzeć [pełną listę problemów w usłudze GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="3fd6e-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="3fd6e-110">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="3fd6e-110">Known Issues</span></span>

<span data-ttu-id="3fd6e-111">Wiele znanych problemów dostarczone w tej wersji, a wszystkie te elementy zostały usunięte w wersji 3.1 zaplanowanego postoju wersji systemu Windows 10 na 29 lipca.</span><span class="sxs-lookup"><span data-stu-id="3fd6e-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="3fd6e-112">Jesteś w stanie zaktualizować rozszerzenia programu Visual Studio z galerii na lub po tej dacie, aby rozwiązać te znane problemy.</span><span class="sxs-lookup"><span data-stu-id="3fd6e-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="3fd6e-113">Tłumaczenie nie jest dostępna do etykiety "Nie pokazuj ponownie", w oknie Podgląd i etykiety "Autorzy" w oknie Opis pakietu.</span><span class="sxs-lookup"><span data-stu-id="3fd6e-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="3fd6e-114">Podczas pracy nad projektem przy użyciu serwera TFS kontroli źródła NuGet nie może przedstawiać Menedżera pakietów interfejsu użytkownika, jeśli plik Nuget.Config jest oznaczony jako tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="3fd6e-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="3fd6e-115">**Obejście** wyewidencjonować plik z serwera TFS.</span><span class="sxs-lookup"><span data-stu-id="3fd6e-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="3fd6e-116">Tekst w kolorze żółtym "bar ponowne uruchomienie" w oknie programu NuGet Powershell nie jest widoczny, gdy używasz ciemnego motywu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3fd6e-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="3fd6e-117">**Obejście** Użyj motyw jasny programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3fd6e-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="3fd6e-118">Podsumowanie Najważniejsze problemy rozwiązane</span><span class="sxs-lookup"><span data-stu-id="3fd6e-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="3fd6e-119">Aktualizacja sieci częste wywołania podczas odświeżania okno Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="3fd6e-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="3fd6e-120">Opóźnione przewijania zainstalowanym zmiana na widok w Menedżerze pakietów</span><span class="sxs-lookup"><span data-stu-id="3fd6e-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="3fd6e-121">Wywołania sieciowe powinien zostać uruchomiony na wątku w tle</span><span class="sxs-lookup"><span data-stu-id="3fd6e-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="3fd6e-122">Dodano pole wyboru "Nie pokazuj okna (wersja zapoznawcza)"</span><span class="sxs-lookup"><span data-stu-id="3fd6e-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="3fd6e-123">Dodano proces ograniczania przepustowości, aby zmniejszyć obciążenie procesora</span><span class="sxs-lookup"><span data-stu-id="3fd6e-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="3fd6e-124">Ulepszona obsługa odwołanie do biblioteki w przypadku klas przenośna</span><span class="sxs-lookup"><span data-stu-id="3fd6e-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="3fd6e-125">Usługa autouzupełniania była uwzględniana wielkość liter</span><span class="sxs-lookup"><span data-stu-id="3fd6e-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="3fd6e-126">Aktualizacja ponownie wprowadzić poświadczenia uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="3fd6e-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="3fd6e-127">Rejestrowanie udoskonalone błędów</span><span class="sxs-lookup"><span data-stu-id="3fd6e-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="3fd6e-128">Powershell Ulepszone komunikaty o błędach podczas wywoływania pakiet aktualizacji</span><span class="sxs-lookup"><span data-stu-id="3fd6e-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="3fd6e-129">Naprawiono link "Dowiedz się więcej na temat opcji", aby uniknąć awarii w systemie Windows 10</span><span class="sxs-lookup"><span data-stu-id="3fd6e-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="3fd6e-130">Pamiętaj ustawienie pola wyboru wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="3fd6e-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="3fd6e-131">Zbieranie ulepszoną wydajność przez buforowanie wyników w projektach w rozwiązaniu</span><span class="sxs-lookup"><span data-stu-id="3fd6e-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="3fd6e-132">Wiele pakietów można gromadzić równolegle</span><span class="sxs-lookup"><span data-stu-id="3fd6e-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="3fd6e-133">Usunięte install-package-force polecenia</span><span class="sxs-lookup"><span data-stu-id="3fd6e-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="3fd6e-134">Można nadzorować [naszym blogu](http://blog.nuget.org) więcej postępu i anonse uzyskując chcesz zaoferować wsparcie dla programowania systemu Windows 10.</span><span class="sxs-lookup"><span data-stu-id="3fd6e-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>