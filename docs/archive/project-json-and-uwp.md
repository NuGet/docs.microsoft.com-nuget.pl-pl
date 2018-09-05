---
title: Plik project.json NuGet w projektach platformy uniwersalnej systemu Windows
description: Opis sposobu używania pliku project.json do śledzenia zależności NuGet w projektach platformy uniwersalnej Windows (UWP).
author: karann-msft
ms.author: karann
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: ac3c137dd0ba50571737093eef11c8ab0ef932b2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548667"
---
# <a name="projectjson-and-uwp"></a><span data-ttu-id="cca2a-103">Plik Project.JSON i platformy uniwersalnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="cca2a-103">project.json and UWP</span></span>

> [!Important]
> <span data-ttu-id="cca2a-104">Ta zawartość jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="cca2a-104">This content is deprecated.</span></span> <span data-ttu-id="cca2a-105">Projekty powinny używać albo `packages.config` lub PackageReference podzielony na fragmenty.</span><span class="sxs-lookup"><span data-stu-id="cca2a-105">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="cca2a-106">W tym dokumencie opisano strukturę pakietu, która używa funkcji NuGet 3 + (Visual Studio 2015 i nowszych).</span><span class="sxs-lookup"><span data-stu-id="cca2a-106">This document describes the package structure that employs features in NuGet 3+ (Visual Studio 2015 and later).</span></span> <span data-ttu-id="cca2a-107">`minClientVersion` Właściwości usługi `.nuspec` może służyć do stanu wymagane funkcje opisane w tym miejscu, ustawiając go na 3.1.</span><span class="sxs-lookup"><span data-stu-id="cca2a-107">The `minClientVersion` property of your `.nuspec` can be used to state that you require the features described here by setting it to 3.1.</span></span>

## <a name="adding-uwp-support-to-an-existing-package"></a><span data-ttu-id="cca2a-108">Dodawanie obsługi platformy uniwersalnej systemu Windows do istniejącego pakietu</span><span class="sxs-lookup"><span data-stu-id="cca2a-108">Adding UWP support to an existing package</span></span>

<span data-ttu-id="cca2a-109">Jeśli masz istniejący pakiet, i chcesz dodać obsługę aplikacji platformy uniwersalnej systemu Windows, nie należy do przyjęcia format pakowania, opisane w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="cca2a-109">If you have an existing package and you want to add support for UWP applications, then you don’t need to adopt the  packaging format described here.</span></span> <span data-ttu-id="cca2a-110">Należy przyjąć tego formatu, jeśli potrzebujesz funkcji, w tym artykule opisano i jest gotowa do pracy tylko w przypadku klientów, które zostały zaktualizowane do wersji 3 + klienta programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="cca2a-110">You only need to adopt this format if you require the features it describes and are willing to  work only with clients that have updated to version 3+ of the NuGet client.</span></span>

## <a name="i-already-target-netcore45"></a><span data-ttu-id="cca2a-111">Czy mogę wskazać już netcore45</span><span class="sxs-lookup"><span data-stu-id="cca2a-111">I already target netcore45</span></span>

<span data-ttu-id="cca2a-112">Jeśli platformą docelową jest `netcore45` i nie trzeba korzystać z funkcji w tym miejscu, jest wymagana żadna akcja.</span><span class="sxs-lookup"><span data-stu-id="cca2a-112">If you target `netcore45` already, and you don’t need to take advantage of the features here, no action is needed.</span></span> <span data-ttu-id="cca2a-113">`netcore45` pakiety mogą być używane przez aplikacje platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="cca2a-113">`netcore45` packages can be consumed by UWP applications.</span></span>

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a><span data-ttu-id="cca2a-114">Chcę móc korzystać z określonych interfejsów API systemu Windows 10</span><span class="sxs-lookup"><span data-stu-id="cca2a-114">I want to take advantage of Windows 10 specific APIs</span></span>

<span data-ttu-id="cca2a-115">W takim przypadku należy dodać `uap10.0` docelowe moniker struktury (TFM lub TxM) do pakietu.</span><span class="sxs-lookup"><span data-stu-id="cca2a-115">In this case you need to add the `uap10.0` target framework moniker (TFM or TxM) to your package.</span></span> <span data-ttu-id="cca2a-116">Utwórz nowy folder w pakiecie i dodać zestaw, który został wcześniej skompilowany do pracy z systemem Windows 10 do tego folderu.</span><span class="sxs-lookup"><span data-stu-id="cca2a-116">Create a new folder in your package and add the assembly that has been compiled to work with Windows 10 to that folder.</span></span>

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a><span data-ttu-id="cca2a-117">Nie potrzebuję określonych interfejsów API systemu Windows 10, ale ma nowe funkcje platformy .NET lub nie został jeszcze netcore45</span><span class="sxs-lookup"><span data-stu-id="cca2a-117">I don’t need Windows 10 specific APIs, but want new .NET features or don’t have netcore45 already</span></span>

<span data-ttu-id="cca2a-118">W takim przypadku należy dodać `dotnet` TxM do pakietu.</span><span class="sxs-lookup"><span data-stu-id="cca2a-118">In this case you would add the `dotnet` TxM to your package.</span></span> <span data-ttu-id="cca2a-119">W przeciwieństwie do innych TxMs `dotnet` nie sugeruje się udzielenia, powierzchni lub platformy.</span><span class="sxs-lookup"><span data-stu-id="cca2a-119">Unlike other TxMs, `dotnet` doesn't imply a surface area or platform.</span></span> <span data-ttu-id="cca2a-120">Jest o pakietu działa na dowolnej platformie, które zależności działają w treści.</span><span class="sxs-lookup"><span data-stu-id="cca2a-120">It is stating that your package works on any platform that your dependencies work on.</span></span> <span data-ttu-id="cca2a-121">Podczas tworzenia pakietu o `dotnet` TxM, najprawdopodobniej będzie mieć wiele więcej zależności TxM określonych w swojej `.nuspec`, jak należy zdefiniować pakietów BCL, na przykład `System.Text`, `System.Xml`itp. Lokalizacje, które te zależności pracować nad definiują, gdzie działa pakiet.</span><span class="sxs-lookup"><span data-stu-id="cca2a-121">When building a package with the `dotnet` TxM, you are likely to have many more TxM-specific dependencies in your `.nuspec`, as you need to define the BCL packages you depend on, such `System.Text`, `System.Xml`, etc. The locations that those dependencies work on define where your package works.</span></span>

### <a name="how-do-i-find-out-my-dependencies"></a><span data-ttu-id="cca2a-122">Jak sprawdzić zależności</span><span class="sxs-lookup"><span data-stu-id="cca2a-122">How do I find out my dependencies</span></span>

<span data-ttu-id="cca2a-123">Istnieją dwa sposoby, aby ustalić którym zależności, aby wyświetlić listę:</span><span class="sxs-lookup"><span data-stu-id="cca2a-123">There are two ways to figure out which dependencies to list:</span></span>

1. <span data-ttu-id="cca2a-124">Użyj [Generator zależności NuSpec](https://github.com/onovotny/ReferenceGenerator) **firm 3** narzędzia.</span><span class="sxs-lookup"><span data-stu-id="cca2a-124">Use the [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) **3rd party** tool.</span></span> <span data-ttu-id="cca2a-125">Narzędzie automatyzuje proces i aktualizacji usługi `.nuspec` plików za pomocą pakietów zależnych podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="cca2a-125">The tool automates the process and updates your `.nuspec` file with the dependant packages on build.</span></span> <span data-ttu-id="cca2a-126">Jest on dostępny za pośrednictwem pakietu NuGet, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span><span class="sxs-lookup"><span data-stu-id="cca2a-126">It is available via a NuGet package, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span></span>

1. <span data-ttu-id="cca2a-127">(Sposób) Użyj `ILDasm` Przyjrzyj się Twoje `.dll` aby zobaczyć, jakie zestawy są rzeczywiście potrzebne w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="cca2a-127">(The hard way) Use `ILDasm` to look at your `.dll` to see what assemblies are actually needed at runtime.</span></span> <span data-ttu-id="cca2a-128">Następnie określ pakiet NuGet, które każdy pochodzą z.</span><span class="sxs-lookup"><span data-stu-id="cca2a-128">Then determine which NuGet package they each come from.</span></span>

<span data-ttu-id="cca2a-129">Zobacz [ `project.json` ](project-json.md) tematu, aby uzyskać szczegółowe informacje na temat funkcji, które pomagają w utworzeniu pakietu, który obsługuje `dotnet` TxM.</span><span class="sxs-lookup"><span data-stu-id="cca2a-129">See the [`project.json`](project-json.md) topic for details on features that help in the creation of a package that supports the `dotnet` TxM.</span></span>

> [!Important]
> <span data-ttu-id="cca2a-130">Jeśli pakiet jest przeznaczony do pracy z projektów PCL, zalecamy tworzenie `dotnet` folderu, w celu uniknięcia ostrzeżeń i potencjalnych problemów ze zgodnością.</span><span class="sxs-lookup"><span data-stu-id="cca2a-130">If your package is intended to work with PCL projects, we highly recommend to create a `dotnet` folder, to avoid warnings and potential compatibility issues.</span></span>

## <a name="directory-structure"></a><span data-ttu-id="cca2a-131">Struktura katalogów</span><span class="sxs-lookup"><span data-stu-id="cca2a-131">Directory structure</span></span>

<span data-ttu-id="cca2a-132">Pakiety NuGet, używając następującego formatu mają następujące dobrze znany folder i zachowania:</span><span class="sxs-lookup"><span data-stu-id="cca2a-132">NuGet packages using this format have the following well-known folder and behaviors:</span></span>

| <span data-ttu-id="cca2a-133">Folder</span><span class="sxs-lookup"><span data-stu-id="cca2a-133">Folder</span></span> | <span data-ttu-id="cca2a-134">Zachowania</span><span class="sxs-lookup"><span data-stu-id="cca2a-134">Behaviors</span></span> |
| --- | --- |
| <span data-ttu-id="cca2a-135">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="cca2a-135">Build</span></span> | <span data-ttu-id="cca2a-136">Zawiera program MSBuild cele i pliki właściwości w tym folderze są zintegrowane inaczej w projekcie, ale w przeciwnym razie nie nastąpiła żadna zmiana.</span><span class="sxs-lookup"><span data-stu-id="cca2a-136">Contains MSBuild targets and props files in this folder are integrated differently into the project, but otherwise there is no change.</span></span> |
| <span data-ttu-id="cca2a-137">Narzędzia</span><span class="sxs-lookup"><span data-stu-id="cca2a-137">Tools</span></span> | <span data-ttu-id="cca2a-138">`install.ps1` i `uninstall.ps1` nie są uruchamiane.</span><span class="sxs-lookup"><span data-stu-id="cca2a-138">`install.ps1` and `uninstall.ps1` are not run.</span></span> <span data-ttu-id="cca2a-139">`init.ps1` działa jak zawsze ma.</span><span class="sxs-lookup"><span data-stu-id="cca2a-139">`init.ps1` works as it always has.</span></span> |
| <span data-ttu-id="cca2a-140">Zawartość</span><span class="sxs-lookup"><span data-stu-id="cca2a-140">Content</span></span> | <span data-ttu-id="cca2a-141">Zawartość nie jest kopiowana automatycznie do projektu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cca2a-141">Content is not copied automatically into a user's project.</span></span> <span data-ttu-id="cca2a-142">Obsługa zawartości uwzględnianie w projekcie jest planowana w nowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="cca2a-142">Support for content inclusion in the project is planned for a later release.</span></span> |
| <span data-ttu-id="cca2a-143">lib</span><span class="sxs-lookup"><span data-stu-id="cca2a-143">Lib</span></span> | <span data-ttu-id="cca2a-144">W przypadku wielu pakietów `lib` działa tak samo w NuGet 2.x, ale z rozszerzone opcje nazwy, jakie może być używany wewnątrz go i lepiej logiki dla pobrania poprawne podfolder, podczas korzystania z pakietów.</span><span class="sxs-lookup"><span data-stu-id="cca2a-144">For many packages the `lib` works the same way it does in NuGet 2.x, but with expanded options for what names can be used inside it and better logic for picking the correct sub-folder when consuming packages.</span></span> <span data-ttu-id="cca2a-145">Jednakże gdy jest używana w połączeniu z `ref`, `lib` folder zawiera zestawy, które implementują podatny na atak obszar zdefiniowany przez zestawy w `ref` folderu.</span><span class="sxs-lookup"><span data-stu-id="cca2a-145">However, when used in conjunction with `ref`, the `lib` folder contains assemblies that implement the surface area defined by the assemblies in the `ref` folder.</span></span> |
| <span data-ttu-id="cca2a-146">REF</span><span class="sxs-lookup"><span data-stu-id="cca2a-146">Ref</span></span> | <span data-ttu-id="cca2a-147">`ref` jest opcjonalny folder zawierający zestawy .NET, definiując publicznie powierzchni (typy i metody publiczne) do kompilowanie z użyciem aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cca2a-147">`ref` is an optional folder that contains .NET assemblies defining the public surface (public types and methods) for an application to compile against.</span></span> <span data-ttu-id="cca2a-148">Zestawy znajdujące się w tym folderze może nie mają implementacji, czysto służą one do definiowania powierzchni dla kompilatora.</span><span class="sxs-lookup"><span data-stu-id="cca2a-148">The assemblies in this folder may have no implementation, they are purely used to define surface area for the compiler.</span></span> <span data-ttu-id="cca2a-149">Jeśli nie ma pakietu `ref` folder, a następnie `lib` jest zestaw odwołania i zestawu implementacji.</span><span class="sxs-lookup"><span data-stu-id="cca2a-149">If the package has no `ref` folder, then the `lib` is both the reference assembly and the implementation assembly.</span></span> |
| <span data-ttu-id="cca2a-150">środowiska uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="cca2a-150">Runtimes</span></span> | <span data-ttu-id="cca2a-151">`runtimes` jest opcjonalny folder zawierający kod określonego systemu operacyjnego, takich jak architektura procesora CPU i określonych lub w inny sposób zależny od platformy plików binarnych systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="cca2a-151">`runtimes` is an optional folder that contains OS specific code, such as CPU architecture and OS specific or otherwise platform-dependent binaries.</span></span> |

## <a name="msbuild-targets-and-props-files-in-packages"></a><span data-ttu-id="cca2a-152">Program MSBuild cele i pliki właściwości w pakietach</span><span class="sxs-lookup"><span data-stu-id="cca2a-152">MSBuild targets and props files in packages</span></span>

<span data-ttu-id="cca2a-153">Pakiety NuGet może zawierać `.targets` i `.props` pliki, które są importowane do każdego projektu MSBuild, który pakiet jest zainstalowany w.</span><span class="sxs-lookup"><span data-stu-id="cca2a-153">NuGet packages can contain `.targets` and `.props` files which are imported into any MSBuild project that the package is installed into.</span></span> <span data-ttu-id="cca2a-154">W pakiecie NuGet 2.x, stało się przez wstrzykiwanie `<Import>` instrukcje do `.csproj` plików, NuGet 3.0 nie ma określonych "Instalacja z projektem" akcji.</span><span class="sxs-lookup"><span data-stu-id="cca2a-154">In NuGet 2.x, this was done by injecting `<Import>` statements into the `.csproj` file, in NuGet 3.0 there is no specific "installation to project" action.</span></span> <span data-ttu-id="cca2a-155">Zamiast tego proces przywracania pakietów zapisuje dwa pliki `[projectname].nuget.props` i `[projectname].NuGet.targets`.</span><span class="sxs-lookup"><span data-stu-id="cca2a-155">Instead the package restore process writes two files `[projectname].nuget.props` and `[projectname].NuGet.targets`.</span></span>

<span data-ttu-id="cca2a-156">Program MSBuild wie, aby wyszukać te dwa pliki i automatycznie importuje, na początku i pod koniec procesu kompilacji projektu.</span><span class="sxs-lookup"><span data-stu-id="cca2a-156">MSBuild knows to look for these two files and automatically imports them near the beginning and near the end of the project build process.</span></span> <span data-ttu-id="cca2a-157">Zapewnia to zachowanie bardzo podobne do narzędzia NuGet 2.x, ale z jedną główną różnicą: *nie jest zagwarantowana kolejność plików celów/arkuszy właściwości w tym przypadku*.</span><span class="sxs-lookup"><span data-stu-id="cca2a-157">This provides very similar behavior to NuGet 2.x, but with one major difference: *there is no guaranteed order of targets/props files in this case*.</span></span> <span data-ttu-id="cca2a-158">Jednak program MSBuild umożliwiają kolejność elementów docelowych, za pośrednictwem `BeforeTargets` i `AfterTargets` atrybuty `<Target>` definicji (zobacz [Target — Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span><span class="sxs-lookup"><span data-stu-id="cca2a-158">However, MSBuild does provide ways to order targets through the `BeforeTargets` and `AfterTargets` attributes of the `<Target>` definition (see [Target Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span></span>

## <a name="lib-and-ref"></a><span data-ttu-id="cca2a-159">Biblioteki i Ref</span><span class="sxs-lookup"><span data-stu-id="cca2a-159">Lib and Ref</span></span>

<span data-ttu-id="cca2a-160">Zachowanie `lib` folderu nie zmieniły się znacznie w wersji NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="cca2a-160">The behavior of the `lib` folder hasn't changed significantly in NuGet v3.</span></span> <span data-ttu-id="cca2a-161">Jednak wszystkie zestawy muszą znajdować się w podfolderach o nazwie po TxM i nie będzie można umieścić bezpośrednio pod `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="cca2a-161">However, all assemblies must be within sub-folders named after a TxM, and can no longer be placed directly under the `lib` folder.</span></span> <span data-ttu-id="cca2a-162">TxM nazywa się to platforma, która powinna działać w przypadku danego elementu zawartości w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="cca2a-162">A TxM is the name of a platform that a given asset in a package is supposed to work for.</span></span> <span data-ttu-id="cca2a-163">Logicznie te stanowią rozszerzenie z monikerów Framework docelowych (TFM) np. `net45`, `net46`, `netcore50`, i `dnxcore50` należą do nich TxMs (zobacz [platform docelowych](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="cca2a-163">Logically these are an extension of the Target Framework Monikers (TFM) e.g. `net45`, `net46`, `netcore50`, and `dnxcore50` are all examples of TxMs (see [Target Frameworks](../reference/target-frameworks.md).</span></span> <span data-ttu-id="cca2a-164">TxM mogą odwoływać się do struktury (TFM) oraz innych obszarów specyficzne dla platformy.</span><span class="sxs-lookup"><span data-stu-id="cca2a-164">TxM can refer to a framework (TFM) as well as other platform-specific surface areas.</span></span> <span data-ttu-id="cca2a-165">Na przykład TxM platformy uniwersalnej systemu Windows (`uap10.0`) reprezentuje obszar powierzchni .NET, a także Windows podatny na atak obszar dla aplikacji platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="cca2a-165">For example the UWP TxM (`uap10.0`) represents the .NET surface area as well as the Windows surface area for UWP applications.</span></span>

<span data-ttu-id="cca2a-166">Przykład struktury lib:</span><span class="sxs-lookup"><span data-stu-id="cca2a-166">An example lib structure:</span></span>

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

<span data-ttu-id="cca2a-167">`lib` Folder zawiera zestawy, które są używane w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="cca2a-167">The `lib` folder contains assemblies that are used at runtime.</span></span> <span data-ttu-id="cca2a-168">Większość pakietów folder w węźle `lib` dla każdego obiektu docelowego TxMs to wszystko, co jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="cca2a-168">For most packages a folder under `lib` for each of the target TxMs is all that is required.</span></span>

## <a name="ref"></a><span data-ttu-id="cca2a-169">REF</span><span class="sxs-lookup"><span data-stu-id="cca2a-169">Ref</span></span>

<span data-ttu-id="cca2a-170">Czasami są przypadki użycia innego zestawu podczas kompilacji (do tego dzisiaj zestawy referencyjne platformy .NET).</span><span class="sxs-lookup"><span data-stu-id="cca2a-170">There are sometimes cases where a different assembly should be used during compilation (.NET Reference Assemblies do this today).</span></span> <span data-ttu-id="cca2a-171">Dla tych przypadków użycia folder najwyższego poziomu o nazwie `ref` (skrót od "zestawy odwołań").</span><span class="sxs-lookup"><span data-stu-id="cca2a-171">For those cases, use a top-level folder called `ref` (short for "Reference Assemblies").</span></span>

<span data-ttu-id="cca2a-172">Większość autorom pakietów nie wymagają `ref` folderu.</span><span class="sxs-lookup"><span data-stu-id="cca2a-172">Most package authors don't require the `ref` folder.</span></span> <span data-ttu-id="cca2a-173">Jest to przydatne w przypadku pakietów, które muszą zapewnić spójny obszar powierzchni dla IntelliSense i kompilacja, ale następnie różne implementacje dla różnych TxMs.</span><span class="sxs-lookup"><span data-stu-id="cca2a-173">It is useful for packages that need to provide a consistent surface area for compilation and IntelliSense but then have different implementation for different TxMs.</span></span> <span data-ttu-id="cca2a-174">Największe przypadek użycia są `System.*` pakietów oferowanych w ramach wysyłki platformy .NET Core dla narzędzia NuGet.</span><span class="sxs-lookup"><span data-stu-id="cca2a-174">The biggest use case of this are the `System.*` packages that are being produced as part of shipping .NET Core on NuGet.</span></span> <span data-ttu-id="cca2a-175">Te pakiety mają różne implementacje, które są trwa unified według spójny zbiór zestawów odwołania.</span><span class="sxs-lookup"><span data-stu-id="cca2a-175">These packages have various implementations that are being unified by a consistent set of ref assemblies.</span></span>

<span data-ttu-id="cca2a-176">Mechanicznie zestawy zawarte w `ref` folderu są zestawy odwołania są przekazywane do kompilator.</span><span class="sxs-lookup"><span data-stu-id="cca2a-176">Mechanically, the assemblies included in the `ref` folder are the reference assemblies being passed to the compiler.</span></span> <span data-ttu-id="cca2a-177">Dla osób, które były używane csc.exe są zestawy, firma Microsoft kończy się sukcesem [opcji/Reference C#](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) przełącznika.</span><span class="sxs-lookup"><span data-stu-id="cca2a-177">For those of you who have used csc.exe these are the assemblies we are passing to the [C# /reference option](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) switch.</span></span>

<span data-ttu-id="cca2a-178">Struktura `ref` folderu jest taka sama jak `lib`, na przykład:</span><span class="sxs-lookup"><span data-stu-id="cca2a-178">The structure of the `ref` folder is the same as `lib`, for example:</span></span>

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

<span data-ttu-id="cca2a-179">W tym przykładzie zestawów w `ref` katalogów wszystkie będzie taka sama.</span><span class="sxs-lookup"><span data-stu-id="cca2a-179">In this example the assemblies in the `ref` directories would all be identical.</span></span>

## <a name="runtimes"></a><span data-ttu-id="cca2a-180">środowiska uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="cca2a-180">Runtimes</span></span>

<span data-ttu-id="cca2a-181">Folder środowiska uruchomieniowe zawiera zestawów i bibliotek natywnych wymagane do uruchamiania na określonych "runtimes", które są zazwyczaj definiowane przez architekturę systemu operacyjnego i procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="cca2a-181">The runtimes folder contains assemblies and native libraries required to run on specific "runtimes", which are generally defined by Operating System and CPU architecture.</span></span> <span data-ttu-id="cca2a-182">Te środowiska uruchomieniowe są identyfikowane za pomocą [identyfikatorów środowiska uruchomieniowego (RID)](/dotnet/core/rid-catalog) takich jak `win`, `win-x86`, `win7-x86`, `win8-64`itp.</span><span class="sxs-lookup"><span data-stu-id="cca2a-182">These runtimes are identified using [Runtime Identifiers (RIDs)](/dotnet/core/rid-catalog) such as `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span></span>

## <a name="native-helpers-to-use-platform-specific-apis"></a><span data-ttu-id="cca2a-183">Natywne pomocników użycia interfejsów API specyficznych dla platformy</span><span class="sxs-lookup"><span data-stu-id="cca2a-183">Native helpers to use platform-specific APIs</span></span>

<span data-ttu-id="cca2a-184">Poniższy przykład pokazuje czysto zarządzaną implementację dla różnych platform, które używa pomocników natywnych w systemie Windows 8, gdzie może wywołać do natywnych interfejsów API systemu Windows 8 określonego pakietu.</span><span class="sxs-lookup"><span data-stu-id="cca2a-184">The following example shows a package that has a purely managed implementation for several platforms, but uses native helpers on Windows 8 where it can call into Windows 8-specific native APIs.</span></span>

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

<span data-ttu-id="cca2a-185">Biorąc pod uwagę powyższe pakietu się zdarzyć następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="cca2a-185">Given the above package the following things happen:</span></span>

- <span data-ttu-id="cca2a-186">Kiedy nie w systemie Windows 8 `lib/net40/MyLibrary.dll` zestaw jest używany.</span><span class="sxs-lookup"><span data-stu-id="cca2a-186">When not on Windows 8 the `lib/net40/MyLibrary.dll` assembly is used.</span></span>

- <span data-ttu-id="cca2a-187">Gdy w systemie Windows 8 `runtimes/win8-<architecture>/lib/MyLibrary.dll` jest używany i `native/MyNativeHelper.dll` jest kopiowany do wyjściowego kompilacji.</span><span class="sxs-lookup"><span data-stu-id="cca2a-187">When on Windows 8 the `runtimes/win8-<architecture>/lib/MyLibrary.dll` is used and the `native/MyNativeHelper.dll` is copied to the output of your build.</span></span>

<span data-ttu-id="cca2a-188">W powyższym przykładzie `lib/net40` zestaw jest tylko kod zarządzany, podczas gdy zestawy znajdujące się w folderze środowiska uruchomieniowe będzie p/invoke do zestawu macierzystego pomocnika do wywoływania interfejsów API specyficznych dla systemu Windows 8.</span><span class="sxs-lookup"><span data-stu-id="cca2a-188">In the example above the `lib/net40` assembly is purely managed code, whilst the assemblies in the runtimes folder will p/invoke into the native helper assembly to call APIs specific to Windows 8.</span></span>

<span data-ttu-id="cca2a-189">Tylko jeden `lib` folderu jest nigdy nie zostać pobrane, więc w przypadku określonego folderu środowiska uruchomieniowego jest wybierany za pośrednictwem określonego bez środowiska uruchomieniowego `lib`.</span><span class="sxs-lookup"><span data-stu-id="cca2a-189">Only a single `lib` folder is ever be picked, so if there is a runtime specific folder it's chosen over non-runtime specific `lib`.</span></span> <span data-ttu-id="cca2a-190">Folder macierzysty to dodatek, jeśli taki istnieje, jest kopiowany do danych wyjściowych kompilacji.</span><span class="sxs-lookup"><span data-stu-id="cca2a-190">The native folder is additive, if it exists it's copied to the output of the build.</span></span>

## <a name="managed-wrapper"></a><span data-ttu-id="cca2a-191">Zarządzana otoka</span><span class="sxs-lookup"><span data-stu-id="cca2a-191">Managed wrapper</span></span>

<span data-ttu-id="cca2a-192">Innym sposobem użycia środowiska uruchomieniowe jest na potrzeby wysłania pakietu, który jest całkowicie zarządzana otoka za pośrednictwem natywnych zestawów.</span><span class="sxs-lookup"><span data-stu-id="cca2a-192">Another way to use runtimes is to ship a package that is purely a managed wrapper over a native assembly.</span></span> <span data-ttu-id="cca2a-193">W tym scenariuszu utworzysz pakietu, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="cca2a-193">In this scenario you create a package like the following:</span></span>

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

<span data-ttu-id="cca2a-194">W tym przypadku istnieje nie najwyższego poziomu `lib` folderze, w tym folderze, co tam się bez wdrażania tego pakietu, który nie jest zależny od odpowiedniego natywny zestaw.</span><span class="sxs-lookup"><span data-stu-id="cca2a-194">In this case there is no top-level `lib` folder as that folder as there is no implementation of this package that doesn't rely on the corresponding native assembly.</span></span> <span data-ttu-id="cca2a-195">Jeśli zestaw zarządzany `MyLibrary.dll`, została dokładnie takie same w obu przypadkach firma Microsoft może umieścić go w najwyższego poziomu `lib` folderu, ale ponieważ brak natywny zestaw nie powoduje pakietu niepowodzenie instalacji, jeśli została zainstalowana na platformie, nie były win x86 lub win x64, a następnie lib najwyższego poziomu będzie używana, ale nie natywny zestaw zostałoby skopiowanych.</span><span class="sxs-lookup"><span data-stu-id="cca2a-195">If the managed assembly, `MyLibrary.dll`, was exactly the same in both of these cases then we could put it in a top level `lib` folder, but because the lack of a native assembly doesn't cause the package to fail installing if it was installed on a platform that wasn't win-x86 or win-x64 then the top level lib would be used but no native assembly would be copied.</span></span>

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a><span data-ttu-id="cca2a-196">Tworzenie pakietów NuGet, 2 i NuGet 3</span><span class="sxs-lookup"><span data-stu-id="cca2a-196">Authoring packages for NuGet 2 and NuGet 3</span></span>

<span data-ttu-id="cca2a-197">Jeśli chcesz utworzyć pakiet, który może być zużyte przez projektów przy użyciu `packages.config` również jako pakiety przy użyciu `project.json` następnie następujących warunków:</span><span class="sxs-lookup"><span data-stu-id="cca2a-197">If you want to create a package that can be consumed by projects using `packages.config` as well as packages using `project.json` then the following apply:</span></span>

- <span data-ttu-id="cca2a-198">REF i środowisk wykonawczych pracować tylko NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="cca2a-198">Ref and runtimes only work on NuGet 3.</span></span> <span data-ttu-id="cca2a-199">Są one zarówno ignorowane przez NuGet 2.</span><span class="sxs-lookup"><span data-stu-id="cca2a-199">They are both ignored by NuGet 2.</span></span>

- <span data-ttu-id="cca2a-200">Nie można polegać na `install.ps1` lub `uninstall.ps1` funkcji.</span><span class="sxs-lookup"><span data-stu-id="cca2a-200">You cannot rely on `install.ps1` or `uninstall.ps1` to function.</span></span> <span data-ttu-id="cca2a-201">Wykonaj te pliki, korzystając z `packages.config`, ale są ignorowane z `project.json`.</span><span class="sxs-lookup"><span data-stu-id="cca2a-201">These files execute when using `packages.config`, but are ignored with `project.json`.</span></span> <span data-ttu-id="cca2a-202">Więc pakietu musi być możliwe bez ich uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="cca2a-202">So your package needs to be usable without them running.</span></span> <span data-ttu-id="cca2a-203">`init.ps1` wciąż działa na NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="cca2a-203">`init.ps1` still runs on NuGet 3.</span></span>

- <span data-ttu-id="cca2a-204">Cele i właściwości instalacji jest inny, dlatego upewnij się, że pakiet działa zgodnie z oczekiwaniami na obu komputerach klienckich.</span><span class="sxs-lookup"><span data-stu-id="cca2a-204">Targets and Props installation is different, so make sure that your package works as expected on both clients.</span></span>

- <span data-ttu-id="cca2a-205">Podkatalogi lib musi być TxM NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="cca2a-205">Subdirectories of lib must be a TxM in NuGet 3.</span></span> <span data-ttu-id="cca2a-206">Nie można umieścić bibliotek w katalogu głównym `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="cca2a-206">You cannot place libraries at the root of the `lib` folder.</span></span>

- <span data-ttu-id="cca2a-207">Zawartość nie jest kopiowana automatycznie za pomocą NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="cca2a-207">Content is not copied automatically with NuGet 3.</span></span> <span data-ttu-id="cca2a-208">Konsumentów pakietu można kopiować pliki, samodzielnie lub użyj narzędzia, takiego jak modułu uruchamiającego zadania do zautomatyzowania kopiowania plików.</span><span class="sxs-lookup"><span data-stu-id="cca2a-208">Consumers of your package could copy the files themselves or use a tool like a task runner to automate copying the files.</span></span>

- <span data-ttu-id="cca2a-209">Przekształcenia pliku źródłowego i konfiguracji nie są uruchamiane przez NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="cca2a-209">Source and config file transforms are not run by NuGet 3.</span></span>

<span data-ttu-id="cca2a-210">Jeśli są obsługiwane NuGet 2 i 3 wówczas `minClientVersion` powinno być najniższą wersją klienta NuGet 2, który pracuje pakietu.</span><span class="sxs-lookup"><span data-stu-id="cca2a-210">If you are supporting NuGet 2 and 3 then your `minClientVersion` should be the lowest version of NuGet 2 client that your package works on.</span></span> <span data-ttu-id="cca2a-211">W przypadku istniejącego pakietu nie powinna wymagać zmiany.</span><span class="sxs-lookup"><span data-stu-id="cca2a-211">In the case of an existing package it shouldn't need to change.</span></span>
