---
title: Formatu NuGet PackageReference (odwołania do pakietu w plikach projektu)
description: Szczegółowe informacje na temat formatu NuGet PackageReference w plikach projektu jako obsługiwane przez NuGet 4.0 + i programu VS 2017 i platformy .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 17960e42a69b00f2524b9ab7d78710d7551b5a9c
ms.sourcegitcommit: a1846edf70ddb2505d58e536e08e952d870931b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2018
ms.locfileid: "52303657"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="a82c8-103">Odwołania do pakietu (PackageReference) w plikach projektu</span><span class="sxs-lookup"><span data-stu-id="a82c8-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="a82c8-104">Pakiet odwołań, za pomocą `PackageReference` węzła, zarządzanie zależnościami NuGet bezpośrednio z poziomu plików projektu (w przeciwieństwie do oddzielnego `packages.config` pliku).</span><span class="sxs-lookup"><span data-stu-id="a82c8-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="a82c8-105">Za pomocą funkcji PackageReference, ponieważ jest to, nie ma wpływu na inne aspekty pakietu nuget; na przykład ustawienia "NuGet.</span><span class="sxs-lookup"><span data-stu-id="a82c8-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in \`NuGet.</span></span>





<span data-ttu-id="a82c8-106">fig "plików (w tym źródeł pakietów) nadal są stosowane zgodnie z objaśnieniem w [Konfigurowanie zachowania pakietu NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="a82c8-106">fig\` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="a82c8-107">Za pomocą funkcji PackageReference umożliwia także warunki MSBuild do wyboru na platformę docelową, konfiguracji, platforma lub inne grupy będzie odwoływał się pakiet.</span><span class="sxs-lookup"><span data-stu-id="a82c8-107">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="a82c8-108">Umożliwia ona również szczegółową kontrolę nad tym zależności i zawartości przepływu.</span><span class="sxs-lookup"><span data-stu-id="a82c8-108">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="a82c8-109">(Aby uzyskać więcej informacji, zobacz [NuGet pakowanie i przywrócić jako elementów docelowych MSBuild](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="a82c8-109">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="a82c8-110">Domyślnie PackageReference jest używany dla projektów .NET Core, .NET Standard projektów i projektów platformy UWP przeznaczonych dla systemu Windows 10 kompilacja 15063 (Aktualizacja dla twórców) lub nowszy, z wyjątkiem projektów platformy UWP w języku C++.</span><span class="sxs-lookup"><span data-stu-id="a82c8-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="a82c8-111">Projektów programu .NET framework obsługuje PackageReference, ale obecnie domyślnie `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="a82c8-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="a82c8-112">Aby korzystać z funkcji PackageReference, migracja zależności z `packages.config` do pliku projektu, a następnie usuń packages.config.</span><span class="sxs-lookup"><span data-stu-id="a82c8-112">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="a82c8-113">Dodawanie odwołanie PackageReference</span><span class="sxs-lookup"><span data-stu-id="a82c8-113">Adding a PackageReference</span></span>

<span data-ttu-id="a82c8-114">Dodawanie zależności w pliku projektu przy użyciu następującej składni:</span><span class="sxs-lookup"><span data-stu-id="a82c8-114">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="a82c8-115">Kontrolowanie wersja zależności</span><span class="sxs-lookup"><span data-stu-id="a82c8-115">Controlling dependency version</span></span>

<span data-ttu-id="a82c8-116">Konwencja określania wersję pakietu jest taka sama jak, korzystając z `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="a82c8-116">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="a82c8-117">W powyższym przykładzie 3.6.0 oznacza dowolną wersję, którą jest > = 3.6.0 z preferencją dla Najniższa wersja zgodnie z opisem na [przechowywanie wersji pakietów](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="a82c8-117">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="a82c8-118">Za pomocą funkcji PackageReference dla projektu z nie składnika PackageReferences</span><span class="sxs-lookup"><span data-stu-id="a82c8-118">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="a82c8-119">Zaawansowane: Jeśli ma żadnych pakietów zainstalowany w projekcie (nie składnika PackageReferences w pliku projektu) i Brak pliku packages.config, ale Project, które ma zostać przywrócone jako styl PackageReference, możesz ustawić właściwość projektu RestoreProjectStyle do odwołania PackageReference w plik projektu.</span><span class="sxs-lookup"><span data-stu-id="a82c8-119">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="a82c8-120">Może to być przydatne, jeśli odwołujesz się projekty, które są PackageReference różne (istniejącego pliku csproj lub projektów w stylu zestawu SDK).</span><span class="sxs-lookup"><span data-stu-id="a82c8-120">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="a82c8-121">Spowoduje to włączenie pakiety, które projekty dotyczą przywoływanie "przechodnio" w projekcie.</span><span class="sxs-lookup"><span data-stu-id="a82c8-121">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="a82c8-122">Wersje</span><span class="sxs-lookup"><span data-stu-id="a82c8-122">Floating Versions</span></span>

<span data-ttu-id="a82c8-123">[Wersje](../consume-packages/dependency-resolution.md#floating-versions) są obsługiwane w przypadku `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="a82c8-123">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="a82c8-124">Kontrolowanie zależności zasobów</span><span class="sxs-lookup"><span data-stu-id="a82c8-124">Controlling dependency assets</span></span>

<span data-ttu-id="a82c8-125">Być może używasz zależność wyłącznie jako kontroler rozwoju i nie chcieć ujawnić, do projektów, które będą korzystać z pakietu.</span><span class="sxs-lookup"><span data-stu-id="a82c8-125">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="a82c8-126">W tym scenariuszu można użyć `PrivateAssets` metadanych w celu kontrolowania tego zachowania.</span><span class="sxs-lookup"><span data-stu-id="a82c8-126">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="a82c8-127">Następujące tagi metadanych kontrolować zasoby zależności:</span><span class="sxs-lookup"><span data-stu-id="a82c8-127">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="a82c8-128">Tag</span><span class="sxs-lookup"><span data-stu-id="a82c8-128">Tag</span></span> | <span data-ttu-id="a82c8-129">Opis</span><span class="sxs-lookup"><span data-stu-id="a82c8-129">Description</span></span> | <span data-ttu-id="a82c8-130">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="a82c8-130">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a82c8-131">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="a82c8-131">IncludeAssets</span></span> | <span data-ttu-id="a82c8-132">Te zasoby będą używane.</span><span class="sxs-lookup"><span data-stu-id="a82c8-132">These assets will be consumed</span></span> | <span data-ttu-id="a82c8-133">wszystkie</span><span class="sxs-lookup"><span data-stu-id="a82c8-133">all</span></span> |
| <span data-ttu-id="a82c8-134">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="a82c8-134">ExcludeAssets</span></span> | <span data-ttu-id="a82c8-135">Te zasoby nie będą używane.</span><span class="sxs-lookup"><span data-stu-id="a82c8-135">These assets will not be consumed</span></span> | <span data-ttu-id="a82c8-136">brak</span><span class="sxs-lookup"><span data-stu-id="a82c8-136">none</span></span> |
| <span data-ttu-id="a82c8-137">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="a82c8-137">PrivateAssets</span></span> | <span data-ttu-id="a82c8-138">Te zasoby będą używane, ale nie będzie przepływać do projektu nadrzędnego</span><span class="sxs-lookup"><span data-stu-id="a82c8-138">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="a82c8-139">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="a82c8-139">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="a82c8-140">Dopuszczalnych wartości dla tych tagów, są w następujący sposób, przy użyciu wielu wartości, rozdzielając je średnikiem z wyjątkiem za pomocą `all` i `none` której musi znajdować się w sobie:</span><span class="sxs-lookup"><span data-stu-id="a82c8-140">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="a82c8-141">Wartość</span><span class="sxs-lookup"><span data-stu-id="a82c8-141">Value</span></span> | <span data-ttu-id="a82c8-142">Opis</span><span class="sxs-lookup"><span data-stu-id="a82c8-142">Description</span></span> |
| --- | ---
| <span data-ttu-id="a82c8-143">Kompilacji</span><span class="sxs-lookup"><span data-stu-id="a82c8-143">compile</span></span> | <span data-ttu-id="a82c8-144">Zawartość `lib` folder i formanty czy projektu można kompilować dla zestawów w folderze</span><span class="sxs-lookup"><span data-stu-id="a82c8-144">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="a82c8-145">środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="a82c8-145">runtime</span></span> | <span data-ttu-id="a82c8-146">Zawartość `lib` i `runtimes` folder i formanty czy te zestawy będzie kopiowana do kompilacji katalogu wyjściowego</span><span class="sxs-lookup"><span data-stu-id="a82c8-146">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="a82c8-147">Pliki</span><span class="sxs-lookup"><span data-stu-id="a82c8-147">contentFiles</span></span> | <span data-ttu-id="a82c8-148">Zawartość `contentfiles` folderu</span><span class="sxs-lookup"><span data-stu-id="a82c8-148">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="a82c8-149">kompilacja</span><span class="sxs-lookup"><span data-stu-id="a82c8-149">build</span></span> | <span data-ttu-id="a82c8-150">Właściwości i elementów docelowych w `build` folderu</span><span class="sxs-lookup"><span data-stu-id="a82c8-150">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="a82c8-151">Analizatory</span><span class="sxs-lookup"><span data-stu-id="a82c8-151">analyzers</span></span> | <span data-ttu-id="a82c8-152">Analizatory platformy .NET</span><span class="sxs-lookup"><span data-stu-id="a82c8-152">.NET analyzers</span></span> |
| <span data-ttu-id="a82c8-153">natywne</span><span class="sxs-lookup"><span data-stu-id="a82c8-153">native</span></span> | <span data-ttu-id="a82c8-154">Zawartość `native` folderu</span><span class="sxs-lookup"><span data-stu-id="a82c8-154">Contents of the `native` folder</span></span> |
| <span data-ttu-id="a82c8-155">brak</span><span class="sxs-lookup"><span data-stu-id="a82c8-155">none</span></span> | <span data-ttu-id="a82c8-156">Żadne z powyższych są używane.</span><span class="sxs-lookup"><span data-stu-id="a82c8-156">None of the above are used.</span></span> |
| <span data-ttu-id="a82c8-157">wszystkie</span><span class="sxs-lookup"><span data-stu-id="a82c8-157">all</span></span> | <span data-ttu-id="a82c8-158">Wszystkie powyższe (z wyjątkiem `none`)</span><span class="sxs-lookup"><span data-stu-id="a82c8-158">All of the above (except `none`)</span></span> |

<span data-ttu-id="a82c8-159">W poniższym przykładzie wszystkim, z wyjątkiem plików zawartości z pakietu może być używane przez projekt i wszystkim, z wyjątkiem analizatory i pliki zawartości będą przepływać do projektu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="a82c8-159">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="a82c8-160">Należy pamiętać, że ponieważ `build` nie znajduje się za pomocą `PrivateAssets`, cele i właściwości *będzie* przepływ do nadrzędnego projektu.</span><span class="sxs-lookup"><span data-stu-id="a82c8-160">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="a82c8-161">Należy wziąć pod uwagę, na przykład, że odwołanie powyżej jest używany w projekcie, który tworzy pakiet NuGet o nazwie AppLogger.</span><span class="sxs-lookup"><span data-stu-id="a82c8-161">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="a82c8-162">AppLogger mogą wykorzystywać obiektów docelowych i właściwości z `Contoso.Utility.UsefulStuff`, tak jak w projektach korzystających z AppLogger.</span><span class="sxs-lookup"><span data-stu-id="a82c8-162">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="a82c8-163">Dodawanie warunku PackageReference</span><span class="sxs-lookup"><span data-stu-id="a82c8-163">Adding a PackageReference condition</span></span>

<span data-ttu-id="a82c8-164">Możesz użyć warunek do kontroli, czy pakiet jest uwzględnione, w przypadku, gdy warunki, można użyć dowolnej zmiennej programu MSBuild lub zmienną zdefiniowaną w pliku elementów docelowych lub właściwości.</span><span class="sxs-lookup"><span data-stu-id="a82c8-164">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="a82c8-165">Jednak w obecnie tylko `TargetFramework` zmienna jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="a82c8-165">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="a82c8-166">Załóżmy na przykład, gdy elementem docelowym `netstandard1.4` także `net452` , ale ma zależność, która ma zastosowanie tylko do `net452`.</span><span class="sxs-lookup"><span data-stu-id="a82c8-166">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="a82c8-167">W takim przypadku nie ma `netstandard1.4` projektu, który zużywa pakietu do dodania tej zależności niepotrzebne.</span><span class="sxs-lookup"><span data-stu-id="a82c8-167">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="a82c8-168">Aby temu zapobiec, określamy warunek na `PackageReference` w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a82c8-168">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="a82c8-169">Pakiet, który został skompilowany przy użyciu tego projektu pokaże, że pakiet Newtonsoft.Json jest uwzględniany jako zależności tylko w przypadku `net452` docelowej:</span><span class="sxs-lookup"><span data-stu-id="a82c8-169">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Wynik zastosowania warunku na PackageReference za pomocą programu VS 2017](media/PackageReference-Condition.png)

<span data-ttu-id="a82c8-171">Warunki mogą być również stosowane przy `ItemGroup` poziomu i będą stosowane do wszystkich obiektów podrzędnych `PackageReference` elementy:</span><span class="sxs-lookup"><span data-stu-id="a82c8-171">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a><span data-ttu-id="a82c8-172">Blokowanie zależności</span><span class="sxs-lookup"><span data-stu-id="a82c8-172">Locking dependencies</span></span>
<span data-ttu-id="a82c8-173">*Ta funkcja jest dostępna z NuGet **4.9** lub w górę i w programie Visual Studio 2017 **15.9 w wersji zapoznawczej 5** lub nowszej.*</span><span class="sxs-lookup"><span data-stu-id="a82c8-173">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9 Preview 5** or above.*</span></span>

<span data-ttu-id="a82c8-174">Dane wejściowe, aby przywracanie pakietów NuGet jest zestaw odwołania do pakietu z pliku projektu (dependenices najwyższego poziomu lub direct) i dane wyjściowe są pełne zamknięcie wszystkie zależności pakietów wraz z zależnościami przechodnie.</span><span class="sxs-lookup"><span data-stu-id="a82c8-174">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependenices) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="a82c8-175">NuGet próbuje zawsze powodowało tego samego pełne zamknięcie zależności pakietów, jeśli lista wejściowa PackageReference nie uległy zmianie.</span><span class="sxs-lookup"><span data-stu-id="a82c8-175">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="a82c8-176">Jednak istnieją pewne scenariusze, w którym nie jest w stanie to zrobić.</span><span class="sxs-lookup"><span data-stu-id="a82c8-176">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="a82c8-177">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="a82c8-177">For example:</span></span>

* <span data-ttu-id="a82c8-178">Gdy używasz liczb zmiennoprzecinkowych wersji, takich jak `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span><span class="sxs-lookup"><span data-stu-id="a82c8-178">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="a82c8-179">Natomiast tutaj jest float do najnowszej wersji podczas każdego przywracania pakietów, istnieją scenariusze, w której użytkownicy wymagają wykresu zostanie zablokowane do niektórych najnowszej wersji, a wartość zmiennoprzecinkowa do nowszej wersji, jeśli to możliwe, na jawne gestu.</span><span class="sxs-lookup"><span data-stu-id="a82c8-179">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="a82c8-180">Nowsza wersja pakietu zgodnego PackageReference wymagania dotyczące wersji została opublikowana.</span><span class="sxs-lookup"><span data-stu-id="a82c8-180">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="a82c8-181">Np.</span><span class="sxs-lookup"><span data-stu-id="a82c8-181">E.g.</span></span> 

  * <span data-ttu-id="a82c8-182">Dzień 1: Jeśli określono `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` , ale wersje dostępne w repozytoria NuGet 4.1.0, 4.2.0 i 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="a82c8-182">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="a82c8-183">W tym przypadku NuGet czy problem został rozwiązany w celu 4.1.0 (najbliższym minimalna wersja)</span><span class="sxs-lookup"><span data-stu-id="a82c8-183">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="a82c8-184">Dzień 2: Wersji 4.0.0 zostanie opublikowany.</span><span class="sxs-lookup"><span data-stu-id="a82c8-184">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="a82c8-185">NuGet teraz zostanie znalezione dokładne dopasowanie i uruchomienia rozpoznawania 4.0.0</span><span class="sxs-lookup"><span data-stu-id="a82c8-185">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="a82c8-186">Wersja dany pakiet zostanie usunięty z repozytorium.</span><span class="sxs-lookup"><span data-stu-id="a82c8-186">A given package version is removed from the repository.</span></span> <span data-ttu-id="a82c8-187">Chociaż nuget.org nie zezwala na usunięcia pakietu, nie wszystkie repozytoria pakietu ma tego ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="a82c8-187">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="a82c8-188">Skutkuje to znajdowanie najlepsze dopasowanie, gdy nie można rozpoznać usuniętych wersji NuGet.</span><span class="sxs-lookup"><span data-stu-id="a82c8-188">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="a82c8-189">Włączenie pliku blokady</span><span class="sxs-lookup"><span data-stu-id="a82c8-189">Enabling lock file</span></span>
<span data-ttu-id="a82c8-190">Aby zachować pełną zamknięcia zależności pakietów, które użytkownik może wyrazić zgodę na funkcji blokowania plików, ustawiając właściwość MSBuild `RestorePackagesWithLockFile` dla projektu:</span><span class="sxs-lookup"><span data-stu-id="a82c8-190">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="a82c8-191">Jeśli ta właściwość jest ustawiona, przywracanie pakietów NuGet, spowoduje wygenerowanie pliku blokady - `packages.lock.json` pliku w katalogu głównym projektu, który znajduje się wykaz zależności pakietów.</span><span class="sxs-lookup"><span data-stu-id="a82c8-191">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="a82c8-192">Gdy projekt ma `packages.lock.json` plik w jego katalogu głównego pliku blokady jest zawsze używane przy użyciu przywracania nawet wtedy, gdy właściwość `RestorePackagesWithLockFile` nie jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="a82c8-192">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="a82c8-193">Dlatego inny sposób, aby wyrazić zgodę na tę funkcję, jest utworzenie pustego fikcyjnego `packages.lock.json` pliku w katalogu głównym projektu.</span><span class="sxs-lookup"><span data-stu-id="a82c8-193">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="a82c8-194">`restore` zachowanie przy użyciu pliku blokady</span><span class="sxs-lookup"><span data-stu-id="a82c8-194">`restore` behavior with lock file</span></span>
<span data-ttu-id="a82c8-195">Jeśli plik blokady jest obecny dla projektu, NuGet używa tego pliku blokady, aby uruchomić `restore`.</span><span class="sxs-lookup"><span data-stu-id="a82c8-195">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="a82c8-196">NuGet jest szybkie sprawdzenie, czy wystąpiły wszelkie zmiany w zależności pakietów, jak wspomniano wcześniej w pliku projektu (lub pliki projektów zależnych), a jeśli nie wprowadzono żadnych zmian po prostu przywraca pakiety wymienione w pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="a82c8-196">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="a82c8-197">Nie ma żadnych ponownej oceny zależności pakietów.</span><span class="sxs-lookup"><span data-stu-id="a82c8-197">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="a82c8-198">Jeśli NuGet wykryje zmianę dependenices zdefiniowane, jak wspomniano w plikach projektu, ponownie ocenia wykres pakietu i aktualizuje plik blokady w celu odzwierciedlenia nowego zamknięcia pakietu dla projektu.</span><span class="sxs-lookup"><span data-stu-id="a82c8-198">If NuGet detects a change in the defined dependenices as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="a82c8-199">Ciągła Integracja/ciągłe dostarczanie i inne scenariusze, w których nie chcesz zmienić dependenies pakietu na bieżąco, możesz to zrobić, ustawiając `lockedmode` do `true`:</span><span class="sxs-lookup"><span data-stu-id="a82c8-199">For CI/CD and other scenarios, where you would not want to change the package dependenies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="a82c8-200">Aby uzyskać dotnet.exe Uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="a82c8-200">For dotnet.exe, run:</span></span>
```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="a82c8-201">Aby uzyskać msbuild.exe Uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="a82c8-201">For msbuild.exe, run:</span></span>
```
> msbuild.exe /t:restore /p:RestoreLockedMode=true
```

<span data-ttu-id="a82c8-202">Można również ustawić właściwość ta warunkowe MSBuild w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="a82c8-202">You may also set this conditional MSBuild property in your project file:</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="a82c8-203">Jeśli w trybie zablokowanym `true`, przywracania będzie przywrócić dokładnie pakiety wymienione w pliku blokady lub się nie powieść, jeśli zaktualizowane zależności pakietu zdefiniowanych dla projektu, po utworzeniu pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="a82c8-203">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="a82c8-204">Blokowanie pliku częścią repozytorium źródłowym</span><span class="sxs-lookup"><span data-stu-id="a82c8-204">Make lock file part of your source repository</span></span>
<span data-ttu-id="a82c8-205">Jeśli tworzysz aplikację, plik wykonywalny, a projekt jest na końcu łańcuch zależności następnie zaewidencjonuj pliku blokady do repozytorium kodu źródłowego tak, aby wprowadzić NuGet z niego korzystać podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="a82c8-205">If you are building an application, an executable and the project in question is at the end of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="a82c8-206">Jednakże jeśli projekt jest projekt biblioteki, które nie dostarczaj lub wspólnej projekt kodu, na które inne projekty zależą od tego, możesz **nie powinien** Zaewidencjonuj pliku blokady jako część kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="a82c8-206">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="a82c8-207">Nie przynosi żadnych szkód w ochronie pliku blokady, ale zależności pakietu zablokowany dla wspólnego projektu kodu nie można używać, zgodnie z zaleceniami z pliku blokady podczas przywracania/kompilacji projektu, który zależy od tego projektu wspólnego kodu.</span><span class="sxs-lookup"><span data-stu-id="a82c8-207">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="a82c8-208">Np.</span><span class="sxs-lookup"><span data-stu-id="a82c8-208">Eg.</span></span>
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
<span data-ttu-id="a82c8-209">Jeśli `ProjectA` zależny od `PackageX` wersji `2.0.0` i odwołujący się `ProjectB` zależy `PackageX` wersji `1.0.0`, następnie blokada pliku `ProjectB` będzie wyświetlana zależność `PackageX` Wersja `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="a82c8-209">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="a82c8-210">Jednak, gdy `ProjectA` powstała blokady plik będzie zawierać zależności na `PackageX` wersji **`2.0.0`** i **nie** `1.0.0` wymienionych w pliku blokady `ProjectB`.</span><span class="sxs-lookup"><span data-stu-id="a82c8-210">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="a82c8-211">W związku z tym plik blokady wspólnego projektu kodu ma nieco powiedzieć za pośrednictwem pakietów dla projektów, które zależą od niej.</span><span class="sxs-lookup"><span data-stu-id="a82c8-211">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="a82c8-212">Rozszerzalność pliku blokady</span><span class="sxs-lookup"><span data-stu-id="a82c8-212">Lock file extensibility</span></span>
<span data-ttu-id="a82c8-213">Aby sterować różnych zachowań przywracania za pomocą pliku blokady, zgodnie z poniższym opisem:</span><span class="sxs-lookup"><span data-stu-id="a82c8-213">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="a82c8-214">Opcja</span><span class="sxs-lookup"><span data-stu-id="a82c8-214">Option</span></span> | <span data-ttu-id="a82c8-215">Opcji równoważne MSBuild</span><span class="sxs-lookup"><span data-stu-id="a82c8-215">MSBuild equivalent option</span></span> | 
|:---  |:--- |
| `--use-lock-file` | <span data-ttu-id="a82c8-216">Bootstraps korzystanie z pliku blokady dla projektu.</span><span class="sxs-lookup"><span data-stu-id="a82c8-216">Bootstraps use of lock file for a project.</span></span> <span data-ttu-id="a82c8-217">Można również ustawić `RestorePackagesWithLockFile` właściwość w pliku projektu</span><span class="sxs-lookup"><span data-stu-id="a82c8-217">You can alternatively set `RestorePackagesWithLockFile` property in the project file</span></span> | 
| `--locked-mode` | <span data-ttu-id="a82c8-218">Włącza zablokowany tryb przywracania.</span><span class="sxs-lookup"><span data-stu-id="a82c8-218">Enables locked mode for restore.</span></span> <span data-ttu-id="a82c8-219">Jest to przydatne w scenariuszach ciągłej integracji/ciągłego wdrażania, w której chcesz uzyskać powtarzalnych kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a82c8-219">This is useful in CI/CD scenarios where you would like to get the repeatable builds.</span></span> <span data-ttu-id="a82c8-220">Może to być również przez ustawienie `RestoreLockedMode` właściwości programu MSBuild `true`</span><span class="sxs-lookup"><span data-stu-id="a82c8-220">This can be also by setting the `RestoreLockedMode` MSBuild property to `true`</span></span> |  
| `--force-evaluate` | <span data-ttu-id="a82c8-221">Ta opcja jest przydatna przy użyciu pakietów przy użyciu wersji zmiennoprzecinkowy zdefiniowane w projekcie.</span><span class="sxs-lookup"><span data-stu-id="a82c8-221">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="a82c8-222">Domyślnie, przywracanie pakietów NuGet nie może zaktualizować wersję pakietu automatycznie po każdym przywracania, chyba że uruchomieniu przywracania z `--force-evaluate` opcji.</span><span class="sxs-lookup"><span data-stu-id="a82c8-222">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with `--force-evaluate` option.</span></span> |
| `--lock-file-path` | <span data-ttu-id="a82c8-223">Definiuje blokady niestandardowych lokalizacji plików dla projektu.</span><span class="sxs-lookup"><span data-stu-id="a82c8-223">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="a82c8-224">Można to również osiągnąć przez ustawienie właściwości programu MSBuild `NuGetLockFilePath`.</span><span class="sxs-lookup"><span data-stu-id="a82c8-224">This can be also achieved by setting the MSBuild property `NuGetLockFilePath`.</span></span> <span data-ttu-id="a82c8-225">Domyślnie obsługuje NuGet `packages.lock.json` w katalogu głównym.</span><span class="sxs-lookup"><span data-stu-id="a82c8-225">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="a82c8-226">Jeśli masz wiele projektów w tym samym katalogu NuGet obsługuje pliku blokady określonego projektu `packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="a82c8-226">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
