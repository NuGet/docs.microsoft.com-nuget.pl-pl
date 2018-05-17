---
title: Polecenie pakietu NuGet interfejsu wiersza polecenia
description: Informacje dotyczące polecenia pakiet nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a2468b099a822e69298ea78c80cfd1d5d5c09938
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="e8146-103">pack command, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="e8146-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="e8146-104">**Dotyczy:** pakietu tworzenia &bullet; **obsługiwane wersje:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="e8146-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="e8146-105">Tworzy oparte na określony pakiet NuGet `.nuspec` lub pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="e8146-105">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="e8146-106">`dotnet pack` Polecenia (zobacz [polecenia dotnet](dotnet-Commands.md)) i `msbuild /t:pack` (zobacz [docelowych elementów MSBuild](../reference/msbuild-targets.md)) może być używany jako alternatyw.</span><span class="sxs-lookup"><span data-stu-id="e8146-106">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../reference/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="e8146-107">W obszarze Mono Tworzenie pakietu z pliku projektu nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="e8146-107">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="e8146-108">Należy również dostosować innego niż lokalne ścieżki w `.nuspec` plików do ścieżek typu Unix, jak nuget.exe nie konwertuje nazwy ścieżek systemu Windows, sama.</span><span class="sxs-lookup"><span data-stu-id="e8146-108">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="e8146-109">Użycie</span><span class="sxs-lookup"><span data-stu-id="e8146-109">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="e8146-110">gdzie `<nuspecPath>` i `<projectPath>` określ `.nuspec` lub odpowiednio projektu pliku.</span><span class="sxs-lookup"><span data-stu-id="e8146-110">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="e8146-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="e8146-111">Options</span></span>

| <span data-ttu-id="e8146-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="e8146-112">Option</span></span> | <span data-ttu-id="e8146-113">Opis</span><span class="sxs-lookup"><span data-stu-id="e8146-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e8146-114">BasePath</span><span class="sxs-lookup"><span data-stu-id="e8146-114">BasePath</span></span> | <span data-ttu-id="e8146-115">Ustawia ścieżki podstawowej plików zdefiniowanych w `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="e8146-115">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="e8146-116">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="e8146-116">Build</span></span> | <span data-ttu-id="e8146-117">Określa, czy projekt powinien skompilowany przed zbudowaniem pakietu.</span><span class="sxs-lookup"><span data-stu-id="e8146-117">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="e8146-118">Wyklucz</span><span class="sxs-lookup"><span data-stu-id="e8146-118">Exclude</span></span> | <span data-ttu-id="e8146-119">Określa jeden lub więcej wzorców symboli wieloznacznych, które mają zostać wykluczone podczas tworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="e8146-119">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="e8146-120">Aby określić więcej niż jeden wzorzec, powtórz flagi - Exclude.</span><span class="sxs-lookup"><span data-stu-id="e8146-120">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="e8146-121">Zobacz poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="e8146-121">See example below.</span></span> |
| <span data-ttu-id="e8146-122">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="e8146-122">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="e8146-123">Uniemożliwia włączenie puste katalogi, podczas tworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="e8146-123">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="e8146-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e8146-124">ForceEnglishOutput</span></span> | <span data-ttu-id="e8146-125">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="e8146-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e8146-126">Pomoc</span><span class="sxs-lookup"><span data-stu-id="e8146-126">Help</span></span> | <span data-ttu-id="e8146-127">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="e8146-127">Displays help information for the command.</span></span> |
| <span data-ttu-id="e8146-128">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="e8146-128">IncludeReferencedProjects</span></span> | <span data-ttu-id="e8146-129">Wskazuje, że wbudowanych pakiet powinien zawierać przywoływane projekty jako zależności lub jako część pakietu.</span><span class="sxs-lookup"><span data-stu-id="e8146-129">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="e8146-130">Jeśli przywoływanego projektu ma odpowiadające mu `.nuspec` pliku, który ma taką samą nazwę jak projekt, do którego istnieje odwołanie projektu jest dodawana jako zależność.</span><span class="sxs-lookup"><span data-stu-id="e8146-130">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="e8146-131">W przeciwnym razie przywoływanego projektu jest dodawana jako część pakietu.</span><span class="sxs-lookup"><span data-stu-id="e8146-131">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="e8146-132">Element MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="e8146-132">MinClientVersion</span></span> | <span data-ttu-id="e8146-133">Ustaw *minClientVersion* atrybutu utworzonego pakietu.</span><span class="sxs-lookup"><span data-stu-id="e8146-133">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="e8146-134">Ta wartość zastępuje wartość istniejącej *minClientVersion* atrybutu (jeśli istnieją) w `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="e8146-134">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="e8146-135">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="e8146-135">MSBuildPath</span></span> | <span data-ttu-id="e8146-136">*(4.0 +)*  Określa ścieżkę MSBuild do użycia z poleceniem pierwszeństwo `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="e8146-136">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="e8146-137">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="e8146-137">MSBuildVersion</span></span> | <span data-ttu-id="e8146-138">*(3.2 +)*  Określa wersję programu MSBuild ma być używany z tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="e8146-138">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="e8146-139">Obsługiwane wartości to 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="e8146-139">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="e8146-140">Domyślnie jest wybierany MSBuild w ścieżce w przeciwnym razie domyślnie najwyższy zainstalowanej wersji programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="e8146-140">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="e8146-141">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="e8146-141">NoDefaultExcludes</span></span> | <span data-ttu-id="e8146-142">Zapobiega domyślne wykluczenie NuGet pakiet plików i pliki i foldery rozpoczynający się kropką, na przykład `.svn` i `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="e8146-142">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="e8146-143">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="e8146-143">NoPackageAnalysis</span></span> | <span data-ttu-id="e8146-144">Określa, że pakiet nie należy uruchamiać analizy pakietu po utworzeniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="e8146-144">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="e8146-145">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="e8146-145">OutputDirectory</span></span> | <span data-ttu-id="e8146-146">Określa folder, w którym przechowywany jest utworzony pakiet.</span><span class="sxs-lookup"><span data-stu-id="e8146-146">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="e8146-147">Jeśli folder nie jest określony, używany jest bieżący folder.</span><span class="sxs-lookup"><span data-stu-id="e8146-147">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="e8146-148">Właściwości</span><span class="sxs-lookup"><span data-stu-id="e8146-148">Properties</span></span> | <span data-ttu-id="e8146-149">Powinna zostać wyświetlona ostatniego wiersza polecenia po innych opcji.</span><span class="sxs-lookup"><span data-stu-id="e8146-149">Should appear last on the command line after other options.</span></span> <span data-ttu-id="e8146-150">Określa listę właściwości, które przesłaniają wartości w pliku projektu. zobacz [wspólne właściwości projektów MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) dla nazwy właściwości.</span><span class="sxs-lookup"><span data-stu-id="e8146-150">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="e8146-151">Argument właściwości w tym miejscu znajduje się lista tokenu = pary wartości, oddziel je średnikami, gdzie każde wystąpienie `$token$` w `.nuspec` pliku zostaną zastąpione podanej wartości.</span><span class="sxs-lookup"><span data-stu-id="e8146-151">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="e8146-152">Możliwe wartości ciągów w cudzysłowy.</span><span class="sxs-lookup"><span data-stu-id="e8146-152">Values can be strings in quotation marks.</span></span> <span data-ttu-id="e8146-153">Należy pamiętać, że dla właściwości "Konfiguracja", wartość domyślna to "Debug".</span><span class="sxs-lookup"><span data-stu-id="e8146-153">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="e8146-154">Aby zmienić konfigurację, wersji, należy użyć `-Properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="e8146-154">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="e8146-155">Suffix</span><span class="sxs-lookup"><span data-stu-id="e8146-155">Suffix</span></span> | <span data-ttu-id="e8146-156">*(3.4.4+)*  Dołącza sufiks z numerem wersji wewnętrznie generowane zwykle używany w przypadku dołączania kompilacji lub innych identyfikatorów w wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="e8146-156">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="e8146-157">Na przykład za pomocą `-suffix nightly` utworzy pakiet z podobne do numeru wersji `1.2.3-nightly`.</span><span class="sxs-lookup"><span data-stu-id="e8146-157">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="e8146-158">Sufiksy musi rozpoczynać się od litery, aby uniknąć potencjalnych niezgodności z różnymi wersjami programu NuGet i Menedżer pakietów NuGet, błędy i ostrzeżenia.</span><span class="sxs-lookup"><span data-stu-id="e8146-158">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="e8146-159">Symbole</span><span class="sxs-lookup"><span data-stu-id="e8146-159">Symbols</span></span> | <span data-ttu-id="e8146-160">Określa, że pakiet zawiera źródła i symbole.</span><span class="sxs-lookup"><span data-stu-id="e8146-160">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="e8146-161">W przypadku użycia z `.nuspec` pliku, tworzy zwykły plik pakietu NuGet i odpowiedniego pakietu symboli.</span><span class="sxs-lookup"><span data-stu-id="e8146-161">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="e8146-162">Narzędzie</span><span class="sxs-lookup"><span data-stu-id="e8146-162">Tool</span></span> | <span data-ttu-id="e8146-163">Określa, że pliki wyjściowe projektu powinna zostać umieszczona w `tool` folderu.</span><span class="sxs-lookup"><span data-stu-id="e8146-163">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="e8146-164">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="e8146-164">Verbosity</span></span> | <span data-ttu-id="e8146-165">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="e8146-165">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="e8146-166">Wersja</span><span class="sxs-lookup"><span data-stu-id="e8146-166">Version</span></span> | <span data-ttu-id="e8146-167">Zastępuje numer wersji z `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="e8146-167">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="e8146-168">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e8146-168">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="e8146-169">Z wyjątkiem programowanie zależności</span><span class="sxs-lookup"><span data-stu-id="e8146-169">Excluding development dependencies</span></span>

<span data-ttu-id="e8146-170">Niektóre pakiety NuGet są przydatne jako programowanie zależności, które ułatwiają tworzenie własnych biblioteki, ale niekoniecznie nie są wymagane jako zależności pakietów rzeczywiste.</span><span class="sxs-lookup"><span data-stu-id="e8146-170">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="e8146-171">`pack` Zignoruje polecenia `package` wpisów w `packages.config` zawierających `developmentDependency` ustawić atrybutu `true`.</span><span class="sxs-lookup"><span data-stu-id="e8146-171">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="e8146-172">Te wpisy nie będzie zawierał jako zależności w pakiecie utworzony.</span><span class="sxs-lookup"><span data-stu-id="e8146-172">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="e8146-173">Na przykład, należy wziąć pod uwagę następujące `packages.config` plik w projekcie źródła:</span><span class="sxs-lookup"><span data-stu-id="e8146-173">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="e8146-174">Dla tego projektu, pakiet utworzony przez `nuget pack` będzie zależy od `jQuery` i `microsoft-web-helpers` , ale nie `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="e8146-174">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="e8146-175">Przykłady</span><span class="sxs-lookup"><span data-stu-id="e8146-175">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
