---
title: Format NuGet PackageReference (odwołania do pakietu w plikach projektu) | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Szczegółowe informacje o NuGet PackageReference w plikach projektu jako obsługiwany przez NuGet 4.0 +, VS2017 i .NET Core 2.0
keywords: NuGet package dependencies, package references, project files, PackageReference, packages.config, VS2017, Visual Studio 2017, NuGet 4, .NET Core 2.0
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 99caf371ca1bd85e6af4e879741e3e2caab6e860
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="558bf-104">Odwołania do pakietu (PackageReference) w plikach projektu</span><span class="sxs-lookup"><span data-stu-id="558bf-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="558bf-105">Pakiet odwołań, za pomocą `PackageReference` węzła, zarządzanie zależności NuGet bezpośrednio w ramach plików projektu (w przeciwieństwie do oddzielnej `packages.config` pliku).</span><span class="sxs-lookup"><span data-stu-id="558bf-105">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="558bf-106">Przy użyciu PackageReference, ponieważ jest ona wywoływana, nie ma wpływu na inne aspekty NuGet; na przykład ustawienia w `NuGet.Config` plików (w tym źródeł pakietów) nadal są stosowane zgodnie z objaśnieniem w [Konfigurowanie zachowania NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="558bf-106">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="558bf-107">Z PackageReference można również użyć warunki MSBuild do wybrania odwołania do pakietu dla platformy docelowej, konfiguracji, platformy lub inne grupy.</span><span class="sxs-lookup"><span data-stu-id="558bf-107">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="558bf-108">Umożliwia on również precyzyjną kontrolę nad zależności i zawartości przepływu.</span><span class="sxs-lookup"><span data-stu-id="558bf-108">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="558bf-109">(Aby uzyskać więcej informacji, zobacz [NuGet pakietu i ich przywracania docelowych elementów MSBuild](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="558bf-109">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="558bf-110">Domyślnie PackageReference jest używany dla platformy .NET Core projektów, .NET Standard projektów i projekty platformy UWP przeznaczonych dla systemu Windows 10 kompilacji 15063 (twórców aktualizacji), a później, z wyjątkiem projektów C++ platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="558bf-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="558bf-111">Projekty pełna platformy .NET obsługuje PackageReference, ale obecnie domyślnie `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="558bf-111">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="558bf-112">Aby użyć PackageReference, należy przeprowadzić migrację zależności z `packages.config` w pliku projektu, a następnie usuń pliku packages.config.</span><span class="sxs-lookup"><span data-stu-id="558bf-112">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="558bf-113">Dodawanie PackageReference</span><span class="sxs-lookup"><span data-stu-id="558bf-113">Adding a PackageReference</span></span>

<span data-ttu-id="558bf-114">Dodawanie zależności w pliku projektu, używając następującej składni:</span><span class="sxs-lookup"><span data-stu-id="558bf-114">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="558bf-115">Kontrolowanie wersję zależności</span><span class="sxs-lookup"><span data-stu-id="558bf-115">Controlling dependency version</span></span>

<span data-ttu-id="558bf-116">Konwencja określania wersji pakietu jest taka sama jak przy użyciu `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="558bf-116">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="558bf-117">W powyższym przykładzie 3.6.0 oznacza dowolną wersję, którą jest > = 3.6.0, z preferencją dla Najniższa wersja zgodnie z opisem na [wersji pakietu](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="558bf-117">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="558bf-118">Liczby zmiennoprzecinkowe wersji</span><span class="sxs-lookup"><span data-stu-id="558bf-118">Floating Versions</span></span>

<span data-ttu-id="558bf-119">[Liczby zmiennoprzecinkowe wersji](../consume-packages/dependency-resolution.md#floating-versions) są obsługiwane z `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="558bf-119">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="558bf-120">Kontrolowanie zależności zasobów</span><span class="sxs-lookup"><span data-stu-id="558bf-120">Controlling dependency assets</span></span>

<span data-ttu-id="558bf-121">Mogą używać zależność wyłącznie jako kontroler programowanie i może nie należy udostępniać który do projektów, które będą korzystać z pakietu.</span><span class="sxs-lookup"><span data-stu-id="558bf-121">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="558bf-122">W tym scenariuszu można użyć `PrivateAssets` metadanych do kontroli tego zachowania.</span><span class="sxs-lookup"><span data-stu-id="558bf-122">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="558bf-123">Następujących tagów metadanych kontrolować zależności zasobów:</span><span class="sxs-lookup"><span data-stu-id="558bf-123">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="558bf-124">Tag</span><span class="sxs-lookup"><span data-stu-id="558bf-124">Tag</span></span> | <span data-ttu-id="558bf-125">Opis</span><span class="sxs-lookup"><span data-stu-id="558bf-125">Description</span></span> | <span data-ttu-id="558bf-126">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="558bf-126">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="558bf-127">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="558bf-127">IncludeAssets</span></span> | <span data-ttu-id="558bf-128">Te zasoby będą używane.</span><span class="sxs-lookup"><span data-stu-id="558bf-128">These assets will be consumed</span></span> | <span data-ttu-id="558bf-129">wszystkie</span><span class="sxs-lookup"><span data-stu-id="558bf-129">all</span></span> |
| <span data-ttu-id="558bf-130">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="558bf-130">ExcludeAssets</span></span> | <span data-ttu-id="558bf-131">Te zasoby nie będą używane.</span><span class="sxs-lookup"><span data-stu-id="558bf-131">These assets will not be consumed</span></span> | <span data-ttu-id="558bf-132">brak</span><span class="sxs-lookup"><span data-stu-id="558bf-132">none</span></span> |
| <span data-ttu-id="558bf-133">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="558bf-133">PrivateAssets</span></span> | <span data-ttu-id="558bf-134">Te zasoby będą działały, ale nie będą przepływać do projektu nadrzędnego</span><span class="sxs-lookup"><span data-stu-id="558bf-134">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="558bf-135">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="558bf-135">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="558bf-136">Dopuszczalne wartości tych tagów są następujące, z wieloma wartościami oddzielone średnikami z wyjątkiem z `all` i `none` której musi występować samodzielnie:</span><span class="sxs-lookup"><span data-stu-id="558bf-136">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="558bf-137">Wartość</span><span class="sxs-lookup"><span data-stu-id="558bf-137">Value</span></span> | <span data-ttu-id="558bf-138">Opis</span><span class="sxs-lookup"><span data-stu-id="558bf-138">Description</span></span> |
| --- | ---
| <span data-ttu-id="558bf-139">Kompilacji</span><span class="sxs-lookup"><span data-stu-id="558bf-139">compile</span></span> | <span data-ttu-id="558bf-140">Zawartość `lib` folderu</span><span class="sxs-lookup"><span data-stu-id="558bf-140">Contents of the `lib` folder</span></span> |
| <span data-ttu-id="558bf-141">środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="558bf-141">runtime</span></span> | <span data-ttu-id="558bf-142">Zawartość `runtimes` folderu</span><span class="sxs-lookup"><span data-stu-id="558bf-142">Contents of the `runtimes` folder</span></span> |
| <span data-ttu-id="558bf-143">Pliki</span><span class="sxs-lookup"><span data-stu-id="558bf-143">contentFiles</span></span> | <span data-ttu-id="558bf-144">Zawartość `contentfiles` folderu</span><span class="sxs-lookup"><span data-stu-id="558bf-144">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="558bf-145">kompilacja</span><span class="sxs-lookup"><span data-stu-id="558bf-145">build</span></span> | <span data-ttu-id="558bf-146">Właściwości i elementów docelowych w `build` folderu</span><span class="sxs-lookup"><span data-stu-id="558bf-146">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="558bf-147">Analizatory</span><span class="sxs-lookup"><span data-stu-id="558bf-147">analyzers</span></span> | <span data-ttu-id="558bf-148">Analizatory .NET</span><span class="sxs-lookup"><span data-stu-id="558bf-148">.NET analyzers</span></span> |
| <span data-ttu-id="558bf-149">natywne</span><span class="sxs-lookup"><span data-stu-id="558bf-149">native</span></span> | <span data-ttu-id="558bf-150">Zawartość `native` folderu</span><span class="sxs-lookup"><span data-stu-id="558bf-150">Contents of the `native` folder</span></span> |
| <span data-ttu-id="558bf-151">brak</span><span class="sxs-lookup"><span data-stu-id="558bf-151">none</span></span> | <span data-ttu-id="558bf-152">Żadne z powyższych są używane.</span><span class="sxs-lookup"><span data-stu-id="558bf-152">None of the above are used.</span></span> |
| <span data-ttu-id="558bf-153">wszystkie</span><span class="sxs-lookup"><span data-stu-id="558bf-153">all</span></span> | <span data-ttu-id="558bf-154">Wszystkie powyższe (z wyjątkiem `none`)</span><span class="sxs-lookup"><span data-stu-id="558bf-154">All of the above (except `none`)</span></span> |

<span data-ttu-id="558bf-155">W poniższym przykładzie wszystkie elementy z wyjątkiem plików zawartości z pakietu może być zużyte przez projekt i wszystkie elementy z wyjątkiem plików zawartości i analizatorów będą przepływać do projektu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="558bf-155">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="558bf-156">Należy pamiętać, że ponieważ `build` nie wchodzi z `PrivateAssets`, elementów docelowych i właściwości *będzie* przepływu projektu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="558bf-156">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="558bf-157">Należy wziąć pod uwagę, na przykład, że powyższe odwołania jest używana w projekt, który tworzy pakiet NuGet o nazwie AppLogger.</span><span class="sxs-lookup"><span data-stu-id="558bf-157">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="558bf-158">Cele i właściwości, z jaką może wykorzystać AppLogger `Contoso.Utility.UsefulStuff`, jak można projektów używające AppLogger.</span><span class="sxs-lookup"><span data-stu-id="558bf-158">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="558bf-159">Dodawanie warunku PackageReference</span><span class="sxs-lookup"><span data-stu-id="558bf-159">Adding a PackageReference condition</span></span>

<span data-ttu-id="558bf-160">W przypadku użycia warunku do formantu, czy pakiet jest uwzględnione, których warunki, można użyć dowolnej zmiennej MSBuild lub zmienna zdefiniowana w pliku elementów docelowych lub właściwości.</span><span class="sxs-lookup"><span data-stu-id="558bf-160">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="558bf-161">Jednak w chwili obecnej tylko `TargetFramework` zmiennej jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="558bf-161">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="558bf-162">Na przykład docelowych `netstandard1.4` oraz `net452` , ale ma zależność, która ma zastosowanie tylko do `net452`.</span><span class="sxs-lookup"><span data-stu-id="558bf-162">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="558bf-163">W takim przypadku nie mają `netstandard1.4` projektu, który zużywa pakietu, aby dodać Zależność ta niepotrzebne.</span><span class="sxs-lookup"><span data-stu-id="558bf-163">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="558bf-164">Aby tego uniknąć, należy określić warunek na `PackageReference` w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="558bf-164">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="558bf-165">Pakiet, który został utworzony przy użyciu tego projektu zostanie pokazują, że Newtonsoft.json jest uwzględniona jako zależności tylko w przypadku `net452` docelowych:</span><span class="sxs-lookup"><span data-stu-id="558bf-165">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![Wynik zastosowania warunek na PackageReference z VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="558bf-167">Warunki można stosować na `ItemGroup` poziomu i będą stosowane do wszystkich obiektów podrzędnych `PackageReference` elementy:</span><span class="sxs-lookup"><span data-stu-id="558bf-167">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
