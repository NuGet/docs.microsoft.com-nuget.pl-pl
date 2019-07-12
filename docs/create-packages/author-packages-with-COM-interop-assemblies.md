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
## <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a>Tworzenie pakietów NuGet, które zawierają zestawy międzyoperacyjne COM

Pakiety, które zawierają zestawy międzyoperacyjne COM musi zawierać odpowiednią [plik docelowy](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) tak, aby poprawny `EmbedInteropTypes` metadane dodawane do projektów przy użyciu formatu PackageReference. Domyślnie `EmbedInteropTypes` metadanych ma zawsze wartość false dla wszystkich zestawów stosowania PackageReference więc plik elementów docelowych dodaje te metadane jawnie. Aby uniknąć konfliktów, nazwa docelowego powinna być unikatowa. w idealnym przypadku należy użyć zestawienia nazwę pakietu i zestaw jest osadzony, zastępując `{InteropAssemblyName}` w poniższym przykładzie przy użyciu tej wartości. (Zobacz też [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) np.)

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

Należy pamiętać, że podczas korzystania `packages.config` zarządzania formatu, dodawanie odwołań do zestawów z pakietów powoduje, że NuGet i programu Visual Studio sprawdzić, czy są zestawy międzyoperacyjne COM i ustawić `EmbedInteropTypes` na wartość true w pliku projektu. W tym przypadku cele są zastąpione.

Ponadto domyślnie [zasoby kompilacji nie została przechodnio przepływu](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets). Pakiety utworzone zgodnie z opisem w tym miejscu pracy inaczej, gdy są one pobierane jako zależność przechodnich z odwołaniem projektu do projektu. Konsument pakietu można zezwolić na przepływ, modyfikując wartość domyślną PrivateAssets wykluczającą kompilacji.

<a name="creating-the-package"></a>