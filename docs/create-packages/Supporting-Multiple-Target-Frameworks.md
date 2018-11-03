---
title: Wielowersyjność kodu dla pakietów NuGet
description: Opis różnych metod pod kątem wiele wersji .NET Framework z w obrębie jednego pakietu NuGet.
author: karann-msft
ms.author: karann
ms.date: 09/27/2017
ms.topic: conceptual
ms.openlocfilehash: c59839240935e2a6c590dea3adf623313f79f02f
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981148"
---
# <a name="supporting-multiple-net-framework-versions"></a><span data-ttu-id="aba1c-103">Obsługiwanie wielu wersji programu .NET framework</span><span class="sxs-lookup"><span data-stu-id="aba1c-103">Supporting multiple .NET framework versions</span></span>

<span data-ttu-id="aba1c-104">*Dla projektów .NET Core za pomocą narzędzia NuGet 4.0 +, zobacz [NuGet pakowanie i przywrócić jako elementów docelowych MSBuild](../reference/msbuild-targets.md) szczegółowe informacje na temat określania wartości docelowej dla wielu.*</span><span class="sxs-lookup"><span data-stu-id="aba1c-104">*For .NET Core projects using NuGet 4.0+, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md) for details on cross-targeting.*</span></span>

<span data-ttu-id="aba1c-105">Wiele bibliotek docelowej określonej wersji programu .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="aba1c-105">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="aba1c-106">Na przykład Niewykluczone, że jedna wersja biblioteki, które są specyficzne dla platformy uniwersalnej systemu Windows, a inna wersja, która korzysta z funkcji .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="aba1c-106">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span>

<span data-ttu-id="aba1c-107">Aby uwzględnić w efekcie NuGet obsługuje wprowadzanie wielu wersji tej samej biblioteki w jednym pakiecie, korzystając z oparty na Konwencji pracy katalogu metody opisanej w [Tworzenie pakietu](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="aba1c-107">To accommodate this, NuGet supports putting multiple versions of the same library in a single package when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="aba1c-108">Struktura folderów wersji Framework</span><span class="sxs-lookup"><span data-stu-id="aba1c-108">Framework version folder structure</span></span>

<span data-ttu-id="aba1c-109">Podczas tworzenia pakietu zawierającego tylko jedna wersja biblioteki lub docelowej wielu platform, zawsze tworzyć podfoldery `lib` przy użyciu różnych framework uwzględniana wielkość liter nazwy przy użyciu następującej konwencji:</span><span class="sxs-lookup"><span data-stu-id="aba1c-109">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="aba1c-110">Aby uzyskać pełną listę obsługiwanych nazw, zobacz [odwoływać się do platform docelowych](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="aba1c-110">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="aba1c-111">Nigdy nie powinny mieć wersję biblioteki, która nie jest przeznaczone do struktury i umieszczone bezpośrednio w katalogu głównym `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="aba1c-111">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="aba1c-112">(Ta funkcja była obsługiwana tylko w przypadku `packages.config`).</span><span class="sxs-lookup"><span data-stu-id="aba1c-112">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="aba1c-113">Ten sposób będzie dzięki bibliotece zgodny z dowolnej platformy docelowej i zezwolenie na można zainstalować w dowolnym miejscu, prawdopodobnie skutkuje nieoczekiwane błędy.</span><span class="sxs-lookup"><span data-stu-id="aba1c-113">Doing so would make the library compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="aba1c-114">Dodawanie zestawów w katalogu głównym (takie jak `lib\abc.dll`) lub jego podfolderach (takie jak `lib\abc\abc.dll`) jest przestarzały i jest ignorowana, gdy przy użyciu formatu PackagesReference.</span><span class="sxs-lookup"><span data-stu-id="aba1c-114">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="aba1c-115">Na przykład następującą strukturę folderów obsługuje cztery wersji zestawu, które są specyficzne dla framework:</span><span class="sxs-lookup"><span data-stu-id="aba1c-115">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="aba1c-116">Aby łatwo dołączyć te pliki, podczas tworzenia pakietu, należy użyć cyklicznej `**` symbolu wieloznacznego w `<files>` części Twojej `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="aba1c-116">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="aba1c-117">Foldery architektury</span><span class="sxs-lookup"><span data-stu-id="aba1c-117">Architecture-specific folders</span></span>

<span data-ttu-id="aba1c-118">W przypadku architektury zestawów, czyli oddzielne zestawy, których platformą docelową ARM, x 86 i x64, trzeba je umieścić w folderze o nazwie `runtimes` w podfolderach o nazwie `{platform}-{architecture}\lib\{framework}` lub `{platform}-{architecture}\native`.</span><span class="sxs-lookup"><span data-stu-id="aba1c-118">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="aba1c-119">Na przykład następującą strukturę folderów może pomieścić natywnych i zarządzanych bibliotek DLL, przeznaczonych dla systemu Windows 10 i `uap10.0` framework:</span><span class="sxs-lookup"><span data-stu-id="aba1c-119">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

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

<span data-ttu-id="aba1c-120">Te zestawy będą dostępne tylko w czasie wykonywania, więc jeśli chcesz zapewnić odpowiednie także następnie zestawu czasu kompilacji `AnyCPU` zestawu w `/ref{tfm}` folderu.</span><span class="sxs-lookup"><span data-stu-id="aba1c-120">These assemblies will only be available at runtime, so if you want to provide the corresponding compile time assembly as well then have `AnyCPU` assembly in `/ref{tfm}` folder.</span></span> 

<span data-ttu-id="aba1c-121">Należy pamiętać, NuGet zawsze wybiera te zasoby kompilacji lub środowisko uruchomieniowe z jednego folderu tak w przypadku niektórych zasoby zgodne z `/ref` następnie `/lib` zostanie zignorowana, aby dodać zestawy kompilacji.</span><span class="sxs-lookup"><span data-stu-id="aba1c-121">Please note, NuGet always picks these compile or runtime assets from one folder so if there are some compatible assets from `/ref` then `/lib` will be ignored to add compile-time assemblies.</span></span> <span data-ttu-id="aba1c-122">Podobnie jeśli istnieją pewne zasoby zgodna z `/runtime` , a następnie również `/lib` zostanie zignorowane dla środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="aba1c-122">Similarly, if there are some compatbile assets from `/runtime` then also `/lib` will be ignored for runtime.</span></span>

<span data-ttu-id="aba1c-123">Zobacz [tworzenie pakietów platformy UWP](../guides/create-uwp-packages.md) przykład odwołuje się do tych plików w `.nuspec` manifestu.</span><span class="sxs-lookup"><span data-stu-id="aba1c-123">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

<span data-ttu-id="aba1c-124">Zobacz też [pakowania składnika aplikacji Sklepu Windows za pomocą NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span><span class="sxs-lookup"><span data-stu-id="aba1c-124">Also, see [Packing a Windows store app component with NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="aba1c-125">Zgodne wersje zestawów i platformy docelowej w projekcie</span><span class="sxs-lookup"><span data-stu-id="aba1c-125">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="aba1c-126">Podczas instalowania pakietu, który ma wiele wersji zestawu NuGet próbuje dopasować nazwę framework zestawu za pomocą platformy docelowej projektu.</span><span class="sxs-lookup"><span data-stu-id="aba1c-126">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="aba1c-127">Jeśli nie zostanie znalezione dopasowanie, NuGet kopiuje zestawu dla najwyższa wersja, która jest mniejsza lub równa platformy docelowej projektu, jeśli jest dostępny.</span><span class="sxs-lookup"><span data-stu-id="aba1c-127">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="aba1c-128">Jeśli zestawy zgodna, nie zostanie znaleziony, NuGet zwraca odpowiedni komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="aba1c-128">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="aba1c-129">Na przykład rozważmy następującą strukturę folderów w pakiecie:</span><span class="sxs-lookup"><span data-stu-id="aba1c-129">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="aba1c-130">Podczas instalowania tego pakietu w projekcie, który jest przeznaczony dla .NET Framework 4.6, NuGet instaluje zestaw w `net45` folderu, ponieważ jest to najnowsza wersja dostępna o rozmiarze mniejszym niż 4.6.</span><span class="sxs-lookup"><span data-stu-id="aba1c-130">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="aba1c-131">Jeśli projekt jest przeznaczony dla platformy .NET Framework 4.6.1, z drugiej strony, NuGet instaluje zestaw w `net461` folderu.</span><span class="sxs-lookup"><span data-stu-id="aba1c-131">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="aba1c-132">Jeśli projekt jest przeznaczony dla .NET framework 4.0 i starszych, NuGet zgłasza odpowiedni komunikat o błędzie dla nie wyszukuje zgodny zestawu.</span><span class="sxs-lookup"><span data-stu-id="aba1c-132">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="aba1c-133">Zestawy są grupowane według framework w wersji</span><span class="sxs-lookup"><span data-stu-id="aba1c-133">Grouping assemblies by framework version</span></span>

<span data-ttu-id="aba1c-134">NuGet kopiuje zestawy z tylko jedna biblioteka folder w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="aba1c-134">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="aba1c-135">Na przykład załóżmy, że pakiet ma następującą strukturę folderów:</span><span class="sxs-lookup"><span data-stu-id="aba1c-135">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="aba1c-136">Gdy pakiet jest zainstalowany w projekcie, który jest przeznaczony dla .NET Framework 4.5, `MyAssembly.dll` (w wersji 2.0) to zestaw tylko zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="aba1c-136">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="aba1c-137">`MyAssembly.Core.dll` (w wersji 1.0) nie jest zainstalowany, ponieważ nie znajduje się w `net45` folderu.</span><span class="sxs-lookup"><span data-stu-id="aba1c-137">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="aba1c-138">NuGet zachowuje się w ten sposób, ponieważ `MyAssembly.Core.dll` może mieć scalonego w wersji 2.0 programu `MyAssembly.dll`.</span><span class="sxs-lookup"><span data-stu-id="aba1c-138">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="aba1c-139">Jeśli chcesz `MyAssembly.Core.dll` konieczności instalowania programu .NET Framework 4.5, Umieść kopię w `net45` folderu.</span><span class="sxs-lookup"><span data-stu-id="aba1c-139">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="aba1c-140">Zestawy grupowania w ramach profilu</span><span class="sxs-lookup"><span data-stu-id="aba1c-140">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="aba1c-141">NuGet obsługuje także przeznaczonych dla profilu określonego framework, dodając kreską i nazwę profilu w celu folderu.</span><span class="sxs-lookup"><span data-stu-id="aba1c-141">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="aba1c-142">Profile obsługiwane są następujące:</span><span class="sxs-lookup"><span data-stu-id="aba1c-142">The supported profiles are as follows:</span></span>

- <span data-ttu-id="aba1c-143">`client`: Profil klienta</span><span class="sxs-lookup"><span data-stu-id="aba1c-143">`client`: Client Profile</span></span>
- <span data-ttu-id="aba1c-144">`full`: Pełny profil</span><span class="sxs-lookup"><span data-stu-id="aba1c-144">`full`: Full Profile</span></span>
- <span data-ttu-id="aba1c-145">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="aba1c-145">`wp`: Windows Phone</span></span>
- <span data-ttu-id="aba1c-146">`cf`: Compact Framework</span><span class="sxs-lookup"><span data-stu-id="aba1c-146">`cf`: Compact Framework</span></span>

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="aba1c-147">Określenie, która docelowa NuGet do użycia</span><span class="sxs-lookup"><span data-stu-id="aba1c-147">Determining which NuGet target to use</span></span>

<span data-ttu-id="aba1c-148">Gdy bibliotek tworzenia pakietów przeznaczonych dla biblioteki klas przenośnych może być trudne do określenia docelowej NuGet, które należy używać w nazwach folderów i `.nuspec` pliku, zwłaszcza, jeśli jest to obsługiwane tylko podzbiór PCL.</span><span class="sxs-lookup"><span data-stu-id="aba1c-148">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="aba1c-149">Następujące zasoby zewnętrzne pomoże Ci w tym:</span><span class="sxs-lookup"><span data-stu-id="aba1c-149">The following external resources will help you with this:</span></span>

- <span data-ttu-id="aba1c-150">[Profile Framework na platformie .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span><span class="sxs-lookup"><span data-stu-id="aba1c-150">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span></span>
- <span data-ttu-id="aba1c-151">[Przenośne biblioteki klas profile](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Tabela wyliczania ich równoważne cele NuGet i profile PCL</span><span class="sxs-lookup"><span data-stu-id="aba1c-151">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="aba1c-152">[Przenośne biblioteki klas profilów narzędzia](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): narzędzie wiersza polecenia umożliwiające określanie PCL profile dostępna w systemie</span><span class="sxs-lookup"><span data-stu-id="aba1c-152">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="aba1c-153">Pliki zawartości i skryptów programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="aba1c-153">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="aba1c-154">Modyfikowalne pliki zawartości i wykonywanie skryptu są dostępne z `packages.config` formatowania tylko; zostały zaniechane w innych formatach i nie powinna być używana dla żadnych nowych pakietów.</span><span class="sxs-lookup"><span data-stu-id="aba1c-154">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="aba1c-155">Za pomocą `packages.config`zawartości, pliki i skrypty programu PowerShell można grupować według platformy docelowej przy użyciu tych samych konwencji folder wewnątrz `content` i `tools` folderów.</span><span class="sxs-lookup"><span data-stu-id="aba1c-155">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="aba1c-156">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="aba1c-156">For example:</span></span>

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

<span data-ttu-id="aba1c-157">Jeśli folder struktury jest puste, NuGet nie jest dodawanie odwołań do zestawów lub plików zawartości i uruchamiaj skrypty programu PowerShell dla tej struktury.</span><span class="sxs-lookup"><span data-stu-id="aba1c-157">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="aba1c-158">Ponieważ `init.ps1` jest wykonywany w rozwiązaniu poziomu i nie jest zależny od projektu musi zostać umieszczony bezpośrednio pod `tools` folderu.</span><span class="sxs-lookup"><span data-stu-id="aba1c-158">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="aba1c-159">Jest on ignorowany, jeśli umieszczony w folderze framework.</span><span class="sxs-lookup"><span data-stu-id="aba1c-159">It's ignored if placed under a framework folder.</span></span>
