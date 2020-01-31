---
title: Informacje o wersji narzędzia NuGet 3,3
description: Informacje o wersji programu NuGet 3,3, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa8290c80cc500b59d1779bf76662c07382fd277
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813783"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="d2d2c-103">Informacje o wersji narzędzia NuGet 3,3</span><span class="sxs-lookup"><span data-stu-id="d2d2c-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="d2d2c-104">[Informacje o wersji pakietu NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3,4-RC — informacje o wersji](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="d2d2c-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="d2d2c-105">Pakiet NuGet 3,3 został wydane 30 listopada 2015 z znaczącą liczbą aktualizacji interfejsu użytkownika i funkcjami wiersza polecenia, a także kolekcją przydatnych poprawek do klientów programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="d2d2c-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="d2d2c-106">Nowe funkcje</span><span class="sxs-lookup"><span data-stu-id="d2d2c-106">New Features</span></span>

* <span data-ttu-id="d2d2c-107">Wprowadzono dostawców poświadczeń, dzięki którym klienci wiersza polecenia NuGet mogą bezproblemowo współpracować z uwierzytelnionym źródłem danych.</span><span class="sxs-lookup"><span data-stu-id="d2d2c-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="d2d2c-108">[Instrukcje dotyczące sposobu instalowania dostawcy poświadczeń Visual Studio Team Services](../reference/extensibility/nuget-exe-credential-providers.md) i konfigurowania klientów NuGet do korzystania z nich są dostępne w dokumentach programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="d2d2c-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../reference/extensibility/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="d2d2c-109">Nowe funkcje interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="d2d2c-109">New User Interface Features</span></span>

* <span data-ttu-id="d2d2c-110">Oddziel dostępne karty przeglądania, instalacji i aktualizacji</span><span class="sxs-lookup"><span data-stu-id="d2d2c-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="d2d2c-111">Dostępne aktualizacje znaczek wskazujące liczbę pakietów z dostępnymi aktualizacjami</span><span class="sxs-lookup"><span data-stu-id="d2d2c-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="d2d2c-112">Identyfikatory pakietów na liście pakietów wskazujące, czy pakiet jest zainstalowany lub czy jest dostępna aktualizacja</span><span class="sxs-lookup"><span data-stu-id="d2d2c-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="d2d2c-113">Liczba pobrań i autor dodana do listy pakietów</span><span class="sxs-lookup"><span data-stu-id="d2d2c-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="d2d2c-114">Najwyższy dostępny numer wersji i aktualnie zainstalowany numer wersji na liście pakietów</span><span class="sxs-lookup"><span data-stu-id="d2d2c-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="d2d2c-115">Przyciski akcji umożliwiające szybkie instalowanie, aktualizowanie i odinstalowywanie z listy pakietów</span><span class="sxs-lookup"><span data-stu-id="d2d2c-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="d2d2c-116">Wyczyść przyciski akcji na panelu szczegółów pakietu</span><span class="sxs-lookup"><span data-stu-id="d2d2c-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="d2d2c-117">Data aktualizacji pakietu na panelu szczegółów pakietu</span><span class="sxs-lookup"><span data-stu-id="d2d2c-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="d2d2c-118">Konsolidowanie panelu w widoku rozwiązania</span><span class="sxs-lookup"><span data-stu-id="d2d2c-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="d2d2c-119">Sortowanie siatki projektów i zainstalowanych numerów wersji w widoku rozwiązania</span><span class="sxs-lookup"><span data-stu-id="d2d2c-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="d2d2c-120">Nowe funkcje wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="d2d2c-120">New Command-line Features</span></span>

<span data-ttu-id="d2d2c-121">W tej wersji wprowadziliśmy polecenia `add` i `init` w celu zainicjowania repozytoriów opartych na folderach zgodnie z opisem w [dokumentacji NuGet. exe](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="d2d2c-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="d2d2c-122">Repozytoria tworzone i utrzymywane przy użyciu tej struktury folderów [zapewniają znaczący](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) wpływ na wydajność, jak opisano w naszym blogu.</span><span class="sxs-lookup"><span data-stu-id="d2d2c-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="d2d2c-123">contentFiles</span><span class="sxs-lookup"><span data-stu-id="d2d2c-123">ContentFiles</span></span>

<span data-ttu-id="d2d2c-124">Zawartość jest teraz obsługiwana w `project.json` projektach zarządzanych za pomocą nowego folderu `contentFiles` i `.nuspec` notacji elementu `contentFiles`.</span><span class="sxs-lookup"><span data-stu-id="d2d2c-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="d2d2c-125">Ta zawartość może być bardziej bezpośrednio określona przez autora pakietu na potrzeby interakcji z systemami projektu.</span><span class="sxs-lookup"><span data-stu-id="d2d2c-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="d2d2c-126">Więcej informacji o sposobach konfigurowania contentFiles w dokumencie `.nuspec` można znaleźć w [dokumentacji. nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="d2d2c-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="d2d2c-127">Zarządzanie pamięcią podręczną pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="d2d2c-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="d2d2c-128">Wiersz polecenia NuGet został zaktualizowany w celu uwzględnienia informacji o sposobach zarządzania lokalnymi pamięciami podręcznymi na stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="d2d2c-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="d2d2c-129">Więcej informacji na temat polecenia locales jest dostępnych w [dokumentacji wiersza polecenia NuGet](../reference/cli-reference/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="d2d2c-129">More information about the locals command is available in the [NuGet command-line reference](../reference/cli-reference/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="d2d2c-130">Rozwiązano problemy</span><span class="sxs-lookup"><span data-stu-id="d2d2c-130">Fixed Issues</span></span>

<span data-ttu-id="d2d2c-131">**Istotne problemy**</span><span class="sxs-lookup"><span data-stu-id="d2d2c-131">**Notable Issues**</span></span>

* <span data-ttu-id="d2d2c-132">Przywrócono obsługę wiersza polecenia NuGet w celu przywrócenia pakietów z plikiem rozwiązania na platformie mono- [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="d2d2c-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="d2d2c-133">Pełną listę problemów, które zostały rozwiązane w wersji 3,3, można znaleźć w witrynie GitHub w punkcie [kontrolnym 3,3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="d2d2c-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="d2d2c-134">Lista problemów rozwiązanych w wersji wiersza polecenia 3,3 jest rejestrowana w [kontrolce wiersza polecenia 3,3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="d2d2c-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="d2d2c-135">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="d2d2c-135">Known Issues</span></span>

<span data-ttu-id="d2d2c-136">Będziemy nadal śledzić problemy na naszej liście problemów usługi GitHub, którą można znaleźć w witrynie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="d2d2c-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>