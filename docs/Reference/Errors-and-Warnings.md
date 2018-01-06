---
title: "Przywracanie NuGet błędy i ostrzeżenia odwołania | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/13/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: b76b8a00-7155-4163-b533-894086d2ef78
description: "Pełną dokumentację dla ostrzeżeń i błędów wystawione przez NuGet w czasie przywracania pakietu"
keywords: "NuGet błędy, ostrzeżenia NuGet diagnostyki"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 53fccbb86f2920d870b5383070d043e25045a626
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/05/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="662dd-104">Błędy i ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="662dd-104">Errors and warnings</span></span>

<span data-ttu-id="662dd-105">W NuGet 4.3.0 błędy i ostrzeżenia są numerowane zgodnie z opisem w tym temacie i zawierają szczegółowe informacje pozwalające rozwiązać problemy związane z.</span><span class="sxs-lookup"><span data-stu-id="662dd-105">In NuGet 4.3.0, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span> 

<span data-ttu-id="662dd-106">Błędy i ostrzeżenia wymienione w tym miejscu są dostępne tylko w przypadku [na podstawie PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) projektów i NuGet 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="662dd-106">The errors and warnings listed here are available only with [PackageReference-based](../Consume-Packages/Package-References-in-Project-Files.md) projects and NuGet 4.3.0.</span></span> <span data-ttu-id="662dd-107">NuGet honoruje także właściwości programu MSBuild tłumienie ostrzeżeń lub podniesienie ich poziomu błędy.</span><span class="sxs-lookup"><span data-stu-id="662dd-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="662dd-108">Aby uzyskać więcej informacji, zobacz [porady: pomijanie ostrzeżeń kompilatora](/visualstudio/ide/how-to-suppress-compiler-warnings) w dokumentacji programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="662dd-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="662dd-109">**Błędy**</span><span class="sxs-lookup"><span data-stu-id="662dd-109">**Errors**</span></span>

| <span data-ttu-id="662dd-110">Grupa</span><span class="sxs-lookup"><span data-stu-id="662dd-110">Group</span></span> | <span data-ttu-id="662dd-111">Błąd liczby</span><span class="sxs-lookup"><span data-stu-id="662dd-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="662dd-112">Nieprawidłowy błędów na wejściu</span><span class="sxs-lookup"><span data-stu-id="662dd-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="662dd-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="662dd-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="662dd-114">Brak błędów pakietu i projektu</span><span class="sxs-lookup"><span data-stu-id="662dd-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="662dd-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [ NU1106](#nu1106), [NU1107](#nu1107) (wcześniej NU1607) [NU1108](#nu1107) (wcześniej NU1606)</span><span class="sxs-lookup"><span data-stu-id="662dd-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1107) (previously NU1606)</span></span> |
| [<span data-ttu-id="662dd-116">Błędy zgodności</span><span class="sxs-lookup"><span data-stu-id="662dd-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="662dd-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="662dd-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="662dd-118">**Ostrzeżenia**</span><span class="sxs-lookup"><span data-stu-id="662dd-118">**Warnings**</span></span>

| <span data-ttu-id="662dd-119">Grupa</span><span class="sxs-lookup"><span data-stu-id="662dd-119">Group</span></span> | <span data-ttu-id="662dd-120">Numery ostrzeżeń</span><span class="sxs-lookup"><span data-stu-id="662dd-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="662dd-121">Nieprawidłowy wejściowy ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="662dd-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="662dd-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="662dd-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="662dd-123">Nieoczekiwany pakietu wersji ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="662dd-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="662dd-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="662dd-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="662dd-125">Mechanizm rozpoznawania konfliktu ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="662dd-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="662dd-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="662dd-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="662dd-127">Ostrzeżenia rezerwowy pakietu</span><span class="sxs-lookup"><span data-stu-id="662dd-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="662dd-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="662dd-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="662dd-129">Źródła danych ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="662dd-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="662dd-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="662dd-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="662dd-131">NuGet wewnętrzne błędy i ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="662dd-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="662dd-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="662dd-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="662dd-133">Nieprawidłowy błędów na wejściu</span><span class="sxs-lookup"><span data-stu-id="662dd-133">Invalid input errors</span></span>

<span data-ttu-id="662dd-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="662dd-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="662dd-135">NU1001</span><span class="sxs-lookup"><span data-stu-id="662dd-135">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-136">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-136">**Issue**</span></span> | <span data-ttu-id="662dd-137">Projekt nie zawiera co najmniej jeden struktury.</span><span class="sxs-lookup"><span data-stu-id="662dd-137">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="662dd-138">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-138">**Common causes**</span></span> | <span data-ttu-id="662dd-139">Projekt nie zawiera `TargetFramework` lub `TargetFrameworks` właściwości.</span><span class="sxs-lookup"><span data-stu-id="662dd-139">The project doesn't contain a `TargetFramework` or `TargetFrameworks` property.</span></span> |
| <span data-ttu-id="662dd-140">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-140">**Example message**</span></span> | <span data-ttu-id="662dd-141">*ProjA projektu nie określa żadnych docelowych platform w c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="662dd-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |

### <a name="nu1002"></a><span data-ttu-id="662dd-142">NU1002</span><span class="sxs-lookup"><span data-stu-id="662dd-142">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-143">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-143">**Issue**</span></span> | <span data-ttu-id="662dd-144">Nieprawidłowa kombinacja danych wejściowych oraz wyczyść — słowo kluczowe.</span><span class="sxs-lookup"><span data-stu-id="662dd-144">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="662dd-145">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-145">**Common causes**</span></span> | <span data-ttu-id="662dd-146">Wyczyść nie mogą być łączone z innymi elementami wejściowymi.</span><span class="sxs-lookup"><span data-stu-id="662dd-146">CLEAR may not be combined with other inputs.</span></span> |
| <span data-ttu-id="662dd-147">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-147">**Example message**</span></span> | <span data-ttu-id="662dd-148">*"CLEAR" nie można używać w połączeniu z innymi wartości*</span><span class="sxs-lookup"><span data-stu-id="662dd-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |

### <a name="nu1003"></a><span data-ttu-id="662dd-149">NU1003</span><span class="sxs-lookup"><span data-stu-id="662dd-149">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-150">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-150">**Issue**</span></span> | <span data-ttu-id="662dd-151">`PackageTargetFallback`i `AssetTargetFallback` Podaj inaczej wybierania zasobów i nie mogą być używane razem.</span><span class="sxs-lookup"><span data-stu-id="662dd-151">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="662dd-152">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-152">**Common causes**</span></span> | <span data-ttu-id="662dd-153">Zarówno `PackageTargetFallback` i `AssetTargetFallback` istnieje w projekcie.</span><span class="sxs-lookup"><span data-stu-id="662dd-153">Both `PackageTargetFallback` and `AssetTargetFallback` exist in the project.</span></span> |
| <span data-ttu-id="662dd-154">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-154">**Example message**</span></span> | <span data-ttu-id="662dd-155">*PackageTargetFallback i AssetTargetFallback nie mogą być używane razem. Usuń odwołania PackageTargetFallback(deprecated) ze środowiska projektu.*</span><span class="sxs-lookup"><span data-stu-id="662dd-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="662dd-156">Brak błędów pakietu i projektu</span><span class="sxs-lookup"><span data-stu-id="662dd-156">Missing package and project errors</span></span>

<span data-ttu-id="662dd-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104 ](#nu1104)  |  [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="662dd-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="662dd-158">NU1100</span><span class="sxs-lookup"><span data-stu-id="662dd-158">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-159">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-159">**Issue**</span></span> | <span data-ttu-id="662dd-160">Grupa zależności nie można rozpoznać.</span><span class="sxs-lookup"><span data-stu-id="662dd-160">A dependency group not be resolved.</span></span> <span data-ttu-id="662dd-161">Jest to problem rodzajowy dla typów, które nie są pakiety lub projektów.</span><span class="sxs-lookup"><span data-stu-id="662dd-161">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="662dd-162">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-162">**Common causes**</span></span> | <span data-ttu-id="662dd-163">Projekt zawiera zależności elementu, który nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="662dd-163">The project contains a dependency on an item that doesn't exist.</span></span> |
| <span data-ttu-id="662dd-164">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-164">**Example message**</span></span> | <span data-ttu-id="662dd-165">*Nie można rozpoznać System.Missing dla net45*</span><span class="sxs-lookup"><span data-stu-id="662dd-165">*Unable to resolve System.Missing for net45*</span></span> |

### <a name="nu1101"></a><span data-ttu-id="662dd-166">NU1101</span><span class="sxs-lookup"><span data-stu-id="662dd-166">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-167">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-167">**Issue**</span></span> | <span data-ttu-id="662dd-168">Nie można odnaleźć pakietu na wszystkich źródeł.</span><span class="sxs-lookup"><span data-stu-id="662dd-168">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="662dd-169">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-169">**Common causes**</span></span> | <span data-ttu-id="662dd-170">Brak źródła poprawny pakiet lub identyfikator pakietu jest nieprawidłowa.</span><span class="sxs-lookup"><span data-stu-id="662dd-170">The correct package source is missing or the package identifier is incorrect.</span></span> |
| <span data-ttu-id="662dd-171">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-171">**Example message**</span></span> | <span data-ttu-id="662dd-172">*Nie można odnaleźć pakietu System.Missing. Żadne pakiety nie istnieje z tym identyfikatorem w źródłach: dotnet core, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="662dd-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |

### <a name="nu1102"></a><span data-ttu-id="662dd-173">NU1102</span><span class="sxs-lookup"><span data-stu-id="662dd-173">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-174">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-174">**Issue**</span></span> | <span data-ttu-id="662dd-175">Identyfikator pakietu został znaleziony, lecz nie można odnaleźć wersji w zakresie określonym zależności na żadnym z źródeł.</span><span class="sxs-lookup"><span data-stu-id="662dd-175">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> |
| <span data-ttu-id="662dd-176">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-176">**Common causes**</span></span> | <span data-ttu-id="662dd-177">Brak źródła poprawny pakiet lub zakres zależności jest niepoprawny.</span><span class="sxs-lookup"><span data-stu-id="662dd-177">The correct package source is missing or the dependency range is incorrect.</span></span> <span data-ttu-id="662dd-178">Pakiet, a użytkownik nie może być określony zakres.</span><span class="sxs-lookup"><span data-stu-id="662dd-178">The range might be specified by a package and not the user.</span></span> <span data-ttu-id="662dd-179">Użytkownik może być konieczne przełączenie się do wersji dostępnych w przypadku tego pakietu jest odwołuje się projekt bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="662dd-179">The user may need to switch to an available version if this package is referenced by the project directly.</span></span> |
| <span data-ttu-id="662dd-180">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-180">**Example message**</span></span> | <span data-ttu-id="662dd-181">*Nie można odnaleźć pakietu NuGet.Versioning z wersją (> = 9.0.1)<br/> — wersje 30 znalezione w usłudze nuget.org [najbliższej wersji: 4.0.0]<br/> — wersje znaleziono 10 w dotnet buildtools [najbliższej wersji: 4.0.0-rc-2129]<br/> -znaleziono 9 wersje w NuGetVolatile [najbliższej wersji: 3.0.0-beta-00032]<br/> -znaleziono wersje 0 w podstawowej platformy dotnet<br/> -znaleziono wersje 0 w dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="662dd-181">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1103"></a><span data-ttu-id="662dd-182">NU1103</span><span class="sxs-lookup"><span data-stu-id="662dd-182">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-183">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-183">**Issue**</span></span> | <span data-ttu-id="662dd-184">Nie odnaleziono żadnych stabilne wersje w zakresie zależności.</span><span class="sxs-lookup"><span data-stu-id="662dd-184">No stable versions were found in the dependency range.</span></span> <span data-ttu-id="662dd-185">Wersje wstępne znaleziono, ale nie są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="662dd-185">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="662dd-186">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-186">**Common causes**</span></span> | <span data-ttu-id="662dd-187">Projekt określony stabilną wersję dla zakresu zależności.</span><span class="sxs-lookup"><span data-stu-id="662dd-187">The project specified a stable version for the dependency range.</span></span> <span data-ttu-id="662dd-188">Użytkownicy muszą zmienić zakres wersji, aby uwzględnić wersje wstępne.</span><span class="sxs-lookup"><span data-stu-id="662dd-188">Users need to change the version range to include pre-release versions.</span></span> |
| <span data-ttu-id="662dd-189">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-189">**Example message**</span></span> | <span data-ttu-id="662dd-190">*Nie można odnaleźć pakietu stabilna NuGet.Versioning z wersją (> = 3.0.0)<br/> — wersje znaleziono 10 w dotnet buildtools [najbliższej wersji: 4.0.0-rc-2129]<br/> -znaleziono 9 wersje w NuGetVolatile [najbliższej wersji: 3.0.0-beta-00032] <br/> -Znaleziono wersje 0 w podstawowej platformy dotnet<br/> -znaleziono wersje 0 w dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="662dd-190">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1104"></a><span data-ttu-id="662dd-191">NU1104</span><span class="sxs-lookup"><span data-stu-id="662dd-191">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-192">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-192">**Issue**</span></span> | <span data-ttu-id="662dd-193">Wskazuje element ProjectReference do pliku, który nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="662dd-193">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="662dd-194">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-194">**Common causes**</span></span> | <span data-ttu-id="662dd-195">Brakuje pliku projektu z dysku lub odniesienia jest nieprawidłowa.</span><span class="sxs-lookup"><span data-stu-id="662dd-195">The project file is missing from disk or the reference is incorrect.</span></span> |
| <span data-ttu-id="662dd-196">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-196">**Example message**</span></span> | <span data-ttu-id="662dd-197">*Odwołanie do projektu nie istnieje "c:\a.csproj". Sprawdź, czy odwołanie do projektu jest prawidłowa i czy istnieje plik projektu.*</span><span class="sxs-lookup"><span data-stu-id="662dd-197">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |

### <a name="nu1105"></a><span data-ttu-id="662dd-198">NU1105</span><span class="sxs-lookup"><span data-stu-id="662dd-198">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-199">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-199">**Issue**</span></span> | <span data-ttu-id="662dd-200">Plik projektu istnieje, ale go nie dostarczono żadnych informacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="662dd-200">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="662dd-201">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-201">**Common causes**</span></span> | <span data-ttu-id="662dd-202">W programie Visual Studio to może oznaczać, że projekt jest zwolniony.</span><span class="sxs-lookup"><span data-stu-id="662dd-202">In Visual Studio this could mean that the project is unloaded.</span></span> <span data-ttu-id="662dd-203">W wierszu polecenia to może oznaczać, że plik jest uszkodzony lub nie zawiera niestandardowego po elemencie docelowym importów potrzebne do odzyskiwania do odczytu projektu.</span><span class="sxs-lookup"><span data-stu-id="662dd-203">From the command line this could mean that the file is corrupt or that it doesn't contain the custom after imports target needed for restore to read the project.</span></span> |
| <span data-ttu-id="662dd-204">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-204">**Example message**</span></span> | <span data-ttu-id="662dd-205">*Nie można odczytać informacji o projekcie dla "c:\a.csproj". Plik projektu może być nieprawidłowe lub brakujące elementy docelowe, wymaganych do przywrócenia.*</span><span class="sxs-lookup"><span data-stu-id="662dd-205">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

### <a name="nu1106"></a><span data-ttu-id="662dd-206">NU1106</span><span class="sxs-lookup"><span data-stu-id="662dd-206">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-207">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-207">**Issue**</span></span> | <span data-ttu-id="662dd-208">Nie można rozpoznać zależności ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="662dd-208">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="662dd-209">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-209">**Common causes**</span></span> | <span data-ttu-id="662dd-210">Pakiety zawierają zależność od dokładnej wersji pakietu zamiast nieograniczoną zakresów.</span><span class="sxs-lookup"><span data-stu-id="662dd-210">Packages contain dependency on exact versions of a package instead of open-ended ranges.</span></span> |
| <span data-ttu-id="662dd-211">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-211">**Example message**</span></span> | <span data-ttu-id="662dd-212">*Nie można zrealizować żądań będących w konflikcie dla {id}: {konflikt path} Framework: {docelowy wykres}*</span><span class="sxs-lookup"><span data-stu-id="662dd-212">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |

<span data-ttu-id="662dd-213">< name = "NU1107 ></a></span><span class="sxs-lookup"><span data-stu-id="662dd-213"><a name="NU1107></a></span></span>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="662dd-214">NU1107 (wcześniej NU1607)</span><span class="sxs-lookup"><span data-stu-id="662dd-214">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-215">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-215">**Issue**</span></span> | <span data-ttu-id="662dd-216">Nie można rozpoznać ograniczenia zależności między pakietami.</span><span class="sxs-lookup"><span data-stu-id="662dd-216">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="662dd-217">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-217">**Common causes**</span></span> | <span data-ttu-id="662dd-218">Pakiety z ograniczeniami zależności na dokładną wersję nie zezwalają na inne pakiety w razie potrzeby zwiększyć wersji.</span><span class="sxs-lookup"><span data-stu-id="662dd-218">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> |
| <span data-ttu-id="662dd-219">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-219">**Example message**</span></span> | <span data-ttu-id="662dd-220">*Konflikt wersji dla NuGet.Versioning wykryte. Pakiet odwoływać się bezpośrednio z projektu, aby rozwiązać ten problem.<br/>  NuGet.Versioning (= 3.5.0) -> NuGet.Packaging 3.5.0<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="662dd-220">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |

<span data-ttu-id="662dd-221">< name = "NU1108 ></a></span><span class="sxs-lookup"><span data-stu-id="662dd-221"><a name="NU1108></a></span></span>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="662dd-222">NU1108 (wcześniej NU1606)</span><span class="sxs-lookup"><span data-stu-id="662dd-222">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-223">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-223">**Issue**</span></span> | <span data-ttu-id="662dd-224">Wykryto zależność cykliczną.</span><span class="sxs-lookup"><span data-stu-id="662dd-224">A circular dependency was detected.</span></span> |
| <span data-ttu-id="662dd-225">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-225">**Common causes**</span></span> | <span data-ttu-id="662dd-226">Pakiet jest autoryzowane.</span><span class="sxs-lookup"><span data-stu-id="662dd-226">A package is authored incorrectly.</span></span> |
| <span data-ttu-id="662dd-227">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-227">**Example message**</span></span> | <span data-ttu-id="662dd-228">*Wykryto cykl: A -> B -> A*</span><span class="sxs-lookup"><span data-stu-id="662dd-228">*Cycle detected: A -> B -> A*</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="662dd-229">Błędy zgodności</span><span class="sxs-lookup"><span data-stu-id="662dd-229">Compatibility errors</span></span>

<span data-ttu-id="662dd-230">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="662dd-230">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="662dd-231">NU1201</span><span class="sxs-lookup"><span data-stu-id="662dd-231">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-232">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-232">**Issue**</span></span> | <span data-ttu-id="662dd-233">Zależności projektu nie zawiera struktury zgodne z bieżącego projektu.</span><span class="sxs-lookup"><span data-stu-id="662dd-233">A dependency project doesn't contain a framework compatible with the current project.</span></span> |
| <span data-ttu-id="662dd-234">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-234">**Common causes**</span></span> | <span data-ttu-id="662dd-235">Platforma docelowa projektu jest wyższą wersję niż odbierającą projektu.</span><span class="sxs-lookup"><span data-stu-id="662dd-235">The project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="662dd-236">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-236">**Example message**</span></span> | <span data-ttu-id="662dd-237">*ServerWeb projektu nie jest zgodny z netstandard1.3 (. Krótkich nazw NETStandard, Version = w wersji 1.3). Projekt obsługuje ServerWeb:<br/> -netstandard1.6 (. Krótkich nazw NETStandard, Version = w wersji 1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = 1.0)*</span><span class="sxs-lookup"><span data-stu-id="662dd-237">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |

### <a name="nu1202"></a><span data-ttu-id="662dd-238">NU1202</span><span class="sxs-lookup"><span data-stu-id="662dd-238">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-239">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-239">**Issue**</span></span> | <span data-ttu-id="662dd-240">Pakiet zależności nie zawiera żadnych zasobów, które są zgodne z projektem.</span><span class="sxs-lookup"><span data-stu-id="662dd-240">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="662dd-241">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-241">**Common causes**</span></span> | <span data-ttu-id="662dd-242">Pakiet nie obsługuje platformy docelowej projektu.</span><span class="sxs-lookup"><span data-stu-id="662dd-242">The package doesn't support the project's target framework.</span></span> |
| <span data-ttu-id="662dd-243">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-243">**Example message**</span></span> | <span data-ttu-id="662dd-244">*Pakiet System.ComponentModel.EventBasedAsync 4.0.11 nie jest zgodny z netstandard1.3 (. Krótkich nazw NETStandard, Version = w wersji 1.3). Pakiet obsługuje System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, wersja = 1.0)<br/> -monotouch10 (MonoTouch, wersja = 1.0)<br/> -net45 (. NETFramework, Version = 4.5)<br/> -netcore50 (. NETCore, Version = v5.0)<br/> -netstandard1.0 (. Krótkich nazw NETStandard, Version = 1.0)<br/> -przenośny net45 + win8 + wp8 + wpa81 (. NETPortable, wersja = v0.0, profil = Profile259)<br/> — Windows 8 (Windows, wersja = w wersji 8.0)<br/> -wp8 (WindowsPhone, wersja = w wersji 8.0)<br/> -wpa81 (WindowsPhoneApp, wersja = v8.1)<br/> — xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="662dd-244">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|

### <a name="nu1203"></a><span data-ttu-id="662dd-245">NU1203</span><span class="sxs-lookup"><span data-stu-id="662dd-245">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-246">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-246">**Issue**</span></span> | <span data-ttu-id="662dd-247">Pakiet nie obsługuje projektu `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="662dd-247">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="662dd-248">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-248">**Common causes**</span></span> | <span data-ttu-id="662dd-249">Pakiet nie obsługuje bieżącej `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="662dd-249">The package doesn't support the current `RuntimeIdentifier`.</span></span> <span data-ttu-id="662dd-250">Zmień `RuntimeIdentifier` wartości używanych w projekcie, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="662dd-250">Change the `RuntimeIdentifier` values used in the project if needed.</span></span> |
| <span data-ttu-id="662dd-251">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-251">**Example message**</span></span> | <span data-ttu-id="662dd-252">*System.Example 1.0.0 udostępnia zestaw odwołania czasu kompilowania dla a.dll na net461, ale nie nie zgodny zestaw czasu wykonywania.*</span><span class="sxs-lookup"><span data-stu-id="662dd-252">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |

### <a name="nu1401"></a><span data-ttu-id="662dd-253">NU1401</span><span class="sxs-lookup"><span data-stu-id="662dd-253">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-254">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-254">**Issue**</span></span> | <span data-ttu-id="662dd-255">Pakiet wymaga funkcji lub struktur nie są obecnie obsługiwane przez zainstalowaną wersję programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="662dd-255">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="662dd-256">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-256">**Common causes**</span></span> | <span data-ttu-id="662dd-257">Uaktualnij program NuGet, aby rozwiązać problem.</span><span class="sxs-lookup"><span data-stu-id="662dd-257">Upgrade NuGet to fix the issue.</span></span> |
| <span data-ttu-id="662dd-258">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-258">**Example message**</span></span> | <span data-ttu-id="662dd-259">*Pakiet "NuGet.Versioning" wymaga wersji klienta "5.0.0" NuGet lub nowszej, ale bieżąca wersja NuGet to "4.3.0". Aby uaktualnić narzędzie NuGet, przejdź do http://docs.nuget.org/consume/installing-nuget.*</span><span class="sxs-lookup"><span data-stu-id="662dd-259">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'. To upgrade NuGet, please go to http://docs.nuget.org/consume/installing-nuget.*</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="662dd-260">Nieprawidłowy wejściowy ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="662dd-260">Invalid input warnings</span></span>

<span data-ttu-id="662dd-261">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="662dd-261">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="662dd-262">NU1501</span><span class="sxs-lookup"><span data-stu-id="662dd-262">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-263">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-263">**Issue**</span></span> | <span data-ttu-id="662dd-264">Przywracanie projektu próbuje działać na nie został znaleziony.</span><span class="sxs-lookup"><span data-stu-id="662dd-264">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="662dd-265">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-265">**Common causes**</span></span> | <span data-ttu-id="662dd-266">Brak projektu.</span><span class="sxs-lookup"><span data-stu-id="662dd-266">The project is missing.</span></span> |
| <span data-ttu-id="662dd-267">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-267">**Example message**</span></span> | <span data-ttu-id="662dd-268">*Folder "c:\projects\a" nie zawiera projektu do przywrócenia.*</span><span class="sxs-lookup"><span data-stu-id="662dd-268">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |

### <a name="nu1502"></a><span data-ttu-id="662dd-269">NU1502</span><span class="sxs-lookup"><span data-stu-id="662dd-269">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-270">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-270">**Issue**</span></span> | <span data-ttu-id="662dd-271">`RuntimeSupports`zawiera nieprawidłowy profil.</span><span class="sxs-lookup"><span data-stu-id="662dd-271">`RuntimeSupports` contains an invalid profile.</span></span> |
| <span data-ttu-id="662dd-272">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-272">**Common causes**</span></span> | <span data-ttu-id="662dd-273">Nie znaleziono profilu obsługuje w `runtime.json` plik z bieżącego zależności pakietów.</span><span class="sxs-lookup"><span data-stu-id="662dd-273">The supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span> |
| <span data-ttu-id="662dd-274">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-274">**Example message**</span></span> | <span data-ttu-id="662dd-275">*Profil zgodności nieznany: aaa*</span><span class="sxs-lookup"><span data-stu-id="662dd-275">*Unknown Compatibility Profile: aaa*</span></span> |

### <a name="nu1503"></a><span data-ttu-id="662dd-276">NU1503</span><span class="sxs-lookup"><span data-stu-id="662dd-276">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-277">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-277">**Issue**</span></span> | <span data-ttu-id="662dd-278">Zależności projektu nie importuje obiekty docelowe przywracania NuGet.</span><span class="sxs-lookup"><span data-stu-id="662dd-278">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="662dd-279">Ten jest podobny do NU1105, ale w tym miejscu projektu zostanie pominięty i zignorowany zamiast powoduje wszystkie przywracania się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="662dd-279">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="662dd-280">W złożonych rozwiązań są często innych typów projektów, które mogą nie obsługiwać przywracania.</span><span class="sxs-lookup"><span data-stu-id="662dd-280">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="662dd-281">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-281">**Common causes**</span></span> | <span data-ttu-id="662dd-282">Może to nastąpić dla projektów, które nie należy importować wspólne właściwości/cele, które są automatycznie importowane przywracania.</span><span class="sxs-lookup"><span data-stu-id="662dd-282">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="662dd-283">Jeśli projekt nie trzeba przywrócić możesz go zignorować.</span><span class="sxs-lookup"><span data-stu-id="662dd-283">If the project doesn't need to be restored this can be ignored.</span></span> |
| <span data-ttu-id="662dd-284">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-284">**Example message**</span></span> | <span data-ttu-id="662dd-285">*Pomijanie przywracania dla projektu "c:\a.csproj". Plik projektu może być nieprawidłowe lub brakujące elementy docelowe, wymaganych do przywrócenia.*</span><span class="sxs-lookup"><span data-stu-id="662dd-285">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="662dd-286">Nieoczekiwany pakietu wersji ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="662dd-286">Unexpected package version warnings</span></span>

<span data-ttu-id="662dd-287">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="662dd-287">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="662dd-288">NU1601</span><span class="sxs-lookup"><span data-stu-id="662dd-288">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-289">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-289">**Issue**</span></span> | <span data-ttu-id="662dd-290">Zależności bezpośrednich projektu był upadku na wyższą wersję niż określonego projektu.</span><span class="sxs-lookup"><span data-stu-id="662dd-290">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="662dd-291">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-291">**Common causes**</span></span> | <span data-ttu-id="662dd-292">Inny pakiet zależności wymagane wyższą wersję i upadku pakietu w.</span><span class="sxs-lookup"><span data-stu-id="662dd-292">Another dependency package required a higher version and bumped the package up.</span></span> |
| <span data-ttu-id="662dd-293">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-293">**Example message**</span></span> | <span data-ttu-id="662dd-294">*Określoną zależnością było NuGet.Versioning (> = 3.5.0), ale ostatecznie otrzymano NuGet.Versioning 4.0.0.*</span><span class="sxs-lookup"><span data-stu-id="662dd-294">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |

### <a name="nu1602"></a><span data-ttu-id="662dd-295">NU1602</span><span class="sxs-lookup"><span data-stu-id="662dd-295">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-296">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-296">**Issue**</span></span> | <span data-ttu-id="662dd-297">Zależność pakietu brak dolnej granicy.</span><span class="sxs-lookup"><span data-stu-id="662dd-297">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="662dd-298">To nie zezwala na przywracania znaleźć *najlepszego dopasowania*.</span><span class="sxs-lookup"><span data-stu-id="662dd-298">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="662dd-299">Każdy przywracania będzie przestawiany dół próby znalezienia starszej wersji, który może być używany.</span><span class="sxs-lookup"><span data-stu-id="662dd-299">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="662dd-300">Oznacza to, że przywracanie przejdzie do trybu online, aby sprawdzić wszystkie źródła zawsze zamiast pakietów, które już istnieją w folderze pakietów użytkowników.</span><span class="sxs-lookup"><span data-stu-id="662dd-300">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="662dd-301">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-301">**Common causes**</span></span> | <span data-ttu-id="662dd-302">Jest to zazwyczaj błąd tworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="662dd-302">This is usually a package authoring error.</span></span> |
| <span data-ttu-id="662dd-303">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-303">**Example message**</span></span> | <span data-ttu-id="662dd-304">*NuGet.Packaging 4.0.0 nie zapewnia włącznie dolna granica dla zależności NuGet.Versioning (> 3.5.0). Przybliżony najlepsze dopasowanie 3.6.0 został rozwiązany.*</span><span class="sxs-lookup"><span data-stu-id="662dd-304">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |

### <a name="nu1603"></a><span data-ttu-id="662dd-305">NU1603</span><span class="sxs-lookup"><span data-stu-id="662dd-305">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-306">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-306">**Issue**</span></span> | <span data-ttu-id="662dd-307">Zależność pakietu określonej wersji, którego nie można odnaleźć.</span><span class="sxs-lookup"><span data-stu-id="662dd-307">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="662dd-308">Nowsza wersja użyto zamiast tego, który różni się od pakietu opracowania przed.</span><span class="sxs-lookup"><span data-stu-id="662dd-308">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="662dd-309">Oznacza to, że przywracanie nie znalazł *najlepszego dopasowania*.</span><span class="sxs-lookup"><span data-stu-id="662dd-309">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="662dd-310">Każdy przywracania będzie przestawiany dół próby znalezienia starszej wersji, który może być używany.</span><span class="sxs-lookup"><span data-stu-id="662dd-310">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="662dd-311">Oznacza to, że przywracanie przejdzie do trybu online, aby sprawdzić wszystkie źródła zawsze zamiast pakietów, które już istnieją w folderze pakietów użytkowników.</span><span class="sxs-lookup"><span data-stu-id="662dd-311">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="662dd-312">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-312">**Common causes**</span></span> | <span data-ttu-id="662dd-313">Źródła pakietu nie zawierają wersja oczekiwana dolnej granicy.</span><span class="sxs-lookup"><span data-stu-id="662dd-313">The package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="662dd-314">Jeśli nie zostało zwolnione pakietu oczekiwano może to być błąd tworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="662dd-314">If the package expected has not been released then this may be a package authoring error.</span></span> |
| <span data-ttu-id="662dd-315">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-315">**Example message**</span></span> | <span data-ttu-id="662dd-316">NuGet.Packaging 4.0.0 zależy od NuGet.Versioning (> = 4.0.0), ale nie można odnaleźć 4.0.0.</span><span class="sxs-lookup"><span data-stu-id="662dd-316">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="662dd-317">Przybliżony najlepsze dopasowanie 5.0.0 został rozwiązany.</span><span class="sxs-lookup"><span data-stu-id="662dd-317">An approximate best match of 5.0.0 was resolved.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="662dd-318">NU1604</span><span class="sxs-lookup"><span data-stu-id="662dd-318">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-319">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-319">**Issue**</span></span> | <span data-ttu-id="662dd-320">Zależności projektu nie definiuje dolną granicą.</span><span class="sxs-lookup"><span data-stu-id="662dd-320">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="662dd-321">Oznacza to, że przywracanie nie znalazł *najlepszego dopasowania*.</span><span class="sxs-lookup"><span data-stu-id="662dd-321">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="662dd-322">Każdy przywracania będzie przestawiany dół próby znalezienia starszej wersji, który może być używany.</span><span class="sxs-lookup"><span data-stu-id="662dd-322">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="662dd-323">Oznacza to, że przywracanie przejdzie do trybu online, aby sprawdzić wszystkie źródła zawsze zamiast pakietów, które już istnieją w folderze pakietów użytkowników.</span><span class="sxs-lookup"><span data-stu-id="662dd-323">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="662dd-324">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-324">**Common causes**</span></span> | <span data-ttu-id="662dd-325">Projektu *PackageReference* *wersji* można zaktualizować atrybutu, aby uwzględnić dolną granicą.</span><span class="sxs-lookup"><span data-stu-id="662dd-325">The project's *PackageReference* *Version* attribute should be updated to include a lower bound.</span></span> |
| <span data-ttu-id="662dd-326">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-326">**Example message**</span></span> | <span data-ttu-id="662dd-327">*Projekt zależności NuGet.Versioning (< = od 9.0.0) Nowak zawiera włącznie dolnej granicy. Dolna granica należy uwzględnić w wersji zależności, aby zapewnić wyniki przywracania na poziomie.*</span><span class="sxs-lookup"><span data-stu-id="662dd-327">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |

### <a name="nu1605"></a><span data-ttu-id="662dd-328">NU1605</span><span class="sxs-lookup"><span data-stu-id="662dd-328">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-329">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-329">**Issue**</span></span> | <span data-ttu-id="662dd-330">Pakiet zależności określić ograniczenia wersji za pomocą nowszej wersji pakietu niż przywracania ostatecznie rozwiązane.</span><span class="sxs-lookup"><span data-stu-id="662dd-330">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> |
| <span data-ttu-id="662dd-331">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-331">**Common causes**</span></span> | <span data-ttu-id="662dd-332">Najbliższej wins podczas rozpoznawania pakietów.</span><span class="sxs-lookup"><span data-stu-id="662dd-332">Nearest wins when resolving packages.</span></span> <span data-ttu-id="662dd-333">Bliżej położonego pakietu na wykresie mogą mieć zastąpione odległymi pakiet.</span><span class="sxs-lookup"><span data-stu-id="662dd-333">A nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="662dd-334">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-334">**Example message**</span></span> | <span data-ttu-id="662dd-335">*Wykryto starszą wersję pakietu: NuGet.Versioning z 4.0.0 do 3.5.0. Odwoływać się bezpośrednio z projektu, aby wybrać inną wersję pakietu.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="662dd-335">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="662dd-336">Mechanizm rozpoznawania konfliktu ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="662dd-336">Resolver conflict warnings</span></span>

[<span data-ttu-id="662dd-337">NU1608</span><span class="sxs-lookup"><span data-stu-id="662dd-337">NU1608</span></span>](#nu1608)

### <a name="nu1608"></a><span data-ttu-id="662dd-338">NU1608</span><span class="sxs-lookup"><span data-stu-id="662dd-338">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-339">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-339">**Issue**</span></span> | <span data-ttu-id="662dd-340">Usuń pakiet jest większa niż umożliwia ograniczenie zależności.</span><span class="sxs-lookup"><span data-stu-id="662dd-340">A resolve package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="662dd-341">W niektórych przypadkach jest to zamierzone i można pominąć to ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="662dd-341">In some cases this is intentional and the warning can be suppressed.</span></span> |
| <span data-ttu-id="662dd-342">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-342">**Common causes**</span></span> | <span data-ttu-id="662dd-343">Pakiet bezpośrednio odwołuje się projekt spowoduje zastąpienie ograniczenia zależności z innymi pakietami.</span><span class="sxs-lookup"><span data-stu-id="662dd-343">A package referenced directly by a project will override dependency constraints from other packages.</span></span>   |
| <span data-ttu-id="662dd-344">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-344">**Example message**</span></span> | <span data-ttu-id="662dd-345">*Wersja pakietu wykrytych poza ograniczenia zależności: x 1.0.0 wymaga y (= 1.0.0), ale wersja y 2.0.0 został rozwiązany.*</span><span class="sxs-lookup"><span data-stu-id="662dd-345">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="662dd-346">Ostrzeżenia rezerwowy pakietu</span><span class="sxs-lookup"><span data-stu-id="662dd-346">Package fallback warnings</span></span>

[<span data-ttu-id="662dd-347">NU1701</span><span class="sxs-lookup"><span data-stu-id="662dd-347">NU1701</span></span>](#nu1701)

### <a name="nu1701"></a><span data-ttu-id="662dd-348">NU1701</span><span class="sxs-lookup"><span data-stu-id="662dd-348">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-349">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-349">**Issue**</span></span> | <span data-ttu-id="662dd-350">*PackageTargetFallback/AssetTargetFallback* zostało użyte do wybrania zasoby z pakietu.</span><span class="sxs-lookup"><span data-stu-id="662dd-350">*PackageTargetFallback/AssetTargetFallback* was used to select assets from a package.</span></span> <span data-ttu-id="662dd-351">To ostrzeżenie, aby umożliwić użytkownikowi wiedzieć, że zasoby nie mogą być 100% zgodny.</span><span class="sxs-lookup"><span data-stu-id="662dd-351">This is a warning to let the user know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="662dd-352">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-352">**Common causes**</span></span> | <span data-ttu-id="662dd-353">Pakiet nie obsługuje platformy projektu.</span><span class="sxs-lookup"><span data-stu-id="662dd-353">The package doesn't support the project framework.</span></span> |
| <span data-ttu-id="662dd-354">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-354">**Example message**</span></span> | <span data-ttu-id="662dd-355">*Pakiet "NuGet.Versioning" został przywrócony przy użyciu "portable net45 + win8" zamiast platformy docelowej projektu "netstandard1.5". Ten pakiet nie może być całkowicie zgodne z projektem.*</span><span class="sxs-lookup"><span data-stu-id="662dd-355">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="662dd-356">Źródła danych ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="662dd-356">Feed warnings</span></span>

[<span data-ttu-id="662dd-357">NU1801</span><span class="sxs-lookup"><span data-stu-id="662dd-357">NU1801</span></span>](#nu1801)

### <a name="nu1801"></a><span data-ttu-id="662dd-358">NU1801</span><span class="sxs-lookup"><span data-stu-id="662dd-358">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-359">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-359">**Issue**</span></span> | <span data-ttu-id="662dd-360">Wystąpił błąd podczas odczytywania źródła po `IgnoreFailedSources` jest ustawiona na wartość true, konwersją niekrytyczny ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="662dd-360">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="662dd-361">To może zawierać żadnych komunikatów i jest rodzajowy.</span><span class="sxs-lookup"><span data-stu-id="662dd-361">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="662dd-362">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-362">**Common causes**</span></span> | <span data-ttu-id="662dd-363">Źródło jest nieprawidłowe.</span><span class="sxs-lookup"><span data-stu-id="662dd-363">The source is invalid.</span></span> |
| <span data-ttu-id="662dd-364">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="662dd-364">**Example message**</span></span> | <span data-ttu-id="662dd-365">n/d</span><span class="sxs-lookup"><span data-stu-id="662dd-365">n/a</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="662dd-366">NuGet wewnętrzne błędy i ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="662dd-366">NuGet internal errors and warnings</span></span>

<span data-ttu-id="662dd-367">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="662dd-367">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="662dd-368">NU1000</span><span class="sxs-lookup"><span data-stu-id="662dd-368">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-369">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-369">**Issue**</span></span> | <span data-ttu-id="662dd-370">Nieokreślony błąd wewnętrzny z pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="662dd-370">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="662dd-371">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-371">**Common causes**</span></span> | <span data-ttu-id="662dd-372">Sprawdź dzienniki, aby uzyskać więcej informacji</span><span class="sxs-lookup"><span data-stu-id="662dd-372">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="662dd-373">NU1500</span><span class="sxs-lookup"><span data-stu-id="662dd-373">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="662dd-374">**Problem**</span><span class="sxs-lookup"><span data-stu-id="662dd-374">**Issue**</span></span> | <span data-ttu-id="662dd-375">Nieokreślony ostrzeżenie wewnętrzny z pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="662dd-375">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="662dd-376">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="662dd-376">**Common causes**</span></span> | <span data-ttu-id="662dd-377">Sprawdź dzienniki, aby uzyskać więcej informacji</span><span class="sxs-lookup"><span data-stu-id="662dd-377">Check the logs for more information</span></span> |
