---
title: Tworzenie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet
description: Szczegółowy przewodnik dotyczący procesu projektowania i tworzenia pakietu NuGet, w tym najważniejszych punktów decyzyjnych, takich jak pliki i przechowywanie wersji.
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 712e4c7159aa9719052330d8e45f63e18e390325
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230590"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a><span data-ttu-id="99851-103">Tworzenie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet</span><span class="sxs-lookup"><span data-stu-id="99851-103">Create a NuGet package using the dotnet CLI</span></span>

<span data-ttu-id="99851-104">Niezależnie od tego, co Twój pakiet lub jaki kod zawiera, użyj jednego z narzędzi interfejsu wiersza polecenia, `nuget.exe` lub `dotnet.exe`, aby spakować tę funkcję do składnika, który może być współużytkowany i używany przez dowolną liczbę innych deweloperów.</span><span class="sxs-lookup"><span data-stu-id="99851-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="99851-105">W tym artykule opisano sposób tworzenia pakietu przy użyciu interfejsu wiersza polecenia dotnet.</span><span class="sxs-lookup"><span data-stu-id="99851-105">This article describes how to create a package using the dotnet CLI.</span></span> <span data-ttu-id="99851-106">Aby zainstalować interfejs wiersza polecenia `dotnet`, zobacz [Instalowanie narzędzi klienckich programu NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="99851-106">To install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="99851-107">Począwszy od programu Visual Studio 2017, interfejs wiersza polecenia dotnet jest dołączany do obciążeń .NET Core.</span><span class="sxs-lookup"><span data-stu-id="99851-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="99851-108">W przypadku projektów .NET Core i .NET Standard, które korzystają z [formatu zestawu SDK](../resources/check-project-format.md)i innych projektów w stylu zestawu SDK, NuGet używa informacji w pliku projektu bezpośrednio do tworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="99851-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="99851-109">Aby zapoznać się z samouczkami krok po kroku, zobacz [Tworzenie pakietów .NET standard za pomocą interfejsu wiersza polecenia dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) lub [Tworzenie pakietów .NET standard przy użyciu programu Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="99851-109">For step-by-step tutorials, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) or [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="99851-110">`msbuild -t:pack` jest funkcją równoważną z `dotnet pack`.</span><span class="sxs-lookup"><span data-stu-id="99851-110">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="99851-111">Aby skompilować przy użyciu programu MSBuild, zobacz [Tworzenie pakietu NuGet przy użyciu programu MSBuild](creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="99851-111">To build with MSBuild, see [Create a NuGet package using MSBuild](creating-a-package-msbuild.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="99851-112">Ten temat ma zastosowanie do projektów w [stylu zestawu SDK](../resources/check-project-format.md) , zwykle .NET Core i projektów .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="99851-112">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="99851-113">Ustawianie właściwości</span><span class="sxs-lookup"><span data-stu-id="99851-113">Set properties</span></span>

<span data-ttu-id="99851-114">Do utworzenia pakietu wymagane są następujące właściwości.</span><span class="sxs-lookup"><span data-stu-id="99851-114">The following properties are required to create a package.</span></span>

- <span data-ttu-id="99851-115">`PackageId`identyfikator pakietu, który musi być unikatowy w galerii, w której znajduje się pakiet.</span><span class="sxs-lookup"><span data-stu-id="99851-115">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="99851-116">Jeśli nie zostanie określony, wartość domyślna to `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="99851-116">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="99851-117">`Version`, określony numer wersji w postaci *główna. pomocnicza. poprawka [-sufiks]* , gdzie *-sufiks* określa [wersję wstępną](prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="99851-117">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="99851-118">Jeśli nie zostanie określony, wartość domyślna to 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="99851-118">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="99851-119">Tytuł pakietu, który powinien pojawić się na hoście (na przykład nuget.org)</span><span class="sxs-lookup"><span data-stu-id="99851-119">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="99851-120">informacje dotyczące `Authors`, autora i właściciela.</span><span class="sxs-lookup"><span data-stu-id="99851-120">`Authors`, author and owner information.</span></span> <span data-ttu-id="99851-121">Jeśli nie zostanie określony, wartość domyślna to `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="99851-121">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="99851-122">`Company`, nazwa firmy.</span><span class="sxs-lookup"><span data-stu-id="99851-122">`Company`, your company name.</span></span> <span data-ttu-id="99851-123">Jeśli nie zostanie określony, wartość domyślna to `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="99851-123">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="99851-124">W programie Visual Studio można ustawić te wartości we właściwościach projektu (kliknij prawym przyciskiem myszy projekt w Eksplorator rozwiązań, wybierz **Właściwości**, a następnie wybierz kartę **pakiet** ).</span><span class="sxs-lookup"><span data-stu-id="99851-124">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="99851-125">Te właściwości można również ustawić bezpośrednio w plikach projektu (`.csproj`).</span><span class="sxs-lookup"><span data-stu-id="99851-125">You can also set these properties directly in the project files (`.csproj`).</span></span>

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="99851-126">Nadaj pakietowi identyfikator, który jest unikatowy w obrębie nuget.org lub dowolnego źródła pakietów, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="99851-126">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="99851-127">Poniższy przykład pokazuje prosty, kompletny plik projektu z tymi właściwościami.</span><span class="sxs-lookup"><span data-stu-id="99851-127">The following example shows a simple, complete project file with these properties included.</span></span> <span data-ttu-id="99851-128">(Nowy projekt domyślny można utworzyć przy użyciu polecenia `dotnet new classlib`).</span><span class="sxs-lookup"><span data-stu-id="99851-128">(You can create a new default project using the `dotnet new classlib` command.)</span></span>

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

<span data-ttu-id="99851-129">Można również ustawić właściwości opcjonalne, takie jak `Title`, `PackageDescription`i `PackageTags`, zgodnie z opisem w obszarze [targets pakietu MSBuild](../reference/msbuild-targets.md#pack-target), [kontrolując elementy zależne](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)i [właściwości metadanych NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="99851-129">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="99851-130">W przypadku pakietów przeznaczonych do użycia publicznego należy zwrócić szczególną uwagę na Właściwość **PackageTags** , ponieważ Tagi ułatwiają innym znalezienie pakietu i zrozumienie jego działania.</span><span class="sxs-lookup"><span data-stu-id="99851-130">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="99851-131">Aby uzyskać szczegółowe informacje na temat deklarowania zależności i określania numerów wersji, zobacz [odwołania do pakietów w plikach projektu](../consume-packages/package-references-in-project-files.md) i [przechowywanie wersji pakietu](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="99851-131">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="99851-132">Istnieje również możliwość, że zasoby są zależne od zależności bezpośrednio w pakiecie przy użyciu atrybutów `<IncludeAssets>` i `<ExcludeAssets>`.</span><span class="sxs-lookup"><span data-stu-id="99851-132">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="99851-133">Aby uzyskać więcej informacji, seee [kontrolowania elementów zależnych](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="99851-133">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="add-an-optional-description-field"></a><span data-ttu-id="99851-134">Dodaj opcjonalne pole opisu</span><span class="sxs-lookup"><span data-stu-id="99851-134">Add an optional description field</span></span>

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="99851-135">Wybierz unikatowy identyfikator pakietu i ustaw numer wersji</span><span class="sxs-lookup"><span data-stu-id="99851-135">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a><span data-ttu-id="99851-136">Uruchom pakiet polecenie</span><span class="sxs-lookup"><span data-stu-id="99851-136">Run the pack command</span></span>

<span data-ttu-id="99851-137">Aby skompilować pakiet NuGet (plik `.nupkg`) z projektu, uruchom polecenie `dotnet pack`, które również automatycznie kompiluje projekt:</span><span class="sxs-lookup"><span data-stu-id="99851-137">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="99851-138">Dane wyjściowe przedstawiają ścieżkę do pliku `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="99851-138">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="99851-139">Automatycznie Generuj pakiet podczas kompilacji</span><span class="sxs-lookup"><span data-stu-id="99851-139">Automatically generate package on build</span></span>

<span data-ttu-id="99851-140">Aby automatycznie uruchomić `dotnet pack` podczas uruchamiania `dotnet build`, Dodaj następujący wiersz do pliku projektu w `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="99851-140">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="99851-141">Po uruchomieniu `dotnet pack` w rozwiązaniu wszystkie projekty w rozwiązaniu, które są możliwe do spakowania (Właściwość[<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) jest ustawiona na `true`).</span><span class="sxs-lookup"><span data-stu-id="99851-141">When you run `dotnet pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="99851-142">Po automatycznym wygenerowaniu pakietu czas do spakowania zwiększa czas kompilacji projektu.</span><span class="sxs-lookup"><span data-stu-id="99851-142">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="99851-143">Instalacja pakietu testowego</span><span class="sxs-lookup"><span data-stu-id="99851-143">Test package installation</span></span>

<span data-ttu-id="99851-144">Przed opublikowaniem pakietu zazwyczaj należy przetestować proces instalacji pakietu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="99851-144">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="99851-145">Testy upewniają się, że wszystkie pliki, które się na bieżąco, kończą się w ich prawidłowym miejscu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="99851-145">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="99851-146">Instalacje można testować ręcznie w programie Visual Studio lub w wierszu polecenia przy użyciu standardowych [kroków instalacji pakietu](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span><span class="sxs-lookup"><span data-stu-id="99851-146">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="99851-147">Pakiety są niezmienne.</span><span class="sxs-lookup"><span data-stu-id="99851-147">Packages are immutable.</span></span> <span data-ttu-id="99851-148">W przypadku usunięcia problemu należy ponownie zmienić zawartość pakietu i pakietu, po ponownym przetestowaniu nadal będzie używana stara wersja pakietu do momentu [wyczyszczenia folderu pakiety globalne](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) .</span><span class="sxs-lookup"><span data-stu-id="99851-148">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="99851-149">Jest to szczególnie istotne w przypadku testowania pakietów, które nie używają unikatowej etykiety wersji wstępnej dla każdej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="99851-149">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99851-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="99851-150">Next Steps</span></span>

<span data-ttu-id="99851-151">Po utworzeniu pakietu, który jest plikiem `.nupkg`, można opublikować go w wybranej galerii, zgodnie z opisem w artykule [Publikowanie pakietu](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="99851-151">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="99851-152">Możesz również chcieć zwiększyć możliwości pakietu lub w inny sposób obsługiwać inne scenariusze zgodnie z opisem w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="99851-152">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="99851-153">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="99851-153">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="99851-154">Obsługa wielu platform docelowych</span><span class="sxs-lookup"><span data-stu-id="99851-154">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="99851-155">Dodaj ikonę pakietu</span><span class="sxs-lookup"><span data-stu-id="99851-155">Add a package icon</span></span>](../reference/nuspec.md#icon)
- [<span data-ttu-id="99851-156">Przekształcenia plików źródłowych i konfiguracji</span><span class="sxs-lookup"><span data-stu-id="99851-156">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="99851-157">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="99851-157">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="99851-158">Wersje wstępne</span><span class="sxs-lookup"><span data-stu-id="99851-158">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="99851-159">Ustawianie typu pakietu</span><span class="sxs-lookup"><span data-stu-id="99851-159">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="99851-160">Tworzenie pakietów z zestawami międzyoperacyjnymi modelu COM</span><span class="sxs-lookup"><span data-stu-id="99851-160">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="99851-161">Na koniec należy pamiętać o dodatkowych typach pakietów:</span><span class="sxs-lookup"><span data-stu-id="99851-161">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="99851-162">Pakiety natywne</span><span class="sxs-lookup"><span data-stu-id="99851-162">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="99851-163">Pakiety symboli</span><span class="sxs-lookup"><span data-stu-id="99851-163">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
