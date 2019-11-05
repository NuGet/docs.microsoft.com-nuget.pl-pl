---
title: Wiele elementów docelowych dla pakietów NuGet
description: Opis różnych metod ukierunkowanych na wiele wersji .NET Framework z jednego pakietu NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 69e12ce1c78f8d4d50cbad7a0237d767064193ab
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610649"
---
# <a name="support-multiple-net-versions"></a><span data-ttu-id="6dc57-103">Obsługa wielu wersji platformy .NET</span><span class="sxs-lookup"><span data-stu-id="6dc57-103">Support multiple .NET versions</span></span>

<span data-ttu-id="6dc57-104">Wiele bibliotek jest przeznaczonych dla określonej wersji .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="6dc57-104">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="6dc57-105">Na przykład może istnieć jedna wersja biblioteki, która jest specyficzna dla platformy UWP, oraz inna wersja, która wykorzystuje funkcje w .NET Framework 4,6.</span><span class="sxs-lookup"><span data-stu-id="6dc57-105">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span> <span data-ttu-id="6dc57-106">Aby to umożliwić, pakiet NuGet obsługuje umieszczanie wielu wersji tej samej biblioteki w jednym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="6dc57-106">To accommodate this, NuGet supports putting multiple versions of the same library in a single package.</span></span>

<span data-ttu-id="6dc57-107">W tym artykule opisano układ pakietu NuGet, niezależnie od tego, w jaki sposób pakiet lub zestawy zostały skompilowane (oznacza to, że układ jest taki sam, niezależnie od tego, czy jest używany *wiele plików* *csproj.* SDK — style *. csproj*).</span><span class="sxs-lookup"><span data-stu-id="6dc57-107">This article describes the layout of a NuGet package, regardless of how the package or assemblies are built (that is, the layout is the same whether using multiple non-SDK-style *.csproj* files and a custom *.nuspec* file, or a single multi-targeted SDK-style *.csproj*).</span></span> <span data-ttu-id="6dc57-108">W przypadku projektu w stylu zestawu SDK [elementy docelowe pakietu](../reference/msbuild-targets.md) NuGet wiedzą, w jaki sposób pakiet musi być layed i automatyzuje umieszczanie zestawów w poprawnych folderach lib i tworzenie grup zależności dla każdej platformy docelowej (TFM).</span><span class="sxs-lookup"><span data-stu-id="6dc57-108">For an SDK-style project, NuGet [pack targets](../reference/msbuild-targets.md) knows how the package must be layed out and automates putting the assemblies in the correct lib folders and creating dependency groups for each target framework (TFM).</span></span> <span data-ttu-id="6dc57-109">Aby uzyskać szczegółowe instrukcje, zobacz [Obsługa wielu wersji .NET Framework w pliku projektu](multiple-target-frameworks-project-file.md).</span><span class="sxs-lookup"><span data-stu-id="6dc57-109">For detailed instructions, see [Support multiple .NET Framework versions in your project file](multiple-target-frameworks-project-file.md).</span></span>

<span data-ttu-id="6dc57-110">Należy ręcznie określić pakiet, zgodnie z opisem w tym artykule w przypadku korzystania z metody katalogu roboczego opartej na Konwencji opisanej w temacie [Tworzenie pakietu](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="6dc57-110">You must manually lay out the package as described in this article when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> <span data-ttu-id="6dc57-111">W przypadku projektu w stylu zestawu SDK zaleca się metodę zautomatyzowaną, ale można również ręcznie określić układ pakietu zgodnie z opisem w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="6dc57-111">For an SDK-style project, the automated method is recommended, but you may also choose to manually lay out the package as described in this article.</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="6dc57-112">Struktura folderu wersji struktury</span><span class="sxs-lookup"><span data-stu-id="6dc57-112">Framework version folder structure</span></span>

<span data-ttu-id="6dc57-113">Podczas kompilowania pakietu, który zawiera tylko jedną wersję biblioteki lub docelową wiele struktur, należy zawsze tworzyć podfoldery w `lib` przy użyciu różnych nazw struktur uwzględniających wielkość liter z następującą konwencją:</span><span class="sxs-lookup"><span data-stu-id="6dc57-113">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="6dc57-114">Aby uzyskać pełną listę obsługiwanych nazw, zobacz [Dokumentacja platformy docelowej](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="6dc57-114">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="6dc57-115">Nigdy nie należy mieć wersji biblioteki, która nie jest specyficzna dla struktury i umieszczona bezpośrednio w folderze głównym `lib`.</span><span class="sxs-lookup"><span data-stu-id="6dc57-115">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="6dc57-116">(Ta funkcja była obsługiwana tylko z `packages.config`).</span><span class="sxs-lookup"><span data-stu-id="6dc57-116">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="6dc57-117">Dzięki temu biblioteka będzie zgodna z żadną platformą docelową i będzie można ją zainstalować w dowolnym miejscu, co może spowodować nieoczekiwane błędy w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="6dc57-117">Doing so would make the library compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="6dc57-118">Dodawanie zestawów w folderze głównym (na przykład `lib\abc.dll`) lub podfolderach (takich jak `lib\abc\abc.dll`) zostało zaniechane i jest ignorowane w przypadku używania formatu PackagesReference.</span><span class="sxs-lookup"><span data-stu-id="6dc57-118">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="6dc57-119">Na przykład następująca struktura folderów obsługuje cztery wersje zestawu, który jest specyficzny dla platformy:</span><span class="sxs-lookup"><span data-stu-id="6dc57-119">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="6dc57-120">Aby łatwo uwzględnić wszystkie te pliki podczas kompilowania pakietu, użyj cyklicznego symbolu wieloznacznego `**` w sekcji `<files>` `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="6dc57-120">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="6dc57-121">Foldery specyficzne dla architektury</span><span class="sxs-lookup"><span data-stu-id="6dc57-121">Architecture-specific folders</span></span>

<span data-ttu-id="6dc57-122">W przypadku zestawów specyficznych dla architektury, czyli oddzielnych zestawów przeznaczonych dla ARM, x86 i x64, należy umieścić je w folderze o nazwie `runtimes` w podfolderach o nazwie `{platform}-{architecture}\lib\{framework}` lub `{platform}-{architecture}\native`.</span><span class="sxs-lookup"><span data-stu-id="6dc57-122">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="6dc57-123">Na przykład następująca struktura folderów dotyczy zarówno natywnej, jak i zarządzanej biblioteki DLL przeznaczonej dla systemu Windows 10 i platformy `uap10.0`:</span><span class="sxs-lookup"><span data-stu-id="6dc57-123">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

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

<span data-ttu-id="6dc57-124">Te zestawy będą dostępne tylko w czasie wykonywania, dlatego jeśli chcesz podać odpowiedni zestaw czasu kompilacji, a następnie `AnyCPU` Assembly w folderze `/ref/{tfm}`.</span><span class="sxs-lookup"><span data-stu-id="6dc57-124">These assemblies will only be available at runtime, so if you want to provide the corresponding compile time assembly as well then have `AnyCPU` assembly in `/ref/{tfm}` folder.</span></span> 

<span data-ttu-id="6dc57-125">Należy pamiętać, że pakiet NuGet zawsze wybiera te zasoby kompilacji lub środowiska uruchomieniowego z jednego folderu, więc jeśli istnieją pewne zgodne zasoby z `/ref`, `/lib` zostanie zignorowane w celu dodania zestawów czasu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="6dc57-125">Please note, NuGet always picks these compile or runtime assets from one folder so if there are some compatible assets from `/ref` then `/lib` will be ignored to add compile-time assemblies.</span></span> <span data-ttu-id="6dc57-126">Podobnie, jeśli istnieją pewne zgodne zasoby z `/runtime`, wówczas `/lib` zostanie zignorowane dla środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="6dc57-126">Similarly, if there are some compatible assets from `/runtime` then also `/lib` will be ignored for runtime.</span></span>

<span data-ttu-id="6dc57-127">Zobacz [Tworzenie pakietów platformy UWP](../guides/create-uwp-packages.md) na przykład odwoływania się do tych plików w manifeście `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="6dc57-127">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

<span data-ttu-id="6dc57-128">Zobacz też artykuł [pakowanie składnika aplikacji ze sklepu Windows za pomocą narzędzia NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span><span class="sxs-lookup"><span data-stu-id="6dc57-128">Also, see [Packing a Windows store app component with NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="6dc57-129">Dopasowanie wersji zestawu i platformy docelowej w projekcie</span><span class="sxs-lookup"><span data-stu-id="6dc57-129">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="6dc57-130">Gdy narzędzie NuGet zainstaluje pakiet z wieloma wersjami zestawu, próbuje dopasować nazwę platformy do zestawu przy użyciu platformy docelowej projektu.</span><span class="sxs-lookup"><span data-stu-id="6dc57-130">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="6dc57-131">Jeśli dopasowanie nie zostanie znalezione, pakiet NuGet kopiuje zestaw dla najwyższej wersji, która jest mniejsza lub równa docelowej platformy projektu, jeśli jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="6dc57-131">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="6dc57-132">Jeśli nie odnaleziono zgodnego zestawu, pakiet NuGet zwróci odpowiedni komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="6dc57-132">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="6dc57-133">Rozważmy na przykład następującą strukturę folderów w pakiecie:</span><span class="sxs-lookup"><span data-stu-id="6dc57-133">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="6dc57-134">Podczas instalowania tego pakietu w projekcie, który jest przeznaczony dla .NET Framework 4,6, pakiet NuGet instaluje zestaw w folderze `net45`, ponieważ to jest najwyższa dostępna wersja, która jest mniejsza lub równa 4,6.</span><span class="sxs-lookup"><span data-stu-id="6dc57-134">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="6dc57-135">Jeśli projekt jest przeznaczony .NET Framework 4.6.1, z drugiej strony pakiet NuGet instaluje zestaw w folderze `net461`.</span><span class="sxs-lookup"><span data-stu-id="6dc57-135">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="6dc57-136">Jeśli projekt jest przeznaczony dla programu .NET Framework 4,0 i jego wcześniejszych wersji, pakiet NuGet zgłasza odpowiedni komunikat o błędzie, aby nie znaleźć zgodnego zestawu.</span><span class="sxs-lookup"><span data-stu-id="6dc57-136">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="6dc57-137">Grupowanie zestawów według wersji struktury</span><span class="sxs-lookup"><span data-stu-id="6dc57-137">Grouping assemblies by framework version</span></span>

<span data-ttu-id="6dc57-138">Pakiet NuGet kopiuje zestawy tylko z jednego folderu biblioteki w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="6dc57-138">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="6dc57-139">Załóżmy na przykład, że pakiet ma następującą strukturę folderów:</span><span class="sxs-lookup"><span data-stu-id="6dc57-139">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="6dc57-140">Gdy pakiet jest zainstalowany w projekcie, który jest przeznaczony dla .NET Framework 4,5, `MyAssembly.dll` (v 2.0) jest jedynym zainstalowanym zestawem.</span><span class="sxs-lookup"><span data-stu-id="6dc57-140">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="6dc57-141">`MyAssembly.Core.dll` (v 1.0) nie jest zainstalowany, ponieważ nie znajduje się w folderze `net45`.</span><span class="sxs-lookup"><span data-stu-id="6dc57-141">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="6dc57-142">Pakiet NuGet działa w ten sposób, ponieważ `MyAssembly.Core.dll` mogło zostać scalone w wersji 2,0 z `MyAssembly.dll`.</span><span class="sxs-lookup"><span data-stu-id="6dc57-142">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="6dc57-143">Jeśli chcesz zainstalować `MyAssembly.Core.dll` dla .NET Framework 4,5, Umieść kopię w folderze `net45`.</span><span class="sxs-lookup"><span data-stu-id="6dc57-143">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="6dc57-144">Grupowanie zestawów według profilu struktury</span><span class="sxs-lookup"><span data-stu-id="6dc57-144">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="6dc57-145">Pakiet NuGet obsługuje również określanie konkretnego profilu struktury przez dołączenie kreski i nazwy profilu do końca folderu.</span><span class="sxs-lookup"><span data-stu-id="6dc57-145">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="6dc57-146">Obsługiwane są następujące profile:</span><span class="sxs-lookup"><span data-stu-id="6dc57-146">The supported profiles are as follows:</span></span>

- <span data-ttu-id="6dc57-147">`client`: profil klienta</span><span class="sxs-lookup"><span data-stu-id="6dc57-147">`client`: Client Profile</span></span>
- <span data-ttu-id="6dc57-148">`full`: pełny profil</span><span class="sxs-lookup"><span data-stu-id="6dc57-148">`full`: Full Profile</span></span>
- <span data-ttu-id="6dc57-149">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="6dc57-149">`wp`: Windows Phone</span></span>
- <span data-ttu-id="6dc57-150">`cf`: Compact Framework</span><span class="sxs-lookup"><span data-stu-id="6dc57-150">`cf`: Compact Framework</span></span>

## <a name="declaring-dependencies-advanced"></a><span data-ttu-id="6dc57-151">Deklarowanie zależności (Zaawansowane)</span><span class="sxs-lookup"><span data-stu-id="6dc57-151">Declaring dependencies (Advanced)</span></span>

<span data-ttu-id="6dc57-152">Podczas pakowania pliku projektu, pakiet NuGet próbuje automatycznie wygenerować zależności od projektu.</span><span class="sxs-lookup"><span data-stu-id="6dc57-152">When packing a project file, NuGet tries to automatically generate the dependencies from the project.</span></span> <span data-ttu-id="6dc57-153">Informacje przedstawione w tej sekcji dotyczące używania pliku *. nuspec* do deklarowania zależności są zwykle wymagane tylko w przypadku zaawansowanych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="6dc57-153">The information in this section about using a *.nuspec* file to declare dependencies is typically necessary for advanced scenarios only.</span></span>

<span data-ttu-id="6dc57-154">*(Wersja 2.0 +)* Zależności pakietu można zadeklarować w elemencie *. nuspec* odpowiadającym platformie docelowej projektu docelowego za pomocą elementów `<group>` w obrębie elementu `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="6dc57-154">*(Version 2.0+)* You can declare package dependencies in the *.nuspec* corresponding to the target framework of the target project using `<group>` elements within the `<dependencies>` element.</span></span> <span data-ttu-id="6dc57-155">Aby uzyskać więcej informacji, zobacz [zależności elementu](../reference/nuspec.md#dependencies-element).</span><span class="sxs-lookup"><span data-stu-id="6dc57-155">For more information, see [dependencies element](../reference/nuspec.md#dependencies-element).</span></span>

<span data-ttu-id="6dc57-156">Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej elementów `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="6dc57-156">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="6dc57-157">Te zależności są instalowane razem, gdy struktura docelowa jest zgodna z profilem struktury projektu.</span><span class="sxs-lookup"><span data-stu-id="6dc57-157">Those dependencies are installed together when the target framework is compatible with the project's framework profile.</span></span> <span data-ttu-id="6dc57-158">Zobacz [Platformy docelowe](../reference/target-frameworks.md) dla dokładnych identyfikatorów platformy.</span><span class="sxs-lookup"><span data-stu-id="6dc57-158">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

<span data-ttu-id="6dc57-159">Zalecamy używanie jednej grupy na potrzeby monikera platformy docelowej (TFM) dla plików w *bibliotekach lib/* i *ref/* foldery.</span><span class="sxs-lookup"><span data-stu-id="6dc57-159">We recommend using one group per Target Framework Moniker (TFM) for files in the *lib/* and *ref/* folders.</span></span>

<span data-ttu-id="6dc57-160">W poniższym przykładzie przedstawiono różne odmiany elementu `<group>`:</span><span class="sxs-lookup"><span data-stu-id="6dc57-160">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>

    <group targetFramework="net472">
        <dependency id="jQuery" version="1.10.2" />
        <dependency id="WebActivatorEx" version="2.2.0" />
    </group>

    <group targetFramework="net20">
    </group>

</dependencies>
```

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="6dc57-161">Ustalanie, który obiekt docelowy NuGet ma być używany</span><span class="sxs-lookup"><span data-stu-id="6dc57-161">Determining which NuGet target to use</span></span>

<span data-ttu-id="6dc57-162">W przypadku bibliotek opakowaniowych przeznaczonych dla przenośnej biblioteki klas może być to konieczne, aby określić, który obiekt docelowy NuGet ma być używany w nazwach folderów i pliku `.nuspec`, szczególnie w przypadku określania tylko podzestawu PCL.</span><span class="sxs-lookup"><span data-stu-id="6dc57-162">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="6dc57-163">Następujące zasoby zewnętrzne pomogą Ci:</span><span class="sxs-lookup"><span data-stu-id="6dc57-163">The following external resources will help you with this:</span></span>

- <span data-ttu-id="6dc57-164">[Profile struktury w programie .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span><span class="sxs-lookup"><span data-stu-id="6dc57-164">[Framework profiles in .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span></span>
- <span data-ttu-id="6dc57-165">[Profile biblioteki klas przenośnych](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): tabele wyliczające profile PCL i ich równoważne cele NuGet</span><span class="sxs-lookup"><span data-stu-id="6dc57-165">[Portable Class Library profiles](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="6dc57-166">[Narzędzie profilów biblioteki klas przenośnych](https://github.com/StephenCleary/PortableLibraryProfiles) (GitHub.com): Narzędzie wiersza polecenia służące do określania profilów PCL dostępnych w systemie.</span><span class="sxs-lookup"><span data-stu-id="6dc57-166">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="6dc57-167">Pliki zawartości i skrypty programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="6dc57-167">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="6dc57-168">Modyfikowalne pliki zawartości i wykonywanie skryptów są dostępne tylko w formacie `packages.config`. są one przestarzałe ze wszystkimi innymi formatami i nie powinny być używane dla żadnych nowych pakietów.</span><span class="sxs-lookup"><span data-stu-id="6dc57-168">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="6dc57-169">W przypadku `packages.config` pliki zawartości i skrypty programu PowerShell mogą być pogrupowane według platformy docelowej przy użyciu tej samej Konwencji folderów w folderach `content` i `tools`.</span><span class="sxs-lookup"><span data-stu-id="6dc57-169">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="6dc57-170">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="6dc57-170">For example:</span></span>

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

<span data-ttu-id="6dc57-171">Jeśli folder struktury pozostanie pusty, pakiet NuGet nie dodaje odwołań do zestawu ani plików zawartości ani nie uruchamia skryptów programu PowerShell dla tej struktury.</span><span class="sxs-lookup"><span data-stu-id="6dc57-171">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="6dc57-172">Ponieważ `init.ps1` jest wykonywany na poziomie rozwiązania i nie zależy od projektu, musi być umieszczony bezpośrednio w folderze `tools`.</span><span class="sxs-lookup"><span data-stu-id="6dc57-172">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="6dc57-173">Ta wartość jest ignorowana, jeśli jest umieszczona w folderze struktury.</span><span class="sxs-lookup"><span data-stu-id="6dc57-173">It's ignored if placed under a framework folder.</span></span>
