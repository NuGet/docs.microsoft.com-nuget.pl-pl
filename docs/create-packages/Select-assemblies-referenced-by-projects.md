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
# <a name="select-assemblies-referenced-by-projects"></a><span data-ttu-id="bd91a-103">Wybierz zestawy, do których odwołują się projekty</span><span class="sxs-lookup"><span data-stu-id="bd91a-103">Select Assemblies Referenced By Projects</span></span>

<span data-ttu-id="bd91a-104">Jawne odwołania do zestawu umożliwia podzbiór zestawów do użycia dla IntelliSense i kompilacji, podczas gdy wszystkie zestawy są dostępne w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="bd91a-104">Explicit assembly references allows a subset of assemblies to be used for IntelliSense and compiling, while all assemblies are available at run-time.</span></span> <span data-ttu-id="bd91a-105">`PackageReference`i `packages.config` działać inaczej, a w rezultacie autorzy pakietu muszą zadbać o stworzenie pakietu, aby był zgodny z obu typów projektu.</span><span class="sxs-lookup"><span data-stu-id="bd91a-105">`PackageReference` and `packages.config` work differently, and as a result package authors need to take care to create the package to be compatible with both project types.</span></span>

> [!Note]
> <span data-ttu-id="bd91a-106">Jawne odwołania do zestawu są powiązane z zestawami .NET.</span><span class="sxs-lookup"><span data-stu-id="bd91a-106">Explicit assembly references are related to .NET assemblies.</span></span> <span data-ttu-id="bd91a-107">Nie jest to metoda dystrybucji natywnych zestawów, które są P/Invoked przez zestaw zarządzany.</span><span class="sxs-lookup"><span data-stu-id="bd91a-107">It is not a method to distribute native assemblies that are P/Invoked by a managed assembly.</span></span>

## <a name="packagereference-support"></a><span data-ttu-id="bd91a-108">`PackageReference`Wsparcie</span><span class="sxs-lookup"><span data-stu-id="bd91a-108">`PackageReference` support</span></span>

<span data-ttu-id="bd91a-109">Gdy projekt używa pakietu `PackageReference` z i pakiet `ref\<tfm>\` zawiera katalog, NuGet klasyfikuje te zestawy jako zasoby `lib\<tfm>\` w czasie kompilacji, podczas gdy zestawy są klasyfikowane jako zasoby środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="bd91a-109">When a project uses a package with `PackageReference` and the package contains a `ref\<tfm>\` directory, NuGet will classify those assembles as compile-time assets, while the `lib\<tfm>\` assemblies are classified as runtime assets.</span></span> <span data-ttu-id="bd91a-110">Zestawy w `ref\<tfm>\` nie są używane w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="bd91a-110">Assemblies in `ref\<tfm>\` are not used at runtime.</span></span> <span data-ttu-id="bd91a-111">Oznacza to, że jest `ref\<tfm>\` to konieczne dla każdego `lib\<tfm>\` zestawu w `runtime\` mieć pasujące zestawu w jednym lub odpowiedniego katalogu, w przeciwnym razie błędy środowiska uruchomieniowego prawdopodobnie wystąpią.</span><span class="sxs-lookup"><span data-stu-id="bd91a-111">This means it is necessary for any assembly in `ref\<tfm>\` to have a matching assembly in either `lib\<tfm>\` or a relevant `runtime\` directory, otherwise runtime errors will likely occur.</span></span> <span data-ttu-id="bd91a-112">Ponieważ zestawy `ref\<tfm>\` w nie są używane w czasie wykonywania, mogą być [tylko do metadanych zestawów](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) w celu zmniejszenia rozmiaru pakietu.</span><span class="sxs-lookup"><span data-stu-id="bd91a-112">Since assemblies in `ref\<tfm>\` are not used at runtime, they may be [metadata-only assemblies](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) to reduce package size.</span></span>

> [!Important]
> <span data-ttu-id="bd91a-113">Jeśli pakiet `<references>` zawiera nuspec element `packages.config`(używany przez , patrz poniżej) i nie zawiera zestawów w `ref\<tfm>\` `<references>` , NuGet anonsuje zestawy wymienione w nuspec element zarówno skompilować i zasobów środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="bd91a-113">If a package contains the nuspec `<references>` element (used by `packages.config`, see below) and does not contain assemblies in `ref\<tfm>\`, NuGet will advertise the assemblies listed in the nuspec `<references>` element as both the compile and runtime assets.</span></span> <span data-ttu-id="bd91a-114">Oznacza to, że będą wyjątki środowiska uruchomieniowego, gdy zestawy, `lib\<tfm>\` do których istnieje odwołanie, muszą załadować inny zestaw w katalogu.</span><span class="sxs-lookup"><span data-stu-id="bd91a-114">This means there will be runtime exceptions when the referenced assemblies need to load any other assembly in the `lib\<tfm>\` directory.</span></span>

> [!Note]
> <span data-ttu-id="bd91a-115">Jeśli pakiet zawiera `runtime\` katalog, NuGet nie może używać `lib\` zasobów w katalogu.</span><span class="sxs-lookup"><span data-stu-id="bd91a-115">If the package contains a `runtime\` directory, NuGet may not use the assets in the `lib\` directory.</span></span>

## <a name="packagesconfig-support"></a><span data-ttu-id="bd91a-116">`packages.config`Wsparcie</span><span class="sxs-lookup"><span data-stu-id="bd91a-116">`packages.config` support</span></span>

<span data-ttu-id="bd91a-117">Projekty `packages.config` używane do zarządzania pakietami NuGet zwykle dodają odwołania do wszystkich zestawów w `lib\<tfm>\` katalogu.</span><span class="sxs-lookup"><span data-stu-id="bd91a-117">Projects using `packages.config` to manage NuGet packages normally add references to all assemblies in the `lib\<tfm>\` directory.</span></span> <span data-ttu-id="bd91a-118">Katalog `ref\` został dodany do `PackageReference` obsługi i dlatego nie `packages.config`jest brany pod uwagę podczas korzystania .</span><span class="sxs-lookup"><span data-stu-id="bd91a-118">The `ref\` directory was added to support `PackageReference` and therefore isn't considered when using `packages.config`.</span></span> <span data-ttu-id="bd91a-119">Aby jawnie ustawić, do których zestawów są przywoływane dla projektów przy użyciu, `packages.config`pakiet musi użyć [ `<references>` elementu w pliku nuspec](../reference/nuspec.md#explicit-assembly-references).</span><span class="sxs-lookup"><span data-stu-id="bd91a-119">To explicitly set which assemblies are referenced for projects using `packages.config`, the package must use the [`<references>` element in the nuspec file](../reference/nuspec.md#explicit-assembly-references).</span></span> <span data-ttu-id="bd91a-120">Przykład:</span><span class="sxs-lookup"><span data-stu-id="bd91a-120">For example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> <span data-ttu-id="bd91a-121">`packages.config`projekt użyć procesu o nazwie [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) `bin\<configuration>\` do kopiowania zestawów do katalogu wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="bd91a-121">`packages.config` project use a process called [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) to copy assemblies to the `bin\<configuration>\` output directory.</span></span> <span data-ttu-id="bd91a-122">Zestaw projektu jest kopiowany, a następnie system kompilacji patrzy na manifest zestawu dla zestawów, do których istnieje odwołanie, a następnie kopiuje te zestawy i powtarza się rekurencyjnie dla wszystkich zestawów.</span><span class="sxs-lookup"><span data-stu-id="bd91a-122">Your project's assembly is copied, then the build system looks at the assembly manifest for referenced assemblies, then copies those assemblies and recursively repeats for all assemblies.</span></span> <span data-ttu-id="bd91a-123">Oznacza to, że jeśli którykolwiek `lib\<tfm>\` z zestawów w katalogu nie są wymienione w manifeście innego zestawu `Assembly.Load`jako zależność (jeśli zestaw jest ładowany w czasie wykonywania `bin\<configuration>\` przy użyciu MEF `bin\<tfm>\`lub innej struktury iniekcji zależności), to nie może być kopiowany do katalogu wyjściowego projektu, mimo że jest w .</span><span class="sxs-lookup"><span data-stu-id="bd91a-123">This means that if any of the assemblies in your `lib\<tfm>\` directory are not listed in any other assembly's manifest as a dependency (if the assembly is loaded at runtime using `Assembly.Load`, MEF or another dependency injection framework), then it may not be copied to your project's `bin\<configuration>\` output directory despite being in `bin\<tfm>\`.</span></span>

## <a name="example"></a><span data-ttu-id="bd91a-124">Przykład</span><span class="sxs-lookup"><span data-stu-id="bd91a-124">Example</span></span>

<span data-ttu-id="bd91a-125">Mój pakiet będzie zawierać `MyLib.dll`trzy `MyHelpers.dll` `MyUtilities.dll`zestawy i , które są przeznaczone dla .NET Framework 4.7.2.</span><span class="sxs-lookup"><span data-stu-id="bd91a-125">My package will contain three assemblies, `MyLib.dll`, `MyHelpers.dll` and `MyUtilities.dll`, which are targeting the .NET Framework 4.7.2.</span></span> <span data-ttu-id="bd91a-126">`MyUtilities.dll`zawiera klasy przeznaczone do użycia tylko przez pozostałe dwa zestawy, więc nie chcę, aby te klasy dostępne w IntelliSense lub w czasie kompilacji do projektów przy użyciu mojego pakietu.</span><span class="sxs-lookup"><span data-stu-id="bd91a-126">`MyUtilities.dll` contains classes intended to be used only by the other two assemblies, so I don't want to make those classes available in IntelliSense or at compile time to projects using my package.</span></span> <span data-ttu-id="bd91a-127">Mój `nuspec` plik musi zawierać następujące elementy XML:</span><span class="sxs-lookup"><span data-stu-id="bd91a-127">My `nuspec` file needs to contain the following XML elements:</span></span>

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

<span data-ttu-id="bd91a-128">a pliki w pakiecie będą:</span><span class="sxs-lookup"><span data-stu-id="bd91a-128">and the files in the package will be:</span></span>

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
