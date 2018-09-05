---
title: Informacje o wersji 3.3 NuGet
description: Informacje o wersji rozszerzenia NuGet 3.3 tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5fb840ab6a1329611e9cf417724bcdcd75efe2df
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546650"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="101ae-103">Informacje o wersji 3.3 NuGet</span><span class="sxs-lookup"><span data-stu-id="101ae-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="101ae-104">[Informacje o wersji NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC wersji](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="101ae-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="101ae-105">Rozszerzenia NuGet 3.3 został wydany do 30 listopada 2015 za pomocą znaczna liczba aktualizacje interfejsu użytkownika i funkcje wiersza polecenia, a także zbiór poprawek przydatne dla klientów NuGet.</span><span class="sxs-lookup"><span data-stu-id="101ae-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="101ae-106">Nowe funkcje</span><span class="sxs-lookup"><span data-stu-id="101ae-106">New Features</span></span>

* <span data-ttu-id="101ae-107">Wprowadzono dostawcy poświadczeń, które umożliwiają klientom wiersza polecenia NuGet można było bezproblemowej współpracy z uwierzytelnionego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="101ae-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="101ae-108">[Instrukcje dotyczące sposobu instalowania programu Visual Studio Team Services poświadczeń dostawcy ](../api/nuget-exe-credential-providers.md) i konfigurowanie pakietu NuGet klientów z niej korzystać, są dostępne w dokumentacji systemu NuGet.</span><span class="sxs-lookup"><span data-stu-id="101ae-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="101ae-109">Nowe funkcje interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="101ae-109">New User Interface Features</span></span>

* <span data-ttu-id="101ae-110">Oddzielne karty przeglądania, zainstalowane i dostępna aktualizacje</span><span class="sxs-lookup"><span data-stu-id="101ae-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="101ae-111">Aktualizacje dostępne wskaźniku określającą liczbę pakietów wraz z dostępnymi aktualizacjami</span><span class="sxs-lookup"><span data-stu-id="101ae-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="101ae-112">Wskaźniki pakietu na liście pakietu, aby wskazać, czy pakiet jest zainstalowany, czy dostępna jest aktualizacja</span><span class="sxs-lookup"><span data-stu-id="101ae-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="101ae-113">Pobierz liczbę i autor dodane do listy pakietów</span><span class="sxs-lookup"><span data-stu-id="101ae-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="101ae-114">Najwyższy numer wersji dostępnych i Liczba obecnie zainstalowanej wersji na liście pakietów</span><span class="sxs-lookup"><span data-stu-id="101ae-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="101ae-115">Przyciski akcji, aby umożliwić szybkiej instalacji aktualizacji i odinstalować z listy pakietów</span><span class="sxs-lookup"><span data-stu-id="101ae-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="101ae-116">Bardziej zrozumiały przyciski akcji na panelu szczegółów pakietu</span><span class="sxs-lookup"><span data-stu-id="101ae-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="101ae-117">Data aktualizacji pakietu na panelu szczegółów pakietu</span><span class="sxs-lookup"><span data-stu-id="101ae-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="101ae-118">Konsolidacja panelu w widoku rozwiązania</span><span class="sxs-lookup"><span data-stu-id="101ae-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="101ae-119">Sortowanie siatki projektów i numery wersji zainstalowanej w widoku rozwiązania</span><span class="sxs-lookup"><span data-stu-id="101ae-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="101ae-120">Nowe funkcje wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="101ae-120">New Command-line Features</span></span>

<span data-ttu-id="101ae-121">W tej wersji wprowadziliśmy `add` i `init` polecenia, aby zainicjować folderu repozytoriów, zgodnie z opisem w [odwołania nuget.exe](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="101ae-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="101ae-122">Repozytoria, które są zbudowane i z tego folderu struktury będzie [dostarczać korzystny wydajności](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) zgodnie z opisem w naszym blogu.</span><span class="sxs-lookup"><span data-stu-id="101ae-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="101ae-123">Pliki</span><span class="sxs-lookup"><span data-stu-id="101ae-123">ContentFiles</span></span>

<span data-ttu-id="101ae-124">Zawartość jest teraz obsługiwana w `project.json` zarządzanych projektów za pomocą nowego `contentFiles` folder i `.nuspec` `contentFiles` element notation.</span><span class="sxs-lookup"><span data-stu-id="101ae-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="101ae-125">Ta zawartość można określić więcej bezpośrednio przez autora pakietu w celu interakcji z systemami projektu.</span><span class="sxs-lookup"><span data-stu-id="101ae-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="101ae-126">Więcej informacji na temat sposobu konfigurowania pliki w `.nuspec` można znaleźć dokumentu w [.nuspec odwołania](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="101ae-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="101ae-127">Zmienne lokalne NuGet w pamięci podręcznej zarządzania</span><span class="sxs-lookup"><span data-stu-id="101ae-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="101ae-128">Wiersza polecenia NuGet został zaktualizowany w celu uwzględnienia informacji o sposobie zarządzania pamięciach podręcznych na stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="101ae-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="101ae-129">Więcej informacji o poleceniu zmiennych lokalnych jest dostępna w [wiersza polecenia NuGet](../tools/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="101ae-129">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="101ae-130">Rozwiązane problemy</span><span class="sxs-lookup"><span data-stu-id="101ae-130">Fixed Issues</span></span>

<span data-ttu-id="101ae-131">**Problemy godne uwagi**</span><span class="sxs-lookup"><span data-stu-id="101ae-131">**Notable Issues**</span></span>

* <span data-ttu-id="101ae-132">NuGet przywróconej za pomocą wiersza polecenia przywracania pakietów z plikiem rozwiązania na platformy Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="101ae-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="101ae-133">Pełną listę problemów, które zostały rozwiązane w wersji 3.3 można znaleźć w witrynie GitHub w ramach [3.3 punkt kontrolny](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="101ae-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="101ae-134">Lista problemów rozwiązanych w wersji 3.3 wiersza polecenia są rejestrowane w [3.3 wiersza polecenia punkt kontrolny](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="101ae-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="101ae-135">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="101ae-135">Known Issues</span></span>

<span data-ttu-id="101ae-136">W dalszym ciągu śledzenia problemów na naszej liście problemów GitHub, który znajduje się w temacie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="101ae-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>