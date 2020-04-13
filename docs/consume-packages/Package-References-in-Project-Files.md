---
title: Format NuGet PackageReference (odwołania do pakietów w plikach projektu)
description: Szczegółowe informacje na temat wnioskowania pakietu NuGet w plikach projektu obsługiwanych przez nuget 4.0+ i VS2017 oraz .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: a5833df60c5f7905359f421141347b1237f45d86
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428871"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="68444-103">Odwołania do pakietów (PackageReference) w plikach projektu</span><span class="sxs-lookup"><span data-stu-id="68444-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="68444-104">Odwołania do pakietu, `PackageReference` za pomocą węzła, zarządzać zależnościami NuGet bezpośrednio `packages.config` w plikach projektu (w przeciwieństwie do oddzielnego pliku).</span><span class="sxs-lookup"><span data-stu-id="68444-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="68444-105">Za pomocą PackageReference, jak to się nazywa, nie wpływa na inne aspekty NuGet; na przykład ustawienia `NuGet.config` w plikach (w tym źródła pakietów) są nadal stosowane, jak wyjaśniono w [typowych konfiguracjach NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="68444-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="68444-106">Za pomocą PackageReference można również użyć MSBuild warunki, aby wybrać odwołania do pakietu na platformę docelową lub innych grup.</span><span class="sxs-lookup"><span data-stu-id="68444-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, or other groupings.</span></span> <span data-ttu-id="68444-107">Umożliwia również szczegółową kontrolę nad zależnościami i przepływem zawartości.</span><span class="sxs-lookup"><span data-stu-id="68444-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="68444-108">(Zobacz więcej szczegółów [NuGet pack i restore jako obiekty docelowe MSBuild).)](../reference/msbuild-targets.md)</span><span class="sxs-lookup"><span data-stu-id="68444-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="68444-109">Obsługa typów projektów</span><span class="sxs-lookup"><span data-stu-id="68444-109">Project type support</span></span>

<span data-ttu-id="68444-110">Domyślnie PackageReference jest używany dla projektów .NET Core, .NET Standard i projektów platformy uniwersalnej systemu Windows przeznaczonych dla systemu Windows 10 Build 15063 (Creators Update) i nowszych, z wyjątkiem projektów platformy uniwersalnej systemu Windows++ platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="68444-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="68444-111">Projekty programu .NET Framework obsługują packagereference, ale obecnie domyślnie `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="68444-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="68444-112">Aby użyć PackageReference, należy przeprowadzić `packages.config` [migrację](../consume-packages/migrate-packages-config-to-package-reference.md) zależności z pliku projektu, a następnie usunąć plik packages.config.</span><span class="sxs-lookup"><span data-stu-id="68444-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="68444-113">ASP.NET aplikacje przeznaczone dla pełnego programu .NET Framework obejmują tylko [ograniczoną obsługę](https://github.com/NuGet/Home/issues/5877) packagereference.</span><span class="sxs-lookup"><span data-stu-id="68444-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="68444-114">Typy projektów języka C++ i JavaScript nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="68444-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="68444-115">Dodawanie packagereference</span><span class="sxs-lookup"><span data-stu-id="68444-115">Adding a PackageReference</span></span>

<span data-ttu-id="68444-116">Dodaj zależność w pliku projektu przy użyciu następującej składni:</span><span class="sxs-lookup"><span data-stu-id="68444-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="68444-117">Kontrolowanie wersji zależności</span><span class="sxs-lookup"><span data-stu-id="68444-117">Controlling dependency version</span></span>

<span data-ttu-id="68444-118">Konwencja określająca wersję pakietu jest taka sama, `packages.config`jak w przypadku korzystania z:</span><span class="sxs-lookup"><span data-stu-id="68444-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="68444-119">W powyższym przykładzie 3.6.0 oznacza dowolną wersję, która jest >= 3.6.0 z preferencją dla najniższej wersji, zgodnie z opisem w [wersji pakietu](../concepts/package-versioning.md#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="68444-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="68444-120">Korzystanie z packagereference dla projektu bez packagereferences</span><span class="sxs-lookup"><span data-stu-id="68444-120">Using PackageReference for a project with no PackageReferences</span></span>

<span data-ttu-id="68444-121">Zaawansowane: Jeśli nie masz żadnych pakietów zainstalowanych w projekcie (nie PackageReferences w pliku projektu i bez pliku packages.config), ale chcesz, aby projekt został przywrócony jako styl PackageReference, można ustawić właściwość projektu RestoreProjectStyle do PackageReference w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="68444-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="68444-122">Może to być przydatne, jeśli odwołujesz się do projektów, które są PackageReference stylu (istniejące csproj lub SDK stylu projektów).</span><span class="sxs-lookup"><span data-stu-id="68444-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="68444-123">Umożliwi to pakiety, które te projekty odnoszą się do, aby być "przechodnie" odwołuje się do projektu.</span><span class="sxs-lookup"><span data-stu-id="68444-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="packagereference-and-sources"></a><span data-ttu-id="68444-124">PackageReference i źródła</span><span class="sxs-lookup"><span data-stu-id="68444-124">PackageReference and sources</span></span>

<span data-ttu-id="68444-125">W projektach PackageReference przechodnie wersje zależności są rozpoznawane w czasie przywracania.</span><span class="sxs-lookup"><span data-stu-id="68444-125">In PackageReference projects, the transitive dependency versions are resolved at restore time.</span></span> <span data-ttu-id="68444-126">W związku z tym w PackageReference projektów wszystkie źródła muszą być dostępne dla wszystkich przywraca.</span><span class="sxs-lookup"><span data-stu-id="68444-126">As such, in PackageReference projects all sources need to be available for all restores.</span></span> 

## <a name="floating-versions"></a><span data-ttu-id="68444-127">Wersje pływające</span><span class="sxs-lookup"><span data-stu-id="68444-127">Floating Versions</span></span>

<span data-ttu-id="68444-128">[Wersje przestawne](../concepts/dependency-resolution.md#floating-versions) `PackageReference`są obsługiwane z:</span><span class="sxs-lookup"><span data-stu-id="68444-128">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="68444-129">Kontrolowanie zasobów zależności</span><span class="sxs-lookup"><span data-stu-id="68444-129">Controlling dependency assets</span></span>

<span data-ttu-id="68444-130">Może być przy użyciu zależności wyłącznie jako uprzęży rozwoju i nie może chcieć udostępnić, że do projektów, które będą korzystać z pakietu.</span><span class="sxs-lookup"><span data-stu-id="68444-130">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="68444-131">W tym scenariuszu `PrivateAssets` można użyć metadanych do kontrolowania tego zachowania.</span><span class="sxs-lookup"><span data-stu-id="68444-131">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="68444-132">Następujące tagi metadanych kontrolują zasoby zależności:</span><span class="sxs-lookup"><span data-stu-id="68444-132">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="68444-133">Tag</span><span class="sxs-lookup"><span data-stu-id="68444-133">Tag</span></span> | <span data-ttu-id="68444-134">Opis</span><span class="sxs-lookup"><span data-stu-id="68444-134">Description</span></span> | <span data-ttu-id="68444-135">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="68444-135">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="68444-136">Zestawy dołączane</span><span class="sxs-lookup"><span data-stu-id="68444-136">IncludeAssets</span></span> | <span data-ttu-id="68444-137">Aktywa te zostaną zużyte</span><span class="sxs-lookup"><span data-stu-id="68444-137">These assets will be consumed</span></span> | <span data-ttu-id="68444-138">all</span><span class="sxs-lookup"><span data-stu-id="68444-138">all</span></span> |
| <span data-ttu-id="68444-139">WykluczAzestawy</span><span class="sxs-lookup"><span data-stu-id="68444-139">ExcludeAssets</span></span> | <span data-ttu-id="68444-140">Aktywa te nie będą zużywane</span><span class="sxs-lookup"><span data-stu-id="68444-140">These assets will not be consumed</span></span> | <span data-ttu-id="68444-141">brak</span><span class="sxs-lookup"><span data-stu-id="68444-141">none</span></span> |
| <span data-ttu-id="68444-142">Zestawy prywatne</span><span class="sxs-lookup"><span data-stu-id="68444-142">PrivateAssets</span></span> | <span data-ttu-id="68444-143">Te zasoby zostaną zużyte, ale nie będą przepływać do projektu nadrzędnego</span><span class="sxs-lookup"><span data-stu-id="68444-143">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="68444-144">contentfiles;analizatory;kompilacja</span><span class="sxs-lookup"><span data-stu-id="68444-144">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="68444-145">Dopuszczalne wartości dla tych znaczników są następujące, z wieloma wartościami `all` `none` oddzielonymi średnikiem, z wyjątkiem i które muszą być wyświetlane same w sobie:</span><span class="sxs-lookup"><span data-stu-id="68444-145">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="68444-146">Wartość</span><span class="sxs-lookup"><span data-stu-id="68444-146">Value</span></span> | <span data-ttu-id="68444-147">Opis</span><span class="sxs-lookup"><span data-stu-id="68444-147">Description</span></span> |
| --- | ---
| <span data-ttu-id="68444-148">kompilowanie</span><span class="sxs-lookup"><span data-stu-id="68444-148">compile</span></span> | <span data-ttu-id="68444-149">Zawartość folderu `lib` i określa, czy projekt może kompilować względem zestawów w folderze</span><span class="sxs-lookup"><span data-stu-id="68444-149">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="68444-150">środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="68444-150">runtime</span></span> | <span data-ttu-id="68444-151">Zawartość `lib` folderu `runtimes` i i określa, czy te zestawy zostaną skopiowane do katalogu wyjściowego kompilacji</span><span class="sxs-lookup"><span data-stu-id="68444-151">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="68444-152">contentFiles</span><span class="sxs-lookup"><span data-stu-id="68444-152">contentFiles</span></span> | <span data-ttu-id="68444-153">Zawartość folderu `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="68444-153">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="68444-154">kompilacja</span><span class="sxs-lookup"><span data-stu-id="68444-154">build</span></span> | <span data-ttu-id="68444-155">`.props`i `.targets` w `build` folderze</span><span class="sxs-lookup"><span data-stu-id="68444-155">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="68444-156">buildMultitargeting</span><span class="sxs-lookup"><span data-stu-id="68444-156">buildMultitargeting</span></span> | <span data-ttu-id="68444-157">*(4.0)* `.props` `.targets` oraz `buildMultitargeting` w folderze, w celu ukierunkowania na</span><span class="sxs-lookup"><span data-stu-id="68444-157">*(4.0)* `.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="68444-158">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="68444-158">buildTransitive</span></span> | <span data-ttu-id="68444-159">*(5.0+)* `.props` `.targets` i `buildTransitive` w folderze, dla zasobów, które przepływają przechodnie do dowolnego projektu zużywającego.</span><span class="sxs-lookup"><span data-stu-id="68444-159">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="68444-160">Zobacz stronę [funkcji.](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior)</span><span class="sxs-lookup"><span data-stu-id="68444-160">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="68444-161">Analizatory</span><span class="sxs-lookup"><span data-stu-id="68444-161">analyzers</span></span> | <span data-ttu-id="68444-162">Analizatory .NET</span><span class="sxs-lookup"><span data-stu-id="68444-162">.NET analyzers</span></span> |
| <span data-ttu-id="68444-163">natywne</span><span class="sxs-lookup"><span data-stu-id="68444-163">native</span></span> | <span data-ttu-id="68444-164">Zawartość folderu `native`</span><span class="sxs-lookup"><span data-stu-id="68444-164">Contents of the `native` folder</span></span> |
| <span data-ttu-id="68444-165">brak</span><span class="sxs-lookup"><span data-stu-id="68444-165">none</span></span> | <span data-ttu-id="68444-166">Żadne z powyższych są używane.</span><span class="sxs-lookup"><span data-stu-id="68444-166">None of the above are used.</span></span> |
| <span data-ttu-id="68444-167">all</span><span class="sxs-lookup"><span data-stu-id="68444-167">all</span></span> | <span data-ttu-id="68444-168">Wszystkie powyższe (z wyjątkiem) `none`</span><span class="sxs-lookup"><span data-stu-id="68444-168">All of the above (except `none`)</span></span> |

<span data-ttu-id="68444-169">W poniższym przykładzie wszystko oprócz plików zawartości z pakietu będzie używane przez projekt i wszystko z wyjątkiem plików zawartości i analizatorów będzie przepływać do projektu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="68444-169">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="68444-170">Należy zauważyć, że `build` ponieważ `PrivateAssets`nie jest dołączony do , cele i rekwizyty *będą* przepływać do projektu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="68444-170">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="68444-171">Należy wziąć pod uwagę, na przykład, że powyższe odwołanie jest używane w projekcie, który tworzy pakiet NuGet o nazwie AppLogger.</span><span class="sxs-lookup"><span data-stu-id="68444-171">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="68444-172">AppLogger może korzystać z `Contoso.Utility.UsefulStuff`obiektów docelowych i rekwizytów z , podobnie jak projekty, które korzystają z AppLogger.</span><span class="sxs-lookup"><span data-stu-id="68444-172">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="68444-173">Gdy `developmentDependency` jest `true` ustawiona `.nuspec` w pliku, oznacza to pakiet jako zależność tylko dla deweloperów, co uniemożliwia pakiet zostanie uwzględniony jako zależność w innych pakietach.</span><span class="sxs-lookup"><span data-stu-id="68444-173">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="68444-174">Z PackageReference *(NuGet 4.8+)* ta flaga oznacza również, że będzie wykluczać zasoby kompilacji z kompilacji.</span><span class="sxs-lookup"><span data-stu-id="68444-174">With PackageReference *(NuGet 4.8+)*, this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="68444-175">Aby uzyskać więcej informacji, zobacz [RozwójZależność obsługi packagereference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="68444-175">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="68444-176">Dodawanie warunku PackageReference</span><span class="sxs-lookup"><span data-stu-id="68444-176">Adding a PackageReference condition</span></span>

<span data-ttu-id="68444-177">Warunek służy do kontrolowania, czy pakiet jest dołączony, gdzie warunki można użyć dowolnej zmiennej MSBuild lub zmiennej zdefiniowanej w pliku obiektów docelowych lub props.</span><span class="sxs-lookup"><span data-stu-id="68444-177">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="68444-178">Jednak obecnie tylko zmienna `TargetFramework` jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="68444-178">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="68444-179">Załóżmy na przykład, `netstandard1.4` że kierujesz reklamy, a także `net452` `net452`masz zależność, która ma zastosowanie tylko do .</span><span class="sxs-lookup"><span data-stu-id="68444-179">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="68444-180">W takim przypadku nie `netstandard1.4` chcesz, aby projekt, który zużywa pakiet, aby dodać tę niepotrzebną zależność.</span><span class="sxs-lookup"><span data-stu-id="68444-180">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="68444-181">Aby temu zapobiec, należy określić warunek w następujący sposób: `PackageReference`</span><span class="sxs-lookup"><span data-stu-id="68444-181">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="68444-182">Pakiet zbudowany przy użyciu tego projektu pokaże, że Newtonsoft.Json jest `net452` uwzględniony jako zależność tylko dla obiektu docelowego:</span><span class="sxs-lookup"><span data-stu-id="68444-182">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Wynik zastosowania warunku na PackageReference z VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="68444-184">Warunki mogą być również `ItemGroup` stosowane na poziomie i `PackageReference` będą miały zastosowanie do wszystkich elementów dla dzieci:</span><span class="sxs-lookup"><span data-stu-id="68444-184">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a><span data-ttu-id="68444-185">GeneratePathProperty</span><span class="sxs-lookup"><span data-stu-id="68444-185">GeneratePathProperty</span></span>

<span data-ttu-id="68444-186">Ta funkcja jest dostępna w wersji NuGet **5.0** lub wyższej oraz w programie Visual Studio 2019 **16.0** lub wyższym.</span><span class="sxs-lookup"><span data-stu-id="68444-186">This feature is available with NuGet **5.0** or above and with Visual Studio 2019 **16.0** or above.</span></span>

<span data-ttu-id="68444-187">Czasami pożądane jest odwoływanie się do plików w pakiecie z obiektu docelowego MSBuild.</span><span class="sxs-lookup"><span data-stu-id="68444-187">Sometimes it is desirable to reference files in a package from an MSBuild target.</span></span>
<span data-ttu-id="68444-188">W `packages.config` projektach opartych pakiety są instalowane w folderze względem pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="68444-188">In `packages.config` based projects, the packages are installed in a folder relative to the project file.</span></span> <span data-ttu-id="68444-189">Jednak w PackageReference pakiety są [używane](../concepts/package-installation-process.md) z globalnego folderu *pakietów,* które mogą się różnić od komputera do komputera.</span><span class="sxs-lookup"><span data-stu-id="68444-189">However in PackageReference, the packages are [consumed](../concepts/package-installation-process.md) from the *global-packages* folder, which can vary from machine to machine.</span></span>

<span data-ttu-id="68444-190">Aby wypełnić tę lukę, NuGet wprowadził właściwość, która wskazuje lokalizację, z której pakiet zostanie wykorzystany.</span><span class="sxs-lookup"><span data-stu-id="68444-190">To bridge that gap, NuGet introduced a property that points to the location from which the package will be consumed.</span></span>

<span data-ttu-id="68444-191">Przykład:</span><span class="sxs-lookup"><span data-stu-id="68444-191">Example:</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

<span data-ttu-id="68444-192">Ponadto NuGet automatycznie wygeneruje właściwości dla pakietów zawierających folder narzędzi.</span><span class="sxs-lookup"><span data-stu-id="68444-192">Additionally NuGet will automatically generate properties for packages containing a tools folder.</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
````

<span data-ttu-id="68444-193">Właściwości MSBuild i tożsamości pakietów nie mają tych samych ograniczeń, więc tożsamość pakietu musi zostać zmieniona `Pkg`na przyjazną nazwę MSBuild, poprzedzony wyrazem .</span><span class="sxs-lookup"><span data-stu-id="68444-193">MSBuild properties and package identities do not have the same restrictions so the package identity needs to be changed to an MSBuild friendly name, prefixed by the word `Pkg`.</span></span>
<span data-ttu-id="68444-194">Aby sprawdzić dokładną nazwę wygenerowanej właściwości, przyjrzyj się wygenerowanemu plikowi [nuget.g.props.](../reference/msbuild-targets.md#restore-outputs)</span><span class="sxs-lookup"><span data-stu-id="68444-194">To verify the exact name of the property generated, look at the generated [nuget.g.props](../reference/msbuild-targets.md#restore-outputs) file.</span></span>

## <a name="nuget-warnings-and-errors"></a><span data-ttu-id="68444-195">Ostrzeżenia i błędy NuGet</span><span class="sxs-lookup"><span data-stu-id="68444-195">NuGet warnings and errors</span></span>

<span data-ttu-id="68444-196">*Ta funkcja jest dostępna w wersji NuGet **4.3** lub wyższej oraz w programie Visual Studio 2017 **15.3** lub wyższym.*</span><span class="sxs-lookup"><span data-stu-id="68444-196">*This feature is available with NuGet **4.3** or above and with Visual Studio 2017 **15.3** or above.*</span></span>

<span data-ttu-id="68444-197">W przypadku wielu scenariuszy pakowania i przywracania wszystkie ostrzeżenia i `NU****`błędy NuGet są kodowane i zaczynają się od .</span><span class="sxs-lookup"><span data-stu-id="68444-197">For many pack and restore scenarios, all NuGet warnings and errors are coded, and start with `NU****`.</span></span> <span data-ttu-id="68444-198">Wszystkie ostrzeżenia i błędy NuGet są wymienione w dokumentacji [referencyjnej.](../reference/errors-and-warnings.md)</span><span class="sxs-lookup"><span data-stu-id="68444-198">All NuGet warnings and errors are listed in the [reference](../reference/errors-and-warnings.md) documentation.</span></span>

<span data-ttu-id="68444-199">NuGet przestrzega następujących właściwości ostrzeżenia:</span><span class="sxs-lookup"><span data-stu-id="68444-199">NuGet observes the following warning properties:</span></span>

- <span data-ttu-id="68444-200">`TreatWarningsAsErrors`, potraktuj wszystkie ostrzeżenia jako błędy</span><span class="sxs-lookup"><span data-stu-id="68444-200">`TreatWarningsAsErrors`, treat all warnings as errors</span></span>
- <span data-ttu-id="68444-201">`WarningsAsErrors`, traktować określone ostrzeżenia jako błędy</span><span class="sxs-lookup"><span data-stu-id="68444-201">`WarningsAsErrors`, treat specific warnings as errors</span></span>
- <span data-ttu-id="68444-202">`NoWarn`, ukryj określone ostrzeżenia, obejmujące cały projekt lub pakiet.</span><span class="sxs-lookup"><span data-stu-id="68444-202">`NoWarn`, hide specific warnings, either project-wide or package-wide.</span></span>

<span data-ttu-id="68444-203">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="68444-203">Examples:</span></span>

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

### <a name="suppressing-nuget-warnings"></a><span data-ttu-id="68444-204">Pomijanie ostrzeżeń NuGet</span><span class="sxs-lookup"><span data-stu-id="68444-204">Suppressing NuGet warnings</span></span>

<span data-ttu-id="68444-205">Chociaż zaleca się, aby rozwiązać wszystkie ostrzeżenia NuGet podczas pakietu i przywrócić operacje, w niektórych sytuacjach pomijając je jest uzasadnione.</span><span class="sxs-lookup"><span data-stu-id="68444-205">While it is recommended that you resolve all NuGet warnings during your pack and restore operations, in certain situations suppressing them is warranted.</span></span>
<span data-ttu-id="68444-206">Aby pominąć projekt ostrzegawczy w szerokim zakresie, należy rozważyć wykonanie:</span><span class="sxs-lookup"><span data-stu-id="68444-206">To suppress a warning project wide, consider doing:</span></span>

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

<span data-ttu-id="68444-207">Czasami ostrzeżenia dotyczą tylko określonego pakietu na wykresie.</span><span class="sxs-lookup"><span data-stu-id="68444-207">Sometimes warnings apply only to a certain package in the graph.</span></span> <span data-ttu-id="68444-208">Możemy wybrać, aby pominąć to ostrzeżenie `NoWarn` bardziej selektywnie, dodając na PackageReference elementu.</span><span class="sxs-lookup"><span data-stu-id="68444-208">We can choose to suppress that warning more selectively by adding a `NoWarn` on the PackageReference item.</span></span> 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a><span data-ttu-id="68444-209">Pomijanie ostrzeżeń pakietu NuGet w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="68444-209">Suppressing NuGet package warnings in Visual Studio</span></span>

<span data-ttu-id="68444-210">W programie Visual Studio można również [pominąć ostrzeżenia](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) za pośrednictwem IDE.</span><span class="sxs-lookup"><span data-stu-id="68444-210">When in Visual Studio, you can also [suppress warnings](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) through the IDE.</span></span>

## <a name="locking-dependencies"></a><span data-ttu-id="68444-211">Blokowanie zależności</span><span class="sxs-lookup"><span data-stu-id="68444-211">Locking dependencies</span></span>

<span data-ttu-id="68444-212">*Ta funkcja jest dostępna w wersji NuGet **4.9** lub wyższej oraz w programie Visual Studio 2017 **15.9** lub wyższym.*</span><span class="sxs-lookup"><span data-stu-id="68444-212">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="68444-213">Dane wejściowe do nuget restore to zestaw odwołań do pakietu z pliku projektu (zależności najwyższego poziomu lub bezpośrednie), a dane wyjściowe są pełnym zamknięciem wszystkich zależności pakietu, w tym zależności przechodnich.</span><span class="sxs-lookup"><span data-stu-id="68444-213">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="68444-214">NuGet próbuje zawsze produkować takie same pełne zamknięcie zależności pakietu, jeśli lista danych wejściowych PackageReference nie uległa zmianie.</span><span class="sxs-lookup"><span data-stu-id="68444-214">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="68444-215">Istnieją jednak pewne scenariusze, w których nie jest w stanie tego zrobić.</span><span class="sxs-lookup"><span data-stu-id="68444-215">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="68444-216">Przykład:</span><span class="sxs-lookup"><span data-stu-id="68444-216">For example:</span></span>

* <span data-ttu-id="68444-217">W przypadku korzystania `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`z wersji przestawnych, takich jak .</span><span class="sxs-lookup"><span data-stu-id="68444-217">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="68444-218">Podczas gdy intencją w tym miejscu jest float do najnowszej wersji na każdym przywracaniu pakietów, istnieją scenariusze, w których użytkownicy wymagają wykresu, aby zablokować do określonej najnowszej wersji i float do nowszej wersji, jeśli są dostępne, na jawny gest.</span><span class="sxs-lookup"><span data-stu-id="68444-218">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="68444-219">Opublikowano nowszą wersję pakietu pasującego wymagania dotyczące wersji PackageReference.</span><span class="sxs-lookup"><span data-stu-id="68444-219">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="68444-220">Na przykład</span><span class="sxs-lookup"><span data-stu-id="68444-220">E.g.</span></span> 

  * <span data-ttu-id="68444-221">Dzień 1: jeśli `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` określono, ale wersje dostępne w repozytoriach NuGet były 4.1.0, 4.2.0 i 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="68444-221">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="68444-222">W takim przypadku NuGet rozpoznałby do 4.1.0 (najbliższa minimalna wersja)</span><span class="sxs-lookup"><span data-stu-id="68444-222">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="68444-223">Dzień 2: Wersja 4.0.0 zostanie opublikowana.</span><span class="sxs-lookup"><span data-stu-id="68444-223">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="68444-224">NuGet znajdzie teraz dokładne dopasowanie i rozpocznie rozwiązywanie do 4.0.0</span><span class="sxs-lookup"><span data-stu-id="68444-224">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="68444-225">Dana wersja pakietu jest usuwana z repozytorium.</span><span class="sxs-lookup"><span data-stu-id="68444-225">A given package version is removed from the repository.</span></span> <span data-ttu-id="68444-226">Chociaż nuget.org nie zezwala na usuwanie pakietów, nie wszystkie repozytoria pakietów mają te ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="68444-226">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="68444-227">Powoduje to, że NuGet znalezienie najlepszego dopasowania, gdy nie można rozwiązać do usuniętej wersji.</span><span class="sxs-lookup"><span data-stu-id="68444-227">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="68444-228">Włączanie pliku blokady</span><span class="sxs-lookup"><span data-stu-id="68444-228">Enabling lock file</span></span>

<span data-ttu-id="68444-229">Aby utrwalić pełne zamknięcie zależności pakietu można wyrazić zgodę na funkcję pliku `RestorePackagesWithLockFile` blokady, ustawiając właściwość MSBuild dla projektu:</span><span class="sxs-lookup"><span data-stu-id="68444-229">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="68444-230">Jeśli ta właściwość jest ustawiona, NuGet `packages.lock.json` restore wygeneruje plik blokady - plik w katalogu głównym projektu, który zawiera listę wszystkich zależności pakietu.</span><span class="sxs-lookup"><span data-stu-id="68444-230">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="68444-231">Gdy projekt `packages.lock.json` ma plik w katalogu głównym, plik blokady jest zawsze `RestorePackagesWithLockFile` używany z przywracania, nawet jeśli właściwość nie jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="68444-231">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="68444-232">Innym sposobem wyrażenia zgody na tę funkcję jest utworzenie `packages.lock.json` fikcyjnego pustego pliku w katalogu głównym projektu.</span><span class="sxs-lookup"><span data-stu-id="68444-232">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="68444-233">`restore`zachowanie z plikiem blokady</span><span class="sxs-lookup"><span data-stu-id="68444-233">`restore` behavior with lock file</span></span>
<span data-ttu-id="68444-234">Jeśli plik blokady jest obecny dla projektu, NuGet `restore`używa tego pliku blokady do uruchomienia .</span><span class="sxs-lookup"><span data-stu-id="68444-234">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="68444-235">NuGet wykonuje szybkie sprawdzanie, czy były jakieś zmiany w zależności pakietu, jak wspomniano w pliku projektu (lub plików projektów zależnych) i jeśli nie było żadnych zmian po prostu przywraca pakiety wymienione w pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="68444-235">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="68444-236">Nie ma ponownej oceny zależności pakietu.</span><span class="sxs-lookup"><span data-stu-id="68444-236">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="68444-237">Jeśli NuGet wykryje zmianę w zdefiniowanych zależności, jak wspomniano w pliku projektu(-ów), ponownie ocenia wykres pakietu i aktualizuje plik blokady, aby odzwierciedlić nowe zamknięcie pakietu dla projektu.</span><span class="sxs-lookup"><span data-stu-id="68444-237">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="68444-238">W przypadku ciągłej integracji/ciągłego wdrażania i innych scenariuszy, w których nie chcesz `lockedmode` zmieniać `true`zależności pakietów na bieżąco, można to zrobić, ustawiając na:</span><span class="sxs-lookup"><span data-stu-id="68444-238">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="68444-239">W przypadku pliku dotnet.exe uruchom:</span><span class="sxs-lookup"><span data-stu-id="68444-239">For dotnet.exe, run:</span></span>

```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="68444-240">Dla msbuild.exe, uruchom:</span><span class="sxs-lookup"><span data-stu-id="68444-240">For msbuild.exe, run:</span></span>

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="68444-241">Można również ustawić tę warunkową właściwość MSBuild w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="68444-241">You may also set this conditional MSBuild property in your project file:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="68444-242">Jeśli tryb zablokowany `true`jest , przywracanie przywróci dokładne pakiety wymienione w pliku blokady lub zakończy się niepowodzeniem, jeśli zaktualizowano zdefiniowane zależności pakietów dla projektu po utworzeniu pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="68444-242">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="68444-243">Przeksztą do repozytorium źródłowego pliku blokady</span><span class="sxs-lookup"><span data-stu-id="68444-243">Make lock file part of your source repository</span></span>
<span data-ttu-id="68444-244">Jeśli budujesz aplikację, plik wykonywalny i projekt, o którym mowa jest na początku łańcucha zależności, a następnie zaewidencjonuj plik blokady do repozytorium kodu źródłowego, dzięki czemu NuGet może z niego korzystać podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="68444-244">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="68444-245">Jednak jeśli projekt jest projekt biblioteki, które nie są dostarczane lub wspólny projekt kodu, od którego zależą inne projekty, **nie należy** zaewidencjonować pliku blokady jako część kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="68444-245">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="68444-246">Nie ma żadnych szkód w zachowaniu pliku blokady, ale zablokowane zależności pakietu dla wspólnego projektu kodu nie mogą być używane, jak wymieniono w pliku blokady, podczas przywracania/kompilacji projektu, który zależy od tego projektu wspólnego kodu.</span><span class="sxs-lookup"><span data-stu-id="68444-246">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="68444-247">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="68444-247">Eg.</span></span>

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

<span data-ttu-id="68444-248">Jeśli `ProjectA` ma zależność `PackageX` od `2.0.0` wersji, `ProjectB` a także `PackageX` `1.0.0`odwołuje się do `ProjectB` wersji, a następnie `PackageX` `1.0.0`plik blokady dla wyświetli zależność od wersji .</span><span class="sxs-lookup"><span data-stu-id="68444-248">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="68444-249">Jednak po `ProjectA` zbudowaniu jego plik blokady `PackageX` będzie **`2.0.0`** zawierał zależność od wersji, a **nie** `1.0.0` wymienioną w pliku blokady dla `ProjectB`.</span><span class="sxs-lookup"><span data-stu-id="68444-249">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="68444-250">W związku z tym plik blokady wspólnego projektu kodu ma niewiele do powiedzenia na temat pakietów rozwiązanych dla projektów, które zależą od niego.</span><span class="sxs-lookup"><span data-stu-id="68444-250">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="68444-251">Rozszerzalność pliku blokady</span><span class="sxs-lookup"><span data-stu-id="68444-251">Lock file extensibility</span></span>

<span data-ttu-id="68444-252">Można kontrolować różne zachowania przywracania za pomocą pliku blokady, jak opisano poniżej:</span><span class="sxs-lookup"><span data-stu-id="68444-252">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="68444-253">NuGet.exe, opcja</span><span class="sxs-lookup"><span data-stu-id="68444-253">NuGet.exe option</span></span> | <span data-ttu-id="68444-254">dotnet, opcja</span><span class="sxs-lookup"><span data-stu-id="68444-254">dotnet option</span></span> | <span data-ttu-id="68444-255">Opcja równoważna MSBuild</span><span class="sxs-lookup"><span data-stu-id="68444-255">MSBuild equivalent option</span></span> | <span data-ttu-id="68444-256">Opis</span><span class="sxs-lookup"><span data-stu-id="68444-256">Description</span></span> |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | <span data-ttu-id="68444-257">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="68444-257">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="68444-258">Decyduje się na użycie pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="68444-258">Opts into the usage of a lock file.</span></span> |
| `-LockedMode` | `--locked-mode` | <span data-ttu-id="68444-259">Tryb RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="68444-259">RestoreLockedMode</span></span> | <span data-ttu-id="68444-260">Włącza tryb zablokowany do przywracania.</span><span class="sxs-lookup"><span data-stu-id="68444-260">Enables locked mode for restore.</span></span> <span data-ttu-id="68444-261">Jest to przydatne w scenariuszach ciągłej integracji/ciągłego wdrażania, w których mają być powtarzalne kompilacje.</span><span class="sxs-lookup"><span data-stu-id="68444-261">This is useful in CI/CD scenarios where you want repeatable builds.</span></span>|   
| `-ForceEvaluate` | `--force-evaluate` | <span data-ttu-id="68444-262">Wartość RestoreForceE</span><span class="sxs-lookup"><span data-stu-id="68444-262">RestoreForceEvaluate</span></span> | <span data-ttu-id="68444-263">Ta opcja jest przydatna w przypadku pakietów z wersją przestawną zdefiniowaną w projekcie.</span><span class="sxs-lookup"><span data-stu-id="68444-263">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="68444-264">Domyślnie przywracanie NuGet nie zaktualizuje wersji pakietu automatycznie przy każdym przywracanie, chyba że uruchomisz przywracanie za pomocą tej opcji.</span><span class="sxs-lookup"><span data-stu-id="68444-264">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with this option.</span></span> |
| `-LockFilePath` | `--lock-file-path` | <span data-ttu-id="68444-265">Ścieżka pliku NuGetLock</span><span class="sxs-lookup"><span data-stu-id="68444-265">NuGetLockFilePath</span></span> | <span data-ttu-id="68444-266">Definiuje niestandardową lokalizację pliku blokady dla projektu.</span><span class="sxs-lookup"><span data-stu-id="68444-266">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="68444-267">Domyślnie NuGet `packages.lock.json` obsługuje w katalogu głównym.</span><span class="sxs-lookup"><span data-stu-id="68444-267">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="68444-268">Jeśli masz wiele projektów w tym samym katalogu, NuGet obsługuje plik blokady specyficzne dla projektu`packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="68444-268">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
