---
title: "Odwołanie do pliku Project.JSON programu NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/27/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "W niektórych typów projektów project.json przechowuje listę pakiety NuGet służące do projektu."
keywords: "Odwołania do pakietu NuGet, zależności NuGet, plikiem project.lock.json w pliku project.json NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2e2c521b18dd67e49942cc20eafef0be7f91573a
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="projectjson-reference"></a><span data-ttu-id="d5df4-104">Odwołanie do pliku Project.JSON</span><span class="sxs-lookup"><span data-stu-id="d5df4-104">project.json reference</span></span>

<span data-ttu-id="d5df4-105">*NuGet 3.x+*</span><span class="sxs-lookup"><span data-stu-id="d5df4-105">*NuGet 3.x+*</span></span>

<span data-ttu-id="d5df4-106">`project.json` Pliku przechowuje listę pakietów używane w projekcie, znany jako formatu odwołanie do pakietu.</span><span class="sxs-lookup"><span data-stu-id="d5df4-106">The `project.json` file maintains a list of packages used in a project, known as a package reference format.</span></span> <span data-ttu-id="d5df4-107">Zastępuje ona `packages.config` , ale z kolei został zastąpiony przez [PackageReference](../consume-packages/package-references-in-project-files.md) nuget 4.0 +.</span><span class="sxs-lookup"><span data-stu-id="d5df4-107">It supersedes `packages.config` but is in turn superseded by [PackageReference](../consume-packages/package-references-in-project-files.md) with NuGet 4.0+.</span></span>

<span data-ttu-id="d5df4-108">[ `project.lock.json` ](#projectlockjson) Pliku (opisanych poniżej) służy także projektów wykorzystujących `project.json`.</span><span class="sxs-lookup"><span data-stu-id="d5df4-108">The [`project.lock.json`](#projectlockjson) file (described below) is also used in projects employing `project.json`.</span></span>

<span data-ttu-id="d5df4-109">`project.json`ma następującą strukturę podstawowe, gdzie każdy z czterech obiektów najwyższego poziomu może mieć dowolną liczbę obiektów podrzędnych:</span><span class="sxs-lookup"><span data-stu-id="d5df4-109">`project.json` has the following basic structure, where each of the four top-level objects can have any number of child objects:</span></span>

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

## <a name="dependencies"></a><span data-ttu-id="d5df4-110">Zależności</span><span class="sxs-lookup"><span data-stu-id="d5df4-110">Dependencies</span></span>

<span data-ttu-id="d5df4-111">Zawiera listę zależności pakietu NuGet projektu w następującej postaci:</span><span class="sxs-lookup"><span data-stu-id="d5df4-111">Lists the NuGet package dependencies of your project in the following form:</span></span>

```json
"PackageID" : "version_constraint"
```

<span data-ttu-id="d5df4-112">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="d5df4-112">For example:</span></span>

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

<span data-ttu-id="d5df4-113">`dependencies` Sekcja jest, gdy okno dialogowe Menedżer pakietów NuGet dodaje zależności pakietów do projektu.</span><span class="sxs-lookup"><span data-stu-id="d5df4-113">The `dependencies` section is where the NuGet Package Manager dialog adds package dependencies to your project.</span></span>

<span data-ttu-id="d5df4-114">Identyfikator pakietu identyfikatorowi pakietu na nuget.org, taki sam jak identyfikator używany w konsoli Menedżera pakietów: `Install-Package Microsoft.NETCore`.</span><span class="sxs-lookup"><span data-stu-id="d5df4-114">The Package id corresponds to the id of the package on nuget.org , the same as the id used in the package manager console: `Install-Package Microsoft.NETCore`.</span></span>

<span data-ttu-id="d5df4-115">Podczas przywracania pakietów, ograniczenie wersji `"5.0.0"` oznacza `>= 5.0.0`.</span><span class="sxs-lookup"><span data-stu-id="d5df4-115">When restoring packages, the version constraint of `"5.0.0"` implies `>= 5.0.0`.</span></span> <span data-ttu-id="d5df4-116">Oznacza to, że jeśli 5.0.0 nie jest dostępny na serwerze, ale jest 5.0.1, NuGet instaluje 5.0.1 i ostrzega użytkownika o uaktualnienie.</span><span class="sxs-lookup"><span data-stu-id="d5df4-116">That is, if 5.0.0 is not available on the server but 5.0.1 is, NuGet installs  5.0.1 and warns you about the upgrade.</span></span> <span data-ttu-id="d5df4-117">NuGet, w przeciwnym razie wybiera Najniższa wersja możliwe na serwerze ograniczenie dopasowania.</span><span class="sxs-lookup"><span data-stu-id="d5df4-117">NuGet otherwise picks the lowest possible version on the server matching the constraint.</span></span>

<span data-ttu-id="d5df4-118">Zobacz [rozpoznawania zależności](../consume-packages/dependency-resolution.md) uzyskać więcej informacji na temat reguł rozwiązywania.</span><span class="sxs-lookup"><span data-stu-id="d5df4-118">See [Dependency resolution](../consume-packages/dependency-resolution.md) for more details on resolution rules.</span></span>

### <a name="managing-dependency-assets"></a><span data-ttu-id="d5df4-119">Zarządzanie zasobami zależności</span><span class="sxs-lookup"><span data-stu-id="d5df4-119">Managing dependency assets</span></span>

<span data-ttu-id="d5df4-120">Które zasoby z zależnościami przepływać do projektu najwyższego poziomu jest kontrolowany przez podanie rozdzielana przecinkami zestawu tagów w `include` i `exclude` właściwości zależności odwołania.</span><span class="sxs-lookup"><span data-stu-id="d5df4-120">Which assets from dependencies flow into the top-level project is controlled by specifying a comma-delimited set of tags in the `include` and `exclude` properties of the dependency reference.</span></span> <span data-ttu-id="d5df4-121">Tagi są wymienione w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="d5df4-121">The tags are listed the table below:</span></span>

| <span data-ttu-id="d5df4-122">Dołączania/wykluczania tag</span><span class="sxs-lookup"><span data-stu-id="d5df4-122">Include/Exclude tag</span></span> | <span data-ttu-id="d5df4-123">Odpowiednie foldery elementu docelowego</span><span class="sxs-lookup"><span data-stu-id="d5df4-123">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="d5df4-124">Pliki</span><span class="sxs-lookup"><span data-stu-id="d5df4-124">contentFiles</span></span> | <span data-ttu-id="d5df4-125">Zawartość</span><span class="sxs-lookup"><span data-stu-id="d5df4-125">Content</span></span>  |
| <span data-ttu-id="d5df4-126">środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="d5df4-126">runtime</span></span> | <span data-ttu-id="d5df4-127">Środowisko uruchomieniowe, zasobów i FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="d5df4-127">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="d5df4-128">Kompilacji</span><span class="sxs-lookup"><span data-stu-id="d5df4-128">compile</span></span> | <span data-ttu-id="d5df4-129">lib</span><span class="sxs-lookup"><span data-stu-id="d5df4-129">lib</span></span> |
| <span data-ttu-id="d5df4-130">kompilacja</span><span class="sxs-lookup"><span data-stu-id="d5df4-130">build</span></span> | <span data-ttu-id="d5df4-131">Kompilacja (właściwości programu MSBuild i elementy docelowe)</span><span class="sxs-lookup"><span data-stu-id="d5df4-131">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="d5df4-132">natywne</span><span class="sxs-lookup"><span data-stu-id="d5df4-132">native</span></span> | <span data-ttu-id="d5df4-133">natywne</span><span class="sxs-lookup"><span data-stu-id="d5df4-133">native</span></span> |
| <span data-ttu-id="d5df4-134">brak</span><span class="sxs-lookup"><span data-stu-id="d5df4-134">none</span></span> | <span data-ttu-id="d5df4-135">Brak folderów</span><span class="sxs-lookup"><span data-stu-id="d5df4-135">No folders</span></span> |
| <span data-ttu-id="d5df4-136">wszystkie</span><span class="sxs-lookup"><span data-stu-id="d5df4-136">all</span></span> | <span data-ttu-id="d5df4-137">Wszystkie foldery</span><span class="sxs-lookup"><span data-stu-id="d5df4-137">All folders</span></span> |

<span data-ttu-id="d5df4-138">Określony za pomocą tagów `exclude` pierwszeństwo określony za pomocą `include`.</span><span class="sxs-lookup"><span data-stu-id="d5df4-138">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="d5df4-139">Na przykład `include="runtime, compile" exclude="compile"` jest taka sama jak `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="d5df4-139">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span>

<span data-ttu-id="d5df4-140">Na przykład, aby uwzględnić `build` i `native` foldery zależności, należy użyć następującego:</span><span class="sxs-lookup"><span data-stu-id="d5df4-140">For example, to include the `build` and `native` folders of a dependency, use the following:</span></span>

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

<span data-ttu-id="d5df4-141">Aby wykluczyć `content` i `build` foldery zależności, należy użyć następującego:</span><span class="sxs-lookup"><span data-stu-id="d5df4-141">To exclude the `content` and `build` folders of a dependency, use the following:</span></span>

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

## <a name="frameworks"></a><span data-ttu-id="d5df4-142">Struktury</span><span class="sxs-lookup"><span data-stu-id="d5df4-142">Frameworks</span></span>

<span data-ttu-id="d5df4-143">Wyświetla listę platform, których projekt używa, takich jak `net45`, `netcoreapp`, `netstandard`.</span><span class="sxs-lookup"><span data-stu-id="d5df4-143">Lists the frameworks that the project runs on, such as `net45`, `netcoreapp`, `netstandard`.</span></span>

```json
"frameworks": {
    "netcore50": {}
    }
 ```

<span data-ttu-id="d5df4-144">Tylko jeden wpis jest dozwolony w `frameworks` sekcji.</span><span class="sxs-lookup"><span data-stu-id="d5df4-144">Only a single entry is allowed in the `frameworks` section.</span></span> <span data-ttu-id="d5df4-145">(Wyjątkiem jest `project.json` pliki projektów ASP.NET, które są kompilowane z przestarzałe DNX łańcuch narzędzi, co umożliwia obsługę wielu elementów docelowych.)</span><span class="sxs-lookup"><span data-stu-id="d5df4-145">(An exception is `project.json` files for ASP.NET projects that are build with deprecated DNX toolchain, which allows for multiple targets.)</span></span>

## <a name="runtimes"></a><span data-ttu-id="d5df4-146">środowisk uruchomieniowych</span><span class="sxs-lookup"><span data-stu-id="d5df4-146">Runtimes</span></span>

<span data-ttu-id="d5df4-147">Zawiera listę systemów operacyjnych i architektur, których aplikacja będzie działać, takich jak `win10-arm`, `win8-x64`, `win8-x86`.</span><span class="sxs-lookup"><span data-stu-id="d5df4-147">Lists the operating systems and architectures that your app runs on, such as `win10-arm`, `win8-x64`, `win8-x86`.</span></span>

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

<span data-ttu-id="d5df4-148">Pakiet zawierający PCL, która może działać na dowolnym środowiska uruchomieniowego nie trzeba określić środowisko uruchomieniowe.</span><span class="sxs-lookup"><span data-stu-id="d5df4-148">A package containing a PCL that can run on any runtime doesn't need to specify a runtime.</span></span> <span data-ttu-id="d5df4-149">Musi to być także spełnione wszystkie zależności, w przeciwnym razie należy określić środowisk uruchomieniowych.</span><span class="sxs-lookup"><span data-stu-id="d5df4-149">This must also be true of any dependencies, otherwise you must specify runtimes.</span></span>


## <a name="supports"></a><span data-ttu-id="d5df4-150">Obsługuje</span><span class="sxs-lookup"><span data-stu-id="d5df4-150">Supports</span></span>

<span data-ttu-id="d5df4-151">Definiuje zestaw sprawdza, czy zależności pakietów.</span><span class="sxs-lookup"><span data-stu-id="d5df4-151">Defines a set of checks for package dependencies.</span></span> <span data-ttu-id="d5df4-152">Można określić, którego można spodziewać się PCL lub uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5df4-152">You can define where you expect the PCL or app to run.</span></span> <span data-ttu-id="d5df4-153">Definicje nie są restrykcyjne kodu mogą być w stanie do uruchamiania innych miejscach.</span><span class="sxs-lookup"><span data-stu-id="d5df4-153">The definitions are not restrictive, as your code may be able to run elsewhere.</span></span> <span data-ttu-id="d5df4-154">Ale określenie kontrole powoduje, że NuGet, sprawdź, czy wszystkie zależności na liście TxMs.</span><span class="sxs-lookup"><span data-stu-id="d5df4-154">But specifying these checks makes NuGet check that all dependencies are satisfied on the listed TxMs.</span></span> <span data-ttu-id="d5df4-155">Przykładowe wartości tej sytuacji należą: `net46.app`, `uwp.10.0.app`itp.</span><span class="sxs-lookup"><span data-stu-id="d5df4-155">Examples of the values for this are: `net46.app`, `uwp.10.0.app`, etc.</span></span>

<span data-ttu-id="d5df4-156">W tej sekcji powinny zostać wypełnione automatycznie po wybraniu pozycji w oknie dialogowym elementy docelowe przenośnej biblioteki klas.</span><span class="sxs-lookup"><span data-stu-id="d5df4-156">This section should be populated automatically when you select an entry in the Portable Class Library targets dialog.</span></span>

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a><span data-ttu-id="d5df4-157">Importy</span><span class="sxs-lookup"><span data-stu-id="d5df4-157">Imports</span></span>

<span data-ttu-id="d5df4-158">Importy pozwalają pakiety, które używają `dotnet` TxM do pracy z pakietami, które nie deklaruje dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="d5df4-158">Imports are designed to allow packages that use the `dotnet` TxM to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="d5df4-159">Jeśli w twoim projekcie są używani `dotnet` TxM, a następnie wszystkie pakiety zależą od musi mieć również `dotnet` TxM, chyba że Dodaj następujący kod do Twojej `project.json` umożliwia z systemem innym niż `dotnet` platformy, aby był zgodny z `dotnet`:</span><span class="sxs-lookup"><span data-stu-id="d5df4-159">If your project is using the `dotnet` TxM then all the packages you depend on must also have a `dotnet` TxM, unless you add the following to your `project.json` to allow non `dotnet` platforms to be compatible with `dotnet`:</span></span>

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

<span data-ttu-id="d5df4-160">Jeśli używasz `dotnet` TxM następnie system projektu PCL dodaje odpowiednie `imports` instrukcji na podstawie obsługiwanych celów.</span><span class="sxs-lookup"><span data-stu-id="d5df4-160">If you are using the `dotnet` TxM then the PCL project system adds the appropriate `imports` statement based on the supported targets.</span></span>

## <a name="differences-from-portable-apps-and-web-projects"></a><span data-ttu-id="d5df4-161">Różnice z przenośnym aplikacji i projekty sieci web</span><span class="sxs-lookup"><span data-stu-id="d5df4-161">Differences from portable apps and web projects</span></span>

<span data-ttu-id="d5df4-162">`project.json` Plik używany przez narzędzie NuGet jest podzbiorem wykryte w projektach platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="d5df4-162">The `project.json` file used by NuGet is a subset of that found in ASP.NET Core projects.</span></span> <span data-ttu-id="d5df4-163">W przypadku platformy ASP.NET Core `project.json` służy do metadanych projektu, informacje o kompilacji i zależności.</span><span class="sxs-lookup"><span data-stu-id="d5df4-163">In ASP.NET Core `project.json` is used for project metadata, compilation information, and dependencies.</span></span> <span data-ttu-id="d5df4-164">Gdy są używane w innych systemach projektu, te trzy elementy są podzielone na osobne pliki i `project.json` zawiera mniej informacji.</span><span class="sxs-lookup"><span data-stu-id="d5df4-164">When used in other project systems, those three things are split into separate files and `project.json` contains less information.</span></span> <span data-ttu-id="d5df4-165">Istotnych różnic obejmują:</span><span class="sxs-lookup"><span data-stu-id="d5df4-165">Notable differences include:</span></span>

- <span data-ttu-id="d5df4-166">Może istnieć tylko jeden framework w `frameworks` sekcji.</span><span class="sxs-lookup"><span data-stu-id="d5df4-166">There can only be one framework in the `frameworks` section.</span></span>

- <span data-ttu-id="d5df4-167">Plik nie może zawierać zależności, opcje kompilacji, itp., który pojawi się w DNX `project.json` plików.</span><span class="sxs-lookup"><span data-stu-id="d5df4-167">The file cannot contain dependencies, compilation options, etc. that you see in DNX `project.json` files.</span></span> <span data-ttu-id="d5df4-168">Biorąc pod uwagę, że może istnieć tylko jeden framework go nie ma sensu wprowadzenia zależności określonej struktury.</span><span class="sxs-lookup"><span data-stu-id="d5df4-168">Given that there can only be a single framework it doesn't make sense to enter framework-specific dependencies.</span></span>

- <span data-ttu-id="d5df4-169">Kompilacja jest obsługiwany przez MSBuild tak definiuje opcje kompilacji preprocesora, itp. to części pliku projektu MSBuild i nie `project.json`.</span><span class="sxs-lookup"><span data-stu-id="d5df4-169">Compilation is handled by MSBuild so compilation options, preprocessor defines, etc. are all part of the MSBuild project file and not `project.json`.</span></span>

<span data-ttu-id="d5df4-170">W NuGet 3 + deweloperzy najprawdopodobniej nie ręcznie edytować `project.json`, ponieważ zawartość manipuluje interfejsu użytkownika Menedżera pakietów w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d5df4-170">In NuGet 3+, developers are not expected to manually edit the `project.json`, as the Package Manager UI in Visual Studio manipulates the content.</span></span> <span data-ttu-id="d5df4-171">Inaczej mówiąc, na pewno można edytować plik, ale musisz go skompilować projekt, aby uruchomić Przywracanie pakietu lub wywołanie przywracania w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="d5df4-171">That said, you can certainly edit the file, but you must build the project to start a package restore or invoke restore in another way.</span></span> <span data-ttu-id="d5df4-172">Zobacz [Przywracanie pakietu](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="d5df4-172">See [Package restore](../consume-packages/package-restore.md).</span></span>


## <a name="projectlockjson"></a><span data-ttu-id="d5df4-173">project.lock.json</span><span class="sxs-lookup"><span data-stu-id="d5df4-173">project.lock.json</span></span>

<span data-ttu-id="d5df4-174">`project.lock.json` Plik został wygenerowany w trakcie przywracania pakietów NuGet w projektach, które używają `project.json`.</span><span class="sxs-lookup"><span data-stu-id="d5df4-174">The `project.lock.json` file is generated in the process of restoring the NuGet packages in projects that use `project.json`.</span></span> <span data-ttu-id="d5df4-175">Przechowuje migawkę wszystkie informacje, które są generowane zgodnie z NuGet przedstawia wykres pakietów i zawiera wersję, zawartość i zależności wszystkich pakietów w projekcie.</span><span class="sxs-lookup"><span data-stu-id="d5df4-175">It holds a snapshot of all the information that is generated as NuGet walks the graph of packages and includes the version, contents, and dependencies of all the packages in your project.</span></span> <span data-ttu-id="d5df4-176">System kompilacji używa go do wybierz pakiety z globalnej lokalizacji, które mają zastosowanie podczas kompilowania projektu zamiast w zależności od folderem lokalnym pakietów w samym projekcie.</span><span class="sxs-lookup"><span data-stu-id="d5df4-176">The build system uses this to choose packages from a global location that are relevant when building the project instead of depending on a local packages folder in the project itself.</span></span> <span data-ttu-id="d5df4-177">Powoduje to zwiększyć wydajność kompilacji, ponieważ jest tylko do odczytu `project.lock.json` zamiast wielu oddzielnych `.nuspec` plików.</span><span class="sxs-lookup"><span data-stu-id="d5df4-177">This results in faster build performance because it's necessary to read only `project.lock.json` instead of many separate `.nuspec` files.</span></span>

<span data-ttu-id="d5df4-178">`project.lock.json`jest generowana automatycznie na Przywracanie pakietu, dlatego można je pominąć z kontroli źródła, dodając go do `.gitignore` i `.tfignore` plików (zobacz [pakietów i kontroli źródła](../consume-packages/packages-and-source-control.md).</span><span class="sxs-lookup"><span data-stu-id="d5df4-178">`project.lock.json` is automatically generated on package restore, so it can be omitted from source control by adding it to `.gitignore` and `.tfignore` files (see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> <span data-ttu-id="d5df4-179">Jednak jeśli uwzględniony w kontroli źródła, historii zmian przedstawia zmiany w zależnościach rozwiązał w czasie.</span><span class="sxs-lookup"><span data-stu-id="d5df4-179">However, if you include it in source control, the change history shows changes in dependencies resolved over time.</span></span>
