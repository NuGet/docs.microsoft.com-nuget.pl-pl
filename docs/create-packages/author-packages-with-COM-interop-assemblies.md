---
title: Tworzenie pakietów przy użyciu zestawów międzyoperacyjnych COM
description: W tym artykule opisano sposób tworzenia pakietów, które zawierają zestawy międzyoperacyjne COM
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: d0e368f43171ce71abc60b3e09d08b010d2d8880
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843531"
---
## <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a><span data-ttu-id="b586a-103">Tworzenie pakietów NuGet, które zawierają zestawy międzyoperacyjne COM</span><span class="sxs-lookup"><span data-stu-id="b586a-103">Create NuGet packages that contain COM interop assemblies</span></span>

<span data-ttu-id="b586a-104">Pakiety, które zawierają zestawy międzyoperacyjne COM musi zawierać odpowiednią [plik docelowy](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) tak, aby poprawny `EmbedInteropTypes` metadane dodawane do projektów przy użyciu formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="b586a-104">Packages that contain COM interop assemblies must include an appropriate [targets file](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="b586a-105">Domyślnie `EmbedInteropTypes` metadanych ma zawsze wartość false dla wszystkich zestawów stosowania PackageReference więc plik elementów docelowych dodaje te metadane jawnie.</span><span class="sxs-lookup"><span data-stu-id="b586a-105">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="b586a-106">Aby uniknąć konfliktów, nazwa docelowego powinna być unikatowa. w idealnym przypadku należy użyć zestawienia nazwę pakietu i zestaw jest osadzony, zastępując `{InteropAssemblyName}` w poniższym przykładzie przy użyciu tej wartości.</span><span class="sxs-lookup"><span data-stu-id="b586a-106">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="b586a-107">(Zobacz też [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) np.)</span><span class="sxs-lookup"><span data-stu-id="b586a-107">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="b586a-108">Należy pamiętać, że podczas korzystania `packages.config` zarządzania formatu, dodawanie odwołań do zestawów z pakietów powoduje, że NuGet i programu Visual Studio sprawdzić, czy są zestawy międzyoperacyjne COM i ustawić `EmbedInteropTypes` na wartość true w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="b586a-108">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="b586a-109">W tym przypadku cele są zastąpione.</span><span class="sxs-lookup"><span data-stu-id="b586a-109">In this case the targets are overriden.</span></span>

<span data-ttu-id="b586a-110">Ponadto domyślnie [zasoby kompilacji nie została przechodnio przepływu](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="b586a-110">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="b586a-111">Pakiety utworzone zgodnie z opisem w tym miejscu pracy inaczej, gdy są one pobierane jako zależność przechodnich z odwołaniem projektu do projektu.</span><span class="sxs-lookup"><span data-stu-id="b586a-111">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="b586a-112">Konsument pakietu można zezwolić na przepływ, modyfikując wartość domyślną PrivateAssets wykluczającą kompilacji.</span><span class="sxs-lookup"><span data-stu-id="b586a-112">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>