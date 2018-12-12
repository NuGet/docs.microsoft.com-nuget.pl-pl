---
title: Formatu NuGet PackageReference (odwołania do pakietu w plikach projektu)
description: Szczegółowe informacje na temat formatu NuGet PackageReference w plikach projektu jako obsługiwane przez NuGet 4.0 + i programu VS 2017 i platformy .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: e4df15be1f29e2c611876aaa49e16ac7d1823938
ms.sourcegitcommit: be9c51b4b095aea40ef41bbea7e12ef0a194ee74
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248458"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="cc47a-103">Odwołania do pakietu (PackageReference) w plikach projektu</span><span class="sxs-lookup"><span data-stu-id="cc47a-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="cc47a-104">Pakiet odwołań, za pomocą `PackageReference` węzła, zarządzanie zależnościami NuGet bezpośrednio z poziomu plików projektu (w przeciwieństwie do oddzielnego `packages.config` pliku).</span><span class="sxs-lookup"><span data-stu-id="cc47a-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="cc47a-105">Za pomocą funkcji PackageReference, ponieważ jest to, nie ma wpływu na inne aspekty pakietu nuget; na przykład ustawienia w `NuGet.config` plików (w tym źródeł pakietów) nadal są stosowane zgodnie z objaśnieniem w [Konfigurowanie zachowania pakietu NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="cc47a-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="cc47a-106">Za pomocą funkcji PackageReference umożliwia także warunki MSBuild do wyboru na platformę docelową, konfiguracji, platforma lub inne grupy będzie odwoływał się pakiet.</span><span class="sxs-lookup"><span data-stu-id="cc47a-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="cc47a-107">Umożliwia ona również szczegółową kontrolę nad tym zależności i zawartości przepływu.</span><span class="sxs-lookup"><span data-stu-id="cc47a-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="cc47a-108">(Aby uzyskać więcej informacji, zobacz [NuGet pakowanie i przywrócić jako elementów docelowych MSBuild](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="cc47a-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="cc47a-109">Domyślnie PackageReference jest używany dla projektów .NET Core, .NET Standard projektów i projektów platformy UWP przeznaczonych dla systemu Windows 10 kompilacja 15063 (Aktualizacja dla twórców) lub nowszy, z wyjątkiem projektów platformy UWP w języku C++.</span><span class="sxs-lookup"><span data-stu-id="cc47a-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="cc47a-110">Projektów programu .NET framework obsługuje PackageReference, ale obecnie domyślnie `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="cc47a-110">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="cc47a-111">Aby korzystać z funkcji PackageReference, migracja zależności z `packages.config` do pliku projektu, a następnie usuń packages.config.</span><span class="sxs-lookup"><span data-stu-id="cc47a-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="cc47a-112">Dodawanie odwołanie PackageReference</span><span class="sxs-lookup"><span data-stu-id="cc47a-112">Adding a PackageReference</span></span>

<span data-ttu-id="cc47a-113">Dodawanie zależności w pliku projektu przy użyciu następującej składni:</span><span class="sxs-lookup"><span data-stu-id="cc47a-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="cc47a-114">Kontrolowanie wersja zależności</span><span class="sxs-lookup"><span data-stu-id="cc47a-114">Controlling dependency version</span></span>

<span data-ttu-id="cc47a-115">Konwencja określania wersję pakietu jest taka sama jak, korzystając z `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="cc47a-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="cc47a-116">W powyższym przykładzie 3.6.0 oznacza dowolną wersję, którą jest > = 3.6.0 z preferencją dla Najniższa wersja zgodnie z opisem na [przechowywanie wersji pakietów](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="cc47a-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="cc47a-117">Za pomocą funkcji PackageReference dla projektu z nie składnika PackageReferences</span><span class="sxs-lookup"><span data-stu-id="cc47a-117">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="cc47a-118">Zaawansowane: Jeśli ma żadnych pakietów zainstalowany w projekcie (nie składnika PackageReferences w pliku projektu) i Brak pliku packages.config, ale Project, które ma zostać przywrócone jako styl PackageReference w projekcie można ustawić właściwości projektu RestoreProjectStyle PackageReference plik.</span><span class="sxs-lookup"><span data-stu-id="cc47a-118">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="cc47a-119">Może to być przydatne, jeśli odwołujesz się projekty, które są PackageReference różne (istniejącego pliku csproj lub projektów w stylu zestawu SDK).</span><span class="sxs-lookup"><span data-stu-id="cc47a-119">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="cc47a-120">Spowoduje to włączenie pakiety, które projekty dotyczą przywoływanie "przechodnio" w projekcie.</span><span class="sxs-lookup"><span data-stu-id="cc47a-120">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="cc47a-121">Wersje</span><span class="sxs-lookup"><span data-stu-id="cc47a-121">Floating Versions</span></span>

<span data-ttu-id="cc47a-122">[Wersje](../consume-packages/dependency-resolution.md#floating-versions) są obsługiwane w przypadku `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="cc47a-122">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="cc47a-123">Kontrolowanie zależności zasobów</span><span class="sxs-lookup"><span data-stu-id="cc47a-123">Controlling dependency assets</span></span>

<span data-ttu-id="cc47a-124">Być może używasz zależność wyłącznie jako kontroler rozwoju i nie chcieć ujawnić, do projektów, które będą korzystać z pakietu.</span><span class="sxs-lookup"><span data-stu-id="cc47a-124">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="cc47a-125">W tym scenariuszu można użyć `PrivateAssets` metadanych w celu kontrolowania tego zachowania.</span><span class="sxs-lookup"><span data-stu-id="cc47a-125">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="cc47a-126">Następujące tagi metadanych kontrolować zasoby zależności:</span><span class="sxs-lookup"><span data-stu-id="cc47a-126">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="cc47a-127">Tag</span><span class="sxs-lookup"><span data-stu-id="cc47a-127">Tag</span></span> | <span data-ttu-id="cc47a-128">Opis</span><span class="sxs-lookup"><span data-stu-id="cc47a-128">Description</span></span> | <span data-ttu-id="cc47a-129">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="cc47a-129">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cc47a-130">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="cc47a-130">IncludeAssets</span></span> | <span data-ttu-id="cc47a-131">Te zasoby będą używane.</span><span class="sxs-lookup"><span data-stu-id="cc47a-131">These assets will be consumed</span></span> | <span data-ttu-id="cc47a-132">wszystkie</span><span class="sxs-lookup"><span data-stu-id="cc47a-132">all</span></span> |
| <span data-ttu-id="cc47a-133">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="cc47a-133">ExcludeAssets</span></span> | <span data-ttu-id="cc47a-134">Te zasoby nie będą używane.</span><span class="sxs-lookup"><span data-stu-id="cc47a-134">These assets will not be consumed</span></span> | <span data-ttu-id="cc47a-135">brak</span><span class="sxs-lookup"><span data-stu-id="cc47a-135">none</span></span> |
| <span data-ttu-id="cc47a-136">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="cc47a-136">PrivateAssets</span></span> | <span data-ttu-id="cc47a-137">Te zasoby będą używane, ale nie będzie przepływać do projektu nadrzędnego</span><span class="sxs-lookup"><span data-stu-id="cc47a-137">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="cc47a-138">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="cc47a-138">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="cc47a-139">Dopuszczalnych wartości dla tych tagów, są w następujący sposób, przy użyciu wielu wartości, rozdzielając je średnikiem z wyjątkiem za pomocą `all` i `none` której musi znajdować się w sobie:</span><span class="sxs-lookup"><span data-stu-id="cc47a-139">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="cc47a-140">Wartość</span><span class="sxs-lookup"><span data-stu-id="cc47a-140">Value</span></span> | <span data-ttu-id="cc47a-141">Opis</span><span class="sxs-lookup"><span data-stu-id="cc47a-141">Description</span></span> |
| --- | ---
| <span data-ttu-id="cc47a-142">Kompilacji</span><span class="sxs-lookup"><span data-stu-id="cc47a-142">compile</span></span> | <span data-ttu-id="cc47a-143">Zawartość `lib` folder i formanty czy projektu można kompilować dla zestawów w folderze</span><span class="sxs-lookup"><span data-stu-id="cc47a-143">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="cc47a-144">środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="cc47a-144">runtime</span></span> | <span data-ttu-id="cc47a-145">Zawartość `lib` i `runtimes` folder i formanty czy te zestawy będzie kopiowana do kompilacji katalogu wyjściowego</span><span class="sxs-lookup"><span data-stu-id="cc47a-145">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="cc47a-146">Pliki</span><span class="sxs-lookup"><span data-stu-id="cc47a-146">contentFiles</span></span> | <span data-ttu-id="cc47a-147">Zawartość `contentfiles` folderu</span><span class="sxs-lookup"><span data-stu-id="cc47a-147">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="cc47a-148">kompilacja</span><span class="sxs-lookup"><span data-stu-id="cc47a-148">build</span></span> | <span data-ttu-id="cc47a-149">Właściwości i elementów docelowych w `build` folderu</span><span class="sxs-lookup"><span data-stu-id="cc47a-149">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="cc47a-150">Analizatory</span><span class="sxs-lookup"><span data-stu-id="cc47a-150">analyzers</span></span> | <span data-ttu-id="cc47a-151">Analizatory platformy .NET</span><span class="sxs-lookup"><span data-stu-id="cc47a-151">.NET analyzers</span></span> |
| <span data-ttu-id="cc47a-152">natywne</span><span class="sxs-lookup"><span data-stu-id="cc47a-152">native</span></span> | <span data-ttu-id="cc47a-153">Zawartość `native` folderu</span><span class="sxs-lookup"><span data-stu-id="cc47a-153">Contents of the `native` folder</span></span> |
| <span data-ttu-id="cc47a-154">brak</span><span class="sxs-lookup"><span data-stu-id="cc47a-154">none</span></span> | <span data-ttu-id="cc47a-155">Żadne z powyższych są używane.</span><span class="sxs-lookup"><span data-stu-id="cc47a-155">None of the above are used.</span></span> |
| <span data-ttu-id="cc47a-156">wszystkie</span><span class="sxs-lookup"><span data-stu-id="cc47a-156">all</span></span> | <span data-ttu-id="cc47a-157">Wszystkie powyższe (z wyjątkiem `none`)</span><span class="sxs-lookup"><span data-stu-id="cc47a-157">All of the above (except `none`)</span></span> |

<span data-ttu-id="cc47a-158">W poniższym przykładzie wszystkim, z wyjątkiem plików zawartości z pakietu może być używane przez projekt i wszystkim, z wyjątkiem analizatory i pliki zawartości będą przepływać do projektu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="cc47a-158">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="cc47a-159">Należy pamiętać, że ponieważ `build` nie znajduje się za pomocą `PrivateAssets`, cele i właściwości *będzie* przepływ do nadrzędnego projektu.</span><span class="sxs-lookup"><span data-stu-id="cc47a-159">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="cc47a-160">Należy wziąć pod uwagę, na przykład, że odwołanie powyżej jest używany w projekcie, który tworzy pakiet NuGet o nazwie AppLogger.</span><span class="sxs-lookup"><span data-stu-id="cc47a-160">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="cc47a-161">AppLogger mogą wykorzystywać obiektów docelowych i właściwości z `Contoso.Utility.UsefulStuff`, tak jak w projektach korzystających z AppLogger.</span><span class="sxs-lookup"><span data-stu-id="cc47a-161">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="cc47a-162">Dodawanie warunku PackageReference</span><span class="sxs-lookup"><span data-stu-id="cc47a-162">Adding a PackageReference condition</span></span>

<span data-ttu-id="cc47a-163">Możesz użyć warunek do kontroli, czy pakiet jest uwzględnione, w przypadku, gdy warunki, można użyć dowolnej zmiennej programu MSBuild lub zmienną zdefiniowaną w pliku elementów docelowych lub właściwości.</span><span class="sxs-lookup"><span data-stu-id="cc47a-163">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="cc47a-164">Jednak w obecnie tylko `TargetFramework` zmienna jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="cc47a-164">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="cc47a-165">Załóżmy na przykład, gdy elementem docelowym `netstandard1.4` także `net452` , ale ma zależność, która ma zastosowanie tylko do `net452`.</span><span class="sxs-lookup"><span data-stu-id="cc47a-165">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="cc47a-166">W takim przypadku nie ma `netstandard1.4` projektu, który zużywa pakietu do dodania tej zależności niepotrzebne.</span><span class="sxs-lookup"><span data-stu-id="cc47a-166">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="cc47a-167">Aby temu zapobiec, określamy warunek na `PackageReference` w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="cc47a-167">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="cc47a-168">Pakiet, który został skompilowany przy użyciu tego projektu pokaże, że pakiet Newtonsoft.Json jest uwzględniany jako zależności tylko w przypadku `net452` docelowej:</span><span class="sxs-lookup"><span data-stu-id="cc47a-168">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Wynik zastosowania warunku na PackageReference za pomocą programu VS 2017](media/PackageReference-Condition.png)

<span data-ttu-id="cc47a-170">Warunki mogą być również stosowane przy `ItemGroup` poziomu i będą stosowane do wszystkich obiektów podrzędnych `PackageReference` elementy:</span><span class="sxs-lookup"><span data-stu-id="cc47a-170">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a><span data-ttu-id="cc47a-171">Blokowanie zależności</span><span class="sxs-lookup"><span data-stu-id="cc47a-171">Locking dependencies</span></span>
<span data-ttu-id="cc47a-172">*Ta funkcja jest dostępna z NuGet **4.9** lub w górę i w programie Visual Studio 2017 **15.9** lub nowszej.*</span><span class="sxs-lookup"><span data-stu-id="cc47a-172">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="cc47a-173">Dane wejściowe, aby przywracanie pakietów NuGet jest zestaw odwołania do pakietu z pliku projektu (zależności najwyższego poziomu lub direct) i dane wyjściowe są pełne zamknięcie wszystkie zależności pakietów wraz z zależnościami przechodnie.</span><span class="sxs-lookup"><span data-stu-id="cc47a-173">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="cc47a-174">NuGet próbuje zawsze powodowało tego samego pełne zamknięcie zależności pakietów, jeśli lista wejściowa PackageReference nie uległy zmianie.</span><span class="sxs-lookup"><span data-stu-id="cc47a-174">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="cc47a-175">Jednak istnieją pewne scenariusze, w którym nie jest w stanie to zrobić.</span><span class="sxs-lookup"><span data-stu-id="cc47a-175">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="cc47a-176">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="cc47a-176">For example:</span></span>

* <span data-ttu-id="cc47a-177">Gdy używasz liczb zmiennoprzecinkowych wersji, takich jak `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span><span class="sxs-lookup"><span data-stu-id="cc47a-177">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="cc47a-178">Natomiast tutaj jest float do najnowszej wersji podczas każdego przywracania pakietów, istnieją scenariusze, w której użytkownicy wymagają wykresu zostanie zablokowane do niektórych najnowszej wersji, a wartość zmiennoprzecinkowa do nowszej wersji, jeśli to możliwe, na jawne gestu.</span><span class="sxs-lookup"><span data-stu-id="cc47a-178">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="cc47a-179">Nowsza wersja pakietu zgodnego PackageReference wymagania dotyczące wersji została opublikowana.</span><span class="sxs-lookup"><span data-stu-id="cc47a-179">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="cc47a-180">Na przykład</span><span class="sxs-lookup"><span data-stu-id="cc47a-180">E.g.</span></span> 

  * <span data-ttu-id="cc47a-181">Dzień 1: Jeśli określono `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` , ale wersje dostępne w repozytoria NuGet 4.1.0, 4.2.0 i 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="cc47a-181">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="cc47a-182">W tym przypadku NuGet czy problem został rozwiązany w celu 4.1.0 (najbliższym minimalna wersja)</span><span class="sxs-lookup"><span data-stu-id="cc47a-182">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="cc47a-183">Dzień 2: Zostanie opublikowany w wersji 4.0.0.</span><span class="sxs-lookup"><span data-stu-id="cc47a-183">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="cc47a-184">NuGet teraz zostanie znalezione dokładne dopasowanie i uruchomienia rozpoznawania 4.0.0</span><span class="sxs-lookup"><span data-stu-id="cc47a-184">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="cc47a-185">Wersja dany pakiet zostanie usunięty z repozytorium.</span><span class="sxs-lookup"><span data-stu-id="cc47a-185">A given package version is removed from the repository.</span></span> <span data-ttu-id="cc47a-186">Chociaż nuget.org nie zezwala na usunięcia pakietu, nie wszystkie repozytoria pakietu ma tego ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="cc47a-186">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="cc47a-187">Skutkuje to znajdowanie najlepsze dopasowanie, gdy nie można rozpoznać usuniętych wersji NuGet.</span><span class="sxs-lookup"><span data-stu-id="cc47a-187">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="cc47a-188">Włączenie pliku blokady</span><span class="sxs-lookup"><span data-stu-id="cc47a-188">Enabling lock file</span></span>
<span data-ttu-id="cc47a-189">Aby zachować pełną zamknięcia zależności pakietów, które użytkownik może wyrazić zgodę na funkcji blokowania plików, ustawiając właściwość MSBuild `RestorePackagesWithLockFile` dla projektu:</span><span class="sxs-lookup"><span data-stu-id="cc47a-189">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="cc47a-190">Jeśli ta właściwość jest ustawiona, przywracanie pakietów NuGet, spowoduje wygenerowanie pliku blokady - `packages.lock.json` pliku w katalogu głównym projektu, który znajduje się wykaz zależności pakietów.</span><span class="sxs-lookup"><span data-stu-id="cc47a-190">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="cc47a-191">Gdy projekt ma `packages.lock.json` plik w jego katalogu głównego pliku blokady jest zawsze używane przy użyciu przywracania nawet wtedy, gdy właściwość `RestorePackagesWithLockFile` nie jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="cc47a-191">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="cc47a-192">Dlatego inny sposób, aby wyrazić zgodę na tę funkcję, jest utworzenie pustego fikcyjnego `packages.lock.json` pliku w katalogu głównym projektu.</span><span class="sxs-lookup"><span data-stu-id="cc47a-192">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="cc47a-193">`restore` zachowanie przy użyciu pliku blokady</span><span class="sxs-lookup"><span data-stu-id="cc47a-193">`restore` behavior with lock file</span></span>
<span data-ttu-id="cc47a-194">Jeśli plik blokady jest obecny dla projektu, NuGet używa tego pliku blokady, aby uruchomić `restore`.</span><span class="sxs-lookup"><span data-stu-id="cc47a-194">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="cc47a-195">NuGet jest szybkie sprawdzenie, czy wystąpiły wszelkie zmiany w zależności pakietów, jak wspomniano wcześniej w pliku projektu (lub pliki projektów zależnych), a jeśli nie wprowadzono żadnych zmian po prostu przywraca pakiety wymienione w pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="cc47a-195">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="cc47a-196">Nie ma żadnych ponownej oceny zależności pakietów.</span><span class="sxs-lookup"><span data-stu-id="cc47a-196">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="cc47a-197">Jeśli NuGet wykryje zmianę w zdefiniowanych zależności, jak wspomniano w plikach projektu, ponownie ocenia wykres pakietu i aktualizuje plik blokady w celu odzwierciedlenia nowego zamknięcia pakietu dla projektu.</span><span class="sxs-lookup"><span data-stu-id="cc47a-197">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="cc47a-198">Ciągła Integracja/ciągłe dostarczanie i inne scenariusze, w których nie chcesz zmienić zależności pakietów na bieżąco, możesz to zrobić, ustawiając `lockedmode` do `true`:</span><span class="sxs-lookup"><span data-stu-id="cc47a-198">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="cc47a-199">Aby uzyskać dotnet.exe Uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="cc47a-199">For dotnet.exe, run:</span></span>
```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="cc47a-200">Aby uzyskać msbuild.exe Uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="cc47a-200">For msbuild.exe, run:</span></span>
```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="cc47a-201">Można również ustawić właściwość ta warunkowe MSBuild w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="cc47a-201">You may also set this conditional MSBuild property in your project file:</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="cc47a-202">Jeśli w trybie zablokowanym `true`, przywracania będzie przywrócić dokładnie pakiety wymienione w pliku blokady lub się nie powieść, jeśli zaktualizowane zależności pakietu zdefiniowanych dla projektu, po utworzeniu pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="cc47a-202">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="cc47a-203">Blokowanie pliku częścią repozytorium źródłowym</span><span class="sxs-lookup"><span data-stu-id="cc47a-203">Make lock file part of your source repository</span></span>
<span data-ttu-id="cc47a-204">Jeśli tworzysz aplikację, plik wykonywalny, a projekt jest na początku łańcuch zależności następnie zaewidencjonuj pliku blokady do repozytorium kodu źródłowego tak, aby wprowadzić NuGet z niego korzystać podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="cc47a-204">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="cc47a-205">Jednakże jeśli projekt jest projekt biblioteki, które nie dostarczaj lub wspólnej projekt kodu, na które inne projekty zależą od tego, możesz **nie powinien** Zaewidencjonuj pliku blokady jako część kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="cc47a-205">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="cc47a-206">Nie przynosi żadnych szkód w ochronie pliku blokady, ale zależności pakietu zablokowany dla wspólnego projektu kodu nie można używać, zgodnie z zaleceniami z pliku blokady podczas przywracania/kompilacji projektu, który zależy od tego projektu wspólnego kodu.</span><span class="sxs-lookup"><span data-stu-id="cc47a-206">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="cc47a-207">Np.</span><span class="sxs-lookup"><span data-stu-id="cc47a-207">Eg.</span></span>
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
<span data-ttu-id="cc47a-208">Jeśli `ProjectA` zależny od `PackageX` wersji `2.0.0` i odwołujący się `ProjectB` zależy `PackageX` wersji `1.0.0`, następnie blokada pliku `ProjectB` będzie wyświetlana zależność `PackageX` Wersja `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="cc47a-208">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="cc47a-209">Jednak, gdy `ProjectA` powstała blokady plik będzie zawierać zależności na `PackageX` wersji **`2.0.0`** i **nie** `1.0.0` wymienionych w pliku blokady `ProjectB`.</span><span class="sxs-lookup"><span data-stu-id="cc47a-209">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="cc47a-210">W związku z tym plik blokady wspólnego projektu kodu ma nieco powiedzieć za pośrednictwem pakietów dla projektów, które zależą od niej.</span><span class="sxs-lookup"><span data-stu-id="cc47a-210">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="cc47a-211">Rozszerzalność pliku blokady</span><span class="sxs-lookup"><span data-stu-id="cc47a-211">Lock file extensibility</span></span>
<span data-ttu-id="cc47a-212">Aby sterować różnych zachowań przywracania za pomocą pliku blokady, zgodnie z poniższym opisem:</span><span class="sxs-lookup"><span data-stu-id="cc47a-212">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="cc47a-213">Opcja</span><span class="sxs-lookup"><span data-stu-id="cc47a-213">Option</span></span> | <span data-ttu-id="cc47a-214">Opcji równoważne MSBuild</span><span class="sxs-lookup"><span data-stu-id="cc47a-214">MSBuild equivalent option</span></span> | 
|:---  |:--- |
| `--use-lock-file` | <span data-ttu-id="cc47a-215">Bootstraps korzystanie z pliku blokady dla projektu.</span><span class="sxs-lookup"><span data-stu-id="cc47a-215">Bootstraps use of lock file for a project.</span></span> <span data-ttu-id="cc47a-216">Można również ustawić `RestorePackagesWithLockFile` właściwość w pliku projektu</span><span class="sxs-lookup"><span data-stu-id="cc47a-216">You can alternatively set `RestorePackagesWithLockFile` property in the project file</span></span> | 
| `--locked-mode` | <span data-ttu-id="cc47a-217">Włącza zablokowany tryb przywracania.</span><span class="sxs-lookup"><span data-stu-id="cc47a-217">Enables locked mode for restore.</span></span> <span data-ttu-id="cc47a-218">Jest to przydatne w scenariuszach ciągłej integracji/ciągłego wdrażania, w której chcesz uzyskać powtarzalnych kompilacji.</span><span class="sxs-lookup"><span data-stu-id="cc47a-218">This is useful in CI/CD scenarios where you would like to get the repeatable builds.</span></span> <span data-ttu-id="cc47a-219">Może to być również przez ustawienie `RestoreLockedMode` właściwości programu MSBuild `true`</span><span class="sxs-lookup"><span data-stu-id="cc47a-219">This can be also by setting the `RestoreLockedMode` MSBuild property to `true`</span></span> |  
| `--force-evaluate` | <span data-ttu-id="cc47a-220">Ta opcja jest przydatna przy użyciu pakietów przy użyciu wersji zmiennoprzecinkowy zdefiniowane w projekcie.</span><span class="sxs-lookup"><span data-stu-id="cc47a-220">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="cc47a-221">Domyślnie, przywracanie pakietów NuGet nie może zaktualizować wersję pakietu automatycznie po każdym przywracania, chyba że uruchomieniu przywracania z `--force-evaluate` opcji.</span><span class="sxs-lookup"><span data-stu-id="cc47a-221">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with `--force-evaluate` option.</span></span> |
| `--lock-file-path` | <span data-ttu-id="cc47a-222">Definiuje blokady niestandardowych lokalizacji plików dla projektu.</span><span class="sxs-lookup"><span data-stu-id="cc47a-222">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="cc47a-223">Można to również osiągnąć przez ustawienie właściwości programu MSBuild `NuGetLockFilePath`.</span><span class="sxs-lookup"><span data-stu-id="cc47a-223">This can be also achieved by setting the MSBuild property `NuGetLockFilePath`.</span></span> <span data-ttu-id="cc47a-224">Domyślnie obsługuje NuGet `packages.lock.json` w katalogu głównym.</span><span class="sxs-lookup"><span data-stu-id="cc47a-224">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="cc47a-225">Jeśli masz wiele projektów w tym samym katalogu NuGet obsługuje pliku blokady określonego projektu `packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="cc47a-225">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
