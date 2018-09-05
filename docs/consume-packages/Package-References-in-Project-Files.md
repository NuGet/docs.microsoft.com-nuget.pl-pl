---
title: Formatu NuGet PackageReference (odwołania do pakietu w plikach projektu)
description: Szczegółowe informacje na temat formatu NuGet PackageReference w plikach projektu jako obsługiwane przez NuGet 4.0 + i programu VS 2017 i platformy .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 9ae8e8dc4e7e901acacffed8b7dfb4162c5ad2b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551393"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="90218-103">Odwołania do pakietu (PackageReference) w plikach projektu</span><span class="sxs-lookup"><span data-stu-id="90218-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="90218-104">Pakiet odwołań, za pomocą `PackageReference` węzła, zarządzanie zależnościami NuGet bezpośrednio z poziomu plików projektu (w przeciwieństwie do oddzielnego `packages.config` pliku).</span><span class="sxs-lookup"><span data-stu-id="90218-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="90218-105">Za pomocą funkcji PackageReference, ponieważ jest to, nie ma wpływu na inne aspekty pakietu nuget; na przykład ustawienia w `NuGet.Config` plików (w tym źródeł pakietów) nadal są stosowane zgodnie z objaśnieniem w [Konfigurowanie zachowania pakietu NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="90218-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="90218-106">Za pomocą funkcji PackageReference umożliwia także warunki MSBuild do wyboru na platformę docelową, konfiguracji, platforma lub inne grupy będzie odwoływał się pakiet.</span><span class="sxs-lookup"><span data-stu-id="90218-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="90218-107">Umożliwia ona również szczegółową kontrolę nad tym zależności i zawartości przepływu.</span><span class="sxs-lookup"><span data-stu-id="90218-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="90218-108">(Aby uzyskać więcej informacji, zobacz [NuGet pakowanie i przywrócić jako elementów docelowych MSBuild](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="90218-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="90218-109">Domyślnie PackageReference jest używany dla projektów .NET Core, .NET Standard projektów i projektów platformy UWP przeznaczonych dla systemu Windows 10 kompilacja 15063 (Aktualizacja dla twórców) lub nowszy, z wyjątkiem projektów platformy UWP w języku C++.</span><span class="sxs-lookup"><span data-stu-id="90218-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="90218-110">Projekty programu .NET framework pełnej obsługi PackageReference, ale obecnie domyślnie `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="90218-110">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="90218-111">Aby korzystać z funkcji PackageReference, migracja zależności z `packages.config` do pliku projektu, a następnie usuń packages.config.</span><span class="sxs-lookup"><span data-stu-id="90218-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="90218-112">Dodawanie odwołanie PackageReference</span><span class="sxs-lookup"><span data-stu-id="90218-112">Adding a PackageReference</span></span>

<span data-ttu-id="90218-113">Dodawanie zależności w pliku projektu przy użyciu następującej składni:</span><span class="sxs-lookup"><span data-stu-id="90218-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="90218-114">Kontrolowanie wersja zależności</span><span class="sxs-lookup"><span data-stu-id="90218-114">Controlling dependency version</span></span>

<span data-ttu-id="90218-115">Konwencja określania wersję pakietu jest taka sama jak, korzystając z `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="90218-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="90218-116">W powyższym przykładzie 3.6.0 oznacza dowolną wersję, którą jest > = 3.6.0 z preferencją dla Najniższa wersja zgodnie z opisem na [przechowywanie wersji pakietów](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="90218-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="90218-117">Za pomocą funkcji PackageReference dla projektu z nie składnika PackageReferences</span><span class="sxs-lookup"><span data-stu-id="90218-117">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="90218-118">Zaawansowane: Jeśli ma żadnych pakietów zainstalowany w projekcie (nie składnika PackageReferences w pliku projektu) i Brak pliku packages.config, ale Project, które ma zostać przywrócone jako styl PackageReference, możesz ustawić właściwość projektu RestoreProjectStyle do odwołania PackageReference w plik projektu.</span><span class="sxs-lookup"><span data-stu-id="90218-118">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="90218-119">Może to być przydatne, jeśli odwołujesz się projekty, które są PackageReference różne (istniejącego pliku csproj lub projektów w stylu zestawu SDK).</span><span class="sxs-lookup"><span data-stu-id="90218-119">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="90218-120">Spowoduje to włączenie pakiety, które projekty dotyczą przywoływanie "przechodnio" w projekcie.</span><span class="sxs-lookup"><span data-stu-id="90218-120">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="90218-121">Wersje</span><span class="sxs-lookup"><span data-stu-id="90218-121">Floating Versions</span></span>

<span data-ttu-id="90218-122">[Wersje](../consume-packages/dependency-resolution.md#floating-versions) są obsługiwane w przypadku `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="90218-122">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="90218-123">Kontrolowanie zależności zasobów</span><span class="sxs-lookup"><span data-stu-id="90218-123">Controlling dependency assets</span></span>

<span data-ttu-id="90218-124">Być może używasz zależność wyłącznie jako kontroler rozwoju i nie chcieć ujawnić, do projektów, które będą korzystać z pakietu.</span><span class="sxs-lookup"><span data-stu-id="90218-124">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="90218-125">W tym scenariuszu można użyć `PrivateAssets` metadanych w celu kontrolowania tego zachowania.</span><span class="sxs-lookup"><span data-stu-id="90218-125">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="90218-126">Następujące tagi metadanych kontrolować zasoby zależności:</span><span class="sxs-lookup"><span data-stu-id="90218-126">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="90218-127">Tag</span><span class="sxs-lookup"><span data-stu-id="90218-127">Tag</span></span> | <span data-ttu-id="90218-128">Opis</span><span class="sxs-lookup"><span data-stu-id="90218-128">Description</span></span> | <span data-ttu-id="90218-129">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="90218-129">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="90218-130">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="90218-130">IncludeAssets</span></span> | <span data-ttu-id="90218-131">Te zasoby będą używane.</span><span class="sxs-lookup"><span data-stu-id="90218-131">These assets will be consumed</span></span> | <span data-ttu-id="90218-132">wszystkie</span><span class="sxs-lookup"><span data-stu-id="90218-132">all</span></span> |
| <span data-ttu-id="90218-133">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="90218-133">ExcludeAssets</span></span> | <span data-ttu-id="90218-134">Te zasoby nie będą używane.</span><span class="sxs-lookup"><span data-stu-id="90218-134">These assets will not be consumed</span></span> | <span data-ttu-id="90218-135">brak</span><span class="sxs-lookup"><span data-stu-id="90218-135">none</span></span> |
| <span data-ttu-id="90218-136">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="90218-136">PrivateAssets</span></span> | <span data-ttu-id="90218-137">Te zasoby będą używane, ale nie będzie przepływać do projektu nadrzędnego</span><span class="sxs-lookup"><span data-stu-id="90218-137">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="90218-138">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="90218-138">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="90218-139">Dopuszczalnych wartości dla tych tagów, są w następujący sposób, przy użyciu wielu wartości, rozdzielając je średnikiem z wyjątkiem za pomocą `all` i `none` której musi znajdować się w sobie:</span><span class="sxs-lookup"><span data-stu-id="90218-139">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="90218-140">Wartość</span><span class="sxs-lookup"><span data-stu-id="90218-140">Value</span></span> | <span data-ttu-id="90218-141">Opis</span><span class="sxs-lookup"><span data-stu-id="90218-141">Description</span></span> |
| --- | ---
| <span data-ttu-id="90218-142">Kompilacji</span><span class="sxs-lookup"><span data-stu-id="90218-142">compile</span></span> | <span data-ttu-id="90218-143">Zawartość `lib` folder i formanty czy projektu można kompilować dla zestawów w folderze</span><span class="sxs-lookup"><span data-stu-id="90218-143">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="90218-144">środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="90218-144">runtime</span></span> | <span data-ttu-id="90218-145">Zawartość `lib` i `runtimes` folder i formanty czy te zestawy będzie kopiowana do kompilacji katalogu wyjściowego</span><span class="sxs-lookup"><span data-stu-id="90218-145">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="90218-146">Pliki</span><span class="sxs-lookup"><span data-stu-id="90218-146">contentFiles</span></span> | <span data-ttu-id="90218-147">Zawartość `contentfiles` folderu</span><span class="sxs-lookup"><span data-stu-id="90218-147">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="90218-148">kompilacja</span><span class="sxs-lookup"><span data-stu-id="90218-148">build</span></span> | <span data-ttu-id="90218-149">Właściwości i elementów docelowych w `build` folderu</span><span class="sxs-lookup"><span data-stu-id="90218-149">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="90218-150">Analizatory</span><span class="sxs-lookup"><span data-stu-id="90218-150">analyzers</span></span> | <span data-ttu-id="90218-151">Analizatory platformy .NET</span><span class="sxs-lookup"><span data-stu-id="90218-151">.NET analyzers</span></span> |
| <span data-ttu-id="90218-152">natywne</span><span class="sxs-lookup"><span data-stu-id="90218-152">native</span></span> | <span data-ttu-id="90218-153">Zawartość `native` folderu</span><span class="sxs-lookup"><span data-stu-id="90218-153">Contents of the `native` folder</span></span> |
| <span data-ttu-id="90218-154">brak</span><span class="sxs-lookup"><span data-stu-id="90218-154">none</span></span> | <span data-ttu-id="90218-155">Żadne z powyższych są używane.</span><span class="sxs-lookup"><span data-stu-id="90218-155">None of the above are used.</span></span> |
| <span data-ttu-id="90218-156">wszystkie</span><span class="sxs-lookup"><span data-stu-id="90218-156">all</span></span> | <span data-ttu-id="90218-157">Wszystkie powyższe (z wyjątkiem `none`)</span><span class="sxs-lookup"><span data-stu-id="90218-157">All of the above (except `none`)</span></span> |

<span data-ttu-id="90218-158">W poniższym przykładzie wszystkim, z wyjątkiem plików zawartości z pakietu może być używane przez projekt i wszystkim, z wyjątkiem analizatory i pliki zawartości będą przepływać do projektu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="90218-158">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="90218-159">Należy pamiętać, że ponieważ `build` nie znajduje się za pomocą `PrivateAssets`, cele i właściwości *będzie* przepływ do nadrzędnego projektu.</span><span class="sxs-lookup"><span data-stu-id="90218-159">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="90218-160">Należy wziąć pod uwagę, na przykład, że odwołanie powyżej jest używany w projekcie, który tworzy pakiet NuGet o nazwie AppLogger.</span><span class="sxs-lookup"><span data-stu-id="90218-160">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="90218-161">AppLogger mogą wykorzystywać obiektów docelowych i właściwości z `Contoso.Utility.UsefulStuff`, tak jak w projektach korzystających z AppLogger.</span><span class="sxs-lookup"><span data-stu-id="90218-161">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="90218-162">Dodawanie warunku PackageReference</span><span class="sxs-lookup"><span data-stu-id="90218-162">Adding a PackageReference condition</span></span>

<span data-ttu-id="90218-163">Możesz użyć warunek do kontroli, czy pakiet jest uwzględnione, w przypadku, gdy warunki, można użyć dowolnej zmiennej programu MSBuild lub zmienną zdefiniowaną w pliku elementów docelowych lub właściwości.</span><span class="sxs-lookup"><span data-stu-id="90218-163">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="90218-164">Jednak w obecnie tylko `TargetFramework` zmienna jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="90218-164">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="90218-165">Załóżmy na przykład, gdy elementem docelowym `netstandard1.4` także `net452` , ale ma zależność, która ma zastosowanie tylko do `net452`.</span><span class="sxs-lookup"><span data-stu-id="90218-165">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="90218-166">W takim przypadku nie ma `netstandard1.4` projektu, który zużywa pakietu do dodania tej zależności niepotrzebne.</span><span class="sxs-lookup"><span data-stu-id="90218-166">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="90218-167">Aby temu zapobiec, określamy warunek na `PackageReference` w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="90218-167">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="90218-168">Pakiet, który został skompilowany przy użyciu tego projektu pokaże, że pakiet Newtonsoft.Json jest uwzględniany jako zależności tylko w przypadku `net452` docelowej:</span><span class="sxs-lookup"><span data-stu-id="90218-168">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Wynik zastosowania warunku na PackageReference za pomocą programu VS 2017](media/PackageReference-Condition.png)

<span data-ttu-id="90218-170">Warunki mogą być również stosowane przy `ItemGroup` poziomu i będą stosowane do wszystkich obiektów podrzędnych `PackageReference` elementy:</span><span class="sxs-lookup"><span data-stu-id="90218-170">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
