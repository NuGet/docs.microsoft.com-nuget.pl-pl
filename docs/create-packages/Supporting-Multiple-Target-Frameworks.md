---
title: Wielokierunkowe dla pakietów NuGet
description: Opis różnych metod do docelowych wielu wersji programu .NET Framework z jednego pakietu NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 34f7c6132ba6050e20114642932ccf29a5ec088d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429011"
---
# <a name="support-multiple-net-versions"></a><span data-ttu-id="d8dea-103">Obsługa wielu wersji platformy .NET</span><span class="sxs-lookup"><span data-stu-id="d8dea-103">Support multiple .NET versions</span></span>

<span data-ttu-id="d8dea-104">Wiele bibliotek jest przeznaczone dla określonej wersji programu .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="d8dea-104">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="d8dea-105">Na przykład może mieć jedną wersję biblioteki, która jest specyficzna dla platformy uniwersalnej systemu i innej wersji, która korzysta z funkcji w .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="d8dea-105">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span> <span data-ttu-id="d8dea-106">Aby to uwzględnić, NuGet obsługuje umieszczanie wielu wersji tej samej biblioteki w jednym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="d8dea-106">To accommodate this, NuGet supports putting multiple versions of the same library in a single package.</span></span>

<span data-ttu-id="d8dea-107">W tym artykule opisano układ pakietu NuGet, niezależnie od sposobu zbudowania pakietu lub zestawów (oznacza to, że układ jest taki sam, czy przy użyciu wielu plików *csproj* w stylu innych niż SDK i niestandardowego pliku *nuspec,* czy pojedynczego wielokierunkowego zestawu SDK w stylu *csproj*).</span><span class="sxs-lookup"><span data-stu-id="d8dea-107">This article describes the layout of a NuGet package, regardless of how the package or assemblies are built (that is, the layout is the same whether using multiple non-SDK-style *.csproj* files and a custom *.nuspec* file, or a single multi-targeted SDK-style *.csproj*).</span></span> <span data-ttu-id="d8dea-108">W przypadku projektu w stylu zestawu SDK [obiekty docelowe pakietu](../reference/msbuild-targets.md) NuGet pack wie, jak pakiet musi być rozłożony i automatyzuje umieszczanie zestawów w odpowiednich folderach lib i tworzenie grup zależności dla każdej struktury docelowej (TFM).</span><span class="sxs-lookup"><span data-stu-id="d8dea-108">For an SDK-style project, NuGet [pack targets](../reference/msbuild-targets.md) knows how the package must be layed out and automates putting the assemblies in the correct lib folders and creating dependency groups for each target framework (TFM).</span></span> <span data-ttu-id="d8dea-109">Aby uzyskać szczegółowe instrukcje, zobacz [Obsługa wielu wersji programu .NET Framework w pliku projektu](multiple-target-frameworks-project-file.md).</span><span class="sxs-lookup"><span data-stu-id="d8dea-109">For detailed instructions, see [Support multiple .NET Framework versions in your project file](multiple-target-frameworks-project-file.md).</span></span>

<span data-ttu-id="d8dea-110">Należy ręcznie rozłożyć pakiet zgodnie z opisem w tym artykule podczas korzystania z metody katalogu roboczego opartego na konwencji [opisanej](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)w temacie Tworzenie pakietu .</span><span class="sxs-lookup"><span data-stu-id="d8dea-110">You must manually lay out the package as described in this article when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> <span data-ttu-id="d8dea-111">W przypadku projektu w stylu zestawu SDK zalecana jest metoda zautomatyzowana, ale można również ręcznie rozłożyć pakiet zgodnie z opisem w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="d8dea-111">For an SDK-style project, the automated method is recommended, but you may also choose to manually lay out the package as described in this article.</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="d8dea-112">Struktura folderów wersji frameworka</span><span class="sxs-lookup"><span data-stu-id="d8dea-112">Framework version folder structure</span></span>

<span data-ttu-id="d8dea-113">Podczas tworzenia pakietu, który zawiera tylko jedną wersję biblioteki lub docelowe `lib` wiele struktur, zawsze należy wykonać podfoldery w ramach przy użyciu różnych nazw struktury z uwzględnieniem wielkości liter z następującą konwencją:</span><span class="sxs-lookup"><span data-stu-id="d8dea-113">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="d8dea-114">Aby uzyskać pełną listę obsługiwanych nazw, zobacz [odwołanie do ram docelowych](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="d8dea-114">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="d8dea-115">Nigdy nie należy mieć wersji biblioteki, która nie jest specyficzna dla struktury i umieszczona bezpośrednio w folderze głównym. `lib`</span><span class="sxs-lookup"><span data-stu-id="d8dea-115">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="d8dea-116">(Ta funkcja była obsługiwana `packages.config`tylko z ).</span><span class="sxs-lookup"><span data-stu-id="d8dea-116">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="d8dea-117">W ten sposób sprawi, że biblioteka będzie zgodna z dowolną platformą docelową i pozwoli na zainstalowanie jej w dowolnym miejscu, co prawdopodobnie spowoduje nieoczekiwane błędy środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="d8dea-117">Doing so would make the library compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="d8dea-118">Dodawanie zestawów w folderze `lib\abc.dll`głównym (na przykład) `lib\abc\abc.dll`lub podfolderach (takich jak ) zostało przestarzałe i jest ignorowane podczas korzystania z formatu PackagesReference.</span><span class="sxs-lookup"><span data-stu-id="d8dea-118">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="d8dea-119">Na przykład następująca struktura folderów obsługuje cztery wersje zestawu, które są specyficzne dla struktury:</span><span class="sxs-lookup"><span data-stu-id="d8dea-119">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="d8dea-120">Aby łatwo dołączyć wszystkie te pliki podczas tworzenia pakietu, użyj `<files>` cyklicznego `.nuspec` `**` symbolu wieloznacznego w sekcji :</span><span class="sxs-lookup"><span data-stu-id="d8dea-120">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="d8dea-121">Foldery specyficzne dla architektury</span><span class="sxs-lookup"><span data-stu-id="d8dea-121">Architecture-specific folders</span></span>

<span data-ttu-id="d8dea-122">Jeśli masz zestawy specyficzne dla architektury, czyli oddzielne zestawy docelowe ARM, x86 i x64, `runtimes` należy umieścić je `{platform}-{architecture}\lib\{framework}` w `{platform}-{architecture}\native`folderze o nazwie w podfolderach o nazwie lub .</span><span class="sxs-lookup"><span data-stu-id="d8dea-122">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="d8dea-123">Na przykład następująca struktura folderów będzie uwzględniać zarówno natywne, `uap10.0` jak i zarządzane biblioteki DLL przeznaczone dla systemu Windows 10 i strukturę:</span><span class="sxs-lookup"><span data-stu-id="d8dea-123">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

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

<span data-ttu-id="d8dea-124">Te zestawy będą dostępne tylko w czasie wykonywania, więc jeśli chcesz podać odpowiedni `AnyCPU` zestaw `/ref/{tfm}` czasu kompilacji, a następnie mają zestaw w folderze.</span><span class="sxs-lookup"><span data-stu-id="d8dea-124">These assemblies will only be available at runtime, so if you want to provide the corresponding compile time assembly as well then have `AnyCPU` assembly in `/ref/{tfm}` folder.</span></span> 

<span data-ttu-id="d8dea-125">Należy pamiętać, NuGet zawsze wybiera te zasoby kompilacji lub środowiska uruchomieniowego z `/ref` `/lib` jednego folderu, więc jeśli istnieją pewne zgodne zasoby od tego czasu zostaną zignorowane, aby dodać zestawy w czasie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="d8dea-125">Please note, NuGet always picks these compile or runtime assets from one folder so if there are some compatible assets from `/ref` then `/lib` will be ignored to add compile-time assemblies.</span></span> <span data-ttu-id="d8dea-126">Podobnie, jeśli istnieją pewne zgodne `/runtimes` zasoby `/lib` od tego czasu również zostaną zignorowane dla środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="d8dea-126">Similarly, if there are some compatible assets from `/runtimes` then also `/lib` will be ignored for runtime.</span></span>

<span data-ttu-id="d8dea-127">Zobacz [Tworzenie pakietów platformy uniwersalnej](../guides/create-uwp-packages.md) systemu i `.nuspec` platformy uniwersalnej systemu, aby uzyskać przykład odwoływania się do tych plików w manifeście.</span><span class="sxs-lookup"><span data-stu-id="d8dea-127">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

<span data-ttu-id="d8dea-128">Zobacz [też: Pakowanie składnika aplikacji ze Sklepu Windows za pomocą usługi NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span><span class="sxs-lookup"><span data-stu-id="d8dea-128">Also, see [Packing a Windows store app component with NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="d8dea-129">Pasujące wersje zestawu i struktura docelowa w projekcie</span><span class="sxs-lookup"><span data-stu-id="d8dea-129">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="d8dea-130">Gdy NuGet instaluje pakiet, który ma wiele wersji zestawu, próbuje dopasować nazwę struktury zestawu z ramą docelową projektu.</span><span class="sxs-lookup"><span data-stu-id="d8dea-130">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="d8dea-131">Jeśli dopasowanie nie zostanie znalezione, NuGet kopiuje zestaw dla najwyższej wersji, która jest mniejsza lub równa platformie docelowej projektu, jeśli jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="d8dea-131">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="d8dea-132">Jeśli nie znaleziono zgodnego zestawu, NuGet zwraca odpowiedni komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="d8dea-132">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="d8dea-133">Rozważmy na przykład następującą strukturę folderów w pakiecie:</span><span class="sxs-lookup"><span data-stu-id="d8dea-133">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="d8dea-134">Podczas instalowania tego pakietu w projekcie, który jest przeznaczony dla platformy .NET `net45` Framework 4.6, NuGet instaluje zestaw w folderze, ponieważ jest to najwyższa dostępna wersja, która jest mniejsza lub równa 4.6.</span><span class="sxs-lookup"><span data-stu-id="d8dea-134">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="d8dea-135">Jeśli projekt jest przeznaczony dla platformy .NET Framework 4.6.1, z `net461` drugiej strony NuGet instaluje zestaw w folderze.</span><span class="sxs-lookup"><span data-stu-id="d8dea-135">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="d8dea-136">Jeśli projekt jest przeznaczony dla platformy .NET framework 4.0 i wcześniejszych, NuGet zgłasza odpowiedni komunikat o błędzie, aby nie znaleźć zgodnego zestawu.</span><span class="sxs-lookup"><span data-stu-id="d8dea-136">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="d8dea-137">Grupowanie zestawów według wersji framework</span><span class="sxs-lookup"><span data-stu-id="d8dea-137">Grouping assemblies by framework version</span></span>

<span data-ttu-id="d8dea-138">NuGet kopiuje zestawy tylko z jednego folderu biblioteki w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="d8dea-138">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="d8dea-139">Załóżmy na przykład, że pakiet ma następującą strukturę folderów:</span><span class="sxs-lookup"><span data-stu-id="d8dea-139">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="d8dea-140">Gdy pakiet jest zainstalowany w projekcie, który jest przeznaczony `MyAssembly.dll` dla platformy .NET Framework 4.5(v2.0) jest jedynym zainstalowanym zestawem.</span><span class="sxs-lookup"><span data-stu-id="d8dea-140">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="d8dea-141">`MyAssembly.Core.dll`(wersja 1.0) nie jest zainstalowany, ponieważ `net45` nie jest wymieniony w folderze.</span><span class="sxs-lookup"><span data-stu-id="d8dea-141">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="d8dea-142">NuGet zachowuje się `MyAssembly.Core.dll` w ten sposób, ponieważ może być `MyAssembly.dll`scalony w wersji 2.0 .</span><span class="sxs-lookup"><span data-stu-id="d8dea-142">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="d8dea-143">Jeśli chcesz `MyAssembly.Core.dll` zostać zainstalowany dla programu .NET Framework 4.5, umieść kopię w folderze. `net45`</span><span class="sxs-lookup"><span data-stu-id="d8dea-143">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="d8dea-144">Grupowanie zestawów według profilu struktury</span><span class="sxs-lookup"><span data-stu-id="d8dea-144">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="d8dea-145">NuGet obsługuje również kierowanie określonego profilu struktury przez dołączenie kreski i nazwę profilu na końcu folderu.</span><span class="sxs-lookup"><span data-stu-id="d8dea-145">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="d8dea-146">Obsługiwane profile są następujące:</span><span class="sxs-lookup"><span data-stu-id="d8dea-146">The supported profiles are as follows:</span></span>

- <span data-ttu-id="d8dea-147">`client`: Profil klienta</span><span class="sxs-lookup"><span data-stu-id="d8dea-147">`client`: Client Profile</span></span>
- <span data-ttu-id="d8dea-148">`full`: Pełny profil</span><span class="sxs-lookup"><span data-stu-id="d8dea-148">`full`: Full Profile</span></span>
- <span data-ttu-id="d8dea-149">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="d8dea-149">`wp`: Windows Phone</span></span>
- <span data-ttu-id="d8dea-150">`cf`: Kompaktowa struktura</span><span class="sxs-lookup"><span data-stu-id="d8dea-150">`cf`: Compact Framework</span></span>

## <a name="declaring-dependencies-advanced"></a><span data-ttu-id="d8dea-151">Deklarowanie zależności (zaawansowane)</span><span class="sxs-lookup"><span data-stu-id="d8dea-151">Declaring dependencies (Advanced)</span></span>

<span data-ttu-id="d8dea-152">Podczas pakowania pliku projektu NuGet próbuje automatycznie wygenerować zależności od projektu.</span><span class="sxs-lookup"><span data-stu-id="d8dea-152">When packing a project file, NuGet tries to automatically generate the dependencies from the project.</span></span> <span data-ttu-id="d8dea-153">Informacje w tej sekcji dotyczące używania pliku *nuspec* do deklarowania zależności jest zazwyczaj konieczne tylko w przypadku zaawansowanych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="d8dea-153">The information in this section about using a *.nuspec* file to declare dependencies is typically necessary for advanced scenarios only.</span></span>

<span data-ttu-id="d8dea-154">*(Wersja 2.0+)* Można zadeklarować zależności pakietu w *.nuspec* odpowiadające platformie `<group>` docelowej `<dependencies>` projektu docelowego przy użyciu elementów w elemencie.</span><span class="sxs-lookup"><span data-stu-id="d8dea-154">*(Version 2.0+)* You can declare package dependencies in the *.nuspec* corresponding to the target framework of the target project using `<group>` elements within the `<dependencies>` element.</span></span> <span data-ttu-id="d8dea-155">Aby uzyskać więcej informacji, zobacz [element zależności](../reference/nuspec.md#dependencies-element).</span><span class="sxs-lookup"><span data-stu-id="d8dea-155">For more information, see [dependencies element](../reference/nuspec.md#dependencies-element).</span></span>

<span data-ttu-id="d8dea-156">Każda grupa ma atrybut `targetFramework` o nazwie `<dependency>` i zawiera zero lub więcej elementów.</span><span class="sxs-lookup"><span data-stu-id="d8dea-156">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="d8dea-157">Te zależności są instalowane razem, gdy struktura docelowa jest zgodna z profilem framework projektu.</span><span class="sxs-lookup"><span data-stu-id="d8dea-157">Those dependencies are installed together when the target framework is compatible with the project's framework profile.</span></span> <span data-ttu-id="d8dea-158">Zobacz [struktury docelowe](../reference/target-frameworks.md) dla dokładnych identyfikatorów struktury.</span><span class="sxs-lookup"><span data-stu-id="d8dea-158">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

<span data-ttu-id="d8dea-159">Zalecamy użycie jednej grupy na moniker ram docelowych (TFM) dla plików w folderach *lib/* i *ref/.*</span><span class="sxs-lookup"><span data-stu-id="d8dea-159">We recommend using one group per Target Framework Moniker (TFM) for files in the *lib/* and *ref/* folders.</span></span>

<span data-ttu-id="d8dea-160">Poniższy przykład pokazuje różne `<group>` odmiany elementu:</span><span class="sxs-lookup"><span data-stu-id="d8dea-160">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="d8dea-161">Określanie, który obiekt docelowy NuGet ma być używany</span><span class="sxs-lookup"><span data-stu-id="d8dea-161">Determining which NuGet target to use</span></span>

<span data-ttu-id="d8dea-162">Podczas pakowania bibliotek docelowych biblioteki klas przenośnych może być trudne do określenia, który `.nuspec` obiekt docelowy NuGet należy użyć w nazwach folderów i pliku, zwłaszcza jeśli kierowanie tylko podzbiór PCL.</span><span class="sxs-lookup"><span data-stu-id="d8dea-162">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="d8dea-163">Pomogą Ci w tym następujące zasoby zewnętrzne:</span><span class="sxs-lookup"><span data-stu-id="d8dea-163">The following external resources will help you with this:</span></span>

- <span data-ttu-id="d8dea-164">[Profile frameworka w .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span><span class="sxs-lookup"><span data-stu-id="d8dea-164">[Framework profiles in .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span></span>
- <span data-ttu-id="d8dea-165">[Profile przenośnej biblioteki klas](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): tabela wyliczająca profile PCL i ich równoważne obiekty docelowe NuGet</span><span class="sxs-lookup"><span data-stu-id="d8dea-165">[Portable Class Library profiles](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="d8dea-166">[Narzędzie Profile Portable Class Library](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): narzędzie wiersza polecenia do określania profili PCL dostępnych w systemie</span><span class="sxs-lookup"><span data-stu-id="d8dea-166">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="d8dea-167">Pliki zawartości i skrypty programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8dea-167">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="d8dea-168">Pliki modyfikowalne zawartości i `packages.config` wykonywanie skryptów są dostępne tylko w formacie; są przestarzałe ze wszystkimi innymi formatami i nie powinny być używane dla żadnych nowych pakietów.</span><span class="sxs-lookup"><span data-stu-id="d8dea-168">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="d8dea-169">Z `packages.config`, pliki zawartości i skrypty programu PowerShell mogą być pogrupowane według struktury docelowej przy użyciu tej samej konwencji folderów `content` wewnątrz folderów i `tools` folderów.</span><span class="sxs-lookup"><span data-stu-id="d8dea-169">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="d8dea-170">Przykład:</span><span class="sxs-lookup"><span data-stu-id="d8dea-170">For example:</span></span>

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

<span data-ttu-id="d8dea-171">Jeśli folder framework pozostaje pusty, NuGet nie dodaje odwołań do zestawu lub plików zawartości ani nie uruchamia skryptów programu PowerShell dla tej struktury.</span><span class="sxs-lookup"><span data-stu-id="d8dea-171">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="d8dea-172">Ponieważ `init.ps1` jest wykonywany na poziomie rozwiązania i nie zależy od projektu, musi być umieszczony bezpośrednio pod folderem. `tools`</span><span class="sxs-lookup"><span data-stu-id="d8dea-172">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="d8dea-173">Jest ignorowana, jeśli jest umieszczana w folderze framework.</span><span class="sxs-lookup"><span data-stu-id="d8dea-173">It's ignored if placed under a framework folder.</span></span>
