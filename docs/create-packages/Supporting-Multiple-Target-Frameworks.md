---
title: Wielowersyjność kodu dla pakietów NuGet
description: Opis różnych metod pod kątem wiele wersji .NET Framework z w obrębie jednego pakietu NuGet.
author: karann-msft
ms.author: karann
ms.date: 09/27/2017
ms.topic: conceptual
ms.openlocfilehash: 0b22d48b9151b903a5307beafa5ccef14e5fecf3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551709"
---
# <a name="supporting-multiple-net-framework-versions"></a><span data-ttu-id="a6ed8-103">Obsługiwanie wielu wersji programu .NET framework</span><span class="sxs-lookup"><span data-stu-id="a6ed8-103">Supporting multiple .NET framework versions</span></span>

<span data-ttu-id="a6ed8-104">*Dla projektów .NET Core za pomocą narzędzia NuGet 4.0 +, zobacz [NuGet pakowanie i przywrócić jako elementów docelowych MSBuild](../reference/msbuild-targets.md) szczegółowe informacje na temat określania wartości docelowej dla wielu.*</span><span class="sxs-lookup"><span data-stu-id="a6ed8-104">*For .NET Core projects using NuGet 4.0+, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md) for details on cross-targeting.*</span></span>

<span data-ttu-id="a6ed8-105">Wiele bibliotek docelowej określonej wersji programu .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-105">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="a6ed8-106">Na przykład Niewykluczone, że jedna wersja biblioteki, które są specyficzne dla platformy uniwersalnej systemu Windows, a inna wersja, która korzysta z funkcji .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-106">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span>

<span data-ttu-id="a6ed8-107">Aby uwzględnić w efekcie NuGet obsługuje wprowadzanie wielu wersji tej samej biblioteki w jednym pakiecie, korzystając z oparty na Konwencji pracy katalogu metody opisanej w [Tworzenie pakietu](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="a6ed8-107">To accommodate this, NuGet supports putting multiple versions of the same library in a single package when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="a6ed8-108">Struktura folderów wersji Framework</span><span class="sxs-lookup"><span data-stu-id="a6ed8-108">Framework version folder structure</span></span>

<span data-ttu-id="a6ed8-109">Podczas tworzenia pakietu zawierającego tylko jedna wersja biblioteki lub docelowej wielu platform, zawsze tworzyć podfoldery `lib` przy użyciu różnych framework uwzględniana wielkość liter nazwy przy użyciu następującej konwencji:</span><span class="sxs-lookup"><span data-stu-id="a6ed8-109">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="a6ed8-110">Aby uzyskać pełną listę obsługiwanych nazw, zobacz [odwoływać się do platform docelowych](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="a6ed8-110">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="a6ed8-111">Nigdy nie powinny mieć wersję biblioteki, która nie jest przeznaczone do struktury i umieszczone bezpośrednio w katalogu głównym `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-111">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="a6ed8-112">(Ta funkcja była obsługiwana tylko w przypadku `packages.config`).</span><span class="sxs-lookup"><span data-stu-id="a6ed8-112">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="a6ed8-113">Ten sposób będzie dzięki bibliotece zgodny z dowolnej platformy docelowej i zezwolenie na można zainstalować w dowolnym miejscu, prawdopodobnie skutkuje nieoczekiwane błędy.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-113">Doing so would make the library compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="a6ed8-114">Dodawanie zestawów w katalogu głównym (takie jak `lib\abc.dll`) lub jego podfolderach (takie jak `lib\abc\abc.dll`) jest przestarzały i jest ignorowana, gdy przy użyciu formatu PackagesReference.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-114">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="a6ed8-115">Na przykład następującą strukturę folderów obsługuje cztery wersji zestawu, które są specyficzne dla framework:</span><span class="sxs-lookup"><span data-stu-id="a6ed8-115">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="a6ed8-116">Aby łatwo dołączyć te pliki, podczas tworzenia pakietu, należy użyć cyklicznej `**` symbolu wieloznacznego w `<files>` części Twojej `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="a6ed8-116">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="a6ed8-117">Foldery architektury</span><span class="sxs-lookup"><span data-stu-id="a6ed8-117">Architecture-specific folders</span></span>

<span data-ttu-id="a6ed8-118">W przypadku architektury zestawów, czyli oddzielne zestawy, których platformą docelową ARM, x 86 i x64, trzeba je umieścić w folderze o nazwie `runtimes` w podfolderach o nazwie `{platform}-{architecture}\lib\{framework}` lub `{platform}-{architecture}\native`.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-118">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="a6ed8-119">Na przykład następującą strukturę folderów może pomieścić natywnych i zarządzanych bibliotek DLL, przeznaczonych dla systemu Windows 10 i `uap10.0` framework:</span><span class="sxs-lookup"><span data-stu-id="a6ed8-119">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

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

<span data-ttu-id="a6ed8-120">Zobacz [tworzenie pakietów platformy UWP](../guides/create-uwp-packages.md) przykład odwołuje się do tych plików w `.nuspec` manifestu.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-120">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="a6ed8-121">Zgodne wersje zestawów i platformy docelowej w projekcie</span><span class="sxs-lookup"><span data-stu-id="a6ed8-121">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="a6ed8-122">Podczas instalowania pakietu, który ma wiele wersji zestawu NuGet próbuje dopasować nazwę framework zestawu za pomocą platformy docelowej projektu.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-122">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="a6ed8-123">Jeśli nie zostanie znalezione dopasowanie, NuGet kopiuje zestawu dla najwyższa wersja, która jest mniejsza lub równa platformy docelowej projektu, jeśli jest dostępny.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-123">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="a6ed8-124">Jeśli zestawy zgodna, nie zostanie znaleziony, NuGet zwraca odpowiedni komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-124">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="a6ed8-125">Na przykład rozważmy następującą strukturę folderów w pakiecie:</span><span class="sxs-lookup"><span data-stu-id="a6ed8-125">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="a6ed8-126">Podczas instalowania tego pakietu w projekcie, który jest przeznaczony dla .NET Framework 4.6, NuGet instaluje zestaw w `net45` folderu, ponieważ jest to najnowsza wersja dostępna o rozmiarze mniejszym niż 4.6.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-126">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="a6ed8-127">Jeśli projekt jest przeznaczony dla platformy .NET Framework 4.6.1, z drugiej strony, NuGet instaluje zestaw w `net461` folderu.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-127">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="a6ed8-128">Jeśli projekt jest przeznaczony dla .NET framework 4.0 i starszych, NuGet zgłasza odpowiedni komunikat o błędzie dla nie wyszukuje zgodny zestawu.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-128">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="a6ed8-129">Zestawy są grupowane według framework w wersji</span><span class="sxs-lookup"><span data-stu-id="a6ed8-129">Grouping assemblies by framework version</span></span>

<span data-ttu-id="a6ed8-130">NuGet kopiuje zestawy z tylko jedna biblioteka folder w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-130">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="a6ed8-131">Na przykład załóżmy, że pakiet ma następującą strukturę folderów:</span><span class="sxs-lookup"><span data-stu-id="a6ed8-131">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="a6ed8-132">Gdy pakiet jest zainstalowany w projekcie, który jest przeznaczony dla .NET Framework 4.5, `MyAssembly.dll` (w wersji 2.0) to zestaw tylko zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-132">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="a6ed8-133">`MyAssembly.Core.dll` (w wersji 1.0) nie jest zainstalowany, ponieważ nie znajduje się w `net45` folderu.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-133">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="a6ed8-134">NuGet zachowuje się w ten sposób, ponieważ `MyAssembly.Core.dll` może mieć scalonego w wersji 2.0 programu `MyAssembly.dll`.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-134">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="a6ed8-135">Jeśli chcesz `MyAssembly.Core.dll` konieczności instalowania programu .NET Framework 4.5, Umieść kopię w `net45` folderu.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-135">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="a6ed8-136">Zestawy grupowania w ramach profilu</span><span class="sxs-lookup"><span data-stu-id="a6ed8-136">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="a6ed8-137">NuGet obsługuje także przeznaczonych dla profilu określonego framework, dodając kreską i nazwę profilu w celu folderu.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-137">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="a6ed8-138">Profile obsługiwane są następujące:</span><span class="sxs-lookup"><span data-stu-id="a6ed8-138">The supported profiles are as follows:</span></span>

- <span data-ttu-id="a6ed8-139">`client`: Profil klienta</span><span class="sxs-lookup"><span data-stu-id="a6ed8-139">`client`: Client Profile</span></span>
- <span data-ttu-id="a6ed8-140">`full`: Pełny profil</span><span class="sxs-lookup"><span data-stu-id="a6ed8-140">`full`: Full Profile</span></span>
- <span data-ttu-id="a6ed8-141">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="a6ed8-141">`wp`: Windows Phone</span></span>
- <span data-ttu-id="a6ed8-142">`cf`: Compact Framework</span><span class="sxs-lookup"><span data-stu-id="a6ed8-142">`cf`: Compact Framework</span></span>

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="a6ed8-143">Określenie, która docelowa NuGet do użycia</span><span class="sxs-lookup"><span data-stu-id="a6ed8-143">Determining which NuGet target to use</span></span>

<span data-ttu-id="a6ed8-144">Gdy bibliotek tworzenia pakietów przeznaczonych dla biblioteki klas przenośnych może być trudne do określenia docelowej NuGet, które należy używać w nazwach folderów i `.nuspec` pliku, zwłaszcza, jeśli jest to obsługiwane tylko podzbiór PCL.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-144">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="a6ed8-145">Następujące zasoby zewnętrzne pomoże Ci w tym:</span><span class="sxs-lookup"><span data-stu-id="a6ed8-145">The following external resources will help you with this:</span></span>

- <span data-ttu-id="a6ed8-146">[Profile Framework na platformie .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span><span class="sxs-lookup"><span data-stu-id="a6ed8-146">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span></span>
- <span data-ttu-id="a6ed8-147">[Przenośne biblioteki klas profile](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Tabela wyliczania ich równoważne cele NuGet i profile PCL</span><span class="sxs-lookup"><span data-stu-id="a6ed8-147">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="a6ed8-148">[Przenośne biblioteki klas profilów narzędzia](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): narzędzie wiersza polecenia umożliwiające określanie PCL profile dostępna w systemie</span><span class="sxs-lookup"><span data-stu-id="a6ed8-148">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="a6ed8-149">Pliki zawartości i skryptów programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6ed8-149">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="a6ed8-150">Modyfikowalne pliki zawartości i wykonywanie skryptu są dostępne z `packages.config` formatowania tylko; zostały zaniechane w innych formatach i nie powinna być używana dla żadnych nowych pakietów.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-150">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="a6ed8-151">Za pomocą `packages.config`zawartości, pliki i skrypty programu PowerShell można grupować według platformy docelowej przy użyciu tych samych konwencji folder wewnątrz `content` i `tools` folderów.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-151">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="a6ed8-152">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="a6ed8-152">For example:</span></span>

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

<span data-ttu-id="a6ed8-153">Jeśli folder struktury jest puste, NuGet nie jest dodawanie odwołań do zestawów lub plików zawartości i uruchamiaj skrypty programu PowerShell dla tej struktury.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-153">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="a6ed8-154">Ponieważ `init.ps1` jest wykonywany w rozwiązaniu poziomu i nie jest zależny od projektu musi zostać umieszczony bezpośrednio pod `tools` folderu.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-154">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="a6ed8-155">Jest on ignorowany, jeśli umieszczony w folderze framework.</span><span class="sxs-lookup"><span data-stu-id="a6ed8-155">It's ignored if placed under a framework folder.</span></span>
