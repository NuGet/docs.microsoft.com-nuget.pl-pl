---
title: Wybierz zestawy, które odwołują się projekty
description: Udostępnić podzbiór zestawów w pakiecie do kompilatora, gdy wszystkie zestawy są dostępne w czasie wykonywania.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b32075c3f2c06c15c07d36602bdabdaee8b9405a
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427660"
---
# <a name="select-assemblies-referenced-by-projects"></a>Wybierz zestawy, które odwołują się projekty

Odwołania do zestawu jawnych umożliwia podzbiór zestawów do użytku z technologii IntelliSense i kompilacja, gdy wszystkie zestawy są dostępne w czasie wykonywania. `PackageReference` i `packages.config` działają inaczej, a w rezultacie autorom pakietów należy zachować ostrożność do utworzenia pakietu, aby był zgodny z oboma typami projektów.

> [!Note]
> Odwołania do zestawu jawnych odnoszą się do zestawów platformy .NET. Nie jest metodą do rozpowszechniania zestawów natywnych, które są P/wywoływany przez zestaw zarządzany.

## <a name="packagereference-support"></a>`PackageReference` Obsługa

Jeśli projekt używa pakietu o `PackageReference` i pakiet zawiera `ref\<tfm>\` katalogu NuGet zostanie klasyfikowanie tych składa się jako zasoby kompilacji podczas `lib\<tfm>\` zestawy są klasyfikowane jako zasoby w czasie wykonywania. Zestawy w `ref\<tfm>\` nie są używane w czasie wykonywania. Oznacza to, niezbędne jest, aby każdy zespół w `ref\<tfm>\` mieć pasujący zestaw albo `lib\<tfm>\` nieznaczące `runtime\` katalogu, w przeciwnym razie środowisko uruchomieniowe prawdopodobnie wystąpią błędy. Ponieważ zestawy w `ref\<tfm>\` nie są używane w czasie wykonywania, może być [zestawów zawierających tylko metadane](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) zmniejszyć rozmiar pakietu.

> [!Important]
> Jeśli pakiet zawiera nuspec `<references>` — element (używane przez `packages.config`, patrz poniżej) i nie zawiera zestawy w `ref\<tfm>\`, NuGet będzie anonsować zestawów na liście nuspec `<references>` elementu jako zasoby kompilacji i środowiska uruchomieniowego. Oznacza to, będzie istnieć wyjątki środowiska uruchomieniowego podczas musisz załadować innego zestawu, w przywoływanych zestawach `lib\<tfm>\` katalogu.

> [!Note]
> Jeśli pakiet zawiera `runtime\` katalogu NuGet nie wolno korzystać z zasobów w `lib\` katalogu.

## <a name="packagesconfig-support"></a>`packages.config` Obsługa

Projekty, za pomocą `packages.config` do zarządzania NuGet pakietów zwykle dodać odwołania do wszystkich zestawów w `lib\<tfm>\` katalogu. `ref\` Katalog został dodany do obsługi `PackageReference` i dlatego nie jest traktowane jako przy użyciu `packages.config`. Aby jawnie ustawić zestawy, które są określone dla projektów przy użyciu `packages.config`, należy użyć pakietu [ `<references>` elementu w pliku nuspec](../reference/nuspec.md#explicit-assembly-references). Na przykład:

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> `packages.config` Użyj projektu w proces nazywany [resolveassemblyreference —](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) Aby skopiować zestawy `bin\<configuration>\` katalogu wyjściowego. Zestawu projektu jest kopiowana, a następnie system kompilacji analizuje manifestu zestawu dla zestawów odwołania, a następnie kopiuje te zestawy i rekursywnie powtarza się dla wszystkich zestawów. Oznacza to, że jeśli żadnego z zestawów w swojej `lib\<tfm>\` katalogu nie są wymienione w manifeście żadnych innych zestawów jako zależność (Jeśli zestaw jest ładowany w czasie wykonywania za pomocą `Assembly.Load`, MEF lub innej struktury iniekcji zależności), nie może mieć skopiowany do swojego projektu `bin\<configuration>\` katalog wyjściowy, mimo że znajduje się w `bin\<tfm>\`.

## <a name="example"></a>Przykład

Mój pakiet będzie zawierał trzy zestawy `MyLib.dll`, `MyHelpers.dll` i `MyUtilities.dll`, które są przeznaczone dla .NET Framework 4.7.2. `MyUtilities.dll` zawiera klasy przeznaczone do użycia tylko przez te dwa zestawy, dzięki czemu nie chcesz udostępnić te klasy w technologii IntelliSense lub w czasie kompilacji projektów za pomocą Mój pakiet. Moje `nuspec` plik musi zawierać następujące elementy XML:

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

pliki w pakiecie. zostanie ona:

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
