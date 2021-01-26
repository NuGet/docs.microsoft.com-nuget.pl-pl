---
title: Informacje o wersji narzędzia NuGet 3,0
description: Informacje o wersji programu NuGet 3.0.0, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4d4ce17c33dc38df5504a77d9cc3530d466d70af
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776551"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="d774a-103">Informacje o wersji narzędzia NuGet 3,0</span><span class="sxs-lookup"><span data-stu-id="d774a-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="d774a-104">Informacje o wersji narzędzia [NuGet 3,0 RC2](../release-notes/nuget-3.0-RC2.md)  |  [Informacje o wersji narzędzia NuGet 3,1](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="d774a-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="d774a-105">Pakiet NuGet 3,0 został wydano 20 lipca 2015 jako rozszerzenie pakietu do programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="d774a-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="d774a-106">Firma Microsoft wypychamy, aby dostarczyć tę wersję za pomocą programu Visual Studio, dzięki czemu kompletne zaktualizowane środowisko NuGet 3,0 będzie dostępne dla nowych użytkowników programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d774a-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="d774a-107">Ta wersja rozszerzenia NuGet jest dostępna tylko dla programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="d774a-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="d774a-108">Zaleca się, aby Ci deweloperzy mieli dostęp do aktualizacji galerii programu Visual Studio do najnowszej dostępnej wersji, ponieważ publikujemy aktualizację wkrótce po wydaniu programu Visual Studio 2015, który zawiera wsparcie dla rozwoju systemu Windows 10.</span><span class="sxs-lookup"><span data-stu-id="d774a-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="d774a-109">W sumie zostały zamknięte 240 problemów w wersji 3,0 i można zapoznać się z [pełną listą problemów w witrynie GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="d774a-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="d774a-110">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="d774a-110">Known Issues</span></span>

<span data-ttu-id="d774a-111">Istniało wiele znanych problemów z tą wersją, a wszystkie te elementy zostały rozwiązane w naszym zaplanowanym 3,1 wersji, aby uzyskać zbieżność z wersją systemu Windows 10 w dniu 29 lipca.</span><span class="sxs-lookup"><span data-stu-id="d774a-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="d774a-112">Możesz zaktualizować rozszerzenie programu Visual Studio z galerii w tej dacie lub później, aby rozwiązać te znane problemy.</span><span class="sxs-lookup"><span data-stu-id="d774a-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="d774a-113">Nie podano tłumaczenia na etykietę "nie pokazuj ponownie" w oknie podglądu i etykiecie "autorów" w oknie opisu pakietu.</span><span class="sxs-lookup"><span data-stu-id="d774a-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="d774a-114">Podczas pracy nad projektem przy użyciu kontroli źródła TFS, NuGet nie może przedstawić interfejsu użytkownika Menedżera pakietów, jeśli plik Nuget.Config jest oznaczony jako tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="d774a-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="d774a-115">**Obejście problemu** Wyewidencjonuj plik z TFS.</span><span class="sxs-lookup"><span data-stu-id="d774a-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="d774a-116">W przypadku korzystania z ciemnego motywu programu Visual Studio tekst w żółtym "pasku ponownego uruchamiania" w oknie programu PowerShell NuGet nie jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="d774a-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="d774a-117">**Obejście problemu** Użyj motywu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d774a-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="d774a-118">Podsumowanie najważniejszych problemów rozwiązanych</span><span class="sxs-lookup"><span data-stu-id="d774a-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="d774a-119">Częste wywołania aktualizacji sieci podczas odświeżania okna Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="d774a-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="d774a-120">Opóźnione przewijanie podczas zmiany widoku na zainstalowany w Menedżerze pakietów</span><span class="sxs-lookup"><span data-stu-id="d774a-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="d774a-121">Wywołania sieciowe powinny być uruchamiane w wątku w tle</span><span class="sxs-lookup"><span data-stu-id="d774a-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="d774a-122">Dodano pole wyboru "nie pokazuj okna podglądu"</span><span class="sxs-lookup"><span data-stu-id="d774a-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="d774a-123">Dodano ograniczanie procesów w celu zmniejszenia użycia procesora</span><span class="sxs-lookup"><span data-stu-id="d774a-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="d774a-124">Ulepszona obsługa odwołań do biblioteki klas przenośnych</span><span class="sxs-lookup"><span data-stu-id="d774a-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="d774a-125">W usłudze autouzupełniania była rozróżniana wielkość liter</span><span class="sxs-lookup"><span data-stu-id="d774a-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="d774a-126">Aktualizuj, aby wprowadzić poświadczenia uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="d774a-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="d774a-127">Ulepszone rejestrowanie błędów</span><span class="sxs-lookup"><span data-stu-id="d774a-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="d774a-128">Ulepszone komunikaty o błędach programu PowerShell podczas wywoływania polecenia Update-Package</span><span class="sxs-lookup"><span data-stu-id="d774a-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="d774a-129">Rozwiązano link "informacje o opcjach", aby zapobiec awariom systemu Windows 10</span><span class="sxs-lookup"><span data-stu-id="d774a-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="d774a-130">Zapamiętaj ustawienie pola wyboru w wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="d774a-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="d774a-131">Ulepszone zbieranie wydajności przez buforowanie wyników między projektami w rozwiązaniu</span><span class="sxs-lookup"><span data-stu-id="d774a-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="d774a-132">Wiele pakietów może być zebranych równolegle</span><span class="sxs-lookup"><span data-stu-id="d774a-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="d774a-133">Usunięto polecenie install-package-Force</span><span class="sxs-lookup"><span data-stu-id="d774a-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="d774a-134">Zapoznaj się z [naszym blogiem](http://blog.nuget.org) , aby uzyskać więcej informacji o postępie i ogłoszeniach, jak jesteśmy gotowi do świadczenia pomocy technicznej dla rozwoju systemu Windows 10.</span><span class="sxs-lookup"><span data-stu-id="d774a-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>