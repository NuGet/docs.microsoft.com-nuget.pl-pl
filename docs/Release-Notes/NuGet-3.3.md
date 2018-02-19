---
title: Informacje o wersji NuGet 3.3 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informacje o wersji dla tym znanych problemów, poprawki, dodatkowe funkcje i dcr 3.3 NuGet."
keywords: NuGet 3.3 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4d077fb53abd8033aad6da01ad090297109aa68c
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="78cfe-104">Informacje o wersji 3.3 NuGet</span><span class="sxs-lookup"><span data-stu-id="78cfe-104">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="78cfe-105">[Informacje o wersji NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC informacje o wersji](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="78cfe-105">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="78cfe-106">NuGet 3.3 został wydany 30 listopada 2015 z znaczących aktualizacje interfejsu użytkownika i funkcje wiersza polecenia, a także kolekcję przydatne poprawek klientom NuGet.</span><span class="sxs-lookup"><span data-stu-id="78cfe-106">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="78cfe-107">Nowe funkcje</span><span class="sxs-lookup"><span data-stu-id="78cfe-107">New Features</span></span>

* <span data-ttu-id="78cfe-108">Dostawcy poświadczeń zostały wprowadzone zezwalające klientom wiersza polecenia NuGet można było współpracuje z uwierzytelnionego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="78cfe-108">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="78cfe-109">[Instrukcje dotyczące instalowania programu Visual Studio Team Services poświadczeń dostawcy ](../api/nuget-exe-credential-providers.md) i skonfigurować NuGet klientom na używanie go są dostępne na NuGet Docs.</span><span class="sxs-lookup"><span data-stu-id="78cfe-109">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="78cfe-110">Nowe funkcje interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="78cfe-110">New User Interface Features</span></span>

* <span data-ttu-id="78cfe-111">Oddzielne karty przeglądania, zainstalowane i dostępne aktualizacje</span><span class="sxs-lookup"><span data-stu-id="78cfe-111">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="78cfe-112">Aktualizacje dostępne wskaźnika wskazującą liczbę pakietów o dostępności aktualizacji</span><span class="sxs-lookup"><span data-stu-id="78cfe-112">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="78cfe-113">Identyfikatory pakietów na liście pakietów, aby wskazać, czy pakiet jest zainstalowany, czy dostępna jest aktualizacja</span><span class="sxs-lookup"><span data-stu-id="78cfe-113">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="78cfe-114">Pobierz liczbę i autora dodane do listy pakietów</span><span class="sxs-lookup"><span data-stu-id="78cfe-114">Download count and author added to the package list</span></span>
* <span data-ttu-id="78cfe-115">Największa liczba dostępnych wersji i numer obecnie zainstalowanej wersji na liście pakietu</span><span class="sxs-lookup"><span data-stu-id="78cfe-115">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="78cfe-116">Przyciski akcji umożliwia szybkiej instalacji aktualizacji i odinstalować z listy pakietów</span><span class="sxs-lookup"><span data-stu-id="78cfe-116">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="78cfe-117">Jaśniejszy przycisków akcji w panelu szczegółów pakietu</span><span class="sxs-lookup"><span data-stu-id="78cfe-117">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="78cfe-118">Data aktualizacji pakietu w panelu szczegółów pakietu</span><span class="sxs-lookup"><span data-stu-id="78cfe-118">Package update date on the package detail panel</span></span>
* <span data-ttu-id="78cfe-119">Konsolidacja panelu w widoku Solution</span><span class="sxs-lookup"><span data-stu-id="78cfe-119">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="78cfe-120">Sortowanie siatki projektów i numery wersji zainstalowanej w widoku rozwiązania</span><span class="sxs-lookup"><span data-stu-id="78cfe-120">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="78cfe-121">Nowe funkcje wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="78cfe-121">New Command-line Features</span></span>

<span data-ttu-id="78cfe-122">W tej wersji wprowadzono `add` i `init` polecenia, aby zainicjować na podstawie folderu repozytoria zgodnie z opisem w [odwołania nuget.exe](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="78cfe-122">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="78cfe-123">Repozytoria, które są konstruowane i z tego folderu struktury będzie [dostarczania korzystny wydajności](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) w sposób opisany w naszym blogu.</span><span class="sxs-lookup"><span data-stu-id="78cfe-123">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="78cfe-124">Pliki</span><span class="sxs-lookup"><span data-stu-id="78cfe-124">ContentFiles</span></span>

<span data-ttu-id="78cfe-125">Zawartość jest teraz obsługiwana w `project.json` zarządzane za pomocą nowej `contentFiles` folderu i `.nuspec` `contentFiles` element notation.</span><span class="sxs-lookup"><span data-stu-id="78cfe-125">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="78cfe-126">Ta zawartość można określić więcej bezpośrednio przez autora pakietu w celu interakcji z systemami projektu.</span><span class="sxs-lookup"><span data-stu-id="78cfe-126">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="78cfe-127">Więcej informacji na temat sposobu konfigurowania pliki w `.nuspec` można znaleźć w dokumencie [.nuspec odwołania](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="78cfe-127">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="78cfe-128">Zmienne lokalne NuGet pamięci podręcznej zarządzania</span><span class="sxs-lookup"><span data-stu-id="78cfe-128">NuGet Locals Cache Management</span></span>

<span data-ttu-id="78cfe-129">Wiersza polecenia NuGet została zaktualizowana w celu uwzględnienia informacji o sposobie zarządzania lokalnej pamięci podręcznej na stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="78cfe-129">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="78cfe-130">Więcej informacji o poleceniu zmiennych lokalnych jest dostępna w [wiersza polecenia NuGet](../tools/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="78cfe-130">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="78cfe-131">Rozwiązane problemy</span><span class="sxs-lookup"><span data-stu-id="78cfe-131">Fixed Issues</span></span>

<span data-ttu-id="78cfe-132">**Godne uwagi problemy**</span><span class="sxs-lookup"><span data-stu-id="78cfe-132">**Notable Issues**</span></span>

* <span data-ttu-id="78cfe-133">Pakiety NuGet przywrócone za pomocą wiersza polecenia przywracania z pliku rozwiązania na Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="78cfe-133">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="78cfe-134">Pełną listę problemów, które zostały opisane w 3.3 wersji można znaleźć w witrynie GitHub pod [3.3 punkt kontrolny](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="78cfe-134">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="78cfe-135">Lista problemów rozwiązanych w 3.3 wersji wiersza polecenia są rejestrowane w [3.3 wiersza polecenia punkt kontrolny](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="78cfe-135">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="78cfe-136">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="78cfe-136">Known Issues</span></span>

<span data-ttu-id="78cfe-137">W dalszym ciągu do śledzenia problemów w naszej listy problemów GitHub, który znajduje się w temacie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="78cfe-137">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>