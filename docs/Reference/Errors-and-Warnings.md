---
title: NuGet błędy i ostrzeżenia odwołania
description: Pełną dokumentację dla ostrzeżeń i błędów wystawiony na podstawie NuGet podczas różne operacje NuGet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: anangaur
f1_keywords:
- NU1000
- NU1001
- NU1002
- NU1003
- NU1100
- NU1101
- NU1102
- NU1103
- NU1104
- NU1105
- NU1106
- NU1107
- NU1108
- NU1201
- NU1202
- NU1203
- NU1401
- NU1500
- NU1501
- NU1502
- NU1503
- NU1601
- NU1602
- NU1603
- NU1604
- NU1605
- NU1608
- NU1701
- NU1801
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: dcff20e35adc0a3dbcc7bef482f81a937cf059c5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="3ea3c-103">Błędy i ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="3ea3c-103">Errors and warnings</span></span>

<span data-ttu-id="3ea3c-104">W 4.3.0+ NuGet błędy i ostrzeżenia są numerowane zgodnie z opisem w tym temacie i zawierają szczegółowe informacje pozwalające rozwiązać problemy związane z.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-104">In NuGet 4.3.0+, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span>

<span data-ttu-id="3ea3c-105">Błędy i ostrzeżenia wymienione w tym miejscu są dostępne tylko w przypadku [na podstawie PackageReference](../consume-packages/package-references-in-project-files.md) projektów i NuGet 4.3.0+.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-105">The errors and warnings listed here are available only with [PackageReference-based](../consume-packages/package-references-in-project-files.md) projects and NuGet 4.3.0+.</span></span> <span data-ttu-id="3ea3c-106">NuGet honoruje także właściwości programu MSBuild tłumienie ostrzeżeń lub podniesienie ich poziomu błędy.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-106">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="3ea3c-107">Aby uzyskać więcej informacji, zobacz [porady: pomijanie ostrzeżeń kompilatora](/visualstudio/ide/how-to-suppress-compiler-warnings) w dokumentacji programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-107">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="3ea3c-108">**Błędy**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-108">**Errors**</span></span>

| <span data-ttu-id="3ea3c-109">Grupa</span><span class="sxs-lookup"><span data-stu-id="3ea3c-109">Group</span></span> | <span data-ttu-id="3ea3c-110">Błąd liczby</span><span class="sxs-lookup"><span data-stu-id="3ea3c-110">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="3ea3c-111">Nieprawidłowy błędów na wejściu</span><span class="sxs-lookup"><span data-stu-id="3ea3c-111">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="3ea3c-112">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="3ea3c-112">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="3ea3c-113">Brak błędów pakietu i projektu</span><span class="sxs-lookup"><span data-stu-id="3ea3c-113">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="3ea3c-114">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (wcześniej NU1607) [NU1108](#nu1108) (wcześniej NU1606)</span><span class="sxs-lookup"><span data-stu-id="3ea3c-114">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="3ea3c-115">Błędy zgodności</span><span class="sxs-lookup"><span data-stu-id="3ea3c-115">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="3ea3c-116">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="3ea3c-116">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="3ea3c-117">**Ostrzeżenia**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-117">**Warnings**</span></span>

| <span data-ttu-id="3ea3c-118">Grupa</span><span class="sxs-lookup"><span data-stu-id="3ea3c-118">Group</span></span> | <span data-ttu-id="3ea3c-119">Numery ostrzeżeń</span><span class="sxs-lookup"><span data-stu-id="3ea3c-119">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="3ea3c-120">Nieprawidłowy wejściowy ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="3ea3c-120">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="3ea3c-121">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="3ea3c-121">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="3ea3c-122">Nieoczekiwany pakietu wersji ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="3ea3c-122">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="3ea3c-123">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="3ea3c-123">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="3ea3c-124">Mechanizm rozpoznawania konfliktu ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="3ea3c-124">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="3ea3c-125">NU1608</span><span class="sxs-lookup"><span data-stu-id="3ea3c-125">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="3ea3c-126">Ostrzeżenia rezerwowy pakietu</span><span class="sxs-lookup"><span data-stu-id="3ea3c-126">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="3ea3c-127">NU1701</span><span class="sxs-lookup"><span data-stu-id="3ea3c-127">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="3ea3c-128">Źródła danych ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="3ea3c-128">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="3ea3c-129">NU1801</span><span class="sxs-lookup"><span data-stu-id="3ea3c-129">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="3ea3c-130">NuGet wewnętrzne błędy i ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="3ea3c-130">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="3ea3c-131">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="3ea3c-131">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |
| [<span data-ttu-id="3ea3c-132">Podpisanych pakietów (tworzenia i weryfikacji)</span><span class="sxs-lookup"><span data-stu-id="3ea3c-132">Signed packages (creation and verification)</span></span>](#signed-packages-creation-and-verification)| <span data-ttu-id="3ea3c-133">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="3ea3c-133">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="3ea3c-134">Nieprawidłowy błędów na wejściu</span><span class="sxs-lookup"><span data-stu-id="3ea3c-134">Invalid input errors</span></span>

<span data-ttu-id="3ea3c-135">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="3ea3c-135">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="3ea3c-136">NU1001</span><span class="sxs-lookup"><span data-stu-id="3ea3c-136">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-137">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-137">**Issue**</span></span> | <span data-ttu-id="3ea3c-138">Projekt nie zawiera co najmniej jeden struktury.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-138">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="3ea3c-139">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-139">**Example message**</span></span> | <span data-ttu-id="3ea3c-140">*ProjA projektu nie określa żadnych docelowych platform w c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-140">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |
| <span data-ttu-id="3ea3c-141">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-141">**Solution**</span></span> | <span data-ttu-id="3ea3c-142">Dodaj `TargetFramework` lub `TargetFrameworks` właściwości do pliku określonego projektu.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-142">Add a `TargetFramework` or `TargetFrameworks` property to the specified project file.</span></span> |

### <a name="nu1002"></a><span data-ttu-id="3ea3c-143">NU1002</span><span class="sxs-lookup"><span data-stu-id="3ea3c-143">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-144">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-144">**Issue**</span></span> | <span data-ttu-id="3ea3c-145">Nieprawidłowa kombinacja danych wejściowych oraz wyczyść — słowo kluczowe.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-145">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="3ea3c-146">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-146">**Example message**</span></span> | <span data-ttu-id="3ea3c-147">*"CLEAR" nie można używać w połączeniu z innymi wartości*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-147">*'CLEAR' cannot be used in conjunction with other values*</span></span> |
| <span data-ttu-id="3ea3c-148">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-148">**Solution**</span></span> | <span data-ttu-id="3ea3c-149">Użyj wyczyść samodzielnie i pominąć wszystkie inne dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-149">Use CLEAR by itself and omit all other inputs.</span></span> |

### <a name="nu1003"></a><span data-ttu-id="3ea3c-150">NU1003</span><span class="sxs-lookup"><span data-stu-id="3ea3c-150">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-151">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-151">**Issue**</span></span> | <span data-ttu-id="3ea3c-152">`PackageTargetFallback` i `AssetTargetFallback` Podaj inaczej wybierania zasobów i nie mogą być używane razem.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-152">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="3ea3c-153">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-153">**Example message**</span></span> | <span data-ttu-id="3ea3c-154">*PackageTargetFallback i AssetTargetFallback nie mogą być używane razem. Usuń odwołania PackageTargetFallback(deprecated) ze środowiska projektu.*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-154">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |
| <span data-ttu-id="3ea3c-155">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-155">**Solution**</span></span> | <span data-ttu-id="3ea3c-156">Usuń przestarzałe `PackageTargetFallback` elementu z projektu.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-156">Remove the deprecated `PackageTargetFallback` element from the project.</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="3ea3c-157">Brak błędów pakietu i projektu</span><span class="sxs-lookup"><span data-stu-id="3ea3c-157">Missing package and project errors</span></span>

<span data-ttu-id="3ea3c-158">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="3ea3c-158">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="3ea3c-159">NU1100</span><span class="sxs-lookup"><span data-stu-id="3ea3c-159">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-160">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-160">**Issue**</span></span> | <span data-ttu-id="3ea3c-161">Grupa zależności nie można rozpoznać.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-161">A dependency group not be resolved.</span></span> <span data-ttu-id="3ea3c-162">Jest to problem rodzajowy dla typów, które nie są pakiety lub projektów.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-162">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="3ea3c-163">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-163">**Example message**</span></span> | <span data-ttu-id="3ea3c-164">*Nie można rozpoznać System.Missing dla net45*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-164">*Unable to resolve System.Missing for net45*</span></span> |
| <span data-ttu-id="3ea3c-165">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-165">**Solution**</span></span> | <span data-ttu-id="3ea3c-166">Otwórz plik projektu i sprawdź, czy lista jego zależności.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-166">Open the project file and examine the list of its dependencies.</span></span> <span data-ttu-id="3ea3c-167">Sprawdź, czy poszczególne zależności istnieje na źródła pakietów, którego używasz, i że pakiet obsługuje platforma docelowa projektu.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-167">Check that each dependency exists on the package sources you're using, and that the package supports the project's target framework.</span></span> |

### <a name="nu1101"></a><span data-ttu-id="3ea3c-168">NU1101</span><span class="sxs-lookup"><span data-stu-id="3ea3c-168">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-169">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-169">**Issue**</span></span> | <span data-ttu-id="3ea3c-170">Nie można odnaleźć pakietu na wszystkich źródeł.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-170">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="3ea3c-171">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-171">**Example message**</span></span> | <span data-ttu-id="3ea3c-172">*Nie można odnaleźć pakietu System.Missing. Żadne pakiety nie istnieje z tym identyfikatorem w źródłach: dotnet core, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |
| <span data-ttu-id="3ea3c-173">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-173">**Solution**</span></span> | <span data-ttu-id="3ea3c-174">Sprawdź, czy zależności projektu w programie Visual Studio należy upewnić się, że używasz pakietu poprawny identyfikator i numer wersji.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-174">Examine the project's dependencies in Visual Studio to be sure you're using the correct package identifier and version number.</span></span> <span data-ttu-id="3ea3c-175">Sprawdź także, czy [Konfiguracja nuget projektu](../consume-packages/Configuring-NuGet-Behavior.md) identyfikuje źródła pakietów w sieci spodziewać się przy użyciu.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-175">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="3ea3c-176">Jeśli używasz pakiety, które mają [Wersjonowania semantycznego 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), upewnij się, że używasz [V3 źródła](https://api.nuget.org/v3/index.json) w [Konfiguracja nuget projektu](../consume-packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="3ea3c-176">If you use packages that have [Semantic Versioning 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), please make sure that you are using the [V3 feed](https://api.nuget.org/v3/index.json) in the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> |

### <a name="nu1102"></a><span data-ttu-id="3ea3c-177">NU1102</span><span class="sxs-lookup"><span data-stu-id="3ea3c-177">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-178">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-178">**Issue**</span></span> | <span data-ttu-id="3ea3c-179">Identyfikator pakietu został znaleziony, lecz nie można odnaleźć wersji w zakresie określonym zależności na żadnym z źródeł.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-179">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> <span data-ttu-id="3ea3c-180">Pakiet, a użytkownik nie może być określony zakres.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-180">The range might be specified by a package and not the user.</span></span> |
| <span data-ttu-id="3ea3c-181">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-181">**Example message**</span></span> | <span data-ttu-id="3ea3c-182">*Nie można odnaleźć pakietu NuGet.Versioning z wersją (> = 9.0.1)<br/> — wersje 30 znalezione w usłudze nuget.org [najbliższej wersji: 4.0.0]<br/> — wersje znaleziono 10 w dotnet buildtools [najbliższej wersji: 4.0.0-rc-2129]<br/> -znaleziono 9 wersje w NuGetVolatile [najbliższej wersji: 3.0.0-beta-00032]<br/> -znaleziono wersje 0 w podstawowej platformy dotnet<br/> -znaleziono wersje 0 w dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-182">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="3ea3c-183">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-183">**Solution**</span></span> | <span data-ttu-id="3ea3c-184">Edytuj plik projektu, aby poprawić wersji pakietu.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-184">Edit the project file to correct the package version.</span></span> <span data-ttu-id="3ea3c-185">Sprawdź także, czy [Konfiguracja nuget projektu](../consume-packages/Configuring-NuGet-Behavior.md) identyfikuje źródła pakietów w sieci spodziewać się przy użyciu.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-185">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="3ea3c-186">Konieczne może być zmiana wersji requeted, jeśli ten pakiet jest bezpośrednio wywoływany przez projekt.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-186">You may need to change the requeted version if this package is referenced by the project directly.</span></span> |

### <a name="nu1103"></a><span data-ttu-id="3ea3c-187">NU1103</span><span class="sxs-lookup"><span data-stu-id="3ea3c-187">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-188">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-188">**Issue**</span></span> | <span data-ttu-id="3ea3c-189">Projekt określony stabilną wersję dla zakresu zależności, ale w zakresie nie znaleziono żadnych wersji stabilnej.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-189">The project specified a stable version for the dependency range, but no stable versions were found in that range.</span></span> <span data-ttu-id="3ea3c-190">Wersje wstępne znaleziono, ale nie są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-190">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="3ea3c-191">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-191">**Example message**</span></span> | <span data-ttu-id="3ea3c-192">*Nie można odnaleźć pakietu stabilna NuGet.Versioning z wersją (> = 3.0.0)<br/> — wersje znaleziono 10 w dotnet buildtools [najbliższej wersji: 4.0.0-rc-2129]<br/> -znaleziono 9 wersje w NuGetVolatile [najbliższej wersji: 3.0.0-beta-00032] <br/> -Znaleziono wersje 0 w podstawowej platformy dotnet<br/> -znaleziono wersje 0 w dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-192">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="3ea3c-193">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-193">**Solution**</span></span> |  <span data-ttu-id="3ea3c-194">Edytuj zakres wersji w pliku projektu, aby uwzględnić wersje wstępne.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-194">Edit the version range in the project file to include pre-release versions.</span></span> <span data-ttu-id="3ea3c-195">Zobacz [wersji pakietu](../reference/Package-Versioning.md).</span><span class="sxs-lookup"><span data-stu-id="3ea3c-195">See [Package versioning](../reference/Package-Versioning.md).</span></span> |

### <a name="nu1104"></a><span data-ttu-id="3ea3c-196">NU1104</span><span class="sxs-lookup"><span data-stu-id="3ea3c-196">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-197">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-197">**Issue**</span></span> | <span data-ttu-id="3ea3c-198">Wskazuje element ProjectReference do pliku, który nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-198">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="3ea3c-199">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-199">**Example message**</span></span> | <span data-ttu-id="3ea3c-200">*Odwołanie do projektu nie istnieje "c:\a.csproj". Sprawdź, czy odwołanie do projektu jest prawidłowa i czy istnieje plik projektu.*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-200">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |
| <span data-ttu-id="3ea3c-201">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-201">**Solution**</span></span> | <span data-ttu-id="3ea3c-202">Edytuj plik projektu albo poprawną ścieżkę do przywoływanego projektu lub Usuń odwołanie całkowicie, jeśli nie jest już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-202">Edit the project file to either correct the path to the referenced project or to remove the reference altogether if it's no longer needed.</span></span> |

### <a name="nu1105"></a><span data-ttu-id="3ea3c-203">NU1105</span><span class="sxs-lookup"><span data-stu-id="3ea3c-203">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-204">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-204">**Issue**</span></span> | <span data-ttu-id="3ea3c-205">Plik projektu istnieje, ale go nie dostarczono żadnych informacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-205">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="3ea3c-206">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-206">**Example message**</span></span> | <span data-ttu-id="3ea3c-207">*Nie można odczytać informacji o projekcie dla "c:\a.csproj". Plik projektu może być nieprawidłowe lub brakujące elementy docelowe, wymaganych do przywrócenia.*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-207">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="3ea3c-208">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-208">**Solution**</span></span> | <span data-ttu-id="3ea3c-209">W programie Visual Studio błąd może oznaczać, że projekt jest zwolniony, w którym to przypadku ponownie Załaduj projekt.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-209">In Visual Studio, the error could mean that the project is unloaded, in which case reload the project.</span></span> <span data-ttu-id="3ea3c-210">W wierszu polecenia może to oznaczać, że plik jest uszkodzony lub nie zawiera niestandardowego "po imports" potrzebne do odzyskiwania do odczytu do projektu docelowego.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-210">From the command line this could mean that the file is corrupt or that it doesn't contain the custom "after imports" target needed for restore to read the project.</span></span> <span data-ttu-id="3ea3c-211">Sprawdź, czy plik projektu jest prawidłowa i czy zawiera element docelowy "po imports".</span><span class="sxs-lookup"><span data-stu-id="3ea3c-211">Check that the project file is valid and contains an "after imports" target.</span></span> |

### <a name="nu1106"></a><span data-ttu-id="3ea3c-212">NU1106</span><span class="sxs-lookup"><span data-stu-id="3ea3c-212">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-213">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-213">**Issue**</span></span> | <span data-ttu-id="3ea3c-214">Nie można rozpoznać zależności ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-214">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="3ea3c-215">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-215">**Example message**</span></span> | <span data-ttu-id="3ea3c-216">*Nie można zrealizować żądań będących w konflikcie dla {id}: {konflikt path} Framework: {docelowy wykres}*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-216">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |
| <span data-ttu-id="3ea3c-217">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-217">**Solution**</span></span> | <span data-ttu-id="3ea3c-218">Edytuj plik projektu, aby określić bardziej uniwersalnym zakresy dla zależności, a nie dokładnej wersji.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-218">Edit the project file to specify more open-ended ranges for the dependency rather than an exact version.</span></span> |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="3ea3c-219">NU1107 (wcześniej NU1607)</span><span class="sxs-lookup"><span data-stu-id="3ea3c-219">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-220">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-220">**Issue**</span></span> | <span data-ttu-id="3ea3c-221">Nie można rozpoznać ograniczenia zależności między pakietami.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-221">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="3ea3c-222">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-222">**Example message**</span></span> | <span data-ttu-id="3ea3c-223">*Konflikt wersji dla NuGet.Versioning wykryte. Pakiet odwoływać się bezpośrednio z projektu, aby rozwiązać ten problem.<br/>  NuGet.Versioning (= 3.5.0) -> NuGet.Packaging 3.5.0<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-223">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |
| <span data-ttu-id="3ea3c-224">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-224">**Solution**</span></span> | <span data-ttu-id="3ea3c-225">Pakiety z ograniczeniami zależności na dokładną wersję nie zezwalają na inne pakiety w razie potrzeby zwiększyć wersji.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-225">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> <span data-ttu-id="3ea3c-226">Dodaj odwołanie do projektu bezpośrednio (w pliku projektu) na dokładną wersję wymaganą.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-226">Add a reference to the project directly (in the project file) with the exact version required.</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="3ea3c-227">NU1108 (wcześniej NU1606)</span><span class="sxs-lookup"><span data-stu-id="3ea3c-227">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-228">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-228">**Issue**</span></span> | <span data-ttu-id="3ea3c-229">Wykryto zależność cykliczną.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-229">A circular dependency was detected.</span></span> |
| <span data-ttu-id="3ea3c-230">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-230">**Example message**</span></span> | <span data-ttu-id="3ea3c-231">*Wykryto cykl: A -> B -> A*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-231">*Cycle detected: A -> B -> A*</span></span> |
| <span data-ttu-id="3ea3c-232">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-232">**Solution**</span></span> | <span data-ttu-id="3ea3c-233">Pakiet jest w pełni autoryzowane; Skontaktuj się z właścicielem pakietu, aby naprawić ten błąd.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-233">The package is authored incorrectly; contact the package owner to correct the bug.</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="3ea3c-234">Błędy zgodności</span><span class="sxs-lookup"><span data-stu-id="3ea3c-234">Compatibility errors</span></span>

<span data-ttu-id="3ea3c-235">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="3ea3c-235">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="3ea3c-236">NU1201</span><span class="sxs-lookup"><span data-stu-id="3ea3c-236">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-237">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-237">**Issue**</span></span> | <span data-ttu-id="3ea3c-238">Zależności projektu nie zawiera struktury zgodne z bieżącego projektu.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-238">A dependency project doesn't contain a framework compatible with the current project.</span></span> <span data-ttu-id="3ea3c-239">Zazwyczaj platformę docelową projektu jest wyższą wersję niż odbierającą projektu.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-239">Typically, the project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="3ea3c-240">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-240">**Example message**</span></span> | <span data-ttu-id="3ea3c-241">*ServerWeb projektu nie jest zgodny z netstandard1.3 (. Krótkich nazw NETStandard, Version = w wersji 1.3). Projekt obsługuje ServerWeb:<br/> -netstandard1.6 (. Krótkich nazw NETStandard, Version = w wersji 1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = 1.0)*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-241">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |
| <span data-ttu-id="3ea3c-242">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-242">**Solution**</span></span> | <span data-ttu-id="3ea3c-243">Zmień platformę docelową projektu na wersję równa lub mniejsza niż odbierającą projektu.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-243">Change the project's target framework to an equal or lower version than the consuming project.</span></span> |

### <a name="nu1202"></a><span data-ttu-id="3ea3c-244">NU1202</span><span class="sxs-lookup"><span data-stu-id="3ea3c-244">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-245">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-245">**Issue**</span></span> | <span data-ttu-id="3ea3c-246">Pakiet zależności nie zawiera żadnych zasobów, które są zgodne z projektem.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-246">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="3ea3c-247">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-247">**Example message**</span></span> | <span data-ttu-id="3ea3c-248">*Pakiet System.ComponentModel.EventBasedAsync 4.0.11 nie jest zgodny z netstandard1.3 (. Krótkich nazw NETStandard, Version = w wersji 1.3). Pakiet obsługuje System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, wersja = 1.0)<br/> -monotouch10 (MonoTouch, wersja = 1.0)<br/> -net45 (. NETFramework, Version = 4.5)<br/> -netcore50 (. NETCore, Version = v5.0)<br/> -netstandard1.0 (. Krótkich nazw NETStandard, Version = 1.0)<br/> -przenośny net45 + win8 + wp8 + wpa81 (. NETPortable, wersja = v0.0, profil = Profile259)<br/> — Windows 8 (Windows, wersja = w wersji 8.0)<br/> -wp8 (WindowsPhone, wersja = w wersji 8.0)<br/> -wpa81 (WindowsPhoneApp, wersja = v8.1)<br/> — xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-248">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|
| <span data-ttu-id="3ea3c-249">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-249">**Solution**</span></span> | <span data-ttu-id="3ea3c-250">Zmień platformę docelową projektu na taki, który obsługuje pakietu.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-250">Change the project's target framework to one that the package supports.</span></span> |

### <a name="nu1203"></a><span data-ttu-id="3ea3c-251">NU1203</span><span class="sxs-lookup"><span data-stu-id="3ea3c-251">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-252">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-252">**Issue**</span></span> | <span data-ttu-id="3ea3c-253">Pakiet nie obsługuje projektu `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-253">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="3ea3c-254">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-254">**Example message**</span></span> | <span data-ttu-id="3ea3c-255">*System.Example 1.0.0 udostępnia zestaw odwołania czasu kompilowania dla a.dll na net461, ale nie nie zgodny zestaw czasu wykonywania.*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-255">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |
| <span data-ttu-id="3ea3c-256">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-256">**Solution**</span></span> | <span data-ttu-id="3ea3c-257">Zmień `RuntimeIdentifier` wartości użyte w projekcie, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-257">Change the `RuntimeIdentifier` values used in the project as needed.</span></span> |

### <a name="nu1401"></a><span data-ttu-id="3ea3c-258">NU1401</span><span class="sxs-lookup"><span data-stu-id="3ea3c-258">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-259">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-259">**Issue**</span></span> | <span data-ttu-id="3ea3c-260">Pakiet wymaga funkcji lub struktur nie są obecnie obsługiwane przez zainstalowaną wersję programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-260">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="3ea3c-261">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-261">**Example message**</span></span> | <span data-ttu-id="3ea3c-262">*Pakiet "NuGet.Versioning" wymaga wersji klienta "5.0.0" NuGet lub nowszej, ale bieżąca wersja NuGet to "4.3.0".*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-262">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'.*</span></span> |
| <span data-ttu-id="3ea3c-263">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-263">**Solution**</span></span> | <span data-ttu-id="3ea3c-264">Zainstaluj nowszą wersję programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-264">Install a newer version of NuGet.</span></span> <span data-ttu-id="3ea3c-265">Zobacz [narzędzia klienta instalowania NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="3ea3c-265">See [Installing NuGet client tools](../install-nuget-client-tools.md).</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="3ea3c-266">Nieprawidłowy wejściowy ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="3ea3c-266">Invalid input warnings</span></span>

<span data-ttu-id="3ea3c-267">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="3ea3c-267">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="3ea3c-268">NU1501</span><span class="sxs-lookup"><span data-stu-id="3ea3c-268">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-269">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-269">**Issue**</span></span> | <span data-ttu-id="3ea3c-270">Przywracanie projektu próbuje działać na nie został znaleziony.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-270">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="3ea3c-271">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-271">**Example message**</span></span> | <span data-ttu-id="3ea3c-272">*Folder "c:\projects\a" nie zawiera projektu do przywrócenia.*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-272">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |
| <span data-ttu-id="3ea3c-273">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-273">**Solution**</span></span> | <span data-ttu-id="3ea3c-274">Uruchamianie przywracania nuget w folderze, który zawiera projekt.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-274">Run nuget restore in a folder that contains a project.</span></span> |

### <a name="nu1502"></a><span data-ttu-id="3ea3c-275">NU1502</span><span class="sxs-lookup"><span data-stu-id="3ea3c-275">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-276">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-276">**Issue**</span></span> | <span data-ttu-id="3ea3c-277">`RuntimeSupports` zawiera nieprawidłowy profil.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-277">`RuntimeSupports` contains an invalid profile.</span></span> <span data-ttu-id="3ea3c-278">Zazwyczaj obsługuje profil nie został znaleziony w `runtime.json` plik z bieżącego zależności pakietów.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-278">Typically, the supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span>|
| <span data-ttu-id="3ea3c-279">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-279">**Example message**</span></span> | <span data-ttu-id="3ea3c-280">*Profil zgodności nieznany: aaa*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-280">*Unknown Compatibility Profile: aaa*</span></span> |
| <span data-ttu-id="3ea3c-281">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-281">**Solution**</span></span> | <span data-ttu-id="3ea3c-282">Sprawdź `RuntimeSupports` wartość w projekcie.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-282">Check the `RuntimeSupports` value in your project.</span></span> |

### <a name="nu1503"></a><span data-ttu-id="3ea3c-283">NU1503</span><span class="sxs-lookup"><span data-stu-id="3ea3c-283">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-284">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-284">**Issue**</span></span> | <span data-ttu-id="3ea3c-285">Zależności projektu nie importuje obiekty docelowe przywracania NuGet.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-285">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="3ea3c-286">Ten jest podobny do NU1105, ale w tym miejscu projektu zostanie pominięty i zignorowany zamiast powoduje wszystkie przywracania się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-286">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="3ea3c-287">W złożonych rozwiązań są często innych typów projektów, które mogą nie obsługiwać przywracania.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-287">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="3ea3c-288">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-288">**Example message**</span></span> | <span data-ttu-id="3ea3c-289">*Pomijanie przywracania dla projektu "c:\a.csproj". Plik projektu może być nieprawidłowe lub brakujące elementy docelowe, wymaganych do przywrócenia.*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-289">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="3ea3c-290">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-290">**Solution**</span></span> | <span data-ttu-id="3ea3c-291">Może to nastąpić dla projektów, które nie należy importować wspólne właściwości/cele, które są automatycznie importowane przywracania.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-291">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="3ea3c-292">Jeśli projekt nie trzeba przywrócić możesz go zignorować.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-292">If the project doesn't need to be restored this can be ignored.</span></span> <span data-ttu-id="3ea3c-293">W przeciwnym razie edytować dotyczy projektu, aby dodać elementy docelowe przywracania.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-293">Otherwise, edit the affected project to add targets for restore.</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="3ea3c-294">Nieoczekiwany pakietu wersji ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="3ea3c-294">Unexpected package version warnings</span></span>

<span data-ttu-id="3ea3c-295">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="3ea3c-295">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="3ea3c-296">NU1601</span><span class="sxs-lookup"><span data-stu-id="3ea3c-296">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-297">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-297">**Issue**</span></span> | <span data-ttu-id="3ea3c-298">Zależności bezpośrednich projektu był upadku na wyższą wersję niż określonego projektu.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-298">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="3ea3c-299">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-299">**Example message**</span></span> | <span data-ttu-id="3ea3c-300">*Określoną zależnością było NuGet.Versioning (> = 3.5.0), ale ostatecznie otrzymano NuGet.Versioning 4.0.0.*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-300">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |
| <span data-ttu-id="3ea3c-301">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-301">**Solution**</span></span> | <span data-ttu-id="3ea3c-302">Zaktualizuj zależności w projekcie do odpowiedniej wersji.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-302">Update the dependency in the project to an appropriate version.</span></span> |

### <a name="nu1602"></a><span data-ttu-id="3ea3c-303">NU1602</span><span class="sxs-lookup"><span data-stu-id="3ea3c-303">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-304">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-304">**Issue**</span></span> | <span data-ttu-id="3ea3c-305">Zależność pakietu brak dolnej granicy.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-305">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="3ea3c-306">To nie zezwala na przywracania znaleźć *najlepszego dopasowania*.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-306">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="3ea3c-307">Każdy przywracania będzie przestawiany dół próby znalezienia starszej wersji, który może być używany.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-307">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="3ea3c-308">Oznacza to, że przywracanie przejdzie do trybu online, aby sprawdzić wszystkie źródła zawsze zamiast pakietów, które już istnieją w folderze pakietów użytkowników.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-308">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="3ea3c-309">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-309">**Example message**</span></span> | <span data-ttu-id="3ea3c-310">*NuGet.Packaging 4.0.0 nie zapewnia włącznie dolna granica dla zależności NuGet.Versioning (> 3.5.0). Przybliżony najlepsze dopasowanie 3.6.0 został rozwiązany.*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-310">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |
| <span data-ttu-id="3ea3c-311">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-311">**Solution**</span></span> | <span data-ttu-id="3ea3c-312">Jest to zazwyczaj błąd tworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-312">This is usually a package authoring error.</span></span> <span data-ttu-id="3ea3c-313">Skontaktuj się z autorem pakietu, aby rozwiązać ten problem.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-313">Contact the package author to resolve the issue.</span></span> |

### <a name="nu1603"></a><span data-ttu-id="3ea3c-314">NU1603</span><span class="sxs-lookup"><span data-stu-id="3ea3c-314">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-315">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-315">**Issue**</span></span> | <span data-ttu-id="3ea3c-316">Zależność pakietu określonej wersji, którego nie można odnaleźć.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-316">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="3ea3c-317">Zazwyczaj źródła pakietu nie zawierają wersja oczekiwana dolnej granicy.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-317">Typically, the package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="3ea3c-318">Nowsza wersja użyto zamiast tego, który różni się od pakietu opracowania przed.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-318">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="3ea3c-319">Oznacza to, że przywracanie nie znalazł *najlepszego dopasowania*.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-319">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="3ea3c-320">Każdy przywracania będzie przestawiany dół próby znalezienia starszej wersji, który może być używany.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-320">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="3ea3c-321">Oznacza to, że przywracanie przejdzie do trybu online, aby sprawdzić wszystkie źródła zawsze zamiast pakietów, które już istnieją w folderze pakietów użytkowników.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-321">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="3ea3c-322">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-322">**Example message**</span></span> | <span data-ttu-id="3ea3c-323">NuGet.Packaging 4.0.0 zależy od NuGet.Versioning (> = 4.0.0), ale nie można odnaleźć 4.0.0.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-323">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="3ea3c-324">Przybliżony najlepsze dopasowanie 5.0.0 został rozwiązany.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-324">An approximate best match of 5.0.0 was resolved.</span></span> |
| <span data-ttu-id="3ea3c-325">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-325">**Solution**</span></span> | <span data-ttu-id="3ea3c-326">Jeśli nie zostało zwolnione pakietu oczekiwano może to być błąd tworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-326">If the package expected has not been released then this may be a package authoring error.</span></span> <span data-ttu-id="3ea3c-327">Skontaktuj się z autorem pakietu, aby rozwiązać ten problem.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-327">Contact the package author to resolve the issue.</span></span> <span data-ttu-id="3ea3c-328">Jeśli pakiet został zwolniony, sprawdź, czy plik jest dostępny na źródła pakietów, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-328">If the package has been released, then check that it's available on the package sources you're using.</span></span> <span data-ttu-id="3ea3c-329">Jeśli przy użyciu prywatnych źródła, może być konieczne zaktualizowanie pakietu w tego źródła.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-329">If using a private source, you may need to update the package on that feed.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="3ea3c-330">NU1604</span><span class="sxs-lookup"><span data-stu-id="3ea3c-330">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-331">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-331">**Issue**</span></span> | <span data-ttu-id="3ea3c-332">Zależności projektu nie definiuje dolną granicą.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-332">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="3ea3c-333">Oznacza to, że przywracanie nie znalazł *najlepszego dopasowania*.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-333">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="3ea3c-334">Każdy przywracania będzie przestawiany dół próby znalezienia starszej wersji, który może być używany.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-334">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="3ea3c-335">Oznacza to, że przywracanie przejdzie do trybu online, aby sprawdzić wszystkie źródła zawsze zamiast pakietów, które już istnieją w folderze pakietów użytkowników.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-335">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="3ea3c-336">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-336">**Example message**</span></span> | <span data-ttu-id="3ea3c-337">*Projekt zależności NuGet.Versioning (< = od 9.0.0) Nowak zawiera włącznie dolnej granicy. Dolna granica należy uwzględnić w wersji zależności, aby zapewnić wyniki przywracania na poziomie.*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-337">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |
| <span data-ttu-id="3ea3c-338">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-338">**Solution**</span></span> | <span data-ttu-id="3ea3c-339">Aktualizowanie projektu `PackageReference` `Version` atrybutu uwzględnienie dolną granicą.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-339">Update the project's `PackageReference` `Version` attribute to include a lower bound.</span></span> |

### <a name="nu1605"></a><span data-ttu-id="3ea3c-340">NU1605</span><span class="sxs-lookup"><span data-stu-id="3ea3c-340">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-341">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-341">**Issue**</span></span> | <span data-ttu-id="3ea3c-342">Pakiet zależności określić ograniczenia wersji za pomocą nowszej wersji pakietu niż przywracania ostatecznie rozwiązane.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-342">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> <span data-ttu-id="3ea3c-343">Oznacza to z powodu "najbliższej wins" reguła podczas rozpoznawania pakietów, bliżej położonego pakietu na wykresie mogą mieć zastąpione odległymi pakiet.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-343">That is, because of the "nearest wins" rule when resolving packages, a nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="3ea3c-344">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-344">**Example message**</span></span> | <span data-ttu-id="3ea3c-345">*Wykryto starszą wersję pakietu: NuGet.Versioning z 4.0.0 do 3.5.0. Odwoływać się bezpośrednio z projektu, aby wybrać inną wersję pakietu.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-345">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |
| <span data-ttu-id="3ea3c-346">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-346">**Solution**</span></span> | <span data-ttu-id="3ea3c-347">Dodaj bezpośrednie odwołanie do projektu do nowszej wersji pakietu, który ma być używany.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-347">Add a direct reference to the project for the higher version of the package that you want to use.</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="3ea3c-348">Mechanizm rozpoznawania konfliktu ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="3ea3c-348">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="3ea3c-349">NU1608</span><span class="sxs-lookup"><span data-stu-id="3ea3c-349">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-350">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-350">**Issue**</span></span> | <span data-ttu-id="3ea3c-351">Rozwiązany pakietu jest większa niż umożliwia ograniczenie zależności.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-351">A resolved package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="3ea3c-352">Oznacza to, że pakiet bezpośrednio odwołuje się projekt zastępuje ograniczenia zależności z innymi pakietami.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-352">This means that a package referenced directly by a project overrides dependency constraints from other packages.</span></span>|
| <span data-ttu-id="3ea3c-353">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-353">**Example message**</span></span> | <span data-ttu-id="3ea3c-354">*Wersja pakietu wykrytych poza ograniczenia zależności: x 1.0.0 wymaga y (= 1.0.0), ale wersja y 2.0.0 został rozwiązany.*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-354">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |
| <span data-ttu-id="3ea3c-355">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-355">**Solution**</span></span> | <span data-ttu-id="3ea3c-356">W niektórych przypadkach jest to zamierzone i można pominąć to ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-356">In some cases this is intentional and the warning can be suppressed.</span></span> <span data-ttu-id="3ea3c-357">W przeciwnym razie Zmień odwołanie projektu do pakietu, aby zwiększyć swoje ograniczenia wersji.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-357">Otherwise, change the project's reference to the package to widen its version constraints.</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="3ea3c-358">Ostrzeżenia rezerwowy pakietu</span><span class="sxs-lookup"><span data-stu-id="3ea3c-358">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="3ea3c-359">NU1701</span><span class="sxs-lookup"><span data-stu-id="3ea3c-359">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-360">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-360">**Issue**</span></span> | <span data-ttu-id="3ea3c-361">`PackageTargetFallback` / `AssetTargetFallback` użyto Wybierz zasoby z pakietem.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-361">`PackageTargetFallback` / `AssetTargetFallback` was used to select assets from a package.</span></span> <span data-ttu-id="3ea3c-362">Ostrzeżenie powiadomić użytkowników, że zasoby nie mogą być 100% zgodny.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-362">The warning let users know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="3ea3c-363">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-363">**Example message**</span></span> | <span data-ttu-id="3ea3c-364">*Pakiet "NuGet.Versioning" został przywrócony przy użyciu "portable net45 + win8" zamiast platformy docelowej projektu "netstandard1.5". Ten pakiet nie może być całkowicie zgodne z projektem.*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-364">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |
| <span data-ttu-id="3ea3c-365">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-365">**Solution**</span></span> | <span data-ttu-id="3ea3c-366">Zmień platformę docelową projektu na taki, który obsługuje pakietu.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-366">Change the project's target framework to one that the package supports.</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="3ea3c-367">Źródła danych ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="3ea3c-367">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="3ea3c-368">NU1801</span><span class="sxs-lookup"><span data-stu-id="3ea3c-368">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-369">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-369">**Issue**</span></span> | <span data-ttu-id="3ea3c-370">Wystąpił błąd podczas odczytywania źródła po `IgnoreFailedSources` jest ustawiona na wartość true, konwersją niekrytyczny ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-370">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="3ea3c-371">To może zawierać żadnych komunikatów i jest rodzajowy.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-371">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="3ea3c-372">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-372">**Example message**</span></span> | <span data-ttu-id="3ea3c-373">n/d</span><span class="sxs-lookup"><span data-stu-id="3ea3c-373">n/a</span></span> |
| <span data-ttu-id="3ea3c-374">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-374">**Solution**</span></span> | <span data-ttu-id="3ea3c-375">Edytuj konfigurację, aby określić prawidłową źródła.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-375">Edit your configuration to specify valid sources.</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="3ea3c-376">NuGet wewnętrzne błędy i ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="3ea3c-376">NuGet internal errors and warnings</span></span>

<span data-ttu-id="3ea3c-377">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="3ea3c-377">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="3ea3c-378">NU1000</span><span class="sxs-lookup"><span data-stu-id="3ea3c-378">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-379">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-379">**Issue**</span></span> | <span data-ttu-id="3ea3c-380">Nieokreślony błąd wewnętrzny z pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-380">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="3ea3c-381">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-381">**Solution**</span></span> | <span data-ttu-id="3ea3c-382">Sprawdź dzienniki, aby uzyskać więcej informacji</span><span class="sxs-lookup"><span data-stu-id="3ea3c-382">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="3ea3c-383">NU1500</span><span class="sxs-lookup"><span data-stu-id="3ea3c-383">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-384">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-384">**Issue**</span></span> | <span data-ttu-id="3ea3c-385">Nieokreślony ostrzeżenie wewnętrzny z pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-385">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="3ea3c-386">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-386">**Solution**</span></span> | <span data-ttu-id="3ea3c-387">Sprawdź dzienniki, aby uzyskać więcej informacji</span><span class="sxs-lookup"><span data-stu-id="3ea3c-387">Check the logs for more information</span></span> |

## <a name="signed-packages-creation-and-verification"></a><span data-ttu-id="3ea3c-388">Podpisanych pakietów (tworzenia i weryfikacji)</span><span class="sxs-lookup"><span data-stu-id="3ea3c-388">Signed packages (creation and verification)</span></span>

<span data-ttu-id="3ea3c-389">*NuGet 4.6.0+*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-389">*NuGet 4.6.0+*</span></span>

<span data-ttu-id="3ea3c-390">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="3ea3c-390">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span></span>

### <a name="nu3000"></a><span data-ttu-id="3ea3c-391">NU3000</span><span class="sxs-lookup"><span data-stu-id="3ea3c-391">NU3000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-392">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-392">**Issue**</span></span> | <span data-ttu-id="3ea3c-393">Ogólny błąd odnoszące się do podpisywania pakietu i podpisany weryfikacji pakietu.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-393">A non-specific error related to package signing and signed package verification.</span></span> |
| <span data-ttu-id="3ea3c-394">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-394">**Solution**</span></span> | <span data-ttu-id="3ea3c-395">Sprawdź dzienniki, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-395">Check the logs for more information.</span></span> |

### <a name="nu3001"></a><span data-ttu-id="3ea3c-396">NU3001</span><span class="sxs-lookup"><span data-stu-id="3ea3c-396">NU3001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-397">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-397">**Issue**</span></span> | <span data-ttu-id="3ea3c-398">Nieprawidłowe argumenty albo [zarejestrować polecenia](../tools/cli-ref-sign.md) lub [Sprawdź polecenie](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="3ea3c-398">Invalid arguments to either the [sign command](../tools/cli-ref-sign.md) or the [verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="3ea3c-399">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-399">**Solution**</span></span> | <span data-ttu-id="3ea3c-400">Sprawdź i popraw na podstawie podanych argumentów.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-400">Check and correct the arguments provided.</span></span> |

### <a name="nu3002"></a><span data-ttu-id="3ea3c-401">NU3002</span><span class="sxs-lookup"><span data-stu-id="3ea3c-401">NU3002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-402">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-402">**Issue**</span></span> | <span data-ttu-id="3ea3c-403">`-Timestamper` Nie określono opcję z [polecenia nuget znak](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="3ea3c-403">The `-Timestamper` option was not specified with the [nuget sign command](../tools/cli-ref-sign.md).</span></span> |
| <span data-ttu-id="3ea3c-404">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-404">**Example message**</span></span> | <span data-ttu-id="3ea3c-405">*"-Timestamper" nie określono opcji. Podpisanego pakietu nie jest oznaczony znacznikiem czasowym.*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-405">*The '-Timestamper' option was not provided. The signed package will not be timestamped.*</span></span> |
| <span data-ttu-id="3ea3c-406">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-406">**Solution**</span></span> | <span data-ttu-id="3ea3c-407">Określ `-Timestamper` opcję z `nuget sign`.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-407">Specify the `-Timestamper` option with `nuget sign`.</span></span> |

### <a name="nu3004"></a><span data-ttu-id="3ea3c-408">NU3004</span><span class="sxs-lookup"><span data-stu-id="3ea3c-408">NU3004</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-409">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-409">**Issue**</span></span> | <span data-ttu-id="3ea3c-410">Dostarczono niepodpisanego pakietu [nuget Sprawdź polecenie](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="3ea3c-410">An unsigned package was provided to the [nuget verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="3ea3c-411">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-411">**Solution**</span></span> | <span data-ttu-id="3ea3c-412">Uruchom `nuget verify` przy użyciu podpisanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-412">Run `nuget verify` with a signed package.</span></span> <span data-ttu-id="3ea3c-413">Zobacz [podpisywania pakietu](../create-packages/Sign-a-Package.md).</span><span class="sxs-lookup"><span data-stu-id="3ea3c-413">See [Sign a package](../create-packages/Sign-a-Package.md).</span></span> |

### <a name="nu3008"></a><span data-ttu-id="3ea3c-414">NU3008</span><span class="sxs-lookup"><span data-stu-id="3ea3c-414">NU3008</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-415">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-415">**Issue**</span></span> | <span data-ttu-id="3ea3c-416">Nie można sprawdzić integralność pakietu, co oznacza, że pakiet podpisany został zmodyfikowany od czasu podpisania.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-416">The package integrity check failed, meaning that a signed package was tampered with since being signed.</span></span> |
| <span data-ttu-id="3ea3c-417">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-417">**Solution**</span></span> | <span data-ttu-id="3ea3c-418">Skanowanie komputera za pomocą oprogramowania antywirusowego.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-418">Scan your computer with anti-virus software.</span></span> <span data-ttu-id="3ea3c-419">Następnie usuń pakiet z komputera, zainstaluj go ponownie i spróbuj ponownie wykonać operację.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-419">Then remove the package from the computer, reinstall it, and try the operation again.</span></span> <span data-ttu-id="3ea3c-420">Jeśli problem będzie się powtarzać, skontaktuj się z właścicielem źródła pakietu i właściciela pakietu.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-420">If the problem persists, contact the owner of the package source and the package owner.</span></span> |

### <a name="nu3018"></a><span data-ttu-id="3ea3c-421">NU3018</span><span class="sxs-lookup"><span data-stu-id="3ea3c-421">NU3018</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-422">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-422">**Issue**</span></span> | <span data-ttu-id="3ea3c-423">Tworzenie łańcucha certyfikatów nie powiodło się dla podpisu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-423">Certificate chain building failed for the primary signature.</span></span> <span data-ttu-id="3ea3c-424">Podstawowy certyfikat podpisywania nie jest zaufane, odwołany, lub informacji o odwołaniu dla certyfikatu jest niedostępny.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-424">The primary signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="3ea3c-425">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-425">**Example message**</span></span> | <span data-ttu-id="3ea3c-426">*Ostrzeżenie: NU3018: funkcja odwołania nie może sprawdzić odwołania certyfikatu.*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-426">*WARNING: NU3018: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="3ea3c-427">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-427">**Solution**</span></span> | <span data-ttu-id="3ea3c-428">Użyj zaufanego, ważny certyfikat.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-428">Use a trusted and valid certificate.</span></span> <span data-ttu-id="3ea3c-429">Sprawdź łączność z Internetem.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-429">Check internet connectivity.</span></span> |

### <a name="nu3028"></a><span data-ttu-id="3ea3c-430">NU3028</span><span class="sxs-lookup"><span data-stu-id="3ea3c-430">NU3028</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3ea3c-431">**Problem**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-431">**Issue**</span></span> | <span data-ttu-id="3ea3c-432">Tworzenie łańcucha certyfikatów nie powiodło się dla podpisu sygnatury czasowej.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-432">Certificate chain building failed for the timestamp signature.</span></span> <span data-ttu-id="3ea3c-433">Certyfikat podpisywania sygnatury czasowej nie jest zaufane, odwołany, lub informacji o odwołaniu dla certyfikatu jest niedostępny.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-433">The timestamp signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="3ea3c-434">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-434">**Example message**</span></span> | <span data-ttu-id="3ea3c-435">*Ostrzeżenie: NU3028: funkcja odwołania nie może sprawdzić odwołania certyfikatu.*</span><span class="sxs-lookup"><span data-stu-id="3ea3c-435">*WARNING: NU3028: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="3ea3c-436">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="3ea3c-436">**Solution**</span></span> | <span data-ttu-id="3ea3c-437">Użyj zaufanego, ważny certyfikat.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-437">Use a trusted and valid certificate.</span></span> <span data-ttu-id="3ea3c-438">Sprawdź łączność z Internetem.</span><span class="sxs-lookup"><span data-stu-id="3ea3c-438">Check internet connectivity.</span></span> |
