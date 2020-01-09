---
title: Tworzenie pakietów z zestawami międzyoperacyjnymi modelu COM
description: Opisuje sposób tworzenia pakietów zawierających zestawy międzyoperacyjności modelu COM
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: de164b136a1636b89f674b8626613094fc53e04c
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385575"
---
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a>Utwórz pakiety NuGet zawierające zestawy międzyoperacyjności modelu COM

Pakiety zawierające zestawy międzyoperacyjności modelu COM muszą zawierać odpowiedni [plik docelowy](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) , aby poprawne `EmbedInteropTypes` metadane były dodawane do projektów przy użyciu formatu PackageReference. Domyślnie metadane `EmbedInteropTypes` są zawsze fałszywe dla wszystkich zestawów, gdy jest używana PackageReference, więc plik targets dodaje te metadane jawnie. Aby uniknąć konfliktów, nazwa elementu docelowego powinna być unikatowa. najlepiej użyć kombinacji nazwy pakietu i osadzonego zestawu, zastępując `{InteropAssemblyName}` w poniższym przykładzie z tą wartością. (Zobacz też [NuGet. Samples. Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) na przykład).

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

Należy pamiętać, że w przypadku używania `packages.config`ego formatu zarządzania Dodawanie odwołań do zestawów z pakietów powoduje, że NuGet i Visual Studio sprawdzają zestawy międzyoperacyjności modelu COM i ustawiają dla `EmbedInteropTypes` wartość true w pliku projektu. W takim przypadku cele są zastępowane.

Ponadto domyślnie [zasoby kompilacji nie przepływy przechodnie](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets). Pakiety utworzone zgodnie z opisem w tym miejscu działają inaczej, gdy są ściągane jako zależność przechodnia od projektu do odwołania do projektu. Odbiorca pakietu może zezwolić im na przepływ, modyfikując wartość domyślną PrivateAssets, tak aby nie obejmowała kompilacji.

<a name="creating-the-package"></a>