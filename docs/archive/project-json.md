---
title: project.jsodwołania do pliku dla pakietu NuGet
description: W przypadku niektórych typów projektów project.jsna zachowuje listę pakietów NuGet używanych w projekcie.
author: JonDouglas
ms.author: jodou
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: 6665f4f3e688cb4a3989216c8c8f1a8655b61ed8
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775197"
---
# <a name="projectjson-reference"></a><span data-ttu-id="f97b5-103">project.jsna temat odwołania</span><span class="sxs-lookup"><span data-stu-id="f97b5-103">project.json reference</span></span>

<span data-ttu-id="f97b5-104">*Pakiet NuGet 3. x +*</span><span class="sxs-lookup"><span data-stu-id="f97b5-104">*NuGet 3.x+*</span></span>

<span data-ttu-id="f97b5-105">`project.json`Plik zachowuje listę pakietów używanych w projekcie, nazywanych formatem zarządzania pakietami.</span><span class="sxs-lookup"><span data-stu-id="f97b5-105">The `project.json` file maintains a list of packages used in a project, known as a package management format.</span></span> <span data-ttu-id="f97b5-106">Jest on zastępowany `packages.config` , ale jest zastępowany przez [PackageReference](../consume-packages/package-references-in-project-files.md) z pakietem NuGet 4.0 +.</span><span class="sxs-lookup"><span data-stu-id="f97b5-106">It supersedes `packages.config` but is in turn superseded by [PackageReference](../consume-packages/package-references-in-project-files.md) with NuGet 4.0+.</span></span>

<span data-ttu-id="f97b5-107">[`project.lock.json`](#projectlockjson)Plik (opisany poniżej) jest również używany w projektach korzystających z programu `project.json` .</span><span class="sxs-lookup"><span data-stu-id="f97b5-107">The [`project.lock.json`](#projectlockjson) file (described below) is also used in projects employing `project.json`.</span></span>

<span data-ttu-id="f97b5-108">`project.json` ma następującą strukturę podstawową, w której każdy z czterech obiektów najwyższego poziomu może mieć dowolną liczbę obiektów podrzędnych:</span><span class="sxs-lookup"><span data-stu-id="f97b5-108">`project.json` has the following basic structure, where each of the four top-level objects can have any number of child objects:</span></span>

```json
{
    "dependencies": {
        "PackageID" : "{version_constraint}"
    },
    "frameworks" : {
        "TxM" : {}
    },
    "runtimes" : {
        "RID": {}
    },
    "supports" : {
        "CompatibilityProfile" : {}
    }
}
```

## <a name="dependencies"></a><span data-ttu-id="f97b5-109">Zależności</span><span class="sxs-lookup"><span data-stu-id="f97b5-109">Dependencies</span></span>

<span data-ttu-id="f97b5-110">Wyświetla listę zależności pakietu NuGet projektu w następującej postaci:</span><span class="sxs-lookup"><span data-stu-id="f97b5-110">Lists the NuGet package dependencies of your project in the following form:</span></span>

```json
"PackageID" : "version_constraint"
```

<span data-ttu-id="f97b5-111">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="f97b5-111">For example:</span></span>

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

<span data-ttu-id="f97b5-112">`dependencies`Sekcja jest miejscem, w którym okno dialogowe Menedżera pakietów NuGet dodaje zależności pakietu do projektu.</span><span class="sxs-lookup"><span data-stu-id="f97b5-112">The `dependencies` section is where the NuGet Package Manager dialog adds package dependencies to your project.</span></span>

<span data-ttu-id="f97b5-113">Identyfikator pakietu odpowiada identyfikatorowi pakietu w nuget.org, tak samo jak identyfikator używany w konsoli Menedżera pakietów: `Install-Package Microsoft.NETCore` .</span><span class="sxs-lookup"><span data-stu-id="f97b5-113">The Package id corresponds to the id of the package on nuget.org , the same as the id used in the package manager console: `Install-Package Microsoft.NETCore`.</span></span>

<span data-ttu-id="f97b5-114">Gdy przywracane są pakiety, ograniczenie wersji `"5.0.0"` wskazuje `>= 5.0.0` .</span><span class="sxs-lookup"><span data-stu-id="f97b5-114">When restoring packages, the version constraint of `"5.0.0"` implies `>= 5.0.0`.</span></span> <span data-ttu-id="f97b5-115">Oznacza to, że jeśli 5.0.0 nie jest dostępny na serwerze, ale 5.0.1 to, pakiet NuGet instaluje 5.0.1 i ostrzega o uaktualnieniu.</span><span class="sxs-lookup"><span data-stu-id="f97b5-115">That is, if 5.0.0 is not available on the server but 5.0.1 is, NuGet installs  5.0.1 and warns you about the upgrade.</span></span> <span data-ttu-id="f97b5-116">W przeciwnym razie program NuGet wybiera najmniejszą możliwą wersję na serwerze pasującym do ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="f97b5-116">NuGet otherwise picks the lowest possible version on the server matching the constraint.</span></span>

<span data-ttu-id="f97b5-117">Zobacz [rozpoznawanie zależności](../concepts/dependency-resolution.md) , aby uzyskać więcej informacji o regułach rozpoznawania.</span><span class="sxs-lookup"><span data-stu-id="f97b5-117">See [Dependency resolution](../concepts/dependency-resolution.md) for more details on resolution rules.</span></span>

### <a name="managing-dependency-assets"></a><span data-ttu-id="f97b5-118">Zarządzanie zasobami zależności</span><span class="sxs-lookup"><span data-stu-id="f97b5-118">Managing dependency assets</span></span>

<span data-ttu-id="f97b5-119">Które zasoby z zależności są przepływem do projektu najwyższego poziomu, są kontrolowane przez określenie zestawu tagów rozdzielanych przecinkami we `include` `exclude` właściwościach i odwołania do zależności.</span><span class="sxs-lookup"><span data-stu-id="f97b5-119">Which assets from dependencies flow into the top-level project is controlled by specifying a comma-delimited set of tags in the `include` and `exclude` properties of the dependency reference.</span></span> <span data-ttu-id="f97b5-120">Tagi są wymienione w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="f97b5-120">The tags are listed the table below:</span></span>

| <span data-ttu-id="f97b5-121">Include/Exclude — tag</span><span class="sxs-lookup"><span data-stu-id="f97b5-121">Include/Exclude tag</span></span> | <span data-ttu-id="f97b5-122">Zmodyfikowane foldery elementu docelowego</span><span class="sxs-lookup"><span data-stu-id="f97b5-122">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="f97b5-123">contentFiles</span><span class="sxs-lookup"><span data-stu-id="f97b5-123">contentFiles</span></span> | <span data-ttu-id="f97b5-124">Zawartość</span><span class="sxs-lookup"><span data-stu-id="f97b5-124">Content</span></span>  |
| <span data-ttu-id="f97b5-125">środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="f97b5-125">runtime</span></span> | <span data-ttu-id="f97b5-126">Środowisko uruchomieniowe, zasoby i FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="f97b5-126">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="f97b5-127">kompilowanie</span><span class="sxs-lookup"><span data-stu-id="f97b5-127">compile</span></span> | <span data-ttu-id="f97b5-128">lib</span><span class="sxs-lookup"><span data-stu-id="f97b5-128">lib</span></span> |
| <span data-ttu-id="f97b5-129">kompilacja</span><span class="sxs-lookup"><span data-stu-id="f97b5-129">build</span></span> | <span data-ttu-id="f97b5-130">Kompilacja (właściwości i elementy docelowe programu MSBuild)</span><span class="sxs-lookup"><span data-stu-id="f97b5-130">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="f97b5-131">natywne</span><span class="sxs-lookup"><span data-stu-id="f97b5-131">native</span></span> | <span data-ttu-id="f97b5-132">natywne</span><span class="sxs-lookup"><span data-stu-id="f97b5-132">native</span></span> |
| <span data-ttu-id="f97b5-133">brak</span><span class="sxs-lookup"><span data-stu-id="f97b5-133">none</span></span> | <span data-ttu-id="f97b5-134">Brak folderów</span><span class="sxs-lookup"><span data-stu-id="f97b5-134">No folders</span></span> |
| <span data-ttu-id="f97b5-135">all</span><span class="sxs-lookup"><span data-stu-id="f97b5-135">all</span></span> | <span data-ttu-id="f97b5-136">Wszystkie foldery</span><span class="sxs-lookup"><span data-stu-id="f97b5-136">All folders</span></span> |

<span data-ttu-id="f97b5-137">Tagi określone za pomocą `exclude` mają pierwszeństwo przed tymi określonymi przy użyciu `include` .</span><span class="sxs-lookup"><span data-stu-id="f97b5-137">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="f97b5-138">Na przykład `include="runtime, compile" exclude="compile"` jest taka sama jak `include="runtime"` .</span><span class="sxs-lookup"><span data-stu-id="f97b5-138">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span>

<span data-ttu-id="f97b5-139">Na przykład, aby uwzględnić `build` foldery i `native` zależności, użyj następujących elementów:</span><span class="sxs-lookup"><span data-stu-id="f97b5-139">For example, to include the `build` and `native` folders of a dependency, use the following:</span></span>

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "build, native"
    }
  }
}
```

<span data-ttu-id="f97b5-140">Aby wykluczyć `content` foldery i `build` zależności, użyj następujących elementów:</span><span class="sxs-lookup"><span data-stu-id="f97b5-140">To exclude the `content` and `build` folders of a dependency, use the following:</span></span>

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles, build"
    }
  }
}
```

## <a name="frameworks"></a><span data-ttu-id="f97b5-141">Struktury</span><span class="sxs-lookup"><span data-stu-id="f97b5-141">Frameworks</span></span>

<span data-ttu-id="f97b5-142">Wyświetla listę struktur, na których działa projekt, na przykład, `net45` `netcoreapp` , `netstandard` .</span><span class="sxs-lookup"><span data-stu-id="f97b5-142">Lists the frameworks that the project runs on, such as `net45`, `netcoreapp`, `netstandard`.</span></span>

```json
"frameworks": {
    "netcore50": {}
    }
 ```

<span data-ttu-id="f97b5-143">W sekcji dozwolony jest tylko pojedynczy wpis `frameworks` .</span><span class="sxs-lookup"><span data-stu-id="f97b5-143">Only a single entry is allowed in the `frameworks` section.</span></span> <span data-ttu-id="f97b5-144">(Wyjątek to `project.json` pliki dla projektów ASP.NET, które są kompilowane z nieprawidłowym łańcuchem narzędzi środowiska DNX, który pozwala na wiele elementów docelowych).</span><span class="sxs-lookup"><span data-stu-id="f97b5-144">(An exception is `project.json` files for ASP.NET projects that are build with deprecated DNX tool chain, which allows for multiple targets.)</span></span>

## <a name="runtimes"></a><span data-ttu-id="f97b5-145">Runtime</span><span class="sxs-lookup"><span data-stu-id="f97b5-145">Runtimes</span></span>

<span data-ttu-id="f97b5-146">Wyświetla listę systemów operacyjnych i architektur, na których działa aplikacja, na przykład, `win10-arm` `win8-x64` `win8-x86` .</span><span class="sxs-lookup"><span data-stu-id="f97b5-146">Lists the operating systems and architectures that your app runs on, such as `win10-arm`, `win8-x64`, `win8-x86`.</span></span>

```json
"runtimes": {
    "win10-arm": { },
    "win10-arm-aot": { },
    "win10-x86": { },
    "win10-x86-aot": { },
    "win10-x64": { },
    "win10-x64-aot": { }
}
```

<span data-ttu-id="f97b5-147">Pakiet zawierający PCL, który można uruchomić w dowolnym środowisku uruchomieniowym, nie musi określać środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="f97b5-147">A package containing a PCL that can run on any runtime doesn't need to specify a runtime.</span></span> <span data-ttu-id="f97b5-148">Musi on również mieć wartość true dla wszystkich zależności, w przeciwnym razie należy określić środowiska uruchomieniowe.</span><span class="sxs-lookup"><span data-stu-id="f97b5-148">This must also be true of any dependencies, otherwise you must specify runtimes.</span></span>


## <a name="supports"></a><span data-ttu-id="f97b5-149">Obsługuje</span><span class="sxs-lookup"><span data-stu-id="f97b5-149">Supports</span></span>

<span data-ttu-id="f97b5-150">Definiuje zestaw kontroli zależności pakietów.</span><span class="sxs-lookup"><span data-stu-id="f97b5-150">Defines a set of checks for package dependencies.</span></span> <span data-ttu-id="f97b5-151">Możesz określić, gdzie ma zostać uruchomione PCL lub aplikacja.</span><span class="sxs-lookup"><span data-stu-id="f97b5-151">You can define where you expect the PCL or app to run.</span></span> <span data-ttu-id="f97b5-152">Definicje nie są restrykcyjne, ponieważ kod może być uruchomiony w innym miejscu.</span><span class="sxs-lookup"><span data-stu-id="f97b5-152">The definitions are not restrictive, as your code may be able to run elsewhere.</span></span> <span data-ttu-id="f97b5-153">Jednak określenie tych testów powoduje sprawdzenie, czy wszystkie zależności są spełnione na liście TxMs.</span><span class="sxs-lookup"><span data-stu-id="f97b5-153">But specifying these checks makes NuGet check that all dependencies are satisfied on the listed TxMs.</span></span> <span data-ttu-id="f97b5-154">Przykłady wartości dla tego elementu to: `net46.app` , `uwp.10.0.app` itp.</span><span class="sxs-lookup"><span data-stu-id="f97b5-154">Examples of the values for this are: `net46.app`, `uwp.10.0.app`, etc.</span></span>

<span data-ttu-id="f97b5-155">Ta sekcja powinna być wypełniana automatycznie po wybraniu wpisu w oknie dialogowym elementy docelowe biblioteki klas przenośnych.</span><span class="sxs-lookup"><span data-stu-id="f97b5-155">This section should be populated automatically when you select an entry in the Portable Class Library targets dialog.</span></span>

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a><span data-ttu-id="f97b5-156">Importowania</span><span class="sxs-lookup"><span data-stu-id="f97b5-156">Imports</span></span>

<span data-ttu-id="f97b5-157">Importy zostały zaprojektowane tak, aby zezwalały na pakiety, które używają `dotnet` TxM, do działania z pakietami, które nie deklarują TxM dotnet.</span><span class="sxs-lookup"><span data-stu-id="f97b5-157">Imports are designed to allow packages that use the `dotnet` TxM to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="f97b5-158">Jeśli projekt używa `dotnet` TxM, wszystkie pakiety, od których zależy, muszą mieć również `dotnet` TxM, o ile nie zostanie dodany następujący element do programu, `project.json` Aby zezwolić na `dotnet` niezgodność platform z `dotnet` :</span><span class="sxs-lookup"><span data-stu-id="f97b5-158">If your project is using the `dotnet` TxM then all the packages you depend on must also have a `dotnet` TxM, unless you add the following to your `project.json` to allow non `dotnet` platforms to be compatible with `dotnet`:</span></span>

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

<span data-ttu-id="f97b5-159">Jeśli używasz `dotnet` TxM, system projektu PCL dodaje odpowiednią `imports` instrukcję na podstawie obsługiwanych elementów docelowych.</span><span class="sxs-lookup"><span data-stu-id="f97b5-159">If you are using the `dotnet` TxM then the PCL project system adds the appropriate `imports` statement based on the supported targets.</span></span>

## <a name="differences-from-portable-apps-and-web-projects"></a><span data-ttu-id="f97b5-160">Różnice między aplikacjami przenośnymi i projektami sieci Web</span><span class="sxs-lookup"><span data-stu-id="f97b5-160">Differences from portable apps and web projects</span></span>

<span data-ttu-id="f97b5-161">`project.json`Plik używany przez program NuGet jest podzbiorem znalezionym w projektach ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="f97b5-161">The `project.json` file used by NuGet is a subset of that found in ASP.NET Core projects.</span></span> <span data-ttu-id="f97b5-162">W ASP.NET Core `project.json` jest używany dla metadanych projektu, informacji o kompilacji i zależności.</span><span class="sxs-lookup"><span data-stu-id="f97b5-162">In ASP.NET Core `project.json` is used for project metadata, compilation information, and dependencies.</span></span> <span data-ttu-id="f97b5-163">W przypadku użycia w innych systemach projektów te trzy elementy są podzielone na osobne pliki i `project.json` zawierają mniej informacji.</span><span class="sxs-lookup"><span data-stu-id="f97b5-163">When used in other project systems, those three things are split into separate files and `project.json` contains less information.</span></span> <span data-ttu-id="f97b5-164">Istotne różnice obejmują:</span><span class="sxs-lookup"><span data-stu-id="f97b5-164">Notable differences include:</span></span>

- <span data-ttu-id="f97b5-165">W sekcji może istnieć tylko jedna struktura `frameworks` .</span><span class="sxs-lookup"><span data-stu-id="f97b5-165">There can only be one framework in the `frameworks` section.</span></span>

- <span data-ttu-id="f97b5-166">Plik nie może zawierać zależności, opcji kompilacji itp., które są widoczne w `project.json` plikach środowiska DNX.</span><span class="sxs-lookup"><span data-stu-id="f97b5-166">The file cannot contain dependencies, compilation options, etc. that you see in DNX `project.json` files.</span></span> <span data-ttu-id="f97b5-167">Uwzględniając, że może istnieć tylko jedna struktura, nie ma sensu, aby wprowadzać zależności specyficzne dla struktury.</span><span class="sxs-lookup"><span data-stu-id="f97b5-167">Given that there can only be a single framework it doesn't make sense to enter framework-specific dependencies.</span></span>

- <span data-ttu-id="f97b5-168">Kompilacja jest obsługiwana przez program MSBuild, więc opcje kompilacji, Definicje preprocesora itp. są wszystkie częścią pliku projektu programu MSBuild `project.json` .</span><span class="sxs-lookup"><span data-stu-id="f97b5-168">Compilation is handled by MSBuild so compilation options, preprocessor defines, etc. are all part of the MSBuild project file and not `project.json`.</span></span>

<span data-ttu-id="f97b5-169">W programie NuGet 3 + deweloperzy nie mogą ręcznie edytować programu `project.json` , ponieważ interfejs użytkownika Menedżera pakietów w programie Visual Studio manipuluje zawartością.</span><span class="sxs-lookup"><span data-stu-id="f97b5-169">In NuGet 3+, developers are not expected to manually edit the `project.json`, as the Package Manager UI in Visual Studio manipulates the content.</span></span> <span data-ttu-id="f97b5-170">Tym samym, można wyedytować plik, ale należy skompilować projekt, aby uruchomić pakiet przywracania lub wywołać przywracanie w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="f97b5-170">That said, you can certainly edit the file, but you must build the project to start a package restore or invoke restore in another way.</span></span> <span data-ttu-id="f97b5-171">Zobacz [przywracanie pakietu](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="f97b5-171">See [Package restore](../consume-packages/package-restore.md).</span></span>


## <a name="projectlockjson"></a><span data-ttu-id="f97b5-172">project.lock.jsna</span><span class="sxs-lookup"><span data-stu-id="f97b5-172">project.lock.json</span></span>

<span data-ttu-id="f97b5-173">`project.lock.json`Plik jest generowany w procesie przywracania pakietów NuGet w projektach, które używają `project.json` .</span><span class="sxs-lookup"><span data-stu-id="f97b5-173">The `project.lock.json` file is generated in the process of restoring the NuGet packages in projects that use `project.json`.</span></span> <span data-ttu-id="f97b5-174">Zawiera migawkę wszystkich informacji, które są generowane jako pakiet NuGet, prowadzi do grafu pakietów i zawiera wersję, zawartość i zależności wszystkich pakietów w projekcie.</span><span class="sxs-lookup"><span data-stu-id="f97b5-174">It holds a snapshot of all the information that is generated as NuGet walks the graph of packages and includes the version, contents, and dependencies of all the packages in your project.</span></span> <span data-ttu-id="f97b5-175">System kompilacji używa tego do wybrania pakietów z globalnej lokalizacji, która jest istotna podczas kompilowania projektu, a nie w zależności od lokalnego folderu pakietów w samym projekcie.</span><span class="sxs-lookup"><span data-stu-id="f97b5-175">The build system uses this to choose packages from a global location that are relevant when building the project instead of depending on a local packages folder in the project itself.</span></span> <span data-ttu-id="f97b5-176">Powoduje to szybszą wydajność kompilacji, ponieważ jest konieczna tylko do odczytu, `project.lock.json` a nie wielu oddzielnych `.nuspec` plików.</span><span class="sxs-lookup"><span data-stu-id="f97b5-176">This results in faster build performance because it's necessary to read only `project.lock.json` instead of many separate `.nuspec` files.</span></span>

<span data-ttu-id="f97b5-177">`project.lock.json` jest generowany automatycznie podczas przywracania pakietu, więc można go pominąć z kontroli źródła przez dodanie go do `.gitignore` i `.tfignore` plików (zobacz [pakiety i kontrola źródła](../consume-packages/packages-and-source-control.md).</span><span class="sxs-lookup"><span data-stu-id="f97b5-177">`project.lock.json` is automatically generated on package restore, so it can be omitted from source control by adding it to `.gitignore` and `.tfignore` files (see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> <span data-ttu-id="f97b5-178">Jednakże jeśli zostanie uwzględniony w kontroli źródła, historia zmian pokazuje zmiany w zależnościach rozwiązanych w czasie.</span><span class="sxs-lookup"><span data-stu-id="f97b5-178">However, if you include it in source control, the change history shows changes in dependencies resolved over time.</span></span>
