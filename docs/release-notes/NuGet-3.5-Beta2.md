---
title: 3.5 informacje o wersji Beta2
description: Informacje o wersji programu NuGet 3.5 Beta 2, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b47939e2fafc11823c41a849b3c58bbf0800ada
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551994"
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="3f824-103">Informacje o wersji programu NuGet 3.5 Beta2.</span><span class="sxs-lookup"><span data-stu-id="3f824-103">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="3f824-104">[Informacje o wersji 3.5 Beta NuGet](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5 RC wersji](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="3f824-104">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="3f824-105">NuGet 3.5 Beta 2 RTM została opublikowana 27 czerwca 2016 r dla programu Visual Studio 2013 i nuget.exe</span><span class="sxs-lookup"><span data-stu-id="3f824-105">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="3f824-106">Pełny dziennik zmian</span><span class="sxs-lookup"><span data-stu-id="3f824-106">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="3f824-107">Lista problemów</span><span class="sxs-lookup"><span data-stu-id="3f824-107">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="3f824-108">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="3f824-108">Bug Fixes</span></span>

* <span data-ttu-id="3f824-109">Komunikat o błędzie zaktualizowane na brak obsługi decrpytion hasła w programie .NET Core dla uwierzytelnione kanały informacyjne - [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="3f824-109">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="3f824-110">Konsola Menedżera pakietów Get-Package zakończy się niepowodzeniem, jeśli projekt .NET Core jest otwarty — [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="3f824-110">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="3f824-111">Napraw nieprawidłowa obsługa 403 w poleceniu wypychania NuGet [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="3f824-111">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="3f824-112">Rozwiązywanie problemów w odinstalowywanie pakietów w rozwiązaniu powiązany do kontroli źródła programu TFS, gdy disableSourceControlIntegration jest ustawiona na wartość true - [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="3f824-112">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="3f824-113">Napraw aktualizacji pakietu uwzględniać konto pakiety-target - [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="3f824-113">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="3f824-114">Użyj poziom szczegółowości MSBuild, aby ustawić poziom rejestrowania dla Menedżera pakietów Nuget, akcje interfejsu użytkownika — [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="3f824-114">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="3f824-115">Konfiguracja NuGet poprawka jest nieprawidłowy w projektów witryny sieci Web — VS 2015 VSIX (v3.4.3) — [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="3f824-115">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="3f824-116">Rozwiązywanie problemów z dodatkiem Service pack z `.csproj` gdy pliki zawartości są uwzględnione - [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="3f824-116">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="3f824-117">DefaultPushSource w `NuGetDefaults.Config` (`ProgramData\NuGet`) nie działa — [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="3f824-117">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="3f824-118">Rozwiązać problem w wersji programu Nuget 3.4.3 - wartość nie może być pusta przy tworzeniu pakietu - [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="3f824-118">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="3f824-119">Przywracania przy użyciu przechowywanych poświadczeń z pliku Nuget.Config dla źródeł danych usługi VSTS — [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="3f824-119">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="3f824-120">Wyników — poprawki alokacje nadmierne w kodzie porównania wersji - [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="3f824-120">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="3f824-121">Rozwiązywanie problemów, gdy wiele wystąpień programu nuget.exe próbuje zainstalować ten sam pakiet równolegle - [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="3f824-121">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="3f824-122">Wydajność — pamięć podręczna informacji o zależnościach dla operacji obejmujących wiele projektów — [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="3f824-122">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="3f824-123">Rozwiąż problem w przypadku, gdy nie można źródeł pakietów można dodać z ustawień, gdy lista źródłowa jest pusta — [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="3f824-123">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="3f824-124">Napraw błąd Misleading, podczas próby zainstalowania pakietu, który zależy od czasu projektowania fasad - [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="3f824-124">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="3f824-125">Instalowanie pakietu z poziomu konsoli PackageManager z ustawieniem "All" próbuje tylko pierwsze źródło - [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="3f824-125">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="3f824-126">Rozwiązywanie problemów z pakietami, które znajdują się pliki z czasem zapisu w przyszłości (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="3f824-126">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="3f824-127">Wyświetlanie wyjątku, gdy wystąpi awaria znajdowanie projektów w polecenia update - [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="3f824-127">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="3f824-128">Zawartość pakietu jest nie została poprawnie przywrócona podczas instalowania pakietu z v3.3 nuget + źródła danych z argumentem - Właściwość NoCache Jeśli pakiet zawiera `.nupkg` plików — [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="3f824-128">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="3f824-129">Rozwiązanie problemu z pakietu instalacji (wszystkich źródeł), gdy brak pakietu ze źródła 1 - [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="3f824-129">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="3f824-130">Zainstaluj bloków, jeśli pojedyncze źródło odmawia autoryzacji - [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="3f824-130">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="3f824-131">`.nuspec` zakres powinien przesłonić - IncludeReferencedProjects wersja — wersja [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="3f824-131">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="3f824-132">Aktualizacji NuGet 3.3.0 kończy się niepowodzeniem z "… dodatkowe ograniczenia zdefiniowane w pliku packages.config zapobiega tej operacji."</span><span class="sxs-lookup"><span data-stu-id="3f824-132">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="3f824-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="3f824-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="3f824-134">Aktualizacja nuget.exe spada, silna nazwa zestawu i atrybut Private.</span><span class="sxs-lookup"><span data-stu-id="3f824-134">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="3f824-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="3f824-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="3f824-136">Rozwiązywanie problemów z względna ścieżka do pliku dla "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="3f824-136">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="3f824-137">Poprawić komunikaty o błędach rozpoznawania Update - [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="3f824-137">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="3f824-138">Funkcje i zmiany sposobu działania</span><span class="sxs-lookup"><span data-stu-id="3f824-138">Features and Behavior Changes</span></span>

* <span data-ttu-id="3f824-139">wypychane nuget.exe — parametr limitu czasu nie działa — [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="3f824-139">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="3f824-140">Przywracanie nuget.exe nie generuje `.props` i `.targets` pliki `.nuproj` projektów (Regresja w v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="3f824-140">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="3f824-141">Potrzebujesz rozszerzeń interfejsu API, aby porównać platform z import - [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="3f824-141">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="3f824-142">Ukryj opcje zależność, korzystając z `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="3f824-142">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="3f824-143">Wydrukować nuget.exe nagłówka wersji w szczegółowe dane wyjściowe — [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="3f824-143">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="3f824-144">NuGet należy dodać obsługę /nativeassets/ /runtimes/ {rid} {txm} / - [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="3f824-144">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>