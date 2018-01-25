---
title: Projekty platformy UWP pliku project.json NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Opis sposobu pliku project.json jest używane do śledzenia zależności NuGet w projektach systemu Windows platformy Uniwersalnej."
keywords: "Zależności NuGet, NuGet i platformy uniwersalnej systemu Windows, platformy uniwersalnej systemu Windows i project.json, plik project.json NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0063c959a6d638d7ba1d579d35ff660dccae282c
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="projectjson-and-uwp"></a><span data-ttu-id="029da-104">pliku Project.JSON i platformy uniwersalnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="029da-104">project.json and UWP</span></span>

> [!Important]
> <span data-ttu-id="029da-105">Ta zawartość jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="029da-105">This content is deprecated.</span></span> <span data-ttu-id="029da-106">Projekty powinny używać albo `packages.config` lub PackageReference formatów.</span><span class="sxs-lookup"><span data-stu-id="029da-106">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="029da-107">W tym dokumencie opisano strukturę pakietu, która wykorzystuje funkcje programu NuGet 3 + (Visual Studio 2015 i nowsze).</span><span class="sxs-lookup"><span data-stu-id="029da-107">This document describes the package structure that employs features in NuGet 3+ (Visual Studio 2015 and later).</span></span> <span data-ttu-id="029da-108">`minClientVersion` Właściwości użytkownika `.nuspec` może służyć do stanu, aby wymagać funkcje opisane w tym miejscu, ustawiając go na 3.1.</span><span class="sxs-lookup"><span data-stu-id="029da-108">The `minClientVersion` property of your `.nuspec` can be used to state that you require the features described here by setting it to 3.1.</span></span>

## <a name="adding-uwp-support-to-an-existing-package"></a><span data-ttu-id="029da-109">Dodawanie obsługi platformy uniwersalnej systemu Windows do istniejącego pakietu</span><span class="sxs-lookup"><span data-stu-id="029da-109">Adding UWP support to an existing package</span></span>

<span data-ttu-id="029da-110">Jeśli masz istniejący pakiet i chcesz dodać obsługę aplikacji platformy uniwersalnej systemu Windows, nie muszą przyjęcie format pakowania opisane w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="029da-110">If you have an existing package and you want to add support for UWP applications, then you don’t need to adopt the  packaging format described here.</span></span> <span data-ttu-id="029da-111">Należy przyjąć tego formatu, jeśli wymagane funkcje, w tym artykule opisano i chcesz pracować tylko z klientami, które zostały zaktualizowane w wersji 3 + klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="029da-111">You only need to adopt this format if you require the features it describes and are willing to  work only with clients that have updated to version 3+ of the NuGet client.</span></span>

## <a name="i-already-target-netcore45"></a><span data-ttu-id="029da-112">Mogę wskazać już netcore45</span><span class="sxs-lookup"><span data-stu-id="029da-112">I already target netcore45</span></span>

<span data-ttu-id="029da-113">W przypadku skierowania `netcore45` już i nie trzeba korzystać z funkcji w tym miejscu, nie jest potrzebne nie działanie.</span><span class="sxs-lookup"><span data-stu-id="029da-113">If you target `netcore45` already, and you don’t need to take advantage of the features here, no action is needed.</span></span> <span data-ttu-id="029da-114">`netcore45`pakiety mogą być używane przez aplikacje platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="029da-114">`netcore45` packages can be consumed by UWP applications.</span></span>

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a><span data-ttu-id="029da-115">Chcę korzystać z określonych interfejsów API systemu Windows 10</span><span class="sxs-lookup"><span data-stu-id="029da-115">I want to take advantage of Windows 10 specific APIs</span></span>

<span data-ttu-id="029da-116">W takim przypadku należy dodać `uap10.0` target framework moniker (TFM lub TxM) do pakietu.</span><span class="sxs-lookup"><span data-stu-id="029da-116">In this case you need to add the `uap10.0` target framework moniker (TFM or TxM) to your package.</span></span> <span data-ttu-id="029da-117">Utwórz nowy folder do pakietu, a następnie dodaj zestawu, który został skompilowany do pracy z systemem Windows 10 do tego folderu.</span><span class="sxs-lookup"><span data-stu-id="029da-117">Create a new folder in your package and add the assembly that has been compiled to work with Windows 10 to that folder.</span></span>

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a><span data-ttu-id="029da-118">Nie potrzebuję poszczególnych interfejsów API systemu Windows 10, ale ma nowe funkcje platformy .NET lub nie został jeszcze netcore45</span><span class="sxs-lookup"><span data-stu-id="029da-118">I don’t need Windows 10 specific APIs, but want new .NET features or don’t have netcore45 already</span></span>

<span data-ttu-id="029da-119">W takim przypadku należy dodać `dotnet` TxM do pakietu.</span><span class="sxs-lookup"><span data-stu-id="029da-119">In this case you would add the `dotnet` TxM to your package.</span></span> <span data-ttu-id="029da-120">W odróżnieniu od innych TxMs `dotnet` nie wiąże się z powierzchni ani platformy.</span><span class="sxs-lookup"><span data-stu-id="029da-120">Unlike other TxMs, `dotnet` doesn't imply a surface area or platform.</span></span> <span data-ttu-id="029da-121">Jest informujący pakietu działa na dowolnej platformie, która pracuje zależności.</span><span class="sxs-lookup"><span data-stu-id="029da-121">It is stating that your package works on any platform that your dependencies work on.</span></span> <span data-ttu-id="029da-122">Podczas tworzenia pakietu z `dotnet` TxM, najprawdopodobniej będzie zależnościami dużo więcej TxM określonych Twojej `.nuspec`, musisz zdefiniować pakiety BCL możesz zależne, takie `System.Text`, `System.Xml`itp. Lokalizacje, które działają tych zależności w zdefiniuj, gdzie działa pakietu.</span><span class="sxs-lookup"><span data-stu-id="029da-122">When building a package with the `dotnet` TxM, you are likely to have many more TxM-specific dependencies in your `.nuspec`, as you need to define the BCL packages you depend on, such `System.Text`, `System.Xml`, etc. The locations that those dependencies work on define where your package works.</span></span>

### <a name="how-do-i-find-out-my-dependencies"></a><span data-ttu-id="029da-123">Jak sprawdzić Moje zależności</span><span class="sxs-lookup"><span data-stu-id="029da-123">How do I find out my dependencies</span></span>

<span data-ttu-id="029da-124">Istnieją dwa sposoby, aby dowiedzieć się, które zależności, aby wyświetlić listę:</span><span class="sxs-lookup"><span data-stu-id="029da-124">There are two ways to figure out which dependencies to list:</span></span>

1. <span data-ttu-id="029da-125">Użyj [Generator zależności NuSpec](https://github.com/onovotny/ReferenceGenerator) **3 strona** narzędzia.</span><span class="sxs-lookup"><span data-stu-id="029da-125">Use the [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) **3rd party** tool.</span></span> <span data-ttu-id="029da-126">Narzędzie automatyzuje proces i aktualizacji programu `.nuspec` pliku z pakietów zależnych podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="029da-126">The tool automates the process and updates your `.nuspec` file with the dependant packages on build.</span></span> <span data-ttu-id="029da-127">Jest dostępna za pośrednictwem pakietu NuGet, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span><span class="sxs-lookup"><span data-stu-id="029da-127">It is available via a NuGet package, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span></span>

1. <span data-ttu-id="029da-128">(Sposób twarde) Użyj `ILDasm` spojrzeć na Twojej `.dll` aby zobaczyć, jakie zestawy są faktycznie wymagane w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="029da-128">(The hard way) Use `ILDasm` to look at your `.dll` to see what assemblies are actually needed at runtime.</span></span> <span data-ttu-id="029da-129">Następnie określ pakietu NuGet, które mają pochodzić z.</span><span class="sxs-lookup"><span data-stu-id="029da-129">Then determine which NuGet package they each come from.</span></span>

<span data-ttu-id="029da-130">Zobacz [ `project.json` ](project-json.md) tematu, aby uzyskać szczegółowe informacje na funkcje, które ułatwiają tworzenie pakietu, który obsługuje `dotnet` TxM.</span><span class="sxs-lookup"><span data-stu-id="029da-130">See the [`project.json`](project-json.md) topic for details on features that help in the creation of a package that supports the `dotnet` TxM.</span></span>

> [!Important]
> <span data-ttu-id="029da-131">Jeśli pakiet jest przeznaczony do pracy z projektami PCL, zalecamy tworzenie `dotnet` folderu, aby uniknąć ostrzeżenia i potencjalnych problemów ze zgodnością.</span><span class="sxs-lookup"><span data-stu-id="029da-131">If your package is intended to work with PCL projects, we highly recommend to create a `dotnet` folder, to avoid warnings and potential compatibility issues.</span></span>

## <a name="directory-structure"></a><span data-ttu-id="029da-132">Struktura katalogów</span><span class="sxs-lookup"><span data-stu-id="029da-132">Directory structure</span></span>

<span data-ttu-id="029da-133">Pakiety NuGet, w tym formacie mają następujące dobrze znany folder i zachowania:</span><span class="sxs-lookup"><span data-stu-id="029da-133">NuGet packages using this format have the following well-known folder and behaviors:</span></span>

| <span data-ttu-id="029da-134">Folder</span><span class="sxs-lookup"><span data-stu-id="029da-134">Folder</span></span> | <span data-ttu-id="029da-135">Zachowania</span><span class="sxs-lookup"><span data-stu-id="029da-135">Behaviors</span></span> |
| --- | --- |
| <span data-ttu-id="029da-136">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="029da-136">Build</span></span> | <span data-ttu-id="029da-137">Zawiera MSBuild cele i pliki właściwości w tym folderze są zintegrowane z inną nazwę projektu, ale w przeciwnym razie nie została zmieniona.</span><span class="sxs-lookup"><span data-stu-id="029da-137">Contains MSBuild targets and props files in this folder are integrated differently into the project, but otherwise there is no change.</span></span> |
| <span data-ttu-id="029da-138">Narzędzia</span><span class="sxs-lookup"><span data-stu-id="029da-138">Tools</span></span> | <span data-ttu-id="029da-139">`install.ps1`i `uninstall.ps1` nie są uruchamiane.</span><span class="sxs-lookup"><span data-stu-id="029da-139">`install.ps1` and `uninstall.ps1` are not run.</span></span> <span data-ttu-id="029da-140">`init.ps1`działa jako zawsze ma.</span><span class="sxs-lookup"><span data-stu-id="029da-140">`init.ps1` works as it always has.</span></span> |
| <span data-ttu-id="029da-141">Zawartość</span><span class="sxs-lookup"><span data-stu-id="029da-141">Content</span></span> | <span data-ttu-id="029da-142">Zawartość nie jest kopiowana automatycznie do użytkownika projektu.</span><span class="sxs-lookup"><span data-stu-id="029da-142">Content is not copied automatically into a user's project.</span></span> <span data-ttu-id="029da-143">Obsługa zawartości uwzględnienie w projekcie jest planowane w nowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="029da-143">Support for content inclusion in the project is planned for a later release.</span></span> |
| <span data-ttu-id="029da-144">Lib</span><span class="sxs-lookup"><span data-stu-id="029da-144">Lib</span></span> | <span data-ttu-id="029da-145">Wiele pakietów `lib` działa tak samo w NuGet 2.x, ale bez opcji rozwinięte jakie nazwy może być używany w go i lepsze logiki dla pobrania poprawne podfolderu w przypadku uzyskiwania dostępu do pakietów.</span><span class="sxs-lookup"><span data-stu-id="029da-145">For many packages the `lib` works the same way it does in NuGet 2.x, but with expanded options for what names can be used inside it and better logic for picking the correct sub-folder when consuming packages.</span></span> <span data-ttu-id="029da-146">Jednak w przypadku używania w połączeniu z `ref`, `lib` folder zawiera zestawy, które implementuje powierzchni zdefiniowane przez zestawy w `ref` folderu.</span><span class="sxs-lookup"><span data-stu-id="029da-146">However, when used in conjunction with `ref`, the `lib` folder contains assemblies that implement the surface area defined by the assemblies in the `ref` folder.</span></span> |
| <span data-ttu-id="029da-147">REF</span><span class="sxs-lookup"><span data-stu-id="029da-147">Ref</span></span> | <span data-ttu-id="029da-148">`ref`jest opcjonalny folder zawierający zestawy .NET Definiowanie publicznego powierzchni (typy publiczne i metody) do kompilacji dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="029da-148">`ref` is an optional folder that contains .NET assemblies defining the public surface (public types and methods) for an application to compile against.</span></span> <span data-ttu-id="029da-149">Zestawy w tym folderze może mieć żadnej implementacji, czysto są one używane do definiowania powierzchni dla kompilatora.</span><span class="sxs-lookup"><span data-stu-id="029da-149">The assemblies in this folder may have no implementation, they are purely used to define surface area for the compiler.</span></span> <span data-ttu-id="029da-150">Jeśli nie ma pakietu `ref` folder, a następnie `lib` jest odwołanie do zestawu i zestawu implementacji.</span><span class="sxs-lookup"><span data-stu-id="029da-150">If the package has no `ref` folder, then the `lib` is both the reference assembly and the implementation assembly.</span></span> |
| <span data-ttu-id="029da-151">środowisk uruchomieniowych</span><span class="sxs-lookup"><span data-stu-id="029da-151">Runtimes</span></span> | <span data-ttu-id="029da-152">`runtimes`jest opcjonalny folder zawierający kod określonego systemu operacyjnego, takie jak architektura Procesora i systemu operacyjnego określonego lub w inny sposób zależny od platformy plików binarnych.</span><span class="sxs-lookup"><span data-stu-id="029da-152">`runtimes` is an optional folder that contains OS specific code, such as CPU architecture and OS specific or otherwise platform-dependent binaries.</span></span> |

## <a name="msbuild-targets-and-props-files-in-packages"></a><span data-ttu-id="029da-153">MSBuild cele i pliki właściwości w pakiety</span><span class="sxs-lookup"><span data-stu-id="029da-153">MSBuild targets and props files in packages</span></span>

<span data-ttu-id="029da-154">Pakiety NuGet mogą zawierać `.targets` i `.props` pliki, które są importowane do żadnego projektu MSBuild zainstalowanego pakietu do.</span><span class="sxs-lookup"><span data-stu-id="029da-154">NuGet packages can contain `.targets` and `.props` files which are imported into any MSBuild project that the package is installed into.</span></span> <span data-ttu-id="029da-155">W NuGet 2.x, to był przez wstrzykiwanie `<Import>` instrukcje do `.csproj` pliku, w NuGet 3.0 istnieje akcja określonych "Instalacja do projektu".</span><span class="sxs-lookup"><span data-stu-id="029da-155">In NuGet 2.x, this was done by injecting `<Import>` statements into the `.csproj` file, in NuGet 3.0 there is no specific "installation to project" action.</span></span> <span data-ttu-id="029da-156">Zamiast tego proces przywracania pakietu zapisuje dwa pliki `[projectname].nuget.props` i `[projectname].NuGet.targets`.</span><span class="sxs-lookup"><span data-stu-id="029da-156">Instead the package restore process writes two files `[projectname].nuget.props` and `[projectname].NuGet.targets`.</span></span>

<span data-ttu-id="029da-157">MSBuild zna do wyszukania tych plików i automatycznie importowane na początku i pod koniec procesu tworzenia projektu.</span><span class="sxs-lookup"><span data-stu-id="029da-157">MSBuild knows to look for these two files and automatically imports them near the beginning and near the end of the project build process.</span></span> <span data-ttu-id="029da-158">Zapewnia to bardzo podobnie do NuGet 2.x, ale z jedną główną różnicą: *istnieje w tym przypadku nie gwarantuje kolejność plików celów/arkuszy właściwości*.</span><span class="sxs-lookup"><span data-stu-id="029da-158">This provides very similar behavior to NuGet 2.x, but with one major difference: *there is no guaranteed order of targets/props files in this case*.</span></span> <span data-ttu-id="029da-159">Jednak MSBuild udostępniają sposoby kolejności docelowych za pośrednictwem `BeforeTargets` i `AfterTargets` atrybuty `<Target>` definicji (zobacz [Target — Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span><span class="sxs-lookup"><span data-stu-id="029da-159">However, MSBuild does provide ways to order targets through the `BeforeTargets` and `AfterTargets` attributes of the `<Target>` definition (see [Target Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span></span>

## <a name="lib-and-ref"></a><span data-ttu-id="029da-160">Lib i Ref</span><span class="sxs-lookup"><span data-stu-id="029da-160">Lib and Ref</span></span>

<span data-ttu-id="029da-161">Zachowanie `lib` folderu nie zmieniła się znacznie w NuGet w wersji 3.</span><span class="sxs-lookup"><span data-stu-id="029da-161">The behavior of the `lib` folder hasn't changed significantly in NuGet v3.</span></span> <span data-ttu-id="029da-162">Jednak wszystkie zestawy muszą się znajdować w podfoldery o nazwie po TxM i nie można umieścić bezpośrednio pod `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="029da-162">However, all assemblies must be within sub-folders named after a TxM, and can no longer be placed directly under the `lib` folder.</span></span> <span data-ttu-id="029da-163">TxM jest nazwą platformy, który ma działać w przypadku danej zawartości w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="029da-163">A TxM is the name of a platform that a given asset in a package is supposed to work for.</span></span> <span data-ttu-id="029da-164">Logicznie rozszerzenia elementu docelowego Framework monikerów (TFM) są to np. `net45`, `net46`, `netcore50`, i `dnxcore50` należą do nich TxMs (zobacz [docelowych platform](../Schema/Target-Frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="029da-164">Logically these are an extension of the Target Framework Monikers (TFM) e.g. `net45`, `net46`, `netcore50`, and `dnxcore50` are all examples of TxMs (see [Target Frameworks](../Schema/Target-Frameworks.md).</span></span> <span data-ttu-id="029da-165">TxM mogą odwoływać się do struktury (TFM) oraz innych obszarach powierzchni specyficzne dla platformy.</span><span class="sxs-lookup"><span data-stu-id="029da-165">TxM can refer to a framework (TFM) as well as other platform-specific surface areas.</span></span> <span data-ttu-id="029da-166">Na przykład TxM platformy uniwersalnej systemu Windows (`uap10.0`) reprezentuje powierzchni .NET, a także powierzchni systemu Windows dla aplikacji platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="029da-166">For example the UWP TxM (`uap10.0`) represents the .NET surface area as well as the Windows surface area for UWP applications.</span></span>

<span data-ttu-id="029da-167">Przykład struktury lib:</span><span class="sxs-lookup"><span data-stu-id="029da-167">An example lib structure:</span></span>

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

<span data-ttu-id="029da-168">`lib` Folder zawiera zestawy, które są używane w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="029da-168">The `lib` folder contains assemblies that are used at runtime.</span></span> <span data-ttu-id="029da-169">Większość pakietów folderu `lib` dla każdego elementu docelowego TxMs to wszystko, co jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="029da-169">For most packages a folder under `lib` for each of the target TxMs is all that is required.</span></span>

## <a name="ref"></a><span data-ttu-id="029da-170">REF</span><span class="sxs-lookup"><span data-stu-id="029da-170">Ref</span></span>

<span data-ttu-id="029da-171">Czasami istnieją przypadki, w których należy używać innym zestawie podczas kompilacji (.NET zestawów odwołań do tego dzisiaj).</span><span class="sxs-lookup"><span data-stu-id="029da-171">There are sometimes cases where a different assembly should be used during compilation (.NET Reference Assemblies do this today).</span></span> <span data-ttu-id="029da-172">Dla tych przypadków użycia folder najwyższego poziomu o nazwie `ref` (skrót od "zestawów odwołań").</span><span class="sxs-lookup"><span data-stu-id="029da-172">For those cases, use a top-level folder called `ref` (short for "Reference Assemblies").</span></span>

<span data-ttu-id="029da-173">Większość autorów pakietu nie wymagają `ref` folderu.</span><span class="sxs-lookup"><span data-stu-id="029da-173">Most package authors don't require the `ref` folder.</span></span> <span data-ttu-id="029da-174">Jest to przydatne w przypadku pakietów, które należy zapewnić spójne powierzchni IntelliSense i kompilacji, ale następnie inną implementację dla różnych TxMs.</span><span class="sxs-lookup"><span data-stu-id="029da-174">It is useful for packages that need to provide a consistent surface area for compilation and IntelliSense but then have different implementation for different TxMs.</span></span> <span data-ttu-id="029da-175">Przypadek użycia największych są `System.*` pakietów oferowanych w ramach wysyłanie .NET Core na NuGet.</span><span class="sxs-lookup"><span data-stu-id="029da-175">The biggest use case of this are the `System.*` packages that are being produced as part of shipping .NET Core on NuGet.</span></span> <span data-ttu-id="029da-176">Te pakiety mają różne implementacje, które są trwa unified spójny zestaw zestawy ref.</span><span class="sxs-lookup"><span data-stu-id="029da-176">These packages have various implementations that are being unified by a consistent set of ref assemblies.</span></span>

<span data-ttu-id="029da-177">Mechanicznie zestawy zawarte w `ref` znajdują się zestawy referencyjne przekazywany do kompilatora.</span><span class="sxs-lookup"><span data-stu-id="029da-177">Mechanically, the assemblies included in the `ref` folder are the reference assemblies being passed to the compiler.</span></span> <span data-ttu-id="029da-178">Dla tych osób, które zostały użyte csc.exe są zestawy, możemy przekazywane do [opcji/Reference C#](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) przełącznika.</span><span class="sxs-lookup"><span data-stu-id="029da-178">For those of you who have used csc.exe these are the assemblies we are passing to the [C# /reference option](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) switch.</span></span>

<span data-ttu-id="029da-179">Struktura `ref` folderu jest taka sama jak `lib`, na przykład:</span><span class="sxs-lookup"><span data-stu-id="029da-179">The structure of the `ref` folder is the same as `lib`, for example:</span></span>

    └───MyImageProcessingLib
         ├───lib
         │   ├───net40
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   ├───net451
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   └───win81
         │           MyImageProcessingLibrary.dll
         │
         └───ref
             ├───net40
             │       MyImageProcessingLibrary.dll
             │
             └───portable-net451-win81
                     MyImageProcessingLibrary.dll

<span data-ttu-id="029da-180">W tym przykładzie zestawów w `ref` katalogów wszystkie będą identyczne.</span><span class="sxs-lookup"><span data-stu-id="029da-180">In this example the assemblies in the `ref` directories would all be identical.</span></span>

## <a name="runtimes"></a><span data-ttu-id="029da-181">środowisk uruchomieniowych</span><span class="sxs-lookup"><span data-stu-id="029da-181">Runtimes</span></span>

<span data-ttu-id="029da-182">Folder środowisk uruchomieniowych zawiera zestawy i natywnych bibliotek wymaganych do uruchomienia na określonym "środowisk uruchomieniowych", które są zazwyczaj definiowane przez architekturę systemu operacyjnego i procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="029da-182">The runtimes folder contains assemblies and native libraries required to run on specific "runtimes", which are generally defined by Operating System and CPU architecture.</span></span> <span data-ttu-id="029da-183">Te programy obsługi są identyfikowane za pomocą [identyfikatorów środowiska uruchomieniowego (RID)](/dotnet/core/rid-catalog) takich jak `win`, `win-x86`, `win7-x86`, `win8-64`itp.</span><span class="sxs-lookup"><span data-stu-id="029da-183">These runtimes are identified using [Runtime Identifiers (RIDs)](/dotnet/core/rid-catalog) such as `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span></span>

## <a name="native-light-up"></a><span data-ttu-id="029da-184">Natywny światła w górę</span><span class="sxs-lookup"><span data-stu-id="029da-184">Native light-up</span></span>

<span data-ttu-id="029da-185">W poniższym przykładzie przedstawiono czysto zarządzaną implementację dla różnych platform, które używa pomocników macierzystego w systemie Windows 8, gdzie może wywołać do natywnych interfejsów API systemu Windows 8 określonego pakietu.</span><span class="sxs-lookup"><span data-stu-id="029da-185">The following example shows a package that has a purely managed implementation for several platforms, but uses native helpers on Windows 8 where it can call into Windows 8-specific native APIs.</span></span>

    └───MyLibrary
         ├───lib
         │   └───net40
         │           MyLibrary.dll
         │
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net40
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyNativeLibrary.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net40
                 │           MyLibrary.dll
                 │
                 └───native
                         MyNativeLibrary.dll

<span data-ttu-id="029da-186">Podany pakiet powyżej stanie następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="029da-186">Given the above package the following things happen:</span></span>

- <span data-ttu-id="029da-187">Kiedy nie w systemie Windows 8 `lib/net40/MyLibrary.dll` zestaw jest używany.</span><span class="sxs-lookup"><span data-stu-id="029da-187">When not on Windows 8 the `lib/net40/MyLibrary.dll` assembly is used.</span></span>

- <span data-ttu-id="029da-188">Gdy w systemie Windows 8 `runtimes/win8-<architecture>/lib/MyLibrary.dll` jest używany i `native/MyNativeHelper.dll` jest kopiowany do danych wyjściowych kompilacji.</span><span class="sxs-lookup"><span data-stu-id="029da-188">When on Windows 8 the `runtimes/win8-<architecture>/lib/MyLibrary.dll` is used and the `native/MyNativeHelper.dll` is copied to the output of your build.</span></span>

<span data-ttu-id="029da-189">W powyższym przykładzie `lib/net40` zestaw jest wyłącznie kod zarządzany, podczas gdy zestawów w folderze środowisk uruchomieniowych będzie p/invoke do zestawu macierzystego pomocnika do wywoływania interfejsów API specyficzne dla systemu Windows 8.</span><span class="sxs-lookup"><span data-stu-id="029da-189">In the example above the `lib/net40` assembly is purely managed code, whilst the assemblies in the runtimes folder will p/invoke into the native helper assembly to call APIs specific to Windows 8.</span></span>

<span data-ttu-id="029da-190">Tylko jeden `lib` folder jest kiedykolwiek zostać pobrane, więc jeśli istnieje folder określonego środowiska uruchomieniowego jest wybierany przez konkretnego z systemem innym niż środowisko uruchomieniowe `lib`.</span><span class="sxs-lookup"><span data-stu-id="029da-190">Only a single `lib` folder is ever be picked, so if there is a runtime specific folder it's chosen over non-runtime specific `lib`.</span></span> <span data-ttu-id="029da-191">Folder macierzysty jest dodatku, jeśli taka istnieje jest kopiowany do danych wyjściowych kompilacji.</span><span class="sxs-lookup"><span data-stu-id="029da-191">The native folder is additive, if it exists it's copied to the output of the build.</span></span>

## <a name="managed-wrapper"></a><span data-ttu-id="029da-192">Zarządzany otok</span><span class="sxs-lookup"><span data-stu-id="029da-192">Managed wrapper</span></span>

<span data-ttu-id="029da-193">Innym sposobem użycia środowisk uruchomieniowych jest na potrzeby wysłania pakietu, który jest wyłącznie zarządzany otok za pośrednictwem natywnych zestawów.</span><span class="sxs-lookup"><span data-stu-id="029da-193">Another way to use runtimes is to ship a package that is purely a managed wrapper over a native assembly.</span></span> <span data-ttu-id="029da-194">W tym scenariuszu należy utworzyć pakiet podobne do poniższych:</span><span class="sxs-lookup"><span data-stu-id="029da-194">In this scenario you create a package like the following:</span></span>

    └───MyLibrary
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net451
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyImplementation.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net451
                 │           MyLibrary.dll
                 │
                 └───native
                         MyImplementation.dll

<span data-ttu-id="029da-195">W takim przypadku istnieje nie najwyższego poziomu `lib` folderze, w tym folderze, ponieważ wystąpiły jest żadnej implementacji tego pakietu, które nie korzystają z odpowiedniego zestawu macierzystego.</span><span class="sxs-lookup"><span data-stu-id="029da-195">In this case there is no top-level `lib` folder as that folder as there is no implementation of this package that doesn't rely on the corresponding native assembly.</span></span> <span data-ttu-id="029da-196">Jeśli zestaw zarządzany `MyLibrary.dll`, została dokładnie taka sama w obu przypadkach firma Microsoft może umieść ją w najwyższego poziomu `lib` folderu, ale ponieważ brak natywny zestaw nie powoduje pakietu niepowodzenie instalacji, jeśli została zainstalowana na platformie który następnie lib najwyższego poziomu, które mają być używane, ale nie natywny zestaw jest kopiowany były x86 Windows lub Windows x64.</span><span class="sxs-lookup"><span data-stu-id="029da-196">If the managed assembly, `MyLibrary.dll`, was exactly the same in both of these cases then we could put it in a top level `lib` folder, but because the lack of a native assembly doesn't cause the package to fail installing if it was installed on a platform that wasn't win-x86 or win-x64 then the top level lib would be used but no native assembly would be copied.</span></span>

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a><span data-ttu-id="029da-197">Tworzenie pakietów NuGet 2 i NuGet 3</span><span class="sxs-lookup"><span data-stu-id="029da-197">Authoring packages for NuGet 2 and NuGet 3</span></span>

<span data-ttu-id="029da-198">Jeśli chcesz utworzyć pakiet, który może być zużyte przez projektów przy użyciu `packages.config` również jako pakietów przy użyciu `project.json` następnie następujących warunków:</span><span class="sxs-lookup"><span data-stu-id="029da-198">If you want to create a package that can be consumed by projects using `packages.config` as well as packages using `project.json` then the following apply:</span></span>

- <span data-ttu-id="029da-199">REF i środowisk uruchomieniowych tylko pracy nad NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="029da-199">Ref and runtimes only work on NuGet 3.</span></span> <span data-ttu-id="029da-200">Są one zarówno ignorowane przez NuGet 2.</span><span class="sxs-lookup"><span data-stu-id="029da-200">They are both ignored by NuGet 2.</span></span>

- <span data-ttu-id="029da-201">Nie należy polegać na `install.ps1` lub `uninstall.ps1` funkcji.</span><span class="sxs-lookup"><span data-stu-id="029da-201">You cannot rely on `install.ps1` or `uninstall.ps1` to function.</span></span> <span data-ttu-id="029da-202">Wykonanie tych plików przy użyciu `packages.config`, ale są ignorowane z `project.json`.</span><span class="sxs-lookup"><span data-stu-id="029da-202">These files execute when using `packages.config`, but are ignored with `project.json`.</span></span> <span data-ttu-id="029da-203">Dlatego pakietu musi być możliwe bez ich uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="029da-203">So your package needs to be usable without them running.</span></span> <span data-ttu-id="029da-204">`init.ps1`nadal działa na NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="029da-204">`init.ps1` still runs on NuGet 3.</span></span>

- <span data-ttu-id="029da-205">Cele i właściwości instalacji jest inny, dlatego należy upewnić się, że pakiet działa zgodnie z oczekiwaniami na obu komputerach klienckich.</span><span class="sxs-lookup"><span data-stu-id="029da-205">Targets and Props installation is different, so make sure that your package works as expected on both clients.</span></span>

- <span data-ttu-id="029da-206">Podkatalogi lib musi być TxM w NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="029da-206">Subdirectories of lib must be a TxM in NuGet 3.</span></span> <span data-ttu-id="029da-207">Nie można umieścić bibliotek w katalogu głównym `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="029da-207">You cannot place libraries at the root of the `lib` folder.</span></span>

- <span data-ttu-id="029da-208">Zawartość nie jest kopiowana automatycznie z NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="029da-208">Content is not copied automatically with NuGet 3.</span></span> <span data-ttu-id="029da-209">Konsumentów pakietu można skopiować same pliki lub zautomatyzować kopiowania plików za pomocą narzędzia, takiego jak modułu uruchamiającego zadania.</span><span class="sxs-lookup"><span data-stu-id="029da-209">Consumers of your package could copy the files themselves or use a tool like a task runner to automate copying the files.</span></span>

- <span data-ttu-id="029da-210">Transformacje pliku źródłowego i konfiguracji nie są uruchamiane przez NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="029da-210">Source and config file transforms are not run by NuGet 3.</span></span>

<span data-ttu-id="029da-211">Jeśli są obsługiwane NuGet 2 i 3, a następnie z `minClientVersion` powinny być najniższy wersji klienta NuGet 2, który pracuje pakietu.</span><span class="sxs-lookup"><span data-stu-id="029da-211">If you are supporting NuGet 2 and 3 then your `minClientVersion` should be the lowest version of NuGet 2 client that your package works on.</span></span> <span data-ttu-id="029da-212">W przypadku istniejącego pakietu nie powinna wymagać zmiany.</span><span class="sxs-lookup"><span data-stu-id="029da-212">In the case of an existing package it shouldn't need to change.</span></span>