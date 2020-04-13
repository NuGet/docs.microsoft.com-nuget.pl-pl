---
title: Plik NuGet project.json z projektami platformy uniwersalnej systemuśpiłnie
description: Opis sposobu, w jaki plik project.json jest używany do śledzenia zależności NuGet w projektach platformy uniwersalnej systemu Windows (UWP).
author: karann-msft
ms.author: karann
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: ac3c137dd0ba50571737093eef11c8ab0ef932b2
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "64494372"
---
# <a name="projectjson-and-uwp"></a><span data-ttu-id="b08a8-103">Plik project.json i platforma UWP</span><span class="sxs-lookup"><span data-stu-id="b08a8-103">project.json and UWP</span></span>

> [!Important]
> <span data-ttu-id="b08a8-104">Ta zawartość jest przestarzała.</span><span class="sxs-lookup"><span data-stu-id="b08a8-104">This content is deprecated.</span></span> <span data-ttu-id="b08a8-105">Projekty powinny używać `packages.config` formatów lub PackageReference.</span><span class="sxs-lookup"><span data-stu-id="b08a8-105">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="b08a8-106">W tym dokumencie opisano strukturę pakietu, który wykorzystuje funkcje w NuGet 3+ (Visual Studio 2015 i nowsze).</span><span class="sxs-lookup"><span data-stu-id="b08a8-106">This document describes the package structure that employs features in NuGet 3+ (Visual Studio 2015 and later).</span></span> <span data-ttu-id="b08a8-107">Właściwość `minClientVersion` użytkownika `.nuspec` może służyć do określania, że wymagane są funkcje opisane w tym miejscu, ustawiając ją na 3.1.</span><span class="sxs-lookup"><span data-stu-id="b08a8-107">The `minClientVersion` property of your `.nuspec` can be used to state that you require the features described here by setting it to 3.1.</span></span>

## <a name="adding-uwp-support-to-an-existing-package"></a><span data-ttu-id="b08a8-108">Dodawanie pomocy technicznej platformy uniwersalnej systemu i platformy uniwersalnej do istniejącego pakietu</span><span class="sxs-lookup"><span data-stu-id="b08a8-108">Adding UWP support to an existing package</span></span>

<span data-ttu-id="b08a8-109">Jeśli masz istniejący pakiet i chcesz dodać obsługę aplikacji platformy uniwersalnej systemuśpiłka, nie musisz przyjmować formatu opakowania opisanego w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="b08a8-109">If you have an existing package and you want to add support for UWP applications, then you don’t need to adopt the  packaging format described here.</span></span> <span data-ttu-id="b08a8-110">Wystarczy przyjąć ten format tylko wtedy, gdy wymagane funkcje, które opisuje i są chętni do pracy tylko z klientami, które zostały zaktualizowane do wersji 3 + klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="b08a8-110">You only need to adopt this format if you require the features it describes and are willing to  work only with clients that have updated to version 3+ of the NuGet client.</span></span>

## <a name="i-already-target-netcore45"></a><span data-ttu-id="b08a8-111">Ja już cel netcore45</span><span class="sxs-lookup"><span data-stu-id="b08a8-111">I already target netcore45</span></span>

<span data-ttu-id="b08a8-112">Jeśli już `netcore45` kierujesz reklamy i nie musisz korzystać z funkcji w tym miejscu, nie jest potrzebne żadne działanie.</span><span class="sxs-lookup"><span data-stu-id="b08a8-112">If you target `netcore45` already, and you don’t need to take advantage of the features here, no action is needed.</span></span> <span data-ttu-id="b08a8-113">`netcore45`pakiety mogą być używane przez aplikacje platformy uniwersalnej systemuśpiłnie.</span><span class="sxs-lookup"><span data-stu-id="b08a8-113">`netcore45` packages can be consumed by UWP applications.</span></span>

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a><span data-ttu-id="b08a8-114">Chcę skorzystać z interfejsów API specyficznych dla systemu Windows 10</span><span class="sxs-lookup"><span data-stu-id="b08a8-114">I want to take advantage of Windows 10 specific APIs</span></span>

<span data-ttu-id="b08a8-115">W takim przypadku należy `uap10.0` dodać moniker struktury docelowej (TFM lub TxM) do pakietu.</span><span class="sxs-lookup"><span data-stu-id="b08a8-115">In this case you need to add the `uap10.0` target framework moniker (TFM or TxM) to your package.</span></span> <span data-ttu-id="b08a8-116">Utwórz nowy folder w pakiecie i dodaj zestaw, który został skompilowany do pracy z systemem Windows 10 do tego folderu.</span><span class="sxs-lookup"><span data-stu-id="b08a8-116">Create a new folder in your package and add the assembly that has been compiled to work with Windows 10 to that folder.</span></span>

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a><span data-ttu-id="b08a8-117">Nie potrzebuję specyficznych interfejsów API systemu Windows 10, ale chcę nowych funkcji .NET lub nie mam już netcore45</span><span class="sxs-lookup"><span data-stu-id="b08a8-117">I don’t need Windows 10 specific APIs, but want new .NET features or don’t have netcore45 already</span></span>

<span data-ttu-id="b08a8-118">W takim przypadku należy `dotnet` dodać TxM do pakietu.</span><span class="sxs-lookup"><span data-stu-id="b08a8-118">In this case you would add the `dotnet` TxM to your package.</span></span> <span data-ttu-id="b08a8-119">W przeciwieństwie do innych `dotnet` TxM, nie oznacza powierzchni lub platformy.</span><span class="sxs-lookup"><span data-stu-id="b08a8-119">Unlike other TxMs, `dotnet` doesn't imply a surface area or platform.</span></span> <span data-ttu-id="b08a8-120">Jest to stwierdzające, że pakiet działa na dowolnej platformie, na którym działają zależności.</span><span class="sxs-lookup"><span data-stu-id="b08a8-120">It is stating that your package works on any platform that your dependencies work on.</span></span> <span data-ttu-id="b08a8-121">Podczas tworzenia pakietu `dotnet` z TxM, prawdopodobnie masz o wiele więcej zależności specyficznych dla TxM w , `.nuspec`jak trzeba `System.Text` `System.Xml`zdefiniować pakiety BCL, na których polegasz, takie , itp. Lokalizacje, które działają te zależności na zdefiniować, gdzie działa pakiet.</span><span class="sxs-lookup"><span data-stu-id="b08a8-121">When building a package with the `dotnet` TxM, you are likely to have many more TxM-specific dependencies in your `.nuspec`, as you need to define the BCL packages you depend on, such `System.Text`, `System.Xml`, etc. The locations that those dependencies work on define where your package works.</span></span>

### <a name="how-do-i-find-out-my-dependencies"></a><span data-ttu-id="b08a8-122">Jak sprawdzić moje zależności</span><span class="sxs-lookup"><span data-stu-id="b08a8-122">How do I find out my dependencies</span></span>

<span data-ttu-id="b08a8-123">Istnieją dwa sposoby, aby dowiedzieć się, które zależności do listy:</span><span class="sxs-lookup"><span data-stu-id="b08a8-123">There are two ways to figure out which dependencies to list:</span></span>

1. <span data-ttu-id="b08a8-124">Użyj narzędzia [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) **3rd party.**</span><span class="sxs-lookup"><span data-stu-id="b08a8-124">Use the [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) **3rd party** tool.</span></span> <span data-ttu-id="b08a8-125">Narzędzie automatyzuje proces `.nuspec` i aktualizuje plik za pomocą pakietów zależnych na kompilacji.</span><span class="sxs-lookup"><span data-stu-id="b08a8-125">The tool automates the process and updates your `.nuspec` file with the dependant packages on build.</span></span> <span data-ttu-id="b08a8-126">Jest on dostępny za pośrednictwem pakietu NuGet, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span><span class="sxs-lookup"><span data-stu-id="b08a8-126">It is available via a NuGet package, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span></span>

1. <span data-ttu-id="b08a8-127">(Trudna droga) Użyj, `ILDasm` aby `.dll` spojrzeć na swoje, aby zobaczyć, jakie zestawy są rzeczywiście potrzebne w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="b08a8-127">(The hard way) Use `ILDasm` to look at your `.dll` to see what assemblies are actually needed at runtime.</span></span> <span data-ttu-id="b08a8-128">Następnie należy określić, który pakiet NuGet, z którego pochodzą.</span><span class="sxs-lookup"><span data-stu-id="b08a8-128">Then determine which NuGet package they each come from.</span></span>

<span data-ttu-id="b08a8-129">Zobacz [`project.json`](project-json.md) temat, aby uzyskać szczegółowe informacje na temat funkcji, które pomagają w tworzeniu pakietu, który obsługuje `dotnet` TxM.</span><span class="sxs-lookup"><span data-stu-id="b08a8-129">See the [`project.json`](project-json.md) topic for details on features that help in the creation of a package that supports the `dotnet` TxM.</span></span>

> [!Important]
> <span data-ttu-id="b08a8-130">Jeśli pakiet jest przeznaczony do pracy z projektami PCL, zdecydowanie zaleca się utworzenie folderu, `dotnet` aby uniknąć ostrzeżeń i potencjalnych problemów ze zgodnością.</span><span class="sxs-lookup"><span data-stu-id="b08a8-130">If your package is intended to work with PCL projects, we highly recommend to create a `dotnet` folder, to avoid warnings and potential compatibility issues.</span></span>

## <a name="directory-structure"></a><span data-ttu-id="b08a8-131">Struktura katalogów</span><span class="sxs-lookup"><span data-stu-id="b08a8-131">Directory structure</span></span>

<span data-ttu-id="b08a8-132">Pakiety NuGet przy użyciu tego formatu mają następujący dobrze znany folder i zachowania:</span><span class="sxs-lookup"><span data-stu-id="b08a8-132">NuGet packages using this format have the following well-known folder and behaviors:</span></span>

| <span data-ttu-id="b08a8-133">Folder</span><span class="sxs-lookup"><span data-stu-id="b08a8-133">Folder</span></span> | <span data-ttu-id="b08a8-134">Zachowania</span><span class="sxs-lookup"><span data-stu-id="b08a8-134">Behaviors</span></span> |
| --- | --- |
| <span data-ttu-id="b08a8-135">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="b08a8-135">Build</span></span> | <span data-ttu-id="b08a8-136">Zawiera obiekty docelowe MSBuild i rekwizyty pliki w tym folderze są zintegrowane inaczej do projektu, ale w przeciwnym razie nie ma żadnych zmian.</span><span class="sxs-lookup"><span data-stu-id="b08a8-136">Contains MSBuild targets and props files in this folder are integrated differently into the project, but otherwise there is no change.</span></span> |
| <span data-ttu-id="b08a8-137">Narzędzia</span><span class="sxs-lookup"><span data-stu-id="b08a8-137">Tools</span></span> | <span data-ttu-id="b08a8-138">`install.ps1`i `uninstall.ps1` nie są uruchamiane.</span><span class="sxs-lookup"><span data-stu-id="b08a8-138">`install.ps1` and `uninstall.ps1` are not run.</span></span> <span data-ttu-id="b08a8-139">`init.ps1`działa jak zawsze.</span><span class="sxs-lookup"><span data-stu-id="b08a8-139">`init.ps1` works as it always has.</span></span> |
| <span data-ttu-id="b08a8-140">Zawartość</span><span class="sxs-lookup"><span data-stu-id="b08a8-140">Content</span></span> | <span data-ttu-id="b08a8-141">Zawartość nie jest automatycznie kopiowana do projektu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b08a8-141">Content is not copied automatically into a user's project.</span></span> <span data-ttu-id="b08a8-142">Wsparcie dla dołączania zawartości w projekcie jest planowane w nowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="b08a8-142">Support for content inclusion in the project is planned for a later release.</span></span> |
| <span data-ttu-id="b08a8-143">Lib</span><span class="sxs-lookup"><span data-stu-id="b08a8-143">Lib</span></span> | <span data-ttu-id="b08a8-144">Dla wielu `lib` pakietów działa tak samo jak w NuGet 2.x, ale z rozszerzonymi opcjami dla tego, jakie nazwy mogą być używane wewnątrz niego i lepszą logiką do wybierania poprawnego podfolderu podczas korzystania z pakietów.</span><span class="sxs-lookup"><span data-stu-id="b08a8-144">For many packages the `lib` works the same way it does in NuGet 2.x, but with expanded options for what names can be used inside it and better logic for picking the correct sub-folder when consuming packages.</span></span> <span data-ttu-id="b08a8-145">Jednak w połączeniu z `ref`folderem `lib` zawiera zestawy, które implementują powierzchnię zdefiniowaną przez zestawy w folderze. `ref`</span><span class="sxs-lookup"><span data-stu-id="b08a8-145">However, when used in conjunction with `ref`, the `lib` folder contains assemblies that implement the surface area defined by the assemblies in the `ref` folder.</span></span> |
| <span data-ttu-id="b08a8-146">Ref</span><span class="sxs-lookup"><span data-stu-id="b08a8-146">Ref</span></span> | <span data-ttu-id="b08a8-147">`ref`jest opcjonalnym folderem, który zawiera zestawy .NET definiujące powierzchnię publiczną (typy publiczne i metody) dla aplikacji do skompilowania.</span><span class="sxs-lookup"><span data-stu-id="b08a8-147">`ref` is an optional folder that contains .NET assemblies defining the public surface (public types and methods) for an application to compile against.</span></span> <span data-ttu-id="b08a8-148">Zestawy w tym folderze może mieć żadnej implementacji, są one używane wyłącznie do definiowania powierzchni dla kompilatora.</span><span class="sxs-lookup"><span data-stu-id="b08a8-148">The assemblies in this folder may have no implementation, they are purely used to define surface area for the compiler.</span></span> <span data-ttu-id="b08a8-149">Jeśli pakiet nie `ref` ma folderu, `lib` to jest zarówno zestaw odwołania i zestawu implementacji.</span><span class="sxs-lookup"><span data-stu-id="b08a8-149">If the package has no `ref` folder, then the `lib` is both the reference assembly and the implementation assembly.</span></span> |
| <span data-ttu-id="b08a8-150">Środowiska wykonawcze</span><span class="sxs-lookup"><span data-stu-id="b08a8-150">Runtimes</span></span> | <span data-ttu-id="b08a8-151">`runtimes`to opcjonalny folder zawierający kod specyficzny dla systemu operacyjnego, taki jak architektura procesora i pliki binarne specyficzne dla systemu operacyjnego lub w inny sposób zależne od platformy.</span><span class="sxs-lookup"><span data-stu-id="b08a8-151">`runtimes` is an optional folder that contains OS specific code, such as CPU architecture and OS specific or otherwise platform-dependent binaries.</span></span> |

## <a name="msbuild-targets-and-props-files-in-packages"></a><span data-ttu-id="b08a8-152">MSBuild cele i rekwizyty plików w pakietach</span><span class="sxs-lookup"><span data-stu-id="b08a8-152">MSBuild targets and props files in packages</span></span>

<span data-ttu-id="b08a8-153">Pakiety NuGet `.targets` `.props` mogą zawierać i pliki, które są importowane do dowolnego projektu MSBuild, w którym pakiet jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="b08a8-153">NuGet packages can contain `.targets` and `.props` files which are imported into any MSBuild project that the package is installed into.</span></span> <span data-ttu-id="b08a8-154">W NuGet 2.x zostało to `<Import>` zrobione przez `.csproj` wstrzykiwanie instrukcji do pliku, w NuGet 3.0 nie ma żadnych konkretnych akcji "instalacja do projektu".</span><span class="sxs-lookup"><span data-stu-id="b08a8-154">In NuGet 2.x, this was done by injecting `<Import>` statements into the `.csproj` file, in NuGet 3.0 there is no specific "installation to project" action.</span></span> <span data-ttu-id="b08a8-155">Zamiast tego proces przywracania pakietu `[projectname].nuget.props` `[projectname].NuGet.targets`zapisuje dwa pliki i .</span><span class="sxs-lookup"><span data-stu-id="b08a8-155">Instead the package restore process writes two files `[projectname].nuget.props` and `[projectname].NuGet.targets`.</span></span>

<span data-ttu-id="b08a8-156">MSBuild wie, aby wyszukać te dwa pliki i automatycznie importuje je na początku i pod koniec procesu kompilacji projektu.</span><span class="sxs-lookup"><span data-stu-id="b08a8-156">MSBuild knows to look for these two files and automatically imports them near the beginning and near the end of the project build process.</span></span> <span data-ttu-id="b08a8-157">Zapewnia to bardzo podobne zachowanie do NuGet 2.x, ale z jedną istotną różnicą: *nie ma gwarantowanej kolejności docelowych / rekwizytów plików w tym przypadku*.</span><span class="sxs-lookup"><span data-stu-id="b08a8-157">This provides very similar behavior to NuGet 2.x, but with one major difference: *there is no guaranteed order of targets/props files in this case*.</span></span> <span data-ttu-id="b08a8-158">Jednak MSBuild zapewnia sposoby zamawiania `BeforeTargets` `AfterTargets` obiektów docelowych za pomocą i atrybutów `<Target>` definicji (zobacz Element [docelowy (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span><span class="sxs-lookup"><span data-stu-id="b08a8-158">However, MSBuild does provide ways to order targets through the `BeforeTargets` and `AfterTargets` attributes of the `<Target>` definition (see [Target Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span></span>

## <a name="lib-and-ref"></a><span data-ttu-id="b08a8-159">Lib i ref</span><span class="sxs-lookup"><span data-stu-id="b08a8-159">Lib and Ref</span></span>

<span data-ttu-id="b08a8-160">Zachowanie folderu `lib` nie uległo znacznej zmianie w nuget v3.</span><span class="sxs-lookup"><span data-stu-id="b08a8-160">The behavior of the `lib` folder hasn't changed significantly in NuGet v3.</span></span> <span data-ttu-id="b08a8-161">Jednak wszystkie zestawy muszą znajdować się w podfolderach nazwanych po TxM i `lib` nie mogą być już umieszczane bezpośrednio pod folderem.</span><span class="sxs-lookup"><span data-stu-id="b08a8-161">However, all assemblies must be within sub-folders named after a TxM, and can no longer be placed directly under the `lib` folder.</span></span> <span data-ttu-id="b08a8-162">TxM to nazwa platformy, dla których dany zasób w pakiecie ma działać.</span><span class="sxs-lookup"><span data-stu-id="b08a8-162">A TxM is the name of a platform that a given asset in a package is supposed to work for.</span></span> <span data-ttu-id="b08a8-163">Logicznie rzecz biorąc, są to rozszerzenie docelowego monikers framework `net45` `net46`(TFM) `netcore50` `dnxcore50` [np.](../reference/target-frameworks.md)</span><span class="sxs-lookup"><span data-stu-id="b08a8-163">Logically these are an extension of the Target Framework Monikers (TFM) e.g. `net45`, `net46`, `netcore50`, and `dnxcore50` are all examples of TxMs (see [Target Frameworks](../reference/target-frameworks.md).</span></span> <span data-ttu-id="b08a8-164">TxM może odnosić się do struktury (TFM), jak również innych obszarów powierzchni specyficznych dla platformy.</span><span class="sxs-lookup"><span data-stu-id="b08a8-164">TxM can refer to a framework (TFM) as well as other platform-specific surface areas.</span></span> <span data-ttu-id="b08a8-165">Na przykład uwp TxM (`uap10.0`) reprezentuje obszar powierzchni .NET, a także powierzchni systemu Windows dla aplikacji platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="b08a8-165">For example the UWP TxM (`uap10.0`) represents the .NET surface area as well as the Windows surface area for UWP applications.</span></span>

<span data-ttu-id="b08a8-166">Przykładowa struktura lib:</span><span class="sxs-lookup"><span data-stu-id="b08a8-166">An example lib structure:</span></span>

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

<span data-ttu-id="b08a8-167">Folder `lib` zawiera zestawy, które są używane w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="b08a8-167">The `lib` folder contains assemblies that are used at runtime.</span></span> <span data-ttu-id="b08a8-168">Dla większości pakietów `lib` folder w ramach dla każdego z docelowych TxMs jest wszystko, co jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="b08a8-168">For most packages a folder under `lib` for each of the target TxMs is all that is required.</span></span>

## <a name="ref"></a><span data-ttu-id="b08a8-169">Ref</span><span class="sxs-lookup"><span data-stu-id="b08a8-169">Ref</span></span>

<span data-ttu-id="b08a8-170">Czasami zdarzają się przypadki, w których podczas kompilacji powinien być używany inny zestaw (zestawy odwołań.NET).</span><span class="sxs-lookup"><span data-stu-id="b08a8-170">There are sometimes cases where a different assembly should be used during compilation (.NET Reference Assemblies do this today).</span></span> <span data-ttu-id="b08a8-171">W takich przypadkach należy użyć folderu najwyższego poziomu o nazwie `ref` (skrót od "Zestawy odwołań").</span><span class="sxs-lookup"><span data-stu-id="b08a8-171">For those cases, use a top-level folder called `ref` (short for "Reference Assemblies").</span></span>

<span data-ttu-id="b08a8-172">Większość autorów pakietów `ref` nie wymaga tego folderu.</span><span class="sxs-lookup"><span data-stu-id="b08a8-172">Most package authors don't require the `ref` folder.</span></span> <span data-ttu-id="b08a8-173">Jest to przydatne dla pakietów, które muszą zapewnić spójną powierzchnię kompilacji i IntelliSense, ale następnie mają inną implementację dla różnych TxM.</span><span class="sxs-lookup"><span data-stu-id="b08a8-173">It is useful for packages that need to provide a consistent surface area for compilation and IntelliSense but then have different implementation for different TxMs.</span></span> <span data-ttu-id="b08a8-174">Największym przypadkiem użycia tego `System.*` są pakiety, które są produkowane w ramach wysyłki .NET Core na NuGet.</span><span class="sxs-lookup"><span data-stu-id="b08a8-174">The biggest use case of this are the `System.*` packages that are being produced as part of shipping .NET Core on NuGet.</span></span> <span data-ttu-id="b08a8-175">Te pakiety mają różne implementacje, które są ujednolicone przez spójny zestaw zestawów ref.</span><span class="sxs-lookup"><span data-stu-id="b08a8-175">These packages have various implementations that are being unified by a consistent set of ref assemblies.</span></span>

<span data-ttu-id="b08a8-176">Mechanicznie zestawy zawarte w folderze `ref` są zestawami odwołań przekazywanymi do kompilatora.</span><span class="sxs-lookup"><span data-stu-id="b08a8-176">Mechanically, the assemblies included in the `ref` folder are the reference assemblies being passed to the compiler.</span></span> <span data-ttu-id="b08a8-177">Dla tych z Was, którzy korzystali z csc.exe są zestawy jesteśmy przekazywania do [C# / reference przełącznik opcji.](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option)</span><span class="sxs-lookup"><span data-stu-id="b08a8-177">For those of you who have used csc.exe these are the assemblies we are passing to the [C# /reference option](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) switch.</span></span>

<span data-ttu-id="b08a8-178">Struktura folderu `ref` jest taka `lib`sama jak na przykład:</span><span class="sxs-lookup"><span data-stu-id="b08a8-178">The structure of the `ref` folder is the same as `lib`, for example:</span></span>

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

<span data-ttu-id="b08a8-179">W tym przykładzie zestawy `ref` w katalogach będą identyczne.</span><span class="sxs-lookup"><span data-stu-id="b08a8-179">In this example the assemblies in the `ref` directories would all be identical.</span></span>

## <a name="runtimes"></a><span data-ttu-id="b08a8-180">Środowiska wykonawcze</span><span class="sxs-lookup"><span data-stu-id="b08a8-180">Runtimes</span></span>

<span data-ttu-id="b08a8-181">Folder runtimes zawiera zestawy i biblioteki macierzyste wymagane do uruchamiania w określonych "środowiskach uruchomieniowych", które są zazwyczaj definiowane przez system operacyjny i architekturę procesora.</span><span class="sxs-lookup"><span data-stu-id="b08a8-181">The runtimes folder contains assemblies and native libraries required to run on specific "runtimes", which are generally defined by Operating System and CPU architecture.</span></span> <span data-ttu-id="b08a8-182">Te środowiska wykonawcze są identyfikowane przy użyciu [identyfikatorów środowiska uruchomieniowego (RID),](/dotnet/core/rid-catalog) `win`takich jak `win-x86`, , `win7-x86`, `win8-64`itp.</span><span class="sxs-lookup"><span data-stu-id="b08a8-182">These runtimes are identified using [Runtime Identifiers (RIDs)](/dotnet/core/rid-catalog) such as `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span></span>

## <a name="native-helpers-to-use-platform-specific-apis"></a><span data-ttu-id="b08a8-183">Natywni pomocnicy do korzystania z interfejsów API specyficznych dla platformy</span><span class="sxs-lookup"><span data-stu-id="b08a8-183">Native helpers to use platform-specific APIs</span></span>

<span data-ttu-id="b08a8-184">W poniższym przykładzie pokazano pakiet, który ma czysto zarządzaną implementację dla kilku platform, ale używa natywnych pomocników w systemie Windows 8, gdzie można wywołać natywne interfejsy API specyficzne dla systemu Windows 8.</span><span class="sxs-lookup"><span data-stu-id="b08a8-184">The following example shows a package that has a purely managed implementation for several platforms, but uses native helpers on Windows 8 where it can call into Windows 8-specific native APIs.</span></span>

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

<span data-ttu-id="b08a8-185">Biorąc pod uwagę powyższy pakiet, dzieją się następujące rzeczy:</span><span class="sxs-lookup"><span data-stu-id="b08a8-185">Given the above package the following things happen:</span></span>

- <span data-ttu-id="b08a8-186">Gdy nie ma w `lib/net40/MyLibrary.dll` systemie Windows 8, używany jest zestaw.</span><span class="sxs-lookup"><span data-stu-id="b08a8-186">When not on Windows 8 the `lib/net40/MyLibrary.dll` assembly is used.</span></span>

- <span data-ttu-id="b08a8-187">Gdy w systemie `runtimes/win8-<architecture>/lib/MyLibrary.dll` Windows 8 `native/MyNativeHelper.dll` jest używany i jest kopiowany do danych wyjściowych kompilacji.</span><span class="sxs-lookup"><span data-stu-id="b08a8-187">When on Windows 8 the `runtimes/win8-<architecture>/lib/MyLibrary.dll` is used and the `native/MyNativeHelper.dll` is copied to the output of your build.</span></span>

<span data-ttu-id="b08a8-188">W powyższym `lib/net40` przykładzie zestaw jest czysto zarządzany kod, podczas gdy zestawy w folderze runtimes będzie p/invoke do natywnego zestawu pomocnika do wywołania interfejsów API specyficznych dla systemu Windows 8.</span><span class="sxs-lookup"><span data-stu-id="b08a8-188">In the example above the `lib/net40` assembly is purely managed code, whilst the assemblies in the runtimes folder will p/invoke into the native helper assembly to call APIs specific to Windows 8.</span></span>

<span data-ttu-id="b08a8-189">Tylko jeden `lib` folder jest kiedykolwiek pobierany, więc jeśli istnieje folder specyficzny dla środowiska wykonawczego, jest on wybrany przez niepodejmować specyficznego dla `lib`środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="b08a8-189">Only a single `lib` folder is ever be picked, so if there is a runtime specific folder it's chosen over non-runtime specific `lib`.</span></span> <span data-ttu-id="b08a8-190">Folder macierzysty jest addytywny, jeśli istnieje, jest kopiowany do danych wyjściowych kompilacji.</span><span class="sxs-lookup"><span data-stu-id="b08a8-190">The native folder is additive, if it exists it's copied to the output of the build.</span></span>

## <a name="managed-wrapper"></a><span data-ttu-id="b08a8-191">Otoka zarządzana</span><span class="sxs-lookup"><span data-stu-id="b08a8-191">Managed wrapper</span></span>

<span data-ttu-id="b08a8-192">Innym sposobem użycia środowisk uruchomieniowych jest wysłanie pakietu, który jest czysto otoką zarządzaną przez natywny zestaw.</span><span class="sxs-lookup"><span data-stu-id="b08a8-192">Another way to use runtimes is to ship a package that is purely a managed wrapper over a native assembly.</span></span> <span data-ttu-id="b08a8-193">W tym scenariuszu można utworzyć pakiet, podobnie jak następujące:</span><span class="sxs-lookup"><span data-stu-id="b08a8-193">In this scenario you create a package like the following:</span></span>

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

<span data-ttu-id="b08a8-194">W takim przypadku nie ma `lib` żadnego folderu najwyższego poziomu, ponieważ nie ma implementacji tego pakietu, który nie polega na odpowiednim zestawie macierzystym.</span><span class="sxs-lookup"><span data-stu-id="b08a8-194">In this case there is no top-level `lib` folder as that folder as there is no implementation of this package that doesn't rely on the corresponding native assembly.</span></span> <span data-ttu-id="b08a8-195">Jeśli zarządzanyzespoł, `MyLibrary.dll`, był dokładnie taki sam w obu tych `lib` przypadkach, to możemy umieścić go w folderze najwyższego poziomu, ale ponieważ brak natywnego zestawu nie powoduje, że pakiet nie może zainstalować, jeśli został zainstalowany na platformie, która nie była win-x86 lub win-x64 następnie lib najwyższego poziomu będzie używany, ale nie natywnyzezeszes będzie kopiowany.</span><span class="sxs-lookup"><span data-stu-id="b08a8-195">If the managed assembly, `MyLibrary.dll`, was exactly the same in both of these cases then we could put it in a top level `lib` folder, but because the lack of a native assembly doesn't cause the package to fail installing if it was installed on a platform that wasn't win-x86 or win-x64 then the top level lib would be used but no native assembly would be copied.</span></span>

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a><span data-ttu-id="b08a8-196">Tworzenie pakietów dla NuGet 2 i NuGet 3</span><span class="sxs-lookup"><span data-stu-id="b08a8-196">Authoring packages for NuGet 2 and NuGet 3</span></span>

<span data-ttu-id="b08a8-197">Jeśli chcesz utworzyć pakiet, który może być `packages.config` używany przez projekty `project.json` przy użyciu, a także pakiety przy użyciu następnie stosuje się następujące:</span><span class="sxs-lookup"><span data-stu-id="b08a8-197">If you want to create a package that can be consumed by projects using `packages.config` as well as packages using `project.json` then the following apply:</span></span>

- <span data-ttu-id="b08a8-198">Ref i runtimes działają tylko na NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="b08a8-198">Ref and runtimes only work on NuGet 3.</span></span> <span data-ttu-id="b08a8-199">Oba są ignorowane przez NuGet 2.</span><span class="sxs-lookup"><span data-stu-id="b08a8-199">They are both ignored by NuGet 2.</span></span>

- <span data-ttu-id="b08a8-200">Nie można `install.ps1` polegać na lub `uninstall.ps1` do działania.</span><span class="sxs-lookup"><span data-stu-id="b08a8-200">You cannot rely on `install.ps1` or `uninstall.ps1` to function.</span></span> <span data-ttu-id="b08a8-201">Pliki te są `packages.config`wykonywane podczas korzystania `project.json`z programu , ale są ignorowane za pomocą programu .</span><span class="sxs-lookup"><span data-stu-id="b08a8-201">These files execute when using `packages.config`, but are ignored with `project.json`.</span></span> <span data-ttu-id="b08a8-202">Więc pakiet musi być użyteczny bez ich uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="b08a8-202">So your package needs to be usable without them running.</span></span> <span data-ttu-id="b08a8-203">`init.ps1`nadal działa na NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="b08a8-203">`init.ps1` still runs on NuGet 3.</span></span>

- <span data-ttu-id="b08a8-204">Obiekty docelowe i props instalacji jest inna, więc upewnij się, że pakiet działa zgodnie z oczekiwaniami na obu klientach.</span><span class="sxs-lookup"><span data-stu-id="b08a8-204">Targets and Props installation is different, so make sure that your package works as expected on both clients.</span></span>

- <span data-ttu-id="b08a8-205">Podkatalogi lib musi być TxM w NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="b08a8-205">Subdirectories of lib must be a TxM in NuGet 3.</span></span> <span data-ttu-id="b08a8-206">Nie można umieszczać bibliotek w `lib` katalogu głównym folderu.</span><span class="sxs-lookup"><span data-stu-id="b08a8-206">You cannot place libraries at the root of the `lib` folder.</span></span>

- <span data-ttu-id="b08a8-207">Zawartość nie jest kopiowana automatycznie za pomocą nuget 3.</span><span class="sxs-lookup"><span data-stu-id="b08a8-207">Content is not copied automatically with NuGet 3.</span></span> <span data-ttu-id="b08a8-208">Konsumenci pakietu mogą samodzielnie kopiować pliki lub używać narzędzia, takiego jak narzędzie, aby zautomatyzować kopiowanie plików.</span><span class="sxs-lookup"><span data-stu-id="b08a8-208">Consumers of your package could copy the files themselves or use a tool like a task runner to automate copying the files.</span></span>

- <span data-ttu-id="b08a8-209">Transformacje plików źródłowych i konfiguracyjnych nie są uruchamiane przez nuget 3.</span><span class="sxs-lookup"><span data-stu-id="b08a8-209">Source and config file transforms are not run by NuGet 3.</span></span>

<span data-ttu-id="b08a8-210">Jeśli obsługujesz NuGet 2 i 3 następnie `minClientVersion` powinny być najniższą wersję klienta NuGet 2, że pakiet działa na.</span><span class="sxs-lookup"><span data-stu-id="b08a8-210">If you are supporting NuGet 2 and 3 then your `minClientVersion` should be the lowest version of NuGet 2 client that your package works on.</span></span> <span data-ttu-id="b08a8-211">W przypadku istniejącego pakietu nie należy go zmieniać.</span><span class="sxs-lookup"><span data-stu-id="b08a8-211">In the case of an existing package it shouldn't need to change.</span></span>
