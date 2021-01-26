---
title: 3,5 beta2 — informacje o wersji
description: Informacje o wersji programu NuGet 3,5 Beta 2, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2aa92d4ef97acb2b4b70388cd4d580e7094aea45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776392"
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="1680b-103">Informacje o wersji narzędzia NuGet 3,5 beta2</span><span class="sxs-lookup"><span data-stu-id="1680b-103">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="1680b-104">[NuGet 3,5 — informacje](../release-notes/nuget-3.5-Beta.md)  |  o wersji beta Pakiet [NuGet 3,5 — informacje o wersji RC](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="1680b-104">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="1680b-105">Pakiet NuGet 3,5 Beta 2 RTM został wydano 27 czerwca 2016 dla Visual Studio 2013 i nuget.exe</span><span class="sxs-lookup"><span data-stu-id="1680b-105">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="1680b-106">Pełny dziennik zmian</span><span class="sxs-lookup"><span data-stu-id="1680b-106">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="1680b-107">Lista problemów</span><span class="sxs-lookup"><span data-stu-id="1680b-107">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="1680b-108">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="1680b-108">Bug Fixes</span></span>

* <span data-ttu-id="1680b-109">Zaktualizowano komunikat o błędzie w celu braku obsługi hasła decrpytion w programie .NET Core dla uwierzytelnionych kanałów informacyjnych — [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="1680b-109">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="1680b-110">Get-Package konsoli Menedżera pakietów kończy się niepowodzeniem, jeśli projekt .NET Core jest otwarty — [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="1680b-110">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="1680b-111">Naprawianie niepoprawnej obsługi 403 w poleceniu wypychania NuGet [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="1680b-111">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="1680b-112">Rozwiązywanie problemów podczas odinstalowywania pakietów w rozwiązaniu związanym z kontrolą źródła TFS, gdy disableSourceControlIntegration jest ustawiona na true — [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="1680b-112">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="1680b-113">Napraw aktualizację pakietu, aby wziąć pod uwagę Pakiety inne niż docelowe — [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="1680b-113">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="1680b-114">Poziom szczegółowości programu MSBuild umożliwia ustawianie poziomu rejestratora dla akcji interfejsu użytkownika Menedżera pakietów NuGet — [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="1680b-114">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="1680b-115">Naprawa konfiguracji NuGet jest nieprawidłowa w projektach witryny sieci Web — VS 2015 VSIX (v 3.4.3) — [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="1680b-115">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="1680b-116">Rozwiązywanie problemów z pakietami z `.csproj` uwzględnieniem plików zawartości — [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="1680b-116">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="1680b-117">DefaultPushSource w `NuGetDefaults.Config` ( `ProgramData\NuGet` ) nie działa — [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="1680b-117">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="1680b-118">Usuwanie problemu w programie NuGet 3.4.3 wersja nie może mieć wartości null podczas tworzenia pakietu- [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="1680b-118">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="1680b-119">Funkcja Restore używa przechowywanych poświadczeń z Nuget.Config dla źródeł danych VSTS — [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="1680b-119">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="1680b-120">Wydajność — napraw nadmierne alokacje w wersji comparsion Code- [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="1680b-120">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="1680b-121">Rozwiązywanie problemów, gdy wiele wystąpień nuget.exe próbuje zainstalować ten sam pakiet w równoległej [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="1680b-121">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="1680b-122">Wydajność — informacje o zależnościach pamięci podręcznej dla operacji wieloprojektowych — [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="1680b-122">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="1680b-123">Rozwiąż problem polegający na tym, że nie można źródła pakietów zostaną dodane z ustawień, gdy lista źródłowa jest pusta — [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="1680b-123">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="1680b-124">Naprawianie błędu mylącego podczas próby zainstalowania pakietu, który zależy od [#2594](https://github.com/NuGet/Home/issues/2594) fasad czasu projektowania</span><span class="sxs-lookup"><span data-stu-id="1680b-124">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="1680b-125">Instalowanie pakietu z konsoli pakietu Packagemanager z ustawieniem "All" powoduje tylko próbę pierwszego źródła — [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="1680b-125">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="1680b-126">Rozwiązywanie problemów z pakietami zawierającymi pliki z godzinami zapisu w przyszłości (mono) — [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="1680b-126">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="1680b-127">Wyświetl wyjątek, jeśli wystąpił błąd podczas znajdowania projektów w ramach polecenia Update — [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="1680b-127">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="1680b-128">Zawartość pakietu nie jest przywracana poprawnie podczas instalowania pakietu z programu NuGet v 3.3 + ze źródła danych argument-nocache, gdy pakiet zawiera `.nupkg` pliki- [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="1680b-128">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="1680b-129">Rozwiązywanie problemu z instalacją pakietu (wszystkie źródła), gdy brakuje pakietu z 1 źródła — [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="1680b-129">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="1680b-130">Zainstaluj bloki w przypadku niepowodzenia autoryzacji pojedynczego źródła — [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="1680b-130">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="1680b-131">`.nuspec` zakres wersji powinien przesłonić IncludeReferencedProjects wersji [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="1680b-131">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="1680b-132">Aktualizacja NuGet 3.3.0 kończy się niepowodzeniem z "dodatkowym ograniczeniem... zdefiniowane w packages.config uniemożliwia wykonanie tej operacji ".</span><span class="sxs-lookup"><span data-stu-id="1680b-132">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="1680b-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="1680b-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="1680b-134">nuget.exe Update odrzuca silną nazwę i atrybut prywatny zestawu.</span><span class="sxs-lookup"><span data-stu-id="1680b-134">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="1680b-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="1680b-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="1680b-136">Rozwiązywanie problemów ze względną ścieżką pliku dla "DefaultPushSource" — [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="1680b-136">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="1680b-137">Optymalizowanie komunikatów o błędach rozwiązywania problemów dotyczących aktualizacji — [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="1680b-137">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="1680b-138">Zmiany funkcji i zachowania</span><span class="sxs-lookup"><span data-stu-id="1680b-138">Features and Behavior Changes</span></span>

* <span data-ttu-id="1680b-139">nuget.exe parametr limitu czasu wypychania nie działa — [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="1680b-139">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="1680b-140">Przywracanie nuget.exe nie produkuje `.props` i `.targets` plików dla `.nuproj` projektów (regresja w v 3.4.3.855) — [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="1680b-140">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="1680b-141">Potrzebny interfejs API rozszerzalności do porównywania platform z importami — [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="1680b-141">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="1680b-142">Ukryj Opcje zależności przy użyciu `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="1680b-142">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="1680b-143">Drukuj nagłówek nuget.exe wersji w szczegółowych danych wyjściowych — [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="1680b-143">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="1680b-144">Pakiet NuGet powinien dodać obsługę/Runtimes/{RID}/nativeassets/{TXM}/- [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="1680b-144">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>