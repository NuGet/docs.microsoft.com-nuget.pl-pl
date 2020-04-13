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
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a>Tworzenie pakietów NuGet zawierających zestawy współdziałacze COM

Pakiety, które zawierają zestawy współdziałanie COM musi `EmbedInteropTypes` zawierać odpowiedni plik obiektów [docelowych,](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) tak aby poprawne metadane są dodawane do projektów przy użyciu formatu PackageReference. Domyślnie `EmbedInteropTypes` metadane są zawsze false dla wszystkich zestawów, gdy PackageReference jest używany, więc plik docelowy dodaje te metadane jawnie. Aby uniknąć konfliktów, nazwa obiektu docelowego powinna być unikatowa; najlepiej użyć kombinacji nazwy pakietu i zestawu osadzonego, zastępując `{InteropAssemblyName}` w poniższym przykładzie tą wartością. (Zobacz też [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) dla przykładu).

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

Należy zauważyć, `packages.config` że podczas korzystania z formatu zarządzania, dodawanie odwołań do zestawów z pakietów `EmbedInteropTypes` powoduje NuGet i Visual Studio, aby sprawdzić zestawy współdziałania COM i ustawić true w pliku projektu. W takim przypadku cele są zastępowane.

Ponadto domyślnie [zasoby kompilacji nie przepływają przechodnie](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets). Pakiety, które zostały opisane w tym miejscu, działają inaczej, gdy są pobierane jako przechodnie zależności od projektu do odwołania do projektu. Konsument pakietu można zezwolić na ich przepływ, modyfikując PrivateAssets wartość domyślna, aby nie dołączyć kompilacji.

<a name="creating-the-package"></a>