---
title: Format NuGet PackageReference (odwołania do pakietu w plikach projektu)
description: Szczegółowe informacje o NuGet PackageReference w plikach projektu jako obsługiwany przez NuGet 4.0 +, VS2017 i .NET Core 2.0
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 8f277a8af7f988d6fdcfa75c43a10b3792c2ae22
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="19e33-103">Odwołania do pakietu (PackageReference) w plikach projektu</span><span class="sxs-lookup"><span data-stu-id="19e33-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="19e33-104">Pakiet odwołań, za pomocą `PackageReference` węzła, zarządzanie zależności NuGet bezpośrednio w ramach plików projektu (w przeciwieństwie do oddzielnej `packages.config` pliku).</span><span class="sxs-lookup"><span data-stu-id="19e33-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="19e33-105">Przy użyciu PackageReference, ponieważ jest ona wywoływana, nie ma wpływu na inne aspekty NuGet; na przykład ustawienia w `NuGet.Config` plików (w tym źródeł pakietów) nadal są stosowane zgodnie z objaśnieniem w [Konfigurowanie zachowania NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="19e33-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="19e33-106">Z PackageReference można również użyć warunki MSBuild do wybrania odwołania do pakietu dla platformy docelowej, konfiguracji, platformy lub inne grupy.</span><span class="sxs-lookup"><span data-stu-id="19e33-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="19e33-107">Umożliwia on również precyzyjną kontrolę nad zależności i zawartości przepływu.</span><span class="sxs-lookup"><span data-stu-id="19e33-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="19e33-108">(Aby uzyskać więcej informacji, zobacz [NuGet pakietu i ich przywracania docelowych elementów MSBuild](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="19e33-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="19e33-109">Domyślnie PackageReference jest używany dla platformy .NET Core projektów, .NET Standard projektów i projekty platformy UWP przeznaczonych dla systemu Windows 10 kompilacji 15063 (twórców aktualizacji), a później, z wyjątkiem projektów C++ platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="19e33-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="19e33-110">Projekty pełna platformy .NET obsługuje PackageReference, ale obecnie domyślnie `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="19e33-110">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="19e33-111">Aby użyć PackageReference, należy przeprowadzić migrację zależności z `packages.config` w pliku projektu, a następnie usuń pliku packages.config.</span><span class="sxs-lookup"><span data-stu-id="19e33-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="19e33-112">Dodawanie PackageReference</span><span class="sxs-lookup"><span data-stu-id="19e33-112">Adding a PackageReference</span></span>

<span data-ttu-id="19e33-113">Dodawanie zależności w pliku projektu, używając następującej składni:</span><span class="sxs-lookup"><span data-stu-id="19e33-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="19e33-114">Kontrolowanie wersję zależności</span><span class="sxs-lookup"><span data-stu-id="19e33-114">Controlling dependency version</span></span>

<span data-ttu-id="19e33-115">Konwencja określania wersji pakietu jest taka sama jak przy użyciu `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="19e33-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="19e33-116">W powyższym przykładzie 3.6.0 oznacza dowolną wersję, którą jest > = 3.6.0, z preferencją dla Najniższa wersja zgodnie z opisem na [wersji pakietu](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="19e33-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="19e33-117">Liczby zmiennoprzecinkowe wersji</span><span class="sxs-lookup"><span data-stu-id="19e33-117">Floating Versions</span></span>

<span data-ttu-id="19e33-118">[Liczby zmiennoprzecinkowe wersji](../consume-packages/dependency-resolution.md#floating-versions) są obsługiwane z `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="19e33-118">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="19e33-119">Kontrolowanie zależności zasobów</span><span class="sxs-lookup"><span data-stu-id="19e33-119">Controlling dependency assets</span></span>

<span data-ttu-id="19e33-120">Mogą używać zależność wyłącznie jako kontroler programowanie i może nie należy udostępniać który do projektów, które będą korzystać z pakietu.</span><span class="sxs-lookup"><span data-stu-id="19e33-120">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="19e33-121">W tym scenariuszu można użyć `PrivateAssets` metadanych do kontroli tego zachowania.</span><span class="sxs-lookup"><span data-stu-id="19e33-121">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="19e33-122">Następujących tagów metadanych kontrolować zależności zasobów:</span><span class="sxs-lookup"><span data-stu-id="19e33-122">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="19e33-123">Tag</span><span class="sxs-lookup"><span data-stu-id="19e33-123">Tag</span></span> | <span data-ttu-id="19e33-124">Opis</span><span class="sxs-lookup"><span data-stu-id="19e33-124">Description</span></span> | <span data-ttu-id="19e33-125">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="19e33-125">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19e33-126">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="19e33-126">IncludeAssets</span></span> | <span data-ttu-id="19e33-127">Te zasoby będą używane.</span><span class="sxs-lookup"><span data-stu-id="19e33-127">These assets will be consumed</span></span> | <span data-ttu-id="19e33-128">wszystkie</span><span class="sxs-lookup"><span data-stu-id="19e33-128">all</span></span> |
| <span data-ttu-id="19e33-129">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="19e33-129">ExcludeAssets</span></span> | <span data-ttu-id="19e33-130">Te zasoby nie będą używane.</span><span class="sxs-lookup"><span data-stu-id="19e33-130">These assets will not be consumed</span></span> | <span data-ttu-id="19e33-131">brak</span><span class="sxs-lookup"><span data-stu-id="19e33-131">none</span></span> |
| <span data-ttu-id="19e33-132">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="19e33-132">PrivateAssets</span></span> | <span data-ttu-id="19e33-133">Te zasoby będą działały, ale nie będą przepływać do projektu nadrzędnego</span><span class="sxs-lookup"><span data-stu-id="19e33-133">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="19e33-134">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="19e33-134">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="19e33-135">Dopuszczalne wartości tych tagów są następujące, z wieloma wartościami oddzielone średnikami z wyjątkiem z `all` i `none` której musi występować samodzielnie:</span><span class="sxs-lookup"><span data-stu-id="19e33-135">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="19e33-136">Wartość</span><span class="sxs-lookup"><span data-stu-id="19e33-136">Value</span></span> | <span data-ttu-id="19e33-137">Opis</span><span class="sxs-lookup"><span data-stu-id="19e33-137">Description</span></span> |
| --- | ---
| <span data-ttu-id="19e33-138">Kompilacji</span><span class="sxs-lookup"><span data-stu-id="19e33-138">compile</span></span> | <span data-ttu-id="19e33-139">Zawartość `lib` folder i formanty czy projektu można kompilować z zestawów znajdujących się w folderze</span><span class="sxs-lookup"><span data-stu-id="19e33-139">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="19e33-140">środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="19e33-140">runtime</span></span> | <span data-ttu-id="19e33-141">Zawartość `lib` i `runtimes` folder i formanty czy te zestawy będzie kopiowana do kompilacji output katalogu</span><span class="sxs-lookup"><span data-stu-id="19e33-141">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="19e33-142">Pliki</span><span class="sxs-lookup"><span data-stu-id="19e33-142">contentFiles</span></span> | <span data-ttu-id="19e33-143">Zawartość `contentfiles` folderu</span><span class="sxs-lookup"><span data-stu-id="19e33-143">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="19e33-144">kompilacja</span><span class="sxs-lookup"><span data-stu-id="19e33-144">build</span></span> | <span data-ttu-id="19e33-145">Właściwości i elementów docelowych w `build` folderu</span><span class="sxs-lookup"><span data-stu-id="19e33-145">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="19e33-146">Analizatory</span><span class="sxs-lookup"><span data-stu-id="19e33-146">analyzers</span></span> | <span data-ttu-id="19e33-147">Analizatory .NET</span><span class="sxs-lookup"><span data-stu-id="19e33-147">.NET analyzers</span></span> |
| <span data-ttu-id="19e33-148">natywne</span><span class="sxs-lookup"><span data-stu-id="19e33-148">native</span></span> | <span data-ttu-id="19e33-149">Zawartość `native` folderu</span><span class="sxs-lookup"><span data-stu-id="19e33-149">Contents of the `native` folder</span></span> |
| <span data-ttu-id="19e33-150">brak</span><span class="sxs-lookup"><span data-stu-id="19e33-150">none</span></span> | <span data-ttu-id="19e33-151">Żadne z powyższych są używane.</span><span class="sxs-lookup"><span data-stu-id="19e33-151">None of the above are used.</span></span> |
| <span data-ttu-id="19e33-152">wszystkie</span><span class="sxs-lookup"><span data-stu-id="19e33-152">all</span></span> | <span data-ttu-id="19e33-153">Wszystkie powyższe (z wyjątkiem `none`)</span><span class="sxs-lookup"><span data-stu-id="19e33-153">All of the above (except `none`)</span></span> |

<span data-ttu-id="19e33-154">W poniższym przykładzie wszystkie elementy z wyjątkiem plików zawartości z pakietu może być zużyte przez projekt i wszystkie elementy z wyjątkiem plików zawartości i analizatorów będą przepływać do projektu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="19e33-154">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="19e33-155">Należy pamiętać, że ponieważ `build` nie wchodzi z `PrivateAssets`, elementów docelowych i właściwości *będzie* przepływu projektu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="19e33-155">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="19e33-156">Należy wziąć pod uwagę, na przykład, że powyższe odwołania jest używana w projekt, który tworzy pakiet NuGet o nazwie AppLogger.</span><span class="sxs-lookup"><span data-stu-id="19e33-156">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="19e33-157">Cele i właściwości, z jaką może wykorzystać AppLogger `Contoso.Utility.UsefulStuff`, jak można projektów używające AppLogger.</span><span class="sxs-lookup"><span data-stu-id="19e33-157">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="19e33-158">Dodawanie warunku PackageReference</span><span class="sxs-lookup"><span data-stu-id="19e33-158">Adding a PackageReference condition</span></span>

<span data-ttu-id="19e33-159">W przypadku użycia warunku do formantu, czy pakiet jest uwzględnione, których warunki, można użyć dowolnej zmiennej MSBuild lub zmienna zdefiniowana w pliku elementów docelowych lub właściwości.</span><span class="sxs-lookup"><span data-stu-id="19e33-159">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="19e33-160">Jednak w chwili obecnej tylko `TargetFramework` zmiennej jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="19e33-160">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="19e33-161">Na przykład docelowych `netstandard1.4` oraz `net452` , ale ma zależność, która ma zastosowanie tylko do `net452`.</span><span class="sxs-lookup"><span data-stu-id="19e33-161">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="19e33-162">W takim przypadku nie mają `netstandard1.4` projektu, który zużywa pakietu, aby dodać Zależność ta niepotrzebne.</span><span class="sxs-lookup"><span data-stu-id="19e33-162">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="19e33-163">Aby tego uniknąć, należy określić warunek na `PackageReference` w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="19e33-163">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="19e33-164">Pakiet, który został utworzony przy użyciu tego projektu zostanie pokazują, że Newtonsoft.json jest uwzględniona jako zależności tylko w przypadku `net452` docelowych:</span><span class="sxs-lookup"><span data-stu-id="19e33-164">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![Wynik zastosowania warunek na PackageReference z VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="19e33-166">Warunki można stosować na `ItemGroup` poziomu i będą stosowane do wszystkich obiektów podrzędnych `PackageReference` elementy:</span><span class="sxs-lookup"><span data-stu-id="19e33-166">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
