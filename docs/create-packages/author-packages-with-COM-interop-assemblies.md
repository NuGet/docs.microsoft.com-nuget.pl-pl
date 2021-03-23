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
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a>Utwórz pakiety NuGet zawierające zestawy międzyoperacyjności modelu COM

Pakiety zawierające zestawy międzyoperacyjności modelu COM muszą zawierać odpowiedni [plik targets](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) , aby poprawne `EmbedInteropTypes` metadane były dodawane do projektów przy użyciu formatu PackageReference. Domyślnie `EmbedInteropTypes` metadane są zawsze fałszywe dla wszystkich zestawów, gdy jest używana PackageReference, więc plik targets dodaje te metadane jawnie. Aby uniknąć konfliktów, nazwa elementu docelowego powinna być unikatowa. w idealnym przypadku użyj kombinacji nazwy pakietu i osadzonego zestawu, zastępując `{InteropAssemblyName}` Poniższy przykład wartością. (Zobacz też [NuGet. Samples. Interop](https://github.com/NuGet/Samples/tree/main/NuGet.Samples.Interop) na przykład).

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

Należy pamiętać, że w przypadku korzystania z `packages.config` formatu zarządzania Dodawanie odwołań do zestawów z pakietów powoduje, że NuGet i Visual Studio sprawdzają zestawy międzyoperacyjności modelu COM i ustawiają `EmbedInteropTypes` wartość true w pliku projektu. W takim przypadku cele są zastępowane.

Ponadto domyślnie [zasoby kompilacji nie przepływy przechodnie](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets). Pakiety utworzone zgodnie z opisem w tym miejscu działają inaczej, gdy są ściągane jako zależność przechodnia od projektu do odwołania do projektu. Odbiorca pakietu może zezwolić im na przepływ, modyfikując wartość domyślną PrivateAssets, tak aby nie obejmowała kompilacji.

<a name="creating-the-package"></a>