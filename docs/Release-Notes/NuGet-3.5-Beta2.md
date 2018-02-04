---
title: 3.5 informacje o wersji Beta2 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informacje o wersji programu NuGet 3.5 Beta 2 tym znanych problemów, poprawki, dodatkowe funkcje i dcr."
keywords: 3.5 NuGet w wersji Beta 2 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4073b669c19f9e96ebd35ba269919b5f42313e7c
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="25bcb-104">Informacje o wersji 3.5 Beta2 NuGet</span><span class="sxs-lookup"><span data-stu-id="25bcb-104">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="25bcb-105">[Informacje o wersji 3.5 Beta NuGet](../release-notes/nuget-3.5-Beta.md) | [informacje o wersji 3.5 RC NuGet](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="25bcb-105">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="25bcb-106">NuGet 3.5 Beta 2 RTM wydania dla programu Visual Studio 2013 i nuget.exe 27 czerwca 2016 r.</span><span class="sxs-lookup"><span data-stu-id="25bcb-106">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="25bcb-107">Pełny wykaz zmian</span><span class="sxs-lookup"><span data-stu-id="25bcb-107">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="25bcb-108">Lista problemów</span><span class="sxs-lookup"><span data-stu-id="25bcb-108">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="25bcb-109">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="25bcb-109">Bug Fixes</span></span>

* <span data-ttu-id="25bcb-110">Błąd zaktualizowane wiadomości do Brak obsługi decrpytion hasła w .NET Core dla źródeł uwierzytelnionych - [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="25bcb-110">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="25bcb-111">Get-pakiet konsoli Menedżera pakietów nie powiedzie się, jeśli projekt .NET Core jest otwarty — [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="25bcb-111">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="25bcb-112">Usuń nieprawidłowa obsługa 403 w poleceniu wypychania NuGet [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="25bcb-112">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="25bcb-113">Rozwiązywanie problemów w odinstalowanie pakietów w rozwiązaniu powiązany do kontroli źródła TFS, gdy disableSourceControlIntegration jest ustawiona na true - [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="25bcb-113">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="25bcb-114">Napraw pakiet aktualizacji do pakietów niebędące kontem — [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="25bcb-114">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="25bcb-115">Użyj poziom szczegółowości MSBuild, aby ustawić poziom rejestrowania Menedżera pakietów Nuget akcji UI - [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="25bcb-115">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="25bcb-116">Konfiguracja nuget projektu poprawka jest nieprawidłowy błąd w projektach witryny sieci Web - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="25bcb-116">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="25bcb-117">Rozwiązywanie problemów z dodatkiem Service pack z `.csproj` gdy pliki zawartości są uwzględnione - [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="25bcb-117">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="25bcb-118">DefaultPushSource w `NuGetDefaults.Config` (`ProgramData\NuGet`) nie działa — [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="25bcb-118">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="25bcb-119">Rozwiąż problem w wersji Nuget 3.4.3 - wartość nie może być pusty w tworzeniu pakietu - [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="25bcb-119">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="25bcb-120">Przywracanie używa przechowywanych poświadczeń z pliku Nuget.Config dla źródła danych programu VSTS — [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="25bcb-120">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="25bcb-121">Wydajność — poprawka alokacje nadmierne w kodzie porównania wersji — [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="25bcb-121">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="25bcb-122">Rozwiązywanie problemów, gdy wiele wystąpień nuget.exe próbuje zainstalować tego samego pakietu równolegle - [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="25bcb-122">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="25bcb-123">Wydajność — pamięć podręczna informacji o zależnościach wielu projektów operacji - [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="25bcb-123">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="25bcb-124">Rozwiąż problem w przypadku, gdy pakiet źródła można dodać z ustawień, gdy lista źródła jest pusty — [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="25bcb-124">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="25bcb-125">Usuń błąd Misleading, podczas próby zainstalowania pakietu, który jest zależny od czasu projektowania fasad - [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="25bcb-125">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="25bcb-126">Instalowanie pakietu z konsoli PackageManager, ustawienie "All" próbuje tylko pierwsze źródło - [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="25bcb-126">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="25bcb-127">Rozwiązywanie problemów z pakietami, które plików razy zapisu w przyszłości (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="25bcb-127">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="25bcb-128">Wyświetl wyjątku, gdy nastąpiło uszkodzenie projektów znajdowanie polecenia update - [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="25bcb-128">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="25bcb-129">Zawartość pakietu jest nie została poprawnie przywrócona podczas instalowania pakietu z v3.3 nuget + źródła danych z argumentem - NoCache, jeśli pakiet zawiera `.nupkg` pliki - [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="25bcb-129">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="25bcb-130">Usuń problem z pakietem instalacji (wszystkie źródła), gdy źródło 1 - brakuje pakietu [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="25bcb-130">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="25bcb-131">Zainstaluj bloków, jeśli pojedyncze źródło odmawia autoryzacji - [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="25bcb-131">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="25bcb-132">`.nuspec`Wersja zakresu powinny zastępować wersja - IncludeReferencedProjects - [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="25bcb-132">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="25bcb-133">Aktualizacja NuGet 3.3.0 "... dodatkowe ograniczenie zdefiniowane w pliku packages.config uniemożliwia wykonanie tej operacji."</span><span class="sxs-lookup"><span data-stu-id="25bcb-133">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="25bcb-134"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="25bcb-134"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="25bcb-135">Aktualizacja nuget.exe porzuca silna nazwa zestawu i atrybut Private.</span><span class="sxs-lookup"><span data-stu-id="25bcb-135">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="25bcb-136"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="25bcb-136"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="25bcb-137">Rozwiązywanie problemów z względna ścieżka do pliku dla "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="25bcb-137">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="25bcb-138">Poprawy aktualizacji komunikaty o błędach rozpoznawania - [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="25bcb-138">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="25bcb-139">Funkcje i zmiany sposobu działania</span><span class="sxs-lookup"><span data-stu-id="25bcb-139">Features and Behavior Changes</span></span>

* <span data-ttu-id="25bcb-140">nuget.exe push - parametr limitu czasu nie działa — [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="25bcb-140">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="25bcb-141">nie tworzy przywracania nuget.exe `.props` i `.targets` pliki `.nuproj` projektów (Regresja w v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="25bcb-141">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="25bcb-142">Należy rozszerzeń interfejsu API, aby porównać struktury z Importy — [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="25bcb-142">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="25bcb-143">Ukryj opcje zależności, korzystając z `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="25bcb-143">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="25bcb-144">Wydrukować nagłówka wersji nuget.exe w szczegółowych danych wyjściowych - [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="25bcb-144">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="25bcb-145">NuGet należy dodać obsługę /nativeassets/ /runtimes/ {rid} {txm} / - [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="25bcb-145">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>