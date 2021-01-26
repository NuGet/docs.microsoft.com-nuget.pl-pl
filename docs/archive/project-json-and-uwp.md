---
title: project.jsNuGet dla pliku z projektami platformy UWP
description: Opis sposobu, w jaki project.jsw pliku jest używany do śledzenia zależności NuGet w projektach platforma uniwersalna systemu Windows (platformy UWP).
author: JonDouglas
ms.author: jodou
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: 30e2272aafb5d2ea8d932e3cb0209d97c30b3209
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773804"
---
# <a name="projectjson-and-uwp"></a><span data-ttu-id="dbf4c-103">Plik project.json i platforma UWP</span><span class="sxs-lookup"><span data-stu-id="dbf4c-103">project.json and UWP</span></span>

> [!Important]
> <span data-ttu-id="dbf4c-104">Ta zawartość jest przestarzała.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-104">This content is deprecated.</span></span> <span data-ttu-id="dbf4c-105">Projekty powinny używać `packages.config` formatów lub PackageReference.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-105">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="dbf4c-106">W tym dokumencie opisano strukturę pakietu, która wykorzystuje funkcje programu NuGet 3 + (Visual Studio 2015 i nowsze).</span><span class="sxs-lookup"><span data-stu-id="dbf4c-106">This document describes the package structure that employs features in NuGet 3+ (Visual Studio 2015 and later).</span></span> <span data-ttu-id="dbf4c-107">`minClientVersion`Właściwość użytkownika `.nuspec` może być używana w celu ustalenia, czy są wymagane funkcje opisane w tym miejscu przez ustawienie go na 3,1.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-107">The `minClientVersion` property of your `.nuspec` can be used to state that you require the features described here by setting it to 3.1.</span></span>

## <a name="adding-uwp-support-to-an-existing-package"></a><span data-ttu-id="dbf4c-108">Dodawanie obsługi platformy UWP do istniejącego pakietu</span><span class="sxs-lookup"><span data-stu-id="dbf4c-108">Adding UWP support to an existing package</span></span>

<span data-ttu-id="dbf4c-109">Jeśli masz istniejący pakiet i chcesz dodać obsługę aplikacji platformy UWP, nie musisz przyjąć formatu pakietu opisanego tutaj.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-109">If you have an existing package and you want to add support for UWP applications, then you don’t need to adopt the  packaging format described here.</span></span> <span data-ttu-id="dbf4c-110">Ten format należy zastosować tylko w przypadku, gdy wymagane są funkcje, które opisuje i które są dostępne tylko dla klientów zaktualizowanych do wersji 3 + klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-110">You only need to adopt this format if you require the features it describes and are willing to  work only with clients that have updated to version 3+ of the NuGet client.</span></span>

## <a name="i-already-target-netcore45"></a><span data-ttu-id="dbf4c-111">Mam już element docelowy netcore45</span><span class="sxs-lookup"><span data-stu-id="dbf4c-111">I already target netcore45</span></span>

<span data-ttu-id="dbf4c-112">Jeśli masz już miejsce docelowe `netcore45` i nie musisz korzystać z tych funkcji, nie trzeba wykonywać żadnych czynności.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-112">If you target `netcore45` already, and you don’t need to take advantage of the features here, no action is needed.</span></span> <span data-ttu-id="dbf4c-113">`netcore45` pakiety mogą być używane przez aplikacje platformy UWP.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-113">`netcore45` packages can be consumed by UWP applications.</span></span>

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a><span data-ttu-id="dbf4c-114">Chcę skorzystać z interfejsów API specyficznych dla systemu Windows 10</span><span class="sxs-lookup"><span data-stu-id="dbf4c-114">I want to take advantage of Windows 10 specific APIs</span></span>

<span data-ttu-id="dbf4c-115">W takim przypadku należy dodać `uap10.0` moniker platformy docelowej (TFM lub TxM) do pakietu.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-115">In this case you need to add the `uap10.0` target framework moniker (TFM or TxM) to your package.</span></span> <span data-ttu-id="dbf4c-116">Utwórz nowy folder w pakiecie i Dodaj zestaw, który został skompilowany do pracy z systemem Windows 10 do tego folderu.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-116">Create a new folder in your package and add the assembly that has been compiled to work with Windows 10 to that folder.</span></span>

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a><span data-ttu-id="dbf4c-117">Nie potrzebuję interfejsów API specyficznych dla systemu Windows 10, ale potrzebujesz nowych funkcji platformy .NET lub nie masz już netcore45</span><span class="sxs-lookup"><span data-stu-id="dbf4c-117">I don’t need Windows 10 specific APIs, but want new .NET features or don’t have netcore45 already</span></span>

<span data-ttu-id="dbf4c-118">W takim przypadku należy dodać `dotnet` TxM do pakietu.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-118">In this case you would add the `dotnet` TxM to your package.</span></span> <span data-ttu-id="dbf4c-119">W przeciwieństwie do innych TxMs, `dotnet` nie oznacza obszaru powierzchni lub platformy.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-119">Unlike other TxMs, `dotnet` doesn't imply a surface area or platform.</span></span> <span data-ttu-id="dbf4c-120">Jest stwierdzany, że pakiet działa na dowolnej platformie, na której działają zależności.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-120">It is stating that your package works on any platform that your dependencies work on.</span></span> <span data-ttu-id="dbf4c-121">Podczas kompilowania pakietu przy użyciu `dotnet` TxM istnieje wiele bardziej TxMych zależności określonych w programie `.nuspec` , ponieważ trzeba zdefiniować pakiety BCL, od których zależy, na przykład `System.Text` `System.Xml` itd. Lokalizacje, w których te zależności działają, definiują, gdzie działa pakiet.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-121">When building a package with the `dotnet` TxM, you are likely to have many more TxM-specific dependencies in your `.nuspec`, as you need to define the BCL packages you depend on, such `System.Text`, `System.Xml`, etc. The locations that those dependencies work on define where your package works.</span></span>

### <a name="how-do-i-find-out-my-dependencies"></a><span data-ttu-id="dbf4c-122">Jak mogę sprawdzić moje zależności</span><span class="sxs-lookup"><span data-stu-id="dbf4c-122">How do I find out my dependencies</span></span>

<span data-ttu-id="dbf4c-123">Istnieją dwa sposoby określania zależności do wyświetlenia:</span><span class="sxs-lookup"><span data-stu-id="dbf4c-123">There are two ways to figure out which dependencies to list:</span></span>

1. <span data-ttu-id="dbf4c-124">Użyj narzędzia **innej firmy** dla [generatora zależności NuSpec](https://github.com/onovotny/ReferenceGenerator) .</span><span class="sxs-lookup"><span data-stu-id="dbf4c-124">Use the [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) **3rd party** tool.</span></span> <span data-ttu-id="dbf4c-125">Narzędzie automatyzuje proces i aktualizuje `.nuspec` plik przy użyciu zależnych pakietów podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-125">The tool automates the process and updates your `.nuspec` file with the dependant packages on build.</span></span> <span data-ttu-id="dbf4c-126">Jest on dostępny za pośrednictwem pakietu NuGet [NuSpec. ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span><span class="sxs-lookup"><span data-stu-id="dbf4c-126">It is available via a NuGet package, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span></span>

1. <span data-ttu-id="dbf4c-127">(W sposób twardy) Użyj `ILDasm` , aby `.dll` sprawdzić, jakie zestawy są rzeczywiście potrzebne w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-127">(The hard way) Use `ILDasm` to look at your `.dll` to see what assemblies are actually needed at runtime.</span></span> <span data-ttu-id="dbf4c-128">Następnie ustal, z jakim pakietem NuGet pochodzą.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-128">Then determine which NuGet package they each come from.</span></span>

<span data-ttu-id="dbf4c-129">Zobacz [`project.json`](project-json.md) temat, aby uzyskać szczegółowe informacje na temat funkcji, które ułatwiają tworzenie pakietu, który obsługuje `dotnet` TxM.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-129">See the [`project.json`](project-json.md) topic for details on features that help in the creation of a package that supports the `dotnet` TxM.</span></span>

> [!Important]
> <span data-ttu-id="dbf4c-130">Jeśli pakiet jest przeznaczony do pracy z projektami PCL, zdecydowanie zalecamy utworzenie `dotnet` folderu, aby uniknąć ostrzeżeń i potencjalnych problemów ze zgodnością.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-130">If your package is intended to work with PCL projects, we highly recommend to create a `dotnet` folder, to avoid warnings and potential compatibility issues.</span></span>

## <a name="directory-structure"></a><span data-ttu-id="dbf4c-131">Struktura katalogów</span><span class="sxs-lookup"><span data-stu-id="dbf4c-131">Directory structure</span></span>

<span data-ttu-id="dbf4c-132">Pakiety NuGet używające tego formatu mają następujący dobrze znany folder i zachowania:</span><span class="sxs-lookup"><span data-stu-id="dbf4c-132">NuGet packages using this format have the following well-known folder and behaviors:</span></span>

| <span data-ttu-id="dbf4c-133">Folder</span><span class="sxs-lookup"><span data-stu-id="dbf4c-133">Folder</span></span> | <span data-ttu-id="dbf4c-134">Zachowania</span><span class="sxs-lookup"><span data-stu-id="dbf4c-134">Behaviors</span></span> |
| --- | --- |
| <span data-ttu-id="dbf4c-135">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="dbf4c-135">Build</span></span> | <span data-ttu-id="dbf4c-136">Zawiera elementy docelowe programu MSBuild i pliki props w tym folderze są zintegrowane w inny sposób w projekcie, ale w przeciwnym razie zmiany nie są zmieniane.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-136">Contains MSBuild targets and props files in this folder are integrated differently into the project, but otherwise there is no change.</span></span> |
| <span data-ttu-id="dbf4c-137">Narzędzia</span><span class="sxs-lookup"><span data-stu-id="dbf4c-137">Tools</span></span> | <span data-ttu-id="dbf4c-138">`install.ps1` i `uninstall.ps1` nie są uruchamiane.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-138">`install.ps1` and `uninstall.ps1` are not run.</span></span> <span data-ttu-id="dbf4c-139">`init.ps1` działa jak zawsze.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-139">`init.ps1` works as it always has.</span></span> |
| <span data-ttu-id="dbf4c-140">Zawartość</span><span class="sxs-lookup"><span data-stu-id="dbf4c-140">Content</span></span> | <span data-ttu-id="dbf4c-141">Zawartość nie jest automatycznie kopiowana do projektu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-141">Content is not copied automatically into a user's project.</span></span> <span data-ttu-id="dbf4c-142">Obsługa uwzględniania zawartości w projekcie jest planowana dla późniejszej wersji.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-142">Support for content inclusion in the project is planned for a later release.</span></span> |
| <span data-ttu-id="dbf4c-143">Lib</span><span class="sxs-lookup"><span data-stu-id="dbf4c-143">Lib</span></span> | <span data-ttu-id="dbf4c-144">W przypadku wielu pakietów `lib` działa tak samo jak w programie NuGet 2. x, ale z rozwiniętymi opcjami dotyczącymi nazw, które mogą być używane wewnątrz niego, i lepsza logika do wybierania poprawnego podfolderu podczas korzystania z pakietów.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-144">For many packages the `lib` works the same way it does in NuGet 2.x, but with expanded options for what names can be used inside it and better logic for picking the correct sub-folder when consuming packages.</span></span> <span data-ttu-id="dbf4c-145">Jednak w przypadku użycia w połączeniu z programem `ref` `lib` folder zawiera zestawy implementujące obszar powierzchni zdefiniowany przez zestawy w `ref` folderze.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-145">However, when used in conjunction with `ref`, the `lib` folder contains assemblies that implement the surface area defined by the assemblies in the `ref` folder.</span></span> |
| <span data-ttu-id="dbf4c-146">Umieszczone</span><span class="sxs-lookup"><span data-stu-id="dbf4c-146">Ref</span></span> | <span data-ttu-id="dbf4c-147">`ref` jest opcjonalnym folderem zawierającym zestawy .NET definiujące publiczną (typy publiczne i metody) dla aplikacji do skompilowania.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-147">`ref` is an optional folder that contains .NET assemblies defining the public surface (public types and methods) for an application to compile against.</span></span> <span data-ttu-id="dbf4c-148">Zestawy w tym folderze mogą nie mieć implementacji, są one wyłącznie używane do definiowania obszaru powierzchni dla kompilatora.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-148">The assemblies in this folder may have no implementation, they are purely used to define surface area for the compiler.</span></span> <span data-ttu-id="dbf4c-149">Jeśli pakiet nie ma `ref` folderu, to `lib` zarówno zestaw odwołania, jak i zestaw implementacji.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-149">If the package has no `ref` folder, then the `lib` is both the reference assembly and the implementation assembly.</span></span> |
| <span data-ttu-id="dbf4c-150">Runtime</span><span class="sxs-lookup"><span data-stu-id="dbf4c-150">Runtimes</span></span> | <span data-ttu-id="dbf4c-151">`runtimes` jest folderem opcjonalnym, który zawiera kod specyficzny dla systemu operacyjnego, taki jak architektura procesora CPU i dane binarne zależne od platformy lub w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-151">`runtimes` is an optional folder that contains OS specific code, such as CPU architecture and OS specific or otherwise platform-dependent binaries.</span></span> |

## <a name="msbuild-targets-and-props-files-in-packages"></a><span data-ttu-id="dbf4c-152">Elementy docelowe programu MSBuild i pliki props w pakietach</span><span class="sxs-lookup"><span data-stu-id="dbf4c-152">MSBuild targets and props files in packages</span></span>

<span data-ttu-id="dbf4c-153">Pakiety NuGet mogą zawierać `.targets` i `.props` pliki, które są importowane do dowolnego projektu programu MSBuild, do którego pakiet jest instalowany.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-153">NuGet packages can contain `.targets` and `.props` files which are imported into any MSBuild project that the package is installed into.</span></span> <span data-ttu-id="dbf4c-154">W programie NuGet 2. x zostało to zrobione przez wstrzyknięcie `<Import>` instrukcji do `.csproj` pliku, w programie NuGet 3,0 nie ma określonego działania "Instalacja do projektu".</span><span class="sxs-lookup"><span data-stu-id="dbf4c-154">In NuGet 2.x, this was done by injecting `<Import>` statements into the `.csproj` file, in NuGet 3.0 there is no specific "installation to project" action.</span></span> <span data-ttu-id="dbf4c-155">Zamiast tego proces przywracania pakietu zapisuje dwa pliki `[projectname].nuget.props` i `[projectname].NuGet.targets` .</span><span class="sxs-lookup"><span data-stu-id="dbf4c-155">Instead the package restore process writes two files `[projectname].nuget.props` and `[projectname].NuGet.targets`.</span></span>

<span data-ttu-id="dbf4c-156">Program MSBuild wie o tych dwóch plikach i automatycznie importuje je blisko początku i blisko końca procesu tworzenia projektu.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-156">MSBuild knows to look for these two files and automatically imports them near the beginning and near the end of the project build process.</span></span> <span data-ttu-id="dbf4c-157">Zapewnia to bardzo podobne zachowanie do programu NuGet 2. x, ale z jedną istotną różnicą: *w tym przypadku nie ma gwarantowanej kolejności plików Target/props*.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-157">This provides very similar behavior to NuGet 2.x, but with one major difference: *there is no guaranteed order of targets/props files in this case*.</span></span> <span data-ttu-id="dbf4c-158">Jednak program MSBuild zapewnia sposoby porządkowania obiektów docelowych za pomocą `BeforeTargets` atrybutów i `AfterTargets` `<Target>` definicji (patrz [element Target)](/visualstudio/msbuild/target-element-msbuild).</span><span class="sxs-lookup"><span data-stu-id="dbf4c-158">However, MSBuild does provide ways to order targets through the `BeforeTargets` and `AfterTargets` attributes of the `<Target>` definition (see [Target Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span></span>

## <a name="lib-and-ref"></a><span data-ttu-id="dbf4c-159">Lib i ref</span><span class="sxs-lookup"><span data-stu-id="dbf4c-159">Lib and Ref</span></span>

<span data-ttu-id="dbf4c-160">Zachowanie `lib` folderu nie zmienia się znacząco w programie NuGet v3.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-160">The behavior of the `lib` folder hasn't changed significantly in NuGet v3.</span></span> <span data-ttu-id="dbf4c-161">Jednak wszystkie zestawy muszą znajdować się w podfolderach o nazwie po TxM i nie mogą być umieszczane bezpośrednio w `lib` folderze.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-161">However, all assemblies must be within sub-folders named after a TxM, and can no longer be placed directly under the `lib` folder.</span></span> <span data-ttu-id="dbf4c-162">TxM to nazwa platformy, dla której ma być wykonane działanie danego elementu zawartości w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-162">A TxM is the name of a platform that a given asset in a package is supposed to work for.</span></span> <span data-ttu-id="dbf4c-163">Logicznie są to rozszerzenia monikerów platformy docelowej (TFM), np.,, `net45` `net46` `netcore50` i `dnxcore50` to wszystkie przykłady TxMs (zobacz [Platformy docelowe](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="dbf4c-163">Logically these are an extension of the Target Framework Monikers (TFM) e.g. `net45`, `net46`, `netcore50`, and `dnxcore50` are all examples of TxMs (see [Target Frameworks](../reference/target-frameworks.md).</span></span> <span data-ttu-id="dbf4c-164">TxM może odwoływać się do struktury (TFM), a także innych obszarów powierzchni związanych z platformą.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-164">TxM can refer to a framework (TFM) as well as other platform-specific surface areas.</span></span> <span data-ttu-id="dbf4c-165">Na przykład platformy UWP TxM ( `uap10.0` ) reprezentuje obszar powierzchni .NET, a także obszar powierzchniowy systemu Windows dla aplikacji platformy UWP.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-165">For example the UWP TxM (`uap10.0`) represents the .NET surface area as well as the Windows surface area for UWP applications.</span></span>

<span data-ttu-id="dbf4c-166">Przykładowa struktura lib:</span><span class="sxs-lookup"><span data-stu-id="dbf4c-166">An example lib structure:</span></span>

```
lib
├───net40
│       MyLibrary.dll
└───wp81
        MyLibrary.dll
```

<span data-ttu-id="dbf4c-167">`lib`Folder zawiera zestawy, które są używane w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-167">The `lib` folder contains assemblies that are used at runtime.</span></span> <span data-ttu-id="dbf4c-168">W przypadku większości pakietów wymagany jest folder w ramach `lib` każdego elementu docelowego TxMs.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-168">For most packages a folder under `lib` for each of the target TxMs is all that is required.</span></span>

## <a name="ref"></a><span data-ttu-id="dbf4c-169">Umieszczone</span><span class="sxs-lookup"><span data-stu-id="dbf4c-169">Ref</span></span>

<span data-ttu-id="dbf4c-170">Czasami istnieją przypadki, w których podczas kompilacji należy użyć innego zestawu (zestawy odwołań platformy .NET to dzisiaj).</span><span class="sxs-lookup"><span data-stu-id="dbf4c-170">There are sometimes cases where a different assembly should be used during compilation (.NET Reference Assemblies do this today).</span></span> <span data-ttu-id="dbf4c-171">W tych przypadkach należy użyć folderu najwyższego poziomu o nazwie `ref` (krótkie dla "zestawów odwołań").</span><span class="sxs-lookup"><span data-stu-id="dbf4c-171">For those cases, use a top-level folder called `ref` (short for "Reference Assemblies").</span></span>

<span data-ttu-id="dbf4c-172">Większość autorów pakietów nie wymaga `ref` folderu.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-172">Most package authors don't require the `ref` folder.</span></span> <span data-ttu-id="dbf4c-173">Jest to przydatne w przypadku pakietów, które wymagają zapewnienia spójnego obszaru powierzchni do kompilowania i IntelliSense, a następnie mają różne implementacje dla różnych TxMs.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-173">It is useful for packages that need to provide a consistent surface area for compilation and IntelliSense but then have different implementation for different TxMs.</span></span> <span data-ttu-id="dbf4c-174">Największym przypadkiem użycia są `System.*` pakiety, które są tworzone w ramach wysyłki platformy .NET Core w pakiecie NuGet.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-174">The biggest use case of this are the `System.*` packages that are being produced as part of shipping .NET Core on NuGet.</span></span> <span data-ttu-id="dbf4c-175">Te pakiety mają różne implementacje, które są ujednolicone przez spójny zestaw zestawów referencyjnych.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-175">These packages have various implementations that are being unified by a consistent set of ref assemblies.</span></span>

<span data-ttu-id="dbf4c-176">W sposób mechaniczny zestawy dołączone do tego `ref` folderu są zestawami odwołań, które są przesyłane do kompilatora.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-176">Mechanically, the assemblies included in the `ref` folder are the reference assemblies being passed to the compiler.</span></span> <span data-ttu-id="dbf4c-177">Dla osób, które zostały użyte csc.exe są to zestawy przekazywane do przełącznika [opcji/Reference języka C#](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) .</span><span class="sxs-lookup"><span data-stu-id="dbf4c-177">For those of you who have used csc.exe these are the assemblies we are passing to the [C# /reference option](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) switch.</span></span>

<span data-ttu-id="dbf4c-178">Struktura `ref` folderu jest taka sama jak `lib` na przykład:</span><span class="sxs-lookup"><span data-stu-id="dbf4c-178">The structure of the `ref` folder is the same as `lib`, for example:</span></span>

```
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
```

<span data-ttu-id="dbf4c-179">W tym przykładzie zestawy w `ref` katalogach powinny być identyczne.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-179">In this example the assemblies in the `ref` directories would all be identical.</span></span>

## <a name="runtimes"></a><span data-ttu-id="dbf4c-180">Runtime</span><span class="sxs-lookup"><span data-stu-id="dbf4c-180">Runtimes</span></span>

<span data-ttu-id="dbf4c-181">Folder środowiska uruchomieniowe zawiera zestawy i natywne biblioteki wymagane do uruchamiania w określonych "środowiskach uruchomieniowych", które są zwykle zdefiniowane przez system operacyjny i architekturę procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-181">The runtimes folder contains assemblies and native libraries required to run on specific "runtimes", which are generally defined by Operating System and CPU architecture.</span></span> <span data-ttu-id="dbf4c-182">Te środowiska uruchomieniowe są identyfikowane przy użyciu [identyfikatorów środowiska uruchomieniowego (RID)](/dotnet/core/rid-catalog) , takich jak `win` ,, `win-x86` `win7-x86` , `win8-64` itd.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-182">These runtimes are identified using [Runtime Identifiers (RIDs)](/dotnet/core/rid-catalog) such as `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span></span>

## <a name="native-helpers-to-use-platform-specific-apis"></a><span data-ttu-id="dbf4c-183">Natywni pomocnicy korzystający z interfejsów API specyficznych dla platformy</span><span class="sxs-lookup"><span data-stu-id="dbf4c-183">Native helpers to use platform-specific APIs</span></span>

<span data-ttu-id="dbf4c-184">W poniższym przykładzie przedstawiono pakiet, który ma czysto zarządzaną implementację kilku platform, ale używa natywnych pomocników w systemie Windows 8, gdzie może wywoływać interfejsy natywne interfejsów API dla systemu Windows 8.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-184">The following example shows a package that has a purely managed implementation for several platforms, but uses native helpers on Windows 8 where it can call into Windows 8-specific native APIs.</span></span>

```
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
```

<span data-ttu-id="dbf4c-185">Powyższym pakietem zachodzą następujące kwestie:</span><span class="sxs-lookup"><span data-stu-id="dbf4c-185">Given the above package the following things happen:</span></span>

- <span data-ttu-id="dbf4c-186">Gdy nie ma w systemie Windows 8, `lib/net40/MyLibrary.dll` używany jest zestaw.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-186">When not on Windows 8 the `lib/net40/MyLibrary.dll` assembly is used.</span></span>

- <span data-ttu-id="dbf4c-187">W przypadku systemu Windows 8 `runtimes/win8-<architecture>/lib/MyLibrary.dll` jest używany i `native/MyNativeHelper.dll` jest kopiowany do danych wyjściowych kompilacji.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-187">When on Windows 8 the `runtimes/win8-<architecture>/lib/MyLibrary.dll` is used and the `native/MyNativeHelper.dll` is copied to the output of your build.</span></span>

<span data-ttu-id="dbf4c-188">W powyższym przykładzie `lib/net40` zestaw jest czystym kodem zarządzanym, podczas gdy zestawy w folderze Runtimes są p/Invoke do natywnego zestawu pomocnika, aby wywoływać interfejsy API specyficzne dla systemu Windows 8.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-188">In the example above the `lib/net40` assembly is purely managed code, whilst the assemblies in the runtimes folder will p/invoke into the native helper assembly to call APIs specific to Windows 8.</span></span>

<span data-ttu-id="dbf4c-189">Tylko jeden `lib` folder jest kiedykolwiek wybierany, więc jeśli istnieje folder specyficzny dla środowiska uruchomieniowego, który jest wybierany przez niezależny od środowiska uruchomieniowego `lib` .</span><span class="sxs-lookup"><span data-stu-id="dbf4c-189">Only a single `lib` folder is ever be picked, so if there is a runtime specific folder it's chosen over non-runtime specific `lib`.</span></span> <span data-ttu-id="dbf4c-190">Folder macierzysty jest dodatkiem, jeśli istnieje, jest kopiowany do danych wyjściowych kompilacji.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-190">The native folder is additive, if it exists it's copied to the output of the build.</span></span>

## <a name="managed-wrapper"></a><span data-ttu-id="dbf4c-191">Otoka zarządzana</span><span class="sxs-lookup"><span data-stu-id="dbf4c-191">Managed wrapper</span></span>

<span data-ttu-id="dbf4c-192">Innym sposobem użycia środowiska uruchomieniowego jest dostarczenie pakietu, który jest całkowicie zarządzanym otoką w zestawie natywnym.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-192">Another way to use runtimes is to ship a package that is purely a managed wrapper over a native assembly.</span></span> <span data-ttu-id="dbf4c-193">W tym scenariuszu utworzysz pakiet podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="dbf4c-193">In this scenario you create a package like the following:</span></span>

```
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
```

<span data-ttu-id="dbf4c-194">W takim przypadku nie ma folderu najwyższego poziomu, ponieważ ten folder nie ma `lib` implementacji tego pakietu, który nie bazuje na odpowiednim zestawie macierzystym.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-194">In this case there is no top-level `lib` folder as that folder as there is no implementation of this package that doesn't rely on the corresponding native assembly.</span></span> <span data-ttu-id="dbf4c-195">Jeśli zarządzany zestaw, `MyLibrary.dll` ,, był dokładnie taki sam w obu tych przypadkach, można go umieścić w folderze najwyższego poziomu `lib` , ale ponieważ brak zestawu natywnego nie powoduje, że instalacja pakietu nie powiedzie się, jeśli został on zainstalowany na platformie, która nie powiodła się — x86 lub win-x64, zostanie użyta Biblioteka najwyższego poziomu, ale nie będzie można skopiować zestawu natywnego.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-195">If the managed assembly, `MyLibrary.dll`, was exactly the same in both of these cases then we could put it in a top level `lib` folder, but because the lack of a native assembly doesn't cause the package to fail installing if it was installed on a platform that wasn't win-x86 or win-x64 then the top level lib would be used but no native assembly would be copied.</span></span>

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a><span data-ttu-id="dbf4c-196">Tworzenie pakietów dla programu NuGet 2 i NuGet 3</span><span class="sxs-lookup"><span data-stu-id="dbf4c-196">Authoring packages for NuGet 2 and NuGet 3</span></span>

<span data-ttu-id="dbf4c-197">Jeśli chcesz utworzyć pakiet, który może być używany przez projekty, a `packages.config` także pakiety przy użyciu następujących warunków `project.json` :</span><span class="sxs-lookup"><span data-stu-id="dbf4c-197">If you want to create a package that can be consumed by projects using `packages.config` as well as packages using `project.json` then the following apply:</span></span>

- <span data-ttu-id="dbf4c-198">Odwołania i środowiska uruchomieniowe działają tylko na serwerze NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-198">Ref and runtimes only work on NuGet 3.</span></span> <span data-ttu-id="dbf4c-199">Są one ignorowane przez program NuGet 2.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-199">They are both ignored by NuGet 2.</span></span>

- <span data-ttu-id="dbf4c-200">Nie można polegać na `install.ps1` lub `uninstall.ps1` funkcji.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-200">You cannot rely on `install.ps1` or `uninstall.ps1` to function.</span></span> <span data-ttu-id="dbf4c-201">Te pliki są wykonywane przy użyciu `packages.config` , ale są ignorowane w programie `project.json` .</span><span class="sxs-lookup"><span data-stu-id="dbf4c-201">These files execute when using `packages.config`, but are ignored with `project.json`.</span></span> <span data-ttu-id="dbf4c-202">Aby pakiet był gotowy do użytku bez ich działania.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-202">So your package needs to be usable without them running.</span></span> <span data-ttu-id="dbf4c-203">`init.ps1` nadal działa w programie NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-203">`init.ps1` still runs on NuGet 3.</span></span>

- <span data-ttu-id="dbf4c-204">Instalacja elementów docelowych i właściwości jest inna, dlatego należy się upewnić, że pakiet działa zgodnie z oczekiwaniami na obu klientach.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-204">Targets and Props installation is different, so make sure that your package works as expected on both clients.</span></span>

- <span data-ttu-id="dbf4c-205">Podkatalogi biblioteki lib muszą być TxM w programie NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-205">Subdirectories of lib must be a TxM in NuGet 3.</span></span> <span data-ttu-id="dbf4c-206">Biblioteki nie mogą być umieszczane w katalogu głównym `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-206">You cannot place libraries at the root of the `lib` folder.</span></span>

- <span data-ttu-id="dbf4c-207">Zawartość nie jest kopiowana automatycznie z pakietem NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-207">Content is not copied automatically with NuGet 3.</span></span> <span data-ttu-id="dbf4c-208">Odbiorcy pakietu mogą skopiować same pliki lub użyć narzędzia, takiego jak moduł uruchamiający zadania, aby zautomatyzować kopiowanie plików.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-208">Consumers of your package could copy the files themselves or use a tool like a task runner to automate copying the files.</span></span>

- <span data-ttu-id="dbf4c-209">Przekształcenia plików źródłowych i konfiguracji nie są uruchamiane przez pakiet NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-209">Source and config file transforms are not run by NuGet 3.</span></span>

<span data-ttu-id="dbf4c-210">Jeśli obsługujesz program NuGet 2 i 3, `minClientVersion` powinna to być najniższa wersja klienta NuGet 2, na którym działa pakiet.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-210">If you are supporting NuGet 2 and 3 then your `minClientVersion` should be the lowest version of NuGet 2 client that your package works on.</span></span> <span data-ttu-id="dbf4c-211">W przypadku istniejącego pakietu nie trzeba zmieniać.</span><span class="sxs-lookup"><span data-stu-id="dbf4c-211">In the case of an existing package it shouldn't need to change.</span></span>
