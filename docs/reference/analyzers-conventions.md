---
title: Formaty Analizatora platformy .NET kompilatora, NuGet
description: Konwencje analizatorów .NET, które spakowany i rozpowszechniać za pomocą pakietów NuGet, które implementują interfejs API lub biblioteki.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 0a8db9f6c55b7e79f9b338119e0b3ac6cb7a1e35
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324802"
---
# <a name="analyzer-nuget-formats"></a><span data-ttu-id="46714-103">Formaty NuGet analizatora</span><span class="sxs-lookup"><span data-stu-id="46714-103">Analyzer NuGet formats</span></span>

<span data-ttu-id="46714-104">Platforma kompilatora .NET (znany także jako "Roslyn") umożliwia deweloperom tworzenie [analizatory](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) który bada drzewa składnia i semantyka kod jest zapisywany.</span><span class="sxs-lookup"><span data-stu-id="46714-104">The .NET Compiler Platform (also known as "Roslyn") allows developers to create [analyzers](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) that examine the syntax tree and semantics of code as it's being written.</span></span> <span data-ttu-id="46714-105">Dzięki temu deweloperzy ze sposobem tworzenia narzędziami do analizowania specyficznego dla domeny, takie jak te, które może pomóc Przewodnik użytkowania konkretnego interfejsu API lub biblioteki.</span><span class="sxs-lookup"><span data-stu-id="46714-105">This provides developers with a way to create domain-specific analysis tools, such as those that would help guide the use of a particular API or library.</span></span> <span data-ttu-id="46714-106">Więcej informacji można znaleźć na [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) witryny typu wiki w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="46714-106">You can find more information on the [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span></span> <span data-ttu-id="46714-107">Zobacz też artykuł [Roslyn użycia do zapisania na żywo analizator kodu dla interfejsu API](https://msdn.microsoft.com/magazine/dn879356.aspx) w MSDN Magazine.</span><span class="sxs-lookup"><span data-stu-id="46714-107">Also see the article, [Use Roslyn to Write a Live Code Analyzer for your API](https://msdn.microsoft.com/magazine/dn879356.aspx) in MSDN Magazine.</span></span>

<span data-ttu-id="46714-108">Analizatory się zwykle są spakowane i dystrybuowanych jako część pakietów NuGet, które implementują interfejs API lub biblioteki w danym.</span><span class="sxs-lookup"><span data-stu-id="46714-108">Analyzers themselves are typically packaged and distributed as part of the NuGet packages that implement the API or library in question.</span></span>

<span data-ttu-id="46714-109">Aby uzyskać dobrym przykładem, zobacz [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) pakiet, który ma następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="46714-109">For a good example, see the [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) package, which has the following contents:</span></span>

- <span data-ttu-id="46714-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="46714-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span></span>
- <span data-ttu-id="46714-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="46714-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span></span>
- <span data-ttu-id="46714-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="46714-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span></span>
- <span data-ttu-id="46714-113">build\System.Runtime.Analyzers.Common.props</span><span class="sxs-lookup"><span data-stu-id="46714-113">build\System.Runtime.Analyzers.Common.props</span></span>
- <span data-ttu-id="46714-114">build\System.Runtime.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="46714-114">build\System.Runtime.Analyzers.props</span></span>
- <span data-ttu-id="46714-115">build\System.Runtime.CSharp.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="46714-115">build\System.Runtime.CSharp.Analyzers.props</span></span>
- <span data-ttu-id="46714-116">build\System.Runtime.VisualBasic.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="46714-116">build\System.Runtime.VisualBasic.Analyzers.props</span></span>
- <span data-ttu-id="46714-117">tools\install.ps1</span><span class="sxs-lookup"><span data-stu-id="46714-117">tools\install.ps1</span></span>
- <span data-ttu-id="46714-118">tools\uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="46714-118">tools\uninstall.ps1</span></span>

<span data-ttu-id="46714-119">Jak widać, umieść biblioteki DLL analizatora do `analyzers` folderu w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="46714-119">As you can see, you place the analyzer DLLs into an `analyzers` folder in the package.</span></span>

<span data-ttu-id="46714-120">Właściwości plików, wchodzące w skład wyłączyć starszych reguł programu FxCop na rzecz implementacji analizatora, są umieszczane w `build` folderu.</span><span class="sxs-lookup"><span data-stu-id="46714-120">Props files, which are included to disable legacy FxCop rules in favor of the analyzer implementation, are placed in the `build` folder.</span></span>

<span data-ttu-id="46714-121">Instalowanie i odinstalowywanie skrypty, które obsługują projektów przy użyciu `packages.config` są umieszczane w `tools`.</span><span class="sxs-lookup"><span data-stu-id="46714-121">Install and uninstall scripts that support projects using `packages.config` are placed in `tools`.</span></span>

<span data-ttu-id="46714-122">Należy również zauważyć, że ponieważ ten pakiet nie ma żadnych wymagań specyficznych dla platformy `platform` folderu zostanie pominięty.</span><span class="sxs-lookup"><span data-stu-id="46714-122">Also note that because this package has no platform-specific requirements, the `platform` folder is omitted.</span></span>


## <a name="analyzers-path-format"></a><span data-ttu-id="46714-123">Format ścieżki analizatorów</span><span class="sxs-lookup"><span data-stu-id="46714-123">Analyzers path format</span></span>

<span data-ttu-id="46714-124">Korzystanie z `analyzers` folderu jest podobny do celów [ustalać platformy docelowe](../create-packages/supporting-multiple-target-frameworks.md), z wyjątkiem specyfikatorów w ścieżce opisano zależności hosta development zamiast czas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="46714-124">The use of the `analyzers` folder is similar to that used for [target frameworks](../create-packages/supporting-multiple-target-frameworks.md), except the specifiers in the path describe development host dependencies instead of build-time.</span></span> <span data-ttu-id="46714-125">Ogólny format jest następujący:</span><span class="sxs-lookup"><span data-stu-id="46714-125">The general format is as follows:</span></span>

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- <span data-ttu-id="46714-126">**framework_name**: *opcjonalne* obszarze powierzchni interfejsu API programu .NET Framework zawartej bibliotek DLL, trzeba uruchomić program.</span><span class="sxs-lookup"><span data-stu-id="46714-126">**framework_name**: the *optional* API surface area of the .NET Framework that the contained DLLs need to run.</span></span> <span data-ttu-id="46714-127">`dotnet` nie ma obecnie jedyną prawidłową wartością ponieważ tylko hosta, który można uruchomić analizatory Roslyn.</span><span class="sxs-lookup"><span data-stu-id="46714-127">`dotnet` is presently the only valid value because Roslyn is the only host that can run analyzers.</span></span> <span data-ttu-id="46714-128">Jeśli żadne miejsce docelowe nie jest określony, biblioteki DLL są zakłada się, że dotyczą *wszystkich* elementów docelowych.</span><span class="sxs-lookup"><span data-stu-id="46714-128">If no target is specified, DLLs are assumed to apply to *all* targets.</span></span>
- <span data-ttu-id="46714-129">**supported_language**: języka, dla której Biblioteka DLL ma zastosowanie, jeden z `cs` (C#) i `vb` (Visual Basic), a `fs` (F#).</span><span class="sxs-lookup"><span data-stu-id="46714-129">**supported_language**: the language for which the DLL applies, one of `cs` (C#) and `vb` (Visual Basic), and `fs` (F#).</span></span> <span data-ttu-id="46714-130">Język wskazuje, że analizator powinien być ładowany tylko do projektu przy użyciu tego języka.</span><span class="sxs-lookup"><span data-stu-id="46714-130">The language indicates that the analyzer should be loaded only for a project using that language.</span></span> <span data-ttu-id="46714-131">Jeśli język nie zostanie określony, a następnie przyjęto, że biblioteka DLL dotyczą *wszystkich* języki, które obsługują analizatorów.</span><span class="sxs-lookup"><span data-stu-id="46714-131">If no language is specified then the DLL is assumed to apply to *all* languages that support analyzers.</span></span>
- <span data-ttu-id="46714-132">**analyzer_name**: Określa pliki DLL analizatora.</span><span class="sxs-lookup"><span data-stu-id="46714-132">**analyzer_name**: specifies the DLLs of the analyzer.</span></span> <span data-ttu-id="46714-133">Jeśli potrzebujesz dodatkowych plików innych niż bibliotek DLL, muszą być dołączone za pomocą plików elementów docelowych lub właściwości.</span><span class="sxs-lookup"><span data-stu-id="46714-133">If you need additional files beyond DLLs, they must be included through a targets or properties files.</span></span>


## <a name="install-and-uninstall-scripts"></a><span data-ttu-id="46714-134">Instalowanie i odinstalowywanie skryptów</span><span class="sxs-lookup"><span data-stu-id="46714-134">Install and uninstall scripts</span></span>

<span data-ttu-id="46714-135">Jeśli użytkownik projekcie są używani `packages.config`, skrypt programu MSBuild, który przejmuje Analizator nie dochodzą do głosu, więc należy umieszczać `install.ps1` i `uninstall.ps1` w `tools` folder z zawartością, które są opisane poniżej.</span><span class="sxs-lookup"><span data-stu-id="46714-135">If the user's project is using `packages.config`, the MSBuild script that picks up the analyzer does not come into play, so you should place `install.ps1` and `uninstall.ps1` in the `tools` folder with the contents that are described below.</span></span>

<span data-ttu-id="46714-136">**zawartość pliku Install.ps1**</span><span class="sxs-lookup"><span data-stu-id="46714-136">**install.ps1 file contents**</span></span>

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Install the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Install language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}
```


<span data-ttu-id="46714-137">**zawartość pliku Uninstall.ps1**</span><span class="sxs-lookup"><span data-stu-id="46714-137">**uninstall.ps1 file contents**</span></span>

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                try
                {
                    $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
                }
                catch
                {

                }
            }
        }
    }
}
```
