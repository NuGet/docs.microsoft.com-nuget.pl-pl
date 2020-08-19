---
title: Pakiet interfejsu wiersza polecenia NuGet
description: Informacje dotyczące polecenia nuget.exe Pack
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0483a75c7ee1fd851f935f44d96a417e2e86bf20
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622957"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="e4e44-103">Pack — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="e4e44-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="e4e44-104">**Dotyczy:** &bullet; **obsługiwane wersje** tworzenia pakietów: 2.7 +</span><span class="sxs-lookup"><span data-stu-id="e4e44-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="e4e44-105">Tworzy pakiet NuGet na podstawie określonego pliku [. nuspec](../nuspec.md) lub projektu.</span><span class="sxs-lookup"><span data-stu-id="e4e44-105">Creates a NuGet package based on the specified [.nuspec](../nuspec.md) or project file.</span></span> <span data-ttu-id="e4e44-106">`dotnet pack`Polecenie (zobacz [polecenia dotnet](../dotnet-Commands.md)) i `msbuild -t:pack` (zobacz [elementy docelowe programu MSBuild](../msbuild-targets.md)) może być używane jako alternatywy.</span><span class="sxs-lookup"><span data-stu-id="e4e44-106">The `dotnet pack` command (see [dotnet Commands](../dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="e4e44-107">Użyj [`dotnet pack`](../dotnet-Commands.md) lub [`msbuild -t:pack`](../msbuild-targets.md) dla projektów opartych na [PackageReference](../../consume-packages/package-references-in-project-files.md) .</span><span class="sxs-lookup"><span data-stu-id="e4e44-107">Use [`dotnet pack`](../dotnet-Commands.md) or [`msbuild -t:pack`](../msbuild-targets.md) for [PackageReference](../../consume-packages/package-references-in-project-files.md) based projects.</span></span>
> <span data-ttu-id="e4e44-108">W obszarze mono Tworzenie pakietu z pliku projektu nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="e4e44-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="e4e44-109">Należy również dostosować ścieżki nielokalne w `.nuspec` pliku do ścieżek w stylu systemu UNIX, ponieważ nuget.exe nie konwertują samych nazw ścieżek systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="e4e44-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="e4e44-110">Użycie</span><span class="sxs-lookup"><span data-stu-id="e4e44-110">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="e4e44-111">gdzie `<nuspecPath>` i `<projectPath>` Określ `.nuspec` odpowiednio plik projektu lub.</span><span class="sxs-lookup"><span data-stu-id="e4e44-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="e4e44-112">Opcje</span><span class="sxs-lookup"><span data-stu-id="e4e44-112">Options</span></span>
- **`-BasePath`**

   <span data-ttu-id="e4e44-113">Ustawia ścieżkę podstawową plików zdefiniowanych w pliku [. nuspec](../nuspec.md) .</span><span class="sxs-lookup"><span data-stu-id="e4e44-113">Sets the base path of the files defined in the [.nuspec](../nuspec.md) file.</span></span>

- **`-Build`**

  <span data-ttu-id="e4e44-114">Określa, że projekt powinien zostać skompilowany przed skompilowaniem pakietu.</span><span class="sxs-lookup"><span data-stu-id="e4e44-114">Specifies that the project should be built before building the package.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="e4e44-115">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="e4e44-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e4e44-116">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="e4e44-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Exclude`**

  <span data-ttu-id="e4e44-117">Określa jeden lub więcej wzorców symboli wieloznacznych, które mają zostać wykluczone podczas tworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="e4e44-117">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="e4e44-118">Aby określić więcej niż jeden wzorzec, powtórz flagę-Exclude.</span><span class="sxs-lookup"><span data-stu-id="e4e44-118">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="e4e44-119">Zobacz przykład poniżej.</span><span class="sxs-lookup"><span data-stu-id="e4e44-119">See example below.</span></span>

- **`-ExcludeEmptyDirectories`**

  <span data-ttu-id="e4e44-120">Uniemożliwia dołączenie pustych katalogów podczas kompilowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="e4e44-120">Prevents inclusion of empty directories when building the package.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="e4e44-121">*(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.</span><span class="sxs-lookup"><span data-stu-id="e4e44-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="e4e44-122">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="e4e44-122">Displays help information for the command.</span></span>

- **`-IncludeReferencedProjects`**

  <span data-ttu-id="e4e44-123">Wskazuje, że skompilowany pakiet powinien zawierać przywoływane projekty jako zależności lub jako część pakietu.</span><span class="sxs-lookup"><span data-stu-id="e4e44-123">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="e4e44-124">Jeśli projekt, do którego istnieje odwołanie `.nuspec` , ma odpowiedni plik, który ma taką samą nazwę jak projekt, ten, do którego odwołuje się projekt, jest dodawany jako zależność.</span><span class="sxs-lookup"><span data-stu-id="e4e44-124">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="e4e44-125">W przeciwnym razie przywoływany projekt zostanie dodany jako część pakietu.</span><span class="sxs-lookup"><span data-stu-id="e4e44-125">Otherwise, the referenced project is added as part of the package.</span></span>

- **`-InstallPackageToOutputPath`**

  <span data-ttu-id="e4e44-126">Określ, czy polecenie ma przygotować katalog wyjściowy pakietu, aby obsługiwał udział jako źródło danych.</span><span class="sxs-lookup"><span data-stu-id="e4e44-126">Specify if the command should prepare the package output directory to support share as feed.</span></span>

- **`-MinClientVersion`**

  <span data-ttu-id="e4e44-127">Ustaw atrybut *minClientVersion* dla utworzonego pakietu.</span><span class="sxs-lookup"><span data-stu-id="e4e44-127">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="e4e44-128">Ta wartość spowoduje przesłonięcie wartości istniejącego atrybutu *minClientVersion* (jeśli istnieje) w `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="e4e44-128">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="e4e44-129">*(4.0 +)* Określa ścieżkę programu MSBuild do użycia z poleceniem, które ma pierwszeństwo przed `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="e4e44-129">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="e4e44-130">*(3.2 +)* Określa wersję programu MSBuild, która ma być używana z tym poleceniem.</span><span class="sxs-lookup"><span data-stu-id="e4e44-130">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="e4e44-131">Obsługiwane wartości to 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="e4e44-131">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="e4e44-132">Domyślnie program MSBuild w ścieżce jest wybierany, w przeciwnym razie domyślnie jest to najwyższa zainstalowana wersja programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="e4e44-132">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NoDefaultExcludes`**

  <span data-ttu-id="e4e44-133">Zapobiega domyślnemu wykluczeniu plików pakietów NuGet oraz plików i folderów rozpoczynających się od kropki, takich jak `.svn` i `.gitignore` .</span><span class="sxs-lookup"><span data-stu-id="e4e44-133">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="e4e44-134">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e4e44-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-NoPackageAnalysis`**

  <span data-ttu-id="e4e44-135">Określa, że pakiet nie powinien uruchamiać analizy pakietu po skompilowaniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="e4e44-135">Specifies that pack should not run package analysis after building the package.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="e4e44-136">Określa folder, w którym jest przechowywany utworzony pakiet.</span><span class="sxs-lookup"><span data-stu-id="e4e44-136">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="e4e44-137">Jeśli folder nie zostanie określony, używany jest bieżący folder.</span><span class="sxs-lookup"><span data-stu-id="e4e44-137">If no folder is specified, the current folder is used.</span></span>

- **`-OutputFileNamesWithoutVersion`**

  <span data-ttu-id="e4e44-138">Określ, czy polecenie ma przygotować nazwę wyjściową pakietu bez wersji.</span><span class="sxs-lookup"><span data-stu-id="e4e44-138">Specify if the command should prepare the package output name without the version.</span></span>

- **`-PackagesDirectory`**

  <span data-ttu-id="e4e44-139">Określa folder Packages.</span><span class="sxs-lookup"><span data-stu-id="e4e44-139">Specifies the packages folder.</span></span>

- **`-p|-Properties`**

  <span data-ttu-id="e4e44-140">Powinna zostać wyświetlona jako Ostatnia w wierszu polecenia po innych opcjach.</span><span class="sxs-lookup"><span data-stu-id="e4e44-140">Should appear last on the command line after other options.</span></span> <span data-ttu-id="e4e44-141">Określa listę właściwości, które zastępują wartości w pliku projektu; Zobacz [wspólne właściwości projektu MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) dla nazw właściwości.</span><span class="sxs-lookup"><span data-stu-id="e4e44-141">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="e4e44-142">Argument właściwości znajduje się na liście par token = wartość, oddzielonych średnikami, gdzie każde wystąpienie `$token$` w `.nuspec` pliku zostanie zastąpione daną wartością.</span><span class="sxs-lookup"><span data-stu-id="e4e44-142">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="e4e44-143">Wartości mogą być ciągami w cudzysłowie.</span><span class="sxs-lookup"><span data-stu-id="e4e44-143">Values can be strings in quotation marks.</span></span> <span data-ttu-id="e4e44-144">Należy pamiętać, że w przypadku właściwości "Configuration" wartością domyślną jest "debug".</span><span class="sxs-lookup"><span data-stu-id="e4e44-144">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="e4e44-145">Aby zmienić konfigurację wydania, użyj programu `-Properties Configuration=Release` .</span><span class="sxs-lookup"><span data-stu-id="e4e44-145">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> <span data-ttu-id="e4e44-146">**Ogólnie rzecz**biorąc, właściwości powinny być takie same, które były używane podczas odpowiedniej kompilacji projektu, aby uniknąć potencjalnie nietypowego zachowania.</span><span class="sxs-lookup"><span data-stu-id="e4e44-146">**In general**, Properties should be the same that were used during the corresponding project build, in order to avoid potentially strange behavior.</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="e4e44-147">Określa katalog rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="e4e44-147">Specifies the solution directory.</span></span>

- **`-Suffix`**

  <span data-ttu-id="e4e44-148">*(3.4.4 +)* Dołącza sufiks do wewnętrznie wygenerowanego numeru wersji, zazwyczaj używany do dołączania kompilacji lub innych identyfikatorów w wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="e4e44-148">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="e4e44-149">Na przykład za pomocą `-suffix nightly` program utworzy pakiet z numerem wersji podobnym do `1.2.3-nightly` .</span><span class="sxs-lookup"><span data-stu-id="e4e44-149">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="e4e44-150">Sufiksy muszą zaczynać się literą, aby uniknąć ostrzeżeń, błędów i potencjalnych niezgodności z różnymi wersjami programu NuGet i Menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="e4e44-150">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span>

- **`-SymbolPackageFormat`**

  <span data-ttu-id="e4e44-151">Podczas tworzenia pakietu symboli, umożliwia wybór między `snupkg` `symbols.nupkg` formatem a.</span><span class="sxs-lookup"><span data-stu-id="e4e44-151">When creating a symbols package, allows to choose between the `snupkg` and `symbols.nupkg` format.</span></span>

- **`-Symbols`**

  <span data-ttu-id="e4e44-152">Określa, że pakiet zawiera źródła i symbole.</span><span class="sxs-lookup"><span data-stu-id="e4e44-152">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="e4e44-153">W przypadku użycia z `.nuspec` plikiem tworzony jest zwykły plik pakietu NuGet i odpowiedni pakiet symboli.</span><span class="sxs-lookup"><span data-stu-id="e4e44-153">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="e4e44-154">Domyślnie tworzy on [starszy pakiet symboli](../../create-packages/Symbol-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="e4e44-154">By default it creates a [legacy symbol package](../../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="e4e44-155">Nowy zalecany format pakietów symboli to. snupkg.</span><span class="sxs-lookup"><span data-stu-id="e4e44-155">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="e4e44-156">Zobacz [Tworzenie pakietów symboli (. snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="e4e44-156">See [Creating symbol packages (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span></span>

- **`-Tool`**

   <span data-ttu-id="e4e44-157">Określa, że pliki wyjściowe projektu powinny zostać umieszczone w `tool` folderze.</span><span class="sxs-lookup"><span data-stu-id="e4e44-157">Specifies that the output files of the project should be placed in the `tool` folder.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="e4e44-158">Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .</span><span class="sxs-lookup"><span data-stu-id="e4e44-158">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="e4e44-159">Zastępuje numer wersji z `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="e4e44-159">Overrides the version number from the `.nuspec` file.</span></span>

<span data-ttu-id="e4e44-160">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e4e44-160">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="e4e44-161">Wykluczanie zależności programistycznych</span><span class="sxs-lookup"><span data-stu-id="e4e44-161">Excluding development dependencies</span></span>

<span data-ttu-id="e4e44-162">Niektóre pakiety NuGet są przydatne jako zależności programistyczne, które ułatwiają tworzenie własnych bibliotek, ale nie muszą być potrzebne jako rzeczywiste zależności pakietów.</span><span class="sxs-lookup"><span data-stu-id="e4e44-162">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="e4e44-163">`pack`Polecenie zignoruje `package` wpisy w `packages.config` , które mają `developmentDependency` atrybut ustawiony na `true` .</span><span class="sxs-lookup"><span data-stu-id="e4e44-163">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="e4e44-164">Te wpisy nie zostaną uwzględnione jako zależności w utworzonym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="e4e44-164">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="e4e44-165">Rozważmy na przykład następujący `packages.config` plik w projekcie źródłowym:</span><span class="sxs-lookup"><span data-stu-id="e4e44-165">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="e4e44-166">Dla tego projektu pakiet utworzony przez ma `nuget pack` zależność od elementu `jQuery` , `microsoft-web-helpers` ale nie `netfx-Guard` .</span><span class="sxs-lookup"><span data-stu-id="e4e44-166">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="suppressing-pack-warnings"></a><span data-ttu-id="e4e44-167">Pomijanie ostrzeżeń pakietu</span><span class="sxs-lookup"><span data-stu-id="e4e44-167">Suppressing pack warnings</span></span>

<span data-ttu-id="e4e44-168">Mimo że zaleca się rozwiązanie wszystkich ostrzeżeń NuGet podczas operacji pakietu, w niektórych sytuacjach pomijanie ich jest uzasadnione.</span><span class="sxs-lookup"><span data-stu-id="e4e44-168">While it is recommended that you resolve all NuGet warnings during your pack operations, in certain situations suppressing them is warranted.</span></span>

<span data-ttu-id="e4e44-169">Można to osiągnąć w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e4e44-169">You can achieve that in the following way:</span></span> 

> <span data-ttu-id="e4e44-170">Pakiet nuget.exe Pack nuspec-Properties nowarn = NU5104</span><span class="sxs-lookup"><span data-stu-id="e4e44-170">nuget.exe pack package.nuspec -Properties NoWarn=NU5104</span></span>

## <a name="examples"></a><span data-ttu-id="e4e44-171">Przykłady</span><span class="sxs-lookup"><span data-stu-id="e4e44-171">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
