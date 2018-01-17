---
title: Polecenie pakietu NuGet interfejsu wiersza polecenia | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 55e9e4d2-8039-4e9b-bdd9-c8b3eb0e894b
description: "Informacje dotyczące polecenia pakiet nuget.exe"
keywords: "Odwołanie do pakietu nuget, polecenie pakietu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0dbecb8f01acf781ab8d2e77e8df7fa405f74cf1
ms.sourcegitcommit: d576d84fb4b6a178eb2ac11f55deb08ac771ba1c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/16/2018
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="1ef46-104">polecenie pakietu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="1ef46-104">pack command (NuGet CLI)</span></span>

<span data-ttu-id="1ef46-105">**Dotyczy:** pakietu tworzenia &bullet; **obsługiwane wersje:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="1ef46-105">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="1ef46-106">Tworzy oparte na określony pakiet NuGet `.nuspec` lub pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="1ef46-106">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="1ef46-107">`dotnet pack` Polecenia (zobacz [polecenia dotnet](dotnet-Commands.md)) i `msbuild /t:pack` (zobacz [docelowych elementów MSBuild](../schema/msbuild-targets.md)) może być używany jako alternatyw.</span><span class="sxs-lookup"><span data-stu-id="1ef46-107">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../schema/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="1ef46-108">W obszarze Mono Tworzenie pakietu z pliku projektu nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="1ef46-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="1ef46-109">Należy również dostosować innego niż lokalne ścieżki w `.nuspec` plików do ścieżek typu Unix, jak nuget.exe nie konwertuje nazwy ścieżek systemu Windows, sama.</span><span class="sxs-lookup"><span data-stu-id="1ef46-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="1ef46-110">Użycie</span><span class="sxs-lookup"><span data-stu-id="1ef46-110">Usage</span></span>

```
nuget pack <nuspecPath | projectPath> [options]
```

<span data-ttu-id="1ef46-111">gdzie `<nuspecPath>` i `<projectPath>` określ `.nuspec` lub odpowiednio projektu pliku.</span><span class="sxs-lookup"><span data-stu-id="1ef46-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="1ef46-112">Opcje</span><span class="sxs-lookup"><span data-stu-id="1ef46-112">Options</span></span>

| <span data-ttu-id="1ef46-113">Opcja</span><span class="sxs-lookup"><span data-stu-id="1ef46-113">Option</span></span> | <span data-ttu-id="1ef46-114">Opis</span><span class="sxs-lookup"><span data-stu-id="1ef46-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1ef46-115">BasePath</span><span class="sxs-lookup"><span data-stu-id="1ef46-115">BasePath</span></span> | <span data-ttu-id="1ef46-116">Ustawia ścieżki podstawowej plików zdefiniowanych w `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="1ef46-116">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="1ef46-117">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="1ef46-117">Build</span></span> | <span data-ttu-id="1ef46-118">Określa, czy projekt powinien skompilowany przed zbudowaniem pakietu.</span><span class="sxs-lookup"><span data-stu-id="1ef46-118">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="1ef46-119">Wyklucz</span><span class="sxs-lookup"><span data-stu-id="1ef46-119">Exclude</span></span> | <span data-ttu-id="1ef46-120">Określa jeden lub więcej wzorców symboli wieloznacznych, które mają zostać wykluczone podczas tworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="1ef46-120">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="1ef46-121">Aby określić więcej niż jeden wzorzec, powtórz flagi - Exclude.</span><span class="sxs-lookup"><span data-stu-id="1ef46-121">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="1ef46-122">Zobacz poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="1ef46-122">See example below.</span></span> |
| <span data-ttu-id="1ef46-123">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="1ef46-123">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="1ef46-124">Uniemożliwia włączenie puste katalogi, podczas tworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="1ef46-124">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="1ef46-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1ef46-125">ForceEnglishOutput</span></span> | <span data-ttu-id="1ef46-126">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="1ef46-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1ef46-127">Pomoc</span><span class="sxs-lookup"><span data-stu-id="1ef46-127">Help</span></span> | <span data-ttu-id="1ef46-128">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="1ef46-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="1ef46-129">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="1ef46-129">IncludeReferencedProjects</span></span> | <span data-ttu-id="1ef46-130">Wskazuje, że wbudowanych pakiet powinien zawierać przywoływane projekty jako zależności lub jako część pakietu.</span><span class="sxs-lookup"><span data-stu-id="1ef46-130">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="1ef46-131">Jeśli przywoływanego projektu ma odpowiadające mu `.nuspec` pliku, który ma taką samą nazwę jak projekt, do którego istnieje odwołanie projektu jest dodawana jako zależność.</span><span class="sxs-lookup"><span data-stu-id="1ef46-131">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="1ef46-132">W przeciwnym razie przywoływanego projektu jest dodawana jako część pakietu.</span><span class="sxs-lookup"><span data-stu-id="1ef46-132">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="1ef46-133">Element MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="1ef46-133">MinClientVersion</span></span> | <span data-ttu-id="1ef46-134">Ustaw *minClientVersion* atrybutu utworzonego pakietu.</span><span class="sxs-lookup"><span data-stu-id="1ef46-134">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="1ef46-135">Ta wartość zastępuje wartość istniejącej *minClientVersion* atrybutu (jeśli istnieją) w `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="1ef46-135">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="1ef46-136">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="1ef46-136">MSBuildPath</span></span> | <span data-ttu-id="1ef46-137">*(4.0 +)*  Określa ścieżkę MSBuild do użycia z poleceniem pierwszeństwo `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="1ef46-137">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="1ef46-138">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="1ef46-138">MSBuildVersion</span></span> | <span data-ttu-id="1ef46-139">*(3.2 +)*  Określa wersję programu MSBuild ma być używany z tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="1ef46-139">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="1ef46-140">Obsługiwane wartości to 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="1ef46-140">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="1ef46-141">Domyślnie jest wybierany MSBuild w ścieżce w przeciwnym razie domyślnie najwyższy zainstalowanej wersji programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="1ef46-141">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="1ef46-142">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="1ef46-142">NoDefaultExcludes</span></span> | <span data-ttu-id="1ef46-143">Zapobiega domyślne wykluczenie NuGet pakiet plików i pliki i foldery rozpoczynający się kropką, na przykład `.svn` i `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="1ef46-143">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="1ef46-144">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="1ef46-144">NoPackageAnalysis</span></span> | <span data-ttu-id="1ef46-145">Określa, że pakiet nie należy uruchamiać analizy pakietu po utworzeniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="1ef46-145">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="1ef46-146">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="1ef46-146">OutputDirectory</span></span> | <span data-ttu-id="1ef46-147">Określa folder, w którym przechowywany jest utworzony pakiet.</span><span class="sxs-lookup"><span data-stu-id="1ef46-147">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="1ef46-148">Jeśli folder nie jest określony, używany jest bieżący folder.</span><span class="sxs-lookup"><span data-stu-id="1ef46-148">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="1ef46-149">Właściwości</span><span class="sxs-lookup"><span data-stu-id="1ef46-149">Properties</span></span> | <span data-ttu-id="1ef46-150">Określa listę właściwości, które przesłaniają wartości w pliku projektu. zobacz [wspólne właściwości projektów MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) dla nazwy właściwości.</span><span class="sxs-lookup"><span data-stu-id="1ef46-150">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="1ef46-151">Argument właściwości w tym miejscu znajduje się lista tokenu = pary wartości, oddziel je średnikami, gdzie każde wystąpienie `$token$` w `.nuspec` pliku zostaną zastąpione podanej wartości.</span><span class="sxs-lookup"><span data-stu-id="1ef46-151">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="1ef46-152">Możliwe wartości ciągów w cudzysłowy.</span><span class="sxs-lookup"><span data-stu-id="1ef46-152">Values can be strings in quotation marks.</span></span> <span data-ttu-id="1ef46-153">Należy pamiętać, że dla właściwości "Konfiguracja", wartość domyślna to "Debug".</span><span class="sxs-lookup"><span data-stu-id="1ef46-153">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="1ef46-154">Aby zmienić konfigurację, wersji, należy użyć `-Properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="1ef46-154">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="1ef46-155">Suffix</span><span class="sxs-lookup"><span data-stu-id="1ef46-155">Suffix</span></span> | <span data-ttu-id="1ef46-156">*(3.4.4+)*  Dołącza sufiks z numerem wersji wewnętrznie generowane zwykle używany w przypadku dołączania kompilacji lub innych identyfikatorów w wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="1ef46-156">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="1ef46-157">Na przykład za pomocą `-suffix nightly` utworzy pakiet z podobne do numeru wersji `1.2.3-nightly`.</span><span class="sxs-lookup"><span data-stu-id="1ef46-157">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="1ef46-158">Sufiksy musi rozpoczynać się od litery, aby uniknąć potencjalnych niezgodności z różnymi wersjami programu NuGet i Menedżer pakietów NuGet, błędy i ostrzeżenia.</span><span class="sxs-lookup"><span data-stu-id="1ef46-158">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="1ef46-159">Symbole</span><span class="sxs-lookup"><span data-stu-id="1ef46-159">Symbols</span></span> | <span data-ttu-id="1ef46-160">Określa, że pakiet zawiera źródła i symbole.</span><span class="sxs-lookup"><span data-stu-id="1ef46-160">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="1ef46-161">W przypadku użycia z `.nuspec` pliku, tworzy zwykły plik pakietu NuGet i odpowiedniego pakietu symboli.</span><span class="sxs-lookup"><span data-stu-id="1ef46-161">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="1ef46-162">Narzędzie</span><span class="sxs-lookup"><span data-stu-id="1ef46-162">Tool</span></span> | <span data-ttu-id="1ef46-163">Określa, że pliki wyjściowe projektu powinna zostać umieszczona w `tool` folderu.</span><span class="sxs-lookup"><span data-stu-id="1ef46-163">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="1ef46-164">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="1ef46-164">Verbosity</span></span> | <span data-ttu-id="1ef46-165">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="1ef46-165">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="1ef46-166">Wersja</span><span class="sxs-lookup"><span data-stu-id="1ef46-166">Version</span></span> | <span data-ttu-id="1ef46-167">Zastępuje numer wersji z `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="1ef46-167">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="1ef46-168">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1ef46-168">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="1ef46-169">Z wyjątkiem programowanie zależności</span><span class="sxs-lookup"><span data-stu-id="1ef46-169">Excluding development dependencies</span></span>

<span data-ttu-id="1ef46-170">Niektóre pakiety NuGet są przydatne jako programowanie zależności, które ułatwiają tworzenie własnych biblioteki, ale niekoniecznie nie są wymagane jako zależności pakietów rzeczywiste.</span><span class="sxs-lookup"><span data-stu-id="1ef46-170">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="1ef46-171">`pack` Zignoruje polecenia `package` wpisów w `packages.config` zawierających `developmentDependency` ustawić atrybutu `true`.</span><span class="sxs-lookup"><span data-stu-id="1ef46-171">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="1ef46-172">Te wpisy nie będzie zawierał jako zależności w pakiecie utworzony.</span><span class="sxs-lookup"><span data-stu-id="1ef46-172">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="1ef46-173">Na przykład, należy wziąć pod uwagę następujące `packages.config` plik w projekcie źródła:</span><span class="sxs-lookup"><span data-stu-id="1ef46-173">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="1ef46-174">Dla tego projektu, pakiet utworzony przez `nuget pack` będzie zależy od `jQuery` i `microsoft-web-helpers` , ale nie `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="1ef46-174">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="1ef46-175">Przykłady</span><span class="sxs-lookup"><span data-stu-id="1ef46-175">Examples</span></span>

```
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5" -MSBuildVersion 12

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
