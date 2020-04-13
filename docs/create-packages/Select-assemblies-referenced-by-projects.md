---
title: Wybierz zestawy, do których odwołują się projekty
description: Udostępnij kompilatorowi podzbiór zestawów w pakiecie, podczas gdy wszystkie zestawy są dostępne w czasie wykonywania.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b32075c3f2c06c15c07d36602bdabdaee8b9405a
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427660"
---
# <a name="select-assemblies-referenced-by-projects"></a>Wybierz zestawy, do których odwołują się projekty

Jawne odwołania do zestawu umożliwia podzbiór zestawów do użycia dla IntelliSense i kompilacji, podczas gdy wszystkie zestawy są dostępne w czasie wykonywania. `PackageReference`i `packages.config` działać inaczej, a w rezultacie autorzy pakietu muszą zadbać o stworzenie pakietu, aby był zgodny z obu typów projektu.

> [!Note]
> Jawne odwołania do zestawu są powiązane z zestawami .NET. Nie jest to metoda dystrybucji natywnych zestawów, które są P/Invoked przez zestaw zarządzany.

## <a name="packagereference-support"></a>`PackageReference`Wsparcie

Gdy projekt używa pakietu `PackageReference` z i pakiet `ref\<tfm>\` zawiera katalog, NuGet klasyfikuje te zestawy jako zasoby `lib\<tfm>\` w czasie kompilacji, podczas gdy zestawy są klasyfikowane jako zasoby środowiska wykonawczego. Zestawy w `ref\<tfm>\` nie są używane w czasie wykonywania. Oznacza to, że jest `ref\<tfm>\` to konieczne dla każdego `lib\<tfm>\` zestawu w `runtime\` mieć pasujące zestawu w jednym lub odpowiedniego katalogu, w przeciwnym razie błędy środowiska uruchomieniowego prawdopodobnie wystąpią. Ponieważ zestawy `ref\<tfm>\` w nie są używane w czasie wykonywania, mogą być [tylko do metadanych zestawów](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) w celu zmniejszenia rozmiaru pakietu.

> [!Important]
> Jeśli pakiet `<references>` zawiera nuspec element `packages.config`(używany przez , patrz poniżej) i nie zawiera zestawów w `ref\<tfm>\` `<references>` , NuGet anonsuje zestawy wymienione w nuspec element zarówno skompilować i zasobów środowiska wykonawczego. Oznacza to, że będą wyjątki środowiska uruchomieniowego, gdy zestawy, `lib\<tfm>\` do których istnieje odwołanie, muszą załadować inny zestaw w katalogu.

> [!Note]
> Jeśli pakiet zawiera `runtime\` katalog, NuGet nie może używać `lib\` zasobów w katalogu.

## <a name="packagesconfig-support"></a>`packages.config`Wsparcie

Projekty `packages.config` używane do zarządzania pakietami NuGet zwykle dodają odwołania do wszystkich zestawów w `lib\<tfm>\` katalogu. Katalog `ref\` został dodany do `PackageReference` obsługi i dlatego nie `packages.config`jest brany pod uwagę podczas korzystania . Aby jawnie ustawić, do których zestawów są przywoływane dla projektów przy użyciu, `packages.config`pakiet musi użyć [ `<references>` elementu w pliku nuspec](../reference/nuspec.md#explicit-assembly-references). Przykład:

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> `packages.config`projekt użyć procesu o nazwie [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) `bin\<configuration>\` do kopiowania zestawów do katalogu wyjściowego. Zestaw projektu jest kopiowany, a następnie system kompilacji patrzy na manifest zestawu dla zestawów, do których istnieje odwołanie, a następnie kopiuje te zestawy i powtarza się rekurencyjnie dla wszystkich zestawów. Oznacza to, że jeśli którykolwiek `lib\<tfm>\` z zestawów w katalogu nie są wymienione w manifeście innego zestawu `Assembly.Load`jako zależność (jeśli zestaw jest ładowany w czasie wykonywania `bin\<configuration>\` przy użyciu MEF `bin\<tfm>\`lub innej struktury iniekcji zależności), to nie może być kopiowany do katalogu wyjściowego projektu, mimo że jest w .

## <a name="example"></a>Przykład

Mój pakiet będzie zawierać `MyLib.dll`trzy `MyHelpers.dll` `MyUtilities.dll`zestawy i , które są przeznaczone dla .NET Framework 4.7.2. `MyUtilities.dll`zawiera klasy przeznaczone do użycia tylko przez pozostałe dwa zestawy, więc nie chcę, aby te klasy dostępne w IntelliSense lub w czasie kompilacji do projektów przy użyciu mojego pakietu. Mój `nuspec` plik musi zawierać następujące elementy XML:

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

a pliki w pakiecie będą:

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
