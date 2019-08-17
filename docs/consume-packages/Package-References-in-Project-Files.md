---
title: Format PackageReference NuGet (odwołania do pakietów w plikach projektu)
description: Szczegóły dotyczące PackageReference NuGet w plikach projektu, które są obsługiwane przez narzędzia NuGet 4.0 + i program VS2017 i .NET Core 2,0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: ae80206117eed639140a0c7977043d8330bc37bb
ms.sourcegitcommit: 80cf99f40759911324468be1ec815c96aebf376d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/17/2019
ms.locfileid: "69564568"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="62b7d-103">Odwołania do pakietów (PackageReference) w plikach projektu</span><span class="sxs-lookup"><span data-stu-id="62b7d-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="62b7d-104">Odwołania do pakietów, używanie `PackageReference` węzła, zarządzanie zależnościami NuGet bezpośrednio w plikach projektu (w przeciwieństwie do oddzielnego `packages.config` pliku).</span><span class="sxs-lookup"><span data-stu-id="62b7d-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="62b7d-105">Przy użyciu PackageReference, gdy jest wywoływana, nie ma wpływu na inne aspekty NuGet; na przykład ustawienia w `NuGet.config` plikach (w tym źródła pakietów) są nadal stosowane, jak wyjaśniono w [typowych konfiguracjach NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="62b7d-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="62b7d-106">Za pomocą PackageReference można także użyć warunków MSBuild, aby wybrać odwołania do pakietów dla platformy docelowej, konfiguracji, platformy lub innych grup.</span><span class="sxs-lookup"><span data-stu-id="62b7d-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="62b7d-107">Umożliwia również precyzyjne sterowanie zależnościami i przepływem zawartości.</span><span class="sxs-lookup"><span data-stu-id="62b7d-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="62b7d-108">(Zobacz, aby uzyskać więcej szczegółów na temat [pakietu NuGet i przywracania jako elementy docelowe programu MSBuild](../reference/msbuild-targets.md)).</span><span class="sxs-lookup"><span data-stu-id="62b7d-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="62b7d-109">Obsługa typu projektu</span><span class="sxs-lookup"><span data-stu-id="62b7d-109">Project type support</span></span>

<span data-ttu-id="62b7d-110">Domyślnie PackageReference jest używany dla projektów .NET Core, projektów .NET Standard i projektów platformy UWP przeznaczonych dla systemu Windows 10 Build 15063 (Aktualizacja dla twórców) i nowszych, z wyjątkiem projektów C++ platformy UWP.</span><span class="sxs-lookup"><span data-stu-id="62b7d-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="62b7d-111">Projekty .NET Framework obsługują PackageReference, ale obecnie domyślnie `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="62b7d-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="62b7d-112">Aby użyć PackageReference, [Migruj](../consume-packages/migrate-packages-config-to-package-reference.md) zależności z `packages.config` do pliku projektu, a następnie usuń Packages. config.</span><span class="sxs-lookup"><span data-stu-id="62b7d-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="62b7d-113">ASP.NET aplikacje obsługujące pełną .NET Framework obejmują tylko [ograniczoną obsługę](https://github.com/NuGet/Home/issues/5877) PackageReference.</span><span class="sxs-lookup"><span data-stu-id="62b7d-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="62b7d-114">C++i typy projektów JavaScript nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="62b7d-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="62b7d-115">Dodawanie elementu PackageReference</span><span class="sxs-lookup"><span data-stu-id="62b7d-115">Adding a PackageReference</span></span>

<span data-ttu-id="62b7d-116">Dodaj zależność w pliku projektu przy użyciu następującej składni:</span><span class="sxs-lookup"><span data-stu-id="62b7d-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="62b7d-117">Kontrolowanie wersji zależności</span><span class="sxs-lookup"><span data-stu-id="62b7d-117">Controlling dependency version</span></span>

<span data-ttu-id="62b7d-118">Konwencja określania wersji pakietu jest taka sama jak w przypadku użycia `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="62b7d-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="62b7d-119">W powyższym przykładzie 3.6.0 oznacza dowolną wersję, która jest > = 3.6.0 z preferencją dla najniższej wersji, zgodnie z opisem w temacie [przechowywanie wersji pakietu](../concepts/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="62b7d-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="62b7d-120">Używanie PackageReference dla projektu bez składnika packagereferences</span><span class="sxs-lookup"><span data-stu-id="62b7d-120">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="62b7d-121">Doświadczonych Jeśli nie masz żadnych pakietów zainstalowanych w projekcie (nie składnika packagereferences w pliku projektu i bez pliku Packages. config), ale chcesz przywrócić projekt jako styl PackageReference, możesz ustawić właściwość projektu RestoreProjectStyle na PackageReference w projekcie rozszerzeniem.</span><span class="sxs-lookup"><span data-stu-id="62b7d-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="62b7d-122">Może to być przydatne, jeśli odwołują się do projektów, które są PackageReference w stylu (istniejące projekty csproj lub zestawu SDK).</span><span class="sxs-lookup"><span data-stu-id="62b7d-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="62b7d-123">Spowoduje to włączenie pakietów, do których odwołują się te projekty, do których odwołuje się projekt.</span><span class="sxs-lookup"><span data-stu-id="62b7d-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="62b7d-124">Wersje zmiennoprzecinkowe</span><span class="sxs-lookup"><span data-stu-id="62b7d-124">Floating Versions</span></span>

<span data-ttu-id="62b7d-125">[Wersje zmiennoprzecinkowe](../concepts/dependency-resolution.md#floating-versions) są obsługiwane `PackageReference`za pomocą:</span><span class="sxs-lookup"><span data-stu-id="62b7d-125">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="62b7d-126">Kontrolowanie zasobów zależności</span><span class="sxs-lookup"><span data-stu-id="62b7d-126">Controlling dependency assets</span></span>

<span data-ttu-id="62b7d-127">Można używać zależności wyłącznie jako zespołu programistycznego i może nie chcieć ujawniać projektów, które będą korzystać z pakietu.</span><span class="sxs-lookup"><span data-stu-id="62b7d-127">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="62b7d-128">W tym scenariuszu można użyć `PrivateAssets` metadanych do kontrolowania tego zachowania.</span><span class="sxs-lookup"><span data-stu-id="62b7d-128">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="62b7d-129">Następujące znaczniki metadanych kontrolują elementy zależne:</span><span class="sxs-lookup"><span data-stu-id="62b7d-129">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="62b7d-130">Tag</span><span class="sxs-lookup"><span data-stu-id="62b7d-130">Tag</span></span> | <span data-ttu-id="62b7d-131">Opis</span><span class="sxs-lookup"><span data-stu-id="62b7d-131">Description</span></span> | <span data-ttu-id="62b7d-132">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="62b7d-132">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="62b7d-133">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="62b7d-133">IncludeAssets</span></span> | <span data-ttu-id="62b7d-134">Te zasoby zostaną wykorzystane</span><span class="sxs-lookup"><span data-stu-id="62b7d-134">These assets will be consumed</span></span> | <span data-ttu-id="62b7d-135">wszystkie</span><span class="sxs-lookup"><span data-stu-id="62b7d-135">all</span></span> |
| <span data-ttu-id="62b7d-136">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="62b7d-136">ExcludeAssets</span></span> | <span data-ttu-id="62b7d-137">Te zasoby nie będą używane</span><span class="sxs-lookup"><span data-stu-id="62b7d-137">These assets will not be consumed</span></span> | <span data-ttu-id="62b7d-138">brak</span><span class="sxs-lookup"><span data-stu-id="62b7d-138">none</span></span> |
| <span data-ttu-id="62b7d-139">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="62b7d-139">PrivateAssets</span></span> | <span data-ttu-id="62b7d-140">Te zasoby będą wykorzystane, ale nie będą przepływać do projektu nadrzędnego</span><span class="sxs-lookup"><span data-stu-id="62b7d-140">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="62b7d-141">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="62b7d-141">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="62b7d-142">Wartości dozwolone dla tych tagów są następujące, z wieloma wartościami oddzielonymi średnikami z wyjątkiem `all` i `none` , które muszą być wyświetlane przez siebie:</span><span class="sxs-lookup"><span data-stu-id="62b7d-142">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="62b7d-143">Wartość</span><span class="sxs-lookup"><span data-stu-id="62b7d-143">Value</span></span> | <span data-ttu-id="62b7d-144">Opis</span><span class="sxs-lookup"><span data-stu-id="62b7d-144">Description</span></span> |
| --- | ---
| <span data-ttu-id="62b7d-145">opracowania</span><span class="sxs-lookup"><span data-stu-id="62b7d-145">compile</span></span> | <span data-ttu-id="62b7d-146">`lib` Zawartość folderu i kontroluje, czy projekt może być kompilowany względem zestawów w folderze</span><span class="sxs-lookup"><span data-stu-id="62b7d-146">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="62b7d-147">środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="62b7d-147">runtime</span></span> | <span data-ttu-id="62b7d-148">Zawartość folderu `runtimes` i i kontroluje, czy te zestawy zostaną skopiowane do katalogu wyjściowego kompilacji `lib`</span><span class="sxs-lookup"><span data-stu-id="62b7d-148">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="62b7d-149">contentFiles</span><span class="sxs-lookup"><span data-stu-id="62b7d-149">contentFiles</span></span> | <span data-ttu-id="62b7d-150">`contentfiles` Zawartość folderu</span><span class="sxs-lookup"><span data-stu-id="62b7d-150">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="62b7d-151">kompilacja</span><span class="sxs-lookup"><span data-stu-id="62b7d-151">build</span></span> | <span data-ttu-id="62b7d-152">`.props``.targets` i`build` w folderze</span><span class="sxs-lookup"><span data-stu-id="62b7d-152">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="62b7d-153">buildMultitargeting</span><span class="sxs-lookup"><span data-stu-id="62b7d-153">buildMultitargeting</span></span> | <span data-ttu-id="62b7d-154">*(4,0)* `.props` i `.targets` w`buildMultitargeting` folderze, dla celów określania wartości docelowej między platformami</span><span class="sxs-lookup"><span data-stu-id="62b7d-154">*(4.0)* `.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="62b7d-155">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="62b7d-155">buildTransitive</span></span> | <span data-ttu-id="62b7d-156">*(5.0 +)* `.props` i wfolderze`buildTransitive` , dla zasobów, które są przesyłane przechodniie do dowolnego, zużywanego projektu. `.targets`</span><span class="sxs-lookup"><span data-stu-id="62b7d-156">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="62b7d-157">Zobacz stronę [funkcji](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) .</span><span class="sxs-lookup"><span data-stu-id="62b7d-157">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="62b7d-158">Analizatory</span><span class="sxs-lookup"><span data-stu-id="62b7d-158">analyzers</span></span> | <span data-ttu-id="62b7d-159">Analizatory .NET</span><span class="sxs-lookup"><span data-stu-id="62b7d-159">.NET analyzers</span></span> |
| <span data-ttu-id="62b7d-160">natywne</span><span class="sxs-lookup"><span data-stu-id="62b7d-160">native</span></span> | <span data-ttu-id="62b7d-161">`native` Zawartość folderu</span><span class="sxs-lookup"><span data-stu-id="62b7d-161">Contents of the `native` folder</span></span> |
| <span data-ttu-id="62b7d-162">brak</span><span class="sxs-lookup"><span data-stu-id="62b7d-162">none</span></span> | <span data-ttu-id="62b7d-163">Żadne z powyższych nie jest używane.</span><span class="sxs-lookup"><span data-stu-id="62b7d-163">None of the above are used.</span></span> |
| <span data-ttu-id="62b7d-164">wszystkie</span><span class="sxs-lookup"><span data-stu-id="62b7d-164">all</span></span> | <span data-ttu-id="62b7d-165">Wszystkie powyższe (z wyjątkiem `none`)</span><span class="sxs-lookup"><span data-stu-id="62b7d-165">All of the above (except `none`)</span></span> |

<span data-ttu-id="62b7d-166">W poniższym przykładzie wszystko, z wyjątkiem plików zawartości z pakietu, będzie używane przez projekt, a wszystko z wyjątkiem plików zawartości i analizatorów przepływa do projektu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="62b7d-166">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="62b7d-167">Należy pamiętać, `build` że element targets `PrivateAssets`i props *będzie* przepływać do projektu nadrzędnego, ponieważ nie jest zawarty w elemencie.</span><span class="sxs-lookup"><span data-stu-id="62b7d-167">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="62b7d-168">Rozważmy na przykład, że odwołanie powyżej jest używane w projekcie, który kompiluje pakiet NuGet o nazwie AppLogger.</span><span class="sxs-lookup"><span data-stu-id="62b7d-168">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="62b7d-169">AppLogger może zużywać elementy docelowe i wartości z `Contoso.Utility.UsefulStuff`, jak w przypadku projektów, które zużywają AppLogger.</span><span class="sxs-lookup"><span data-stu-id="62b7d-169">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="62b7d-170">Gdy `developmentDependency` jest ustawiona na `true` w `.nuspec` pliku, oznacza to pakiet jako zależność tylko do programowania, co uniemożliwi uwzględnienie pakietu jako zależności w innych pakietach.</span><span class="sxs-lookup"><span data-stu-id="62b7d-170">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="62b7d-171">W przypadku PackageReference *(NuGet 4.8 +)* ta flaga oznacza również, że wykluczają się zasoby czasu kompilacji z kompilacji.</span><span class="sxs-lookup"><span data-stu-id="62b7d-171">With PackageReference *(NuGet 4.8+)*, this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="62b7d-172">Aby uzyskać więcej informacji, zobacz [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="62b7d-172">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="62b7d-173">Dodawanie warunku PackageReference</span><span class="sxs-lookup"><span data-stu-id="62b7d-173">Adding a PackageReference condition</span></span>

<span data-ttu-id="62b7d-174">Możesz użyć warunku, aby określić, czy pakiet jest uwzględniony, gdzie warunki mogą używać dowolnej zmiennej MSBuild lub zmiennej zdefiniowanej w pliku TARGETS lub props.</span><span class="sxs-lookup"><span data-stu-id="62b7d-174">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="62b7d-175">Jednak obecnie obsługiwana jest tylko `TargetFramework` zmienna.</span><span class="sxs-lookup"><span data-stu-id="62b7d-175">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="62b7d-176">Załóżmy na przykład, że jesteś elementem `netstandard1.4` docelowym, `net452` a także masz zależność, która ma zastosowanie tylko do `net452`.</span><span class="sxs-lookup"><span data-stu-id="62b7d-176">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="62b7d-177">W takim przypadku nie chcesz `netstandard1.4` , aby projekt zużywał pakiet, aby dodać niepotrzebną zależność.</span><span class="sxs-lookup"><span data-stu-id="62b7d-177">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="62b7d-178">Aby tego uniknąć, należy określić warunek w `PackageReference` następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="62b7d-178">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="62b7d-179">Pakiet utworzony przy użyciu tego projektu będzie przedstawiał, że Newtonsoft. JSON jest uwzględniany jako zależność tylko `net452` dla elementu docelowego:</span><span class="sxs-lookup"><span data-stu-id="62b7d-179">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Wynik zastosowania warunku na PackageReference z program VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="62b7d-181">Warunki mogą być również stosowane na `ItemGroup` poziomie i będą miały zastosowanie do wszystkich elementów podrzędnych: `PackageReference`</span><span class="sxs-lookup"><span data-stu-id="62b7d-181">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a><span data-ttu-id="62b7d-182">Blokowanie zależności</span><span class="sxs-lookup"><span data-stu-id="62b7d-182">Locking dependencies</span></span>
<span data-ttu-id="62b7d-183">*Ta funkcja jest dostępna w programie NuGet **4,9** lub nowszym oraz z programem Visual Studio 2017 **15,9** lub nowszym.*</span><span class="sxs-lookup"><span data-stu-id="62b7d-183">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="62b7d-184">Dane wejściowe do przywracania NuGet to zbiór odwołań do pakietów z pliku projektu (zależności najwyższego poziomu lub bezpośrednie), a dane wyjściowe to pełny zamknięcie wszystkich zależności pakietu, w tym zależności przechodnie.</span><span class="sxs-lookup"><span data-stu-id="62b7d-184">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="62b7d-185">Pakiet NuGet próbuje zawsze utworzyć to samo pełne zamknięcie zależności pakietów, jeśli lista wejściowa PackageReference nie została zmieniona.</span><span class="sxs-lookup"><span data-stu-id="62b7d-185">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="62b7d-186">Jednak istnieją pewne scenariusze, w których nie można tego zrobić.</span><span class="sxs-lookup"><span data-stu-id="62b7d-186">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="62b7d-187">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="62b7d-187">For example:</span></span>

* <span data-ttu-id="62b7d-188">W przypadku korzystania z wersji zmiennoprzecinkowych, takich jak `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span><span class="sxs-lookup"><span data-stu-id="62b7d-188">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="62b7d-189">Gdy zachodzi taka potrzeba, aby przepływać do najnowszej wersji przy każdym przywracaniu pakietów, istnieją scenariusze, w których użytkownicy wymagają, aby wykres był zablokowany do określonej najnowszej wersji i przepływał do nowszej wersji, o ile jest dostępny, przy jawnym gestie.</span><span class="sxs-lookup"><span data-stu-id="62b7d-189">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="62b7d-190">Opublikowana jest nowsza wersja pakietu spełniająca wymagania dotyczące wersji PackageReference.</span><span class="sxs-lookup"><span data-stu-id="62b7d-190">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="62b7d-191">Na przykład</span><span class="sxs-lookup"><span data-stu-id="62b7d-191">E.g.</span></span> 

  * <span data-ttu-id="62b7d-192">Dzień 1: Jeśli określono `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` , ale wersje dostępne w repozytoriach NuGet zostały 4.1.0, 4.2.0 i 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="62b7d-192">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="62b7d-193">W takim przypadku pakiet NuGet zostałby rozpoznany jako 4.1.0 (Najbliższa wersja minimalna)</span><span class="sxs-lookup"><span data-stu-id="62b7d-193">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="62b7d-194">Dzień 2: Wersja 4.0.0 zostaje opublikowana.</span><span class="sxs-lookup"><span data-stu-id="62b7d-194">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="62b7d-195">Pakiet NuGet znajdzie teraz dokładne dopasowanie i zacznie rozwiązywać 4.0.0</span><span class="sxs-lookup"><span data-stu-id="62b7d-195">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="62b7d-196">Dana wersja pakietu jest usuwana z repozytorium.</span><span class="sxs-lookup"><span data-stu-id="62b7d-196">A given package version is removed from the repository.</span></span> <span data-ttu-id="62b7d-197">Chociaż nuget.org nie zezwala na usuwanie pakietów, te ograniczenia nie są dostępne dla wszystkich repozytoriów pakietów.</span><span class="sxs-lookup"><span data-stu-id="62b7d-197">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="62b7d-198">Spowoduje to znalezienie najlepszego dopasowania przez pakiet NuGet, gdy nie można rozwiązać go do usuniętej wersji.</span><span class="sxs-lookup"><span data-stu-id="62b7d-198">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="62b7d-199">Włączanie pliku blokady</span><span class="sxs-lookup"><span data-stu-id="62b7d-199">Enabling lock file</span></span>
<span data-ttu-id="62b7d-200">W celu utrwalenia pełnego zamknięcia zależności pakietu można wybrać funkcję blokowania pliku przez ustawienie właściwości `RestorePackagesWithLockFile` MSBuild dla projektu:</span><span class="sxs-lookup"><span data-stu-id="62b7d-200">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="62b7d-201">Jeśli ta właściwość jest ustawiona, przywracanie NuGet wygeneruje `packages.lock.json` plik blokady pliku w katalogu głównym projektu, który zawiera listę wszystkich zależności pakietu.</span><span class="sxs-lookup"><span data-stu-id="62b7d-201">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="62b7d-202">Gdy projekt zawiera `packages.lock.json` plik w katalogu głównym, plik blokady jest zawsze używany z przywracaniem, nawet jeśli właściwość `RestorePackagesWithLockFile` nie jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="62b7d-202">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="62b7d-203">Innym sposobem na zgodę na tę funkcję jest utworzenie fikcyjnego pustego `packages.lock.json` pliku w katalogu głównym projektu.</span><span class="sxs-lookup"><span data-stu-id="62b7d-203">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="62b7d-204">`restore`zachowanie z plikiem blokady</span><span class="sxs-lookup"><span data-stu-id="62b7d-204">`restore` behavior with lock file</span></span>
<span data-ttu-id="62b7d-205">Jeśli plik blokady jest obecny dla projektu, NuGet używa tego pliku blokady do uruchomienia `restore`.</span><span class="sxs-lookup"><span data-stu-id="62b7d-205">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="62b7d-206">Program NuGet sprawdza, czy w zależnościach pakietu zostały wprowadzone jakiekolwiek zmiany, jak wspomniano w pliku projektu (lub w plikach projektów zależnych) i czy nie wprowadzono żadnych zmian, po prostu przywraca pakiety wymienione w pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="62b7d-206">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="62b7d-207">Nie ma potrzeby ponownej oceny zależności pakietów.</span><span class="sxs-lookup"><span data-stu-id="62b7d-207">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="62b7d-208">Jeśli NuGet wykryje zmianę zdefiniowanych zależności, jak wspomniano w plikach projektu, ponownie oblicza Graf pakietu i aktualizuje plik blokady w celu odzwierciedlenia nowego zamknięcia pakietu dla projektu.</span><span class="sxs-lookup"><span data-stu-id="62b7d-208">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="62b7d-209">W przypadku ciągłej integracji/ciągłego wdrażania i innych scenariuszy, w których nie chcesz zmienić zależności pakietu na bieżąco, możesz to zrobić, ustawiając `lockedmode` `true`następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="62b7d-209">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="62b7d-210">W przypadku programu dotnet. exe Uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="62b7d-210">For dotnet.exe, run:</span></span>
```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="62b7d-211">Dla programu MSBuild. exe Uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="62b7d-211">For msbuild.exe, run:</span></span>
```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="62b7d-212">Możesz również ustawić tę właściwość warunkowego programu MSBuild w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="62b7d-212">You may also set this conditional MSBuild property in your project file:</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="62b7d-213">W przypadku opcji Tryb `true`zablokowany przywracanie spowoduje przywrócenie dokładnych pakietów wymienionych w pliku blokady lub niepowodzenie w przypadku zaktualizowania zdefiniowanych zależności pakietu dla projektu po utworzeniu pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="62b7d-213">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="62b7d-214">Utwórz część pliku blokady w repozytorium źródłowym</span><span class="sxs-lookup"><span data-stu-id="62b7d-214">Make lock file part of your source repository</span></span>
<span data-ttu-id="62b7d-215">W przypadku kompilowania aplikacji plik wykonywalny i projekt w danym momencie znajdują się na początku łańcucha zależności, a następnie należy zaewidencjonować plik blokady do repozytorium kodu źródłowego, aby pakiet NuGet mógł go używać podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="62b7d-215">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="62b7d-216">Jeśli jednak projekt jest projektem biblioteki, który nie jest dostarczany lub wspólny projekt kodu, od którego zależą inne projekty, **nie należy** ewidencjonować pliku blokady jako części kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="62b7d-216">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="62b7d-217">Nie ma szkody w zachowaniu pliku blokady, ale zablokowane zależności pakietu dla wspólnego projektu kodu nie mogą być używane, jak wymieniono w pliku blokady podczas przywracania/kompilowania projektu, który zależy od tego projektu Common-Code.</span><span class="sxs-lookup"><span data-stu-id="62b7d-217">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="62b7d-218">Zwrotnym.</span><span class="sxs-lookup"><span data-stu-id="62b7d-218">Eg.</span></span>
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
<span data-ttu-id="62b7d-219">Jeśli `ProjectA` ma zależność `PackageX` od wersji `2.0.0` , a także odwołania `ProjectB` , `PackageX` `1.0.0` któresą`PackageX` zależne od wersji, plik blokady zostaniewystawionyzależnościod`ProjectB` wersja `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="62b7d-219">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="62b7d-220">Jednak `ProjectA` po skompilowaniu jego plik blokady będzie zawierał zależność od **`2.0.0`** `PackageX` wersji, a **nie** `1.0.0` tak jak na liście w pliku blokady dla `ProjectB`.</span><span class="sxs-lookup"><span data-stu-id="62b7d-220">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="62b7d-221">W ten sposób plik blokady wspólnego projektu kodu ma niewielki stan dla projektów, które są od niego zależne.</span><span class="sxs-lookup"><span data-stu-id="62b7d-221">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="62b7d-222">Zablokuj rozszerzalność plików</span><span class="sxs-lookup"><span data-stu-id="62b7d-222">Lock file extensibility</span></span>
<span data-ttu-id="62b7d-223">Można kontrolować różne zachowania przywracania za pomocą pliku blokady zgodnie z poniższym opisem:</span><span class="sxs-lookup"><span data-stu-id="62b7d-223">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="62b7d-224">Opcja</span><span class="sxs-lookup"><span data-stu-id="62b7d-224">Option</span></span> | <span data-ttu-id="62b7d-225">Odpowiednik opcji programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="62b7d-225">MSBuild equivalent option</span></span> | 
|:---  |:--- |
| `--use-lock-file` | <span data-ttu-id="62b7d-226">Użycie przez Bootstrap pliku blokady dla projektu.</span><span class="sxs-lookup"><span data-stu-id="62b7d-226">Bootstraps use of lock file for a project.</span></span> <span data-ttu-id="62b7d-227">Możesz Alternatywnie ustawić `RestorePackagesWithLockFile` właściwość w pliku projektu</span><span class="sxs-lookup"><span data-stu-id="62b7d-227">You can alternatively set `RestorePackagesWithLockFile` property in the project file</span></span> | 
| `--locked-mode` | <span data-ttu-id="62b7d-228">Włącza tryb zablokowany do przywracania.</span><span class="sxs-lookup"><span data-stu-id="62b7d-228">Enables locked mode for restore.</span></span> <span data-ttu-id="62b7d-229">Jest to przydatne w scenariuszach ciągłej integracji/ciągłego wdrażania.</span><span class="sxs-lookup"><span data-stu-id="62b7d-229">This is useful in CI/CD scenarios where you would like to get the repeatable builds.</span></span> <span data-ttu-id="62b7d-230">Może to być również ustawienie właściwości programu `RestoreLockedMode` MSBuild na`true`</span><span class="sxs-lookup"><span data-stu-id="62b7d-230">This can be also by setting the `RestoreLockedMode` MSBuild property to `true`</span></span> |  
| `--force-evaluate` | <span data-ttu-id="62b7d-231">Ta opcja jest przydatna w przypadku pakietów z wersją zmiennoprzecinkową zdefiniowaną w projekcie.</span><span class="sxs-lookup"><span data-stu-id="62b7d-231">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="62b7d-232">Domyślnie przywracanie pakietu NuGet nie będzie automatycznie aktualizować wersji programu przy każdym przywracaniu, chyba że zostanie uruchomiona opcja `--force-evaluate` Przywróć z.</span><span class="sxs-lookup"><span data-stu-id="62b7d-232">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with `--force-evaluate` option.</span></span> |
| `--lock-file-path` | <span data-ttu-id="62b7d-233">Definiuje niestandardową lokalizację pliku blokady dla projektu.</span><span class="sxs-lookup"><span data-stu-id="62b7d-233">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="62b7d-234">Można to również osiągnąć przez ustawienie właściwości `NuGetLockFilePath`programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="62b7d-234">This can be also achieved by setting the MSBuild property `NuGetLockFilePath`.</span></span> <span data-ttu-id="62b7d-235">Domyślnie pakiet NuGet obsługuje `packages.lock.json` w katalogu głównym.</span><span class="sxs-lookup"><span data-stu-id="62b7d-235">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="62b7d-236">Jeśli masz wiele projektów w tym samym katalogu, pakiet NuGet obsługuje plik blokady specyficzny dla projektu`packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="62b7d-236">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
