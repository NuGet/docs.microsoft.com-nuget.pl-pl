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
# <a name="select-assemblies-referenced-by-projects"></a><span data-ttu-id="98684-103">Wybierz zestawy, do których odwołują się projekty</span><span class="sxs-lookup"><span data-stu-id="98684-103">Select Assemblies Referenced By Projects</span></span>

<span data-ttu-id="98684-104">Jawne odwołania do zestawów umożliwiają podzbiór zestawów, które mają być używane do IntelliSense i kompilowania, podczas gdy wszystkie zestawy są dostępne w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="98684-104">Explicit assembly references allows a subset of assemblies to be used for IntelliSense and compiling, while all assemblies are available at run-time.</span></span> <span data-ttu-id="98684-105">`PackageReference` i `packages.config` działają inaczej i w związku z tym autorzy pakietu muszą zachować ostrożność, aby utworzyć pakiet zgodny z typem obu projektów.</span><span class="sxs-lookup"><span data-stu-id="98684-105">`PackageReference` and `packages.config` work differently, and as a result package authors need to take care to create the package to be compatible with both project types.</span></span>

> [!Note]
> <span data-ttu-id="98684-106">Jawne odwołania do zestawów są powiązane z zestawami .NET.</span><span class="sxs-lookup"><span data-stu-id="98684-106">Explicit assembly references are related to .NET assemblies.</span></span> <span data-ttu-id="98684-107">Nie jest to metoda dystrybucji natywnych zestawów, które są wywoływane przez zestaw zarządzany.</span><span class="sxs-lookup"><span data-stu-id="98684-107">It is not a method to distribute native assemblies that are P/Invoked by a managed assembly.</span></span>

## <a name="packagereference-support"></a><span data-ttu-id="98684-108">`PackageReference` pomocy</span><span class="sxs-lookup"><span data-stu-id="98684-108">`PackageReference` support</span></span>

<span data-ttu-id="98684-109">Gdy projekt używa pakietu programu `PackageReference` i zawiera `ref\<tfm>\` katalog, pakiet NuGet klasyfikuje je jako zasoby w czasie kompilacji, a `lib\<tfm>\` zestawy są klasyfikowane jako zasoby środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="98684-109">When a project uses a package with `PackageReference` and the package contains a `ref\<tfm>\` directory, NuGet will classify those assembles as compile-time assets, while the `lib\<tfm>\` assemblies are classified as runtime assets.</span></span> <span data-ttu-id="98684-110">Zestawy w programie `ref\<tfm>\` nie są używane w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="98684-110">Assemblies in `ref\<tfm>\` are not used at runtime.</span></span> <span data-ttu-id="98684-111">Oznacza to, że jest to konieczne dla każdego zestawu w programie w `ref\<tfm>\` celu posiadania zestawu zgodnego z `lib\<tfm>\` lub w odpowiednim `runtime\` katalogu, w przeciwnym razie błędy środowiska uruchomieniowego mogą wystąpić.</span><span class="sxs-lookup"><span data-stu-id="98684-111">This means it is necessary for any assembly in `ref\<tfm>\` to have a matching assembly in either `lib\<tfm>\` or a relevant `runtime\` directory, otherwise runtime errors will likely occur.</span></span> <span data-ttu-id="98684-112">Ponieważ zestawy w programie `ref\<tfm>\` nie są używane w czasie wykonywania, mogą one być [zestawami tylko do metadanych](https://github.com/dotnet/roslyn/blob/main/docs/features/refout.md) , aby zmniejszyć rozmiar pakietu.</span><span class="sxs-lookup"><span data-stu-id="98684-112">Since assemblies in `ref\<tfm>\` are not used at runtime, they may be [metadata-only assemblies](https://github.com/dotnet/roslyn/blob/main/docs/features/refout.md) to reduce package size.</span></span>

> [!Important]
> <span data-ttu-id="98684-113">Jeśli pakiet zawiera `<references>` element nuspec (używany przez `packages.config` , zobacz poniżej) i nie zawiera zestawów w programie, program `ref\<tfm>\` NuGet anonsuje zestawy wymienione w `<references>` elemencie nuspec jako zasoby kompilacji i środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="98684-113">If a package contains the nuspec `<references>` element (used by `packages.config`, see below) and does not contain assemblies in `ref\<tfm>\`, NuGet will advertise the assemblies listed in the nuspec `<references>` element as both the compile and runtime assets.</span></span> <span data-ttu-id="98684-114">Oznacza to, że jeśli zestawy, do których istnieją odwołania, muszą załadować każdy inny zestaw w katalogu, zostaną wyjątków w czasie wykonywania `lib\<tfm>\` .</span><span class="sxs-lookup"><span data-stu-id="98684-114">This means there will be runtime exceptions when the referenced assemblies need to load any other assembly in the `lib\<tfm>\` directory.</span></span>

> [!Note]
> <span data-ttu-id="98684-115">Jeśli pakiet zawiera `runtime\` katalog, NuGet nie może używać zasobów w `lib\` katalogu.</span><span class="sxs-lookup"><span data-stu-id="98684-115">If the package contains a `runtime\` directory, NuGet may not use the assets in the `lib\` directory.</span></span>

## <a name="packagesconfig-support"></a><span data-ttu-id="98684-116">`packages.config` pomocy</span><span class="sxs-lookup"><span data-stu-id="98684-116">`packages.config` support</span></span>

<span data-ttu-id="98684-117">Projekty używające `packages.config` do zarządzania pakietami NuGet zwykle dodają odwołania do wszystkich zestawów w `lib\<tfm>\` katalogu.</span><span class="sxs-lookup"><span data-stu-id="98684-117">Projects using `packages.config` to manage NuGet packages normally add references to all assemblies in the `lib\<tfm>\` directory.</span></span> <span data-ttu-id="98684-118">`ref\`Katalog został dodany do obsługi `PackageReference` i w związku z tym nie jest brany pod uwagę podczas korzystania z programu `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="98684-118">The `ref\` directory was added to support `PackageReference` and therefore isn't considered when using `packages.config`.</span></span> <span data-ttu-id="98684-119">Aby jawnie ustawić zestawy, do których odwołują się projekty `packages.config` , pakiet musi używać [ `<references>` elementu w pliku nuspec](../reference/nuspec.md#explicit-assembly-references).</span><span class="sxs-lookup"><span data-stu-id="98684-119">To explicitly set which assemblies are referenced for projects using `packages.config`, the package must use the [`<references>` element in the nuspec file](../reference/nuspec.md#explicit-assembly-references).</span></span> <span data-ttu-id="98684-120">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="98684-120">For example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> <span data-ttu-id="98684-121">`packages.config` projekt używa procesu o nazwie [ResolveAssemblyReference —](https://github.com/Microsoft/msbuild/blob/main/documentation/wiki/ResolveAssemblyReference.md) do kopiowania zestawów do `bin\<configuration>\` katalogu wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="98684-121">`packages.config` project use a process called [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/main/documentation/wiki/ResolveAssemblyReference.md) to copy assemblies to the `bin\<configuration>\` output directory.</span></span> <span data-ttu-id="98684-122">Zestaw projektu jest kopiowany, a następnie system kompilacji sprawdza manifest zestawu dla przywoływanych zestawów, a następnie kopiuje te zestawy i cyklicznie powtarza dla wszystkich zestawów.</span><span class="sxs-lookup"><span data-stu-id="98684-122">Your project's assembly is copied, then the build system looks at the assembly manifest for referenced assemblies, then copies those assemblies and recursively repeats for all assemblies.</span></span> <span data-ttu-id="98684-123">Oznacza to, że jeśli którykolwiek z zestawów w `lib\<tfm>\` katalogu nie jest wymieniony w żadnym innym manifeście zestawu jako zależność (Jeśli zestaw jest ładowany w czasie wykonywania za pomocą `Assembly.Load` , MEF lub inną platformą wstrzykiwania zależności), wówczas może nie być kopiowany do katalogu wyjściowego projektu pomimo tego, że `bin\<configuration>\` jest w `bin\<tfm>\` .</span><span class="sxs-lookup"><span data-stu-id="98684-123">This means that if any of the assemblies in your `lib\<tfm>\` directory are not listed in any other assembly's manifest as a dependency (if the assembly is loaded at runtime using `Assembly.Load`, MEF or another dependency injection framework), then it may not be copied to your project's `bin\<configuration>\` output directory despite being in `bin\<tfm>\`.</span></span>

## <a name="example"></a><span data-ttu-id="98684-124">Przykład</span><span class="sxs-lookup"><span data-stu-id="98684-124">Example</span></span>

<span data-ttu-id="98684-125">Mój pakiet będzie zawierać trzy zestawy, `MyLib.dll` `MyHelpers.dll` i `MyUtilities.dll` , które są ukierunkowane na .NET Framework 4.7.2.</span><span class="sxs-lookup"><span data-stu-id="98684-125">My package will contain three assemblies, `MyLib.dll`, `MyHelpers.dll` and `MyUtilities.dll`, which are targeting the .NET Framework 4.7.2.</span></span> <span data-ttu-id="98684-126">`MyUtilities.dll` zawiera klasy przeznaczone do użycia tylko przez pozostałe dwa zestawy, więc nie chcę, aby te klasy były dostępne w technologii IntelliSense ani w czasie kompilacji do projektów przy użyciu mojego pakietu.</span><span class="sxs-lookup"><span data-stu-id="98684-126">`MyUtilities.dll` contains classes intended to be used only by the other two assemblies, so I don't want to make those classes available in IntelliSense or at compile time to projects using my package.</span></span> <span data-ttu-id="98684-127">Mój `nuspec` plik musi zawierać następujące elementy XML:</span><span class="sxs-lookup"><span data-stu-id="98684-127">My `nuspec` file needs to contain the following XML elements:</span></span>

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

<span data-ttu-id="98684-128">pliki w pakiecie będą:</span><span class="sxs-lookup"><span data-stu-id="98684-128">and the files in the package will be:</span></span>

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
