---
title: Format PackageReference pakietu NuGet (odwołania do pakietu w plikach projektu)
description: Szczegóły dotyczące odszukania pakietów NuGet w plikach projektu obsługiwanych przez pakiety NuGet 4.0+ i VS2017 oraz .NET Core 2.0
author: nkolev92
ms.author: nikolev
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: c7b963352e0e9640844a213767a58c883ed0eeb9
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323716"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="8ea3a-103">Odwołania do pakietu ( `PackageReference` ) w plikach projektu</span><span class="sxs-lookup"><span data-stu-id="8ea3a-103">Package references (`PackageReference`) in project files</span></span>

<span data-ttu-id="8ea3a-104">Odwołania do pakietu, używając węzła, zarządzają zależnościami NuGet bezpośrednio w plikach `PackageReference` projektu (w przeciwieństwie do oddzielnego `packages.config` pliku).</span><span class="sxs-lookup"><span data-stu-id="8ea3a-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="8ea3a-105">Wywoływanie funkcji PackageReference nie ma wpływu na inne aspekty narzędzia NuGet. na przykład ustawienia w plikach (w tym źródła pakietów) są nadal stosowane, jak wyjaśniono w `NuGet.Config` tece [Common NuGet configurations (Typowe konfiguracje nuGet).](configuring-nuget-behavior.md)</span><span class="sxs-lookup"><span data-stu-id="8ea3a-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="8ea3a-106">Za pomocą funkcji PackageReference można również użyć warunków programu MSBuild, aby wybrać odwołania do pakietu na platformę docelową lub inne grupowania.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, or other groupings.</span></span> <span data-ttu-id="8ea3a-107">Umożliwia również ujednolicać kontrolę nad zależnościami i przepływem zawartości.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="8ea3a-108">(Zobacz , aby uzyskać więcej szczegółów [na temat pakietu NuGet i przywracania jako obiektów docelowych MSBuild).](../reference/msbuild-targets.md)</span><span class="sxs-lookup"><span data-stu-id="8ea3a-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="8ea3a-109">Obsługa typów projektów</span><span class="sxs-lookup"><span data-stu-id="8ea3a-109">Project type support</span></span>

<span data-ttu-id="8ea3a-110">Domyślnie packageReference jest używany dla projektów platformy .NET Core, projektów platformy .NET Standard i projektów platformy UWP przeznaczonych dla programu Windows 10 Build 15063 (aktualizacja dla twórców) i nowszych, z wyjątkiem projektów platformy UWP w języku C++.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="8ea3a-111">.NET Framework obsługują packageReference, ale obecnie domyślnie są to `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="8ea3a-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="8ea3a-112">Aby użyć packageReference, [zmigruj](../consume-packages/migrate-packages-config-to-package-reference.md) zależności z do pliku projektu, a `packages.config` następnie usuń packages.config.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="8ea3a-113">ASP.NET przeznaczone dla pełnego .NET Framework obejmują tylko [ograniczoną obsługę](https://github.com/NuGet/Home/issues/5877) packageReference.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="8ea3a-114">Typy projektów C++ i JavaScript nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="8ea3a-115">Dodawanie packageReference</span><span class="sxs-lookup"><span data-stu-id="8ea3a-115">Adding a PackageReference</span></span>

<span data-ttu-id="8ea3a-116">Dodaj zależność w pliku projektu przy użyciu następującej składni:</span><span class="sxs-lookup"><span data-stu-id="8ea3a-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="8ea3a-117">Kontrolowanie wersji zależności</span><span class="sxs-lookup"><span data-stu-id="8ea3a-117">Controlling dependency version</span></span>

<span data-ttu-id="8ea3a-118">Konwencja określania wersji pakietu jest taka sama jak w przypadku korzystania z programu `packages.config` :</span><span class="sxs-lookup"><span data-stu-id="8ea3a-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="8ea3a-119">W powyższym przykładzie wersja 3.6.0 oznacza dowolną wersję, która jest >=3.6.0 z preferencjami dla najniższej wersji, zgodnie z opisem w tece [Wersje pakietu](../concepts/package-versioning.md#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="8ea3a-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="8ea3a-120">Używanie packageReference dla projektu bez packageReferences</span><span class="sxs-lookup"><span data-stu-id="8ea3a-120">Using PackageReference for a project with no PackageReferences</span></span>

<span data-ttu-id="8ea3a-121">Zaawansowane: jeśli w projekcie nie ma zainstalowanych pakietów (nie ma żadnych odczekań PackageReferences w pliku projektu ani pliku packages.config), ale chcesz, aby projekt został przywrócony jako styl PackageReference, możesz ustawić właściwość Project RestoreProjectStyle na PackageReference w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="8ea3a-122">Może to być przydatne, jeśli odwołujesz się do projektów w stylu PackageReference (istniejących projektów w stylu csproj lub SDK).</span><span class="sxs-lookup"><span data-stu-id="8ea3a-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="8ea3a-123">Dzięki temu pakiety, do których odwołują się te projekty, będą "przechodnie", do których odwołuje się projekt.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="packagereference-and-sources"></a><span data-ttu-id="8ea3a-124">PackageReference i źródła</span><span class="sxs-lookup"><span data-stu-id="8ea3a-124">PackageReference and sources</span></span>

<span data-ttu-id="8ea3a-125">W projektach PackageReference wersje zależności przechodniej są rozwiązywane podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-125">In PackageReference projects, the transitive dependency versions are resolved at restore time.</span></span> <span data-ttu-id="8ea3a-126">W związku z tym w projektach PackageReference wszystkie źródła muszą być dostępne dla wszystkich przywracania.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-126">As such, in PackageReference projects all sources need to be available for all restores.</span></span> 

## <a name="floating-versions"></a><span data-ttu-id="8ea3a-127">Wersje zmiennoprzecinkowe</span><span class="sxs-lookup"><span data-stu-id="8ea3a-127">Floating Versions</span></span>

<span data-ttu-id="8ea3a-128">[Wersje zmiennoprzecinkowe](../concepts/dependency-resolution.md#floating-versions) są obsługiwane za pomocą programu `PackageReference` :</span><span class="sxs-lookup"><span data-stu-id="8ea3a-128">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="8ea3a-129">Kontrolowanie zasobów zależności</span><span class="sxs-lookup"><span data-stu-id="8ea3a-129">Controlling dependency assets</span></span>

<span data-ttu-id="8ea3a-130">Zależność może być wyłącznie usługą dewelopera i nie chcesz jej ujawniać w projektach, które będą korzystać z pakietu.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-130">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="8ea3a-131">W tym scenariuszu można kontrolować `PrivateAssets` to zachowanie za pomocą metadanych.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-131">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="8ea3a-132">Następujące tagi metadanych kontrolują zasoby zależności:</span><span class="sxs-lookup"><span data-stu-id="8ea3a-132">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="8ea3a-133">Tag</span><span class="sxs-lookup"><span data-stu-id="8ea3a-133">Tag</span></span> | <span data-ttu-id="8ea3a-134">Description</span><span class="sxs-lookup"><span data-stu-id="8ea3a-134">Description</span></span> | <span data-ttu-id="8ea3a-135">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="8ea3a-135">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8ea3a-136">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="8ea3a-136">IncludeAssets</span></span> | <span data-ttu-id="8ea3a-137">Te zasoby zostaną zużyte</span><span class="sxs-lookup"><span data-stu-id="8ea3a-137">These assets will be consumed</span></span> | <span data-ttu-id="8ea3a-138">all</span><span class="sxs-lookup"><span data-stu-id="8ea3a-138">all</span></span> |
| <span data-ttu-id="8ea3a-139">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="8ea3a-139">ExcludeAssets</span></span> | <span data-ttu-id="8ea3a-140">Te zasoby nie będą używane</span><span class="sxs-lookup"><span data-stu-id="8ea3a-140">These assets will not be consumed</span></span> | <span data-ttu-id="8ea3a-141">brak</span><span class="sxs-lookup"><span data-stu-id="8ea3a-141">none</span></span> |
| <span data-ttu-id="8ea3a-142">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="8ea3a-142">PrivateAssets</span></span> | <span data-ttu-id="8ea3a-143">Te zasoby zostaną zużyte, ale nie będą przepływać do projektu nadrzędnego</span><span class="sxs-lookup"><span data-stu-id="8ea3a-143">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="8ea3a-144">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="8ea3a-144">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="8ea3a-145">Dopuszczalne wartości dla tych tagów są następujące: wiele wartości rozdzielonych średnikami z wyjątkiem i , `all` które muszą być wyświetlane `none` samodzielnie:</span><span class="sxs-lookup"><span data-stu-id="8ea3a-145">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="8ea3a-146">Wartość</span><span class="sxs-lookup"><span data-stu-id="8ea3a-146">Value</span></span> | <span data-ttu-id="8ea3a-147">Opis</span><span class="sxs-lookup"><span data-stu-id="8ea3a-147">Description</span></span> |
| --- | ---
| <span data-ttu-id="8ea3a-148">kompilowanie</span><span class="sxs-lookup"><span data-stu-id="8ea3a-148">compile</span></span> | <span data-ttu-id="8ea3a-149">Zawartość folderu `lib` i określa, czy projekt można skompilować względem zestawów w folderze</span><span class="sxs-lookup"><span data-stu-id="8ea3a-149">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="8ea3a-150">środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="8ea3a-150">runtime</span></span> | <span data-ttu-id="8ea3a-151">Zawartość folderu i i określa, czy te zestawy zostaną skopiowane do `lib` `runtimes` katalogu wyjściowego kompilacji</span><span class="sxs-lookup"><span data-stu-id="8ea3a-151">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="8ea3a-152">contentFiles</span><span class="sxs-lookup"><span data-stu-id="8ea3a-152">contentFiles</span></span> | <span data-ttu-id="8ea3a-153">Zawartość `contentfiles` folderu</span><span class="sxs-lookup"><span data-stu-id="8ea3a-153">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="8ea3a-154">kompilacja</span><span class="sxs-lookup"><span data-stu-id="8ea3a-154">build</span></span> | <span data-ttu-id="8ea3a-155">`.props` i `.targets` w `build` folderze</span><span class="sxs-lookup"><span data-stu-id="8ea3a-155">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="8ea3a-156">buildMultitargeting</span><span class="sxs-lookup"><span data-stu-id="8ea3a-156">buildMultitargeting</span></span> | <span data-ttu-id="8ea3a-157">*(4.0)* i w folderze do określania `.props` `.targets` celu między `buildMultitargeting` platformami</span><span class="sxs-lookup"><span data-stu-id="8ea3a-157">*(4.0)* `.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="8ea3a-158">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="8ea3a-158">buildTransitive</span></span> | <span data-ttu-id="8ea3a-159">*(5.0+)* `.props` i `.targets` w `buildTransitive` folderze dla zasobów, które są przechodnie do dowolnego projektu zużywającego zasoby.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-159">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="8ea3a-160">Zobacz stronę [funkcji.](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior)</span><span class="sxs-lookup"><span data-stu-id="8ea3a-160">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="8ea3a-161">Analizatory</span><span class="sxs-lookup"><span data-stu-id="8ea3a-161">analyzers</span></span> | <span data-ttu-id="8ea3a-162">Analizatory .NET</span><span class="sxs-lookup"><span data-stu-id="8ea3a-162">.NET analyzers</span></span> |
| <span data-ttu-id="8ea3a-163">natywne</span><span class="sxs-lookup"><span data-stu-id="8ea3a-163">native</span></span> | <span data-ttu-id="8ea3a-164">Zawartość `native` folderu</span><span class="sxs-lookup"><span data-stu-id="8ea3a-164">Contents of the `native` folder</span></span> |
| <span data-ttu-id="8ea3a-165">brak</span><span class="sxs-lookup"><span data-stu-id="8ea3a-165">none</span></span> | <span data-ttu-id="8ea3a-166">Żadne z powyższych nie są używane.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-166">None of the above are used.</span></span> |
| <span data-ttu-id="8ea3a-167">all</span><span class="sxs-lookup"><span data-stu-id="8ea3a-167">all</span></span> | <span data-ttu-id="8ea3a-168">Wszystkie powyższe (z wyjątkiem `none` )</span><span class="sxs-lookup"><span data-stu-id="8ea3a-168">All of the above (except `none`)</span></span> |

<span data-ttu-id="8ea3a-169">W poniższym przykładzie wszystkie elementy oprócz plików zawartości z pakietu będą używane przez projekt, a wszystkie elementy oprócz plików zawartości i analizatorów będą przepływać do projektu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-169">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="8ea3a-170">Należy pamiętać, że ponieważ element nie jest dołączony do elementu , obiekty docelowe i `build` `PrivateAssets` rekwizyty *będą* przepływać do projektu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-170">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="8ea3a-171">Rozważmy na przykład, że powyższe odwołanie jest używane w projekcie, który tworzy pakiet NuGet o nazwie AppLogger.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-171">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="8ea3a-172">Program AppLogger może korzystać z obiektów docelowych i obiektów prop z `Contoso.Utility.UsefulStuff` , podobnie jak projekty, które zużywają program AppLogger.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-172">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="8ea3a-173">Jeśli w pliku jest ustawiona wartość , oznacza to pakiet jako zależność tylko do projektowania, co uniemożliwia uwzględnianie pakietu jako zależności w `developmentDependency` `true` innych `.nuspec` pakietach.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-173">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="8ea3a-174">W przypadku pakietu PackageReference *(NuGet 4.8+)* ta flaga oznacza również, że wyklucza z kompilacji zasoby czasu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-174">With PackageReference *(NuGet 4.8+)*, this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="8ea3a-175">Aby uzyskać więcej informacji, zobacz [DevelopmentDependency support for PackageReference (Obsługa zależności dla packageReference).](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="8ea3a-175">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="8ea3a-176">Dodawanie warunku PackageReference</span><span class="sxs-lookup"><span data-stu-id="8ea3a-176">Adding a PackageReference condition</span></span>

<span data-ttu-id="8ea3a-177">Można użyć warunku do kontrolowania, czy pakiet jest dołączony, gdzie warunki mogą używać dowolnej zmiennej MSBuild lub zmiennej zdefiniowanej w pliku obiektów docelowych lub props.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-177">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="8ea3a-178">Jednak obecnie obsługiwana jest `TargetFramework` tylko zmienna .</span><span class="sxs-lookup"><span data-stu-id="8ea3a-178">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="8ea3a-179">Załóżmy na przykład, że cel jest docelowy, ale ma zależność, która `netstandard1.4` ma zastosowanie tylko do `net452` . `net452`</span><span class="sxs-lookup"><span data-stu-id="8ea3a-179">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="8ea3a-180">W takim przypadku nie chcesz, aby projekt, który zużywa `netstandard1.4` pakiet, dodać tę niepotrzebną zależność.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-180">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="8ea3a-181">Aby temu zapobiec, należy określić warunek w `PackageReference` następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="8ea3a-181">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="8ea3a-182">Pakiet sbudowaną przy użyciu tego projektu pokaże, że Newtonsoft.Jsjest uwzględniony jako zależność tylko dla obiektu `net452` docelowego:</span><span class="sxs-lookup"><span data-stu-id="8ea3a-182">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Wynik zastosowania warunku w pakiecie PackageReference w programie VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="8ea3a-184">Warunki można również stosować na `ItemGroup` poziomie i dotyczyć wszystkich elementów `PackageReference` kluczowych:</span><span class="sxs-lookup"><span data-stu-id="8ea3a-184">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a><span data-ttu-id="8ea3a-185">GeneratePathProperty</span><span class="sxs-lookup"><span data-stu-id="8ea3a-185">GeneratePathProperty</span></span>

<span data-ttu-id="8ea3a-186">Ta funkcja jest dostępna w pniu NuGet **5.0** lub jego wersji 5.0 lub jego wersji Visual Studio 2019 **16.0** lub jego wersji.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-186">This feature is available with NuGet **5.0** or above and with Visual Studio 2019 **16.0** or above.</span></span>

<span data-ttu-id="8ea3a-187">Czasami pożądane jest odwołanie do plików w pakiecie z obiektu docelowego MSBuild.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-187">Sometimes it is desirable to reference files in a package from an MSBuild target.</span></span>
<span data-ttu-id="8ea3a-188">W `packages.config` projektach opartych pakiety są instalowane w folderze względem pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-188">In `packages.config` based projects, the packages are installed in a folder relative to the project file.</span></span> <span data-ttu-id="8ea3a-189">Jednak w przypadku packageReference [](../concepts/package-installation-process.md) pakiety są używane z folderu *global-packages,* który może się różnić w zależności od komputera.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-189">However in PackageReference, the packages are [consumed](../concepts/package-installation-process.md) from the *global-packages* folder, which can vary from machine to machine.</span></span>

<span data-ttu-id="8ea3a-190">Aby wypełnić tę lukę, program NuGet wprowadził właściwość, która wskazuje lokalizację, z której zostanie zużyty pakiet.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-190">To bridge that gap, NuGet introduced a property that points to the location from which the package will be consumed.</span></span>

<span data-ttu-id="8ea3a-191">Przykład:</span><span class="sxs-lookup"><span data-stu-id="8ea3a-191">Example:</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

<span data-ttu-id="8ea3a-192">Ponadto narzędzie NuGet automatycznie wygeneruje właściwości dla pakietów zawierających folder narzędzi.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-192">Additionally NuGet will automatically generate properties for packages containing a tools folder.</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
```

<span data-ttu-id="8ea3a-193">Właściwości i tożsamości pakietów programu MSBuild nie mają tych samych ograniczeń, dlatego tożsamość pakietu musi zostać zmieniona na przyjazną nazwę msBuild poprzedzoną słowem `Pkg` .</span><span class="sxs-lookup"><span data-stu-id="8ea3a-193">MSBuild properties and package identities do not have the same restrictions so the package identity needs to be changed to an MSBuild friendly name, prefixed by the word `Pkg`.</span></span>
<span data-ttu-id="8ea3a-194">Aby sprawdzić dokładną nazwę wygenerowanej właściwości, przyjrzyj się [wygenerowanemu plikowi nuget.g.props.](../reference/msbuild-targets.md#restore-outputs)</span><span class="sxs-lookup"><span data-stu-id="8ea3a-194">To verify the exact name of the property generated, look at the generated [nuget.g.props](../reference/msbuild-targets.md#restore-outputs) file.</span></span>

## <a name="packagereference-aliases"></a><span data-ttu-id="8ea3a-195">PackageReference Aliases</span><span class="sxs-lookup"><span data-stu-id="8ea3a-195">PackageReference Aliases</span></span>

<span data-ttu-id="8ea3a-196">W niektórych rzadkich przypadkach różne pakiety będą zawierać klasy w tej samej przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-196">In some rare instances different packages will contain classes in the same namespace.</span></span> <span data-ttu-id="8ea3a-197">Począwszy od wersji NuGet 5.7 & Visual Studio 2019 Update 7, równoważnej wnioskowi ProjectReference, packageReference obsługuje funkcję [`Aliases`](/dotnet/api/microsoft.codeanalysis.projectreference.aliases) .</span><span class="sxs-lookup"><span data-stu-id="8ea3a-197">Starting with NuGet 5.7 & Visual Studio 2019 Update 7, equivalent to ProjectReference, PackageReference supports [`Aliases`](/dotnet/api/microsoft.codeanalysis.projectreference.aliases).</span></span>
<span data-ttu-id="8ea3a-198">Domyślnie aliasy nie są udostępniane.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-198">By default no aliases are provided.</span></span> <span data-ttu-id="8ea3a-199">Jeśli określono alias, *wszystkie* zestawy pochodzące z pakietu z adnotacjami muszą być przywołyne przy użyciu aliasu.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-199">When an alias is specified, *all* assemblies coming from the annotated package with need to be referenced with an alias.</span></span>

<span data-ttu-id="8ea3a-200">Przykładowe użycie można sprawdzić w folderze [NuGet\Samples](https://github.com/NuGet/Samples/tree/main/PackageReferenceAliasesExample)</span><span class="sxs-lookup"><span data-stu-id="8ea3a-200">You can look at sample usage at [NuGet\Samples](https://github.com/NuGet/Samples/tree/main/PackageReferenceAliasesExample)</span></span>

<span data-ttu-id="8ea3a-201">W pliku projektu określ aliasy w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="8ea3a-201">In the project file, specify the aliases as follows:</span></span>

```xml
  <ItemGroup>
    <PackageReference Include="NuGet.Versioning" Version="5.8.0" Aliases="ExampleAlias" />
  </ItemGroup>
```

<span data-ttu-id="8ea3a-202">W kodzie użyj go w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="8ea3a-202">and in the code use it as follows:</span></span>

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

## <a name="nuget-warnings-and-errors"></a><span data-ttu-id="8ea3a-203">Ostrzeżenia i błędy nuGet</span><span class="sxs-lookup"><span data-stu-id="8ea3a-203">NuGet warnings and errors</span></span>

<span data-ttu-id="8ea3a-204">*Ta funkcja jest dostępna w pniu NuGet **4.3** lub jego wersji i Visual Studio 2017 **15.3** lub jego wersji.*</span><span class="sxs-lookup"><span data-stu-id="8ea3a-204">*This feature is available with NuGet **4.3** or above and with Visual Studio 2017 **15.3** or above.*</span></span>

<span data-ttu-id="8ea3a-205">W przypadku wielu scenariuszy pakowania i przywracania wszystkie ostrzeżenia i błędy NuGet są kodowane i zaczynają się od `NU****` .</span><span class="sxs-lookup"><span data-stu-id="8ea3a-205">For many pack and restore scenarios, all NuGet warnings and errors are coded, and start with `NU****`.</span></span> <span data-ttu-id="8ea3a-206">Wszystkie ostrzeżenia i błędy programu NuGet są wymienione w [dokumentacji referencyjnej.](../reference/errors-and-warnings.md)</span><span class="sxs-lookup"><span data-stu-id="8ea3a-206">All NuGet warnings and errors are listed in the [reference](../reference/errors-and-warnings.md) documentation.</span></span>

<span data-ttu-id="8ea3a-207">NuGet obserwuje następujące właściwości ostrzeżenia:</span><span class="sxs-lookup"><span data-stu-id="8ea3a-207">NuGet observes the following warning properties:</span></span>

- <span data-ttu-id="8ea3a-208">`TreatWarningsAsErrors`, traktuj wszystkie ostrzeżenia jako błędy</span><span class="sxs-lookup"><span data-stu-id="8ea3a-208">`TreatWarningsAsErrors`, treat all warnings as errors</span></span>
- <span data-ttu-id="8ea3a-209">`WarningsAsErrors`, traktuj określone ostrzeżenia jako błędy</span><span class="sxs-lookup"><span data-stu-id="8ea3a-209">`WarningsAsErrors`, treat specific warnings as errors</span></span>
- <span data-ttu-id="8ea3a-210">`NoWarn`— ukrywa określone ostrzeżenia dla całego projektu lub całego pakietu.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-210">`NoWarn`, hide specific warnings, either project-wide or package-wide.</span></span>

<span data-ttu-id="8ea3a-211">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="8ea3a-211">Examples:</span></span>

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

### <a name="suppressing-nuget-warnings"></a><span data-ttu-id="8ea3a-212">Pomijanie ostrzeżeń nuGet</span><span class="sxs-lookup"><span data-stu-id="8ea3a-212">Suppressing NuGet warnings</span></span>

<span data-ttu-id="8ea3a-213">Chociaż zaleca się rozwiązanie wszystkich ostrzeżeń NuGet podczas operacji pakowania i przywracania, w niektórych sytuacjach ich pomijanie jest uzasadnione.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-213">While it is recommended that you resolve all NuGet warnings during your pack and restore operations, in certain situations suppressing them is warranted.</span></span>
<span data-ttu-id="8ea3a-214">Aby pominąć projekt ostrzeżenia w całym projekcie, rozważ wykonanie:</span><span class="sxs-lookup"><span data-stu-id="8ea3a-214">To suppress a warning project wide, consider doing:</span></span>

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

<span data-ttu-id="8ea3a-215">Czasami ostrzeżenia dotyczą tylko określonego pakietu w grafie.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-215">Sometimes warnings apply only to a certain package in the graph.</span></span> <span data-ttu-id="8ea3a-216">Możemy bardziej selektywnie pominąć to ostrzeżenie, dodając element `NoWarn` w pozycji PackageReference.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-216">We can choose to suppress that warning more selectively by adding a `NoWarn` on the PackageReference item.</span></span> 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a><span data-ttu-id="8ea3a-217">Pomijanie ostrzeżeń pakietu NuGet w Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8ea3a-217">Suppressing NuGet package warnings in Visual Studio</span></span>

<span data-ttu-id="8ea3a-218">W przypadku Visual Studio można również [pominąć ostrzeżenia za](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) pośrednictwem środowiska IDE.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-218">When in Visual Studio, you can also [suppress warnings](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) through the IDE.</span></span>

## <a name="locking-dependencies"></a><span data-ttu-id="8ea3a-219">Blokowanie zależności</span><span class="sxs-lookup"><span data-stu-id="8ea3a-219">Locking dependencies</span></span>

<span data-ttu-id="8ea3a-220">*Ta funkcja jest dostępna w pniu NuGet **4.9** lub jego wersji i Visual Studio 2017 w wersji **15.9** lub powyższej.*</span><span class="sxs-lookup"><span data-stu-id="8ea3a-220">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="8ea3a-221">Dane wejściowe przywracania pakietów NuGet to zestaw odwołań do pakietów z pliku projektu (zależności najwyższego poziomu lub bezpośrednie), a dane wyjściowe są pełnym zamknięciem wszystkich zależności pakietu, w tym zależności przechodniej.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-221">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="8ea3a-222">Program NuGet próbuje zawsze utworzyć to samo pełne zamknięcie zależności pakietów, jeśli wejściowa lista PackageReference nie zmieniła się.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-222">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="8ea3a-223">Istnieją jednak pewne scenariusze, w których nie jest to możliwe.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-223">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="8ea3a-224">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="8ea3a-224">For example:</span></span>

* <span data-ttu-id="8ea3a-225">W przypadku używania wersji zmiennoprzecinowych, takich jak `<PackageReference Include="My.Sample.Lib" Version="4.*"/>` .</span><span class="sxs-lookup"><span data-stu-id="8ea3a-225">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="8ea3a-226">W tym przypadku celem jest przesłonięcia do najnowszej wersji przy każdym przywróceniu pakietów, jednak istnieją scenariusze, w których użytkownicy wymagają, aby graf był zablokowany dla określonej najnowszej wersji i zmiennoprzecinkowy do nowszej wersji, jeśli jest dostępny, przy jawnym gestie.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-226">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="8ea3a-227">Opublikowano nowszą wersję pakietu pasującą do wymagań dotyczących wersji packageReference.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-227">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="8ea3a-228">Na przykład</span><span class="sxs-lookup"><span data-stu-id="8ea3a-228">E.g.</span></span> 

  * <span data-ttu-id="8ea3a-229">Dzień 1: jeśli określono wersję, ale wersje dostępne w repozytoriach `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` NuGet to 4.1.0, 4.2.0 i 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-229">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="8ea3a-230">W tym przypadku rozwiązanie NuGet zostanie rozpoznane jako 4.1.0 (najbliższa minimalna wersja)</span><span class="sxs-lookup"><span data-stu-id="8ea3a-230">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="8ea3a-231">Dzień 2. Opublikowanie wersji 4.0.0.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-231">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="8ea3a-232">NuGet teraz znajdzie dokładne dopasowanie i rozpocznie rozpoznawanie do 4.0.0</span><span class="sxs-lookup"><span data-stu-id="8ea3a-232">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="8ea3a-233">Danej wersji pakietu jest usuwana z repozytorium.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-233">A given package version is removed from the repository.</span></span> <span data-ttu-id="8ea3a-234">Chociaż nuget.org nie zezwala na usunięcie pakietów, nie wszystkie repozytoria pakietów mają takie ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-234">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="8ea3a-235">Powoduje to znalezienie najlepszego dopasowania przez program NuGet, gdy nie można go rozpoznać do usuniętej wersji.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-235">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="8ea3a-236">Włączanie pliku blokady</span><span class="sxs-lookup"><span data-stu-id="8ea3a-236">Enabling lock file</span></span>

<span data-ttu-id="8ea3a-237">Aby utrwalić pełne zamknięcie zależności pakietów, możesz wyrazić zgodę na funkcję pliku blokady, ustawiając właściwość MSBuild `RestorePackagesWithLockFile` dla projektu:</span><span class="sxs-lookup"><span data-stu-id="8ea3a-237">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="8ea3a-238">Jeśli ta właściwość jest ustawiona, przywracanie NuGet wygeneruje plik blokady — plik w katalogu głównym projektu, który zawiera listę `packages.lock.json` wszystkich zależności pakietów.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-238">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="8ea3a-239">Gdy plik projektu znajduje się w katalogu głównym, plik blokady jest zawsze używany z `packages.lock.json` przywracaniem, nawet jeśli właściwość nie jest `RestorePackagesWithLockFile` ustawiona.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-239">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="8ea3a-240">Innym sposobem, aby wyrazić zgodę na tę funkcję, jest utworzenie fikcyjnego pustego pliku w `packages.lock.json` katalogu głównym projektu.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-240">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="8ea3a-241">`restore` zachowanie w przypadku pliku blokady</span><span class="sxs-lookup"><span data-stu-id="8ea3a-241">`restore` behavior with lock file</span></span>
<span data-ttu-id="8ea3a-242">Jeśli w projekcie znajduje się plik blokady, program NuGet używa tego pliku blokady do uruchomienia pliku `restore` .</span><span class="sxs-lookup"><span data-stu-id="8ea3a-242">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="8ea3a-243">Program NuGet szybko sprawdza, czy w zależnościach pakietu zostały wprowadzone jakieś zmiany, jak wspomniano w pliku projektu (lub w plikach projektów zależnych), a jeśli nie zostały wprowadzone żadne zmiany, przywraca tylko pakiety wymienione w pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-243">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="8ea3a-244">Nie ma możliwości ponownej oceny zależności pakietów.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-244">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="8ea3a-245">Jeśli program NuGet wykryje zmianę zdefiniowanych zależności, jak wspomniano w plikach projektu, ponownie oceni wykres pakietu i aktualizuje plik blokady, aby odzwierciedlić nowe zamknięcie pakietu dla projektu.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-245">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="8ea3a-246">W przypadku scenariuszy z ciasną/cd i innymi scenariuszami, w których nie chcesz zmieniać zależności pakietów na bieżąco, możesz to zrobić, ustawiając `lockedmode` na `true` :</span><span class="sxs-lookup"><span data-stu-id="8ea3a-246">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="8ea3a-247">Aby dotnet.exe, uruchom:</span><span class="sxs-lookup"><span data-stu-id="8ea3a-247">For dotnet.exe, run:</span></span>

```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="8ea3a-248">Aby msbuild.exe, uruchom:</span><span class="sxs-lookup"><span data-stu-id="8ea3a-248">For msbuild.exe, run:</span></span>

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="8ea3a-249">Możesz również ustawić tę warunkową właściwość MSBuild w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="8ea3a-249">You may also set this conditional MSBuild property in your project file:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="8ea3a-250">Jeśli tryb zablokowany to , przywracanie spowoduje przywrócenie dokładnych pakietów wymienionych w pliku blokady lub niepowodzenie w przypadku zaktualizowania zdefiniowanych zależności pakietu dla projektu po utworzeniu `true` pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-250">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="8ea3a-251">Make lock file part of your source repository (Blokowanie pliku w repozytorium źródłowym)</span><span class="sxs-lookup"><span data-stu-id="8ea3a-251">Make lock file part of your source repository</span></span>
<span data-ttu-id="8ea3a-252">Jeśli tworzyć aplikację, plik wykonywalny i projekt, których dotyczy ten projekt, znajdują się na początku łańcucha zależności, należy zaewidencjonić plik blokady w repozytorium kodu źródłowego, aby nuGet można było z niego korzystać podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-252">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="8ea3a-253">Jeśli jednak projekt jest projektem biblioteki, którego nie wysyłasz, lub wspólnym projektem  kodu, od którego zależą inne projekty, nie należy sprawdzać pliku blokady jako części kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-253">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="8ea3a-254">Przechowywanie pliku blokady nie ma żadnych szkód, ale zablokowane zależności pakietu dla wspólnego projektu kodu mogą nie być używane, jak podano w pliku blokady, podczas przywracania/kompilowania projektu, który zależy od tego wspólnego projektu kodu.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-254">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="8ea3a-255">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="8ea3a-255">Eg.</span></span>

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

<span data-ttu-id="8ea3a-256">Jeśli ma zależność od wersji, a także odwołania, które zależą od wersji , plik blokady dla pliku będzie `ProjectA` `PackageX` `2.0.0` `ProjectB` `PackageX` `1.0.0` `ProjectB` zawierał zależność od `PackageX` wersji `1.0.0` .</span><span class="sxs-lookup"><span data-stu-id="8ea3a-256">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="8ea3a-257">Jednak podczas budowana wersja pliku blokady będzie zawierać zależność od wersji, a nie jak podano w `ProjectA` pliku blokady dla programu `PackageX` **`2.0.0`**  `1.0.0` `ProjectB` .</span><span class="sxs-lookup"><span data-stu-id="8ea3a-257">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="8ea3a-258">W związku z tym plik blokady wspólnego projektu kodu ma niewiele informacji o pakietach rozpoznanych dla projektów, które od niego zależą.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-258">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="8ea3a-259">Blokowanie rozszerzalności plików</span><span class="sxs-lookup"><span data-stu-id="8ea3a-259">Lock file extensibility</span></span>

<span data-ttu-id="8ea3a-260">Możesz kontrolować różne zachowania przywracania za pomocą pliku blokady, jak opisano poniżej:</span><span class="sxs-lookup"><span data-stu-id="8ea3a-260">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="8ea3a-261">NuGet.exe opcji</span><span class="sxs-lookup"><span data-stu-id="8ea3a-261">NuGet.exe option</span></span> | <span data-ttu-id="8ea3a-262">dotnet option (opcja dotnet)</span><span class="sxs-lookup"><span data-stu-id="8ea3a-262">dotnet option</span></span> | <span data-ttu-id="8ea3a-263">Równoważna opcja msBuild</span><span class="sxs-lookup"><span data-stu-id="8ea3a-263">MSBuild equivalent option</span></span> | <span data-ttu-id="8ea3a-264">Opis</span><span class="sxs-lookup"><span data-stu-id="8ea3a-264">Description</span></span> |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | <span data-ttu-id="8ea3a-265">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="8ea3a-265">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="8ea3a-266">Decyduje się na użycie pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-266">Opts into the usage of a lock file.</span></span> |
| `-LockedMode` | `--locked-mode` | <span data-ttu-id="8ea3a-267">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="8ea3a-267">RestoreLockedMode</span></span> | <span data-ttu-id="8ea3a-268">Włącza tryb zablokowany dla przywracania.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-268">Enables locked mode for restore.</span></span> <span data-ttu-id="8ea3a-269">Jest to przydatne w scenariuszach z ciasną/cd, w których chcesz tworzyć powtarzalne kompilacje.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-269">This is useful in CI/CD scenarios where you want repeatable builds.</span></span>|   
| `-ForceEvaluate` | `--force-evaluate` | <span data-ttu-id="8ea3a-270">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="8ea3a-270">RestoreForceEvaluate</span></span> | <span data-ttu-id="8ea3a-271">Ta opcja jest przydatna w przypadku pakietów z wersją zmiennoprzecową zdefiniowaną w projekcie.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-271">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="8ea3a-272">Domyślnie przywracanie NuGet nie aktualizuje wersji pakietu automatycznie przy każdym przywróceniu, chyba że zostanie uruchomione przywracanie przy użyciu tej opcji.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-272">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with this option.</span></span> |
| `-LockFilePath` | `--lock-file-path` | <span data-ttu-id="8ea3a-273">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="8ea3a-273">NuGetLockFilePath</span></span> | <span data-ttu-id="8ea3a-274">Definiuje niestandardową lokalizację pliku blokady dla projektu.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-274">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="8ea3a-275">Domyślnie program NuGet obsługuje `packages.lock.json` program w katalogu głównym.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-275">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="8ea3a-276">Jeśli masz wiele projektów w tym samym katalogu, nuGet obsługuje plik blokady specyficzny dla projektu `packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="8ea3a-276">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |

## <a name="assettargetfallback"></a><span data-ttu-id="8ea3a-277">AssetTargetFallback</span><span class="sxs-lookup"><span data-stu-id="8ea3a-277">AssetTargetFallback</span></span>

<span data-ttu-id="8ea3a-278">Właściwość umożliwia określenie dodatkowych zgodnych wersji struktury dla projektów, do których odwołuje się projekt, i pakietów `AssetTargetFallback` NuGet, które są używane przez projekt.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-278">The `AssetTargetFallback` property lets you specify additional compatible framework versions for projects that your project references and NuGet packages that your project consumes.</span></span>

<span data-ttu-id="8ea3a-279">Jeśli określisz zależność pakietu przy użyciu funkcji , ale ten pakiet nie zawiera zasobów, które są zgodne ze platformą docelową projektów, właściwość `PackageReference` zostanie w pełni `AssetTargetFallback` wyeksp czasowa.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-279">If you specify a package dependency using `PackageReference` but that package doesn't contain assets that are compatible with your projects's target framework, the `AssetTargetFallback` property comes into play.</span></span> <span data-ttu-id="8ea3a-280">Zgodność przywoływanego pakietu jest ponownie sprawdzana przy użyciu każdej struktury docelowej określonej w pliku `AssetTargetFallback` .</span><span class="sxs-lookup"><span data-stu-id="8ea3a-280">The compatibility of the referenced package is rechecked using each target framework that's specified in `AssetTargetFallback`.</span></span>
<span data-ttu-id="8ea3a-281">W przypadku odwołania do lub za pośrednictwem , zostanie podniesione ostrzeżenie `project` `package` `AssetTargetFallback` [NU1701.](../reference/errors-and-warnings/NU1701.md)</span><span class="sxs-lookup"><span data-stu-id="8ea3a-281">When a `project` or a `package` is referenced through `AssetTargetFallback`, the [NU1701](../reference/errors-and-warnings/NU1701.md) warning will be raised.</span></span>

<span data-ttu-id="8ea3a-282">Zapoznaj się z tabelą poniżej, aby zapoznać się z przykładami wpływu `AssetTargetFallback` na zgodność.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-282">Refer to the table below for examples of how `AssetTargetFallback` affects compatibility.</span></span>

| <span data-ttu-id="8ea3a-283">Project framework</span><span class="sxs-lookup"><span data-stu-id="8ea3a-283">Project framework</span></span> | <span data-ttu-id="8ea3a-284">AssetTargetFallback</span><span class="sxs-lookup"><span data-stu-id="8ea3a-284">AssetTargetFallback</span></span> | <span data-ttu-id="8ea3a-285">Struktury pakietów</span><span class="sxs-lookup"><span data-stu-id="8ea3a-285">Package frameworks</span></span> | <span data-ttu-id="8ea3a-286">Wynik</span><span class="sxs-lookup"><span data-stu-id="8ea3a-286">Result</span></span> |
|-------------------|---------------------|--------------------|--------|
| <span data-ttu-id="8ea3a-287"> .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="8ea3a-287">.NET Framework 4.7.2</span></span> | | <span data-ttu-id="8ea3a-288">.NET Standard 2.0</span><span class="sxs-lookup"><span data-stu-id="8ea3a-288">.NET Standard 2.0</span></span> | <span data-ttu-id="8ea3a-289">.NET Standard 2.0</span><span class="sxs-lookup"><span data-stu-id="8ea3a-289">.NET Standard 2.0</span></span> |
| <span data-ttu-id="8ea3a-290">Aplikacja .NET Core 3.1</span><span class="sxs-lookup"><span data-stu-id="8ea3a-290">.NET Core App 3.1</span></span> | | <span data-ttu-id="8ea3a-291">.NET Standard 2.0, .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="8ea3a-291">.NET Standard 2.0, .NET Framework 4.7.2</span></span> | <span data-ttu-id="8ea3a-292">.NET Standard 2.0</span><span class="sxs-lookup"><span data-stu-id="8ea3a-292">.NET Standard 2.0</span></span> |
| <span data-ttu-id="8ea3a-293">Aplikacja .NET Core 3.1</span><span class="sxs-lookup"><span data-stu-id="8ea3a-293">.NET Core App 3.1</span></span> | | <span data-ttu-id="8ea3a-294"> .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="8ea3a-294">.NET Framework 4.7.2</span></span> | <span data-ttu-id="8ea3a-295">Niezgodne, niepowodzenie z [`NU1202`](../reference/errors-and-warnings/NU1202.md)</span><span class="sxs-lookup"><span data-stu-id="8ea3a-295">Incompatible, fail with [`NU1202`](../reference/errors-and-warnings/NU1202.md)</span></span> |
| <span data-ttu-id="8ea3a-296">Aplikacja .NET Core 3.1</span><span class="sxs-lookup"><span data-stu-id="8ea3a-296">.NET Core App 3.1</span></span> | <span data-ttu-id="8ea3a-297">net472;net471</span><span class="sxs-lookup"><span data-stu-id="8ea3a-297">net472;net471</span></span> | <span data-ttu-id="8ea3a-298"> .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="8ea3a-298">.NET Framework 4.7.2</span></span> | <span data-ttu-id="8ea3a-299">.NET Framework 4.7.2 z [`NU1701`](../reference/errors-and-warnings/NU1701.md)</span><span class="sxs-lookup"><span data-stu-id="8ea3a-299">.NET Framework 4.7.2 with [`NU1701`](../reference/errors-and-warnings/NU1701.md)</span></span> |

<span data-ttu-id="8ea3a-300">Za pomocą ogranicznika można określić `;` wiele platform.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-300">Multiple frameworks can be specified using `;` as a delimiter.</span></span> <span data-ttu-id="8ea3a-301">Aby dodać platformę rezerwową, możesz wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8ea3a-301">To add a fallback framework you can do the following:</span></span>

```xml
<AssetTargetFallback Condition=" '$(TargetFramework)'=='netcoreapp3.1' ">
    $(AssetTargetFallback);net472;net471
</AssetTargetFallback>
```

<span data-ttu-id="8ea3a-302">Jeśli chcesz zastąpić wartość, możesz pozostawić ją bez dodawania `$(AssetTargetFallback)` do istniejących `AssetTargetFallback` wartości.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-302">You can leave off `$(AssetTargetFallback)` if you wish to overwrite, instead of add to the existing `AssetTargetFallback` values.</span></span>

> [!NOTE]
> <span data-ttu-id="8ea3a-303">Jeśli używasz projektu opartego na zestawie SDK platformy [.NET,](/dotnet/core/sdk)skonfigurowane są odpowiednie wartości i nie trzeba `$(AssetTargetFallback)` ich ustawiać ręcznie.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-303">If you are using a [.NET SDK based project](/dotnet/core/sdk), appropriate `$(AssetTargetFallback)` values are configured and you do not need to set them manually.</span></span>
>
> <span data-ttu-id="8ea3a-304">`$(PackageTargetFallback)` była wcześniejszą funkcją, która próbowała rozwiązać to wyzwanie, ale jest zasadniczo uszkodzona i *nie* powinna być używana.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-304">`$(PackageTargetFallback)` was an earlier feature that attempted to address this challenge, but it is fundamentally broken and *should* not be used.</span></span> <span data-ttu-id="8ea3a-305">Aby przeprowadzić `$(PackageTargetFallback)` migrację `$(AssetTargetFallback)` z do , wystarczy zmienić nazwę właściwości.</span><span class="sxs-lookup"><span data-stu-id="8ea3a-305">To migrate from `$(PackageTargetFallback)` to `$(AssetTargetFallback)`, simply change the property name.</span></span>
