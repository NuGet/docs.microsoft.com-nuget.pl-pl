---
title: "Wielowersyjność kodu dla pakietów NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 9/27/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2646ffcd-83ae-4086-8915-a7fba3f53e45
description: "Opis różnych metod pod kątem wiele wersji .NET Framework z w ramach jednego pakietu NuGet."
keywords: Pakiet NuGet przeznaczonych dla platformy .NET Framework, NuGet i .NET przeznaczonych dla wielu struktur, tworzenia pakietu NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d23158c6dab838b723764994e94fc21cab52f553
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="supporting-multiple-net-framework-versions"></a><span data-ttu-id="e62e6-104">Obsługa wielu wersje programu .NET framework</span><span class="sxs-lookup"><span data-stu-id="e62e6-104">Supporting multiple .NET framework versions</span></span>

<span data-ttu-id="e62e6-105">*Dla platformy .NET Core projektów przy użyciu narzędzia NuGet 4.0 +, zobacz [NuGet pakietu i ich przywracania docelowych elementów MSBuild](../schema/msbuild-targets.md) szczegółowe informacje dotyczące różnych elementów docelowych.*</span><span class="sxs-lookup"><span data-stu-id="e62e6-105">*For .NET Core projects using NuGet 4.0+, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md) for details on cross-targeting.*</span></span>

<span data-ttu-id="e62e6-106">Wiele bibliotek docelowe określonej wersji programu .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="e62e6-106">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="e62e6-107">Na przykład może być jedną wersję biblioteki, które są specyficzne dla platformy uniwersalnej systemu Windows i inną wersję, która korzysta z funkcji .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="e62e6-107">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span>

<span data-ttu-id="e62e6-108">Aby zmieścił się w tym celu NuGet obsługuje wprowadzanie wielu wersji tego samego biblioteki w jednym pakiecie przy korzystaniu z opartych na konwencjach pracy katalogu metody opisane w [utworzenie pakietu](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="e62e6-108">To accommodate this, NuGet supports putting multiple versions of the same library in a single package when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span>

<span data-ttu-id="e62e6-109">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="e62e6-109">In this topic:</span></span>

- [<span data-ttu-id="e62e6-110">Struktura folderów wersji Framework</span><span class="sxs-lookup"><span data-stu-id="e62e6-110">Framework version folder structure</span></span>](#framework-version-folder-structure)
- [<span data-ttu-id="e62e6-111">Zgodnych wersji zestawu i platforma docelowa projektu</span><span class="sxs-lookup"><span data-stu-id="e62e6-111">Matching assembly versions and the target framework in a project</span></span>](#matching-assembly-versions-and-the-target-framework-in-a-project)
- [<span data-ttu-id="e62e6-112">Zestawy grupowania przez framework w wersji</span><span class="sxs-lookup"><span data-stu-id="e62e6-112">Grouping assemblies by framework version</span></span>](#grouping-assemblies-by-framework-version)
- [<span data-ttu-id="e62e6-113">Określanie, która docelowa NuGet do użycia</span><span class="sxs-lookup"><span data-stu-id="e62e6-113">Determining which NuGet target to use</span></span>](#determining-which-nuget-target-to-use)
- [<span data-ttu-id="e62e6-114">Pliki zawartości i skryptów programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="e62e6-114">Content files and PowerShell scripts</span></span>](#content-files-and-powershell-scripts)


## <a name="framework-version-folder-structure"></a><span data-ttu-id="e62e6-115">Struktura folderów wersji Framework</span><span class="sxs-lookup"><span data-stu-id="e62e6-115">Framework version folder structure</span></span>

<span data-ttu-id="e62e6-116">Podczas tworzenia pakietu, który zawiera tylko jedną wersję biblioteki lub docelowej wielu struktur, zawsze utworzyć podfoldery `lib` przy użyciu różnych framework z uwzględnieniem wielkości liter nazwy z następującą konwencją:</span><span class="sxs-lookup"><span data-stu-id="e62e6-116">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="e62e6-117">Aby uzyskać pełną listę obsługiwanych nazw, zobacz [odwołania docelowych platform](../schema/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="e62e6-117">For a complete list of supported names, see the [Target Frameworks reference](../schema/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="e62e6-118">Nigdy nie powinien mieć wersji biblioteki, który nie jest specyficzne dla struktury i umieszczony bezpośrednio w folderze głównym `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="e62e6-118">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="e62e6-119">(Ta funkcja jest obsługiwana tylko w przypadku `packages.config`).</span><span class="sxs-lookup"><span data-stu-id="e62e6-119">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="e62e6-120">To spowoduje upewnij zgodny z platformy docelowej i umożliwia jego zainstalowany gdziekolwiek prawdopodobnie powodujące błędy podczas wykonywania nieoczekiwany.</span><span class="sxs-lookup"><span data-stu-id="e62e6-120">Doing so would make the compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="e62e6-121">Dodawanie zestawów w folderze głównym (takich jak `lib\abc.dll`) lub podfolderów (takie jak `lib\abc\abc.dll`) jest przestarzała i jest ignorowane w przypadku przy użyciu formatu PackagesReference.</span><span class="sxs-lookup"><span data-stu-id="e62e6-121">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="e62e6-122">Na przykład następujące struktury folderów obsługuje cztery wersji zestawu, które są specyficzne dla framework:</span><span class="sxs-lookup"><span data-stu-id="e62e6-122">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="e62e6-123">Aby łatwo obejmują wszystkie te pliki, podczas tworzenia pakietu, należy użyć cyklicznej `**` symbolu wieloznacznego w `<files>` części Twojego `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="e62e6-123">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="e62e6-124">Foldery architektury</span><span class="sxs-lookup"><span data-stu-id="e62e6-124">Architecture-specific folders</span></span> 

<span data-ttu-id="e62e6-125">Jeśli masz zestawy architektury, oznacza to, oddzielne zestawy przeznaczonych dla ARM, x 86 i x64, trzeba je umieścić w folderze o nazwie `runtimes` w podfoldery o nazwie `{platform}-{architecture}\lib\{framework}` lub `{platform}-{architecture}\native`.</span><span class="sxs-lookup"><span data-stu-id="e62e6-125">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="e62e6-126">Na przykład następujące struktury folderów może pomieścić natywnych i zarządzanych biblioteki dll przeznaczonych dla systemu Windows 10 i `uap10.0` framework:</span><span class="sxs-lookup"><span data-stu-id="e62e6-126">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

    \runtimes
        \win10-arm
            \native
            \lib\uap10.0
        \win10-x86
            \native
            \lib\uap10.0
        \win10-x64
            \native
            \lib\uap10.0

<span data-ttu-id="e62e6-127">Zobacz [tworzenie pakietów platformy uniwersalnej systemu Windows](../Guides/Create-UWP-Packages.md) przykład odwołujące się do tych plików w `.nuspec` manifestu.</span><span class="sxs-lookup"><span data-stu-id="e62e6-127">See [Create UWP Packages](../Guides/Create-UWP-Packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>


## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="e62e6-128">Zgodnych wersji zestawu i platforma docelowa projektu</span><span class="sxs-lookup"><span data-stu-id="e62e6-128">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="e62e6-129">Podczas instalowania pakietu, który ma wiele wersji zestawu NuGet próbuje zgodna z nazwą framework zestawu z platformy docelowej projektu.</span><span class="sxs-lookup"><span data-stu-id="e62e6-129">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="e62e6-130">Jeśli nie, NuGet kopiuje zestawu dla najwyższa wersja, która jest mniejsza lub równa platformy docelowej projektu, jeśli jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="e62e6-130">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="e62e6-131">Jeśli nie zgodny zestaw zostanie znaleziony, NuGet zwraca odpowiedni komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="e62e6-131">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="e62e6-132">Na przykład wziąć pod uwagę następujące struktury folderów w pakiecie:</span><span class="sxs-lookup"><span data-stu-id="e62e6-132">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll


<span data-ttu-id="e62e6-133">Podczas instalowania tego pakietu w projekcie, przeznaczonego dla programu .NET Framework 4.6, NuGet instaluje zestaw w `net45` folderu, ponieważ jest to najwyższa wersja dostępne, która jest mniejsza niż 4.6.</span><span class="sxs-lookup"><span data-stu-id="e62e6-133">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="e62e6-134">Jeśli projekt jest przeznaczony dla platformy .NET Framework 4.6.1, z drugiej strony, NuGet instaluje zestaw w `net461` folderu.</span><span class="sxs-lookup"><span data-stu-id="e62e6-134">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="e62e6-135">Jeśli projekt jest przeznaczony dla środowiska .NET framework 4.0 lub starszym, NuGet zgłasza odpowiedni komunikat o błędzie dla nie wyszukuje zgodny zestaw.</span><span class="sxs-lookup"><span data-stu-id="e62e6-135">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="e62e6-136">Zestawy grupowania przez framework w wersji</span><span class="sxs-lookup"><span data-stu-id="e62e6-136">Grouping assemblies by framework version</span></span>

<span data-ttu-id="e62e6-137">NuGet kopiuje zestawy z tylko jedna biblioteka folderu w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="e62e6-137">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="e62e6-138">Na przykład załóżmy, że pakiet ma następującą strukturę folderów:</span><span class="sxs-lookup"><span data-stu-id="e62e6-138">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="e62e6-139">Podczas instalowania pakietu w projekcie, przeznaczonego dla programu .NET Framework 4.5, `MyAssembly.dll` (w wersji 2.0) to zestaw tylko zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="e62e6-139">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="e62e6-140">`MyAssembly.Core.dll`(1.0) nie jest zainstalowany, ponieważ nie znajduje się w `net45` folderu.</span><span class="sxs-lookup"><span data-stu-id="e62e6-140">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="e62e6-141">NuGet działa w ten sposób, ponieważ `MyAssembly.Core.dll` może mieć scalonego w wersji 2.0 `MyAssembly.dll`.</span><span class="sxs-lookup"><span data-stu-id="e62e6-141">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="e62e6-142">Jeśli chcesz `MyAssembly.Core.dll` zainstalowania programu .NET Framework 4.5, Umieść kopię w `net45` folderu.</span><span class="sxs-lookup"><span data-stu-id="e62e6-142">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="e62e6-143">Zestawy grupowania w ramach profilu</span><span class="sxs-lookup"><span data-stu-id="e62e6-143">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="e62e6-144">NuGet obsługuje również przeznaczonych dla określonej platformy profil przez dołączenie kreska i nazwa profilu w celu folderu.</span><span class="sxs-lookup"><span data-stu-id="e62e6-144">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="e62e6-145">Profile obsługiwane są następujące:</span><span class="sxs-lookup"><span data-stu-id="e62e6-145">The supported profiles are as follows:</span></span>

- <span data-ttu-id="e62e6-146">`client`: Profil klienta</span><span class="sxs-lookup"><span data-stu-id="e62e6-146">`client`: Client Profile</span></span>
- <span data-ttu-id="e62e6-147">`full`: Full Profile</span><span class="sxs-lookup"><span data-stu-id="e62e6-147">`full`: Full Profile</span></span>
- <span data-ttu-id="e62e6-148">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="e62e6-148">`wp`: Windows Phone</span></span>
- <span data-ttu-id="e62e6-149">`cf`: Compact Framework</span><span class="sxs-lookup"><span data-stu-id="e62e6-149">`cf`: Compact Framework</span></span>

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="e62e6-150">Określanie, która docelowa NuGet do użycia</span><span class="sxs-lookup"><span data-stu-id="e62e6-150">Determining which NuGet target to use</span></span>

<span data-ttu-id="e62e6-151">Podczas tworzenia pakietów bibliotek przeznaczonych przenośnej biblioteki klas może być trudnych do określenia docelowej NuGet, których należy używać w nazwach folderów i `.nuspec` plik, zwłaszcza, jeśli celem tylko podzestaw PCL.</span><span class="sxs-lookup"><span data-stu-id="e62e6-151">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="e62e6-152">Następujące zasoby zewnętrzne mogą pomóc w tym:</span><span class="sxs-lookup"><span data-stu-id="e62e6-152">The following external resources will help you with this:</span></span>

- <span data-ttu-id="e62e6-153">[Profile Framework w .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span><span class="sxs-lookup"><span data-stu-id="e62e6-153">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span></span>
- <span data-ttu-id="e62e6-154">[Profile biblioteki klas przenośnych](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Tabela wyliczanie profilów PCL i ich równoważne celów NuGet</span><span class="sxs-lookup"><span data-stu-id="e62e6-154">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="e62e6-155">[Przenośnej biblioteki klas profile narzędzie](https://github.com/StephenCleary/PortableLibraryProfiles) (witryną github.com): narzędzie wiersza polecenia, określając PCL profile dostępna w systemie</span><span class="sxs-lookup"><span data-stu-id="e62e6-155">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="e62e6-156">Pliki zawartości i skryptów programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="e62e6-156">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="e62e6-157">Modyfikowalne pliki zawartości i wykonywanie skryptu są dostępne z `packages.config` tylko format; są one przestarzałe, korzystając z `project.json` i PackagesReference formatuje i powinien nie powinna być używana dla dowolnego nowego pakietu.</span><span class="sxs-lookup"><span data-stu-id="e62e6-157">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated when using `project.json` and PackagesReference formats and should should not be used for any new packages.</span></span>

<span data-ttu-id="e62e6-158">Z `packages.config`, zawartości plików i skryptów programu PowerShell można przedstawić w rozbiciu platformy docelowej przy użyciu tej samej Konwencji folder wewnątrz `content` i `tools` folderów.</span><span class="sxs-lookup"><span data-stu-id="e62e6-158">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="e62e6-159">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e62e6-159">For example:</span></span>

    \content
        \net46
            \MyContent.txt
        \net461
            \MyContent461.txt
        \uap
            \MyUWPContent.html
        \netcore
    \tools
        init.ps1
        \net46
            install.ps1
            uninstall.ps1
        \uap
            install.ps1
            uninstall.ps1

<span data-ttu-id="e62e6-160">Jeśli w folderze struktury jest puste, NuGet nie dodać odwołania do zestawów ani plików zawartości i uruchamiać skrypty programu PowerShell dla tej struktury.</span><span class="sxs-lookup"><span data-stu-id="e62e6-160">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="e62e6-161">Ponieważ `init.ps1` jest wykonywany rozwiązania poziomu i nie jest zależna od projektu, należy umieścić bezpośrednio pod `tools` folderu.</span><span class="sxs-lookup"><span data-stu-id="e62e6-161">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="e62e6-162">Jest ona ignorowana, jeśli umieszczony w folderze struktury.</span><span class="sxs-lookup"><span data-stu-id="e62e6-162">It's ignored if placed under a framework folder.</span></span>
