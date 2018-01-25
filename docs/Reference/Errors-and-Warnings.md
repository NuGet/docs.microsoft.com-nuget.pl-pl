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
ms.openlocfilehash: 9e22b63636980ce64017c950148d9005bf9c2fb1
ms.sourcegitcommit: ed01eaeef9bf488c36556b97247ca440384c0242
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/23/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="c36bd-104">Błędy i ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="c36bd-104">Errors and warnings</span></span>

<span data-ttu-id="c36bd-105">W NuGet 4.3.0 błędy i ostrzeżenia są numerowane zgodnie z opisem w tym temacie i zawierają szczegółowe informacje pozwalające rozwiązać problemy związane z.</span><span class="sxs-lookup"><span data-stu-id="c36bd-105">In NuGet 4.3.0, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span> 

<span data-ttu-id="c36bd-106">Błędy i ostrzeżenia wymienione w tym miejscu są dostępne tylko w przypadku [na podstawie PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) projektów i NuGet 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="c36bd-106">The errors and warnings listed here are available only with [PackageReference-based](../Consume-Packages/Package-References-in-Project-Files.md) projects and NuGet 4.3.0.</span></span> <span data-ttu-id="c36bd-107">NuGet honoruje także właściwości programu MSBuild tłumienie ostrzeżeń lub podniesienie ich poziomu błędy.</span><span class="sxs-lookup"><span data-stu-id="c36bd-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="c36bd-108">Aby uzyskać więcej informacji, zobacz [porady: pomijanie ostrzeżeń kompilatora](/visualstudio/ide/how-to-suppress-compiler-warnings) w dokumentacji programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c36bd-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="c36bd-109">**Błędy**</span><span class="sxs-lookup"><span data-stu-id="c36bd-109">**Errors**</span></span>

| <span data-ttu-id="c36bd-110">Grupa</span><span class="sxs-lookup"><span data-stu-id="c36bd-110">Group</span></span> | <span data-ttu-id="c36bd-111">Błąd liczby</span><span class="sxs-lookup"><span data-stu-id="c36bd-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="c36bd-112">Nieprawidłowy błędów na wejściu</span><span class="sxs-lookup"><span data-stu-id="c36bd-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="c36bd-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="c36bd-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="c36bd-114">Brak błędów pakietu i projektu</span><span class="sxs-lookup"><span data-stu-id="c36bd-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="c36bd-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [ NU1106](#nu1106), [NU1107](#nu1107) (wcześniej NU1607) [NU1108](#nu1108) (wcześniej NU1606)</span><span class="sxs-lookup"><span data-stu-id="c36bd-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="c36bd-116">Błędy zgodności</span><span class="sxs-lookup"><span data-stu-id="c36bd-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="c36bd-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="c36bd-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="c36bd-118">**Ostrzeżenia**</span><span class="sxs-lookup"><span data-stu-id="c36bd-118">**Warnings**</span></span>

| <span data-ttu-id="c36bd-119">Grupa</span><span class="sxs-lookup"><span data-stu-id="c36bd-119">Group</span></span> | <span data-ttu-id="c36bd-120">Numery ostrzeżeń</span><span class="sxs-lookup"><span data-stu-id="c36bd-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="c36bd-121">Nieprawidłowy wejściowy ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="c36bd-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="c36bd-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="c36bd-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="c36bd-123">Nieoczekiwany pakietu wersji ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="c36bd-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="c36bd-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="c36bd-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="c36bd-125">Mechanizm rozpoznawania konfliktu ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="c36bd-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="c36bd-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="c36bd-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="c36bd-127">Ostrzeżenia rezerwowy pakietu</span><span class="sxs-lookup"><span data-stu-id="c36bd-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="c36bd-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="c36bd-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="c36bd-129">Źródła danych ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="c36bd-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="c36bd-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="c36bd-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="c36bd-131">NuGet wewnętrzne błędy i ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="c36bd-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="c36bd-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="c36bd-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="c36bd-133">Nieprawidłowy błędów na wejściu</span><span class="sxs-lookup"><span data-stu-id="c36bd-133">Invalid input errors</span></span>

<span data-ttu-id="c36bd-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="c36bd-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="c36bd-135">NU1001</span><span class="sxs-lookup"><span data-stu-id="c36bd-135">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-136">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-136">**Issue**</span></span> | <span data-ttu-id="c36bd-137">Projekt nie zawiera co najmniej jeden struktury.</span><span class="sxs-lookup"><span data-stu-id="c36bd-137">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="c36bd-138">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-138">**Common causes**</span></span> | <span data-ttu-id="c36bd-139">Projekt nie zawiera `TargetFramework` lub `TargetFrameworks` właściwości.</span><span class="sxs-lookup"><span data-stu-id="c36bd-139">The project doesn't contain a `TargetFramework` or `TargetFrameworks` property.</span></span> |
| <span data-ttu-id="c36bd-140">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-140">**Example message**</span></span> | <span data-ttu-id="c36bd-141">*ProjA projektu nie określa żadnych docelowych platform w c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="c36bd-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |

### <a name="nu1002"></a><span data-ttu-id="c36bd-142">NU1002</span><span class="sxs-lookup"><span data-stu-id="c36bd-142">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-143">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-143">**Issue**</span></span> | <span data-ttu-id="c36bd-144">Nieprawidłowa kombinacja danych wejściowych oraz wyczyść — słowo kluczowe.</span><span class="sxs-lookup"><span data-stu-id="c36bd-144">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="c36bd-145">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-145">**Common causes**</span></span> | <span data-ttu-id="c36bd-146">Wyczyść nie mogą być łączone z innymi elementami wejściowymi.</span><span class="sxs-lookup"><span data-stu-id="c36bd-146">CLEAR may not be combined with other inputs.</span></span> |
| <span data-ttu-id="c36bd-147">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-147">**Example message**</span></span> | <span data-ttu-id="c36bd-148">*"CLEAR" nie można używać w połączeniu z innymi wartości*</span><span class="sxs-lookup"><span data-stu-id="c36bd-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |

### <a name="nu1003"></a><span data-ttu-id="c36bd-149">NU1003</span><span class="sxs-lookup"><span data-stu-id="c36bd-149">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-150">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-150">**Issue**</span></span> | <span data-ttu-id="c36bd-151">`PackageTargetFallback`i `AssetTargetFallback` Podaj inaczej wybierania zasobów i nie mogą być używane razem.</span><span class="sxs-lookup"><span data-stu-id="c36bd-151">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="c36bd-152">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-152">**Common causes**</span></span> | <span data-ttu-id="c36bd-153">Zarówno `PackageTargetFallback` i `AssetTargetFallback` istnieje w projekcie.</span><span class="sxs-lookup"><span data-stu-id="c36bd-153">Both `PackageTargetFallback` and `AssetTargetFallback` exist in the project.</span></span> |
| <span data-ttu-id="c36bd-154">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-154">**Example message**</span></span> | <span data-ttu-id="c36bd-155">*PackageTargetFallback i AssetTargetFallback nie mogą być używane razem. Usuń odwołania PackageTargetFallback(deprecated) ze środowiska projektu.*</span><span class="sxs-lookup"><span data-stu-id="c36bd-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="c36bd-156">Brak błędów pakietu i projektu</span><span class="sxs-lookup"><span data-stu-id="c36bd-156">Missing package and project errors</span></span>

<span data-ttu-id="c36bd-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="c36bd-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="c36bd-158">NU1100</span><span class="sxs-lookup"><span data-stu-id="c36bd-158">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-159">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-159">**Issue**</span></span> | <span data-ttu-id="c36bd-160">Grupa zależności nie można rozpoznać.</span><span class="sxs-lookup"><span data-stu-id="c36bd-160">A dependency group not be resolved.</span></span> <span data-ttu-id="c36bd-161">Jest to problem rodzajowy dla typów, które nie są pakiety lub projektów.</span><span class="sxs-lookup"><span data-stu-id="c36bd-161">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="c36bd-162">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-162">**Common causes**</span></span> | <span data-ttu-id="c36bd-163">Projekt zawiera zależności elementu, który nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="c36bd-163">The project contains a dependency on an item that doesn't exist.</span></span> |
| <span data-ttu-id="c36bd-164">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-164">**Example message**</span></span> | <span data-ttu-id="c36bd-165">*Nie można rozpoznać System.Missing dla net45*</span><span class="sxs-lookup"><span data-stu-id="c36bd-165">*Unable to resolve System.Missing for net45*</span></span> |

### <a name="nu1101"></a><span data-ttu-id="c36bd-166">NU1101</span><span class="sxs-lookup"><span data-stu-id="c36bd-166">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-167">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-167">**Issue**</span></span> | <span data-ttu-id="c36bd-168">Nie można odnaleźć pakietu na wszystkich źródeł.</span><span class="sxs-lookup"><span data-stu-id="c36bd-168">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="c36bd-169">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-169">**Common causes**</span></span> | <span data-ttu-id="c36bd-170">Brak źródła poprawny pakiet lub identyfikator pakietu jest nieprawidłowa.</span><span class="sxs-lookup"><span data-stu-id="c36bd-170">The correct package source is missing or the package identifier is incorrect.</span></span> |
| <span data-ttu-id="c36bd-171">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-171">**Example message**</span></span> | <span data-ttu-id="c36bd-172">*Nie można odnaleźć pakietu System.Missing. Żadne pakiety nie istnieje z tym identyfikatorem w źródłach: dotnet core, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="c36bd-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |

### <a name="nu1102"></a><span data-ttu-id="c36bd-173">NU1102</span><span class="sxs-lookup"><span data-stu-id="c36bd-173">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-174">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-174">**Issue**</span></span> | <span data-ttu-id="c36bd-175">Identyfikator pakietu został znaleziony, lecz nie można odnaleźć wersji w zakresie określonym zależności na żadnym z źródeł.</span><span class="sxs-lookup"><span data-stu-id="c36bd-175">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> |
| <span data-ttu-id="c36bd-176">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-176">**Common causes**</span></span> | <span data-ttu-id="c36bd-177">Brak źródła poprawny pakiet lub zakres zależności jest niepoprawny.</span><span class="sxs-lookup"><span data-stu-id="c36bd-177">The correct package source is missing or the dependency range is incorrect.</span></span> <span data-ttu-id="c36bd-178">Pakiet, a użytkownik nie może być określony zakres.</span><span class="sxs-lookup"><span data-stu-id="c36bd-178">The range might be specified by a package and not the user.</span></span> <span data-ttu-id="c36bd-179">Użytkownik może być konieczne przełączenie się do wersji dostępnych w przypadku tego pakietu jest odwołuje się projekt bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="c36bd-179">The user may need to switch to an available version if this package is referenced by the project directly.</span></span> |
| <span data-ttu-id="c36bd-180">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-180">**Example message**</span></span> | <span data-ttu-id="c36bd-181">*Nie można odnaleźć pakietu NuGet.Versioning z wersją (> = 9.0.1)<br/> — wersje 30 znalezione w usłudze nuget.org [najbliższej wersji: 4.0.0]<br/> — wersje znaleziono 10 w dotnet buildtools [najbliższej wersji: 4.0.0-rc-2129]<br/> -znaleziono 9 wersje w NuGetVolatile [najbliższej wersji: 3.0.0-beta-00032]<br/> -znaleziono wersje 0 w podstawowej platformy dotnet<br/> -znaleziono wersje 0 w dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="c36bd-181">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1103"></a><span data-ttu-id="c36bd-182">NU1103</span><span class="sxs-lookup"><span data-stu-id="c36bd-182">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-183">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-183">**Issue**</span></span> | <span data-ttu-id="c36bd-184">Nie odnaleziono żadnych stabilne wersje w zakresie zależności.</span><span class="sxs-lookup"><span data-stu-id="c36bd-184">No stable versions were found in the dependency range.</span></span> <span data-ttu-id="c36bd-185">Wersje wstępne znaleziono, ale nie są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="c36bd-185">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="c36bd-186">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-186">**Common causes**</span></span> | <span data-ttu-id="c36bd-187">Projekt określony stabilną wersję dla zakresu zależności.</span><span class="sxs-lookup"><span data-stu-id="c36bd-187">The project specified a stable version for the dependency range.</span></span> <span data-ttu-id="c36bd-188">Użytkownicy muszą zmienić zakres wersji, aby uwzględnić wersje wstępne.</span><span class="sxs-lookup"><span data-stu-id="c36bd-188">Users need to change the version range to include pre-release versions.</span></span> |
| <span data-ttu-id="c36bd-189">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-189">**Example message**</span></span> | <span data-ttu-id="c36bd-190">*Nie można odnaleźć pakietu stabilna NuGet.Versioning z wersją (> = 3.0.0)<br/> — wersje znaleziono 10 w dotnet buildtools [najbliższej wersji: 4.0.0-rc-2129]<br/> -znaleziono 9 wersje w NuGetVolatile [najbliższej wersji: 3.0.0-beta-00032] <br/> -Znaleziono wersje 0 w podstawowej platformy dotnet<br/> -znaleziono wersje 0 w dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="c36bd-190">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1104"></a><span data-ttu-id="c36bd-191">NU1104</span><span class="sxs-lookup"><span data-stu-id="c36bd-191">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-192">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-192">**Issue**</span></span> | <span data-ttu-id="c36bd-193">Wskazuje element ProjectReference do pliku, który nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="c36bd-193">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="c36bd-194">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-194">**Common causes**</span></span> | <span data-ttu-id="c36bd-195">Brakuje pliku projektu z dysku lub odniesienia jest nieprawidłowa.</span><span class="sxs-lookup"><span data-stu-id="c36bd-195">The project file is missing from disk or the reference is incorrect.</span></span> |
| <span data-ttu-id="c36bd-196">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-196">**Example message**</span></span> | <span data-ttu-id="c36bd-197">*Odwołanie do projektu nie istnieje "c:\a.csproj". Sprawdź, czy odwołanie do projektu jest prawidłowa i czy istnieje plik projektu.*</span><span class="sxs-lookup"><span data-stu-id="c36bd-197">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |

### <a name="nu1105"></a><span data-ttu-id="c36bd-198">NU1105</span><span class="sxs-lookup"><span data-stu-id="c36bd-198">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-199">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-199">**Issue**</span></span> | <span data-ttu-id="c36bd-200">Plik projektu istnieje, ale go nie dostarczono żadnych informacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="c36bd-200">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="c36bd-201">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-201">**Common causes**</span></span> | <span data-ttu-id="c36bd-202">W programie Visual Studio to może oznaczać, że projekt jest zwolniony.</span><span class="sxs-lookup"><span data-stu-id="c36bd-202">In Visual Studio this could mean that the project is unloaded.</span></span> <span data-ttu-id="c36bd-203">W wierszu polecenia to może oznaczać, że plik jest uszkodzony lub nie zawiera niestandardowego po elemencie docelowym importów potrzebne do odzyskiwania do odczytu projektu.</span><span class="sxs-lookup"><span data-stu-id="c36bd-203">From the command line this could mean that the file is corrupt or that it doesn't contain the custom after imports target needed for restore to read the project.</span></span> |
| <span data-ttu-id="c36bd-204">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-204">**Example message**</span></span> | <span data-ttu-id="c36bd-205">*Nie można odczytać informacji o projekcie dla "c:\a.csproj". Plik projektu może być nieprawidłowe lub brakujące elementy docelowe, wymaganych do przywrócenia.*</span><span class="sxs-lookup"><span data-stu-id="c36bd-205">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

### <a name="nu1106"></a><span data-ttu-id="c36bd-206">NU1106</span><span class="sxs-lookup"><span data-stu-id="c36bd-206">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-207">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-207">**Issue**</span></span> | <span data-ttu-id="c36bd-208">Nie można rozpoznać zależności ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="c36bd-208">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="c36bd-209">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-209">**Common causes**</span></span> | <span data-ttu-id="c36bd-210">Pakiety zawierają zależność od dokładnej wersji pakietu zamiast nieograniczoną zakresów.</span><span class="sxs-lookup"><span data-stu-id="c36bd-210">Packages contain dependency on exact versions of a package instead of open-ended ranges.</span></span> |
| <span data-ttu-id="c36bd-211">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-211">**Example message**</span></span> | <span data-ttu-id="c36bd-212">*Nie można zrealizować żądań będących w konflikcie dla {id}: {konflikt path} Framework: {docelowy wykres}*</span><span class="sxs-lookup"><span data-stu-id="c36bd-212">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |

<a name="nu1107"></a> 

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="c36bd-213">NU1107 (wcześniej NU1607)</span><span class="sxs-lookup"><span data-stu-id="c36bd-213">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-214">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-214">**Issue**</span></span> | <span data-ttu-id="c36bd-215">Nie można rozpoznać ograniczenia zależności między pakietami.</span><span class="sxs-lookup"><span data-stu-id="c36bd-215">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="c36bd-216">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-216">**Common causes**</span></span> | <span data-ttu-id="c36bd-217">Pakiety z ograniczeniami zależności na dokładną wersję nie zezwalają na inne pakiety w razie potrzeby zwiększyć wersji.</span><span class="sxs-lookup"><span data-stu-id="c36bd-217">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> |
| <span data-ttu-id="c36bd-218">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-218">**Example message**</span></span> | <span data-ttu-id="c36bd-219">*Konflikt wersji dla NuGet.Versioning wykryte. Pakiet odwoływać się bezpośrednio z projektu, aby rozwiązać ten problem.<br/>  NuGet.Versioning (= 3.5.0) -> NuGet.Packaging 3.5.0<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="c36bd-219">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="c36bd-220">NU1108 (wcześniej NU1606)</span><span class="sxs-lookup"><span data-stu-id="c36bd-220">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-221">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-221">**Issue**</span></span> | <span data-ttu-id="c36bd-222">Wykryto zależność cykliczną.</span><span class="sxs-lookup"><span data-stu-id="c36bd-222">A circular dependency was detected.</span></span> |
| <span data-ttu-id="c36bd-223">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-223">**Common causes**</span></span> | <span data-ttu-id="c36bd-224">Pakiet jest autoryzowane.</span><span class="sxs-lookup"><span data-stu-id="c36bd-224">A package is authored incorrectly.</span></span> |
| <span data-ttu-id="c36bd-225">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-225">**Example message**</span></span> | <span data-ttu-id="c36bd-226">*Wykryto cykl: A -> B -> A*</span><span class="sxs-lookup"><span data-stu-id="c36bd-226">*Cycle detected: A -> B -> A*</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="c36bd-227">Błędy zgodności</span><span class="sxs-lookup"><span data-stu-id="c36bd-227">Compatibility errors</span></span>

<span data-ttu-id="c36bd-228">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="c36bd-228">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="c36bd-229">NU1201</span><span class="sxs-lookup"><span data-stu-id="c36bd-229">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-230">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-230">**Issue**</span></span> | <span data-ttu-id="c36bd-231">Zależności projektu nie zawiera struktury zgodne z bieżącego projektu.</span><span class="sxs-lookup"><span data-stu-id="c36bd-231">A dependency project doesn't contain a framework compatible with the current project.</span></span> |
| <span data-ttu-id="c36bd-232">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-232">**Common causes**</span></span> | <span data-ttu-id="c36bd-233">Platforma docelowa projektu jest wyższą wersję niż odbierającą projektu.</span><span class="sxs-lookup"><span data-stu-id="c36bd-233">The project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="c36bd-234">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-234">**Example message**</span></span> | <span data-ttu-id="c36bd-235">*ServerWeb projektu nie jest zgodny z netstandard1.3 (. Krótkich nazw NETStandard, Version = w wersji 1.3). Projekt obsługuje ServerWeb:<br/> -netstandard1.6 (. Krótkich nazw NETStandard, Version = w wersji 1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = 1.0)*</span><span class="sxs-lookup"><span data-stu-id="c36bd-235">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |

### <a name="nu1202"></a><span data-ttu-id="c36bd-236">NU1202</span><span class="sxs-lookup"><span data-stu-id="c36bd-236">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-237">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-237">**Issue**</span></span> | <span data-ttu-id="c36bd-238">Pakiet zależności nie zawiera żadnych zasobów, które są zgodne z projektem.</span><span class="sxs-lookup"><span data-stu-id="c36bd-238">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="c36bd-239">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-239">**Common causes**</span></span> | <span data-ttu-id="c36bd-240">Pakiet nie obsługuje platformy docelowej projektu.</span><span class="sxs-lookup"><span data-stu-id="c36bd-240">The package doesn't support the project's target framework.</span></span> |
| <span data-ttu-id="c36bd-241">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-241">**Example message**</span></span> | <span data-ttu-id="c36bd-242">*Pakiet System.ComponentModel.EventBasedAsync 4.0.11 nie jest zgodny z netstandard1.3 (. Krótkich nazw NETStandard, Version = w wersji 1.3). Pakiet obsługuje System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, wersja = 1.0)<br/> -monotouch10 (MonoTouch, wersja = 1.0)<br/> -net45 (. NETFramework, Version = 4.5)<br/> -netcore50 (. NETCore, Version = v5.0)<br/> -netstandard1.0 (. Krótkich nazw NETStandard, Version = 1.0)<br/> -przenośny net45 + win8 + wp8 + wpa81 (. NETPortable, wersja = v0.0, profil = Profile259)<br/> — Windows 8 (Windows, wersja = w wersji 8.0)<br/> -wp8 (WindowsPhone, wersja = w wersji 8.0)<br/> -wpa81 (WindowsPhoneApp, wersja = v8.1)<br/> — xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="c36bd-242">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|

### <a name="nu1203"></a><span data-ttu-id="c36bd-243">NU1203</span><span class="sxs-lookup"><span data-stu-id="c36bd-243">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-244">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-244">**Issue**</span></span> | <span data-ttu-id="c36bd-245">Pakiet nie obsługuje projektu `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="c36bd-245">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="c36bd-246">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-246">**Common causes**</span></span> | <span data-ttu-id="c36bd-247">Pakiet nie obsługuje bieżącej `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="c36bd-247">The package doesn't support the current `RuntimeIdentifier`.</span></span> <span data-ttu-id="c36bd-248">Zmień `RuntimeIdentifier` wartości używanych w projekcie, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c36bd-248">Change the `RuntimeIdentifier` values used in the project if needed.</span></span> |
| <span data-ttu-id="c36bd-249">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-249">**Example message**</span></span> | <span data-ttu-id="c36bd-250">*System.Example 1.0.0 udostępnia zestaw odwołania czasu kompilowania dla a.dll na net461, ale nie nie zgodny zestaw czasu wykonywania.*</span><span class="sxs-lookup"><span data-stu-id="c36bd-250">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |

### <a name="nu1401"></a><span data-ttu-id="c36bd-251">NU1401</span><span class="sxs-lookup"><span data-stu-id="c36bd-251">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-252">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-252">**Issue**</span></span> | <span data-ttu-id="c36bd-253">Pakiet wymaga funkcji lub struktur nie są obecnie obsługiwane przez zainstalowaną wersję programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="c36bd-253">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="c36bd-254">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-254">**Common causes**</span></span> | <span data-ttu-id="c36bd-255">Uaktualnij program NuGet, aby rozwiązać problem.</span><span class="sxs-lookup"><span data-stu-id="c36bd-255">Upgrade NuGet to fix the issue.</span></span> |
| <span data-ttu-id="c36bd-256">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-256">**Example message**</span></span> | <span data-ttu-id="c36bd-257">*Pakiet "NuGet.Versioning" wymaga wersji klienta "5.0.0" NuGet lub nowszej, ale bieżąca wersja NuGet to "4.3.0". Aby uaktualnić narzędzie NuGet, przejdź do http://docs.nuget.org/consume/installing-nuget.*</span><span class="sxs-lookup"><span data-stu-id="c36bd-257">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'. To upgrade NuGet, please go to http://docs.nuget.org/consume/installing-nuget.*</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="c36bd-258">Nieprawidłowy wejściowy ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="c36bd-258">Invalid input warnings</span></span>

<span data-ttu-id="c36bd-259">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="c36bd-259">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="c36bd-260">NU1501</span><span class="sxs-lookup"><span data-stu-id="c36bd-260">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-261">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-261">**Issue**</span></span> | <span data-ttu-id="c36bd-262">Przywracanie projektu próbuje działać na nie został znaleziony.</span><span class="sxs-lookup"><span data-stu-id="c36bd-262">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="c36bd-263">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-263">**Common causes**</span></span> | <span data-ttu-id="c36bd-264">Brak projektu.</span><span class="sxs-lookup"><span data-stu-id="c36bd-264">The project is missing.</span></span> |
| <span data-ttu-id="c36bd-265">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-265">**Example message**</span></span> | <span data-ttu-id="c36bd-266">*Folder "c:\projects\a" nie zawiera projektu do przywrócenia.*</span><span class="sxs-lookup"><span data-stu-id="c36bd-266">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |

### <a name="nu1502"></a><span data-ttu-id="c36bd-267">NU1502</span><span class="sxs-lookup"><span data-stu-id="c36bd-267">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-268">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-268">**Issue**</span></span> | <span data-ttu-id="c36bd-269">`RuntimeSupports`zawiera nieprawidłowy profil.</span><span class="sxs-lookup"><span data-stu-id="c36bd-269">`RuntimeSupports` contains an invalid profile.</span></span> |
| <span data-ttu-id="c36bd-270">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-270">**Common causes**</span></span> | <span data-ttu-id="c36bd-271">Nie znaleziono profilu obsługuje w `runtime.json` plik z bieżącego zależności pakietów.</span><span class="sxs-lookup"><span data-stu-id="c36bd-271">The supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span> |
| <span data-ttu-id="c36bd-272">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-272">**Example message**</span></span> | <span data-ttu-id="c36bd-273">*Profil zgodności nieznany: aaa*</span><span class="sxs-lookup"><span data-stu-id="c36bd-273">*Unknown Compatibility Profile: aaa*</span></span> |

### <a name="nu1503"></a><span data-ttu-id="c36bd-274">NU1503</span><span class="sxs-lookup"><span data-stu-id="c36bd-274">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-275">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-275">**Issue**</span></span> | <span data-ttu-id="c36bd-276">Zależności projektu nie importuje obiekty docelowe przywracania NuGet.</span><span class="sxs-lookup"><span data-stu-id="c36bd-276">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="c36bd-277">Ten jest podobny do NU1105, ale w tym miejscu projektu zostanie pominięty i zignorowany zamiast powoduje wszystkie przywracania się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="c36bd-277">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="c36bd-278">W złożonych rozwiązań są często innych typów projektów, które mogą nie obsługiwać przywracania.</span><span class="sxs-lookup"><span data-stu-id="c36bd-278">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="c36bd-279">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-279">**Common causes**</span></span> | <span data-ttu-id="c36bd-280">Może to nastąpić dla projektów, które nie należy importować wspólne właściwości/cele, które są automatycznie importowane przywracania.</span><span class="sxs-lookup"><span data-stu-id="c36bd-280">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="c36bd-281">Jeśli projekt nie trzeba przywrócić możesz go zignorować.</span><span class="sxs-lookup"><span data-stu-id="c36bd-281">If the project doesn't need to be restored this can be ignored.</span></span> |
| <span data-ttu-id="c36bd-282">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-282">**Example message**</span></span> | <span data-ttu-id="c36bd-283">*Pomijanie przywracania dla projektu "c:\a.csproj". Plik projektu może być nieprawidłowe lub brakujące elementy docelowe, wymaganych do przywrócenia.*</span><span class="sxs-lookup"><span data-stu-id="c36bd-283">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="c36bd-284">Nieoczekiwany pakietu wersji ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="c36bd-284">Unexpected package version warnings</span></span>

<span data-ttu-id="c36bd-285">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="c36bd-285">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="c36bd-286">NU1601</span><span class="sxs-lookup"><span data-stu-id="c36bd-286">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-287">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-287">**Issue**</span></span> | <span data-ttu-id="c36bd-288">Zależności bezpośrednich projektu był upadku na wyższą wersję niż określonego projektu.</span><span class="sxs-lookup"><span data-stu-id="c36bd-288">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="c36bd-289">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-289">**Common causes**</span></span> | <span data-ttu-id="c36bd-290">Inny pakiet zależności wymagane wyższą wersję i upadku pakietu w.</span><span class="sxs-lookup"><span data-stu-id="c36bd-290">Another dependency package required a higher version and bumped the package up.</span></span> |
| <span data-ttu-id="c36bd-291">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-291">**Example message**</span></span> | <span data-ttu-id="c36bd-292">*Określoną zależnością było NuGet.Versioning (> = 3.5.0), ale ostatecznie otrzymano NuGet.Versioning 4.0.0.*</span><span class="sxs-lookup"><span data-stu-id="c36bd-292">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |

### <a name="nu1602"></a><span data-ttu-id="c36bd-293">NU1602</span><span class="sxs-lookup"><span data-stu-id="c36bd-293">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-294">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-294">**Issue**</span></span> | <span data-ttu-id="c36bd-295">Zależność pakietu brak dolnej granicy.</span><span class="sxs-lookup"><span data-stu-id="c36bd-295">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="c36bd-296">To nie zezwala na przywracania znaleźć *najlepszego dopasowania*.</span><span class="sxs-lookup"><span data-stu-id="c36bd-296">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="c36bd-297">Każdy przywracania będzie przestawiany dół próby znalezienia starszej wersji, który może być używany.</span><span class="sxs-lookup"><span data-stu-id="c36bd-297">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="c36bd-298">Oznacza to, że przywracanie przejdzie do trybu online, aby sprawdzić wszystkie źródła zawsze zamiast pakietów, które już istnieją w folderze pakietów użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c36bd-298">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="c36bd-299">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-299">**Common causes**</span></span> | <span data-ttu-id="c36bd-300">Jest to zazwyczaj błąd tworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="c36bd-300">This is usually a package authoring error.</span></span> |
| <span data-ttu-id="c36bd-301">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-301">**Example message**</span></span> | <span data-ttu-id="c36bd-302">*NuGet.Packaging 4.0.0 nie zapewnia włącznie dolna granica dla zależności NuGet.Versioning (> 3.5.0). Przybliżony najlepsze dopasowanie 3.6.0 został rozwiązany.*</span><span class="sxs-lookup"><span data-stu-id="c36bd-302">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |

### <a name="nu1603"></a><span data-ttu-id="c36bd-303">NU1603</span><span class="sxs-lookup"><span data-stu-id="c36bd-303">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-304">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-304">**Issue**</span></span> | <span data-ttu-id="c36bd-305">Zależność pakietu określonej wersji, którego nie można odnaleźć.</span><span class="sxs-lookup"><span data-stu-id="c36bd-305">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="c36bd-306">Nowsza wersja użyto zamiast tego, który różni się od pakietu opracowania przed.</span><span class="sxs-lookup"><span data-stu-id="c36bd-306">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="c36bd-307">Oznacza to, że przywracanie nie znalazł *najlepszego dopasowania*.</span><span class="sxs-lookup"><span data-stu-id="c36bd-307">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="c36bd-308">Każdy przywracania będzie przestawiany dół próby znalezienia starszej wersji, który może być używany.</span><span class="sxs-lookup"><span data-stu-id="c36bd-308">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="c36bd-309">Oznacza to, że przywracanie przejdzie do trybu online, aby sprawdzić wszystkie źródła zawsze zamiast pakietów, które już istnieją w folderze pakietów użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c36bd-309">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="c36bd-310">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-310">**Common causes**</span></span> | <span data-ttu-id="c36bd-311">Źródła pakietu nie zawierają wersja oczekiwana dolnej granicy.</span><span class="sxs-lookup"><span data-stu-id="c36bd-311">The package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="c36bd-312">Jeśli nie zostało zwolnione pakietu oczekiwano może to być błąd tworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="c36bd-312">If the package expected has not been released then this may be a package authoring error.</span></span> |
| <span data-ttu-id="c36bd-313">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-313">**Example message**</span></span> | <span data-ttu-id="c36bd-314">NuGet.Packaging 4.0.0 zależy od NuGet.Versioning (> = 4.0.0), ale nie można odnaleźć 4.0.0.</span><span class="sxs-lookup"><span data-stu-id="c36bd-314">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="c36bd-315">Przybliżony najlepsze dopasowanie 5.0.0 został rozwiązany.</span><span class="sxs-lookup"><span data-stu-id="c36bd-315">An approximate best match of 5.0.0 was resolved.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="c36bd-316">NU1604</span><span class="sxs-lookup"><span data-stu-id="c36bd-316">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-317">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-317">**Issue**</span></span> | <span data-ttu-id="c36bd-318">Zależności projektu nie definiuje dolną granicą.</span><span class="sxs-lookup"><span data-stu-id="c36bd-318">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="c36bd-319">Oznacza to, że przywracanie nie znalazł *najlepszego dopasowania*.</span><span class="sxs-lookup"><span data-stu-id="c36bd-319">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="c36bd-320">Każdy przywracania będzie przestawiany dół próby znalezienia starszej wersji, który może być używany.</span><span class="sxs-lookup"><span data-stu-id="c36bd-320">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="c36bd-321">Oznacza to, że przywracanie przejdzie do trybu online, aby sprawdzić wszystkie źródła zawsze zamiast pakietów, które już istnieją w folderze pakietów użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c36bd-321">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="c36bd-322">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-322">**Common causes**</span></span> | <span data-ttu-id="c36bd-323">Projektu *PackageReference* *wersji* można zaktualizować atrybutu, aby uwzględnić dolną granicą.</span><span class="sxs-lookup"><span data-stu-id="c36bd-323">The project's *PackageReference* *Version* attribute should be updated to include a lower bound.</span></span> |
| <span data-ttu-id="c36bd-324">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-324">**Example message**</span></span> | <span data-ttu-id="c36bd-325">*Projekt zależności NuGet.Versioning (< = od 9.0.0) Nowak zawiera włącznie dolnej granicy. Dolna granica należy uwzględnić w wersji zależności, aby zapewnić wyniki przywracania na poziomie.*</span><span class="sxs-lookup"><span data-stu-id="c36bd-325">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |

### <a name="nu1605"></a><span data-ttu-id="c36bd-326">NU1605</span><span class="sxs-lookup"><span data-stu-id="c36bd-326">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-327">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-327">**Issue**</span></span> | <span data-ttu-id="c36bd-328">Pakiet zależności określić ograniczenia wersji za pomocą nowszej wersji pakietu niż przywracania ostatecznie rozwiązane.</span><span class="sxs-lookup"><span data-stu-id="c36bd-328">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> |
| <span data-ttu-id="c36bd-329">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-329">**Common causes**</span></span> | <span data-ttu-id="c36bd-330">Najbliższej wins podczas rozpoznawania pakietów.</span><span class="sxs-lookup"><span data-stu-id="c36bd-330">Nearest wins when resolving packages.</span></span> <span data-ttu-id="c36bd-331">Bliżej położonego pakietu na wykresie mogą mieć zastąpione odległymi pakiet.</span><span class="sxs-lookup"><span data-stu-id="c36bd-331">A nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="c36bd-332">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-332">**Example message**</span></span> | <span data-ttu-id="c36bd-333">*Wykryto starszą wersję pakietu: NuGet.Versioning z 4.0.0 do 3.5.0. Odwoływać się bezpośrednio z projektu, aby wybrać inną wersję pakietu.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="c36bd-333">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="c36bd-334">Mechanizm rozpoznawania konfliktu ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="c36bd-334">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="c36bd-335">NU1608</span><span class="sxs-lookup"><span data-stu-id="c36bd-335">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-336">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-336">**Issue**</span></span> | <span data-ttu-id="c36bd-337">Usuń pakiet jest większa niż umożliwia ograniczenie zależności.</span><span class="sxs-lookup"><span data-stu-id="c36bd-337">A resolve package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="c36bd-338">W niektórych przypadkach jest to zamierzone i można pominąć to ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="c36bd-338">In some cases this is intentional and the warning can be suppressed.</span></span> |
| <span data-ttu-id="c36bd-339">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-339">**Common causes**</span></span> | <span data-ttu-id="c36bd-340">Pakiet bezpośrednio odwołuje się projekt spowoduje zastąpienie ograniczenia zależności z innymi pakietami.</span><span class="sxs-lookup"><span data-stu-id="c36bd-340">A package referenced directly by a project will override dependency constraints from other packages.</span></span>   |
| <span data-ttu-id="c36bd-341">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-341">**Example message**</span></span> | <span data-ttu-id="c36bd-342">*Wersja pakietu wykrytych poza ograniczenia zależności: x 1.0.0 wymaga y (= 1.0.0), ale wersja y 2.0.0 został rozwiązany.*</span><span class="sxs-lookup"><span data-stu-id="c36bd-342">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="c36bd-343">Ostrzeżenia rezerwowy pakietu</span><span class="sxs-lookup"><span data-stu-id="c36bd-343">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="c36bd-344">NU1701</span><span class="sxs-lookup"><span data-stu-id="c36bd-344">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-345">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-345">**Issue**</span></span> | <span data-ttu-id="c36bd-346">*PackageTargetFallback/AssetTargetFallback* zostało użyte do wybrania zasoby z pakietu.</span><span class="sxs-lookup"><span data-stu-id="c36bd-346">*PackageTargetFallback/AssetTargetFallback* was used to select assets from a package.</span></span> <span data-ttu-id="c36bd-347">To ostrzeżenie, aby umożliwić użytkownikowi wiedzieć, że zasoby nie mogą być 100% zgodny.</span><span class="sxs-lookup"><span data-stu-id="c36bd-347">This is a warning to let the user know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="c36bd-348">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-348">**Common causes**</span></span> | <span data-ttu-id="c36bd-349">Pakiet nie obsługuje platformy projektu.</span><span class="sxs-lookup"><span data-stu-id="c36bd-349">The package doesn't support the project framework.</span></span> |
| <span data-ttu-id="c36bd-350">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-350">**Example message**</span></span> | <span data-ttu-id="c36bd-351">*Pakiet "NuGet.Versioning" został przywrócony przy użyciu "portable net45 + win8" zamiast platformy docelowej projektu "netstandard1.5". Ten pakiet nie może być całkowicie zgodne z projektem.*</span><span class="sxs-lookup"><span data-stu-id="c36bd-351">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="c36bd-352">Źródła danych ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="c36bd-352">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="c36bd-353">NU1801</span><span class="sxs-lookup"><span data-stu-id="c36bd-353">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-354">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-354">**Issue**</span></span> | <span data-ttu-id="c36bd-355">Wystąpił błąd podczas odczytywania źródła po `IgnoreFailedSources` jest ustawiona na wartość true, konwersją niekrytyczny ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="c36bd-355">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="c36bd-356">To może zawierać żadnych komunikatów i jest rodzajowy.</span><span class="sxs-lookup"><span data-stu-id="c36bd-356">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="c36bd-357">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-357">**Common causes**</span></span> | <span data-ttu-id="c36bd-358">Źródło jest nieprawidłowe.</span><span class="sxs-lookup"><span data-stu-id="c36bd-358">The source is invalid.</span></span> |
| <span data-ttu-id="c36bd-359">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="c36bd-359">**Example message**</span></span> | <span data-ttu-id="c36bd-360">n/d</span><span class="sxs-lookup"><span data-stu-id="c36bd-360">n/a</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="c36bd-361">NuGet wewnętrzne błędy i ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="c36bd-361">NuGet internal errors and warnings</span></span>

<span data-ttu-id="c36bd-362">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="c36bd-362">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="c36bd-363">NU1000</span><span class="sxs-lookup"><span data-stu-id="c36bd-363">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-364">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-364">**Issue**</span></span> | <span data-ttu-id="c36bd-365">Nieokreślony błąd wewnętrzny z pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="c36bd-365">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="c36bd-366">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-366">**Common causes**</span></span> | <span data-ttu-id="c36bd-367">Sprawdź dzienniki, aby uzyskać więcej informacji</span><span class="sxs-lookup"><span data-stu-id="c36bd-367">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="c36bd-368">NU1500</span><span class="sxs-lookup"><span data-stu-id="c36bd-368">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c36bd-369">**Problem**</span><span class="sxs-lookup"><span data-stu-id="c36bd-369">**Issue**</span></span> | <span data-ttu-id="c36bd-370">Nieokreślony ostrzeżenie wewnętrzny z pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="c36bd-370">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="c36bd-371">**Typowe przyczyny**</span><span class="sxs-lookup"><span data-stu-id="c36bd-371">**Common causes**</span></span> | <span data-ttu-id="c36bd-372">Sprawdź dzienniki, aby uzyskać więcej informacji</span><span class="sxs-lookup"><span data-stu-id="c36bd-372">Check the logs for more information</span></span> |
