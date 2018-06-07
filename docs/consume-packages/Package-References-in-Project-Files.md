---
title: Format NuGet PackageReference (odwołania do pakietu w plikach projektu)
description: Szczegółowe informacje o NuGet PackageReference w plikach projektu jako obsługiwany przez NuGet 4.0 +, VS2017 i .NET Core 2.0
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 61f447877459764906cf9a2b88b32a8bc0553689
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817674"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="a301c-103">Odwołania do pakietu (PackageReference) w plikach projektu</span><span class="sxs-lookup"><span data-stu-id="a301c-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="a301c-104">Pakiet odwołań, za pomocą `PackageReference` węzła, zarządzanie zależności NuGet bezpośrednio w ramach plików projektu (w przeciwieństwie do oddzielnej `packages.config` pliku).</span><span class="sxs-lookup"><span data-stu-id="a301c-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="a301c-105">Przy użyciu PackageReference, ponieważ jest ona wywoływana, nie ma wpływu na inne aspekty NuGet; na przykład ustawienia w `NuGet.Config` plików (w tym źródeł pakietów) nadal są stosowane zgodnie z objaśnieniem w [Konfigurowanie zachowania NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="a301c-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="a301c-106">Z PackageReference można również użyć warunki MSBuild do wybrania odwołania do pakietu dla platformy docelowej, konfiguracji, platformy lub inne grupy.</span><span class="sxs-lookup"><span data-stu-id="a301c-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="a301c-107">Umożliwia on również precyzyjną kontrolę nad zależności i zawartości przepływu.</span><span class="sxs-lookup"><span data-stu-id="a301c-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="a301c-108">(Aby uzyskać więcej informacji, zobacz [NuGet pakietu i ich przywracania docelowych elementów MSBuild](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="a301c-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="a301c-109">Domyślnie PackageReference jest używany dla platformy .NET Core projektów, .NET Standard projektów i projekty platformy UWP przeznaczonych dla systemu Windows 10 kompilacji 15063 (twórców aktualizacji), a później, z wyjątkiem projektów C++ platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="a301c-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="a301c-110">Projekty pełna platformy .NET obsługuje PackageReference, ale obecnie domyślnie `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="a301c-110">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="a301c-111">Aby użyć PackageReference, należy przeprowadzić migrację zależności z `packages.config` w pliku projektu, a następnie usuń pliku packages.config.</span><span class="sxs-lookup"><span data-stu-id="a301c-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="a301c-112">Dodawanie PackageReference</span><span class="sxs-lookup"><span data-stu-id="a301c-112">Adding a PackageReference</span></span>

<span data-ttu-id="a301c-113">Dodawanie zależności w pliku projektu, używając następującej składni:</span><span class="sxs-lookup"><span data-stu-id="a301c-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="a301c-114">Kontrolowanie wersję zależności</span><span class="sxs-lookup"><span data-stu-id="a301c-114">Controlling dependency version</span></span>

<span data-ttu-id="a301c-115">Konwencja określania wersji pakietu jest taka sama jak przy użyciu `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="a301c-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="a301c-116">W powyższym przykładzie 3.6.0 oznacza dowolną wersję, którą jest > = 3.6.0, z preferencją dla Najniższa wersja zgodnie z opisem na [wersji pakietu](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="a301c-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="a301c-117">Przy użyciu PackageReference dla projektu z nie PackageReferences</span><span class="sxs-lookup"><span data-stu-id="a301c-117">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="a301c-118">Zaawansowane: Jeśli nie pakietów zainstalowanych w projekcie (nie PackageReferences w pliku projektu), a nie pliku packages.config, ale mają projektu do przywrócenia jako styl PackageReference, można ustawić właściwości projektu RestoreProjectStyle do PackageReference w plik projektu.</span><span class="sxs-lookup"><span data-stu-id="a301c-118">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="a301c-119">Może to być przydatne, jeśli odwołanie projektów, które są PackageReference stylem (csproj istniejących lub projektów stylu zestawu SDK).</span><span class="sxs-lookup"><span data-stu-id="a301c-119">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="a301c-120">Umożliwi to pakiety, które projekty te dotyczą przywoływanie "przechodnie" w projekcie.</span><span class="sxs-lookup"><span data-stu-id="a301c-120">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="a301c-121">Liczby zmiennoprzecinkowe wersji</span><span class="sxs-lookup"><span data-stu-id="a301c-121">Floating Versions</span></span>

<span data-ttu-id="a301c-122">[Liczby zmiennoprzecinkowe wersji](../consume-packages/dependency-resolution.md#floating-versions) są obsługiwane z `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="a301c-122">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="a301c-123">Kontrolowanie zależności zasobów</span><span class="sxs-lookup"><span data-stu-id="a301c-123">Controlling dependency assets</span></span>

<span data-ttu-id="a301c-124">Mogą używać zależność wyłącznie jako kontroler programowanie i może nie należy udostępniać który do projektów, które będą korzystać z pakietu.</span><span class="sxs-lookup"><span data-stu-id="a301c-124">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="a301c-125">W tym scenariuszu można użyć `PrivateAssets` metadanych do kontroli tego zachowania.</span><span class="sxs-lookup"><span data-stu-id="a301c-125">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="a301c-126">Następujących tagów metadanych kontrolować zależności zasobów:</span><span class="sxs-lookup"><span data-stu-id="a301c-126">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="a301c-127">Tag</span><span class="sxs-lookup"><span data-stu-id="a301c-127">Tag</span></span> | <span data-ttu-id="a301c-128">Opis</span><span class="sxs-lookup"><span data-stu-id="a301c-128">Description</span></span> | <span data-ttu-id="a301c-129">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="a301c-129">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a301c-130">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="a301c-130">IncludeAssets</span></span> | <span data-ttu-id="a301c-131">Te zasoby będą używane.</span><span class="sxs-lookup"><span data-stu-id="a301c-131">These assets will be consumed</span></span> | <span data-ttu-id="a301c-132">wszystkie</span><span class="sxs-lookup"><span data-stu-id="a301c-132">all</span></span> |
| <span data-ttu-id="a301c-133">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="a301c-133">ExcludeAssets</span></span> | <span data-ttu-id="a301c-134">Te zasoby nie będą używane.</span><span class="sxs-lookup"><span data-stu-id="a301c-134">These assets will not be consumed</span></span> | <span data-ttu-id="a301c-135">brak</span><span class="sxs-lookup"><span data-stu-id="a301c-135">none</span></span> |
| <span data-ttu-id="a301c-136">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="a301c-136">PrivateAssets</span></span> | <span data-ttu-id="a301c-137">Te zasoby będą działały, ale nie będą przepływać do projektu nadrzędnego</span><span class="sxs-lookup"><span data-stu-id="a301c-137">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="a301c-138">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="a301c-138">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="a301c-139">Dopuszczalne wartości tych tagów są następujące, z wieloma wartościami oddzielone średnikami z wyjątkiem z `all` i `none` której musi występować samodzielnie:</span><span class="sxs-lookup"><span data-stu-id="a301c-139">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="a301c-140">Wartość</span><span class="sxs-lookup"><span data-stu-id="a301c-140">Value</span></span> | <span data-ttu-id="a301c-141">Opis</span><span class="sxs-lookup"><span data-stu-id="a301c-141">Description</span></span> |
| --- | ---
| <span data-ttu-id="a301c-142">Kompilacji</span><span class="sxs-lookup"><span data-stu-id="a301c-142">compile</span></span> | <span data-ttu-id="a301c-143">Zawartość `lib` folder i formanty czy projektu można kompilować z zestawów znajdujących się w folderze</span><span class="sxs-lookup"><span data-stu-id="a301c-143">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="a301c-144">środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="a301c-144">runtime</span></span> | <span data-ttu-id="a301c-145">Zawartość `lib` i `runtimes` folder i formanty czy te zestawy będzie kopiowana do kompilacji output katalogu</span><span class="sxs-lookup"><span data-stu-id="a301c-145">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="a301c-146">Pliki</span><span class="sxs-lookup"><span data-stu-id="a301c-146">contentFiles</span></span> | <span data-ttu-id="a301c-147">Zawartość `contentfiles` folderu</span><span class="sxs-lookup"><span data-stu-id="a301c-147">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="a301c-148">kompilacja</span><span class="sxs-lookup"><span data-stu-id="a301c-148">build</span></span> | <span data-ttu-id="a301c-149">Właściwości i elementów docelowych w `build` folderu</span><span class="sxs-lookup"><span data-stu-id="a301c-149">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="a301c-150">Analizatory</span><span class="sxs-lookup"><span data-stu-id="a301c-150">analyzers</span></span> | <span data-ttu-id="a301c-151">Analizatory .NET</span><span class="sxs-lookup"><span data-stu-id="a301c-151">.NET analyzers</span></span> |
| <span data-ttu-id="a301c-152">natywne</span><span class="sxs-lookup"><span data-stu-id="a301c-152">native</span></span> | <span data-ttu-id="a301c-153">Zawartość `native` folderu</span><span class="sxs-lookup"><span data-stu-id="a301c-153">Contents of the `native` folder</span></span> |
| <span data-ttu-id="a301c-154">brak</span><span class="sxs-lookup"><span data-stu-id="a301c-154">none</span></span> | <span data-ttu-id="a301c-155">Żadne z powyższych są używane.</span><span class="sxs-lookup"><span data-stu-id="a301c-155">None of the above are used.</span></span> |
| <span data-ttu-id="a301c-156">wszystkie</span><span class="sxs-lookup"><span data-stu-id="a301c-156">all</span></span> | <span data-ttu-id="a301c-157">Wszystkie powyższe (z wyjątkiem `none`)</span><span class="sxs-lookup"><span data-stu-id="a301c-157">All of the above (except `none`)</span></span> |

<span data-ttu-id="a301c-158">W poniższym przykładzie wszystkie elementy z wyjątkiem plików zawartości z pakietu może być zużyte przez projekt i wszystkie elementy z wyjątkiem plików zawartości i analizatorów będą przepływać do projektu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="a301c-158">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="a301c-159">Należy pamiętać, że ponieważ `build` nie wchodzi z `PrivateAssets`, elementów docelowych i właściwości *będzie* przepływu projektu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="a301c-159">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="a301c-160">Należy wziąć pod uwagę, na przykład, że powyższe odwołania jest używana w projekt, który tworzy pakiet NuGet o nazwie AppLogger.</span><span class="sxs-lookup"><span data-stu-id="a301c-160">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="a301c-161">Cele i właściwości, z jaką może wykorzystać AppLogger `Contoso.Utility.UsefulStuff`, jak można projektów używające AppLogger.</span><span class="sxs-lookup"><span data-stu-id="a301c-161">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="a301c-162">Dodawanie warunku PackageReference</span><span class="sxs-lookup"><span data-stu-id="a301c-162">Adding a PackageReference condition</span></span>

<span data-ttu-id="a301c-163">W przypadku użycia warunku do formantu, czy pakiet jest uwzględnione, których warunki, można użyć dowolnej zmiennej MSBuild lub zmienna zdefiniowana w pliku elementów docelowych lub właściwości.</span><span class="sxs-lookup"><span data-stu-id="a301c-163">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="a301c-164">Jednak w chwili obecnej tylko `TargetFramework` zmiennej jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="a301c-164">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="a301c-165">Na przykład docelowych `netstandard1.4` oraz `net452` , ale ma zależność, która ma zastosowanie tylko do `net452`.</span><span class="sxs-lookup"><span data-stu-id="a301c-165">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="a301c-166">W takim przypadku nie mają `netstandard1.4` projektu, który zużywa pakietu, aby dodać Zależność ta niepotrzebne.</span><span class="sxs-lookup"><span data-stu-id="a301c-166">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="a301c-167">Aby tego uniknąć, należy określić warunek na `PackageReference` w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a301c-167">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="a301c-168">Pakiet, który został utworzony przy użyciu tego projektu zostanie pokazują, że Newtonsoft.json jest uwzględniona jako zależności tylko w przypadku `net452` docelowych:</span><span class="sxs-lookup"><span data-stu-id="a301c-168">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![Wynik zastosowania warunek na PackageReference z VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="a301c-170">Warunki można stosować na `ItemGroup` poziomu i będą stosowane do wszystkich obiektów podrzędnych `PackageReference` elementy:</span><span class="sxs-lookup"><span data-stu-id="a301c-170">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
