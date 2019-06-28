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
# <a name="select-assemblies-referenced-by-projects"></a><span data-ttu-id="54c7a-103">Wybierz zestawy, które odwołują się projekty</span><span class="sxs-lookup"><span data-stu-id="54c7a-103">Select Assemblies Referenced By Projects</span></span>

<span data-ttu-id="54c7a-104">Odwołania do zestawu jawnych umożliwia podzbiór zestawów do użytku z technologii IntelliSense i kompilacja, gdy wszystkie zestawy są dostępne w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="54c7a-104">Explicit assembly references allows a subset of assemblies to be used for IntelliSense and compiling, while all assemblies are available at run-time.</span></span> <span data-ttu-id="54c7a-105">`PackageReference` i `packages.config` działają inaczej, a w rezultacie autorom pakietów należy zachować ostrożność do utworzenia pakietu, aby był zgodny z oboma typami projektów.</span><span class="sxs-lookup"><span data-stu-id="54c7a-105">`PackageReference` and `packages.config` work differently, and as a result package authors need to take care to create the package to be compatible with both project types.</span></span>

> [!Note]
> <span data-ttu-id="54c7a-106">Odwołania do zestawu jawnych odnoszą się do zestawów platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="54c7a-106">Explicit assembly references are related to .NET assemblies.</span></span> <span data-ttu-id="54c7a-107">Nie jest metodą do rozpowszechniania zestawów natywnych, które są P/wywoływany przez zestaw zarządzany.</span><span class="sxs-lookup"><span data-stu-id="54c7a-107">It is not a method to distribute native assemblies that are P/Invoked by a managed assembly.</span></span>

## <a name="packagereference-support"></a><span data-ttu-id="54c7a-108">`PackageReference` Obsługa</span><span class="sxs-lookup"><span data-stu-id="54c7a-108">`PackageReference` support</span></span>

<span data-ttu-id="54c7a-109">Jeśli projekt używa pakietu o `PackageReference` i pakiet zawiera `ref\<tfm>\` katalogu NuGet zostanie klasyfikowanie tych składa się jako zasoby kompilacji podczas `lib\<tfm>\` zestawy są klasyfikowane jako zasoby w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="54c7a-109">When a project uses a package with `PackageReference` and the package contains a `ref\<tfm>\` directory, NuGet will classify those assembles as compile-time assets, while the `lib\<tfm>\` assemblies are classified as runtime assets.</span></span> <span data-ttu-id="54c7a-110">Zestawy w `ref\<tfm>\` nie są używane w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="54c7a-110">Assemblies in `ref\<tfm>\` are not used at runtime.</span></span> <span data-ttu-id="54c7a-111">Oznacza to, niezbędne jest, aby każdy zespół w `ref\<tfm>\` mieć pasujący zestaw albo `lib\<tfm>\` nieznaczące `runtime\` katalogu, w przeciwnym razie środowisko uruchomieniowe prawdopodobnie wystąpią błędy.</span><span class="sxs-lookup"><span data-stu-id="54c7a-111">This means it is necessary for any assembly in `ref\<tfm>\` to have a matching assembly in either `lib\<tfm>\` or a relevant `runtime\` directory, otherwise runtime errors will likely occur.</span></span> <span data-ttu-id="54c7a-112">Ponieważ zestawy w `ref\<tfm>\` nie są używane w czasie wykonywania, może być [zestawów zawierających tylko metadane](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) zmniejszyć rozmiar pakietu.</span><span class="sxs-lookup"><span data-stu-id="54c7a-112">Since assemblies in `ref\<tfm>\` are not used at runtime, they may be [metadata-only assemblies](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) to reduce package size.</span></span>

> [!Important]
> <span data-ttu-id="54c7a-113">Jeśli pakiet zawiera nuspec `<references>` — element (używane przez `packages.config`, patrz poniżej) i nie zawiera zestawy w `ref\<tfm>\`, NuGet będzie anonsować zestawów na liście nuspec `<references>` elementu jako zasoby kompilacji i środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="54c7a-113">If a package contains the nuspec `<references>` element (used by `packages.config`, see below) and does not contain assemblies in `ref\<tfm>\`, NuGet will advertise the assemblies listed in the nuspec `<references>` element as both the compile and runtime assets.</span></span> <span data-ttu-id="54c7a-114">Oznacza to, będzie istnieć wyjątki środowiska uruchomieniowego podczas musisz załadować innego zestawu, w przywoływanych zestawach `lib\<tfm>\` katalogu.</span><span class="sxs-lookup"><span data-stu-id="54c7a-114">This means there will be runtime exceptions when the referenced assemblies need to load any other assembly in the `lib\<tfm>\` directory.</span></span>

> [!Note]
> <span data-ttu-id="54c7a-115">Jeśli pakiet zawiera `runtime\` katalogu NuGet nie wolno korzystać z zasobów w `lib\` katalogu.</span><span class="sxs-lookup"><span data-stu-id="54c7a-115">If the package contains a `runtime\` directory, NuGet may not use the assets in the `lib\` directory.</span></span>

## <a name="packagesconfig-support"></a><span data-ttu-id="54c7a-116">`packages.config` Obsługa</span><span class="sxs-lookup"><span data-stu-id="54c7a-116">`packages.config` support</span></span>

<span data-ttu-id="54c7a-117">Projekty, za pomocą `packages.config` do zarządzania NuGet pakietów zwykle dodać odwołania do wszystkich zestawów w `lib\<tfm>\` katalogu.</span><span class="sxs-lookup"><span data-stu-id="54c7a-117">Projects using `packages.config` to manage NuGet packages normally add references to all assemblies in the `lib\<tfm>\` directory.</span></span> <span data-ttu-id="54c7a-118">`ref\` Katalog został dodany do obsługi `PackageReference` i dlatego nie jest traktowane jako przy użyciu `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="54c7a-118">The `ref\` directory was added to support `PackageReference` and therefore isn't considered when using `packages.config`.</span></span> <span data-ttu-id="54c7a-119">Aby jawnie ustawić zestawy, które są określone dla projektów przy użyciu `packages.config`, należy użyć pakietu [ `<references>` elementu w pliku nuspec](../reference/nuspec.md#explicit-assembly-references).</span><span class="sxs-lookup"><span data-stu-id="54c7a-119">To explicitly set which assemblies are referenced for projects using `packages.config`, the package must use the [`<references>` element in the nuspec file](../reference/nuspec.md#explicit-assembly-references).</span></span> <span data-ttu-id="54c7a-120">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="54c7a-120">For example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> <span data-ttu-id="54c7a-121">`packages.config` Użyj projektu w proces nazywany [resolveassemblyreference —](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) Aby skopiować zestawy `bin\<configuration>\` katalogu wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="54c7a-121">`packages.config` project use a process called [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) to copy assemblies to the `bin\<configuration>\` output directory.</span></span> <span data-ttu-id="54c7a-122">Zestawu projektu jest kopiowana, a następnie system kompilacji analizuje manifestu zestawu dla zestawów odwołania, a następnie kopiuje te zestawy i rekursywnie powtarza się dla wszystkich zestawów.</span><span class="sxs-lookup"><span data-stu-id="54c7a-122">Your project's assembly is copied, then the build system looks at the assembly manifest for referenced assemblies, then copies those assemblies and recursively repeats for all assemblies.</span></span> <span data-ttu-id="54c7a-123">Oznacza to, że jeśli żadnego z zestawów w swojej `lib\<tfm>\` katalogu nie są wymienione w manifeście żadnych innych zestawów jako zależność (Jeśli zestaw jest ładowany w czasie wykonywania za pomocą `Assembly.Load`, MEF lub innej struktury iniekcji zależności), nie może mieć skopiowany do swojego projektu `bin\<configuration>\` katalog wyjściowy, mimo że znajduje się w `bin\<tfm>\`.</span><span class="sxs-lookup"><span data-stu-id="54c7a-123">This means that if any of the assemblies in your `lib\<tfm>\` directory are not listed in any other assembly's manifest as a dependency (if the assembly is loaded at runtime using `Assembly.Load`, MEF or another dependency injection framework), then it may not be copied to your project's `bin\<configuration>\` output directory despite being in `bin\<tfm>\`.</span></span>

## <a name="example"></a><span data-ttu-id="54c7a-124">Przykład</span><span class="sxs-lookup"><span data-stu-id="54c7a-124">Example</span></span>

<span data-ttu-id="54c7a-125">Mój pakiet będzie zawierał trzy zestawy `MyLib.dll`, `MyHelpers.dll` i `MyUtilities.dll`, które są przeznaczone dla .NET Framework 4.7.2.</span><span class="sxs-lookup"><span data-stu-id="54c7a-125">My package will contain three assemblies, `MyLib.dll`, `MyHelpers.dll` and `MyUtilities.dll`, which are targeting the .NET Framework 4.7.2.</span></span> <span data-ttu-id="54c7a-126">`MyUtilities.dll` zawiera klasy przeznaczone do użycia tylko przez te dwa zestawy, dzięki czemu nie chcesz udostępnić te klasy w technologii IntelliSense lub w czasie kompilacji projektów za pomocą Mój pakiet.</span><span class="sxs-lookup"><span data-stu-id="54c7a-126">`MyUtilities.dll` contains classes intended to be used only by the other two assemblies, so I don't want to make those classes available in IntelliSense or at compile time to projects using my package.</span></span> <span data-ttu-id="54c7a-127">Moje `nuspec` plik musi zawierać następujące elementy XML:</span><span class="sxs-lookup"><span data-stu-id="54c7a-127">My `nuspec` file needs to contain the following XML elements:</span></span>

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

<span data-ttu-id="54c7a-128">pliki w pakiecie. zostanie ona:</span><span class="sxs-lookup"><span data-stu-id="54c7a-128">and the files in the package will be:</span></span>

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
