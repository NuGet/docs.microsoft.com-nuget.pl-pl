---
title: project.json— numer pliku dla usługi NuGet
description: W niektórych typach projektów project.json przechowuje listę pakietów NuGet używanych w projekcie.
author: karann-msft
ms.author: karann
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: 5ecbcd4855de8ea7b6301a5e307779216baf96fc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488282"
---
# <a name="projectjson-reference"></a><span data-ttu-id="e595a-103">odwołanie do pliku project.json</span><span class="sxs-lookup"><span data-stu-id="e595a-103">project.json reference</span></span>

<span data-ttu-id="e595a-104">*NuGet 3.x+*</span><span class="sxs-lookup"><span data-stu-id="e595a-104">*NuGet 3.x+*</span></span>

<span data-ttu-id="e595a-105">Plik `project.json` przechowuje listę pakietów używanych w projekcie, znany jako format zarządzania pakietami.</span><span class="sxs-lookup"><span data-stu-id="e595a-105">The `project.json` file maintains a list of packages used in a project, known as a package management format.</span></span> <span data-ttu-id="e595a-106">Zastępuje, `packages.config` ale z kolei zastępuje [packagereference](../consume-packages/package-references-in-project-files.md) z NuGet 4.0 +.</span><span class="sxs-lookup"><span data-stu-id="e595a-106">It supersedes `packages.config` but is in turn superseded by [PackageReference](../consume-packages/package-references-in-project-files.md) with NuGet 4.0+.</span></span>

<span data-ttu-id="e595a-107">Plik [`project.lock.json`](#projectlockjson) (opisany poniżej) jest również używany `project.json`w projektach zatrudniających .</span><span class="sxs-lookup"><span data-stu-id="e595a-107">The [`project.lock.json`](#projectlockjson) file (described below) is also used in projects employing `project.json`.</span></span>

<span data-ttu-id="e595a-108">`project.json`ma następującą podstawową strukturę, w której każdy z czterech obiektów najwyższego poziomu może mieć dowolną liczbę obiektów podrzędnych:</span><span class="sxs-lookup"><span data-stu-id="e595a-108">`project.json` has the following basic structure, where each of the four top-level objects can have any number of child objects:</span></span>

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

## <a name="dependencies"></a><span data-ttu-id="e595a-109">Zależności</span><span class="sxs-lookup"><span data-stu-id="e595a-109">Dependencies</span></span>

<span data-ttu-id="e595a-110">Wyświetla listę zależności pakietu NuGet projektu w następującej formie:</span><span class="sxs-lookup"><span data-stu-id="e595a-110">Lists the NuGet package dependencies of your project in the following form:</span></span>

```json
"PackageID" : "version_constraint"
```

<span data-ttu-id="e595a-111">Przykład:</span><span class="sxs-lookup"><span data-stu-id="e595a-111">For example:</span></span>

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

<span data-ttu-id="e595a-112">Sekcja `dependencies` jest, gdzie NuGet Package Manager okno dialogowe dodaje zależności pakietów do projektu.</span><span class="sxs-lookup"><span data-stu-id="e595a-112">The `dependencies` section is where the NuGet Package Manager dialog adds package dependencies to your project.</span></span>

<span data-ttu-id="e595a-113">Identyfikator pakietu odpowiada identyfikatorowi pakietu na nuget.org , tak samo jak identyfikator używany w konsoli menedżera `Install-Package Microsoft.NETCore`pakietów: .</span><span class="sxs-lookup"><span data-stu-id="e595a-113">The Package id corresponds to the id of the package on nuget.org , the same as the id used in the package manager console: `Install-Package Microsoft.NETCore`.</span></span>

<span data-ttu-id="e595a-114">Podczas przywracania pakietów ograniczenie `"5.0.0"` wersji `>= 5.0.0`implikuje .</span><span class="sxs-lookup"><span data-stu-id="e595a-114">When restoring packages, the version constraint of `"5.0.0"` implies `>= 5.0.0`.</span></span> <span data-ttu-id="e595a-115">Oznacza to, że jeśli 5.0.0 nie jest dostępny na serwerze, ale 5.0.1 jest, NuGet instaluje 5.0.1 i ostrzega o uaktualnieniu.</span><span class="sxs-lookup"><span data-stu-id="e595a-115">That is, if 5.0.0 is not available on the server but 5.0.1 is, NuGet installs  5.0.1 and warns you about the upgrade.</span></span> <span data-ttu-id="e595a-116">NuGet w przeciwnym razie wybiera najniższą możliwą wersję na serwerze pasujące do ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="e595a-116">NuGet otherwise picks the lowest possible version on the server matching the constraint.</span></span>

<span data-ttu-id="e595a-117">Zobacz [rozpoznawanie zależności, aby](../concepts/dependency-resolution.md) uzyskać więcej informacji na temat reguł rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="e595a-117">See [Dependency resolution](../concepts/dependency-resolution.md) for more details on resolution rules.</span></span>

### <a name="managing-dependency-assets"></a><span data-ttu-id="e595a-118">Zarządzanie zasobami zależności</span><span class="sxs-lookup"><span data-stu-id="e595a-118">Managing dependency assets</span></span>

<span data-ttu-id="e595a-119">Które zasoby z zależności przepływu do projektu najwyższego poziomu jest kontrolowana przez określenie rozdzielanych przecinkami zestaw tagów w `include` i `exclude` właściwości odwołania zależności.</span><span class="sxs-lookup"><span data-stu-id="e595a-119">Which assets from dependencies flow into the top-level project is controlled by specifying a comma-delimited set of tags in the `include` and `exclude` properties of the dependency reference.</span></span> <span data-ttu-id="e595a-120">Tagi są wymienione w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="e595a-120">The tags are listed the table below:</span></span>

| <span data-ttu-id="e595a-121">Tag Dołącz/Wyklucz</span><span class="sxs-lookup"><span data-stu-id="e595a-121">Include/Exclude tag</span></span> | <span data-ttu-id="e595a-122">Foldery docelowe, których dotyczy problem,</span><span class="sxs-lookup"><span data-stu-id="e595a-122">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="e595a-123">contentFiles</span><span class="sxs-lookup"><span data-stu-id="e595a-123">contentFiles</span></span> | <span data-ttu-id="e595a-124">Zawartość</span><span class="sxs-lookup"><span data-stu-id="e595a-124">Content</span></span>  |
| <span data-ttu-id="e595a-125">środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="e595a-125">runtime</span></span> | <span data-ttu-id="e595a-126">Środowisko wykonawcze, zasoby i asemblies framework</span><span class="sxs-lookup"><span data-stu-id="e595a-126">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="e595a-127">kompilowanie</span><span class="sxs-lookup"><span data-stu-id="e595a-127">compile</span></span> | <span data-ttu-id="e595a-128">Lib</span><span class="sxs-lookup"><span data-stu-id="e595a-128">lib</span></span> |
| <span data-ttu-id="e595a-129">kompilacja</span><span class="sxs-lookup"><span data-stu-id="e595a-129">build</span></span> | <span data-ttu-id="e595a-130">build (REKWIZYTY i obiekty docelowe MSBuild)</span><span class="sxs-lookup"><span data-stu-id="e595a-130">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="e595a-131">natywne</span><span class="sxs-lookup"><span data-stu-id="e595a-131">native</span></span> | <span data-ttu-id="e595a-132">natywne</span><span class="sxs-lookup"><span data-stu-id="e595a-132">native</span></span> |
| <span data-ttu-id="e595a-133">brak</span><span class="sxs-lookup"><span data-stu-id="e595a-133">none</span></span> | <span data-ttu-id="e595a-134">Brak folderów</span><span class="sxs-lookup"><span data-stu-id="e595a-134">No folders</span></span> |
| <span data-ttu-id="e595a-135">all</span><span class="sxs-lookup"><span data-stu-id="e595a-135">all</span></span> | <span data-ttu-id="e595a-136">Wszystkie foldery</span><span class="sxs-lookup"><span data-stu-id="e595a-136">All folders</span></span> |

<span data-ttu-id="e595a-137">Znaczniki określone `exclude` z pierwszeństwem nad `include`tymi określonymi za pomocą .</span><span class="sxs-lookup"><span data-stu-id="e595a-137">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="e595a-138">Na przykład `include="runtime, compile" exclude="compile"` jest taka `include="runtime"`sama jak .</span><span class="sxs-lookup"><span data-stu-id="e595a-138">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span>

<span data-ttu-id="e595a-139">Na przykład, aby `build` `native` uwzględnić i foldery zależności, należy użyć następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="e595a-139">For example, to include the `build` and `native` folders of a dependency, use the following:</span></span>

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

<span data-ttu-id="e595a-140">Aby wykluczyć `content` `build` i foldery zależności, należy użyć następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="e595a-140">To exclude the `content` and `build` folders of a dependency, use the following:</span></span>

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

## <a name="frameworks"></a><span data-ttu-id="e595a-141">Struktury</span><span class="sxs-lookup"><span data-stu-id="e595a-141">Frameworks</span></span>

<span data-ttu-id="e595a-142">Wyświetla listę struktur, na których działa `net45` `netcoreapp`projekt, takich jak , , `netstandard`.</span><span class="sxs-lookup"><span data-stu-id="e595a-142">Lists the frameworks that the project runs on, such as `net45`, `netcoreapp`, `netstandard`.</span></span>

```json
"frameworks": {
    "netcore50": {}
    }
 ```

<span data-ttu-id="e595a-143">W `frameworks` sekcji dozwolony jest tylko jeden wpis.</span><span class="sxs-lookup"><span data-stu-id="e595a-143">Only a single entry is allowed in the `frameworks` section.</span></span> <span data-ttu-id="e595a-144">(Wyjątkiem są `project.json` pliki dla ASP.NET projektów, które są budowane z przestarzałym łańcuchem narzędzi DNX, co pozwala na wiele obiektów docelowych).</span><span class="sxs-lookup"><span data-stu-id="e595a-144">(An exception is `project.json` files for ASP.NET projects that are build with deprecated DNX tool chain, which allows for multiple targets.)</span></span>

## <a name="runtimes"></a><span data-ttu-id="e595a-145">Środowiska wykonawcze</span><span class="sxs-lookup"><span data-stu-id="e595a-145">Runtimes</span></span>

<span data-ttu-id="e595a-146">Wyświetla listę systemów operacyjnych i architektur, na `win10-arm` `win8-x64`których `win8-x86`działa aplikacja, takich jak , .</span><span class="sxs-lookup"><span data-stu-id="e595a-146">Lists the operating systems and architectures that your app runs on, such as `win10-arm`, `win8-x64`, `win8-x86`.</span></span>

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

<span data-ttu-id="e595a-147">Pakiet zawierający PCL, który można uruchomić w dowolnym czasie wykonywania nie trzeba określać środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="e595a-147">A package containing a PCL that can run on any runtime doesn't need to specify a runtime.</span></span> <span data-ttu-id="e595a-148">Musi to być również prawdziwe wszelkie zależności, w przeciwnym razie należy określić środowiska wykonawcze.</span><span class="sxs-lookup"><span data-stu-id="e595a-148">This must also be true of any dependencies, otherwise you must specify runtimes.</span></span>


## <a name="supports"></a><span data-ttu-id="e595a-149">Obsługuje</span><span class="sxs-lookup"><span data-stu-id="e595a-149">Supports</span></span>

<span data-ttu-id="e595a-150">Definiuje zestaw kontroli zależności pakietu.</span><span class="sxs-lookup"><span data-stu-id="e595a-150">Defines a set of checks for package dependencies.</span></span> <span data-ttu-id="e595a-151">Można zdefiniować, gdzie można oczekiwać PCL lub aplikacji do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="e595a-151">You can define where you expect the PCL or app to run.</span></span> <span data-ttu-id="e595a-152">Definicje nie są restrykcyjne, ponieważ kod może być w stanie uruchomić w innym miejscu.</span><span class="sxs-lookup"><span data-stu-id="e595a-152">The definitions are not restrictive, as your code may be able to run elsewhere.</span></span> <span data-ttu-id="e595a-153">Jednak określenie tych kontroli sprawia, że NuGet sprawdza, czy wszystkie zależności są spełnione na wymienionych TxM.</span><span class="sxs-lookup"><span data-stu-id="e595a-153">But specifying these checks makes NuGet check that all dependencies are satisfied on the listed TxMs.</span></span> <span data-ttu-id="e595a-154">Przykłady wartości dla tego `net46.app`są: , `uwp.10.0.app`, itp.</span><span class="sxs-lookup"><span data-stu-id="e595a-154">Examples of the values for this are: `net46.app`, `uwp.10.0.app`, etc.</span></span>

<span data-ttu-id="e595a-155">Ta sekcja powinna być wypełniana automatycznie po wybraniu wpisu w oknie dialogowym Docelowe biblioteki klas przenośnych.</span><span class="sxs-lookup"><span data-stu-id="e595a-155">This section should be populated automatically when you select an entry in the Portable Class Library targets dialog.</span></span>

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a><span data-ttu-id="e595a-156">Przywozu</span><span class="sxs-lookup"><span data-stu-id="e595a-156">Imports</span></span>

<span data-ttu-id="e595a-157">Importy są przeznaczone do zezwalania pakietom, które używają `dotnet` TxM do pracy z pakietami, które nie deklarują dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="e595a-157">Imports are designed to allow packages that use the `dotnet` TxM to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="e595a-158">Jeśli projekt korzysta `dotnet` z TxM, wszystkie pakiety, od `dotnet` których jesteś zależny, muszą `project.json` mieć również `dotnet` TxM, `dotnet`chyba że dodasz do niego następujące elementy, aby umożliwić zgodność innych platform z:</span><span class="sxs-lookup"><span data-stu-id="e595a-158">If your project is using the `dotnet` TxM then all the packages you depend on must also have a `dotnet` TxM, unless you add the following to your `project.json` to allow non `dotnet` platforms to be compatible with `dotnet`:</span></span>

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

<span data-ttu-id="e595a-159">Jeśli używasz `dotnet` TxM następnie system projektu PCL `imports` dodaje odpowiednią instrukcję na podstawie obsługiwanych obiektów docelowych.</span><span class="sxs-lookup"><span data-stu-id="e595a-159">If you are using the `dotnet` TxM then the PCL project system adds the appropriate `imports` statement based on the supported targets.</span></span>

## <a name="differences-from-portable-apps-and-web-projects"></a><span data-ttu-id="e595a-160">Różnice w stosunku do aplikacji przenośnych i projektów internetowych</span><span class="sxs-lookup"><span data-stu-id="e595a-160">Differences from portable apps and web projects</span></span>

<span data-ttu-id="e595a-161">Plik `project.json` używany przez NuGet jest podzbiorem, który znajduje się w ASP.NET podstawowych projektów.</span><span class="sxs-lookup"><span data-stu-id="e595a-161">The `project.json` file used by NuGet is a subset of that found in ASP.NET Core projects.</span></span> <span data-ttu-id="e595a-162">W ASP.NET Core `project.json` jest używany dla metadanych projektu, informacji kompilacji i zależności.</span><span class="sxs-lookup"><span data-stu-id="e595a-162">In ASP.NET Core `project.json` is used for project metadata, compilation information, and dependencies.</span></span> <span data-ttu-id="e595a-163">Te trzy elementy są używane w innych systemach `project.json` projektu i zawierają mniej informacji.</span><span class="sxs-lookup"><span data-stu-id="e595a-163">When used in other project systems, those three things are split into separate files and `project.json` contains less information.</span></span> <span data-ttu-id="e595a-164">Znaczące różnice obejmują:</span><span class="sxs-lookup"><span data-stu-id="e595a-164">Notable differences include:</span></span>

- <span data-ttu-id="e595a-165">W `frameworks` sekcji może istnieć tylko jedna struktura.</span><span class="sxs-lookup"><span data-stu-id="e595a-165">There can only be one framework in the `frameworks` section.</span></span>

- <span data-ttu-id="e595a-166">Plik nie może zawierać zależności, opcji kompilacji itp., `project.json` które są widoczne w plikach DNX.</span><span class="sxs-lookup"><span data-stu-id="e595a-166">The file cannot contain dependencies, compilation options, etc. that you see in DNX `project.json` files.</span></span> <span data-ttu-id="e595a-167">Biorąc pod uwagę, że może istnieć tylko pojedyncza struktura nie ma sensu, aby wprowadzić zależności specyficzne dla struktury.</span><span class="sxs-lookup"><span data-stu-id="e595a-167">Given that there can only be a single framework it doesn't make sense to enter framework-specific dependencies.</span></span>

- <span data-ttu-id="e595a-168">Kompilacja jest obsługiwana przez MSBuild więc opcje kompilacji, definicje preprocesora itp. `project.json`</span><span class="sxs-lookup"><span data-stu-id="e595a-168">Compilation is handled by MSBuild so compilation options, preprocessor defines, etc. are all part of the MSBuild project file and not `project.json`.</span></span>

<span data-ttu-id="e595a-169">W NuGet 3+, deweloperzy nie oczekuje `project.json`się ręcznie edytować , jak interfejs użytkownika Menedżera pakietów w programie Visual Studio manipuluje zawartością.</span><span class="sxs-lookup"><span data-stu-id="e595a-169">In NuGet 3+, developers are not expected to manually edit the `project.json`, as the Package Manager UI in Visual Studio manipulates the content.</span></span> <span data-ttu-id="e595a-170">To powiedzia się, z pewnością można edytować plik, ale należy utworzyć projekt, aby rozpocząć przywracanie pakietu lub wywołać przywracanie w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="e595a-170">That said, you can certainly edit the file, but you must build the project to start a package restore or invoke restore in another way.</span></span> <span data-ttu-id="e595a-171">Zobacz [Przywracanie pakietu](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="e595a-171">See [Package restore](../consume-packages/package-restore.md).</span></span>


## <a name="projectlockjson"></a><span data-ttu-id="e595a-172">projekt.lock.json</span><span class="sxs-lookup"><span data-stu-id="e595a-172">project.lock.json</span></span>

<span data-ttu-id="e595a-173">Plik `project.lock.json` jest generowany w procesie przywracania pakietów NuGet `project.json`w projektach, które używają .</span><span class="sxs-lookup"><span data-stu-id="e595a-173">The `project.lock.json` file is generated in the process of restoring the NuGet packages in projects that use `project.json`.</span></span> <span data-ttu-id="e595a-174">Posiada migawkę wszystkich informacji, które są generowane jako NuGet spacery wykres pakietów i zawiera wersję, zawartość i zależności wszystkich pakietów w projekcie.</span><span class="sxs-lookup"><span data-stu-id="e595a-174">It holds a snapshot of all the information that is generated as NuGet walks the graph of packages and includes the version, contents, and dependencies of all the packages in your project.</span></span> <span data-ttu-id="e595a-175">System kompilacji używa tego, aby wybrać pakiety z lokalizacji globalnej, które są istotne podczas tworzenia projektu, a nie w zależności od folderu pakietów lokalnych w samym projekcie.</span><span class="sxs-lookup"><span data-stu-id="e595a-175">The build system uses this to choose packages from a global location that are relevant when building the project instead of depending on a local packages folder in the project itself.</span></span> <span data-ttu-id="e595a-176">Powoduje to szybszą wydajność kompilacji, ponieważ `project.lock.json` jest to `.nuspec` konieczne do odczytu tylko zamiast wielu oddzielnych plików.</span><span class="sxs-lookup"><span data-stu-id="e595a-176">This results in faster build performance because it's necessary to read only `project.lock.json` instead of many separate `.nuspec` files.</span></span>

<span data-ttu-id="e595a-177">`project.lock.json`jest generowany automatycznie przy przywracanie pakietu, więc można go pominąć w kontroli źródła, dodając go do `.gitignore` i `.tfignore` plików (zobacz [Pakiety i kontrola źródła](../consume-packages/packages-and-source-control.md).</span><span class="sxs-lookup"><span data-stu-id="e595a-177">`project.lock.json` is automatically generated on package restore, so it can be omitted from source control by adding it to `.gitignore` and `.tfignore` files (see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> <span data-ttu-id="e595a-178">Jednak jeśli uwzględnisz go w kontroli źródła, historia zmian pokazuje zmiany zależności rozwiązane w czasie.</span><span class="sxs-lookup"><span data-stu-id="e595a-178">However, if you include it in source control, the change history shows changes in dependencies resolved over time.</span></span>
