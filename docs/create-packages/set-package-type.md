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
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="ef5c2-103">Ustawianie typu pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="ef5c2-103">Set a NuGet package type</span></span>

<span data-ttu-id="ef5c2-104">Pakiety można oznaczać za pomocą jeszcze jednego *typu pakietu,* aby wskazać jego przeznaczenie.</span><span class="sxs-lookup"><span data-stu-id="ef5c2-104">Packages can be marked with one more more *package types* to indicate its intended use.</span></span>

## <a name="known-package-types"></a><span data-ttu-id="ef5c2-105">Znane typy pakietów</span><span class="sxs-lookup"><span data-stu-id="ef5c2-105">Known package types</span></span>

- <span data-ttu-id="ef5c2-106">`Dependency` pakiety typu dodają zasoby kompilacji lub czasu uruchamiania do bibliotek i aplikacji i mogą być instalowane w dowolnym typie projektu (przy założeniu, że są zgodne).</span><span class="sxs-lookup"><span data-stu-id="ef5c2-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="ef5c2-107">`DotnetTool`Pakiety typu to narzędzia .NET, które można zainstalować za pomocą interfejsu wiersza [polecenia dotnet.](/dotnet/articles/core/tools/index)</span><span class="sxs-lookup"><span data-stu-id="ef5c2-107">`DotnetTool` type packages are .NET tools that can be installed by the [dotnet CLI](/dotnet/articles/core/tools/index).</span></span>

- <span data-ttu-id="ef5c2-108">`Template` Pakiety typu zawierają [szablony niestandardowe,](/dotnet/core/tools/custom-templates) których można używać do tworzenia plików lub projektów, takich jak biblioteka aplikacji, usługi, narzędzia lub klas.</span><span class="sxs-lookup"><span data-stu-id="ef5c2-108">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

<span data-ttu-id="ef5c2-109">Pakiety, które nie są oznaczone typem , łącznie ze wszystkimi pakietami utworzonymi za pomocą wcześniejszych wersji pakietu NuGet, są domyślnie `Dependency` typu.</span><span class="sxs-lookup"><span data-stu-id="ef5c2-109">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

> [!NOTE]
> <span data-ttu-id="ef5c2-110">Obsługa typów pakietów została dodana w pakiecie NuGet 3.5.</span><span class="sxs-lookup"><span data-stu-id="ef5c2-110">Support for package types was added in NuGet 3.5.</span></span>
> <span data-ttu-id="ef5c2-111">Jeśli nie potrzebujesz niestandardowego typu pakietu, najlepiej  nie jawnie ustawić typu pakietu.</span><span class="sxs-lookup"><span data-stu-id="ef5c2-111">If you don't need a custom package type, it's best to *not* explicitly set the package type.</span></span>
> <span data-ttu-id="ef5c2-112">Program NuGet domyślnie określa `Dependency` typ, gdy nie określono typu.</span><span class="sxs-lookup"><span data-stu-id="ef5c2-112">NuGet defaults to the `Dependency` type when no type is specified.</span></span>

## <a name="custom-package-types"></a><span data-ttu-id="ef5c2-113">Niestandardowe typy pakietów</span><span class="sxs-lookup"><span data-stu-id="ef5c2-113">Custom package types</span></span>

<span data-ttu-id="ef5c2-114">Możesz oznaczyć pakiet za pomocą co najmniej jednego niestandardowego typu pakietu, jeśli jego użycie nie pasuje do [znanych typów pakietów](#known-package-types).</span><span class="sxs-lookup"><span data-stu-id="ef5c2-114">You can mark your package with one or more custom package types if its use does not fit the [known package types](#known-package-types).</span></span>

<span data-ttu-id="ef5c2-115">Załóżmy na przykład, że klienci `Contoso` aplikacji mogą instalować rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="ef5c2-115">For example, imagine that customers of the `Contoso` app can install extensions.</span></span> <span data-ttu-id="ef5c2-116">Aplikacja może wymagać od autorów rozszerzeń użycia niestandardowego typu pakietu w celu zidentyfikowania ich pakietów jako odpowiednich rozszerzeń, które są zgodne `ContosoExtension` z wymaganymi konwencjami.</span><span class="sxs-lookup"><span data-stu-id="ef5c2-116">The app could require extension authors to use the custom package type `ContosoExtension` to identify their packages as proper extensions that follow the required conventions.</span></span>

> [!WARNING]
> <span data-ttu-id="ef5c2-117">Pakiet z niestandardowym typem pakietu nie może zostać zainstalowany przez Visual Studio lub nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="ef5c2-117">A package with a custom package type cannot be installed by Visual Studio or nuget.exe.</span></span> <span data-ttu-id="ef5c2-118">Aby uzyskać więcej informacji, zobacz [NuGet/Home#10468.](https://github.com/NuGet/Home/issues/10468)</span><span class="sxs-lookup"><span data-stu-id="ef5c2-118">See [NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468) for more information.</span></span>

# <a name="using-dotnet-cli"></a>[<span data-ttu-id="ef5c2-119">Korzystanie z interfejsu wiersza polecenia dotnet</span><span class="sxs-lookup"><span data-stu-id="ef5c2-119">Using dotnet CLI</span></span>](#tab/dotnet)

<span data-ttu-id="ef5c2-120">Typy pakietów można ustawić w pliku projektu ( `.csproj` ):</span><span class="sxs-lookup"><span data-stu-id="ef5c2-120">Package types can be set in the project file (`.csproj`):</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="ef5c2-121">Pakiety o wielu zamierzonych zastosowaniach można oznaczać wieloma typami pakietów za pomocą `;` ogranicznika:</span><span class="sxs-lookup"><span data-stu-id="ef5c2-121">Packages with multiple intended uses can be marked with multiple package types using the `;` delimiter:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="ef5c2-122">Typy pakietów mogą być wersjonarowane przy użyciu `,` ogranicznika między typem pakietu a jego [`Version`](/dotnet/api/system.version) ciągiem:</span><span class="sxs-lookup"><span data-stu-id="ef5c2-122">Package types can be versioned using a `,` delimiter between the package type and its [`Version`](/dotnet/api/system.version) string:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[<span data-ttu-id="ef5c2-123">Korzystanie z nuget.exe</span><span class="sxs-lookup"><span data-stu-id="ef5c2-123">Using nuget.exe</span></span>](#tab/nugetexe)

<span data-ttu-id="ef5c2-124">Typy pakietów są ustawiane `.nuspec` w pliku w `packageTypes\packageType` węźle w `<metadata>` ramach elementu :</span><span class="sxs-lookup"><span data-stu-id="ef5c2-124">Package types are set in the `.nuspec` file within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

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

<span data-ttu-id="ef5c2-125">Pakiety o wielu zamierzonych zastosowaniach mogą być oznaczone wieloma typami pakietów:</span><span class="sxs-lookup"><span data-stu-id="ef5c2-125">Packages with multiple intended uses may be marked with multiple package types:</span></span>

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

<span data-ttu-id="ef5c2-126">Typy pakietów mogą być wersjonarowane przy użyciu [`Version`](/dotnet/api/system.version) ciągu:</span><span class="sxs-lookup"><span data-stu-id="ef5c2-126">Package types can be versioned using a [`Version`](/dotnet/api/system.version) string:</span></span>

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

<span data-ttu-id="ef5c2-127">Format ciągu typu pakietu jest dokładnie taki sam jak identyfikator pakietu.</span><span class="sxs-lookup"><span data-stu-id="ef5c2-127">The format of a package type string is exactly like a package ID.</span></span> <span data-ttu-id="ef5c2-128">Oznacza to, że typ pakietu jest ciągiem bez uwzględniania liter pasującymi do wyrażenia regularnego, który zawiera co najmniej jeden znak i co najwyżej `^\w+([_.-]\w+)*$` 100 znaków.</span><span class="sxs-lookup"><span data-stu-id="ef5c2-128">That is, a package type is a case-insensitive string matching the regular expression `^\w+([_.-]\w+)*$` having at least one character and at most 100 characters.</span></span>

<span data-ttu-id="ef5c2-129">Jeśli zostanie podany, wersja typu pakietu będzie [`Version`](/dotnet/api/system.version) ciągiem.</span><span class="sxs-lookup"><span data-stu-id="ef5c2-129">If provided, the package type version is a [`Version`](/dotnet/api/system.version) string.</span></span> <span data-ttu-id="ef5c2-130">Wersja typu pakietu jest opcjonalna i domyślnie ma wartość `0.0` .</span><span class="sxs-lookup"><span data-stu-id="ef5c2-130">The package type version is optional and defaults to `0.0`.</span></span>
