---
title: Tworzenie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet
description: Szczegółowy przewodnik po procesie projektowania i tworzenia pakietu NuGet, w tym kluczowych punktów decyzyjnych, takich jak pliki i przechowywanie wersji.
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 712e4c7159aa9719052330d8e45f63e18e390325
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230590"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a><span data-ttu-id="1c182-103">Tworzenie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet</span><span class="sxs-lookup"><span data-stu-id="1c182-103">Create a NuGet package using the dotnet CLI</span></span>

<span data-ttu-id="1c182-104">Bez względu na to, co pakiet robi lub jaki kod zawiera, należy użyć jednego z narzędzi interfejsu wiersza polecenia, albo `nuget.exe` lub `dotnet.exe`, aby spakować tę funkcjonalność do składnika, który może być współużytkowany i używany przez dowolną liczbę innych deweloperów.</span><span class="sxs-lookup"><span data-stu-id="1c182-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="1c182-105">W tym artykule opisano sposób tworzenia pakietu przy użyciu interfejsu wiersza polecenia dotnet.</span><span class="sxs-lookup"><span data-stu-id="1c182-105">This article describes how to create a package using the dotnet CLI.</span></span> <span data-ttu-id="1c182-106">Aby zainstalować `dotnet` wiersz polecenia, zobacz [Instalowanie narzędzi klienckich NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="1c182-106">To install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="1c182-107">Począwszy od programu Visual Studio 2017, dotnet interfejsu wiersza polecenia jest dołączony do obciążeń .NET Core.</span><span class="sxs-lookup"><span data-stu-id="1c182-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="1c182-108">W przypadku projektów .NET Core i .NET Standard, które używają [formatu w stylu zestawu SDK,](../resources/check-project-format.md)oraz innych projektów w stylu zestawu SDK, NuGet używa informacji w pliku projektu bezpośrednio do utworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="1c182-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="1c182-109">Aby uzyskać samouczki krok po kroku, zobacz [Tworzenie pakietów standardowych platformy .NET za pomocą interfejsu wiersza polecenia dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) lub [Tworzenie pakietów standardowych platformy .NET za pomocą programu Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="1c182-109">For step-by-step tutorials, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) or [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="1c182-110">`msbuild -t:pack`jest funkcją `dotnet pack`równoważną .</span><span class="sxs-lookup"><span data-stu-id="1c182-110">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="1c182-111">Aby tworzyć za pomocą msbuild, zobacz [Tworzenie pakietu NuGet przy użyciu msbuild](creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="1c182-111">To build with MSBuild, see [Create a NuGet package using MSBuild](creating-a-package-msbuild.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c182-112">W tym temacie stosuje się do projektów [w stylu SDK,](../resources/check-project-format.md) zazwyczaj .NET Core i .NET Standard projektów.</span><span class="sxs-lookup"><span data-stu-id="1c182-112">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="1c182-113">Ustawianie właściwości</span><span class="sxs-lookup"><span data-stu-id="1c182-113">Set properties</span></span>

<span data-ttu-id="1c182-114">Następujące właściwości są wymagane do utworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="1c182-114">The following properties are required to create a package.</span></span>

- <span data-ttu-id="1c182-115">`PackageId`, identyfikator pakietu, który musi być unikatowy w galerii, która obsługuje pakiet.</span><span class="sxs-lookup"><span data-stu-id="1c182-115">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="1c182-116">Jeśli nie zostanie określona, wartością domyślną jest `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="1c182-116">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="1c182-117">`Version`, określony numer wersji w postaci *Major.Minor.Patch[-Suffix],* gdzie *-Suffix* identyfikuje [wersje przedpremierowe](prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="1c182-117">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="1c182-118">Jeśli nie zostanie określona, wartość domyślna to 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="1c182-118">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="1c182-119">Tytuł pakietu, który powinien pojawić się na hoście (np. nuget.org)</span><span class="sxs-lookup"><span data-stu-id="1c182-119">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="1c182-120">`Authors`, informacje o autorze i właścicielu.</span><span class="sxs-lookup"><span data-stu-id="1c182-120">`Authors`, author and owner information.</span></span> <span data-ttu-id="1c182-121">Jeśli nie zostanie określona, wartością domyślną jest `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="1c182-121">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="1c182-122">`Company`, nazwę firmy.</span><span class="sxs-lookup"><span data-stu-id="1c182-122">`Company`, your company name.</span></span> <span data-ttu-id="1c182-123">Jeśli nie zostanie określona, wartością domyślną jest `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="1c182-123">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="1c182-124">W programie Visual Studio można ustawić te wartości we właściwościach projektu (kliknij prawym przyciskiem myszy projekt w Eksploratorze **rozwiązań,** wybierz polecenie Właściwości i wybierz kartę **Pakiet).**</span><span class="sxs-lookup"><span data-stu-id="1c182-124">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="1c182-125">Można również ustawić te właściwości bezpośrednio w`.csproj`plikach projektu ( ).</span><span class="sxs-lookup"><span data-stu-id="1c182-125">You can also set these properties directly in the project files (`.csproj`).</span></span>

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="1c182-126">Nadaj pakietowi identyfikator, który jest unikatowy w nuget.org lub niezależnie od źródła pakietu, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="1c182-126">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="1c182-127">W poniższym przykładzie przedstawiono prosty, kompletny plik projektu z tymi właściwościami.</span><span class="sxs-lookup"><span data-stu-id="1c182-127">The following example shows a simple, complete project file with these properties included.</span></span> <span data-ttu-id="1c182-128">(Za pomocą `dotnet new classlib` polecenia można utworzyć nowy projekt domyślny).</span><span class="sxs-lookup"><span data-stu-id="1c182-128">(You can create a new default project using the `dotnet new classlib` command.)</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="1c182-129">Można również ustawić właściwości opcjonalne, `Title` `PackageDescription`takie `PackageTags`jak , i , zgodnie z opisem w [msbuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="1c182-129">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="1c182-130">W przypadku pakietów przeznaczonych do użytku publicznego należy zwrócić szczególną uwagę na **PackageTags** właściwości, jak tagi pomóc innym znaleźć pakiet i zrozumieć, co robi.</span><span class="sxs-lookup"><span data-stu-id="1c182-130">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="1c182-131">Aby uzyskać szczegółowe informacje na temat deklarowania zależności i określania numerów wersji, zobacz [Odwołania do pakietów w plikach projektu](../consume-packages/package-references-in-project-files.md) i przechowywanie wersji [pakietu](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="1c182-131">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="1c182-132">Jest również możliwe do powierzchni zasobów z zależności bezpośrednio w `<IncludeAssets>` `<ExcludeAssets>` pakiecie przy użyciu i atrybuty.</span><span class="sxs-lookup"><span data-stu-id="1c182-132">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="1c182-133">Aby uzyskać więcej informacji, zobacz [Kontrolowanie zasobów zależności](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="1c182-133">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="add-an-optional-description-field"></a><span data-ttu-id="1c182-134">Dodawanie opcjonalnego pola opisu</span><span class="sxs-lookup"><span data-stu-id="1c182-134">Add an optional description field</span></span>

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="1c182-135">Wybierz unikatowy identyfikator pakietu i ustaw numer wersji</span><span class="sxs-lookup"><span data-stu-id="1c182-135">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a><span data-ttu-id="1c182-136">Uruchamianie polecenia pack</span><span class="sxs-lookup"><span data-stu-id="1c182-136">Run the pack command</span></span>

<span data-ttu-id="1c182-137">Aby utworzyć pakiet NuGet `.nupkg` (plik) z projektu, uruchom `dotnet pack` polecenie, które również automatycznie tworzy projekt:</span><span class="sxs-lookup"><span data-stu-id="1c182-137">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="1c182-138">Dane wyjściowe pokazuje `.nupkg` ścieżkę do pliku.</span><span class="sxs-lookup"><span data-stu-id="1c182-138">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="1c182-139">Automatyczne generowanie pakietu na kompilacji</span><span class="sxs-lookup"><span data-stu-id="1c182-139">Automatically generate package on build</span></span>

<span data-ttu-id="1c182-140">Aby uruchomić `dotnet pack` je automatycznie `dotnet build`po uruchomieniu, dodaj następujący `<PropertyGroup>`wiersz do pliku projektu w obrębie:</span><span class="sxs-lookup"><span data-stu-id="1c182-140">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="1c182-141">Po uruchomieniu `dotnet pack` rozwiązania, to pakuje wszystkie projekty w rozwiązaniu,[<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) które są `true`spakowane (właściwość jest ustawiona na ).</span><span class="sxs-lookup"><span data-stu-id="1c182-141">When you run `dotnet pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="1c182-142">Po automatycznym wygenerowaniu pakietu czas do spakowania zwiększa czas kompilacji dla projektu.</span><span class="sxs-lookup"><span data-stu-id="1c182-142">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="1c182-143">Instalacja pakietu testowego</span><span class="sxs-lookup"><span data-stu-id="1c182-143">Test package installation</span></span>

<span data-ttu-id="1c182-144">Przed opublikowaniem pakietu zazwyczaj chcesz przetestować proces instalowania pakietu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="1c182-144">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="1c182-145">Testy upewnij się, że wszystkie pliki koniecznie kończy się w ich odpowiednich miejscach w projekcie.</span><span class="sxs-lookup"><span data-stu-id="1c182-145">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="1c182-146">Instalacje można testować ręcznie w programie Visual Studio lub w wierszu polecenia, wykonując [normalne kroki instalacji pakietu](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span><span class="sxs-lookup"><span data-stu-id="1c182-146">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c182-147">Pakiety są niezmienne.</span><span class="sxs-lookup"><span data-stu-id="1c182-147">Packages are immutable.</span></span> <span data-ttu-id="1c182-148">Jeśli rozwiążesz problem, zmień zawartość pakietu i zapakuj ponownie, podczas ponownego testowania nadal będziesz używać starej wersji pakietu, dopóki nie [wyczyścisz folderu pakietów globalnych.](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders)</span><span class="sxs-lookup"><span data-stu-id="1c182-148">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="1c182-149">Jest to szczególnie istotne podczas testowania pakietów, które nie używają unikatowej etykiety wstępnej wersji w każdej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="1c182-149">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c182-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1c182-150">Next Steps</span></span>

<span data-ttu-id="1c182-151">Po utworzeniu pakietu, który jest `.nupkg` plikiem, można go opublikować w wybranej galerii, zgodnie z opisem w [polu Publikowanie pakietu.](../nuget-org/publish-a-package.md)</span><span class="sxs-lookup"><span data-stu-id="1c182-151">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="1c182-152">Można również rozszerzyć możliwości pakietu lub w inny sposób obsługiwać inne scenariusze, jak opisano w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="1c182-152">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="1c182-153">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="1c182-153">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="1c182-154">Obsługa wielu platform docelowych</span><span class="sxs-lookup"><span data-stu-id="1c182-154">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="1c182-155">Dodawanie ikony pakietu</span><span class="sxs-lookup"><span data-stu-id="1c182-155">Add a package icon</span></span>](../reference/nuspec.md#icon)
- [<span data-ttu-id="1c182-156">Przekształcenia plików źródłowych i konfiguracyjnych</span><span class="sxs-lookup"><span data-stu-id="1c182-156">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="1c182-157">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="1c182-157">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="1c182-158">Wersje w wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="1c182-158">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="1c182-159">Ustawianie typu pakietu</span><span class="sxs-lookup"><span data-stu-id="1c182-159">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="1c182-160">Tworzenie pakietów z zestawami współdziałań COM</span><span class="sxs-lookup"><span data-stu-id="1c182-160">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="1c182-161">Na koniec istnieją dodatkowe typy pakietów, o których należy pamiętać:</span><span class="sxs-lookup"><span data-stu-id="1c182-161">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="1c182-162">Pakiety natywne</span><span class="sxs-lookup"><span data-stu-id="1c182-162">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="1c182-163">Pakiety symboli</span><span class="sxs-lookup"><span data-stu-id="1c182-163">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
