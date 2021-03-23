---
title: Wybierz zestawy, do których odwołują się projekty
description: Utwórz podzestaw zestawów w pakiecie dostępnym dla kompilatora, podczas gdy wszystkie zestawy są dostępne w czasie wykonywania.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b2202946d0060e09828250d240f931044d1bf485
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859034"
---
# <a name="select-assemblies-referenced-by-projects"></a>Wybierz zestawy, do których odwołują się projekty

Jawne odwołania do zestawów umożliwiają podzbiór zestawów, które mają być używane do IntelliSense i kompilowania, podczas gdy wszystkie zestawy są dostępne w czasie wykonywania. `PackageReference` i `packages.config` działają inaczej i w związku z tym autorzy pakietu muszą zachować ostrożność, aby utworzyć pakiet zgodny z typem obu projektów.

> [!Note]
> Jawne odwołania do zestawów są powiązane z zestawami .NET. Nie jest to metoda dystrybucji natywnych zestawów, które są wywoływane przez zestaw zarządzany.

## <a name="packagereference-support"></a>`PackageReference` pomocy

Gdy projekt używa pakietu programu `PackageReference` i zawiera `ref\<tfm>\` katalog, pakiet NuGet klasyfikuje je jako zasoby w czasie kompilacji, a `lib\<tfm>\` zestawy są klasyfikowane jako zasoby środowiska uruchomieniowego. Zestawy w programie `ref\<tfm>\` nie są używane w czasie wykonywania. Oznacza to, że jest to konieczne dla każdego zestawu w programie w `ref\<tfm>\` celu posiadania zestawu zgodnego z `lib\<tfm>\` lub w odpowiednim `runtime\` katalogu, w przeciwnym razie błędy środowiska uruchomieniowego mogą wystąpić. Ponieważ zestawy w programie `ref\<tfm>\` nie są używane w czasie wykonywania, mogą one być [zestawami tylko do metadanych](https://github.com/dotnet/roslyn/blob/main/docs/features/refout.md) , aby zmniejszyć rozmiar pakietu.

> [!Important]
> Jeśli pakiet zawiera `<references>` element nuspec (używany przez `packages.config` , zobacz poniżej) i nie zawiera zestawów w programie, program `ref\<tfm>\` NuGet anonsuje zestawy wymienione w `<references>` elemencie nuspec jako zasoby kompilacji i środowiska uruchomieniowego. Oznacza to, że jeśli zestawy, do których istnieją odwołania, muszą załadować każdy inny zestaw w katalogu, zostaną wyjątków w czasie wykonywania `lib\<tfm>\` .

> [!Note]
> Jeśli pakiet zawiera `runtime\` katalog, NuGet nie może używać zasobów w `lib\` katalogu.

## <a name="packagesconfig-support"></a>`packages.config` pomocy

Projekty używające `packages.config` do zarządzania pakietami NuGet zwykle dodają odwołania do wszystkich zestawów w `lib\<tfm>\` katalogu. `ref\`Katalog został dodany do obsługi `PackageReference` i w związku z tym nie jest brany pod uwagę podczas korzystania z programu `packages.config` . Aby jawnie ustawić zestawy, do których odwołują się projekty `packages.config` , pakiet musi używać [ `<references>` elementu w pliku nuspec](../reference/nuspec.md#explicit-assembly-references). Na przykład:

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> `packages.config` projekt używa procesu o nazwie [ResolveAssemblyReference —](https://github.com/Microsoft/msbuild/blob/main/documentation/wiki/ResolveAssemblyReference.md) do kopiowania zestawów do `bin\<configuration>\` katalogu wyjściowego. Zestaw projektu jest kopiowany, a następnie system kompilacji sprawdza manifest zestawu dla przywoływanych zestawów, a następnie kopiuje te zestawy i cyklicznie powtarza dla wszystkich zestawów. Oznacza to, że jeśli którykolwiek z zestawów w `lib\<tfm>\` katalogu nie jest wymieniony w żadnym innym manifeście zestawu jako zależność (Jeśli zestaw jest ładowany w czasie wykonywania za pomocą `Assembly.Load` , MEF lub inną platformą wstrzykiwania zależności), wówczas może nie być kopiowany do katalogu wyjściowego projektu pomimo tego, że `bin\<configuration>\` jest w `bin\<tfm>\` .

## <a name="example"></a>Przykład

Mój pakiet będzie zawierać trzy zestawy, `MyLib.dll` `MyHelpers.dll` i `MyUtilities.dll` , które są ukierunkowane na .NET Framework 4.7.2. `MyUtilities.dll` zawiera klasy przeznaczone do użycia tylko przez pozostałe dwa zestawy, więc nie chcę, aby te klasy były dostępne w technologii IntelliSense ani w czasie kompilacji do projektów przy użyciu mojego pakietu. Mój `nuspec` plik musi zawierać następujące elementy XML:

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

pliki w pakiecie będą:

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
