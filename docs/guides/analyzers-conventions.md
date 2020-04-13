---
title: Formaty analizatora platformy kompilatora platformy .NET dla nuget
description: Konwencje dla analizatorów platformy .NET, które są pakowane i dystrybuowane za pomocą pakietów NuGet, które implementują interfejs API lub biblioteki.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 4d337299f725b38981b0121069d5e6295b05e34e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "72924640"
---
# <a name="analyzer-nuget-formats"></a><span data-ttu-id="fbc79-103">Formaty Analizatora NuGet</span><span class="sxs-lookup"><span data-stu-id="fbc79-103">Analyzer NuGet formats</span></span>

<span data-ttu-id="fbc79-104">Platforma kompilatora .NET (znany również jako "Roslyn") umożliwia deweloperom tworzenie [analizatorów,](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) które badają drzewa składni i semantyki kodu, jak jest zapisywany.</span><span class="sxs-lookup"><span data-stu-id="fbc79-104">The .NET Compiler Platform (also known as "Roslyn") allows developers to create [analyzers](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) that examine the syntax tree and semantics of code as it's being written.</span></span> <span data-ttu-id="fbc79-105">Dzięki temu deweloperzy mogą tworzyć narzędzia analizy specyficzne dla domeny, takie jak te, które pomogą w korzystaniu z określonego interfejsu API lub biblioteki.</span><span class="sxs-lookup"><span data-stu-id="fbc79-105">This provides developers with a way to create domain-specific analysis tools, such as those that would help guide the use of a particular API or library.</span></span> <span data-ttu-id="fbc79-106">Więcej informacji można znaleźć na wiki [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub.</span><span class="sxs-lookup"><span data-stu-id="fbc79-106">You can find more information on the [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span></span> <span data-ttu-id="fbc79-107">Zobacz także [artykuł, Użyj Roslyn napisać analizator kodu na żywo dla interfejsu API](https://msdn.microsoft.com/magazine/dn879356.aspx) w MSDN Magazine.</span><span class="sxs-lookup"><span data-stu-id="fbc79-107">Also see the article, [Use Roslyn to Write a Live Code Analyzer for your API](https://msdn.microsoft.com/magazine/dn879356.aspx) in MSDN Magazine.</span></span>

<span data-ttu-id="fbc79-108">Same analizatory są zazwyczaj pakowane i dystrybuowane jako część pakietów NuGet, które implementują interfejs API lub biblioteki, o których mowa.</span><span class="sxs-lookup"><span data-stu-id="fbc79-108">Analyzers themselves are typically packaged and distributed as part of the NuGet packages that implement the API or library in question.</span></span>

<span data-ttu-id="fbc79-109">Dobrym przykładem jest pakiet [System.Runtime.Analyzers,](https://www.nuget.org/packages/System.Runtime.Analyzers) który zawiera następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="fbc79-109">For a good example, see the [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) package, which has the following contents:</span></span>

- <span data-ttu-id="fbc79-110">analizatory\dotnet\System.Runtime.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="fbc79-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span></span>
- <span data-ttu-id="fbc79-111">analizatory\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="fbc79-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span></span>
- <span data-ttu-id="fbc79-112">analizatory\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="fbc79-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span></span>
- <span data-ttu-id="fbc79-113">build\System.Runtime.Analyzers.Common.props</span><span class="sxs-lookup"><span data-stu-id="fbc79-113">build\System.Runtime.Analyzers.Common.props</span></span>
- <span data-ttu-id="fbc79-114">build\System.Runtime.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="fbc79-114">build\System.Runtime.Analyzers.props</span></span>
- <span data-ttu-id="fbc79-115">build\System.Runtime.CSharp.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="fbc79-115">build\System.Runtime.CSharp.Analyzers.props</span></span>
- <span data-ttu-id="fbc79-116">kompilacja\System.Runtime.VisualBasic.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="fbc79-116">build\System.Runtime.VisualBasic.Analyzers.props</span></span>
- <span data-ttu-id="fbc79-117">narzędzia\install.ps1</span><span class="sxs-lookup"><span data-stu-id="fbc79-117">tools\install.ps1</span></span>
- <span data-ttu-id="fbc79-118">narzędzia\odinstaluj.ps1</span><span class="sxs-lookup"><span data-stu-id="fbc79-118">tools\uninstall.ps1</span></span>

<span data-ttu-id="fbc79-119">Jak widać, umieszczasz biblioteki DLL analizatora w folderze `analyzers` w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="fbc79-119">As you can see, you place the analyzer DLLs into an `analyzers` folder in the package.</span></span>

<span data-ttu-id="fbc79-120">Pliki rekwizytów, które są dołączone do wyłączenia starszych reguł FxCop na `build` rzecz implementacji analizatora, są umieszczane w folderze.</span><span class="sxs-lookup"><span data-stu-id="fbc79-120">Props files, which are included to disable legacy FxCop rules in favor of the analyzer implementation, are placed in the `build` folder.</span></span>

<span data-ttu-id="fbc79-121">Instalowanie i odinstalowywanie `packages.config` skryptów, które obsługują projekty, które są używane, są umieszczane w pliku `tools`.</span><span class="sxs-lookup"><span data-stu-id="fbc79-121">Install and uninstall scripts that support projects using `packages.config` are placed in `tools`.</span></span>

<span data-ttu-id="fbc79-122">Należy również zauważyć, że ponieważ ten pakiet `platform` nie ma wymagań specyficznych dla platformy, folder jest pomijany.</span><span class="sxs-lookup"><span data-stu-id="fbc79-122">Also note that because this package has no platform-specific requirements, the `platform` folder is omitted.</span></span>


## <a name="analyzers-path-format"></a><span data-ttu-id="fbc79-123">Format ścieżki analizatorów</span><span class="sxs-lookup"><span data-stu-id="fbc79-123">Analyzers path format</span></span>

<span data-ttu-id="fbc79-124">Użycie folderu `analyzers` jest podobny do używanego dla [struktur docelowych](../create-packages/supporting-multiple-target-frameworks.md), z wyjątkiem specyfikatorów w ścieżce opisują zależności hosta rozwoju zamiast czasu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="fbc79-124">The use of the `analyzers` folder is similar to that used for [target frameworks](../create-packages/supporting-multiple-target-frameworks.md), except the specifiers in the path describe development host dependencies instead of build-time.</span></span> <span data-ttu-id="fbc79-125">Ogólny format jest następujący:</span><span class="sxs-lookup"><span data-stu-id="fbc79-125">The general format is as follows:</span></span>

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- <span data-ttu-id="fbc79-126">**framework_name** i **wersja:** *opcjonalny* obszar powierzchni interfejsu API programu .NET Framework, który zawiera biblioteki DLL muszą być uruchamiane.</span><span class="sxs-lookup"><span data-stu-id="fbc79-126">**framework_name** and **version**: the *optional* API surface area of the .NET Framework that the contained DLLs need to run.</span></span> <span data-ttu-id="fbc79-127">`dotnet`jest obecnie jedyną prawidłową wartością, ponieważ Roslyn jest jedynym hostem, który może uruchamiać analizatory.</span><span class="sxs-lookup"><span data-stu-id="fbc79-127">`dotnet` is presently the only valid value because Roslyn is the only host that can run analyzers.</span></span> <span data-ttu-id="fbc79-128">Jeśli nie określono celu, zakłada się, że biblioteki DLL mają zastosowanie do *wszystkich* obiektów docelowych.</span><span class="sxs-lookup"><span data-stu-id="fbc79-128">If no target is specified, DLLs are assumed to apply to *all* targets.</span></span>
- <span data-ttu-id="fbc79-129">**supported_language**: język, dla którego jest stosowana biblioteka `cs` DLL, `vb` jeden z (C#) i (Visual Basic) i `fs` (F#).</span><span class="sxs-lookup"><span data-stu-id="fbc79-129">**supported_language**: the language for which the DLL applies, one of `cs` (C#) and `vb` (Visual Basic), and `fs` (F#).</span></span> <span data-ttu-id="fbc79-130">Język wskazuje, że analizator powinien być ładowany tylko dla projektu przy użyciu tego języka.</span><span class="sxs-lookup"><span data-stu-id="fbc79-130">The language indicates that the analyzer should be loaded only for a project using that language.</span></span> <span data-ttu-id="fbc79-131">Jeśli nie określono języka, zakłada się, że biblioteka DLL będzie stosowana do *wszystkich* języków, które obsługują analizatory.</span><span class="sxs-lookup"><span data-stu-id="fbc79-131">If no language is specified then the DLL is assumed to apply to *all* languages that support analyzers.</span></span>
- <span data-ttu-id="fbc79-132">**analyzer_name**: określa biblioteki DLL analizatora.</span><span class="sxs-lookup"><span data-stu-id="fbc79-132">**analyzer_name**: specifies the DLLs of the analyzer.</span></span> <span data-ttu-id="fbc79-133">Jeśli potrzebujesz dodatkowych plików poza bibliotekami DLL, muszą one zostać uwzględnione za pośrednictwem plików docelowych lub właściwości.</span><span class="sxs-lookup"><span data-stu-id="fbc79-133">If you need additional files beyond DLLs, they must be included through a targets or properties files.</span></span>


## <a name="install-and-uninstall-scripts"></a><span data-ttu-id="fbc79-134">Instalowanie i odinstalowywanie skryptów</span><span class="sxs-lookup"><span data-stu-id="fbc79-134">Install and uninstall scripts</span></span>

<span data-ttu-id="fbc79-135">Jeśli używany jest projekt `packages.config`użytkownika, skrypt MSBuild, który odbiera analizator, nie wchodzi w `install.ps1` `uninstall.ps1` grę, `tools` dlatego należy umieścić i w folderze z zawartością, która jest opisana poniżej.</span><span class="sxs-lookup"><span data-stu-id="fbc79-135">If the user's project is using `packages.config`, the MSBuild script that picks up the analyzer does not come into play, so you should place `install.ps1` and `uninstall.ps1` in the `tools` folder with the contents that are described below.</span></span>

<span data-ttu-id="fbc79-136">**zawartość pliku install.ps1**</span><span class="sxs-lookup"><span data-stu-id="fbc79-136">**install.ps1 file contents**</span></span>

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


<span data-ttu-id="fbc79-137">**odinstalowywanie.ps1 zawartość pliku**</span><span class="sxs-lookup"><span data-stu-id="fbc79-137">**uninstall.ps1 file contents**</span></span>

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
