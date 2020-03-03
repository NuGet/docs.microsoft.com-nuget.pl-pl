---
title: Format PackageReference NuGet (odwołania do pakietów w plikach projektu)
description: Szczegóły dotyczące PackageReference NuGet w plikach projektu, które są obsługiwane przez narzędzia NuGet 4.0 + i program VS2017 i .NET Core 2,0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: a5833df60c5f7905359f421141347b1237f45d86
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230619"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="ec009-103">Odwołania do pakietów (PackageReference) w plikach projektu</span><span class="sxs-lookup"><span data-stu-id="ec009-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="ec009-104">Odwołania do pakietów przy użyciu węzła `PackageReference`, zarządzanie zależnościami NuGet bezpośrednio w plikach projektu (w przeciwieństwie do oddzielnego pliku `packages.config`).</span><span class="sxs-lookup"><span data-stu-id="ec009-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="ec009-105">Przy użyciu PackageReference, gdy jest wywoływana, nie ma wpływu na inne aspekty NuGet; na przykład ustawienia w plikach `NuGet.config` (w tym źródła pakietów) są nadal stosowane, jak wyjaśniono w [typowych konfiguracjach NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="ec009-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="ec009-106">Za pomocą PackageReference można także użyć warunków MSBuild, aby wybrać odwołania do pakietów dla platformy docelowej lub innych grup.</span><span class="sxs-lookup"><span data-stu-id="ec009-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, or other groupings.</span></span> <span data-ttu-id="ec009-107">Umożliwia również precyzyjne sterowanie zależnościami i przepływem zawartości.</span><span class="sxs-lookup"><span data-stu-id="ec009-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="ec009-108">(Zobacz, aby uzyskać więcej szczegółów na temat [pakietu NuGet i przywracania jako elementy docelowe programu MSBuild](../reference/msbuild-targets.md)).</span><span class="sxs-lookup"><span data-stu-id="ec009-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="ec009-109">Obsługa typu projektu</span><span class="sxs-lookup"><span data-stu-id="ec009-109">Project type support</span></span>

<span data-ttu-id="ec009-110">Domyślnie PackageReference jest używany dla projektów .NET Core, projektów .NET Standard i projektów platformy UWP przeznaczonych dla systemu Windows 10 Build 15063 (Aktualizacja dla twórców) i nowszych, z wyjątkiem projektów C++ platformy UWP.</span><span class="sxs-lookup"><span data-stu-id="ec009-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="ec009-111">Projekty .NET Framework obsługują PackageReference, ale obecnie domyślnie `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="ec009-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="ec009-112">Aby użyć PackageReference, [Przeprowadź migrację](../consume-packages/migrate-packages-config-to-package-reference.md) zależności z `packages.config` do pliku projektu, a następnie usuń plik Packages. config.</span><span class="sxs-lookup"><span data-stu-id="ec009-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="ec009-113">ASP.NET aplikacje obsługujące pełną .NET Framework obejmują tylko [ograniczoną obsługę](https://github.com/NuGet/Home/issues/5877) PackageReference.</span><span class="sxs-lookup"><span data-stu-id="ec009-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="ec009-114">C++i typy projektów JavaScript nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="ec009-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="ec009-115">Dodawanie elementu PackageReference</span><span class="sxs-lookup"><span data-stu-id="ec009-115">Adding a PackageReference</span></span>

<span data-ttu-id="ec009-116">Dodaj zależność w pliku projektu przy użyciu następującej składni:</span><span class="sxs-lookup"><span data-stu-id="ec009-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="ec009-117">Kontrolowanie wersji zależności</span><span class="sxs-lookup"><span data-stu-id="ec009-117">Controlling dependency version</span></span>

<span data-ttu-id="ec009-118">Konwencja dotycząca określania wersji pakietu jest taka sama jak w przypadku używania `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="ec009-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="ec009-119">W powyższym przykładzie 3.6.0 oznacza dowolną wersję, która jest > = 3.6.0 z preferencją dla najniższej wersji, zgodnie z opisem w temacie [przechowywanie wersji pakietu](../concepts/package-versioning.md#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="ec009-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="ec009-120">Używanie PackageReference dla projektu bez składnika packagereferences</span><span class="sxs-lookup"><span data-stu-id="ec009-120">Using PackageReference for a project with no PackageReferences</span></span>

<span data-ttu-id="ec009-121">Zaawansowane: Jeśli nie masz żadnych pakietów zainstalowanych w projekcie (nie składnika packagereferences w pliku projektu i bez pliku Packages. config), ale chcesz przywrócić projekt jako styl PackageReference, możesz ustawić właściwość projektu RestoreProjectStyle na PackageReference w plik projektu.</span><span class="sxs-lookup"><span data-stu-id="ec009-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="ec009-122">Może to być przydatne, jeśli odwołują się do projektów, które są PackageReference w stylu (istniejące projekty csproj lub zestawu SDK).</span><span class="sxs-lookup"><span data-stu-id="ec009-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="ec009-123">Spowoduje to włączenie pakietów, do których odwołują się te projekty, do których odwołuje się projekt.</span><span class="sxs-lookup"><span data-stu-id="ec009-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="packagereference-and-sources"></a><span data-ttu-id="ec009-124">PackageReference i źródła</span><span class="sxs-lookup"><span data-stu-id="ec009-124">PackageReference and sources</span></span>

<span data-ttu-id="ec009-125">W projektach PackageReference, przechodnie wersje zależności są rozwiązywane w czasie przywracania.</span><span class="sxs-lookup"><span data-stu-id="ec009-125">In PackageReference projects, the transitive dependency versions are resolved at restore time.</span></span> <span data-ttu-id="ec009-126">W związku z tym w projektach PackageReference wszystkie źródła muszą być dostępne dla wszystkich operacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="ec009-126">As such, in PackageReference projects all sources need to be available for all restores.</span></span> 

## <a name="floating-versions"></a><span data-ttu-id="ec009-127">Wersje zmiennoprzecinkowe</span><span class="sxs-lookup"><span data-stu-id="ec009-127">Floating Versions</span></span>

<span data-ttu-id="ec009-128">Obsługiwane są [wersje zmiennoprzecinkowe](../concepts/dependency-resolution.md#floating-versions) `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="ec009-128">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="ec009-129">Kontrolowanie zasobów zależności</span><span class="sxs-lookup"><span data-stu-id="ec009-129">Controlling dependency assets</span></span>

<span data-ttu-id="ec009-130">Można używać zależności wyłącznie jako zespołu programistycznego i może nie chcieć ujawniać projektów, które będą korzystać z pakietu.</span><span class="sxs-lookup"><span data-stu-id="ec009-130">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="ec009-131">W tym scenariuszu można użyć metadanych `PrivateAssets`, aby kontrolować to zachowanie.</span><span class="sxs-lookup"><span data-stu-id="ec009-131">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="ec009-132">Następujące znaczniki metadanych kontrolują elementy zależne:</span><span class="sxs-lookup"><span data-stu-id="ec009-132">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="ec009-133">Tag</span><span class="sxs-lookup"><span data-stu-id="ec009-133">Tag</span></span> | <span data-ttu-id="ec009-134">Opis</span><span class="sxs-lookup"><span data-stu-id="ec009-134">Description</span></span> | <span data-ttu-id="ec009-135">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="ec009-135">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ec009-136">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="ec009-136">IncludeAssets</span></span> | <span data-ttu-id="ec009-137">Te zasoby zostaną wykorzystane</span><span class="sxs-lookup"><span data-stu-id="ec009-137">These assets will be consumed</span></span> | <span data-ttu-id="ec009-138">all</span><span class="sxs-lookup"><span data-stu-id="ec009-138">all</span></span> |
| <span data-ttu-id="ec009-139">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="ec009-139">ExcludeAssets</span></span> | <span data-ttu-id="ec009-140">Te zasoby nie będą używane</span><span class="sxs-lookup"><span data-stu-id="ec009-140">These assets will not be consumed</span></span> | <span data-ttu-id="ec009-141">brak</span><span class="sxs-lookup"><span data-stu-id="ec009-141">none</span></span> |
| <span data-ttu-id="ec009-142">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="ec009-142">PrivateAssets</span></span> | <span data-ttu-id="ec009-143">Te zasoby będą wykorzystane, ale nie będą przepływać do projektu nadrzędnego</span><span class="sxs-lookup"><span data-stu-id="ec009-143">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="ec009-144">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="ec009-144">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="ec009-145">Wartości dozwolone dla tych tagów są następujące, z wieloma wartościami oddzielonymi średnikami z wyjątkiem `all` i `none`, które muszą być wyświetlane samodzielnie:</span><span class="sxs-lookup"><span data-stu-id="ec009-145">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="ec009-146">Wartość</span><span class="sxs-lookup"><span data-stu-id="ec009-146">Value</span></span> | <span data-ttu-id="ec009-147">Opis</span><span class="sxs-lookup"><span data-stu-id="ec009-147">Description</span></span> |
| --- | ---
| <span data-ttu-id="ec009-148">opracowania</span><span class="sxs-lookup"><span data-stu-id="ec009-148">compile</span></span> | <span data-ttu-id="ec009-149">Zawartość folderu `lib` i kontroluje, czy projekt można kompilować względem zestawów w folderze</span><span class="sxs-lookup"><span data-stu-id="ec009-149">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="ec009-150">środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="ec009-150">runtime</span></span> | <span data-ttu-id="ec009-151">Zawartość folderu `lib` i `runtimes` i kontroluje, czy te zestawy zostaną skopiowane do katalogu wyjściowego kompilacji</span><span class="sxs-lookup"><span data-stu-id="ec009-151">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="ec009-152">contentFiles</span><span class="sxs-lookup"><span data-stu-id="ec009-152">contentFiles</span></span> | <span data-ttu-id="ec009-153">Zawartość folderu `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="ec009-153">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="ec009-154">kompilacja</span><span class="sxs-lookup"><span data-stu-id="ec009-154">build</span></span> | <span data-ttu-id="ec009-155">`.props` i `.targets` w folderze `build`</span><span class="sxs-lookup"><span data-stu-id="ec009-155">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="ec009-156">buildMultitargeting</span><span class="sxs-lookup"><span data-stu-id="ec009-156">buildMultitargeting</span></span> | <span data-ttu-id="ec009-157">*(4,0)* `.props` i `.targets` w folderze `buildMultitargeting` dla celów związanych z różnymi platformami</span><span class="sxs-lookup"><span data-stu-id="ec009-157">*(4.0)* `.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="ec009-158">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="ec009-158">buildTransitive</span></span> | <span data-ttu-id="ec009-159">*(5.0 +)* `.props` i `.targets` w folderze `buildTransitive` dla zasobów, które są przechodniie przepływowo do dowolnego konsumowanego projektu.</span><span class="sxs-lookup"><span data-stu-id="ec009-159">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="ec009-160">Zobacz stronę [funkcji](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) .</span><span class="sxs-lookup"><span data-stu-id="ec009-160">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="ec009-161">Analizatory</span><span class="sxs-lookup"><span data-stu-id="ec009-161">analyzers</span></span> | <span data-ttu-id="ec009-162">Analizatory .NET</span><span class="sxs-lookup"><span data-stu-id="ec009-162">.NET analyzers</span></span> |
| <span data-ttu-id="ec009-163">natywne</span><span class="sxs-lookup"><span data-stu-id="ec009-163">native</span></span> | <span data-ttu-id="ec009-164">Zawartość folderu `native`</span><span class="sxs-lookup"><span data-stu-id="ec009-164">Contents of the `native` folder</span></span> |
| <span data-ttu-id="ec009-165">brak</span><span class="sxs-lookup"><span data-stu-id="ec009-165">none</span></span> | <span data-ttu-id="ec009-166">Żadne z powyższych nie jest używane.</span><span class="sxs-lookup"><span data-stu-id="ec009-166">None of the above are used.</span></span> |
| <span data-ttu-id="ec009-167">all</span><span class="sxs-lookup"><span data-stu-id="ec009-167">all</span></span> | <span data-ttu-id="ec009-168">Wszystkie powyższe (z wyjątkiem `none`)</span><span class="sxs-lookup"><span data-stu-id="ec009-168">All of the above (except `none`)</span></span> |

<span data-ttu-id="ec009-169">W poniższym przykładzie wszystko, z wyjątkiem plików zawartości z pakietu, będzie używane przez projekt, a wszystko z wyjątkiem plików zawartości i analizatorów przepływa do projektu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="ec009-169">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="ec009-170">Należy pamiętać, że ponieważ `build` nie jest zawarty w `PrivateAssets`, obiekty docelowe i elementy props *będą* przepływać do projektu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="ec009-170">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="ec009-171">Rozważmy na przykład, że odwołanie powyżej jest używane w projekcie, który kompiluje pakiet NuGet o nazwie AppLogger.</span><span class="sxs-lookup"><span data-stu-id="ec009-171">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="ec009-172">AppLogger może zużywać elementy docelowe i wartości z `Contoso.Utility.UsefulStuff`, tak jak projekty, które zużywają AppLogger.</span><span class="sxs-lookup"><span data-stu-id="ec009-172">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="ec009-173">Gdy `developmentDependency` jest ustawiona na `true` w pliku `.nuspec`, oznacza to pakiet jako zależność tylko do programowania, co uniemożliwi uwzględnienie pakietu jako zależności w innych pakietach.</span><span class="sxs-lookup"><span data-stu-id="ec009-173">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="ec009-174">W przypadku PackageReference *(NuGet 4.8 +)* ta flaga oznacza również, że wykluczają się zasoby czasu kompilacji z kompilacji.</span><span class="sxs-lookup"><span data-stu-id="ec009-174">With PackageReference *(NuGet 4.8+)*, this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="ec009-175">Aby uzyskać więcej informacji, zobacz [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="ec009-175">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="ec009-176">Dodawanie warunku PackageReference</span><span class="sxs-lookup"><span data-stu-id="ec009-176">Adding a PackageReference condition</span></span>

<span data-ttu-id="ec009-177">Możesz użyć warunku, aby określić, czy pakiet jest uwzględniony, gdzie warunki mogą używać dowolnej zmiennej MSBuild lub zmiennej zdefiniowanej w pliku TARGETS lub props.</span><span class="sxs-lookup"><span data-stu-id="ec009-177">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="ec009-178">Jednak obecnie obsługiwana jest tylko zmienna `TargetFramework`.</span><span class="sxs-lookup"><span data-stu-id="ec009-178">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="ec009-179">Załóżmy na przykład, że jesteś celem `netstandard1.4`, a także `net452`, ale ma zależność, która ma zastosowanie tylko do `net452`.</span><span class="sxs-lookup"><span data-stu-id="ec009-179">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="ec009-180">W takim przypadku nie chcesz, aby projekt `netstandard1.4`, który zużywa pakiet w celu dodania niepotrzebnej zależności.</span><span class="sxs-lookup"><span data-stu-id="ec009-180">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="ec009-181">Aby tego uniknąć, należy określić warunek na `PackageReference` w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ec009-181">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="ec009-182">Pakiet utworzony przy użyciu tego projektu będzie przedstawiał, że Newtonsoft. JSON jest uwzględniany jako zależność tylko dla elementu docelowego `net452`:</span><span class="sxs-lookup"><span data-stu-id="ec009-182">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Wynik zastosowania warunku na PackageReference z program VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="ec009-184">Warunki mogą być również stosowane na poziomie `ItemGroup` i będą miały zastosowanie do wszystkich elementów podrzędnych `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="ec009-184">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a><span data-ttu-id="ec009-185">GeneratePathProperty</span><span class="sxs-lookup"><span data-stu-id="ec009-185">GeneratePathProperty</span></span>

<span data-ttu-id="ec009-186">Ta funkcja jest dostępna w programie NuGet **5,0** lub nowszym oraz z programem Visual Studio 2019 **16,0** lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="ec009-186">This feature is available with NuGet **5.0** or above and with Visual Studio 2019 **16.0** or above.</span></span>

<span data-ttu-id="ec009-187">Czasami należy odwoływać się do plików w pakiecie z elementu docelowego programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="ec009-187">Sometimes it is desirable to reference files in a package from an MSBuild target.</span></span>
<span data-ttu-id="ec009-188">W projektach opartych na `packages.config` pakiety są instalowane w folderze odnoszącym się do pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="ec009-188">In `packages.config` based projects, the packages are installed in a folder relative to the project file.</span></span> <span data-ttu-id="ec009-189">Jednak w PackageReference pakiety są [używane](../concepts/package-installation-process.md) z folderu *Global-Packages* , który może się różnić w zależności od maszyny do komputera.</span><span class="sxs-lookup"><span data-stu-id="ec009-189">However in PackageReference, the packages are [consumed](../concepts/package-installation-process.md) from the *global-packages* folder, which can vary from machine to machine.</span></span>

<span data-ttu-id="ec009-190">Aby połączyć ten odstęp, pakiet NuGet wprowadził Właściwość wskazującą lokalizację, z której będzie korzystać pakiet.</span><span class="sxs-lookup"><span data-stu-id="ec009-190">To bridge that gap, NuGet introduced a property that points to the location from which the package will be consumed.</span></span>

<span data-ttu-id="ec009-191">Przykład:</span><span class="sxs-lookup"><span data-stu-id="ec009-191">Example:</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

<span data-ttu-id="ec009-192">Dodatkowo NuGet automatycznie generuje właściwości dla pakietów zawierających folder Tools.</span><span class="sxs-lookup"><span data-stu-id="ec009-192">Additionally NuGet will automatically generate properties for packages containing a tools folder.</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
````

<span data-ttu-id="ec009-193">Właściwości programu MSBuild i tożsamości pakietów nie mają tych samych ograniczeń, dlatego należy zmienić tożsamość pakietu na przyjazną nazwę MSBuild, poprzedzoną prefiksem `Pkg`.</span><span class="sxs-lookup"><span data-stu-id="ec009-193">MSBuild properties and package identities do not have the same restrictions so the package identity needs to be changed to an MSBuild friendly name, prefixed by the word `Pkg`.</span></span>
<span data-ttu-id="ec009-194">Aby sprawdzić dokładną nazwę wygenerowanej właściwości, zobacz wygenerowany plik [NuGet. g. props](../reference/msbuild-targets.md#restore-outputs) .</span><span class="sxs-lookup"><span data-stu-id="ec009-194">To verify the exact name of the property generated, look at the generated [nuget.g.props](../reference/msbuild-targets.md#restore-outputs) file.</span></span>

## <a name="nuget-warnings-and-errors"></a><span data-ttu-id="ec009-195">Ostrzeżenia i błędy NuGet</span><span class="sxs-lookup"><span data-stu-id="ec009-195">NuGet warnings and errors</span></span>

<span data-ttu-id="ec009-196">*Ta funkcja jest dostępna w programie NuGet **4,3** lub nowszym oraz z programem Visual Studio 2017 **15,3** lub nowszym.*</span><span class="sxs-lookup"><span data-stu-id="ec009-196">*This feature is available with NuGet **4.3** or above and with Visual Studio 2017 **15.3** or above.*</span></span>

<span data-ttu-id="ec009-197">W przypadku wielu scenariuszy pakowania i przywracania wszystkie ostrzeżenia i błędy programu NuGet są kodowane i zaczynają się od `NU****`.</span><span class="sxs-lookup"><span data-stu-id="ec009-197">For many pack and restore scenarios, all NuGet warnings and errors are coded, and start with `NU****`.</span></span> <span data-ttu-id="ec009-198">Wszystkie ostrzeżenia i błędy programu NuGet są wymienione w dokumentacji [referencyjnej](../reference/errors-and-warnings.md) .</span><span class="sxs-lookup"><span data-stu-id="ec009-198">All NuGet warnings and errors are listed in the [reference](../reference/errors-and-warnings.md) documentation.</span></span>

<span data-ttu-id="ec009-199">Pakiet NuGet obserwuje następujące właściwości ostrzegawcze:</span><span class="sxs-lookup"><span data-stu-id="ec009-199">NuGet observes the following warning properties:</span></span>

- <span data-ttu-id="ec009-200">`TreatWarningsAsErrors`Traktuj wszystkie ostrzeżenia jako błędy</span><span class="sxs-lookup"><span data-stu-id="ec009-200">`TreatWarningsAsErrors`, treat all warnings as errors</span></span>
- <span data-ttu-id="ec009-201">`WarningsAsErrors`Traktuj określone ostrzeżenia jako błędy</span><span class="sxs-lookup"><span data-stu-id="ec009-201">`WarningsAsErrors`, treat specific warnings as errors</span></span>
- <span data-ttu-id="ec009-202">`NoWarn`, ukrywanie określonych ostrzeżeń, całego projektu lub całego pakietu.</span><span class="sxs-lookup"><span data-stu-id="ec009-202">`NoWarn`, hide specific warnings, either project-wide or package-wide.</span></span>

<span data-ttu-id="ec009-203">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="ec009-203">Examples:</span></span>

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

### <a name="suppressing-nuget-warnings"></a><span data-ttu-id="ec009-204">Pomijanie ostrzeżeń NuGet</span><span class="sxs-lookup"><span data-stu-id="ec009-204">Suppressing NuGet warnings</span></span>

<span data-ttu-id="ec009-205">Chociaż zaleca się, aby wszystkie ostrzeżenia NuGet były rozwiązywane podczas operacji pakietu i przywracania, w niektórych sytuacjach jest to uzasadnione.</span><span class="sxs-lookup"><span data-stu-id="ec009-205">While it is recommended that you resolve all NuGet warnings during your pack and restore operations, in certain situations suppressing them is warranted.</span></span>
<span data-ttu-id="ec009-206">Aby pominąć ostrzeżenia na poziomie projektu, rozważ wykonanie:</span><span class="sxs-lookup"><span data-stu-id="ec009-206">To suppress a warning project wide, consider doing:</span></span>

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

<span data-ttu-id="ec009-207">Czasami ostrzeżenia dotyczą tylko określonego pakietu na grafie.</span><span class="sxs-lookup"><span data-stu-id="ec009-207">Sometimes warnings apply only to a certain package in the graph.</span></span> <span data-ttu-id="ec009-208">Możemy wybrać opcję pomijania tego ostrzeżenia przez dodanie `NoWarn` w elemencie PackageReference.</span><span class="sxs-lookup"><span data-stu-id="ec009-208">We can choose to suppress that warning more selectively by adding a `NoWarn` on the PackageReference item.</span></span> 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a><span data-ttu-id="ec009-209">Pomijanie ostrzeżeń pakietu NuGet w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ec009-209">Suppressing NuGet package warnings in Visual Studio</span></span>

<span data-ttu-id="ec009-210">W programie Visual Studio można także [pominąć ostrzeżenia](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) za pomocą środowiska IDE.</span><span class="sxs-lookup"><span data-stu-id="ec009-210">When in Visual Studio, you can also [suppress warnings](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) through the IDE.</span></span>

## <a name="locking-dependencies"></a><span data-ttu-id="ec009-211">Blokowanie zależności</span><span class="sxs-lookup"><span data-stu-id="ec009-211">Locking dependencies</span></span>

<span data-ttu-id="ec009-212">*Ta funkcja jest dostępna w programie NuGet **4,9** lub nowszym oraz z programem Visual Studio 2017 **15,9** lub nowszym.*</span><span class="sxs-lookup"><span data-stu-id="ec009-212">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="ec009-213">Dane wejściowe do przywracania NuGet to zbiór odwołań do pakietów z pliku projektu (zależności najwyższego poziomu lub bezpośrednie), a dane wyjściowe to pełny zamknięcie wszystkich zależności pakietu, w tym zależności przechodnie.</span><span class="sxs-lookup"><span data-stu-id="ec009-213">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="ec009-214">Pakiet NuGet próbuje zawsze utworzyć to samo pełne zamknięcie zależności pakietów, jeśli lista wejściowa PackageReference nie została zmieniona.</span><span class="sxs-lookup"><span data-stu-id="ec009-214">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="ec009-215">Jednak istnieją pewne scenariusze, w których nie można tego zrobić.</span><span class="sxs-lookup"><span data-stu-id="ec009-215">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="ec009-216">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="ec009-216">For example:</span></span>

* <span data-ttu-id="ec009-217">W przypadku korzystania z wersji zmiennoprzecinkowych, takich jak `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span><span class="sxs-lookup"><span data-stu-id="ec009-217">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="ec009-218">Gdy zachodzi taka potrzeba, aby przepływać do najnowszej wersji przy każdym przywracaniu pakietów, istnieją scenariusze, w których użytkownicy wymagają, aby wykres był zablokowany do określonej najnowszej wersji i przepływał do nowszej wersji, o ile jest dostępny, przy jawnym gestie.</span><span class="sxs-lookup"><span data-stu-id="ec009-218">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="ec009-219">Opublikowana jest nowsza wersja pakietu spełniająca wymagania dotyczące wersji PackageReference.</span><span class="sxs-lookup"><span data-stu-id="ec009-219">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="ec009-220">Na przykład</span><span class="sxs-lookup"><span data-stu-id="ec009-220">E.g.</span></span> 

  * <span data-ttu-id="ec009-221">Dzień 1: Jeśli określono `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`, ale wersje dostępne w repozytoriach NuGet zostały 4.1.0, 4.2.0 i 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="ec009-221">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="ec009-222">W takim przypadku pakiet NuGet zostałby rozpoznany jako 4.1.0 (Najbliższa wersja minimalna)</span><span class="sxs-lookup"><span data-stu-id="ec009-222">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="ec009-223">Dzień 2: wersja 4.0.0 zostaje opublikowana.</span><span class="sxs-lookup"><span data-stu-id="ec009-223">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="ec009-224">Pakiet NuGet znajdzie teraz dokładne dopasowanie i zacznie rozwiązywać 4.0.0</span><span class="sxs-lookup"><span data-stu-id="ec009-224">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="ec009-225">Dana wersja pakietu jest usuwana z repozytorium.</span><span class="sxs-lookup"><span data-stu-id="ec009-225">A given package version is removed from the repository.</span></span> <span data-ttu-id="ec009-226">Chociaż nuget.org nie zezwala na usuwanie pakietów, te ograniczenia nie są dostępne dla wszystkich repozytoriów pakietów.</span><span class="sxs-lookup"><span data-stu-id="ec009-226">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="ec009-227">Spowoduje to znalezienie najlepszego dopasowania przez pakiet NuGet, gdy nie można rozwiązać go do usuniętej wersji.</span><span class="sxs-lookup"><span data-stu-id="ec009-227">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="ec009-228">Włączanie pliku blokady</span><span class="sxs-lookup"><span data-stu-id="ec009-228">Enabling lock file</span></span>

<span data-ttu-id="ec009-229">W celu utrwalenia pełnego zamknięcia zależności pakietu można wybrać funkcję blokowania pliku przez ustawienie właściwości programu MSBuild `RestorePackagesWithLockFile` dla projektu:</span><span class="sxs-lookup"><span data-stu-id="ec009-229">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="ec009-230">Jeśli ta właściwość jest ustawiona, przywracanie NuGet wygeneruje plik blokady `packages.lock.json` pliku w katalogu głównym projektu, który zawiera listę wszystkich zależności pakietu.</span><span class="sxs-lookup"><span data-stu-id="ec009-230">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="ec009-231">Gdy projekt ma `packages.lock.json` plik w katalogu głównym, plik blokady jest zawsze używany z przywracaniem, nawet jeśli właściwość `RestorePackagesWithLockFile` nie jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="ec009-231">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="ec009-232">Innym sposobem na zgodę na tę funkcję jest utworzenie fikcyjnego pustego pliku `packages.lock.json` w katalogu głównym projektu.</span><span class="sxs-lookup"><span data-stu-id="ec009-232">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="ec009-233">`restore` zachowanie przy użyciu pliku blokady</span><span class="sxs-lookup"><span data-stu-id="ec009-233">`restore` behavior with lock file</span></span>
<span data-ttu-id="ec009-234">Jeśli plik blokady jest obecny dla projektu, NuGet używa tego pliku blokady do uruchamiania `restore`.</span><span class="sxs-lookup"><span data-stu-id="ec009-234">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="ec009-235">Program NuGet sprawdza, czy w zależnościach pakietu zostały wprowadzone jakiekolwiek zmiany, jak wspomniano w pliku projektu (lub w plikach projektów zależnych) i czy nie wprowadzono żadnych zmian, po prostu przywraca pakiety wymienione w pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="ec009-235">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="ec009-236">Nie ma potrzeby ponownej oceny zależności pakietów.</span><span class="sxs-lookup"><span data-stu-id="ec009-236">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="ec009-237">Jeśli NuGet wykryje zmianę zdefiniowanych zależności, jak wspomniano w plikach projektu, ponownie oblicza Graf pakietu i aktualizuje plik blokady w celu odzwierciedlenia nowego zamknięcia pakietu dla projektu.</span><span class="sxs-lookup"><span data-stu-id="ec009-237">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="ec009-238">W przypadku ciągłej integracji/ciągłego wdrażania i innych scenariuszy, w których nie chcesz zmienić zależności pakietu na bieżąco, możesz to zrobić, ustawiając `lockedmode` `true`:</span><span class="sxs-lookup"><span data-stu-id="ec009-238">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="ec009-239">W przypadku programu dotnet. exe Uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="ec009-239">For dotnet.exe, run:</span></span>

```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="ec009-240">Dla programu MSBuild. exe Uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="ec009-240">For msbuild.exe, run:</span></span>

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="ec009-241">Możesz również ustawić tę właściwość warunkowego programu MSBuild w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="ec009-241">You may also set this conditional MSBuild property in your project file:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="ec009-242">Jeśli tryb blokowania jest `true`, przywracanie będzie przywracać dokładnie te pakiety jak wymienione w pliku blokady lub niepowodzenie, jeśli podczas tworzenia pliku blokady zostały zaktualizowane zdefiniowane zależności pakietu dla projektu.</span><span class="sxs-lookup"><span data-stu-id="ec009-242">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="ec009-243">Utwórz część pliku blokady w repozytorium źródłowym</span><span class="sxs-lookup"><span data-stu-id="ec009-243">Make lock file part of your source repository</span></span>
<span data-ttu-id="ec009-244">W przypadku kompilowania aplikacji plik wykonywalny i projekt w danym momencie znajdują się na początku łańcucha zależności, a następnie należy zaewidencjonować plik blokady do repozytorium kodu źródłowego, aby pakiet NuGet mógł go używać podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="ec009-244">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="ec009-245">Jeśli jednak projekt jest projektem biblioteki, który nie jest dostarczany lub wspólny projekt kodu, od którego zależą inne projekty, **nie należy** ewidencjonować pliku blokady jako części kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="ec009-245">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="ec009-246">Nie ma szkody w zachowaniu pliku blokady, ale zablokowane zależności pakietu dla wspólnego projektu kodu nie mogą być używane, jak wymieniono w pliku blokady podczas przywracania/kompilowania projektu, który zależy od tego projektu Common-Code.</span><span class="sxs-lookup"><span data-stu-id="ec009-246">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="ec009-247">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="ec009-247">Eg.</span></span>

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

<span data-ttu-id="ec009-248">Jeśli `ProjectA` ma zależność od wersji `PackageX` `2.0.0` a także odwołuje się do `ProjectB`, które są zależne od `PackageX` wersji `1.0.0`, wówczas plik blokady dla `ProjectB` zostanie wystawiony zależność od `PackageX` wersji `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="ec009-248">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="ec009-249">Jednak po skompilowaniu `ProjectA` jego plik blokady będzie zawierał zależność od wersji `PackageX` **`2.0.0`** a **nie** `1.0.0`, jak wymieniono w pliku blokady dla `ProjectB`.</span><span class="sxs-lookup"><span data-stu-id="ec009-249">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="ec009-250">W ten sposób plik blokady wspólnego projektu kodu ma niewielki stan dla projektów, które są od niego zależne.</span><span class="sxs-lookup"><span data-stu-id="ec009-250">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="ec009-251">Zablokuj rozszerzalność plików</span><span class="sxs-lookup"><span data-stu-id="ec009-251">Lock file extensibility</span></span>

<span data-ttu-id="ec009-252">Można kontrolować różne zachowania przywracania za pomocą pliku blokady zgodnie z poniższym opisem:</span><span class="sxs-lookup"><span data-stu-id="ec009-252">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="ec009-253">NuGet. exe — opcja</span><span class="sxs-lookup"><span data-stu-id="ec009-253">NuGet.exe option</span></span> | <span data-ttu-id="ec009-254">Opcja dotnet</span><span class="sxs-lookup"><span data-stu-id="ec009-254">dotnet option</span></span> | <span data-ttu-id="ec009-255">Odpowiednik opcji programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="ec009-255">MSBuild equivalent option</span></span> | <span data-ttu-id="ec009-256">Opis</span><span class="sxs-lookup"><span data-stu-id="ec009-256">Description</span></span> |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | <span data-ttu-id="ec009-257">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="ec009-257">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="ec009-258">Umożliwia użycie pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="ec009-258">Opts into the usage of a lock file.</span></span> |
| `-LockedMode` | `--locked-mode` | <span data-ttu-id="ec009-259">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="ec009-259">RestoreLockedMode</span></span> | <span data-ttu-id="ec009-260">Włącza tryb zablokowany do przywracania.</span><span class="sxs-lookup"><span data-stu-id="ec009-260">Enables locked mode for restore.</span></span> <span data-ttu-id="ec009-261">Jest to przydatne w scenariuszach ciągłej integracji/ciągłego wdrażania.</span><span class="sxs-lookup"><span data-stu-id="ec009-261">This is useful in CI/CD scenarios where you want repeatable builds.</span></span>|   
| `-ForceEvaluate` | `--force-evaluate` | <span data-ttu-id="ec009-262">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="ec009-262">RestoreForceEvaluate</span></span> | <span data-ttu-id="ec009-263">Ta opcja jest przydatna w przypadku pakietów z wersją zmiennoprzecinkową zdefiniowaną w projekcie.</span><span class="sxs-lookup"><span data-stu-id="ec009-263">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="ec009-264">Domyślnie przywracanie pakietu NuGet nie będzie automatycznie aktualizować wersji programu przy każdym przywracaniu, chyba że zostanie uruchomiony przycisk Przywróć z tą opcją.</span><span class="sxs-lookup"><span data-stu-id="ec009-264">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with this option.</span></span> |
| `-LockFilePath` | `--lock-file-path` | <span data-ttu-id="ec009-265">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="ec009-265">NuGetLockFilePath</span></span> | <span data-ttu-id="ec009-266">Definiuje niestandardową lokalizację pliku blokady dla projektu.</span><span class="sxs-lookup"><span data-stu-id="ec009-266">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="ec009-267">Domyślnie NuGet obsługuje `packages.lock.json` w katalogu głównym.</span><span class="sxs-lookup"><span data-stu-id="ec009-267">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="ec009-268">Jeśli masz wiele projektów w tym samym katalogu, pakiet NuGet obsługuje plik blokady specyficzny dla projektu `packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="ec009-268">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
