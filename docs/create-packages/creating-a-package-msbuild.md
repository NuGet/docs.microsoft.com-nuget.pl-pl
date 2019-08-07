---
title: Tworzenie pakietu NuGet przy użyciu programu MSBuild
description: Szczegółowy przewodnik dotyczący procesu projektowania i tworzenia pakietu NuGet, w tym najważniejszych punktów decyzyjnych, takich jak pliki i przechowywanie wersji.
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: 8512b7b214db45fb2a4db742287270cb86054b7c
ms.sourcegitcommit: 5aa49478dc466c67db5c3edda7c6ce8dcd8ae033
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2019
ms.locfileid: "68818081"
---
# <a name="create-a-nuget-package-using-msbuild"></a><span data-ttu-id="92b49-103">Tworzenie pakietu NuGet przy użyciu programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="92b49-103">Create a NuGet package using MSBuild</span></span>

<span data-ttu-id="92b49-104">Niezależnie od tego, co Twój pakiet lub jaki kod zawiera, należy spakować tę funkcję do składnika, który może być współużytkowany i używany przez dowolną liczbę innych deweloperów.</span><span class="sxs-lookup"><span data-stu-id="92b49-104">No matter what your package does or what code it contains, you need to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="92b49-105">W tym artykule opisano sposób tworzenia pakietu przy użyciu programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="92b49-105">This article describes how to create a package using MSBuild.</span></span> <span data-ttu-id="92b49-106">Aby użyć programu `dotnet` MSBuild, najpierw zainstaluj interfejs wiersza polecenia, zobacz [Instalowanie narzędzi klienckich programu NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="92b49-106">To use MSBuild, first install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="92b49-107">Począwszy od programu Visual Studio 2017, interfejs wiersza polecenia dotnet jest dołączany do obciążeń .NET Core.</span><span class="sxs-lookup"><span data-stu-id="92b49-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="92b49-108">W przypadku projektów .NET Core i .NET Standard, które korzystają z [formatu zestawu SDK](../resources/check-project-format.md)i innych projektów w stylu zestawu SDK, NuGet używa informacji w pliku projektu bezpośrednio do tworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="92b49-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span>  <span data-ttu-id="92b49-109">W przypadku projektu typu innego niż zestaw SDK, który `<PackageReference>`używa, można również użyć programu MSBuild`msbuild /t:pack`().</span><span class="sxs-lookup"><span data-stu-id="92b49-109">For a non-SDK-style project that uses `<PackageReference>`, you can also use MSBuild (`msbuild /t:pack`).</span></span>

<span data-ttu-id="92b49-110">Aby skompilować przy użyciu programu MSBuild, należy dodać pakiet NuGet. Build. Tasks. Pack do zależności projektu.</span><span class="sxs-lookup"><span data-stu-id="92b49-110">To build with MSBuild, you need to add the NuGet.Build.Tasks.Pack package to the project dependencies.</span></span> <span data-ttu-id="92b49-111">Aby uzyskać szczegółowe informacje o obiektach docelowych programu MSBuild, zobacz [pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="92b49-111">For detailed information about MSBuild pack targets, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

<span data-ttu-id="92b49-112">`msbuild -t:pack`Funkcja jest równoważna `dotnet pack`z.</span><span class="sxs-lookup"><span data-stu-id="92b49-112">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="92b49-113">Aby zapoznać się `dotnet` z samouczkiem krok po kroku przy użyciu interfejsu wiersza polecenia, zobacz [Tworzenie pakietów .NET standard za pomocą interfejsu wiersza polecenia dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="92b49-113">For step-by-step tutorials using the `dotnet` CLI instead, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="92b49-114">Ten temat ma zastosowanie do projektów w [stylu zestawu SDK](../resources/check-project-format.md) , zwykle .NET Core i projektów .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="92b49-114">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="92b49-115">Ustaw właściwości</span><span class="sxs-lookup"><span data-stu-id="92b49-115">Set properties</span></span>

<span data-ttu-id="92b49-116">Do utworzenia pakietu wymagane są następujące właściwości.</span><span class="sxs-lookup"><span data-stu-id="92b49-116">The following properties are required to create a package.</span></span>

- <span data-ttu-id="92b49-117">`PackageId`Identyfikator pakietu, który musi być unikatowy w galerii, w której znajduje się pakiet.</span><span class="sxs-lookup"><span data-stu-id="92b49-117">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="92b49-118">Jeśli nie zostanie określony, wartość domyślna to `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="92b49-118">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="92b49-119">`Version`, określony numer wersji w postaci *główna. pomocnicza. poprawka [-sufiks]* , gdzie *-sufiks* określa [wersję wstępną](prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="92b49-119">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="92b49-120">Jeśli nie zostanie określony, wartość domyślna to 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="92b49-120">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="92b49-121">Tytuł pakietu, który powinien pojawić się na hoście (na przykład nuget.org)</span><span class="sxs-lookup"><span data-stu-id="92b49-121">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="92b49-122">`Authors`Informacje o autorze i właścicielu.</span><span class="sxs-lookup"><span data-stu-id="92b49-122">`Authors`, author and owner information.</span></span> <span data-ttu-id="92b49-123">Jeśli nie zostanie określony, wartość domyślna to `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="92b49-123">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="92b49-124">`Company`, nazwa firmy.</span><span class="sxs-lookup"><span data-stu-id="92b49-124">`Company`, your company name.</span></span> <span data-ttu-id="92b49-125">Jeśli nie zostanie określony, wartość domyślna to `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="92b49-125">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="92b49-126">W programie Visual Studio można ustawić te wartości we właściwościach projektu (kliknij prawym przyciskiem myszy projekt w Eksplorator rozwiązań, wybierz **Właściwości**, a następnie wybierz kartę **pakiet** ).</span><span class="sxs-lookup"><span data-stu-id="92b49-126">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="92b49-127">Możesz również ustawić te właściwości bezpośrednio w plikach projektu (`.csproj`).</span><span class="sxs-lookup"><span data-stu-id="92b49-127">You can also set these properties directly in the project files (`.csproj`).</span></span>

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="92b49-128">Nadaj pakietowi identyfikator, który jest unikatowy w obrębie nuget.org lub dowolnego źródła pakietów, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="92b49-128">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="92b49-129">Poniższy przykład pokazuje prosty, kompletny plik projektu z tymi właściwościami.</span><span class="sxs-lookup"><span data-stu-id="92b49-129">The following example shows a simple, complete project file with these properties included.</span></span>

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

<span data-ttu-id="92b49-130">Można `Title`również ustawić właściwości opcjonalne, takie jak, `PackageTags` `PackageDescription`, i, zgodnie z opisem w obszarze [targets pakietu MSBuild](../reference/msbuild-targets.md#pack-target), [kontrolować zasoby zależności](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)i [właściwości metadanych NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="92b49-130">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="92b49-131">W przypadku pakietów przeznaczonych do użycia publicznego należy zwrócić szczególną uwagę na Właściwość **PackageTags** , ponieważ Tagi ułatwiają innym znalezienie pakietu i zrozumienie jego działania.</span><span class="sxs-lookup"><span data-stu-id="92b49-131">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="92b49-132">Aby uzyskać szczegółowe informacje na temat deklarowania zależności i określania numerów wersji, zobacz [wersja pakietu](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="92b49-132">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="92b49-133">Istnieje również możliwość, że zasoby są zależne od zależności bezpośrednio w pakiecie przy użyciu `<IncludeAssets>` atrybutów `<ExcludeAssets>` i.</span><span class="sxs-lookup"><span data-stu-id="92b49-133">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="92b49-134">Aby uzyskać więcej informacji, seee [kontrolowania elementów zależnych](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="92b49-134">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="92b49-135">Wybierz unikatowy identyfikator pakietu i ustaw numer wersji</span><span class="sxs-lookup"><span data-stu-id="92b49-135">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a><span data-ttu-id="92b49-136">Dodaj pakiet NuGet. Build. Tasks. Pack</span><span class="sxs-lookup"><span data-stu-id="92b49-136">Add the NuGet.Build.Tasks.Pack package</span></span>

<span data-ttu-id="92b49-137">Aby użyć programu MSBuild, Dodaj pakiet NuGet. Build. Tasks. Pack do projektu.</span><span class="sxs-lookup"><span data-stu-id="92b49-137">To use MSBuild, add the NuGet.Build.Tasks.Pack package to your project.</span></span>

1. <span data-ttu-id="92b49-138">Otwórz plik projektu i Dodaj następujący `<PropertyGroup>` element po elemencie:</span><span class="sxs-lookup"><span data-stu-id="92b49-138">Open the project file and add the following after the `<PropertyGroup>` element:</span></span>

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. <span data-ttu-id="92b49-139">Otwórz wiersz polecenia dewelopera (w polu **wyszukiwania** wpisz **wiersz polecenia programisty**).</span><span class="sxs-lookup"><span data-stu-id="92b49-139">Open a Developer command prompt (In the **Search** box, type **Developer command prompt**).</span></span>

3. <span data-ttu-id="92b49-140">Przejdź do folderu zawierającego plik projektu i wpisz następujące polecenie, aby zainstalować pakiet NuGet. Build. Tasks. Pack.</span><span class="sxs-lookup"><span data-stu-id="92b49-140">Switch to the folder containing the project file and type the following command to install the NuGet.Build.Tasks.Pack package.</span></span>

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   <span data-ttu-id="92b49-141">Upewnij się, że dane wyjściowe programu MSBuild wskazują, że kompilacja została ukończona pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="92b49-141">Make sure that the MSBuild output indicates that the built completed successfully.</span></span>

## <a name="run-the-msbuild--tpack-command"></a><span data-ttu-id="92b49-142">Uruchamianie polecenia MSBuild-t:Pack</span><span class="sxs-lookup"><span data-stu-id="92b49-142">Run the msbuild -t:pack command</span></span>

<span data-ttu-id="92b49-143">Aby skompilować pakiet NuGet ( `.nupkg` plik) z projektu, `msbuild -t:pack` Uruchom polecenie, które również automatycznie kompiluje projekt:</span><span class="sxs-lookup"><span data-stu-id="92b49-143">To build a NuGet package (a `.nupkg` file) from the project, run the `msbuild -t:pack` command, which also builds the project automatically:</span></span>

<span data-ttu-id="92b49-144">W wierszu polecenia dla deweloperów wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="92b49-144">In the Developer command prompt, type the following command:</span></span>

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

<span data-ttu-id="92b49-145">Dane wyjściowe przedstawiają ścieżkę do `.nupkg` pliku.</span><span class="sxs-lookup"><span data-stu-id="92b49-145">The output shows the path to the `.nupkg` file.</span></span>

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

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="92b49-146">Automatycznie Generuj pakiet podczas kompilacji</span><span class="sxs-lookup"><span data-stu-id="92b49-146">Automatically generate package on build</span></span>

<span data-ttu-id="92b49-147">Aby automatycznie uruchomić `msbuild -t:pack` podczas kompilowania lub przywracania projektu, Dodaj następujący wiersz do pliku projektu w: `<PropertyGroup>`</span><span class="sxs-lookup"><span data-stu-id="92b49-147">To automatically run `msbuild -t:pack` when you build or restore the project, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="92b49-148">Po uruchomieniu `msbuild -t:pack` w rozwiązaniu to pakiety wszystkie projekty w rozwiązaniu, które są możliwe do spakowania ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) właściwość jest ustawiona na `true`.</span><span class="sxs-lookup"><span data-stu-id="92b49-148">When you run `msbuild -t:pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="92b49-149">Po automatycznym wygenerowaniu pakietu czas do spakowania zwiększa czas kompilacji projektu.</span><span class="sxs-lookup"><span data-stu-id="92b49-149">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="92b49-150">Instalacja pakietu testowego</span><span class="sxs-lookup"><span data-stu-id="92b49-150">Test package installation</span></span>

<span data-ttu-id="92b49-151">Przed opublikowaniem pakietu zazwyczaj należy przetestować proces instalacji pakietu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="92b49-151">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="92b49-152">Testy upewniają się, że wszystkie pliki, które się na bieżąco, kończą się w ich prawidłowym miejscu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="92b49-152">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="92b49-153">Instalacje można testować ręcznie w programie Visual Studio lub w wierszu polecenia przy użyciu standardowych [kroków instalacji pakietu](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span><span class="sxs-lookup"><span data-stu-id="92b49-153">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="92b49-154">Pakiety są niezmienne.</span><span class="sxs-lookup"><span data-stu-id="92b49-154">Packages are immutable.</span></span> <span data-ttu-id="92b49-155">W przypadku usunięcia problemu należy ponownie zmienić zawartość pakietu i pakietu, po ponownym przetestowaniu nadal będzie używana stara wersja pakietu do momentu wyczyszczenia folderu [pakiety globalne](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) .</span><span class="sxs-lookup"><span data-stu-id="92b49-155">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="92b49-156">Jest to szczególnie istotne w przypadku testowania pakietów, które nie używają unikatowej etykiety wersji wstępnej dla każdej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="92b49-156">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92b49-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="92b49-157">Next Steps</span></span>

<span data-ttu-id="92b49-158">Po utworzeniu pakietu, który jest `.nupkg` plikiem, można go opublikować w wybranej galerii, zgodnie z opisem w artykule [Publikowanie pakietu](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="92b49-158">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="92b49-159">Możesz również chcieć zwiększyć możliwości pakietu lub w inny sposób obsługiwać inne scenariusze zgodnie z opisem w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="92b49-159">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="92b49-160">Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="92b49-160">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
- [<span data-ttu-id="92b49-161">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="92b49-161">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="92b49-162">Obsługa wielu platform docelowych</span><span class="sxs-lookup"><span data-stu-id="92b49-162">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="92b49-163">Przekształcenia plików źródłowych i konfiguracji</span><span class="sxs-lookup"><span data-stu-id="92b49-163">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="92b49-164">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="92b49-164">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="92b49-165">Wersje wstępne</span><span class="sxs-lookup"><span data-stu-id="92b49-165">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="92b49-166">Ustawianie typu pakietu</span><span class="sxs-lookup"><span data-stu-id="92b49-166">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="92b49-167">Tworzenie pakietów z zestawami międzyoperacyjnymi modelu COM</span><span class="sxs-lookup"><span data-stu-id="92b49-167">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="92b49-168">Na koniec należy pamiętać o dodatkowych typach pakietów:</span><span class="sxs-lookup"><span data-stu-id="92b49-168">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="92b49-169">Pakiety natywne</span><span class="sxs-lookup"><span data-stu-id="92b49-169">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="92b49-170">Pakiety symboli</span><span class="sxs-lookup"><span data-stu-id="92b49-170">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
