---
title: Tworzenie pakietów z zestawami współdziałań COM
description: W tym artykule opisano sposób tworzenia pakietów zawierających zestawy współdziałacze COM
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: de164b136a1636b89f674b8626613094fc53e04c
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "75385575"
---
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a><span data-ttu-id="b0a1d-103">Tworzenie pakietów NuGet zawierających zestawy współdziałacze COM</span><span class="sxs-lookup"><span data-stu-id="b0a1d-103">Create NuGet packages that contain COM interop assemblies</span></span>

<span data-ttu-id="b0a1d-104">Pakiety, które zawierają zestawy współdziałanie COM musi `EmbedInteropTypes` zawierać odpowiedni plik obiektów [docelowych,](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) tak aby poprawne metadane są dodawane do projektów przy użyciu formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="b0a1d-104">Packages that contain COM interop assemblies must include an appropriate [targets file](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="b0a1d-105">Domyślnie `EmbedInteropTypes` metadane są zawsze false dla wszystkich zestawów, gdy PackageReference jest używany, więc plik docelowy dodaje te metadane jawnie.</span><span class="sxs-lookup"><span data-stu-id="b0a1d-105">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="b0a1d-106">Aby uniknąć konfliktów, nazwa obiektu docelowego powinna być unikatowa; najlepiej użyć kombinacji nazwy pakietu i zestawu osadzonego, zastępując `{InteropAssemblyName}` w poniższym przykładzie tą wartością.</span><span class="sxs-lookup"><span data-stu-id="b0a1d-106">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="b0a1d-107">(Zobacz też [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) dla przykładu).</span><span class="sxs-lookup"><span data-stu-id="b0a1d-107">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="b0a1d-108">Należy zauważyć, `packages.config` że podczas korzystania z formatu zarządzania, dodawanie odwołań do zestawów z pakietów `EmbedInteropTypes` powoduje NuGet i Visual Studio, aby sprawdzić zestawy współdziałania COM i ustawić true w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="b0a1d-108">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="b0a1d-109">W takim przypadku cele są zastępowane.</span><span class="sxs-lookup"><span data-stu-id="b0a1d-109">In this case, the targets are overridden.</span></span>

<span data-ttu-id="b0a1d-110">Ponadto domyślnie [zasoby kompilacji nie przepływają przechodnie](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="b0a1d-110">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="b0a1d-111">Pakiety, które zostały opisane w tym miejscu, działają inaczej, gdy są pobierane jako przechodnie zależności od projektu do odwołania do projektu.</span><span class="sxs-lookup"><span data-stu-id="b0a1d-111">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="b0a1d-112">Konsument pakietu można zezwolić na ich przepływ, modyfikując PrivateAssets wartość domyślna, aby nie dołączyć kompilacji.</span><span class="sxs-lookup"><span data-stu-id="b0a1d-112">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>