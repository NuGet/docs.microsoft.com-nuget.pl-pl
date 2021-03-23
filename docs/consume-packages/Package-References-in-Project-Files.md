---
title: Format PackageReference NuGet (odwołania do pakietów w plikach projektu)
description: Szczegóły dotyczące PackageReference NuGet w plikach projektu, które są obsługiwane przez narzędzia NuGet 4.0 + i program VS2017 i .NET Core 2,0
author: nkolev92
ms.author: nikolev
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: df7c793d115622f04a148cbbc3ebf396a3e4ab69
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859190"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="01e0e-103">Odwołania do pakietu ( `PackageReference` ) w plikach projektu</span><span class="sxs-lookup"><span data-stu-id="01e0e-103">Package references (`PackageReference`) in project files</span></span>

<span data-ttu-id="01e0e-104">Odwołania do pakietów, używanie `PackageReference` węzła, zarządzanie zależnościami NuGet bezpośrednio w plikach projektu (w przeciwieństwie do oddzielnego `packages.config` pliku).</span><span class="sxs-lookup"><span data-stu-id="01e0e-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="01e0e-105">Przy użyciu PackageReference, gdy jest wywoływana, nie ma wpływu na inne aspekty NuGet; na przykład ustawienia w `NuGet.config` plikach (w tym źródła pakietów) są nadal stosowane, jak wyjaśniono w [typowych konfiguracjach NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="01e0e-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="01e0e-106">Za pomocą PackageReference można także użyć warunków MSBuild, aby wybrać odwołania do pakietów dla platformy docelowej lub innych grup.</span><span class="sxs-lookup"><span data-stu-id="01e0e-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, or other groupings.</span></span> <span data-ttu-id="01e0e-107">Umożliwia również precyzyjne sterowanie zależnościami i przepływem zawartości.</span><span class="sxs-lookup"><span data-stu-id="01e0e-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="01e0e-108">(Zobacz, aby uzyskać więcej szczegółów na temat [pakietu NuGet i przywracania jako elementy docelowe programu MSBuild](../reference/msbuild-targets.md)).</span><span class="sxs-lookup"><span data-stu-id="01e0e-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="01e0e-109">Obsługa typu projektu</span><span class="sxs-lookup"><span data-stu-id="01e0e-109">Project type support</span></span>

<span data-ttu-id="01e0e-110">Domyślnie PackageReference jest używany dla projektów .NET Core, projektów .NET Standard i projektów platformy UWP przeznaczonych dla systemu Windows 10 Build 15063 (Aktualizacja dla twórców) i nowszych, z wyjątkiem projektów C++ platformy UWP.</span><span class="sxs-lookup"><span data-stu-id="01e0e-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="01e0e-111">Projekty .NET Framework obsługują PackageReference, ale obecnie domyślnie `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="01e0e-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="01e0e-112">Aby użyć PackageReference, [Migruj](../consume-packages/migrate-packages-config-to-package-reference.md) zależności z `packages.config` do pliku projektu, a następnie usuń packages.config.</span><span class="sxs-lookup"><span data-stu-id="01e0e-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="01e0e-113">ASP.NET aplikacje obsługujące pełną .NET Framework obejmują tylko [ograniczoną obsługę](https://github.com/NuGet/Home/issues/5877) PackageReference.</span><span class="sxs-lookup"><span data-stu-id="01e0e-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="01e0e-114">Typy projektów C++ i JavaScript nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="01e0e-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="01e0e-115">Dodawanie elementu PackageReference</span><span class="sxs-lookup"><span data-stu-id="01e0e-115">Adding a PackageReference</span></span>

<span data-ttu-id="01e0e-116">Dodaj zależność w pliku projektu przy użyciu następującej składni:</span><span class="sxs-lookup"><span data-stu-id="01e0e-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="01e0e-117">Kontrolowanie wersji zależności</span><span class="sxs-lookup"><span data-stu-id="01e0e-117">Controlling dependency version</span></span>

<span data-ttu-id="01e0e-118">Konwencja określania wersji pakietu jest taka sama jak w przypadku użycia `packages.config` :</span><span class="sxs-lookup"><span data-stu-id="01e0e-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="01e0e-119">W powyższym przykładzie 3.6.0 oznacza dowolną wersję, która jest >= 3.6.0 z preferencją dla najniższej wersji, zgodnie z opisem w temacie [przechowywanie wersji pakietu](../concepts/package-versioning.md#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="01e0e-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="01e0e-120">Używanie PackageReference dla projektu bez składnika packagereferences</span><span class="sxs-lookup"><span data-stu-id="01e0e-120">Using PackageReference for a project with no PackageReferences</span></span>

<span data-ttu-id="01e0e-121">Zaawansowane: Jeśli nie masz żadnych pakietów zainstalowanych w projekcie (nie składnika packagereferences w pliku projektu i nie packages.config pliku), ale chcesz, aby projekt został przywrócony jako styl PackageReference, można ustawić właściwość projektu RestoreProjectStyle na PackageReference w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="01e0e-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="01e0e-122">Może to być przydatne, jeśli odwołują się do projektów, które są PackageReference w stylu (istniejące projekty csproj lub zestawu SDK).</span><span class="sxs-lookup"><span data-stu-id="01e0e-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="01e0e-123">Spowoduje to włączenie pakietów, do których odwołują się te projekty, do których odwołuje się projekt.</span><span class="sxs-lookup"><span data-stu-id="01e0e-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="packagereference-and-sources"></a><span data-ttu-id="01e0e-124">PackageReference i źródła</span><span class="sxs-lookup"><span data-stu-id="01e0e-124">PackageReference and sources</span></span>

<span data-ttu-id="01e0e-125">W projektach PackageReference, przechodnie wersje zależności są rozwiązywane w czasie przywracania.</span><span class="sxs-lookup"><span data-stu-id="01e0e-125">In PackageReference projects, the transitive dependency versions are resolved at restore time.</span></span> <span data-ttu-id="01e0e-126">W związku z tym w projektach PackageReference wszystkie źródła muszą być dostępne dla wszystkich operacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="01e0e-126">As such, in PackageReference projects all sources need to be available for all restores.</span></span> 

## <a name="floating-versions"></a><span data-ttu-id="01e0e-127">Wersje zmiennoprzecinkowe</span><span class="sxs-lookup"><span data-stu-id="01e0e-127">Floating Versions</span></span>

<span data-ttu-id="01e0e-128">[Wersje zmiennoprzecinkowe](../concepts/dependency-resolution.md#floating-versions) są obsługiwane za pomocą `PackageReference` :</span><span class="sxs-lookup"><span data-stu-id="01e0e-128">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="01e0e-129">Kontrolowanie zasobów zależności</span><span class="sxs-lookup"><span data-stu-id="01e0e-129">Controlling dependency assets</span></span>

<span data-ttu-id="01e0e-130">Można używać zależności wyłącznie jako zespołu programistycznego i może nie chcieć ujawniać projektów, które będą korzystać z pakietu.</span><span class="sxs-lookup"><span data-stu-id="01e0e-130">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="01e0e-131">W tym scenariuszu można użyć `PrivateAssets` metadanych do kontrolowania tego zachowania.</span><span class="sxs-lookup"><span data-stu-id="01e0e-131">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="01e0e-132">Następujące znaczniki metadanych kontrolują elementy zależne:</span><span class="sxs-lookup"><span data-stu-id="01e0e-132">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="01e0e-133">Tag</span><span class="sxs-lookup"><span data-stu-id="01e0e-133">Tag</span></span> | <span data-ttu-id="01e0e-134">Description</span><span class="sxs-lookup"><span data-stu-id="01e0e-134">Description</span></span> | <span data-ttu-id="01e0e-135">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="01e0e-135">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="01e0e-136">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="01e0e-136">IncludeAssets</span></span> | <span data-ttu-id="01e0e-137">Te zasoby zostaną wykorzystane</span><span class="sxs-lookup"><span data-stu-id="01e0e-137">These assets will be consumed</span></span> | <span data-ttu-id="01e0e-138">all</span><span class="sxs-lookup"><span data-stu-id="01e0e-138">all</span></span> |
| <span data-ttu-id="01e0e-139">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="01e0e-139">ExcludeAssets</span></span> | <span data-ttu-id="01e0e-140">Te zasoby nie będą używane</span><span class="sxs-lookup"><span data-stu-id="01e0e-140">These assets will not be consumed</span></span> | <span data-ttu-id="01e0e-141">brak</span><span class="sxs-lookup"><span data-stu-id="01e0e-141">none</span></span> |
| <span data-ttu-id="01e0e-142">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="01e0e-142">PrivateAssets</span></span> | <span data-ttu-id="01e0e-143">Te zasoby będą wykorzystane, ale nie będą przepływać do projektu nadrzędnego</span><span class="sxs-lookup"><span data-stu-id="01e0e-143">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="01e0e-144">contentfiles; analizatory; kompilacja</span><span class="sxs-lookup"><span data-stu-id="01e0e-144">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="01e0e-145">Wartości dozwolone dla tych tagów są następujące, z wieloma wartościami oddzielonymi średnikami z wyjątkiem `all` i, `none` które muszą być wyświetlane przez siebie:</span><span class="sxs-lookup"><span data-stu-id="01e0e-145">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="01e0e-146">Wartość</span><span class="sxs-lookup"><span data-stu-id="01e0e-146">Value</span></span> | <span data-ttu-id="01e0e-147">Opis</span><span class="sxs-lookup"><span data-stu-id="01e0e-147">Description</span></span> |
| --- | ---
| <span data-ttu-id="01e0e-148">kompilowanie</span><span class="sxs-lookup"><span data-stu-id="01e0e-148">compile</span></span> | <span data-ttu-id="01e0e-149">Zawartość `lib` folderu i kontroluje, czy projekt może być kompilowany względem zestawów w folderze</span><span class="sxs-lookup"><span data-stu-id="01e0e-149">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="01e0e-150">środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="01e0e-150">runtime</span></span> | <span data-ttu-id="01e0e-151">Zawartość `lib` `runtimes` folderu i i kontroluje, czy te zestawy zostaną skopiowane do katalogu wyjściowego kompilacji</span><span class="sxs-lookup"><span data-stu-id="01e0e-151">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="01e0e-152">contentFiles</span><span class="sxs-lookup"><span data-stu-id="01e0e-152">contentFiles</span></span> | <span data-ttu-id="01e0e-153">Zawartość `contentfiles` folderu</span><span class="sxs-lookup"><span data-stu-id="01e0e-153">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="01e0e-154">kompilacja</span><span class="sxs-lookup"><span data-stu-id="01e0e-154">build</span></span> | <span data-ttu-id="01e0e-155">`.props` i `.targets` w `build` folderze</span><span class="sxs-lookup"><span data-stu-id="01e0e-155">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="01e0e-156">buildMultitargeting</span><span class="sxs-lookup"><span data-stu-id="01e0e-156">buildMultitargeting</span></span> | <span data-ttu-id="01e0e-157">*(4,0)* `.props` i `.targets` w `buildMultitargeting` folderze, dla celów określania wartości docelowej między platformami</span><span class="sxs-lookup"><span data-stu-id="01e0e-157">*(4.0)* `.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="01e0e-158">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="01e0e-158">buildTransitive</span></span> | <span data-ttu-id="01e0e-159">*(5.0 +)* `.props` i `.targets` w `buildTransitive` folderze, dla zasobów, które są przesyłane przechodniie do dowolnego, zużywanego projektu.</span><span class="sxs-lookup"><span data-stu-id="01e0e-159">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="01e0e-160">Zobacz stronę [funkcji](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) .</span><span class="sxs-lookup"><span data-stu-id="01e0e-160">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="01e0e-161">Analizatory</span><span class="sxs-lookup"><span data-stu-id="01e0e-161">analyzers</span></span> | <span data-ttu-id="01e0e-162">Analizatory .NET</span><span class="sxs-lookup"><span data-stu-id="01e0e-162">.NET analyzers</span></span> |
| <span data-ttu-id="01e0e-163">natywne</span><span class="sxs-lookup"><span data-stu-id="01e0e-163">native</span></span> | <span data-ttu-id="01e0e-164">Zawartość `native` folderu</span><span class="sxs-lookup"><span data-stu-id="01e0e-164">Contents of the `native` folder</span></span> |
| <span data-ttu-id="01e0e-165">brak</span><span class="sxs-lookup"><span data-stu-id="01e0e-165">none</span></span> | <span data-ttu-id="01e0e-166">Żadne z powyższych nie jest używane.</span><span class="sxs-lookup"><span data-stu-id="01e0e-166">None of the above are used.</span></span> |
| <span data-ttu-id="01e0e-167">all</span><span class="sxs-lookup"><span data-stu-id="01e0e-167">all</span></span> | <span data-ttu-id="01e0e-168">Wszystkie powyższe (z wyjątkiem `none` )</span><span class="sxs-lookup"><span data-stu-id="01e0e-168">All of the above (except `none`)</span></span> |

<span data-ttu-id="01e0e-169">W poniższym przykładzie wszystko, z wyjątkiem plików zawartości z pakietu, będzie używane przez projekt, a wszystko z wyjątkiem plików zawartości i analizatorów przepływa do projektu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="01e0e-169">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="01e0e-170">Należy pamiętać, że `build` `PrivateAssets` element targets i props *będzie* przepływać do projektu nadrzędnego, ponieważ nie jest zawarty w elemencie.</span><span class="sxs-lookup"><span data-stu-id="01e0e-170">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="01e0e-171">Rozważmy na przykład, że odwołanie powyżej jest używane w projekcie, który kompiluje pakiet NuGet o nazwie AppLogger.</span><span class="sxs-lookup"><span data-stu-id="01e0e-171">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="01e0e-172">AppLogger może zużywać elementy docelowe i wartości z `Contoso.Utility.UsefulStuff` , jak w przypadku projektów, które zużywają AppLogger.</span><span class="sxs-lookup"><span data-stu-id="01e0e-172">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="01e0e-173">Gdy `developmentDependency` jest ustawiona na `true` w `.nuspec` pliku, oznacza to pakiet jako zależność tylko do programowania, co uniemożliwi uwzględnienie pakietu jako zależności w innych pakietach.</span><span class="sxs-lookup"><span data-stu-id="01e0e-173">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="01e0e-174">W przypadku PackageReference *(NuGet 4.8 +)* ta flaga oznacza również, że wykluczają się zasoby czasu kompilacji z kompilacji.</span><span class="sxs-lookup"><span data-stu-id="01e0e-174">With PackageReference *(NuGet 4.8+)*, this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="01e0e-175">Aby uzyskać więcej informacji, zobacz [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="01e0e-175">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="01e0e-176">Dodawanie warunku PackageReference</span><span class="sxs-lookup"><span data-stu-id="01e0e-176">Adding a PackageReference condition</span></span>

<span data-ttu-id="01e0e-177">Możesz użyć warunku, aby określić, czy pakiet jest uwzględniony, gdzie warunki mogą używać dowolnej zmiennej MSBuild lub zmiennej zdefiniowanej w pliku TARGETS lub props.</span><span class="sxs-lookup"><span data-stu-id="01e0e-177">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="01e0e-178">Jednak obecnie `TargetFramework` obsługiwana jest tylko zmienna.</span><span class="sxs-lookup"><span data-stu-id="01e0e-178">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="01e0e-179">Załóżmy na przykład, że jesteś elementem docelowym, `netstandard1.4` `net452` a także masz zależność, która ma zastosowanie tylko do `net452` .</span><span class="sxs-lookup"><span data-stu-id="01e0e-179">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="01e0e-180">W takim przypadku nie chcesz, `netstandard1.4` aby projekt zużywał pakiet, aby dodać niepotrzebną zależność.</span><span class="sxs-lookup"><span data-stu-id="01e0e-180">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="01e0e-181">Aby tego uniknąć, należy określić warunek w następujący sposób `PackageReference` :</span><span class="sxs-lookup"><span data-stu-id="01e0e-181">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="01e0e-182">Pakiet skompilowany przy użyciu tego projektu będzie pokazywał, że Newtonsoft.Json jest uwzględniany jako zależność tylko dla `net452` elementu docelowego:</span><span class="sxs-lookup"><span data-stu-id="01e0e-182">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Wynik zastosowania warunku na PackageReference z program VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="01e0e-184">Warunki mogą być również stosowane na `ItemGroup` poziomie i będą miały zastosowanie do wszystkich `PackageReference` elementów podrzędnych:</span><span class="sxs-lookup"><span data-stu-id="01e0e-184">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a><span data-ttu-id="01e0e-185">GeneratePathProperty</span><span class="sxs-lookup"><span data-stu-id="01e0e-185">GeneratePathProperty</span></span>

<span data-ttu-id="01e0e-186">Ta funkcja jest dostępna w programie NuGet **5,0** lub nowszym oraz z programem Visual Studio 2019 **16,0** lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="01e0e-186">This feature is available with NuGet **5.0** or above and with Visual Studio 2019 **16.0** or above.</span></span>

<span data-ttu-id="01e0e-187">Czasami należy odwoływać się do plików w pakiecie z elementu docelowego programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="01e0e-187">Sometimes it is desirable to reference files in a package from an MSBuild target.</span></span>
<span data-ttu-id="01e0e-188">W `packages.config` projektach opartych na programie pakiety są instalowane w folderze względem pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="01e0e-188">In `packages.config` based projects, the packages are installed in a folder relative to the project file.</span></span> <span data-ttu-id="01e0e-189">Jednak w PackageReference pakiety są [używane](../concepts/package-installation-process.md) z folderu *Global-Packages* , który może się różnić w zależności od maszyny do komputera.</span><span class="sxs-lookup"><span data-stu-id="01e0e-189">However in PackageReference, the packages are [consumed](../concepts/package-installation-process.md) from the *global-packages* folder, which can vary from machine to machine.</span></span>

<span data-ttu-id="01e0e-190">Aby połączyć ten odstęp, pakiet NuGet wprowadził Właściwość wskazującą lokalizację, z której będzie korzystać pakiet.</span><span class="sxs-lookup"><span data-stu-id="01e0e-190">To bridge that gap, NuGet introduced a property that points to the location from which the package will be consumed.</span></span>

<span data-ttu-id="01e0e-191">Przykład:</span><span class="sxs-lookup"><span data-stu-id="01e0e-191">Example:</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

<span data-ttu-id="01e0e-192">Dodatkowo NuGet automatycznie generuje właściwości dla pakietów zawierających folder Tools.</span><span class="sxs-lookup"><span data-stu-id="01e0e-192">Additionally NuGet will automatically generate properties for packages containing a tools folder.</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
```

<span data-ttu-id="01e0e-193">Właściwości programu MSBuild i tożsamości pakietów nie mają tych samych ograniczeń, więc tożsamość pakietu musi zostać zmieniona na przyjazną nazwę MSBuild, poprzedzoną prefiksem `Pkg` .</span><span class="sxs-lookup"><span data-stu-id="01e0e-193">MSBuild properties and package identities do not have the same restrictions so the package identity needs to be changed to an MSBuild friendly name, prefixed by the word `Pkg`.</span></span>
<span data-ttu-id="01e0e-194">Aby sprawdzić dokładną nazwę wygenerowanej właściwości, zobacz wygenerowany plik [NuGet. g. props](../reference/msbuild-targets.md#restore-outputs) .</span><span class="sxs-lookup"><span data-stu-id="01e0e-194">To verify the exact name of the property generated, look at the generated [nuget.g.props](../reference/msbuild-targets.md#restore-outputs) file.</span></span>

## <a name="packagereference-aliases"></a><span data-ttu-id="01e0e-195">Aliasy PackageReference</span><span class="sxs-lookup"><span data-stu-id="01e0e-195">PackageReference Aliases</span></span>

<span data-ttu-id="01e0e-196">W niektórych rzadkich przypadkach różne pakiety będą zawierać klasy znajdujące się w tej samej przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="01e0e-196">In some rare instances different packages will contain classes in the same namespace.</span></span> <span data-ttu-id="01e0e-197">Począwszy od programu NuGet 5,7 & Visual Studio 2019 Update 7, równoważne z elementu ProjectReference, PackageReference obsługuje [`Aliases`](/dotnet/api/microsoft.codeanalysis.projectreference.aliases) .</span><span class="sxs-lookup"><span data-stu-id="01e0e-197">Starting with NuGet 5.7 & Visual Studio 2019 Update 7, equivalent to ProjectReference, PackageReference supports [`Aliases`](/dotnet/api/microsoft.codeanalysis.projectreference.aliases).</span></span>
<span data-ttu-id="01e0e-198">Domyślnie nie są udostępniane żadne aliasy.</span><span class="sxs-lookup"><span data-stu-id="01e0e-198">By default no aliases are provided.</span></span> <span data-ttu-id="01e0e-199">Po określeniu aliasu *wszystkie* zestawy pochodzące z pakietu zawierającego adnotacje muszą być przywoływane z aliasem.</span><span class="sxs-lookup"><span data-stu-id="01e0e-199">When an alias is specified, *all* assemblies coming from the annotated package with need to be referenced with an alias.</span></span>

<span data-ttu-id="01e0e-200">Przykładowe użycie można sprawdzić pod adresem [NuGet\Samples](https://github.com/NuGet/Samples/tree/main/PackageReferenceAliasesExample)</span><span class="sxs-lookup"><span data-stu-id="01e0e-200">You can look at sample usage at [NuGet\Samples](https://github.com/NuGet/Samples/tree/main/PackageReferenceAliasesExample)</span></span>

<span data-ttu-id="01e0e-201">W pliku projektu Określ aliasy w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="01e0e-201">In the project file, specify the aliases as follows:</span></span>

```xml
  <ItemGroup>
    <PackageReference Include="NuGet.Versioning" Version="5.8.0" Aliases="ExampleAlias" />
  </ItemGroup>
```

<span data-ttu-id="01e0e-202">i w kodzie używają go w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="01e0e-202">and in the code use it as follows:</span></span>

```cs
extern alias ExampleAlias;

namespace PackageReferenceAliasesExample
{
...
        {
            var version = ExampleAlias.NuGet.Versioning.NuGetVersion.Parse("5.0.0");
            Console.WriteLine($"Version : {version}");
        }
...
}

```

## <a name="nuget-warnings-and-errors"></a><span data-ttu-id="01e0e-203">Ostrzeżenia i błędy NuGet</span><span class="sxs-lookup"><span data-stu-id="01e0e-203">NuGet warnings and errors</span></span>

<span data-ttu-id="01e0e-204">*Ta funkcja jest dostępna w programie NuGet **4,3** lub nowszym oraz z programem Visual Studio 2017 **15,3** lub nowszym.*</span><span class="sxs-lookup"><span data-stu-id="01e0e-204">*This feature is available with NuGet **4.3** or above and with Visual Studio 2017 **15.3** or above.*</span></span>

<span data-ttu-id="01e0e-205">W przypadku wielu scenariuszy pakietów i przywracania wszystkie ostrzeżenia i błędy NuGet są kodowane i zaczynają się od `NU****` .</span><span class="sxs-lookup"><span data-stu-id="01e0e-205">For many pack and restore scenarios, all NuGet warnings and errors are coded, and start with `NU****`.</span></span> <span data-ttu-id="01e0e-206">Wszystkie ostrzeżenia i błędy programu NuGet są wymienione w dokumentacji [referencyjnej](../reference/errors-and-warnings.md) .</span><span class="sxs-lookup"><span data-stu-id="01e0e-206">All NuGet warnings and errors are listed in the [reference](../reference/errors-and-warnings.md) documentation.</span></span>

<span data-ttu-id="01e0e-207">Pakiet NuGet obserwuje następujące właściwości ostrzegawcze:</span><span class="sxs-lookup"><span data-stu-id="01e0e-207">NuGet observes the following warning properties:</span></span>

- <span data-ttu-id="01e0e-208">`TreatWarningsAsErrors`Traktuj wszystkie ostrzeżenia jako błędy</span><span class="sxs-lookup"><span data-stu-id="01e0e-208">`TreatWarningsAsErrors`, treat all warnings as errors</span></span>
- <span data-ttu-id="01e0e-209">`WarningsAsErrors`Traktuj konkretne ostrzeżenia jako błędy</span><span class="sxs-lookup"><span data-stu-id="01e0e-209">`WarningsAsErrors`, treat specific warnings as errors</span></span>
- <span data-ttu-id="01e0e-210">`NoWarn`ukrywanie określonych ostrzeżeń, całego projektu lub całego pakietu.</span><span class="sxs-lookup"><span data-stu-id="01e0e-210">`NoWarn`, hide specific warnings, either project-wide or package-wide.</span></span>

<span data-ttu-id="01e0e-211">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="01e0e-211">Examples:</span></span>

```xml
<PropertyGroup>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <WarningsAsErrors>$(WarningsAsErrors);NU1603;NU1605</WarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <NoWarn>$(NoWarn);NU5124</NoWarn>
</PropertyGroup>
...
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0" NoWarn="NU1605" />
</ItemGroup>
```

### <a name="suppressing-nuget-warnings"></a><span data-ttu-id="01e0e-212">Pomijanie ostrzeżeń NuGet</span><span class="sxs-lookup"><span data-stu-id="01e0e-212">Suppressing NuGet warnings</span></span>

<span data-ttu-id="01e0e-213">Chociaż zaleca się, aby wszystkie ostrzeżenia NuGet były rozwiązywane podczas operacji pakietu i przywracania, w niektórych sytuacjach jest to uzasadnione.</span><span class="sxs-lookup"><span data-stu-id="01e0e-213">While it is recommended that you resolve all NuGet warnings during your pack and restore operations, in certain situations suppressing them is warranted.</span></span>
<span data-ttu-id="01e0e-214">Aby pominąć ostrzeżenia na poziomie projektu, rozważ wykonanie:</span><span class="sxs-lookup"><span data-stu-id="01e0e-214">To suppress a warning project wide, consider doing:</span></span>

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

<span data-ttu-id="01e0e-215">Czasami ostrzeżenia dotyczą tylko określonego pakietu na grafie.</span><span class="sxs-lookup"><span data-stu-id="01e0e-215">Sometimes warnings apply only to a certain package in the graph.</span></span> <span data-ttu-id="01e0e-216">Możemy zrezygnować z pominięcia tego ostrzeżenia przez dodanie `NoWarn` elementu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="01e0e-216">We can choose to suppress that warning more selectively by adding a `NoWarn` on the PackageReference item.</span></span> 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a><span data-ttu-id="01e0e-217">Pomijanie ostrzeżeń pakietu NuGet w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="01e0e-217">Suppressing NuGet package warnings in Visual Studio</span></span>

<span data-ttu-id="01e0e-218">W programie Visual Studio można także [pominąć ostrzeżenia](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) za pomocą środowiska IDE.</span><span class="sxs-lookup"><span data-stu-id="01e0e-218">When in Visual Studio, you can also [suppress warnings](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) through the IDE.</span></span>

## <a name="locking-dependencies"></a><span data-ttu-id="01e0e-219">Blokowanie zależności</span><span class="sxs-lookup"><span data-stu-id="01e0e-219">Locking dependencies</span></span>

<span data-ttu-id="01e0e-220">*Ta funkcja jest dostępna w programie NuGet **4,9** lub nowszym oraz z programem Visual Studio 2017 **15,9** lub nowszym.*</span><span class="sxs-lookup"><span data-stu-id="01e0e-220">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="01e0e-221">Dane wejściowe do przywracania NuGet to zbiór odwołań do pakietów z pliku projektu (zależności najwyższego poziomu lub bezpośrednie), a dane wyjściowe to pełny zamknięcie wszystkich zależności pakietu, w tym zależności przechodnie.</span><span class="sxs-lookup"><span data-stu-id="01e0e-221">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="01e0e-222">Pakiet NuGet próbuje zawsze utworzyć to samo pełne zamknięcie zależności pakietów, jeśli lista wejściowa PackageReference nie została zmieniona.</span><span class="sxs-lookup"><span data-stu-id="01e0e-222">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="01e0e-223">Jednak istnieją pewne scenariusze, w których nie można tego zrobić.</span><span class="sxs-lookup"><span data-stu-id="01e0e-223">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="01e0e-224">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="01e0e-224">For example:</span></span>

* <span data-ttu-id="01e0e-225">W przypadku korzystania z wersji zmiennoprzecinkowych, takich jak `<PackageReference Include="My.Sample.Lib" Version="4.*"/>` .</span><span class="sxs-lookup"><span data-stu-id="01e0e-225">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="01e0e-226">Gdy zachodzi taka potrzeba, aby przepływać do najnowszej wersji przy każdym przywracaniu pakietów, istnieją scenariusze, w których użytkownicy wymagają, aby wykres był zablokowany do określonej najnowszej wersji i przepływał do nowszej wersji, o ile jest dostępny, przy jawnym gestie.</span><span class="sxs-lookup"><span data-stu-id="01e0e-226">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="01e0e-227">Opublikowana jest nowsza wersja pakietu spełniająca wymagania dotyczące wersji PackageReference.</span><span class="sxs-lookup"><span data-stu-id="01e0e-227">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="01e0e-228">Na przykład</span><span class="sxs-lookup"><span data-stu-id="01e0e-228">E.g.</span></span> 

  * <span data-ttu-id="01e0e-229">Dzień 1: Jeśli określono `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` , ale wersje dostępne w repozytoriach NuGet zostały 4.1.0, 4.2.0 i 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="01e0e-229">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="01e0e-230">W takim przypadku pakiet NuGet zostałby rozpoznany jako 4.1.0 (Najbliższa wersja minimalna)</span><span class="sxs-lookup"><span data-stu-id="01e0e-230">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="01e0e-231">Dzień 2: wersja 4.0.0 zostaje opublikowana.</span><span class="sxs-lookup"><span data-stu-id="01e0e-231">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="01e0e-232">Pakiet NuGet znajdzie teraz dokładne dopasowanie i zacznie rozwiązywać 4.0.0</span><span class="sxs-lookup"><span data-stu-id="01e0e-232">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="01e0e-233">Dana wersja pakietu jest usuwana z repozytorium.</span><span class="sxs-lookup"><span data-stu-id="01e0e-233">A given package version is removed from the repository.</span></span> <span data-ttu-id="01e0e-234">Chociaż nuget.org nie zezwala na usuwanie pakietów, te ograniczenia nie są dostępne dla wszystkich repozytoriów pakietów.</span><span class="sxs-lookup"><span data-stu-id="01e0e-234">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="01e0e-235">Spowoduje to znalezienie najlepszego dopasowania przez pakiet NuGet, gdy nie można rozwiązać go do usuniętej wersji.</span><span class="sxs-lookup"><span data-stu-id="01e0e-235">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="01e0e-236">Włączanie pliku blokady</span><span class="sxs-lookup"><span data-stu-id="01e0e-236">Enabling lock file</span></span>

<span data-ttu-id="01e0e-237">W celu utrwalenia pełnego zamknięcia zależności pakietu można wybrać funkcję blokowania pliku przez ustawienie właściwości MSBuild `RestorePackagesWithLockFile` dla projektu:</span><span class="sxs-lookup"><span data-stu-id="01e0e-237">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="01e0e-238">Jeśli ta właściwość jest ustawiona, przywracanie NuGet wygeneruje plik blokady pliku `packages.lock.json` w katalogu głównym projektu, który zawiera listę wszystkich zależności pakietu.</span><span class="sxs-lookup"><span data-stu-id="01e0e-238">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="01e0e-239">Gdy projekt zawiera `packages.lock.json` plik w katalogu głównym, plik blokady jest zawsze używany z przywracaniem, nawet jeśli właściwość `RestorePackagesWithLockFile` nie jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="01e0e-239">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="01e0e-240">Innym sposobem na zgodę na tę funkcję jest utworzenie fikcyjnego pustego `packages.lock.json` pliku w katalogu głównym projektu.</span><span class="sxs-lookup"><span data-stu-id="01e0e-240">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="01e0e-241">`restore` zachowanie z plikiem blokady</span><span class="sxs-lookup"><span data-stu-id="01e0e-241">`restore` behavior with lock file</span></span>
<span data-ttu-id="01e0e-242">Jeśli plik blokady jest obecny dla projektu, NuGet używa tego pliku blokady do uruchomienia `restore` .</span><span class="sxs-lookup"><span data-stu-id="01e0e-242">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="01e0e-243">Program NuGet sprawdza, czy w zależnościach pakietu zostały wprowadzone jakiekolwiek zmiany, jak wspomniano w pliku projektu (lub w plikach projektów zależnych) i czy nie wprowadzono żadnych zmian, po prostu przywraca pakiety wymienione w pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="01e0e-243">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="01e0e-244">Nie ma potrzeby ponownej oceny zależności pakietów.</span><span class="sxs-lookup"><span data-stu-id="01e0e-244">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="01e0e-245">Jeśli NuGet wykryje zmianę zdefiniowanych zależności, jak wspomniano w plikach projektu, ponownie oblicza Graf pakietu i aktualizuje plik blokady w celu odzwierciedlenia nowego zamknięcia pakietu dla projektu.</span><span class="sxs-lookup"><span data-stu-id="01e0e-245">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="01e0e-246">W przypadku ciągłej integracji/ciągłego wdrażania i innych scenariuszy, w których nie chcesz zmienić zależności pakietu na bieżąco, możesz to zrobić, ustawiając następujące polecenie `lockedmode` `true` :</span><span class="sxs-lookup"><span data-stu-id="01e0e-246">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="01e0e-247">W przypadku dotnet.exe Uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="01e0e-247">For dotnet.exe, run:</span></span>

```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="01e0e-248">W przypadku msbuild.exe Uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="01e0e-248">For msbuild.exe, run:</span></span>

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="01e0e-249">Możesz również ustawić tę właściwość warunkowego programu MSBuild w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="01e0e-249">You may also set this conditional MSBuild property in your project file:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="01e0e-250">W przypadku opcji Tryb zablokowany `true` przywracanie spowoduje przywrócenie dokładnych pakietów wymienionych w pliku blokady lub niepowodzenie w przypadku zaktualizowania zdefiniowanych zależności pakietu dla projektu po utworzeniu pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="01e0e-250">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="01e0e-251">Utwórz część pliku blokady w repozytorium źródłowym</span><span class="sxs-lookup"><span data-stu-id="01e0e-251">Make lock file part of your source repository</span></span>
<span data-ttu-id="01e0e-252">W przypadku kompilowania aplikacji plik wykonywalny i projekt w danym momencie znajdują się na początku łańcucha zależności, a następnie należy zaewidencjonować plik blokady do repozytorium kodu źródłowego, aby pakiet NuGet mógł go używać podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="01e0e-252">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="01e0e-253">Jeśli jednak projekt jest projektem biblioteki, który nie jest dostarczany lub wspólny projekt kodu, od którego zależą inne projekty, **nie należy** ewidencjonować pliku blokady jako części kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="01e0e-253">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="01e0e-254">Nie ma szkody w zachowaniu pliku blokady, ale zablokowane zależności pakietu dla wspólnego projektu kodu nie mogą być używane, jak wymieniono w pliku blokady podczas przywracania/kompilowania projektu, który zależy od tego projektu Common-Code.</span><span class="sxs-lookup"><span data-stu-id="01e0e-254">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="01e0e-255">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="01e0e-255">Eg.</span></span>

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

<span data-ttu-id="01e0e-256">Jeśli `ProjectA` ma zależność od `PackageX` wersji `2.0.0` , a także odwołania, `ProjectB` które są zależne od `PackageX` wersji `1.0.0` , plik blokady `ProjectB` zostanie wystawiony zależności od `PackageX` wersji `1.0.0` .</span><span class="sxs-lookup"><span data-stu-id="01e0e-256">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="01e0e-257">Jednak po `ProjectA` skompilowaniu jego plik blokady będzie zawierał zależność od `PackageX` wersji **`2.0.0`** , a **nie** `1.0.0` tak jak na liście w pliku blokady dla `ProjectB` .</span><span class="sxs-lookup"><span data-stu-id="01e0e-257">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="01e0e-258">W ten sposób plik blokady wspólnego projektu kodu ma niewielki stan dla projektów, które są od niego zależne.</span><span class="sxs-lookup"><span data-stu-id="01e0e-258">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="01e0e-259">Zablokuj rozszerzalność plików</span><span class="sxs-lookup"><span data-stu-id="01e0e-259">Lock file extensibility</span></span>

<span data-ttu-id="01e0e-260">Można kontrolować różne zachowania przywracania za pomocą pliku blokady zgodnie z poniższym opisem:</span><span class="sxs-lookup"><span data-stu-id="01e0e-260">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="01e0e-261">Opcja NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="01e0e-261">NuGet.exe option</span></span> | <span data-ttu-id="01e0e-262">Opcja dotnet</span><span class="sxs-lookup"><span data-stu-id="01e0e-262">dotnet option</span></span> | <span data-ttu-id="01e0e-263">Odpowiednik opcji programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="01e0e-263">MSBuild equivalent option</span></span> | <span data-ttu-id="01e0e-264">Opis</span><span class="sxs-lookup"><span data-stu-id="01e0e-264">Description</span></span> |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | <span data-ttu-id="01e0e-265">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="01e0e-265">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="01e0e-266">Umożliwia użycie pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="01e0e-266">Opts into the usage of a lock file.</span></span> |
| `-LockedMode` | `--locked-mode` | <span data-ttu-id="01e0e-267">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="01e0e-267">RestoreLockedMode</span></span> | <span data-ttu-id="01e0e-268">Włącza tryb zablokowany do przywracania.</span><span class="sxs-lookup"><span data-stu-id="01e0e-268">Enables locked mode for restore.</span></span> <span data-ttu-id="01e0e-269">Jest to przydatne w scenariuszach ciągłej integracji/ciągłego wdrażania.</span><span class="sxs-lookup"><span data-stu-id="01e0e-269">This is useful in CI/CD scenarios where you want repeatable builds.</span></span>|   
| `-ForceEvaluate` | `--force-evaluate` | <span data-ttu-id="01e0e-270">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="01e0e-270">RestoreForceEvaluate</span></span> | <span data-ttu-id="01e0e-271">Ta opcja jest przydatna w przypadku pakietów z wersją zmiennoprzecinkową zdefiniowaną w projekcie.</span><span class="sxs-lookup"><span data-stu-id="01e0e-271">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="01e0e-272">Domyślnie przywracanie pakietu NuGet nie będzie automatycznie aktualizować wersji programu przy każdym przywracaniu, chyba że zostanie uruchomiony przycisk Przywróć z tą opcją.</span><span class="sxs-lookup"><span data-stu-id="01e0e-272">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with this option.</span></span> |
| `-LockFilePath` | `--lock-file-path` | <span data-ttu-id="01e0e-273">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="01e0e-273">NuGetLockFilePath</span></span> | <span data-ttu-id="01e0e-274">Definiuje niestandardową lokalizację pliku blokady dla projektu.</span><span class="sxs-lookup"><span data-stu-id="01e0e-274">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="01e0e-275">Domyślnie pakiet NuGet obsługuje `packages.lock.json` w katalogu głównym.</span><span class="sxs-lookup"><span data-stu-id="01e0e-275">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="01e0e-276">Jeśli masz wiele projektów w tym samym katalogu, pakiet NuGet obsługuje plik blokady specyficzny dla projektu `packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="01e0e-276">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |

## <a name="assettargetfallback"></a><span data-ttu-id="01e0e-277">AssetTargetFallback</span><span class="sxs-lookup"><span data-stu-id="01e0e-277">AssetTargetFallback</span></span>

<span data-ttu-id="01e0e-278">`AssetTargetFallback`Właściwość pozwala określić dodatkowe zgodne wersje platformy dla projektów, do których odwołuje się projekt, oraz pakietów NuGet, które są używane w projekcie.</span><span class="sxs-lookup"><span data-stu-id="01e0e-278">The `AssetTargetFallback` property lets you specify additional compatible framework versions for projects that your project references and NuGet packages that your project consumes.</span></span>

<span data-ttu-id="01e0e-279">Jeśli określisz zależność pakietu przy użyciu programu, `PackageReference` ale ten pakiet nie zawiera zasobów, które są zgodne z platformą docelową projektu, `AssetTargetFallback` Właściwość jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="01e0e-279">If you specify a package dependency using `PackageReference` but that package doesn't contain assets that are compatible with your projects's target framework, the `AssetTargetFallback` property comes into play.</span></span> <span data-ttu-id="01e0e-280">Zgodność przywoływanego pakietu jest ponownie sprawdzana przy użyciu każdej platformy docelowej określonej w `AssetTargetFallback` .</span><span class="sxs-lookup"><span data-stu-id="01e0e-280">The compatibility of the referenced package is rechecked using each target framework that's specified in `AssetTargetFallback`.</span></span>
<span data-ttu-id="01e0e-281">Gdy `project` odwołanie do lub `package` odwołuje się do programu `AssetTargetFallback` , zostanie zgłoszone ostrzeżenie [NU1701](../reference/errors-and-warnings/NU1701.md) .</span><span class="sxs-lookup"><span data-stu-id="01e0e-281">When a `project` or a `package` is referenced through `AssetTargetFallback`, the [NU1701](../reference/errors-and-warnings/NU1701.md) warning will be raised.</span></span>

<span data-ttu-id="01e0e-282">Zapoznaj się z tabelą poniżej, aby zapoznać się z przykładami dotyczącymi `AssetTargetFallback` zgodności.</span><span class="sxs-lookup"><span data-stu-id="01e0e-282">Refer to the table below for examples of how `AssetTargetFallback` affects compatibility.</span></span>

| <span data-ttu-id="01e0e-283">Struktura projektu</span><span class="sxs-lookup"><span data-stu-id="01e0e-283">Project framework</span></span> | <span data-ttu-id="01e0e-284">AssetTargetFallback</span><span class="sxs-lookup"><span data-stu-id="01e0e-284">AssetTargetFallback</span></span> | <span data-ttu-id="01e0e-285">Struktury pakietów</span><span class="sxs-lookup"><span data-stu-id="01e0e-285">Package frameworks</span></span> | <span data-ttu-id="01e0e-286">Wynik</span><span class="sxs-lookup"><span data-stu-id="01e0e-286">Result</span></span> |
|-------------------|---------------------|--------------------|--------|
| <span data-ttu-id="01e0e-287"> .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="01e0e-287">.NET Framework 4.7.2</span></span> | | <span data-ttu-id="01e0e-288">.NET Standard 2,0</span><span class="sxs-lookup"><span data-stu-id="01e0e-288">.NET Standard 2.0</span></span> | <span data-ttu-id="01e0e-289">.NET Standard 2,0</span><span class="sxs-lookup"><span data-stu-id="01e0e-289">.NET Standard 2.0</span></span> |
| <span data-ttu-id="01e0e-290">Aplikacja .NET Core 3,1</span><span class="sxs-lookup"><span data-stu-id="01e0e-290">.NET Core App 3.1</span></span> | | <span data-ttu-id="01e0e-291">.NET Standard 2,0, .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="01e0e-291">.NET Standard 2.0, .NET Framework 4.7.2</span></span> | <span data-ttu-id="01e0e-292">.NET Standard 2,0</span><span class="sxs-lookup"><span data-stu-id="01e0e-292">.NET Standard 2.0</span></span> |
| <span data-ttu-id="01e0e-293">Aplikacja .NET Core 3,1</span><span class="sxs-lookup"><span data-stu-id="01e0e-293">.NET Core App 3.1</span></span> | | <span data-ttu-id="01e0e-294"> .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="01e0e-294">.NET Framework 4.7.2</span></span> | <span data-ttu-id="01e0e-295">Niezgodność, niepowodzenie z [`NU1202`](../reference/errors-and-warnings/NU1202.md)</span><span class="sxs-lookup"><span data-stu-id="01e0e-295">Incompatible, fail with [`NU1202`](../reference/errors-and-warnings/NU1202.md)</span></span> |
| <span data-ttu-id="01e0e-296">Aplikacja .NET Core 3,1</span><span class="sxs-lookup"><span data-stu-id="01e0e-296">.NET Core App 3.1</span></span> | <span data-ttu-id="01e0e-297">net472;net471</span><span class="sxs-lookup"><span data-stu-id="01e0e-297">net472;net471</span></span> | <span data-ttu-id="01e0e-298"> .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="01e0e-298">.NET Framework 4.7.2</span></span> | <span data-ttu-id="01e0e-299">.NET Framework 4.7.2 z [`NU1701`](../reference/errors-and-warnings/NU1701.md)</span><span class="sxs-lookup"><span data-stu-id="01e0e-299">.NET Framework 4.7.2 with [`NU1701`](../reference/errors-and-warnings/NU1701.md)</span></span> |

<span data-ttu-id="01e0e-300">Można określić wiele struktur `;` , używając jako ogranicznika.</span><span class="sxs-lookup"><span data-stu-id="01e0e-300">Multiple frameworks can be specified using `;` as a delimiter.</span></span> <span data-ttu-id="01e0e-301">Aby dodać platformę rezerwową, można wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="01e0e-301">To add a fallback framework you can do the following:</span></span>

```xml
<AssetTargetFallback Condition=" '$(TargetFramework)'=='netcoreapp3.1' ">
    $(AssetTargetFallback);net472;net471
</AssetTargetFallback>
```

<span data-ttu-id="01e0e-302">Możesz opuścić `$(AssetTargetFallback)` tę opcję, jeśli chcesz zastąpić, zamiast dodawać do istniejących `AssetTargetFallback` wartości.</span><span class="sxs-lookup"><span data-stu-id="01e0e-302">You can leave off `$(AssetTargetFallback)` if you wish to overwrite, instead of add to the existing `AssetTargetFallback` values.</span></span>

> [!NOTE]
> <span data-ttu-id="01e0e-303">Jeśli używasz [projektu opartego na zestawie SDK platformy .NET](/dotnet/core/sdk), odpowiednie `$(AssetTargetFallback)` wartości są skonfigurowane i nie trzeba ustawiać ich ręcznie.</span><span class="sxs-lookup"><span data-stu-id="01e0e-303">If you are using a [.NET SDK based project](/dotnet/core/sdk), appropriate `$(AssetTargetFallback)` values are configured and you do not need to set them manually.</span></span>
>
> <span data-ttu-id="01e0e-304">`$(PackageTargetFallback)` była wcześniejszą funkcją, która podjęła próbę rozwiązania tego wezwania, ale jest w sposób zasadniczy przerwany i nie *należy* jej używać.</span><span class="sxs-lookup"><span data-stu-id="01e0e-304">`$(PackageTargetFallback)` was an earlier feature that attempted to address this challenge, but it is fundamentally broken and *should* not be used.</span></span> <span data-ttu-id="01e0e-305">Aby przeprowadzić migrację z `$(PackageTargetFallback)` do programu `$(AssetTargetFallback)` , wystarczy zmienić nazwę właściwości.</span><span class="sxs-lookup"><span data-stu-id="01e0e-305">To migrate from `$(PackageTargetFallback)` to `$(AssetTargetFallback)`, simply change the property name.</span></span>
