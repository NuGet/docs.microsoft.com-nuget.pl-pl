---
title: Odwołanie do pliku Project.JSON do NuGet
description: W niektórych typach projektów project.json przechowuje listę pakietów NuGet, używany w projekcie.
author: karann-msft
ms.author: karann
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: e4d8b5b9ab4605516827ead8939f278d110c7a48
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547787"
---
# <a name="projectjson-reference"></a><span data-ttu-id="ff950-103">Odwołanie do pliku Project.JSON</span><span class="sxs-lookup"><span data-stu-id="ff950-103">project.json reference</span></span>

<span data-ttu-id="ff950-104">*NuGet 3.x+*</span><span class="sxs-lookup"><span data-stu-id="ff950-104">*NuGet 3.x+*</span></span>

<span data-ttu-id="ff950-105">`project.json` Pliku prowadzi listę pakietów używanych w projekcie, znane jako format pakietu zarządzania.</span><span class="sxs-lookup"><span data-stu-id="ff950-105">The `project.json` file maintains a list of packages used in a project, known as a package management format.</span></span> <span data-ttu-id="ff950-106">Zastępuje ona `packages.config` , ale są kolejno zastępowane [PackageReference](../consume-packages/package-references-in-project-files.md) nuget 4.0 +.</span><span class="sxs-lookup"><span data-stu-id="ff950-106">It supersedes `packages.config` but is in turn superseded by [PackageReference](../consume-packages/package-references-in-project-files.md) with NuGet 4.0+.</span></span>

<span data-ttu-id="ff950-107">[ `project.lock.json` ](#projectlockjson) Pliku (opisanych poniżej) jest również używane w projektach wykorzystujących `project.json`.</span><span class="sxs-lookup"><span data-stu-id="ff950-107">The [`project.lock.json`](#projectlockjson) file (described below) is also used in projects employing `project.json`.</span></span>

<span data-ttu-id="ff950-108">`project.json` ma podstawowe następującą strukturę, w którym każdy z czterech obiektów najwyższego poziomu może mieć dowolną liczbę obiektów podrzędnych:</span><span class="sxs-lookup"><span data-stu-id="ff950-108">`project.json` has the following basic structure, where each of the four top-level objects can have any number of child objects:</span></span>

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

## <a name="dependencies"></a><span data-ttu-id="ff950-109">Zależności</span><span class="sxs-lookup"><span data-stu-id="ff950-109">Dependencies</span></span>

<span data-ttu-id="ff950-110">Zawiera listę zależności pakietów NuGet projektu w następującej postaci:</span><span class="sxs-lookup"><span data-stu-id="ff950-110">Lists the NuGet package dependencies of your project in the following form:</span></span>

```json
"PackageID" : "version_constraint"
```

<span data-ttu-id="ff950-111">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="ff950-111">For example:</span></span>

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

<span data-ttu-id="ff950-112">`dependencies` Sekcja jest, gdy okno Menedżera pakietów NuGet dodaje zależności pakietów do projektu.</span><span class="sxs-lookup"><span data-stu-id="ff950-112">The `dependencies` section is where the NuGet Package Manager dialog adds package dependencies to your project.</span></span>

<span data-ttu-id="ff950-113">Identyfikator pakietu odnosi się do identyfikatora pakietu w witrynie nuget.org, taki sam jak identyfikator używany w konsoli Menedżera pakietów: `Install-Package Microsoft.NETCore`.</span><span class="sxs-lookup"><span data-stu-id="ff950-113">The Package id corresponds to the id of the package on nuget.org , the same as the id used in the package manager console: `Install-Package Microsoft.NETCore`.</span></span>

<span data-ttu-id="ff950-114">Podczas przywracania pakietów, ograniczenie wersji `"5.0.0"` oznacza `>= 5.0.0`.</span><span class="sxs-lookup"><span data-stu-id="ff950-114">When restoring packages, the version constraint of `"5.0.0"` implies `>= 5.0.0`.</span></span> <span data-ttu-id="ff950-115">Oznacza to jeśli 5.0.0 nie jest dostępny na serwerze, ale jest 5.0.1, NuGet instaluje 5.0.1 i ostrzega o uaktualnieniu.</span><span class="sxs-lookup"><span data-stu-id="ff950-115">That is, if 5.0.0 is not available on the server but 5.0.1 is, NuGet installs  5.0.1 and warns you about the upgrade.</span></span> <span data-ttu-id="ff950-116">NuGet, w przeciwnym razie wybiera najniższa możliwa wersja na serwerze, pasujących do ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="ff950-116">NuGet otherwise picks the lowest possible version on the server matching the constraint.</span></span>

<span data-ttu-id="ff950-117">Zobacz [rozpoznawania zależności](../consume-packages/dependency-resolution.md) więcej informacji na temat reguł rozwiązywania.</span><span class="sxs-lookup"><span data-stu-id="ff950-117">See [Dependency resolution](../consume-packages/dependency-resolution.md) for more details on resolution rules.</span></span>

### <a name="managing-dependency-assets"></a><span data-ttu-id="ff950-118">Zarządzanie zasobami zależności</span><span class="sxs-lookup"><span data-stu-id="ff950-118">Managing dependency assets</span></span>

<span data-ttu-id="ff950-119">Które zasoby z zależnościami przepływać do najwyższego poziomu projektu jest kontrolowany przez określenie zestawu rozdzielonych przecinkami tagów w `include` i `exclude` właściwości odwołania zależności.</span><span class="sxs-lookup"><span data-stu-id="ff950-119">Which assets from dependencies flow into the top-level project is controlled by specifying a comma-delimited set of tags in the `include` and `exclude` properties of the dependency reference.</span></span> <span data-ttu-id="ff950-120">Tagi są wymienione w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="ff950-120">The tags are listed the table below:</span></span>

| <span data-ttu-id="ff950-121">Uwzględnianie/wykluczanie znaczników</span><span class="sxs-lookup"><span data-stu-id="ff950-121">Include/Exclude tag</span></span> | <span data-ttu-id="ff950-122">Odpowiednie foldery elementu docelowego</span><span class="sxs-lookup"><span data-stu-id="ff950-122">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="ff950-123">Pliki</span><span class="sxs-lookup"><span data-stu-id="ff950-123">contentFiles</span></span> | <span data-ttu-id="ff950-124">Zawartość</span><span class="sxs-lookup"><span data-stu-id="ff950-124">Content</span></span>  |
| <span data-ttu-id="ff950-125">środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="ff950-125">runtime</span></span> | <span data-ttu-id="ff950-126">Środowisko uruchomieniowe, zasobów i FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="ff950-126">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="ff950-127">Kompilacji</span><span class="sxs-lookup"><span data-stu-id="ff950-127">compile</span></span> | <span data-ttu-id="ff950-128">lib</span><span class="sxs-lookup"><span data-stu-id="ff950-128">lib</span></span> |
| <span data-ttu-id="ff950-129">kompilacja</span><span class="sxs-lookup"><span data-stu-id="ff950-129">build</span></span> | <span data-ttu-id="ff950-130">Kompilacja (cele i właściwości programu MSBuild)</span><span class="sxs-lookup"><span data-stu-id="ff950-130">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="ff950-131">natywne</span><span class="sxs-lookup"><span data-stu-id="ff950-131">native</span></span> | <span data-ttu-id="ff950-132">natywne</span><span class="sxs-lookup"><span data-stu-id="ff950-132">native</span></span> |
| <span data-ttu-id="ff950-133">brak</span><span class="sxs-lookup"><span data-stu-id="ff950-133">none</span></span> | <span data-ttu-id="ff950-134">Brak folderów</span><span class="sxs-lookup"><span data-stu-id="ff950-134">No folders</span></span> |
| <span data-ttu-id="ff950-135">wszystkie</span><span class="sxs-lookup"><span data-stu-id="ff950-135">all</span></span> | <span data-ttu-id="ff950-136">Wszystkie foldery</span><span class="sxs-lookup"><span data-stu-id="ff950-136">All folders</span></span> |

<span data-ttu-id="ff950-137">Określony za pomocą tagów `exclude` pierwszeństwo określony za pomocą `include`.</span><span class="sxs-lookup"><span data-stu-id="ff950-137">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="ff950-138">Na przykład `include="runtime, compile" exclude="compile"` jest taka sama jak `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="ff950-138">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span>

<span data-ttu-id="ff950-139">Na przykład w celu uwzględnienia `build` i `native` folderów zależność, należy użyć następującego:</span><span class="sxs-lookup"><span data-stu-id="ff950-139">For example, to include the `build` and `native` folders of a dependency, use the following:</span></span>

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

<span data-ttu-id="ff950-140">Aby wykluczyć `content` i `build` folderów zależność, należy użyć następującego:</span><span class="sxs-lookup"><span data-stu-id="ff950-140">To exclude the `content` and `build` folders of a dependency, use the following:</span></span>

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

## <a name="frameworks"></a><span data-ttu-id="ff950-141">Struktury</span><span class="sxs-lookup"><span data-stu-id="ff950-141">Frameworks</span></span>

<span data-ttu-id="ff950-142">Wyświetla listę struktur, w których działa projektu, taki jak `net45`, `netcoreapp`, `netstandard`.</span><span class="sxs-lookup"><span data-stu-id="ff950-142">Lists the frameworks that the project runs on, such as `net45`, `netcoreapp`, `netstandard`.</span></span>

```json
"frameworks": {
    "netcore50": {}
    }
 ```

<span data-ttu-id="ff950-143">Tylko pojedynczy wpis jest dozwolona w `frameworks` sekcji.</span><span class="sxs-lookup"><span data-stu-id="ff950-143">Only a single entry is allowed in the `frameworks` section.</span></span> <span data-ttu-id="ff950-144">(Wyjątek stanowi `project.json` plików dla projektów programu ASP.NET, które są kompilowane przy użyciu środowiska DNX przestarzałe narzędzie łańcucha, który pozwala na wiele obiektów docelowych.)</span><span class="sxs-lookup"><span data-stu-id="ff950-144">(An exception is `project.json` files for ASP.NET projects that are build with deprecated DNX tool chain, which allows for multiple targets.)</span></span>

## <a name="runtimes"></a><span data-ttu-id="ff950-145">środowiska uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="ff950-145">Runtimes</span></span>

<span data-ttu-id="ff950-146">Zawiera listę systemów operacyjnych i architektur, które aplikacja działa w systemie, takie jak `win10-arm`, `win8-x64`, `win8-x86`.</span><span class="sxs-lookup"><span data-stu-id="ff950-146">Lists the operating systems and architectures that your app runs on, such as `win10-arm`, `win8-x64`, `win8-x86`.</span></span>

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

<span data-ttu-id="ff950-147">Pakiet zawierający wersję PCL, która może działać na dowolnym środowiska uruchomieniowego nie należy określić środowisko uruchomieniowe.</span><span class="sxs-lookup"><span data-stu-id="ff950-147">A package containing a PCL that can run on any runtime doesn't need to specify a runtime.</span></span> <span data-ttu-id="ff950-148">Musi to być również wartość true, wszystkie zależności, w przeciwnym razie należy określić środowisk uruchomieniowych.</span><span class="sxs-lookup"><span data-stu-id="ff950-148">This must also be true of any dependencies, otherwise you must specify runtimes.</span></span>


## <a name="supports"></a><span data-ttu-id="ff950-149">Obsługuje</span><span class="sxs-lookup"><span data-stu-id="ff950-149">Supports</span></span>

<span data-ttu-id="ff950-150">Definiuje zestaw sprawdza, czy zależności pakietów.</span><span class="sxs-lookup"><span data-stu-id="ff950-150">Defines a set of checks for package dependencies.</span></span> <span data-ttu-id="ff950-151">Można zdefiniować, którego można spodziewać się PCL lub aplikacja była uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="ff950-151">You can define where you expect the PCL or app to run.</span></span> <span data-ttu-id="ff950-152">Definicje są restrykcyjna, jak Twój kod może być mogą być uruchamiane w innym miejscu.</span><span class="sxs-lookup"><span data-stu-id="ff950-152">The definitions are not restrictive, as your code may be able to run elsewhere.</span></span> <span data-ttu-id="ff950-153">Ale określenie tych sprawdzeń sprawia, że NuGet, sprawdź, czy wszystkie zależności na liście TxMs.</span><span class="sxs-lookup"><span data-stu-id="ff950-153">But specifying these checks makes NuGet check that all dependencies are satisfied on the listed TxMs.</span></span> <span data-ttu-id="ff950-154">Przykładowe wartości do tego są: `net46.app`, `uwp.10.0.app`itp.</span><span class="sxs-lookup"><span data-stu-id="ff950-154">Examples of the values for this are: `net46.app`, `uwp.10.0.app`, etc.</span></span>

<span data-ttu-id="ff950-155">W tej sekcji powinno zostać automatycznie wypełnione, po wybraniu wpisu w oknie dialogowym cele Portable Class Library.</span><span class="sxs-lookup"><span data-stu-id="ff950-155">This section should be populated automatically when you select an entry in the Portable Class Library targets dialog.</span></span>

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a><span data-ttu-id="ff950-156">Importy</span><span class="sxs-lookup"><span data-stu-id="ff950-156">Imports</span></span>

<span data-ttu-id="ff950-157">Importy pozwalają pakiety, które używają `dotnet` TxM do pracy z pakietami, które nie deklarują dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="ff950-157">Imports are designed to allow packages that use the `dotnet` TxM to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="ff950-158">Jeśli w twoim projekcie są używani `dotnet` TxM, a następnie wszystkich pakietów, na których polegasz musi również mieć `dotnet` TxM, chyba że dodasz następujące polecenie, aby Twoje `project.json` umożliwia bez `dotnet` platform, aby był zgodny z `dotnet`:</span><span class="sxs-lookup"><span data-stu-id="ff950-158">If your project is using the `dotnet` TxM then all the packages you depend on must also have a `dotnet` TxM, unless you add the following to your `project.json` to allow non `dotnet` platforms to be compatible with `dotnet`:</span></span>

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

<span data-ttu-id="ff950-159">Jeśli używasz `dotnet` TxM następnie system projektu PCL dodaje odpowiednie `imports` oświadczenie na podstawie obsługiwanych celów.</span><span class="sxs-lookup"><span data-stu-id="ff950-159">If you are using the `dotnet` TxM then the PCL project system adds the appropriate `imports` statement based on the supported targets.</span></span>

## <a name="differences-from-portable-apps-and-web-projects"></a><span data-ttu-id="ff950-160">Różnice z przenośnym aplikacje oraz projekty sieci web</span><span class="sxs-lookup"><span data-stu-id="ff950-160">Differences from portable apps and web projects</span></span>

<span data-ttu-id="ff950-161">`project.json` Plik używany przez NuGet jest podzbiorem wykrytym w projektach ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="ff950-161">The `project.json` file used by NuGet is a subset of that found in ASP.NET Core projects.</span></span> <span data-ttu-id="ff950-162">W programie ASP.NET Core `project.json` służy do metadanych projektu, informacje o kompilacji i zależności.</span><span class="sxs-lookup"><span data-stu-id="ff950-162">In ASP.NET Core `project.json` is used for project metadata, compilation information, and dependencies.</span></span> <span data-ttu-id="ff950-163">Gdy jest używana w innych systemach projektu, te trzy elementy są podzielone na osobne pliki i `project.json` zawiera mniej informacji.</span><span class="sxs-lookup"><span data-stu-id="ff950-163">When used in other project systems, those three things are split into separate files and `project.json` contains less information.</span></span> <span data-ttu-id="ff950-164">Istotne różnice obejmują:</span><span class="sxs-lookup"><span data-stu-id="ff950-164">Notable differences include:</span></span>

- <span data-ttu-id="ff950-165">Może istnieć tylko jeden struktura w systemie `frameworks` sekcji.</span><span class="sxs-lookup"><span data-stu-id="ff950-165">There can only be one framework in the `frameworks` section.</span></span>

- <span data-ttu-id="ff950-166">Plik nie może zawierać zależności, opcji kompilacji, itp., widoczny w środowiska DNX `project.json` plików.</span><span class="sxs-lookup"><span data-stu-id="ff950-166">The file cannot contain dependencies, compilation options, etc. that you see in DNX `project.json` files.</span></span> <span data-ttu-id="ff950-167">Biorąc pod uwagę, że może istnieć tylko jedną strukturę nie ma sensu wprowadzenia zależności określonej platformy.</span><span class="sxs-lookup"><span data-stu-id="ff950-167">Given that there can only be a single framework it doesn't make sense to enter framework-specific dependencies.</span></span>

- <span data-ttu-id="ff950-168">Kompilacja jest obsługiwany przez program MSBuild, więc definiuje opcje kompilacji preprocesora, itp. są częścią pliku projektu MSBuild i nie `project.json`.</span><span class="sxs-lookup"><span data-stu-id="ff950-168">Compilation is handled by MSBuild so compilation options, preprocessor defines, etc. are all part of the MSBuild project file and not `project.json`.</span></span>

<span data-ttu-id="ff950-169">W pakiecie NuGet 3 +, deweloperzy najprawdopodobniej nie ręcznie edytować `project.json`, ponieważ interfejs użytkownika Menedżera pakietów w programie Visual Studio obsługuje zawartość.</span><span class="sxs-lookup"><span data-stu-id="ff950-169">In NuGet 3+, developers are not expected to manually edit the `project.json`, as the Package Manager UI in Visual Studio manipulates the content.</span></span> <span data-ttu-id="ff950-170">Inaczej mówiąc, plik pewno można edytować, ale należy utworzyć projekt, aby rozpocząć przywracanie pakietu lub wywołaj przywracania w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="ff950-170">That said, you can certainly edit the file, but you must build the project to start a package restore or invoke restore in another way.</span></span> <span data-ttu-id="ff950-171">Zobacz [Przywracanie pakietu](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="ff950-171">See [Package restore](../consume-packages/package-restore.md).</span></span>


## <a name="projectlockjson"></a><span data-ttu-id="ff950-172">project.lock.json</span><span class="sxs-lookup"><span data-stu-id="ff950-172">project.lock.json</span></span>

<span data-ttu-id="ff950-173">`project.lock.json` Plik jest generowany w trakcie przywracania pakietów NuGet w projektach korzystających z `project.json`.</span><span class="sxs-lookup"><span data-stu-id="ff950-173">The `project.lock.json` file is generated in the process of restoring the NuGet packages in projects that use `project.json`.</span></span> <span data-ttu-id="ff950-174">Przechowuje migawki wszystkie informacje, które są generowane zgodnie z narzędzi przedstawia wykres pakietów NuGet i zawiera wersję, zawartość i zależności dla wszystkich pakietów w projekcie.</span><span class="sxs-lookup"><span data-stu-id="ff950-174">It holds a snapshot of all the information that is generated as NuGet walks the graph of packages and includes the version, contents, and dependencies of all the packages in your project.</span></span> <span data-ttu-id="ff950-175">System kompilacji używa tej wartości do wyboru pakietów globalnej lokalizacji, które mają zastosowanie podczas kompilowania projektu, a nie w zależności od folderem lokalnym pakietów w samym projekcie.</span><span class="sxs-lookup"><span data-stu-id="ff950-175">The build system uses this to choose packages from a global location that are relevant when building the project instead of depending on a local packages folder in the project itself.</span></span> <span data-ttu-id="ff950-176">Skutkuje to zwiększyć wydajność kompilacji ponieważ tylko do odczytu `project.lock.json` zamiast wiele oddzielnych `.nuspec` plików.</span><span class="sxs-lookup"><span data-stu-id="ff950-176">This results in faster build performance because it's necessary to read only `project.lock.json` instead of many separate `.nuspec` files.</span></span>

<span data-ttu-id="ff950-177">`project.lock.json` jest generowany automatycznie na Przywracanie pakietu, dzięki czemu może być pominięty z kontroli źródła, dodając ją do `.gitignore` i `.tfignore` plików (zobacz [pakiety i kontrola źródła](../consume-packages/packages-and-source-control.md).</span><span class="sxs-lookup"><span data-stu-id="ff950-177">`project.lock.json` is automatically generated on package restore, so it can be omitted from source control by adding it to `.gitignore` and `.tfignore` files (see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> <span data-ttu-id="ff950-178">Jednak jeśli uwzględniony w kontroli źródła, historię zmian przedstawia zmiany w zależnościach rozwiązane wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="ff950-178">However, if you include it in source control, the change history shows changes in dependencies resolved over time.</span></span>
