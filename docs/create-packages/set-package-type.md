---
title: Ustawianie typu pakietu NuGet
description: Opisuje typy pakietów wskazujące zamierzone użycie pakietu.
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: fa369e8327330e13f5adda39a75008e42ac99896
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067284"
---
# <a name="set-a-nuget-package-type"></a>Ustawianie typu pakietu NuGet

Pakiety można oznaczać za pomocą jeszcze jednego *typu pakietu,* aby wskazać jego przeznaczenie.

## <a name="known-package-types"></a>Znane typy pakietów

- `Dependency` pakiety typu dodają zasoby kompilacji lub czasu uruchamiania do bibliotek i aplikacji i mogą być instalowane w dowolnym typie projektu (przy założeniu, że są zgodne).

- `DotnetTool`Pakiety typu to narzędzia .NET, które można zainstalować za pomocą interfejsu wiersza [polecenia dotnet.](/dotnet/articles/core/tools/index)

- `Template` Pakiety typu zawierają [szablony niestandardowe,](/dotnet/core/tools/custom-templates) których można używać do tworzenia plików lub projektów, takich jak biblioteka aplikacji, usługi, narzędzia lub klas.

Pakiety, które nie są oznaczone typem , łącznie ze wszystkimi pakietami utworzonymi za pomocą wcześniejszych wersji pakietu NuGet, są domyślnie `Dependency` typu.

> [!NOTE]
> Obsługa typów pakietów została dodana w pakiecie NuGet 3.5.
> Jeśli nie potrzebujesz niestandardowego typu pakietu, najlepiej  nie jawnie ustawić typu pakietu.
> Program NuGet domyślnie określa `Dependency` typ, gdy nie określono typu.

## <a name="custom-package-types"></a>Niestandardowe typy pakietów

Możesz oznaczyć pakiet za pomocą co najmniej jednego niestandardowego typu pakietu, jeśli jego użycie nie pasuje do [znanych typów pakietów](#known-package-types).

Załóżmy na przykład, że klienci `Contoso` aplikacji mogą instalować rozszerzenia. Aplikacja może wymagać od autorów rozszerzeń użycia niestandardowego typu pakietu w celu zidentyfikowania ich pakietów jako odpowiednich rozszerzeń, które są zgodne `ContosoExtension` z wymaganymi konwencjami.

> [!WARNING]
> Pakiet z niestandardowym typem pakietu nie może zostać zainstalowany przez Visual Studio lub nuget.exe. Aby uzyskać więcej informacji, zobacz [NuGet/Home#10468.](https://github.com/NuGet/Home/issues/10468)

# <a name="using-dotnet-cli"></a>[Korzystanie z interfejsu wiersza polecenia dotnet](#tab/dotnet)

Typy pakietów można ustawić w pliku projektu ( `.csproj` ):

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

Pakiety o wielu zamierzonych zastosowaniach można oznaczać wieloma typami pakietów za pomocą `;` ogranicznika:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

Typy pakietów mogą być wersjonarowane przy użyciu `,` ogranicznika między typem pakietu a jego [`Version`](/dotnet/api/system.version) ciągiem:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[Korzystanie z nuget.exe](#tab/nugetexe)

Typy pakietów są ustawiane `.nuspec` w pliku w `packageTypes\packageType` węźle w `<metadata>` ramach elementu :

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="ContosoExtension" />
        </packageTypes>
    </metadata>
</package>
```

Pakiety o wielu zamierzonych zastosowaniach mogą być oznaczone wieloma typami pakietów:

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

Typy pakietów mogą być wersjonarowane przy użyciu [`Version`](/dotnet/api/system.version) ciągu:

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" version="1.0.0.0" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

---

Format ciągu typu pakietu jest dokładnie taki sam jak identyfikator pakietu. Oznacza to, że typ pakietu jest ciągiem bez uwzględniania liter pasującymi do wyrażenia regularnego, który zawiera co najmniej jeden znak i co najwyżej `^\w+([_.-]\w+)*$` 100 znaków.

Jeśli zostanie podany, wersja typu pakietu będzie [`Version`](/dotnet/api/system.version) ciągiem. Wersja typu pakietu jest opcjonalna i domyślnie ma wartość `0.0` .
