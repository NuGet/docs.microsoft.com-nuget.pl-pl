---
title: Tworzenie pakietu NuGet przy użyciu programu MSBuild
description: Szczegółowy przewodnik po procesie projektowania i tworzenia pakietu NuGet, w tym kluczowych punktów decyzyjnych, takich jak pliki i przechowywanie wersji.
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 7166d622ef9d3975fc1c931d30caf570a765a6da
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231321"
---
# <a name="create-a-nuget-package-using-msbuild"></a><span data-ttu-id="9b3df-103">Tworzenie pakietu NuGet przy użyciu programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="9b3df-103">Create a NuGet package using MSBuild</span></span>

<span data-ttu-id="9b3df-104">Podczas tworzenia pakietu NuGet z kodu, pakiet tej funkcji do składnika, który może być współużytkowany i używany przez dowolną liczbę innych deweloperów.</span><span class="sxs-lookup"><span data-stu-id="9b3df-104">When you create a NuGet package from your code, you package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="9b3df-105">W tym artykule opisano sposób tworzenia pakietu przy użyciu msbuild.</span><span class="sxs-lookup"><span data-stu-id="9b3df-105">This article describes how to create a package using MSBuild.</span></span> <span data-ttu-id="9b3df-106">MSBuild jest preinstalowany z każdym obciążeniem programu Visual Studio, które zawiera NuGet.</span><span class="sxs-lookup"><span data-stu-id="9b3df-106">MSBuild comes preinstalled with every Visual Studio workload that contains NuGet.</span></span> <span data-ttu-id="9b3df-107">Dodatkowo można również użyć MSBuild za pośrednictwem dotnet CLI z [dotnet msbuild](https://docs.microsoft.com/dotnet/core/tools/dotnet-msbuild).</span><span class="sxs-lookup"><span data-stu-id="9b3df-107">Additionally you can also use MSBuild through the dotnet CLI with [dotnet msbuild](https://docs.microsoft.com/dotnet/core/tools/dotnet-msbuild).</span></span>

<span data-ttu-id="9b3df-108">W przypadku projektów .NET Core i .NET Standard, które używają [formatu w stylu zestawu SDK,](../resources/check-project-format.md)oraz innych projektów w stylu zestawu SDK, NuGet używa informacji w pliku projektu bezpośrednio do utworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="9b3df-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span>  <span data-ttu-id="9b3df-109">W przypadku projektu w stylu nieskładu SDK, który używa, `<PackageReference>`NuGet używa również pliku projektu do utworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="9b3df-109">For a non-SDK-style project that uses `<PackageReference>`, NuGet also uses the project file to create a package.</span></span>

<span data-ttu-id="9b3df-110">Projekty w stylu zestawu SDK mają domyślnie dostępną funkcję pakietu.</span><span class="sxs-lookup"><span data-stu-id="9b3df-110">SDK-style projects have the pack functionality available by default.</span></span> <span data-ttu-id="9b3df-111">W przypadku projektów packagereference w stylu nieskładek zestawu SDK należy dodać pakiet NuGet.Build.Tasks.Pack do zależności projektu.</span><span class="sxs-lookup"><span data-stu-id="9b3df-111">For non SDK-style PackageReference projects, you need to add the NuGet.Build.Tasks.Pack package to the project dependencies.</span></span> <span data-ttu-id="9b3df-112">Aby uzyskać szczegółowe informacje na temat obiektów docelowych pakietu MSBuild, zobacz [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="9b3df-112">For detailed information about MSBuild pack targets, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

<span data-ttu-id="9b3df-113">Polecenie, które tworzy `msbuild -t:pack`pakiet, jest funkcją równoważną `dotnet pack`.</span><span class="sxs-lookup"><span data-stu-id="9b3df-113">The command that creates a package, `msbuild -t:pack`, is functionality equivalent to `dotnet pack`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9b3df-114">W tym temacie stosuje się do projektów [w stylu zestawu SDK,](../resources/check-project-format.md) zazwyczaj .NET Core i .NET Standard projektów i projektów w stylu innych niż SDK, które używają PackageReference.</span><span class="sxs-lookup"><span data-stu-id="9b3df-114">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects, and to non-SDK-style projects that use PackageReference.</span></span>

## <a name="set-properties"></a><span data-ttu-id="9b3df-115">Ustawianie właściwości</span><span class="sxs-lookup"><span data-stu-id="9b3df-115">Set properties</span></span>

<span data-ttu-id="9b3df-116">Następujące właściwości są wymagane do utworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="9b3df-116">The following properties are required to create a package.</span></span>

- <span data-ttu-id="9b3df-117">`PackageId`, identyfikator pakietu, który musi być unikatowy w galerii, która obsługuje pakiet.</span><span class="sxs-lookup"><span data-stu-id="9b3df-117">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="9b3df-118">Jeśli nie zostanie określona, wartością domyślną jest `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="9b3df-118">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="9b3df-119">`Version`, określony numer wersji w postaci *Major.Minor.Patch[-Suffix],* gdzie *-Suffix* identyfikuje [wersje przedpremierowe](prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="9b3df-119">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="9b3df-120">Jeśli nie zostanie określona, wartość domyślna to 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="9b3df-120">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="9b3df-121">Tytuł pakietu, który powinien pojawić się na hoście (np. nuget.org)</span><span class="sxs-lookup"><span data-stu-id="9b3df-121">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="9b3df-122">`Authors`, informacje o autorze i właścicielu.</span><span class="sxs-lookup"><span data-stu-id="9b3df-122">`Authors`, author and owner information.</span></span> <span data-ttu-id="9b3df-123">Jeśli nie zostanie określona, wartością domyślną jest `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="9b3df-123">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="9b3df-124">`Company`, nazwę firmy.</span><span class="sxs-lookup"><span data-stu-id="9b3df-124">`Company`, your company name.</span></span> <span data-ttu-id="9b3df-125">Jeśli nie zostanie określona, wartością domyślną jest `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="9b3df-125">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="9b3df-126">Ponadto w przypadku pakowania projektów w stylu innych niż SDK, które używają PackageReference, wymagane jest:</span><span class="sxs-lookup"><span data-stu-id="9b3df-126">Additionally if you are packing non-SDK-style projects that use PackageReference, the following is required:</span></span>

- <span data-ttu-id="9b3df-127">`PackageOutputPath`, folder wyjściowy pakietu wygenerowanego podczas wywoływania pakietu.</span><span class="sxs-lookup"><span data-stu-id="9b3df-127">`PackageOutputPath`, the output folder for the package generated when calling pack.</span></span>

<span data-ttu-id="9b3df-128">W programie Visual Studio można ustawić te wartości we właściwościach projektu (kliknij prawym przyciskiem myszy projekt w Eksploratorze **rozwiązań,** wybierz polecenie Właściwości i wybierz kartę **Pakiet).**</span><span class="sxs-lookup"><span data-stu-id="9b3df-128">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="9b3df-129">Można również ustawić te właściwości bezpośrednio w plikach projektu (*.csproj*).</span><span class="sxs-lookup"><span data-stu-id="9b3df-129">You can also set these properties directly in the project files (*.csproj*).</span></span>

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="9b3df-130">Nadaj pakietowi identyfikator, który jest unikatowy w nuget.org lub niezależnie od źródła pakietu, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="9b3df-130">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="9b3df-131">W poniższym przykładzie przedstawiono prosty, kompletny plik projektu z tymi właściwościami.</span><span class="sxs-lookup"><span data-stu-id="9b3df-131">The following example shows a simple, complete project file with these properties included.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>ClassLibDotNetStandard</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="9b3df-132">Można również ustawić właściwości opcjonalne, `Title` `PackageDescription`takie `PackageTags`jak , i , zgodnie z opisem w [msbuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="9b3df-132">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="9b3df-133">W przypadku pakietów przeznaczonych do użytku publicznego należy zwrócić szczególną uwagę na **PackageTags** właściwości, jak tagi pomóc innym znaleźć pakiet i zrozumieć, co robi.</span><span class="sxs-lookup"><span data-stu-id="9b3df-133">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="9b3df-134">Aby uzyskać szczegółowe informacje na temat deklarowania zależności i określania numerów wersji, zobacz [Odwołania do pakietów w plikach projektu](../consume-packages/package-references-in-project-files.md) i przechowywanie wersji [pakietu](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="9b3df-134">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="9b3df-135">Jest również możliwe do powierzchni zasobów z zależności bezpośrednio w `<IncludeAssets>` `<ExcludeAssets>` pakiecie przy użyciu i atrybuty.</span><span class="sxs-lookup"><span data-stu-id="9b3df-135">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="9b3df-136">Aby uzyskać więcej informacji, zobacz [Kontrolowanie zasobów zależności](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="9b3df-136">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="add-an-optional-description-field"></a><span data-ttu-id="9b3df-137">Dodawanie opcjonalnego pola opisu</span><span class="sxs-lookup"><span data-stu-id="9b3df-137">Add an optional description field</span></span>

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="9b3df-138">Wybierz unikatowy identyfikator pakietu i ustaw numer wersji</span><span class="sxs-lookup"><span data-stu-id="9b3df-138">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a><span data-ttu-id="9b3df-139">Dodaj pakiet NuGet.Build.Tasks.Pack</span><span class="sxs-lookup"><span data-stu-id="9b3df-139">Add the NuGet.Build.Tasks.Pack package</span></span>

<span data-ttu-id="9b3df-140">Jeśli używasz MSBuild z projektu w stylu nie w stylu SDK i PackageReference, dodaj pakiet NuGet.Build.Tasks.Pack do projektu.</span><span class="sxs-lookup"><span data-stu-id="9b3df-140">If you are using MSBuild with a non-SDK-style project and PackageReference, add the NuGet.Build.Tasks.Pack package to your project.</span></span>

1. <span data-ttu-id="9b3df-141">Otwórz plik projektu i dodaj `<PropertyGroup>` następujące elementy po elemencie:</span><span class="sxs-lookup"><span data-stu-id="9b3df-141">Open the project file and add the following after the `<PropertyGroup>` element:</span></span>

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. <span data-ttu-id="9b3df-142">Otwórz wiersz polecenia Deweloper (w polu **Wyszukiwania** wpisz **wiersz polecenia Deweloper**).</span><span class="sxs-lookup"><span data-stu-id="9b3df-142">Open a Developer command prompt (In the **Search** box, type **Developer command prompt**).</span></span>

   <span data-ttu-id="9b3df-143">Zazwyczaj chcesz uruchomić wiersz polecenia dewelopera dla programu Visual Studio z menu **Start,** ponieważ zostanie on skonfigurowany ze wszystkimi niezbędnymi ścieżkami dla usługi MSBuild.</span><span class="sxs-lookup"><span data-stu-id="9b3df-143">You typically want to start the Developer Command Prompt for Visual Studio from the **Start** menu, as it will be configured with all the necessary paths for MSBuild.</span></span>

3. <span data-ttu-id="9b3df-144">Przełącz się do folderu zawierającego plik projektu i wpisz następujące polecenie, aby zainstalować pakiet NuGet.Build.Tasks.Pack.</span><span class="sxs-lookup"><span data-stu-id="9b3df-144">Switch to the folder containing the project file and type the following command to install the NuGet.Build.Tasks.Pack package.</span></span>

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   <span data-ttu-id="9b3df-145">Upewnij się, że dane wyjściowe MSBuild wskazuje, że kompilacja została pomyślnie ukończona.</span><span class="sxs-lookup"><span data-stu-id="9b3df-145">Make sure that the MSBuild output indicates that the build completed successfully.</span></span>

## <a name="run-the-msbuild--tpack-command"></a><span data-ttu-id="9b3df-146">Uruchom polecenie msbuild -t:pack</span><span class="sxs-lookup"><span data-stu-id="9b3df-146">Run the msbuild -t:pack command</span></span>

<span data-ttu-id="9b3df-147">Aby utworzyć pakiet NuGet `.nupkg` (plik) z projektu, uruchom `msbuild -t:pack` polecenie, które również automatycznie tworzy projekt:</span><span class="sxs-lookup"><span data-stu-id="9b3df-147">To build a NuGet package (a `.nupkg` file) from the project, run the `msbuild -t:pack` command, which also builds the project automatically:</span></span>

<span data-ttu-id="9b3df-148">W wierszu polecenia Deweloper dla programu Visual Studio wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="9b3df-148">In the Developer command prompt for Visual Studio, type the following command:</span></span>

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

<span data-ttu-id="9b3df-149">Dane wyjściowe pokazuje `.nupkg` ścieżkę do pliku.</span><span class="sxs-lookup"><span data-stu-id="9b3df-149">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 16.1.76+g14b0a930a7 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 8/5/2019 3:09:15 PM.
Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" on node 1 (pack target(s)).
GenerateTargetFrameworkMonikerAttribute:
Skipping target "GenerateTargetFrameworkMonikerAttribute" because all output files are up-to-date with respect to the input files.
CoreCompile:
  ...
CopyFilesToOutputDirectory:
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.dll" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll".
  ClassLib_DotNetStandard -> C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb".
GenerateNuspec:
  Successfully created package 'C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\AppLogger.1.0.0.nupkg'.
Done Building Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" (pack target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:01.21
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="9b3df-150">Automatyczne generowanie pakietu na kompilacji</span><span class="sxs-lookup"><span data-stu-id="9b3df-150">Automatically generate package on build</span></span>

<span data-ttu-id="9b3df-151">Aby automatycznie `msbuild -t:pack` uruchamiać projekt podczas tworzenia lub przywracania projektu, `<PropertyGroup>`dodaj następujący wiersz do pliku projektu w obrębie:</span><span class="sxs-lookup"><span data-stu-id="9b3df-151">To automatically run `msbuild -t:pack` when you build or restore the project, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="9b3df-152">Po uruchomieniu `msbuild -t:pack` rozwiązania, to pakuje wszystkie projekty w rozwiązaniu,[<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) które są `true`spakowane (właściwość jest ustawiona na ).</span><span class="sxs-lookup"><span data-stu-id="9b3df-152">When you run `msbuild -t:pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="9b3df-153">Po automatycznym wygenerowaniu pakietu czas do spakowania zwiększa czas kompilacji dla projektu.</span><span class="sxs-lookup"><span data-stu-id="9b3df-153">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="9b3df-154">Instalacja pakietu testowego</span><span class="sxs-lookup"><span data-stu-id="9b3df-154">Test package installation</span></span>

<span data-ttu-id="9b3df-155">Przed opublikowaniem pakietu zazwyczaj chcesz przetestować proces instalowania pakietu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="9b3df-155">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="9b3df-156">Testy upewnij się, że wszystkie pliki koniecznie kończy się w ich odpowiednich miejscach w projekcie.</span><span class="sxs-lookup"><span data-stu-id="9b3df-156">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="9b3df-157">Instalacje można testować ręcznie w programie Visual Studio lub w wierszu polecenia, wykonując [normalne kroki instalacji pakietu](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span><span class="sxs-lookup"><span data-stu-id="9b3df-157">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9b3df-158">Pakiety są niezmienne.</span><span class="sxs-lookup"><span data-stu-id="9b3df-158">Packages are immutable.</span></span> <span data-ttu-id="9b3df-159">Jeśli rozwiążesz problem, zmień zawartość pakietu i zapakuj ponownie, podczas ponownego testowania nadal będziesz używać starej wersji pakietu, dopóki nie [wyczyścisz folderu pakietów globalnych.](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders)</span><span class="sxs-lookup"><span data-stu-id="9b3df-159">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="9b3df-160">Jest to szczególnie istotne podczas testowania pakietów, które nie używają unikatowej etykiety wstępnej wersji w każdej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="9b3df-160">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b3df-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9b3df-161">Next Steps</span></span>

<span data-ttu-id="9b3df-162">Po utworzeniu pakietu, który jest `.nupkg` plikiem, można go opublikować w wybranej galerii, zgodnie z opisem w [polu Publikowanie pakietu.](../nuget-org/publish-a-package.md)</span><span class="sxs-lookup"><span data-stu-id="9b3df-162">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="9b3df-163">Można również rozszerzyć możliwości pakietu lub w inny sposób obsługiwać inne scenariusze, jak opisano w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="9b3df-163">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="9b3df-164">NuGet pack and restore as MSBuild targets NuGet pack and restore as MSBuild targets NuGet pack and restore as MSBuild targets NuGet</span><span class="sxs-lookup"><span data-stu-id="9b3df-164">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
- [<span data-ttu-id="9b3df-165">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="9b3df-165">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="9b3df-166">Obsługa wielu platform docelowych</span><span class="sxs-lookup"><span data-stu-id="9b3df-166">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="9b3df-167">Przekształcenia plików źródłowych i konfiguracyjnych</span><span class="sxs-lookup"><span data-stu-id="9b3df-167">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="9b3df-168">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="9b3df-168">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="9b3df-169">Wersje w wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="9b3df-169">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="9b3df-170">Ustawianie typu pakietu</span><span class="sxs-lookup"><span data-stu-id="9b3df-170">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="9b3df-171">Tworzenie pakietów z zestawami współdziałań COM</span><span class="sxs-lookup"><span data-stu-id="9b3df-171">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="9b3df-172">Na koniec istnieją dodatkowe typy pakietów, o których należy pamiętać:</span><span class="sxs-lookup"><span data-stu-id="9b3df-172">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="9b3df-173">Pakiety natywne</span><span class="sxs-lookup"><span data-stu-id="9b3df-173">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="9b3df-174">Pakiety symboli</span><span class="sxs-lookup"><span data-stu-id="9b3df-174">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
