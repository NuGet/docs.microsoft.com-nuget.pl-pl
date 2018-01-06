---
title: NuGet PackageReference w plikach projektu programu Visual Studio | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5a554e9d-1266-48c2-92e8-6dd00b1d6810
description: "Szczegółowe informacje o NuGet PackageReference w plikach projektu obsługiwana przez NuGet 4.0 + i VS2017"
keywords: "Zależności pakietów NuGet, odwołania do pakietu, projektu packages.config pliki, PackageReference, project.json, VS2017, Visual Studio 2017, NuGet 4"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 275957c94e4a4bb45f359cd48816acf4f286ebad
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/05/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="ec349-104">Odwołania do pakietu (PackageReference) w plikach projektu</span><span class="sxs-lookup"><span data-stu-id="ec349-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="ec349-105">Pakiet odwołań, za pomocą `PackageReference` węzła, umożliwiają zarządzanie zależności NuGet bezpośrednio w ramach plików projektu, zamiast konieczności oddzielnego `packages.config` lub `project.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="ec349-105">Package references, using the `PackageReference` node, allow you to manage NuGet dependencies directly within project files, rather than needing a separate `packages.config` or `project.json` file.</span></span> <span data-ttu-id="ec349-106">Ta metoda nie ma wpływu na inne aspekty NuGet; na przykład ustawienia w `NuGet.Config` plików (w tym źródeł pakietów) nadal są stosowane zgodnie z objaśnieniem w [Konfigurowanie zachowania NuGet](Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="ec349-106">This method doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](Configuring-NuGet-Behavior.md).</span></span>

> [!Important]
> <span data-ttu-id="ec349-107">Obecnie odwołania do pakietu są obsługiwane w Visual Studio 2017 tylko dla projektów .NET Core, .NET Standard projektów i projekty platformy UWP przeznaczonych dla systemu Windows 10 kompilacji 15063 (twórców aktualizacji).</span><span class="sxs-lookup"><span data-stu-id="ec349-107">At present, package references are supported in Visual Studio 2017 only, for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update).</span></span>

<span data-ttu-id="ec349-108">`PackageReference` Podejście pozwala na warunki MSBuild umożliwia wybieranie odwołania do pakietu dla platformy docelowej, konfiguracji, platformy lub inne grupy.</span><span class="sxs-lookup"><span data-stu-id="ec349-108">The `PackageReference` approach allows you to use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="ec349-109">Umożliwia on również precyzyjną kontrolę nad zależności i zawartości przepływu.</span><span class="sxs-lookup"><span data-stu-id="ec349-109">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="ec349-110">Pod względem zachowania i [rozpoznawania zależności](Dependency-Resolution.md), jest taka sama jak `project.json`.</span><span class="sxs-lookup"><span data-stu-id="ec349-110">In terms of behavior and [dependency resolution](Dependency-Resolution.md), it's the same as using `project.json`.</span></span>

<span data-ttu-id="ec349-111">Więcej szczegółów o integracji programu MSBuild z odwołaniami do pakietu w plikach projektu, zobacz [NuGet pakietu i ich przywracania docelowych elementów MSBuild](../schema/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="ec349-111">For more details on the integration of MSBuild with package references in project files, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="ec349-112">Dodawanie PackageReference</span><span class="sxs-lookup"><span data-stu-id="ec349-112">Adding a PackageReference</span></span>

<span data-ttu-id="ec349-113">Dodawanie zależności w pliku projektu, używając następującej składni:</span><span class="sxs-lookup"><span data-stu-id="ec349-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />    
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="ec349-114">Kontrolowanie wersję zależności</span><span class="sxs-lookup"><span data-stu-id="ec349-114">Controlling dependency version</span></span>

<span data-ttu-id="ec349-115">Konwencja określania wersji pakietu jest taka sama jak przy użyciu `packages.config` lub `project.json`:</span><span class="sxs-lookup"><span data-stu-id="ec349-115">The convention for specifying the version of a package is the same as when using `packages.config` or `project.json`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="ec349-116">W powyższym przykładzie 3.6.0 oznacza dowolną wersję, którą jest > = 3.6.0, z preferencją dla Najniższa wersja zgodnie z opisem na [wersji pakietu](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="ec349-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="ec349-117">Liczby zmiennoprzecinkowe wersji</span><span class="sxs-lookup"><span data-stu-id="ec349-117">Floating Versions</span></span>

<span data-ttu-id="ec349-118">[Liczby zmiennoprzecinkowe wersji](../consume-packages/dependency-resolution.md#floating-versions) są obsługiwane z `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="ec349-118">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="ec349-119">Kontrolowanie zależności zasobów</span><span class="sxs-lookup"><span data-stu-id="ec349-119">Controlling dependency assets</span></span>

<span data-ttu-id="ec349-120">Mogą używać zależność wyłącznie jako kontroler programowanie i może nie należy udostępniać który do projektów, które będą korzystać z pakietu.</span><span class="sxs-lookup"><span data-stu-id="ec349-120">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="ec349-121">W tym scenariuszu można użyć `PrivateAssets` metadanych do kontroli tego zachowania.</span><span class="sxs-lookup"><span data-stu-id="ec349-121">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="ec349-122">Następujących tagów metadanych kontrolować zależności zasobów:</span><span class="sxs-lookup"><span data-stu-id="ec349-122">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="ec349-123">Tag</span><span class="sxs-lookup"><span data-stu-id="ec349-123">Tag</span></span> | <span data-ttu-id="ec349-124">Opis</span><span class="sxs-lookup"><span data-stu-id="ec349-124">Description</span></span> | <span data-ttu-id="ec349-125">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="ec349-125">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ec349-126">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="ec349-126">IncludeAssets</span></span> | <span data-ttu-id="ec349-127">Te zasoby będą używane.</span><span class="sxs-lookup"><span data-stu-id="ec349-127">These assets will be consumed</span></span> | <span data-ttu-id="ec349-128">wszystkie</span><span class="sxs-lookup"><span data-stu-id="ec349-128">all</span></span> |
| <span data-ttu-id="ec349-129">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="ec349-129">ExcludeAssets</span></span> | <span data-ttu-id="ec349-130">Te zasoby nie będą używane.</span><span class="sxs-lookup"><span data-stu-id="ec349-130">These assets will not be consumed</span></span> | <span data-ttu-id="ec349-131">brak</span><span class="sxs-lookup"><span data-stu-id="ec349-131">none</span></span> | 
| <span data-ttu-id="ec349-132">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="ec349-132">PrivateAssets</span></span> | <span data-ttu-id="ec349-133">Te zasoby będą działały, ale nie będą przepływać do projektu nadrzędnego</span><span class="sxs-lookup"><span data-stu-id="ec349-133">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="ec349-134">pliki; analizatorów kompilacji</span><span class="sxs-lookup"><span data-stu-id="ec349-134">contentfiles;analyzers;build</span></span> |


<span data-ttu-id="ec349-135">Dopuszczalne wartości tych tagów są następujące, z wieloma wartościami oddzielone średnikami z wyjątkiem z `all` i `none` której musi występować samodzielnie:</span><span class="sxs-lookup"><span data-stu-id="ec349-135">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="ec349-136">Wartość</span><span class="sxs-lookup"><span data-stu-id="ec349-136">Value</span></span> | <span data-ttu-id="ec349-137">Opis</span><span class="sxs-lookup"><span data-stu-id="ec349-137">Description</span></span> |
| --- | ---
| <span data-ttu-id="ec349-138">Kompilacji</span><span class="sxs-lookup"><span data-stu-id="ec349-138">compile</span></span> | <span data-ttu-id="ec349-139">Zawartość `lib` folderu</span><span class="sxs-lookup"><span data-stu-id="ec349-139">Contents of the `lib` folder</span></span> |
| <span data-ttu-id="ec349-140">środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="ec349-140">runtime</span></span> | <span data-ttu-id="ec349-141">Zawartość `runtime` folderu</span><span class="sxs-lookup"><span data-stu-id="ec349-141">Contents of the `runtime` folder</span></span> |
| <span data-ttu-id="ec349-142">Pliki</span><span class="sxs-lookup"><span data-stu-id="ec349-142">contentFiles</span></span> | <span data-ttu-id="ec349-143">Zawartość `contentfiles` folderu</span><span class="sxs-lookup"><span data-stu-id="ec349-143">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="ec349-144">kompilacja</span><span class="sxs-lookup"><span data-stu-id="ec349-144">build</span></span> | <span data-ttu-id="ec349-145">Właściwości i elementów docelowych w `build` folderu</span><span class="sxs-lookup"><span data-stu-id="ec349-145">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="ec349-146">Analizatory</span><span class="sxs-lookup"><span data-stu-id="ec349-146">analyzers</span></span> | <span data-ttu-id="ec349-147">Analizatory .NET</span><span class="sxs-lookup"><span data-stu-id="ec349-147">.NET analyzers</span></span> |
| <span data-ttu-id="ec349-148">natywne</span><span class="sxs-lookup"><span data-stu-id="ec349-148">native</span></span> | <span data-ttu-id="ec349-149">Zawartość `native` folderu</span><span class="sxs-lookup"><span data-stu-id="ec349-149">Contents of the `native` folder</span></span> |
| <span data-ttu-id="ec349-150">brak</span><span class="sxs-lookup"><span data-stu-id="ec349-150">none</span></span> | <span data-ttu-id="ec349-151">Żadne z powyższych są używane.</span><span class="sxs-lookup"><span data-stu-id="ec349-151">None of the above are used.</span></span> |
| <span data-ttu-id="ec349-152">wszystkie</span><span class="sxs-lookup"><span data-stu-id="ec349-152">all</span></span> | <span data-ttu-id="ec349-153">Wszystkie powyższe (z wyjątkiem `none`)</span><span class="sxs-lookup"><span data-stu-id="ec349-153">All of the above (except `none`)</span></span> |

<span data-ttu-id="ec349-154">W poniższym przykładzie wszystkie elementy z wyjątkiem plików zawartości z pakietu może być zużyte przez projekt i wszystkie elementy z wyjątkiem plików zawartości i analizatorów będą przepływać do projektu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="ec349-154">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="ec349-155">Należy pamiętać, że ponieważ `build` nie wchodzi z `PrivateAssets`, elementów docelowych i właściwości *będzie* przepływu projektu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="ec349-155">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="ec349-156">Należy wziąć pod uwagę, na przykład, że powyższe odwołania jest używana w projekt, który tworzy pakiet NuGet o nazwie AppLogger.</span><span class="sxs-lookup"><span data-stu-id="ec349-156">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="ec349-157">Cele i właściwości, z jaką może wykorzystać AppLogger `Contoso.Utility.UsefulStuff`, jak można projektów używające AppLogger.</span><span class="sxs-lookup"><span data-stu-id="ec349-157">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="ec349-158">Dodawanie warunku PackageReference</span><span class="sxs-lookup"><span data-stu-id="ec349-158">Adding a PackageReference condition</span></span>

<span data-ttu-id="ec349-159">W przypadku użycia warunku do formantu, czy pakiet jest uwzględnione, których warunki, można użyć dowolnej zmiennej MSBuild lub zmienna zdefiniowana w pliku elementów docelowych lub właściwości.</span><span class="sxs-lookup"><span data-stu-id="ec349-159">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="ec349-160">Jednak w chwili obecnej tylko `TargetFramework` zmiennej jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="ec349-160">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="ec349-161">Na przykład docelowych `netstandard1.4` oraz `net452` , ale ma zależność, która ma zastosowanie tylko do `net452`.</span><span class="sxs-lookup"><span data-stu-id="ec349-161">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="ec349-162">W takim przypadku nie mają `netstandard1.4` projektu, który zużywa pakietu, aby dodać Zależność ta niepotrzebne.</span><span class="sxs-lookup"><span data-stu-id="ec349-162">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="ec349-163">Aby tego uniknąć, należy określić warunek na `PackageReference` w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ec349-163">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />    
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="ec349-164">Pakiet, który został utworzony przy użyciu tego projektu zostanie pokazują, że Newtonsoft.json jest uwzględniona jako zależności tylko w przypadku `net452` docelowych:</span><span class="sxs-lookup"><span data-stu-id="ec349-164">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![Wynik zastosowania warunek na PackageReference z VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="ec349-166">Warunki można stosować na `ItemGroup` poziomu i będą stosowane do wszystkich obiektów podrzędnych `PackageReference` elementy:</span><span class="sxs-lookup"><span data-stu-id="ec349-166">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
