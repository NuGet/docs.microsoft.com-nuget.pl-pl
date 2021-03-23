---
title: Tworzenie pakietów z zestawami międzyoperacyjnymi modelu COM
description: Opisuje sposób tworzenia pakietów zawierających zestawy międzyoperacyjności modelu COM
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b12672e81a974e113ffbda80560c9d3eede9c69d
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859125"
---
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a><span data-ttu-id="c4ad9-103">Utwórz pakiety NuGet zawierające zestawy międzyoperacyjności modelu COM</span><span class="sxs-lookup"><span data-stu-id="c4ad9-103">Create NuGet packages that contain COM interop assemblies</span></span>

<span data-ttu-id="c4ad9-104">Pakiety zawierające zestawy międzyoperacyjności modelu COM muszą zawierać odpowiedni [plik targets](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) , aby poprawne `EmbedInteropTypes` metadane były dodawane do projektów przy użyciu formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="c4ad9-104">Packages that contain COM interop assemblies must include an appropriate [targets file](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="c4ad9-105">Domyślnie `EmbedInteropTypes` metadane są zawsze fałszywe dla wszystkich zestawów, gdy jest używana PackageReference, więc plik targets dodaje te metadane jawnie.</span><span class="sxs-lookup"><span data-stu-id="c4ad9-105">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="c4ad9-106">Aby uniknąć konfliktów, nazwa elementu docelowego powinna być unikatowa. w idealnym przypadku użyj kombinacji nazwy pakietu i osadzonego zestawu, zastępując `{InteropAssemblyName}` Poniższy przykład wartością.</span><span class="sxs-lookup"><span data-stu-id="c4ad9-106">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="c4ad9-107">(Zobacz też [NuGet. Samples. Interop](https://github.com/NuGet/Samples/tree/main/NuGet.Samples.Interop) na przykład).</span><span class="sxs-lookup"><span data-stu-id="c4ad9-107">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/main/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="c4ad9-108">Należy pamiętać, że w przypadku korzystania z `packages.config` formatu zarządzania Dodawanie odwołań do zestawów z pakietów powoduje, że NuGet i Visual Studio sprawdzają zestawy międzyoperacyjności modelu COM i ustawiają `EmbedInteropTypes` wartość true w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="c4ad9-108">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="c4ad9-109">W takim przypadku cele są zastępowane.</span><span class="sxs-lookup"><span data-stu-id="c4ad9-109">In this case, the targets are overridden.</span></span>

<span data-ttu-id="c4ad9-110">Ponadto domyślnie [zasoby kompilacji nie przepływy przechodnie](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="c4ad9-110">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="c4ad9-111">Pakiety utworzone zgodnie z opisem w tym miejscu działają inaczej, gdy są ściągane jako zależność przechodnia od projektu do odwołania do projektu.</span><span class="sxs-lookup"><span data-stu-id="c4ad9-111">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="c4ad9-112">Odbiorca pakietu może zezwolić im na przepływ, modyfikując wartość domyślną PrivateAssets, tak aby nie obejmowała kompilacji.</span><span class="sxs-lookup"><span data-stu-id="c4ad9-112">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>