---
title: Wiele elementów docelowych dla pakietów NuGet
description: Opis różnych metod ukierunkowanych na wiele wersji .NET Framework z jednego pakietu NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: d12b12c4670f5dcb4c1e7e475d77926bd5d3935b
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342500"
---
# <a name="support-multiple-net-versions"></a><span data-ttu-id="0e3d4-103">Obsługa wielu wersji platformy .NET</span><span class="sxs-lookup"><span data-stu-id="0e3d4-103">Support multiple .NET versions</span></span>

<span data-ttu-id="0e3d4-104">Wiele bibliotek jest przeznaczonych dla określonej wersji .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-104">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="0e3d4-105">Na przykład może istnieć jedna wersja biblioteki, która jest specyficzna dla platformy UWP, oraz inna wersja, która wykorzystuje funkcje w .NET Framework 4,6.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-105">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span> <span data-ttu-id="0e3d4-106">Aby to umożliwić, pakiet NuGet obsługuje umieszczanie wielu wersji tej samej biblioteki w jednym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-106">To accommodate this, NuGet supports putting multiple versions of the same library in a single package.</span></span>

<span data-ttu-id="0e3d4-107">W tym artykule opisano układ pakietu NuGet, niezależnie od tego, w jaki sposób pakiet lub zestawy zostały skompilowane (oznacza to, że układ jest taki sam, niezależnie od tego, czy jest używany wiele plików *csproj.*  SDK — style *. csproj*).</span><span class="sxs-lookup"><span data-stu-id="0e3d4-107">This article describes the layout of a NuGet package, regardless of how the package or assemblies are built (that is, the layout is the same whether using multiple non-SDK-style *.csproj* files and a custom *.nuspec* file, or a single multi-targetecd SDK-style *.csproj*).</span></span> <span data-ttu-id="0e3d4-108">W przypadku projektu w stylu zestawu SDK [elementy docelowe pakietu](../reference/msbuild-targets.md) NuGet wiedzą, w jaki sposób pakiet musi być layed i automatyzuje umieszczanie zestawów w poprawnych folderach lib i tworzenie grup zależności dla każdej platformy docelowej (TFM).</span><span class="sxs-lookup"><span data-stu-id="0e3d4-108">For an SDK-style project, NuGet [pack targets](../reference/msbuild-targets.md) knows how the package must be layed out and automates putting the assemblies in the correct lib folders and creating dependency groups for each target framework (TFM).</span></span> <span data-ttu-id="0e3d4-109">Aby uzyskać szczegółowe instrukcje, zobacz [Obsługa wielu wersji .NET Framework w pliku projektu](multiple-target-frameworks-project-file.md).</span><span class="sxs-lookup"><span data-stu-id="0e3d4-109">For detailed instructions, see [Support multiple .NET Framework versions in your project file](multiple-target-frameworks-project-file.md).</span></span>

<span data-ttu-id="0e3d4-110">Należy ręcznie określić pakiet, zgodnie z opisem w tym artykule w przypadku korzystania z metody katalogu roboczego opartej na Konwencji opisanej w temacie [Tworzenie pakietu](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="0e3d4-110">You must manually lay out the package as described in this article when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> <span data-ttu-id="0e3d4-111">W przypadku projektu w stylu zestawu SDK zaleca się metodę zautomatyzowaną, ale można również ręcznie określić układ pakietu zgodnie z opisem w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-111">For an SDK-style project, the automated method is recommended, but you may also choose to manually lay out the package as described in this article.</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="0e3d4-112">Struktura folderu wersji struktury</span><span class="sxs-lookup"><span data-stu-id="0e3d4-112">Framework version folder structure</span></span>

<span data-ttu-id="0e3d4-113">Podczas kompilowania pakietu zawierającego tylko jedną wersję biblioteki lub docelową wiele struktur, należy zawsze tworzyć podfoldery w `lib` ramach różnych nazw struktur uwzględniających wielkość liter w następującej konwencji:</span><span class="sxs-lookup"><span data-stu-id="0e3d4-113">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="0e3d4-114">Aby uzyskać pełną listę obsługiwanych nazw, zobacz [Dokumentacja platformy docelowej](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="0e3d4-114">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="0e3d4-115">Nigdy nie należy mieć wersji biblioteki, która nie jest specyficzna dla struktury i umieszczona bezpośrednio w folderze głównym `lib` .</span><span class="sxs-lookup"><span data-stu-id="0e3d4-115">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="0e3d4-116">(Ta funkcja była obsługiwana tylko w `packages.config`systemie).</span><span class="sxs-lookup"><span data-stu-id="0e3d4-116">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="0e3d4-117">Dzięki temu biblioteka będzie zgodna z żadną platformą docelową i będzie można ją zainstalować w dowolnym miejscu, co może spowodować nieoczekiwane błędy w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-117">Doing so would make the library compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="0e3d4-118">Dodawanie zestawów w folderze głównym (takim jak `lib\abc.dll`) lub podfolderach (takich jak `lib\abc\abc.dll`) zostało zaniechane i jest ignorowane w przypadku używania formatu PackagesReference.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-118">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="0e3d4-119">Na przykład następująca struktura folderów obsługuje cztery wersje zestawu, który jest specyficzny dla platformy:</span><span class="sxs-lookup"><span data-stu-id="0e3d4-119">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="0e3d4-120">Aby łatwo uwzględnić wszystkie te pliki podczas kompilowania pakietu, użyj cyklicznego `**` symbolu wieloznacznego `<files>` w sekcji `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="0e3d4-120">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="0e3d4-121">Foldery specyficzne dla architektury</span><span class="sxs-lookup"><span data-stu-id="0e3d4-121">Architecture-specific folders</span></span>

<span data-ttu-id="0e3d4-122">W przypadku zestawów specyficznych dla architektury, czyli oddzielnych zestawów przeznaczonych dla ARM, x86 i x64, należy umieścić je w folderze o `runtimes` nazwie w podfolderach o nazwie `{platform}-{architecture}\lib\{framework}` lub `{platform}-{architecture}\native`.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-122">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="0e3d4-123">Na przykład następująca struktura folderów będzie obsługiwać natywne i zarządzane biblioteki DLL przeznaczone dla systemu Windows 10 i `uap10.0` platformy:</span><span class="sxs-lookup"><span data-stu-id="0e3d4-123">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

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

<span data-ttu-id="0e3d4-124">Te zestawy będą dostępne tylko w czasie wykonywania, dlatego jeśli chcesz podać odpowiedni zestaw czasu kompilacji, a następnie `AnyCPU` zestaw w `/ref{tfm}` folderze.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-124">These assemblies will only be available at runtime, so if you want to provide the corresponding compile time assembly as well then have `AnyCPU` assembly in `/ref{tfm}` folder.</span></span> 

<span data-ttu-id="0e3d4-125">Należy pamiętać, że pakiet NuGet zawsze wybiera te zasoby kompilacji lub środowiska uruchomieniowego z jednego folderu, więc jeśli istnieją `/ref` pewne `/lib` zgodne zasoby z tej wersji, zostaną zignorowane w celu dodania zestawów czasu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-125">Please note, NuGet always picks these compile or runtime assets from one folder so if there are some compatible assets from `/ref` then `/lib` will be ignored to add compile-time assemblies.</span></span> <span data-ttu-id="0e3d4-126">Podobnie, jeśli istnieją pewne zasoby `/runtime` compatbile, również `/lib` zostaną zignorowane dla środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-126">Similarly, if there are some compatbile assets from `/runtime` then also `/lib` will be ignored for runtime.</span></span>

<span data-ttu-id="0e3d4-127">Zobacz [Tworzenie pakietów platformy UWP](../guides/create-uwp-packages.md) na przykład odwoływania się do tych plików w `.nuspec` manifeście.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-127">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

<span data-ttu-id="0e3d4-128">Zobacz też artykuł [pakowanie składnika aplikacji ze sklepu Windows za pomocą narzędzia NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span><span class="sxs-lookup"><span data-stu-id="0e3d4-128">Also, see [Packing a Windows store app component with NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="0e3d4-129">Dopasowanie wersji zestawu i platformy docelowej w projekcie</span><span class="sxs-lookup"><span data-stu-id="0e3d4-129">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="0e3d4-130">Gdy narzędzie NuGet zainstaluje pakiet z wieloma wersjami zestawu, próbuje dopasować nazwę platformy do zestawu przy użyciu platformy docelowej projektu.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-130">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="0e3d4-131">Jeśli dopasowanie nie zostanie znalezione, pakiet NuGet kopiuje zestaw dla najwyższej wersji, która jest mniejsza lub równa docelowej platformy projektu, jeśli jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-131">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="0e3d4-132">Jeśli nie odnaleziono zgodnego zestawu, pakiet NuGet zwróci odpowiedni komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-132">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="0e3d4-133">Rozważmy na przykład następującą strukturę folderów w pakiecie:</span><span class="sxs-lookup"><span data-stu-id="0e3d4-133">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="0e3d4-134">Podczas instalowania tego pakietu w projekcie, który jest przeznaczony dla .NET Framework 4,6, pakiet NuGet instaluje zestaw `net45` w folderze, ponieważ jest to najwyższa dostępna wersja, która jest mniejsza lub równa 4,6.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-134">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="0e3d4-135">Jeśli projekt jest przeznaczony .NET Framework 4.6.1, z drugiej strony pakiet NuGet instaluje zestaw w `net461` folderze.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-135">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="0e3d4-136">Jeśli projekt jest przeznaczony dla programu .NET Framework 4,0 i jego wcześniejszych wersji, pakiet NuGet zgłasza odpowiedni komunikat o błędzie, aby nie znaleźć zgodnego zestawu.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-136">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="0e3d4-137">Grupowanie zestawów według wersji struktury</span><span class="sxs-lookup"><span data-stu-id="0e3d4-137">Grouping assemblies by framework version</span></span>

<span data-ttu-id="0e3d4-138">Pakiet NuGet kopiuje zestawy tylko z jednego folderu biblioteki w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-138">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="0e3d4-139">Załóżmy na przykład, że pakiet ma następującą strukturę folderów:</span><span class="sxs-lookup"><span data-stu-id="0e3d4-139">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="0e3d4-140">Gdy pakiet jest zainstalowany w projekcie, który jest przeznaczony dla .NET Framework 4,5 `MyAssembly.dll` , (v 2.0) jest jedynym zainstalowanym zestawem.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-140">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="0e3d4-141">`MyAssembly.Core.dll`(wersja 1.0) nie jest zainstalowana, `net45` ponieważ nie znajduje się ona w folderze.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-141">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="0e3d4-142">Pakiet NuGet działa w ten sposób `MyAssembly.Core.dll` , ponieważ mógł zostać scalony w `MyAssembly.dll`wersji 2,0 programu.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-142">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="0e3d4-143">Jeśli chcesz `MyAssembly.Core.dll` zainstalować program dla .NET Framework 4,5, Umieść kopię `net45` w folderze.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-143">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="0e3d4-144">Grupowanie zestawów według profilu struktury</span><span class="sxs-lookup"><span data-stu-id="0e3d4-144">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="0e3d4-145">Pakiet NuGet obsługuje również określanie konkretnego profilu struktury przez dołączenie kreski i nazwy profilu do końca folderu.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-145">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="0e3d4-146">Obsługiwane są następujące profile:</span><span class="sxs-lookup"><span data-stu-id="0e3d4-146">The supported profiles are as follows:</span></span>

- <span data-ttu-id="0e3d4-147">`client`: Profil klienta</span><span class="sxs-lookup"><span data-stu-id="0e3d4-147">`client`: Client Profile</span></span>
- <span data-ttu-id="0e3d4-148">`full`: Pełny profil</span><span class="sxs-lookup"><span data-stu-id="0e3d4-148">`full`: Full Profile</span></span>
- <span data-ttu-id="0e3d4-149">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="0e3d4-149">`wp`: Windows Phone</span></span>
- <span data-ttu-id="0e3d4-150">`cf`: Platforma kompaktowa</span><span class="sxs-lookup"><span data-stu-id="0e3d4-150">`cf`: Compact Framework</span></span>

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="0e3d4-151">Ustalanie, który obiekt docelowy NuGet ma być używany</span><span class="sxs-lookup"><span data-stu-id="0e3d4-151">Determining which NuGet target to use</span></span>

<span data-ttu-id="0e3d4-152">W przypadku bibliotek opakowaniowych przeznaczonych dla przenośnej biblioteki klas może być to konieczne, aby określić, który obiekt docelowy NuGet ma być `.nuspec` używany w nazwach folderów i pliku, szczególnie w przypadku określania tylko podzestawu PCL.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-152">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="0e3d4-153">Następujące zasoby zewnętrzne pomogą Ci:</span><span class="sxs-lookup"><span data-stu-id="0e3d4-153">The following external resources will help you with this:</span></span>

- <span data-ttu-id="0e3d4-154">[Profile struktury w programie .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span><span class="sxs-lookup"><span data-stu-id="0e3d4-154">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span></span>
- <span data-ttu-id="0e3d4-155">[Profile biblioteki klas przenośnych](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Tabela wyliczanie profilów PCL i ich równoważne cele NuGet</span><span class="sxs-lookup"><span data-stu-id="0e3d4-155">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="0e3d4-156">[Narzędzie profilów biblioteki klas przenośnych](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): Narzędzie wiersza polecenia do określania profilów PCL dostępnych w systemie</span><span class="sxs-lookup"><span data-stu-id="0e3d4-156">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="0e3d4-157">Pliki zawartości i skrypty programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e3d4-157">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="0e3d4-158">Modyfikowalne pliki zawartości i wykonywanie skryptów są dostępne `packages.config` tylko w formacie. są one przestarzałe ze wszystkimi innymi formatami i nie powinny być używane dla żadnych nowych pakietów.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-158">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="0e3d4-159">W `packages.config`programie pliki zawartości i skrypty programu PowerShell mogą być pogrupowane według platformy docelowej przy użyciu tej samej Konwencji `content` folderów `tools` w folderach i.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-159">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="0e3d4-160">Przykład:</span><span class="sxs-lookup"><span data-stu-id="0e3d4-160">For example:</span></span>

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

<span data-ttu-id="0e3d4-161">Jeśli folder struktury pozostanie pusty, pakiet NuGet nie dodaje odwołań do zestawu ani plików zawartości ani nie uruchamia skryptów programu PowerShell dla tej struktury.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-161">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="0e3d4-162">Ponieważ `init.ps1` jest wykonywany na poziomie rozwiązania i nie zależy od projektu, musi być umieszczony bezpośrednio `tools` w folderze.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-162">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="0e3d4-163">Ta wartość jest ignorowana, jeśli jest umieszczona w folderze struktury.</span><span class="sxs-lookup"><span data-stu-id="0e3d4-163">It's ignored if placed under a framework folder.</span></span>
