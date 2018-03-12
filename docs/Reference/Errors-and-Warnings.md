---
title: "NuGet błędy i ostrzeżenia odwołania | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Pełną dokumentację dla ostrzeżeń i błędów wystawiony na podstawie NuGet podczas różne operacje NuGet."
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
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: 59bbe37d1a965e5167800148603869645fc5e0b2
ms.sourcegitcommit: df21fe770900644d476d51622a999597a6f20ef8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/12/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="43672-104">Błędy i ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="43672-104">Errors and warnings</span></span>

<span data-ttu-id="43672-105">W 4.3.0+ NuGet błędy i ostrzeżenia są numerowane zgodnie z opisem w tym temacie i zawierają szczegółowe informacje pozwalające rozwiązać problemy związane z.</span><span class="sxs-lookup"><span data-stu-id="43672-105">In NuGet 4.3.0+, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span>

<span data-ttu-id="43672-106">Błędy i ostrzeżenia wymienione w tym miejscu są dostępne tylko w przypadku [na podstawie PackageReference](../consume-packages/package-references-in-project-files.md) projektów i NuGet 4.3.0+.</span><span class="sxs-lookup"><span data-stu-id="43672-106">The errors and warnings listed here are available only with [PackageReference-based](../consume-packages/package-references-in-project-files.md) projects and NuGet 4.3.0+.</span></span> <span data-ttu-id="43672-107">NuGet honoruje także właściwości programu MSBuild tłumienie ostrzeżeń lub podniesienie ich poziomu błędy.</span><span class="sxs-lookup"><span data-stu-id="43672-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="43672-108">Aby uzyskać więcej informacji, zobacz [porady: pomijanie ostrzeżeń kompilatora](/visualstudio/ide/how-to-suppress-compiler-warnings) w dokumentacji programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="43672-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="43672-109">**Błędy**</span><span class="sxs-lookup"><span data-stu-id="43672-109">**Errors**</span></span>

| <span data-ttu-id="43672-110">Grupa</span><span class="sxs-lookup"><span data-stu-id="43672-110">Group</span></span> | <span data-ttu-id="43672-111">Błąd liczby</span><span class="sxs-lookup"><span data-stu-id="43672-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="43672-112">Nieprawidłowy błędów na wejściu</span><span class="sxs-lookup"><span data-stu-id="43672-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="43672-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="43672-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="43672-114">Brak błędów pakietu i projektu</span><span class="sxs-lookup"><span data-stu-id="43672-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="43672-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (wcześniej NU1607) [NU1108](#nu1108) (wcześniej NU1606)</span><span class="sxs-lookup"><span data-stu-id="43672-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="43672-116">Błędy zgodności</span><span class="sxs-lookup"><span data-stu-id="43672-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="43672-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="43672-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="43672-118">**Ostrzeżenia**</span><span class="sxs-lookup"><span data-stu-id="43672-118">**Warnings**</span></span>

| <span data-ttu-id="43672-119">Grupa</span><span class="sxs-lookup"><span data-stu-id="43672-119">Group</span></span> | <span data-ttu-id="43672-120">Numery ostrzeżeń</span><span class="sxs-lookup"><span data-stu-id="43672-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="43672-121">Nieprawidłowy wejściowy ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="43672-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="43672-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="43672-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="43672-123">Nieoczekiwany pakietu wersji ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="43672-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="43672-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="43672-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="43672-125">Mechanizm rozpoznawania konfliktu ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="43672-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="43672-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="43672-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="43672-127">Ostrzeżenia rezerwowy pakietu</span><span class="sxs-lookup"><span data-stu-id="43672-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="43672-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="43672-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="43672-129">Źródła danych ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="43672-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="43672-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="43672-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="43672-131">NuGet wewnętrzne błędy i ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="43672-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="43672-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="43672-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |
| [<span data-ttu-id="43672-133">Podpisanych pakietów (tworzenia i weryfikacji)</span><span class="sxs-lookup"><span data-stu-id="43672-133">Signed packages (creation and verification)</span></span>](#signed-packages-creation-and-verification)| <span data-ttu-id="43672-134">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="43672-134">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="43672-135">Nieprawidłowy błędów na wejściu</span><span class="sxs-lookup"><span data-stu-id="43672-135">Invalid input errors</span></span>

<span data-ttu-id="43672-136">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="43672-136">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="43672-137">NU1001</span><span class="sxs-lookup"><span data-stu-id="43672-137">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-138">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-138">**Issue**</span></span> | <span data-ttu-id="43672-139">Projekt nie zawiera co najmniej jeden struktury.</span><span class="sxs-lookup"><span data-stu-id="43672-139">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="43672-140">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-140">**Example message**</span></span> | <span data-ttu-id="43672-141">*ProjA projektu nie określa żadnych docelowych platform w c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="43672-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |
| <span data-ttu-id="43672-142">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-142">**Solution**</span></span> | <span data-ttu-id="43672-143">Dodaj `TargetFramework` lub `TargetFrameworks` właściwości do pliku określonego projektu.</span><span class="sxs-lookup"><span data-stu-id="43672-143">Add a `TargetFramework` or `TargetFrameworks` property to the specified project file.</span></span> |

### <a name="nu1002"></a><span data-ttu-id="43672-144">NU1002</span><span class="sxs-lookup"><span data-stu-id="43672-144">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-145">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-145">**Issue**</span></span> | <span data-ttu-id="43672-146">Nieprawidłowa kombinacja danych wejściowych oraz wyczyść — słowo kluczowe.</span><span class="sxs-lookup"><span data-stu-id="43672-146">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="43672-147">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-147">**Example message**</span></span> | <span data-ttu-id="43672-148">*"CLEAR" nie można używać w połączeniu z innymi wartości*</span><span class="sxs-lookup"><span data-stu-id="43672-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |
| <span data-ttu-id="43672-149">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-149">**Solution**</span></span> | <span data-ttu-id="43672-150">Użyj wyczyść samodzielnie i pominąć wszystkie inne dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="43672-150">Use CLEAR by itself and omit all other inputs.</span></span> |

### <a name="nu1003"></a><span data-ttu-id="43672-151">NU1003</span><span class="sxs-lookup"><span data-stu-id="43672-151">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-152">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-152">**Issue**</span></span> | <span data-ttu-id="43672-153">`PackageTargetFallback` i `AssetTargetFallback` Podaj inaczej wybierania zasobów i nie mogą być używane razem.</span><span class="sxs-lookup"><span data-stu-id="43672-153">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="43672-154">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-154">**Example message**</span></span> | <span data-ttu-id="43672-155">*PackageTargetFallback i AssetTargetFallback nie mogą być używane razem. Usuń odwołania PackageTargetFallback(deprecated) ze środowiska projektu.*</span><span class="sxs-lookup"><span data-stu-id="43672-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |
| <span data-ttu-id="43672-156">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-156">**Solution**</span></span> | <span data-ttu-id="43672-157">Usuń przestarzałe `PackageTargetFallback` elementu z projektu.</span><span class="sxs-lookup"><span data-stu-id="43672-157">Remove the deprecated `PackageTargetFallback` element from the project.</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="43672-158">Brak błędów pakietu i projektu</span><span class="sxs-lookup"><span data-stu-id="43672-158">Missing package and project errors</span></span>

<span data-ttu-id="43672-159">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="43672-159">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="43672-160">NU1100</span><span class="sxs-lookup"><span data-stu-id="43672-160">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-161">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-161">**Issue**</span></span> | <span data-ttu-id="43672-162">Grupa zależności nie można rozpoznać.</span><span class="sxs-lookup"><span data-stu-id="43672-162">A dependency group not be resolved.</span></span> <span data-ttu-id="43672-163">Jest to problem rodzajowy dla typów, które nie są pakiety lub projektów.</span><span class="sxs-lookup"><span data-stu-id="43672-163">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="43672-164">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-164">**Example message**</span></span> | <span data-ttu-id="43672-165">*Nie można rozpoznać System.Missing dla net45*</span><span class="sxs-lookup"><span data-stu-id="43672-165">*Unable to resolve System.Missing for net45*</span></span> |
| <span data-ttu-id="43672-166">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-166">**Solution**</span></span> | <span data-ttu-id="43672-167">Otwórz plik projektu i sprawdź, czy lista jego zależności.</span><span class="sxs-lookup"><span data-stu-id="43672-167">Open the project file and examine the list of its dependencies.</span></span> <span data-ttu-id="43672-168">Sprawdź, czy poszczególne zależności istnieje na źródła pakietów, którego używasz, i że pakiet obsługuje platforma docelowa projektu.</span><span class="sxs-lookup"><span data-stu-id="43672-168">Check that each dependency exists on the package sources you're using, and that the package supports the project's target framework.</span></span> |

### <a name="nu1101"></a><span data-ttu-id="43672-169">NU1101</span><span class="sxs-lookup"><span data-stu-id="43672-169">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-170">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-170">**Issue**</span></span> | <span data-ttu-id="43672-171">Nie można odnaleźć pakietu na wszystkich źródeł.</span><span class="sxs-lookup"><span data-stu-id="43672-171">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="43672-172">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-172">**Example message**</span></span> | <span data-ttu-id="43672-173">*Nie można odnaleźć pakietu System.Missing. Żadne pakiety nie istnieje z tym identyfikatorem w źródłach: dotnet core, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="43672-173">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |
| <span data-ttu-id="43672-174">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-174">**Solution**</span></span> | <span data-ttu-id="43672-175">Sprawdź, czy zależności projektu w programie Visual Studio należy upewnić się, że używasz pakietu poprawny identyfikator i numer wersji.</span><span class="sxs-lookup"><span data-stu-id="43672-175">Examine the project's dependencies in Visual Studio to be sure you're using the correct package identifier and version number.</span></span> <span data-ttu-id="43672-176">Sprawdź także, czy [Konfiguracja nuget projektu](../consume-packages/Configuring-NuGet-Behavior.md) identyfikuje źródła pakietów w sieci spodziewać się przy użyciu.</span><span class="sxs-lookup"><span data-stu-id="43672-176">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="43672-177">Jeśli używasz pakiety, które mają [Wersjonowania semantycznego 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), upewnij się, że używasz [V3 źródła](https://api.nuget.org/v3/index.json) w [Konfiguracja nuget projektu](../consume-packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="43672-177">If you use packages that have [Semantic Versioning 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), please make sure that you are using the [V3 feed](https://api.nuget.org/v3/index.json) in the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> |

### <a name="nu1102"></a><span data-ttu-id="43672-178">NU1102</span><span class="sxs-lookup"><span data-stu-id="43672-178">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-179">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-179">**Issue**</span></span> | <span data-ttu-id="43672-180">Identyfikator pakietu został znaleziony, lecz nie można odnaleźć wersji w zakresie określonym zależności na żadnym z źródeł.</span><span class="sxs-lookup"><span data-stu-id="43672-180">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> <span data-ttu-id="43672-181">Pakiet, a użytkownik nie może być określony zakres.</span><span class="sxs-lookup"><span data-stu-id="43672-181">The range might be specified by a package and not the user.</span></span> |
| <span data-ttu-id="43672-182">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-182">**Example message**</span></span> | <span data-ttu-id="43672-183">*Nie można odnaleźć pakietu NuGet.Versioning z wersją (> = 9.0.1)<br/> — wersje 30 znalezione w usłudze nuget.org [najbliższej wersji: 4.0.0]<br/> — wersje znaleziono 10 w dotnet buildtools [najbliższej wersji: 4.0.0-rc-2129]<br/> -znaleziono 9 wersje w NuGetVolatile [najbliższej wersji: 3.0.0-beta-00032]<br/> -znaleziono wersje 0 w podstawowej platformy dotnet<br/> -znaleziono wersje 0 w dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="43672-183">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="43672-184">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-184">**Solution**</span></span> | <span data-ttu-id="43672-185">Edytuj plik projektu lub `packages.config` można poprawić wersji pakietu.</span><span class="sxs-lookup"><span data-stu-id="43672-185">Edit the project file or `packages.config` to correct the package version.</span></span> <span data-ttu-id="43672-186">Sprawdź także, czy [Konfiguracja nuget projektu](../consume-packages/Configuring-NuGet-Behavior.md) identyfikuje źródła pakietów w sieci spodziewać się przy użyciu.</span><span class="sxs-lookup"><span data-stu-id="43672-186">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="43672-187">Konieczne może być zmiana wersji requeted, jeśli ten pakiet jest bezpośrednio wywoływany przez projekt.</span><span class="sxs-lookup"><span data-stu-id="43672-187">You may need to change the requeted version if this package is referenced by the project directly.</span></span> |

### <a name="nu1103"></a><span data-ttu-id="43672-188">NU1103</span><span class="sxs-lookup"><span data-stu-id="43672-188">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-189">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-189">**Issue**</span></span> | <span data-ttu-id="43672-190">Projekt określony stabilną wersję dla zakresu zależności, ale w zakresie nie znaleziono żadnych wersji stabilnej.</span><span class="sxs-lookup"><span data-stu-id="43672-190">The project specified a stable version for the dependency range, but no stable versions were found in that range.</span></span> <span data-ttu-id="43672-191">Wersje wstępne znaleziono, ale nie są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="43672-191">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="43672-192">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-192">**Example message**</span></span> | <span data-ttu-id="43672-193">*Nie można odnaleźć pakietu stabilna NuGet.Versioning z wersją (> = 3.0.0)<br/> — wersje znaleziono 10 w dotnet buildtools [najbliższej wersji: 4.0.0-rc-2129]<br/> -znaleziono 9 wersje w NuGetVolatile [najbliższej wersji: 3.0.0-beta-00032] <br/> -Znaleziono wersje 0 w podstawowej platformy dotnet<br/> -znaleziono wersje 0 w dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="43672-193">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="43672-194">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-194">**Solution**</span></span> |  <span data-ttu-id="43672-195">Edytuj zakres wersji w pliku projektu lub `packages.config` uwzględnienie wersje wstępne.</span><span class="sxs-lookup"><span data-stu-id="43672-195">Edit the version range in the project file or `packages.config` to include pre-release versions.</span></span> <span data-ttu-id="43672-196">Zobacz [wersji pakietu](../reference/Package-Versioning.md).</span><span class="sxs-lookup"><span data-stu-id="43672-196">See [Package versioning](../reference/Package-Versioning.md).</span></span> |

### <a name="nu1104"></a><span data-ttu-id="43672-197">NU1104</span><span class="sxs-lookup"><span data-stu-id="43672-197">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-198">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-198">**Issue**</span></span> | <span data-ttu-id="43672-199">Wskazuje element ProjectReference do pliku, który nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="43672-199">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="43672-200">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-200">**Example message**</span></span> | <span data-ttu-id="43672-201">*Odwołanie do projektu nie istnieje "c:\a.csproj". Sprawdź, czy odwołanie do projektu jest prawidłowa i czy istnieje plik projektu.*</span><span class="sxs-lookup"><span data-stu-id="43672-201">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |
| <span data-ttu-id="43672-202">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-202">**Solution**</span></span> | <span data-ttu-id="43672-203">Edytuj plik projektu albo poprawną ścieżkę do przywoływanego projektu lub Usuń odwołanie całkowicie, jeśli nie jest już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="43672-203">Edit the project file to either correct the path to the referenced project or to remove the reference altogether if it's no longer needed.</span></span> |

### <a name="nu1105"></a><span data-ttu-id="43672-204">NU1105</span><span class="sxs-lookup"><span data-stu-id="43672-204">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-205">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-205">**Issue**</span></span> | <span data-ttu-id="43672-206">Plik projektu istnieje, ale go nie dostarczono żadnych informacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="43672-206">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="43672-207">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-207">**Example message**</span></span> | <span data-ttu-id="43672-208">*Nie można odczytać informacji o projekcie dla "c:\a.csproj". Plik projektu może być nieprawidłowe lub brakujące elementy docelowe, wymaganych do przywrócenia.*</span><span class="sxs-lookup"><span data-stu-id="43672-208">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="43672-209">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-209">**Solution**</span></span> | <span data-ttu-id="43672-210">W programie Visual Studio błąd może oznaczać, że projekt jest zwolniony, w którym to przypadku ponownie Załaduj projekt.</span><span class="sxs-lookup"><span data-stu-id="43672-210">In Visual Studio, the error could mean that the project is unloaded, in which case reload the project.</span></span> <span data-ttu-id="43672-211">W wierszu polecenia może to oznaczać, że plik jest uszkodzony lub nie zawiera niestandardowego "po imports" potrzebne do odzyskiwania do odczytu do projektu docelowego.</span><span class="sxs-lookup"><span data-stu-id="43672-211">From the command line this could mean that the file is corrupt or that it doesn't contain the custom "after imports" target needed for restore to read the project.</span></span> <span data-ttu-id="43672-212">Sprawdź, czy plik projektu jest prawidłowa i czy zawiera element docelowy "po imports".</span><span class="sxs-lookup"><span data-stu-id="43672-212">Check that the project file is valid and contains an "after imports" target.</span></span> |

### <a name="nu1106"></a><span data-ttu-id="43672-213">NU1106</span><span class="sxs-lookup"><span data-stu-id="43672-213">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-214">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-214">**Issue**</span></span> | <span data-ttu-id="43672-215">Nie można rozpoznać zależności ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="43672-215">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="43672-216">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-216">**Example message**</span></span> | <span data-ttu-id="43672-217">*Nie można zrealizować żądań będących w konflikcie dla {id}: {konflikt path} Framework: {docelowy wykres}*</span><span class="sxs-lookup"><span data-stu-id="43672-217">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> 
| <span data-ttu-id="43672-218">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-218">**Solution**</span></span> | <span data-ttu-id="43672-219">Edytuj plik projektu lub `packages.config` do określenia bardziej uniwersalnym zakresy dla zależności, a nie dokładnej wersji.</span><span class="sxs-lookup"><span data-stu-id="43672-219">Edit the project file or `packages.config` to specify more open-ended ranges for the dependency rather than an exact version.</span></span> |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="43672-220">NU1107 (wcześniej NU1607)</span><span class="sxs-lookup"><span data-stu-id="43672-220">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-221">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-221">**Issue**</span></span> | <span data-ttu-id="43672-222">Nie można rozpoznać ograniczenia zależności między pakietami.</span><span class="sxs-lookup"><span data-stu-id="43672-222">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="43672-223">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-223">**Example message**</span></span> | <span data-ttu-id="43672-224">*Konflikt wersji dla NuGet.Versioning wykryte. Pakiet odwoływać się bezpośrednio z projektu, aby rozwiązać ten problem.<br/>  NuGet.Versioning (= 3.5.0) -> NuGet.Packaging 3.5.0<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="43672-224">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |
| <span data-ttu-id="43672-225">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-225">**Solution**</span></span> | <span data-ttu-id="43672-226">Pakiety z ograniczeniami zależności na dokładną wersję nie zezwalają na inne pakiety w razie potrzeby zwiększyć wersji.</span><span class="sxs-lookup"><span data-stu-id="43672-226">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> <span data-ttu-id="43672-227">Dodaj odwołanie do projektu bezpośrednio (w pliku projektu lub `packages.config`) na dokładną wersję wymaganą.</span><span class="sxs-lookup"><span data-stu-id="43672-227">Add a reference to the project directly (in the project file or `packages.config`) with the exact version required.</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="43672-228">NU1108 (wcześniej NU1606)</span><span class="sxs-lookup"><span data-stu-id="43672-228">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-229">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-229">**Issue**</span></span> | <span data-ttu-id="43672-230">Wykryto zależność cykliczną.</span><span class="sxs-lookup"><span data-stu-id="43672-230">A circular dependency was detected.</span></span> |
| <span data-ttu-id="43672-231">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-231">**Example message**</span></span> | <span data-ttu-id="43672-232">*Wykryto cykl: A -> B -> A*</span><span class="sxs-lookup"><span data-stu-id="43672-232">*Cycle detected: A -> B -> A*</span></span> |
| <span data-ttu-id="43672-233">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-233">**Solution**</span></span> | <span data-ttu-id="43672-234">Pakiet jest w pełni autoryzowane; Skontaktuj się z właścicielem pakietu, aby naprawić ten błąd.</span><span class="sxs-lookup"><span data-stu-id="43672-234">The package is authored incorrectly; contact the package owner to correct the bug.</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="43672-235">Błędy zgodności</span><span class="sxs-lookup"><span data-stu-id="43672-235">Compatibility errors</span></span>

<span data-ttu-id="43672-236">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="43672-236">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="43672-237">NU1201</span><span class="sxs-lookup"><span data-stu-id="43672-237">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-238">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-238">**Issue**</span></span> | <span data-ttu-id="43672-239">Zależności projektu nie zawiera struktury zgodne z bieżącego projektu.</span><span class="sxs-lookup"><span data-stu-id="43672-239">A dependency project doesn't contain a framework compatible with the current project.</span></span> <span data-ttu-id="43672-240">Zazwyczaj platformę docelową projektu jest wyższą wersję niż odbierającą projektu.</span><span class="sxs-lookup"><span data-stu-id="43672-240">Typically, the project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="43672-241">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-241">**Example message**</span></span> | <span data-ttu-id="43672-242">*ServerWeb projektu nie jest zgodny z netstandard1.3 (. Krótkich nazw NETStandard, Version = w wersji 1.3). Projekt obsługuje ServerWeb:<br/> -netstandard1.6 (. Krótkich nazw NETStandard, Version = w wersji 1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = 1.0)*</span><span class="sxs-lookup"><span data-stu-id="43672-242">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |
| <span data-ttu-id="43672-243">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-243">**Solution**</span></span> | <span data-ttu-id="43672-244">Zmień platformę docelową projektu na wersję równa lub mniejsza niż odbierającą projektu.</span><span class="sxs-lookup"><span data-stu-id="43672-244">Change the project's target framework to an equal or lower version than the consuming project.</span></span> |

### <a name="nu1202"></a><span data-ttu-id="43672-245">NU1202</span><span class="sxs-lookup"><span data-stu-id="43672-245">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-246">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-246">**Issue**</span></span> | <span data-ttu-id="43672-247">Pakiet zależności nie zawiera żadnych zasobów, które są zgodne z projektem.</span><span class="sxs-lookup"><span data-stu-id="43672-247">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="43672-248">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-248">**Example message**</span></span> | <span data-ttu-id="43672-249">*Pakiet System.ComponentModel.EventBasedAsync 4.0.11 nie jest zgodny z netstandard1.3 (. Krótkich nazw NETStandard, Version = w wersji 1.3). Pakiet obsługuje System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, wersja = 1.0)<br/> -monotouch10 (MonoTouch, wersja = 1.0)<br/> -net45 (. NETFramework, Version = 4.5)<br/> -netcore50 (. NETCore, Version = v5.0)<br/> -netstandard1.0 (. Krótkich nazw NETStandard, Version = 1.0)<br/> -przenośny net45 + win8 + wp8 + wpa81 (. NETPortable, wersja = v0.0, profil = Profile259)<br/> — Windows 8 (Windows, wersja = w wersji 8.0)<br/> -wp8 (WindowsPhone, wersja = w wersji 8.0)<br/> -wpa81 (WindowsPhoneApp, wersja = v8.1)<br/> — xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="43672-249">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|
| <span data-ttu-id="43672-250">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-250">**Solution**</span></span> | <span data-ttu-id="43672-251">Zmień platformę docelową projektu na taki, który obsługuje pakietu.</span><span class="sxs-lookup"><span data-stu-id="43672-251">Change the project's target framework to one that the package supports.</span></span> |

### <a name="nu1203"></a><span data-ttu-id="43672-252">NU1203</span><span class="sxs-lookup"><span data-stu-id="43672-252">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-253">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-253">**Issue**</span></span> | <span data-ttu-id="43672-254">Pakiet nie obsługuje projektu `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="43672-254">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="43672-255">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-255">**Example message**</span></span> | <span data-ttu-id="43672-256">*System.Example 1.0.0 udostępnia zestaw odwołania czasu kompilowania dla a.dll na net461, ale nie nie zgodny zestaw czasu wykonywania.*</span><span class="sxs-lookup"><span data-stu-id="43672-256">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |
| <span data-ttu-id="43672-257">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-257">**Solution**</span></span> | <span data-ttu-id="43672-258">Zmień `RuntimeIdentifier` wartości użyte w projekcie, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="43672-258">Change the `RuntimeIdentifier` values used in the project as needed.</span></span> |

### <a name="nu1401"></a><span data-ttu-id="43672-259">NU1401</span><span class="sxs-lookup"><span data-stu-id="43672-259">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-260">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-260">**Issue**</span></span> | <span data-ttu-id="43672-261">Pakiet wymaga funkcji lub struktur nie są obecnie obsługiwane przez zainstalowaną wersję programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="43672-261">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="43672-262">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-262">**Example message**</span></span> | <span data-ttu-id="43672-263">*Pakiet "NuGet.Versioning" wymaga wersji klienta "5.0.0" NuGet lub nowszej, ale bieżąca wersja NuGet to "4.3.0".*</span><span class="sxs-lookup"><span data-stu-id="43672-263">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'.*</span></span> |
| <span data-ttu-id="43672-264">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-264">**Solution**</span></span> | <span data-ttu-id="43672-265">Zainstaluj nowszą wersję programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="43672-265">Install a newer version of NuGet.</span></span> <span data-ttu-id="43672-266">Zobacz [narzędzia klienta instalowania NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="43672-266">See [Installing NuGet client tools](../install-nuget-client-tools.md).</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="43672-267">Nieprawidłowy wejściowy ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="43672-267">Invalid input warnings</span></span>

<span data-ttu-id="43672-268">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="43672-268">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="43672-269">NU1501</span><span class="sxs-lookup"><span data-stu-id="43672-269">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-270">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-270">**Issue**</span></span> | <span data-ttu-id="43672-271">Przywracanie projektu próbuje działać na nie został znaleziony.</span><span class="sxs-lookup"><span data-stu-id="43672-271">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="43672-272">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-272">**Example message**</span></span> | <span data-ttu-id="43672-273">*Folder "c:\projects\a" nie zawiera projektu do przywrócenia.*</span><span class="sxs-lookup"><span data-stu-id="43672-273">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |
| <span data-ttu-id="43672-274">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-274">**Solution**</span></span> | <span data-ttu-id="43672-275">Uruchamianie przywracania nuget w folderze, który zawiera projekt.</span><span class="sxs-lookup"><span data-stu-id="43672-275">Run nuget restore in a folder that contains a project.</span></span> |

### <a name="nu1502"></a><span data-ttu-id="43672-276">NU1502</span><span class="sxs-lookup"><span data-stu-id="43672-276">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-277">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-277">**Issue**</span></span> | <span data-ttu-id="43672-278">`RuntimeSupports` zawiera nieprawidłowy profil.</span><span class="sxs-lookup"><span data-stu-id="43672-278">`RuntimeSupports` contains an invalid profile.</span></span> <span data-ttu-id="43672-279">Zazwyczaj obsługuje profil nie został znaleziony w `runtime.json` plik z bieżącego zależności pakietów.</span><span class="sxs-lookup"><span data-stu-id="43672-279">Typically, the supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span>|
| <span data-ttu-id="43672-280">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-280">**Example message**</span></span> | <span data-ttu-id="43672-281">*Profil zgodności nieznany: aaa*</span><span class="sxs-lookup"><span data-stu-id="43672-281">*Unknown Compatibility Profile: aaa*</span></span> |
| <span data-ttu-id="43672-282">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-282">**Solution**</span></span> | <span data-ttu-id="43672-283">Sprawdź `RuntimeSupports` wartość w projekcie.</span><span class="sxs-lookup"><span data-stu-id="43672-283">Check the `RuntimeSupports` value in your project.</span></span> |

### <a name="nu1503"></a><span data-ttu-id="43672-284">NU1503</span><span class="sxs-lookup"><span data-stu-id="43672-284">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-285">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-285">**Issue**</span></span> | <span data-ttu-id="43672-286">Zależności projektu nie importuje obiekty docelowe przywracania NuGet.</span><span class="sxs-lookup"><span data-stu-id="43672-286">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="43672-287">Ten jest podobny do NU1105, ale w tym miejscu projektu zostanie pominięty i zignorowany zamiast powoduje wszystkie przywracania się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="43672-287">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="43672-288">W złożonych rozwiązań są często innych typów projektów, które mogą nie obsługiwać przywracania.</span><span class="sxs-lookup"><span data-stu-id="43672-288">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="43672-289">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-289">**Example message**</span></span> | <span data-ttu-id="43672-290">*Pomijanie przywracania dla projektu "c:\a.csproj". Plik projektu może być nieprawidłowe lub brakujące elementy docelowe, wymaganych do przywrócenia.*</span><span class="sxs-lookup"><span data-stu-id="43672-290">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="43672-291">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-291">**Solution**</span></span> | <span data-ttu-id="43672-292">Może to nastąpić dla projektów, które nie należy importować wspólne właściwości/cele, które są automatycznie importowane przywracania.</span><span class="sxs-lookup"><span data-stu-id="43672-292">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="43672-293">Jeśli projekt nie trzeba przywrócić możesz go zignorować.</span><span class="sxs-lookup"><span data-stu-id="43672-293">If the project doesn't need to be restored this can be ignored.</span></span> <span data-ttu-id="43672-294">W przeciwnym razie edytować dotyczy projektu, aby dodać elementy docelowe przywracania.</span><span class="sxs-lookup"><span data-stu-id="43672-294">Otherwise, edit the affected project to add targets for restore.</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="43672-295">Nieoczekiwany pakietu wersji ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="43672-295">Unexpected package version warnings</span></span>

<span data-ttu-id="43672-296">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="43672-296">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="43672-297">NU1601</span><span class="sxs-lookup"><span data-stu-id="43672-297">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-298">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-298">**Issue**</span></span> | <span data-ttu-id="43672-299">Zależności bezpośrednich projektu był upadku na wyższą wersję niż określonego projektu.</span><span class="sxs-lookup"><span data-stu-id="43672-299">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="43672-300">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-300">**Example message**</span></span> | <span data-ttu-id="43672-301">*Określoną zależnością było NuGet.Versioning (> = 3.5.0), ale ostatecznie otrzymano NuGet.Versioning 4.0.0.*</span><span class="sxs-lookup"><span data-stu-id="43672-301">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |
| <span data-ttu-id="43672-302">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-302">**Solution**</span></span> | <span data-ttu-id="43672-303">Zaktualizuj zależności w projekcie do odpowiedniej wersji.</span><span class="sxs-lookup"><span data-stu-id="43672-303">Update the dependency in the project to an appropriate version.</span></span> |

### <a name="nu1602"></a><span data-ttu-id="43672-304">NU1602</span><span class="sxs-lookup"><span data-stu-id="43672-304">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-305">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-305">**Issue**</span></span> | <span data-ttu-id="43672-306">Zależność pakietu brak dolnej granicy.</span><span class="sxs-lookup"><span data-stu-id="43672-306">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="43672-307">To nie zezwala na przywracania znaleźć *najlepszego dopasowania*.</span><span class="sxs-lookup"><span data-stu-id="43672-307">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="43672-308">Każdy przywracania będzie przestawiany dół próby znalezienia starszej wersji, który może być używany.</span><span class="sxs-lookup"><span data-stu-id="43672-308">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="43672-309">Oznacza to, że przywracanie przejdzie do trybu online, aby sprawdzić wszystkie źródła zawsze zamiast pakietów, które już istnieją w folderze pakietów użytkowników.</span><span class="sxs-lookup"><span data-stu-id="43672-309">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="43672-310">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-310">**Example message**</span></span> | <span data-ttu-id="43672-311">*NuGet.Packaging 4.0.0 nie zapewnia włącznie dolna granica dla zależności NuGet.Versioning (> 3.5.0). Przybliżony najlepsze dopasowanie 3.6.0 został rozwiązany.*</span><span class="sxs-lookup"><span data-stu-id="43672-311">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |
| <span data-ttu-id="43672-312">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-312">**Solution**</span></span> | <span data-ttu-id="43672-313">Jest to zazwyczaj błąd tworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="43672-313">This is usually a package authoring error.</span></span> <span data-ttu-id="43672-314">Skontaktuj się z autorem pakietu, aby rozwiązać ten problem.</span><span class="sxs-lookup"><span data-stu-id="43672-314">Contact the package author to resolve the issue.</span></span> |

### <a name="nu1603"></a><span data-ttu-id="43672-315">NU1603</span><span class="sxs-lookup"><span data-stu-id="43672-315">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-316">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-316">**Issue**</span></span> | <span data-ttu-id="43672-317">Zależność pakietu określonej wersji, którego nie można odnaleźć.</span><span class="sxs-lookup"><span data-stu-id="43672-317">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="43672-318">Zazwyczaj źródła pakietu nie zawierają wersja oczekiwana dolnej granicy.</span><span class="sxs-lookup"><span data-stu-id="43672-318">Typically, the package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="43672-319">Nowsza wersja użyto zamiast tego, który różni się od pakietu opracowania przed.</span><span class="sxs-lookup"><span data-stu-id="43672-319">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="43672-320">Oznacza to, że przywracanie nie znalazł *najlepszego dopasowania*.</span><span class="sxs-lookup"><span data-stu-id="43672-320">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="43672-321">Każdy przywracania będzie przestawiany dół próby znalezienia starszej wersji, który może być używany.</span><span class="sxs-lookup"><span data-stu-id="43672-321">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="43672-322">Oznacza to, że przywracanie przejdzie do trybu online, aby sprawdzić wszystkie źródła zawsze zamiast pakietów, które już istnieją w folderze pakietów użytkowników.</span><span class="sxs-lookup"><span data-stu-id="43672-322">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="43672-323">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-323">**Example message**</span></span> | <span data-ttu-id="43672-324">NuGet.Packaging 4.0.0 zależy od NuGet.Versioning (> = 4.0.0), ale nie można odnaleźć 4.0.0.</span><span class="sxs-lookup"><span data-stu-id="43672-324">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="43672-325">Przybliżony najlepsze dopasowanie 5.0.0 został rozwiązany.</span><span class="sxs-lookup"><span data-stu-id="43672-325">An approximate best match of 5.0.0 was resolved.</span></span> |
| <span data-ttu-id="43672-326">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-326">**Solution**</span></span> | <span data-ttu-id="43672-327">Jeśli nie zostało zwolnione pakietu oczekiwano może to być błąd tworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="43672-327">If the package expected has not been released then this may be a package authoring error.</span></span> <span data-ttu-id="43672-328">Skontaktuj się z autorem pakietu, aby rozwiązać ten problem.</span><span class="sxs-lookup"><span data-stu-id="43672-328">Contact the package author to resolve the issue.</span></span> <span data-ttu-id="43672-329">Jeśli pakiet został zwolniony, sprawdź, czy plik jest dostępny na źródła pakietów, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="43672-329">If the package has been released, then check that it's available on the package sources you're using.</span></span> <span data-ttu-id="43672-330">Jeśli przy użyciu prywatnych źródła, może być konieczne zaktualizowanie pakietu w tego źródła.</span><span class="sxs-lookup"><span data-stu-id="43672-330">If using a private source, you may need to update the package on that feed.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="43672-331">NU1604</span><span class="sxs-lookup"><span data-stu-id="43672-331">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-332">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-332">**Issue**</span></span> | <span data-ttu-id="43672-333">Zależności projektu nie definiuje dolną granicą.</span><span class="sxs-lookup"><span data-stu-id="43672-333">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="43672-334">Oznacza to, że przywracanie nie znalazł *najlepszego dopasowania*.</span><span class="sxs-lookup"><span data-stu-id="43672-334">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="43672-335">Każdy przywracania będzie przestawiany dół próby znalezienia starszej wersji, który może być używany.</span><span class="sxs-lookup"><span data-stu-id="43672-335">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="43672-336">Oznacza to, że przywracanie przejdzie do trybu online, aby sprawdzić wszystkie źródła zawsze zamiast pakietów, które już istnieją w folderze pakietów użytkowników.</span><span class="sxs-lookup"><span data-stu-id="43672-336">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="43672-337">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-337">**Example message**</span></span> | <span data-ttu-id="43672-338">*Projekt zależności NuGet.Versioning (< = od 9.0.0) Nowak zawiera włącznie dolnej granicy. Dolna granica należy uwzględnić w wersji zależności, aby zapewnić wyniki przywracania na poziomie.*</span><span class="sxs-lookup"><span data-stu-id="43672-338">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |
| <span data-ttu-id="43672-339">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-339">**Solution**</span></span> | <span data-ttu-id="43672-340">Aktualizowanie projektu `PackageReference` `Version` atrybutu uwzględnienie dolną granicą.</span><span class="sxs-lookup"><span data-stu-id="43672-340">Update the project's `PackageReference` `Version` attribute to include a lower bound.</span></span> |

### <a name="nu1605"></a><span data-ttu-id="43672-341">NU1605</span><span class="sxs-lookup"><span data-stu-id="43672-341">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-342">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-342">**Issue**</span></span> | <span data-ttu-id="43672-343">Pakiet zależności określić ograniczenia wersji za pomocą nowszej wersji pakietu niż przywracania ostatecznie rozwiązane.</span><span class="sxs-lookup"><span data-stu-id="43672-343">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> <span data-ttu-id="43672-344">Oznacza to z powodu "najbliższej wins" reguła podczas rozpoznawania pakietów, bliżej położonego pakietu na wykresie mogą mieć zastąpione odległymi pakiet.</span><span class="sxs-lookup"><span data-stu-id="43672-344">That is, because of the "nearest wins" rule when resolving packages, a nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="43672-345">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-345">**Example message**</span></span> | <span data-ttu-id="43672-346">*Wykryto starszą wersję pakietu: NuGet.Versioning z 4.0.0 do 3.5.0. Odwoływać się bezpośrednio z projektu, aby wybrać inną wersję pakietu.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="43672-346">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |
| <span data-ttu-id="43672-347">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-347">**Solution**</span></span> | <span data-ttu-id="43672-348">Dodaj bezpośrednie odwołanie do projektu do nowszej wersji pakietu, który ma być używany.</span><span class="sxs-lookup"><span data-stu-id="43672-348">Add a direct reference to the project for the higher version of the package that you want to use.</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="43672-349">Mechanizm rozpoznawania konfliktu ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="43672-349">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="43672-350">NU1608</span><span class="sxs-lookup"><span data-stu-id="43672-350">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-351">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-351">**Issue**</span></span> | <span data-ttu-id="43672-352">Rozwiązany pakietu jest większa niż umożliwia ograniczenie zależności.</span><span class="sxs-lookup"><span data-stu-id="43672-352">A resolved package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="43672-353">Oznacza to, że pakiet bezpośrednio odwołuje się projekt zastępuje ograniczenia zależności z innymi pakietami.</span><span class="sxs-lookup"><span data-stu-id="43672-353">This means that a package referenced directly by a project overrides dependency constraints from other packages.</span></span>|
| <span data-ttu-id="43672-354">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-354">**Example message**</span></span> | <span data-ttu-id="43672-355">*Wersja pakietu wykrytych poza ograniczenia zależności: x 1.0.0 wymaga y (= 1.0.0), ale wersja y 2.0.0 został rozwiązany.*</span><span class="sxs-lookup"><span data-stu-id="43672-355">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |
| <span data-ttu-id="43672-356">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-356">**Solution**</span></span> | <span data-ttu-id="43672-357">W niektórych przypadkach jest to zamierzone i można pominąć to ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="43672-357">In some cases this is intentional and the warning can be suppressed.</span></span> <span data-ttu-id="43672-358">W przeciwnym razie Zmień odwołanie projektu do pakietu, aby zwiększyć swoje ograniczenia wersji.</span><span class="sxs-lookup"><span data-stu-id="43672-358">Otherwise, change the project's reference to the package to widen its version constraints.</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="43672-359">Ostrzeżenia rezerwowy pakietu</span><span class="sxs-lookup"><span data-stu-id="43672-359">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="43672-360">NU1701</span><span class="sxs-lookup"><span data-stu-id="43672-360">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-361">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-361">**Issue**</span></span> | <span data-ttu-id="43672-362">`PackageTargetFallback` / `AssetTargetFallback` użyto Wybierz zasoby z pakietem.</span><span class="sxs-lookup"><span data-stu-id="43672-362">`PackageTargetFallback` / `AssetTargetFallback` was used to select assets from a package.</span></span> <span data-ttu-id="43672-363">Ostrzeżenie powiadomić użytkowników, że zasoby nie mogą być 100% zgodny.</span><span class="sxs-lookup"><span data-stu-id="43672-363">The warning let users know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="43672-364">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-364">**Example message**</span></span> | <span data-ttu-id="43672-365">*Pakiet "NuGet.Versioning" został przywrócony przy użyciu "portable net45 + win8" zamiast platformy docelowej projektu "netstandard1.5". Ten pakiet nie może być całkowicie zgodne z projektem.*</span><span class="sxs-lookup"><span data-stu-id="43672-365">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |
| <span data-ttu-id="43672-366">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-366">**Solution**</span></span> | <span data-ttu-id="43672-367">Zmień platformę docelową projektu na taki, który obsługuje pakietu.</span><span class="sxs-lookup"><span data-stu-id="43672-367">Change the project's target framework to one that the package supports.</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="43672-368">Źródła danych ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="43672-368">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="43672-369">NU1801</span><span class="sxs-lookup"><span data-stu-id="43672-369">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-370">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-370">**Issue**</span></span> | <span data-ttu-id="43672-371">Wystąpił błąd podczas odczytywania źródła po `IgnoreFailedSources` jest ustawiona na wartość true, konwersją niekrytyczny ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="43672-371">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="43672-372">To może zawierać żadnych komunikatów i jest rodzajowy.</span><span class="sxs-lookup"><span data-stu-id="43672-372">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="43672-373">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-373">**Example message**</span></span> | <span data-ttu-id="43672-374">n/d</span><span class="sxs-lookup"><span data-stu-id="43672-374">n/a</span></span> |
| <span data-ttu-id="43672-375">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-375">**Solution**</span></span> | <span data-ttu-id="43672-376">Edytuj konfigurację, aby określić prawidłową źródła.</span><span class="sxs-lookup"><span data-stu-id="43672-376">Edit your configuration to specify valid sources.</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="43672-377">NuGet wewnętrzne błędy i ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="43672-377">NuGet internal errors and warnings</span></span>

<span data-ttu-id="43672-378">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="43672-378">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="43672-379">NU1000</span><span class="sxs-lookup"><span data-stu-id="43672-379">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-380">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-380">**Issue**</span></span> | <span data-ttu-id="43672-381">Nieokreślony błąd wewnętrzny z pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="43672-381">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="43672-382">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-382">**Solution**</span></span> | <span data-ttu-id="43672-383">Sprawdź dzienniki, aby uzyskać więcej informacji</span><span class="sxs-lookup"><span data-stu-id="43672-383">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="43672-384">NU1500</span><span class="sxs-lookup"><span data-stu-id="43672-384">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-385">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-385">**Issue**</span></span> | <span data-ttu-id="43672-386">Nieokreślony ostrzeżenie wewnętrzny z pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="43672-386">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="43672-387">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-387">**Solution**</span></span> | <span data-ttu-id="43672-388">Sprawdź dzienniki, aby uzyskać więcej informacji</span><span class="sxs-lookup"><span data-stu-id="43672-388">Check the logs for more information</span></span> |

## <a name="signed-packages-creation-and-verification"></a><span data-ttu-id="43672-389">Podpisanych pakietów (tworzenia i weryfikacji)</span><span class="sxs-lookup"><span data-stu-id="43672-389">Signed packages (creation and verification)</span></span>

<span data-ttu-id="43672-390">*NuGet 4.6.0+*</span><span class="sxs-lookup"><span data-stu-id="43672-390">*NuGet 4.6.0+*</span></span>

<span data-ttu-id="43672-391">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="43672-391">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span></span>

### <a name="nu3000"></a><span data-ttu-id="43672-392">NU3000</span><span class="sxs-lookup"><span data-stu-id="43672-392">NU3000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-393">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-393">**Issue**</span></span> | <span data-ttu-id="43672-394">Ogólny błąd odnoszące się do podpisywania pakietu i podpisany weryfikacji pakietu.</span><span class="sxs-lookup"><span data-stu-id="43672-394">A non-specific error related to package signing and signed package verification.</span></span> |
| <span data-ttu-id="43672-395">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-395">**Solution**</span></span> | <span data-ttu-id="43672-396">Sprawdź dzienniki, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="43672-396">Check the logs for more information.</span></span> |

### <a name="nu3001"></a><span data-ttu-id="43672-397">NU3001</span><span class="sxs-lookup"><span data-stu-id="43672-397">NU3001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-398">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-398">**Issue**</span></span> | <span data-ttu-id="43672-399">Nieprawidłowe argumenty albo [zarejestrować polecenia](../tools/cli-ref-sign.md) lub [Sprawdź polecenie](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="43672-399">Invalid arguments to either the [sign command](../tools/cli-ref-sign.md) or the [verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="43672-400">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-400">**Solution**</span></span> | <span data-ttu-id="43672-401">Sprawdź i popraw na podstawie podanych argumentów.</span><span class="sxs-lookup"><span data-stu-id="43672-401">Check and correct the arguments provided.</span></span> |

### <a name="nu3002"></a><span data-ttu-id="43672-402">NU3002</span><span class="sxs-lookup"><span data-stu-id="43672-402">NU3002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-403">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-403">**Issue**</span></span> | <span data-ttu-id="43672-404">`-Timestamper` Nie określono opcję z [polecenia nuget znak](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="43672-404">The `-Timestamper` option was not specified with the [nuget sign command](../tools/cli-ref-sign.md).</span></span> |
| <span data-ttu-id="43672-405">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-405">**Example message**</span></span> | <span data-ttu-id="43672-406">*"-Timestamper" nie określono opcji. Podpisanego pakietu nie jest oznaczony znacznikiem czasowym.*</span><span class="sxs-lookup"><span data-stu-id="43672-406">*The '-Timestamper' option was not provided. The signed package will not be timestamped.*</span></span> |
| <span data-ttu-id="43672-407">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-407">**Solution**</span></span> | <span data-ttu-id="43672-408">Określ `-Timestamper` opcję z `nuget sign`.</span><span class="sxs-lookup"><span data-stu-id="43672-408">Specify the `-Timestamper` option with `nuget sign`.</span></span> |

### <a name="nu3004"></a><span data-ttu-id="43672-409">NU3004</span><span class="sxs-lookup"><span data-stu-id="43672-409">NU3004</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-410">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-410">**Issue**</span></span> | <span data-ttu-id="43672-411">Dostarczono niepodpisanego pakietu [nuget Sprawdź polecenie](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="43672-411">An unsigned package was provided to the [nuget verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="43672-412">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-412">**Solution**</span></span> | <span data-ttu-id="43672-413">Uruchom `nuget verify` przy użyciu podpisanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="43672-413">Run `nuget verify` with a signed package.</span></span> <span data-ttu-id="43672-414">Zobacz [podpisywania pakietu](../create-packages/Sign-a-Package.md).</span><span class="sxs-lookup"><span data-stu-id="43672-414">See [Sign a package](../create-packages/Sign-a-Package.md).</span></span> |

### <a name="nu3008"></a><span data-ttu-id="43672-415">NU3008</span><span class="sxs-lookup"><span data-stu-id="43672-415">NU3008</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-416">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-416">**Issue**</span></span> | <span data-ttu-id="43672-417">Nie można sprawdzić integralność pakietu, co oznacza, że pakiet podpisany został zmodyfikowany od czasu podpisania.</span><span class="sxs-lookup"><span data-stu-id="43672-417">The package integrity check failed, meaning that a signed package was tampered with since being signed.</span></span> |
| <span data-ttu-id="43672-418">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-418">**Solution**</span></span> | <span data-ttu-id="43672-419">Skanowanie komputera za pomocą oprogramowania antywirusowego.</span><span class="sxs-lookup"><span data-stu-id="43672-419">Scan your computer with anti-virus software.</span></span> <span data-ttu-id="43672-420">Następnie usuń pakiet z komputera, zainstaluj go ponownie i spróbuj ponownie wykonać operację.</span><span class="sxs-lookup"><span data-stu-id="43672-420">Then remove the package from the computer, reinstall it, and try the operation again.</span></span> <span data-ttu-id="43672-421">Jeśli problem będzie się powtarzać, skontaktuj się z właścicielem źródła pakietu i właściciela pakietu.</span><span class="sxs-lookup"><span data-stu-id="43672-421">If the problem persists, contact the owner of the package source and the package owner.</span></span> |

### <a name="nu3018"></a><span data-ttu-id="43672-422">NU3018</span><span class="sxs-lookup"><span data-stu-id="43672-422">NU3018</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-423">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-423">**Issue**</span></span> | <span data-ttu-id="43672-424">Tworzenie łańcucha certyfikatów nie powiodło się dla podpisu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="43672-424">Certificate chain building failed for the primary signature.</span></span> <span data-ttu-id="43672-425">Podstawowy certyfikat podpisywania nie jest zaufane, odwołany, lub informacji o odwołaniu dla certyfikatu jest niedostępny.</span><span class="sxs-lookup"><span data-stu-id="43672-425">The primary signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="43672-426">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-426">**Example message**</span></span> | <span data-ttu-id="43672-427">*Ostrzeżenie: NU3018: funkcja odwołania nie może sprawdzić odwołania certyfikatu.*</span><span class="sxs-lookup"><span data-stu-id="43672-427">*WARNING: NU3018: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="43672-428">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-428">**Solution**</span></span> | <span data-ttu-id="43672-429">Użyj zaufanego, ważny certyfikat.</span><span class="sxs-lookup"><span data-stu-id="43672-429">Use a trusted and valid certificate.</span></span> <span data-ttu-id="43672-430">Sprawdź łączność z Internetem.</span><span class="sxs-lookup"><span data-stu-id="43672-430">Check internet connectivity.</span></span> |

### <a name="nu3028"></a><span data-ttu-id="43672-431">NU3028</span><span class="sxs-lookup"><span data-stu-id="43672-431">NU3028</span></span>

| | |
| --- | --- |
| <span data-ttu-id="43672-432">**Problem**</span><span class="sxs-lookup"><span data-stu-id="43672-432">**Issue**</span></span> | <span data-ttu-id="43672-433">Tworzenie łańcucha certyfikatów nie powiodło się dla podpisu sygnatury czasowej.</span><span class="sxs-lookup"><span data-stu-id="43672-433">Certificate chain building failed for the timestamp signature.</span></span> <span data-ttu-id="43672-434">Certyfikat podpisywania sygnatury czasowej nie jest zaufane, odwołany, lub informacji o odwołaniu dla certyfikatu jest niedostępny.</span><span class="sxs-lookup"><span data-stu-id="43672-434">The timestamp signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="43672-435">**Przykładowy komunikat**</span><span class="sxs-lookup"><span data-stu-id="43672-435">**Example message**</span></span> | <span data-ttu-id="43672-436">*Ostrzeżenie: NU3028: funkcja odwołania nie może sprawdzić odwołania certyfikatu.*</span><span class="sxs-lookup"><span data-stu-id="43672-436">*WARNING: NU3028: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="43672-437">**Rozwiązanie**</span><span class="sxs-lookup"><span data-stu-id="43672-437">**Solution**</span></span> | <span data-ttu-id="43672-438">Użyj zaufanego, ważny certyfikat.</span><span class="sxs-lookup"><span data-stu-id="43672-438">Use a trusted and valid certificate.</span></span> <span data-ttu-id="43672-439">Sprawdź łączność z Internetem.</span><span class="sxs-lookup"><span data-stu-id="43672-439">Check internet connectivity.</span></span> |
