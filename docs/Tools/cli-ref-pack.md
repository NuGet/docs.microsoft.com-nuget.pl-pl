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
ms.openlocfilehash: 353d5d839d85c04bc315c3a0e9cfe274a361bd15
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="93117-104">polecenie pakietu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="93117-104">pack command (NuGet CLI)</span></span>

<span data-ttu-id="93117-105">**Dotyczy:** pakietu tworzenia &bullet; **obsługiwane wersje:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="93117-105">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="93117-106">Tworzy oparte na określony pakiet NuGet `.nuspec` lub pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="93117-106">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="93117-107">`dotnet pack` Polecenia (zobacz [polecenia dotnet](dotnet-Commands.md)) i `msbuild /t:pack` (zobacz [docelowych elementów MSBuild](../schema/msbuild-targets.md)) może być używany jako alternatyw.</span><span class="sxs-lookup"><span data-stu-id="93117-107">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../schema/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="93117-108">W obszarze Mono Tworzenie pakietu z pliku projektu nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="93117-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="93117-109">Należy również dostosować innego niż lokalne ścieżki w `.nuspec` plików do ścieżek typu Unix, jak nuget.exe nie konwertuje nazwy ścieżek systemu Windows, sama.</span><span class="sxs-lookup"><span data-stu-id="93117-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="93117-110">Użycie</span><span class="sxs-lookup"><span data-stu-id="93117-110">Usage</span></span>

```
nuget pack <nuspecPath | projectPath> [options]
```

<span data-ttu-id="93117-111">gdzie `<nuspecPath>` i `<projectPath>` określ `.nuspec` lub odpowiednio projektu pliku.</span><span class="sxs-lookup"><span data-stu-id="93117-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="93117-112">Opcje</span><span class="sxs-lookup"><span data-stu-id="93117-112">Options</span></span>

| <span data-ttu-id="93117-113">Opcja</span><span class="sxs-lookup"><span data-stu-id="93117-113">Option</span></span> | <span data-ttu-id="93117-114">Opis</span><span class="sxs-lookup"><span data-stu-id="93117-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="93117-115">Nieistniejący</span><span class="sxs-lookup"><span data-stu-id="93117-115">BasePath</span></span> | <span data-ttu-id="93117-116">Ustawia ścieżki podstawowej plików zdefiniowanych w `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="93117-116">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="93117-117">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="93117-117">Build</span></span> | <span data-ttu-id="93117-118">Określa, czy projekt powinien skompilowany przed zbudowaniem pakietu.</span><span class="sxs-lookup"><span data-stu-id="93117-118">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="93117-119">Wyklucz</span><span class="sxs-lookup"><span data-stu-id="93117-119">Exclude</span></span> | <span data-ttu-id="93117-120">Określa jeden lub więcej wzorców symboli wieloznacznych, które mają zostać wykluczone podczas tworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="93117-120">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> |
| <span data-ttu-id="93117-121">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="93117-121">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="93117-122">Uniemożliwia włączenie puste katalogi, podczas tworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="93117-122">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="93117-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="93117-123">ForceEnglishOutput</span></span> | <span data-ttu-id="93117-124">*(3.5 +)*  Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="93117-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="93117-125">Pomoc</span><span class="sxs-lookup"><span data-stu-id="93117-125">Help</span></span> | <span data-ttu-id="93117-126">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="93117-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="93117-127">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="93117-127">IncludeReferencedProjects</span></span> | <span data-ttu-id="93117-128">Wskazuje, że wbudowanych pakiet powinien zawierać przywoływane projekty jako zależności lub jako część pakietu.</span><span class="sxs-lookup"><span data-stu-id="93117-128">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="93117-129">Jeśli przywoływanego projektu ma odpowiadające mu `.nuspec` pliku, który ma taką samą nazwę jak projekt, do którego istnieje odwołanie projektu jest dodawana jako zależność.</span><span class="sxs-lookup"><span data-stu-id="93117-129">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="93117-130">W przeciwnym razie przywoływanego projektu jest dodawana jako część pakietu.</span><span class="sxs-lookup"><span data-stu-id="93117-130">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="93117-131">Element MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="93117-131">MinClientVersion</span></span> | <span data-ttu-id="93117-132">Ustaw *minClientVersion* atrybutu utworzonego pakietu.</span><span class="sxs-lookup"><span data-stu-id="93117-132">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="93117-133">Ta wartość zastępuje wartość istniejącej *minClientVersion* atrybutu (jeśli istnieją) w `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="93117-133">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="93117-134">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="93117-134">MSBuildPath</span></span> | <span data-ttu-id="93117-135">*(4.0 +)*  Określa ścieżkę MSBuild do użycia z poleceniem pierwszeństwo `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="93117-135">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="93117-136">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="93117-136">MSBuildVersion</span></span> | <span data-ttu-id="93117-137">*(3.2 +)*  Określa wersję programu MSBuild ma być używany z tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="93117-137">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="93117-138">Obsługiwane wartości to 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="93117-138">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="93117-139">Domyślnie jest wybierany MSBuild w ścieżce w przeciwnym razie domyślnie najwyższy zainstalowanej wersji programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="93117-139">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="93117-140">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="93117-140">NoDefaultExcludes</span></span> | <span data-ttu-id="93117-141">Zapobiega domyślne wykluczenie NuGet pakiet plików i pliki i foldery rozpoczynający się kropką, na przykład `.svn` i `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="93117-141">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="93117-142">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="93117-142">NoPackageAnalysis</span></span> | <span data-ttu-id="93117-143">Określa, że pakiet nie należy uruchamiać analizy pakietu po utworzeniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="93117-143">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="93117-144">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="93117-144">OutputDirectory</span></span> | <span data-ttu-id="93117-145">Określa folder, w którym przechowywany jest utworzony pakiet.</span><span class="sxs-lookup"><span data-stu-id="93117-145">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="93117-146">Jeśli folder nie jest określony, używany jest bieżący folder.</span><span class="sxs-lookup"><span data-stu-id="93117-146">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="93117-147">Właściwości</span><span class="sxs-lookup"><span data-stu-id="93117-147">Properties</span></span> | <span data-ttu-id="93117-148">Określa listę właściwości, które przesłaniają wartości w pliku projektu. zobacz [wspólne właściwości projektów MSBuild](https://docs.microsoft.com/visualstudio/msbuild/common-msbuild-project-properties) dla nazwy właściwości.</span><span class="sxs-lookup"><span data-stu-id="93117-148">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](https://docs.microsoft.com/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="93117-149">Argument właściwości w tym miejscu znajduje się lista tokenu = pary wartości, oddziel je średnikami, gdzie każde wystąpienie `$token$` w `.nuspec` pliku zostaną zastąpione podanej wartości.</span><span class="sxs-lookup"><span data-stu-id="93117-149">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="93117-150">Możliwe wartości ciągów w cudzysłowy.</span><span class="sxs-lookup"><span data-stu-id="93117-150">Values can be strings in quotation marks.</span></span> <span data-ttu-id="93117-151">Należy pamiętać, że dla właściwości "Konfiguracja", wartość domyślna to "Debug".</span><span class="sxs-lookup"><span data-stu-id="93117-151">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="93117-152">Aby zmienić konfigurację, wersji, należy użyć `-Properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="93117-152">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="93117-153">Sufiks</span><span class="sxs-lookup"><span data-stu-id="93117-153">Suffix</span></span> | <span data-ttu-id="93117-154">*(3.4.4+)*  Dołącza sufiks z numerem wersji wewnętrznie generowane zwykle używany w przypadku dołączania kompilacji lub innych identyfikatorów w wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="93117-154">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="93117-155">Na przykład za pomocą `-suffix nightly` utworzy pakiet z podobne do numeru wersji `1.2.3-nightly`.</span><span class="sxs-lookup"><span data-stu-id="93117-155">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="93117-156">Sufiksy musi rozpoczynać się od litery, aby uniknąć potencjalnych niezgodności z różnymi wersjami programu NuGet i Menedżer pakietów NuGet, błędy i ostrzeżenia.</span><span class="sxs-lookup"><span data-stu-id="93117-156">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="93117-157">Symbole</span><span class="sxs-lookup"><span data-stu-id="93117-157">Symbols</span></span> | <span data-ttu-id="93117-158">Określa, że pakiet zawiera źródła i symbole.</span><span class="sxs-lookup"><span data-stu-id="93117-158">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="93117-159">W przypadku użycia z `.nuspec` pliku, tworzy zwykły plik pakietu NuGet i odpowiedniego pakietu symboli.</span><span class="sxs-lookup"><span data-stu-id="93117-159">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="93117-160">Narzędzie</span><span class="sxs-lookup"><span data-stu-id="93117-160">Tool</span></span> | <span data-ttu-id="93117-161">Określa, że pliki wyjściowe projektu powinna zostać umieszczona w `tool` folderu.</span><span class="sxs-lookup"><span data-stu-id="93117-161">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="93117-162">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="93117-162">Verbosity</span></span> | <span data-ttu-id="93117-163">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="93117-163">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="93117-164">Wersja</span><span class="sxs-lookup"><span data-stu-id="93117-164">Version</span></span> | <span data-ttu-id="93117-165">Zastępuje numer wersji z `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="93117-165">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="93117-166">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="93117-166">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="93117-167">Z wyjątkiem programowanie zależności</span><span class="sxs-lookup"><span data-stu-id="93117-167">Excluding development dependencies</span></span>

<span data-ttu-id="93117-168">Niektóre pakiety NuGet są przydatne jako programowanie zależności, które ułatwiają tworzenie własnych biblioteki, ale niekoniecznie nie są wymagane jako zależności pakietów rzeczywiste.</span><span class="sxs-lookup"><span data-stu-id="93117-168">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="93117-169">`pack` Zignoruje polecenia `package` wpisów w `packages.config` zawierających `developmentDependency` ustawić atrybutu `true`.</span><span class="sxs-lookup"><span data-stu-id="93117-169">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="93117-170">Te wpisy nie będzie zawierał jako zależności w pakiecie utworzony.</span><span class="sxs-lookup"><span data-stu-id="93117-170">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="93117-171">Na przykład, należy wziąć pod uwagę następujące `packages.config` plik w projekcie źródła:</span><span class="sxs-lookup"><span data-stu-id="93117-171">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="93117-172">Dla tego projektu, pakiet utworzony przez `nuget pack` będzie zależy od `jQuery` i `microsoft-web-helpers` , ale nie `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="93117-172">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="93117-173">Przykłady</span><span class="sxs-lookup"><span data-stu-id="93117-173">Examples</span></span>

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
```
