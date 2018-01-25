---
title: Analizator platformy kompilatora .NET formaty NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Konwencje dotyczące analizatorów .NET, które są umieszczone i rozpowszechnianej za pomocą pakietów NuGet, które implementują interfejs API lub biblioteki."
keywords: Konwencje analizator NuGet, analizatory .NET, NuGet i platformy kompilatora .NET, NuGet i Roslyn
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e44cfa609c14422d50769e512108844cbd2f96a4
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="analyzer-nuget-formats"></a><span data-ttu-id="71bd7-104">Analizator NuGet formatów</span><span class="sxs-lookup"><span data-stu-id="71bd7-104">Analyzer NuGet formats</span></span>

<span data-ttu-id="71bd7-105">Kompilator platformy .NET (znanej także jako "Roslyn") umożliwiają deweloperom tworzenie [analizatorów] (https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) który bada drzewa składni i semantyki kod jest zapisywany.</span><span class="sxs-lookup"><span data-stu-id="71bd7-105">The .NET Compiler Platform (also known as "Roslyn") allow developers to create [analyzers] (https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) that examine the syntax tree and semantics of code as it's being written.</span></span> <span data-ttu-id="71bd7-106">To zapewnia deweloperom sposób tworzenia i narzędzi analizy specyficznego dla domeny, takich jak te, które mogłyby ułatwić Podręcznik użycia określonego interfejsu API lub biblioteki.</span><span class="sxs-lookup"><span data-stu-id="71bd7-106">This provides developers with a way to create and domain-specific analysis tools, such as those that would help guide the use of a particular API or library.</span></span> <span data-ttu-id="71bd7-107">Więcej informacji można znaleźć na [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) typu wiki w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="71bd7-107">You can find more information on the [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span></span> <span data-ttu-id="71bd7-108">Zobacz również artykuł, [Roslyn używany do zapisywania na żywo analizator kodu dla interfejsu API](https://msdn.microsoft.com/magazine/dn879356.aspx) w witrynie MSDN Magazine.</span><span class="sxs-lookup"><span data-stu-id="71bd7-108">Also see the article, [Use Roslyn to Write a Live Code Analyzer for your API](https://msdn.microsoft.com/magazine/dn879356.aspx) in MSDN Magazine.</span></span>

<span data-ttu-id="71bd7-109">Analizatory samych zazwyczaj są umieszczone i rozproszonych w ramach pakietów NuGet, które implementują interfejs API lub biblioteki w.</span><span class="sxs-lookup"><span data-stu-id="71bd7-109">Analyzers themselves are typically packaged and distributed as part of the NuGet packages that implement the API or library in question.</span></span>

<span data-ttu-id="71bd7-110">Aby uzyskać przykład, zobacz [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) pakiet, który ma następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="71bd7-110">For a good example, see the [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) package, which has the following contents:</span></span>

- <span data-ttu-id="71bd7-111">analyzers\dotnet\System.Runtime.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="71bd7-111">analyzers\dotnet\System.Runtime.Analyzers.dll</span></span>
- <span data-ttu-id="71bd7-112">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="71bd7-112">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span></span>
- <span data-ttu-id="71bd7-113">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="71bd7-113">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span></span>
- <span data-ttu-id="71bd7-114">build\System.Runtime.Analyzers.Common.props</span><span class="sxs-lookup"><span data-stu-id="71bd7-114">build\System.Runtime.Analyzers.Common.props</span></span>
- <span data-ttu-id="71bd7-115">build\System.Runtime.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="71bd7-115">build\System.Runtime.Analyzers.props</span></span>
- <span data-ttu-id="71bd7-116">build\System.Runtime.CSharp.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="71bd7-116">build\System.Runtime.CSharp.Analyzers.props</span></span>
- <span data-ttu-id="71bd7-117">build\System.Runtime.VisualBasic.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="71bd7-117">build\System.Runtime.VisualBasic.Analyzers.props</span></span>
- <span data-ttu-id="71bd7-118">tools\install.ps1</span><span class="sxs-lookup"><span data-stu-id="71bd7-118">tools\install.ps1</span></span>
- <span data-ttu-id="71bd7-119">tools\uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="71bd7-119">tools\uninstall.ps1</span></span>

<span data-ttu-id="71bd7-120">Jak widać, umieść biblioteki DLL analizatora do `analyzers` folderu w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="71bd7-120">As you can see, you place the analyzer DLLs into an `analyzers` folder in the package.</span></span>

<span data-ttu-id="71bd7-121">Pliki właściwości, które są włączone, aby je wyłączyć starszej wersji programu FxCop na rzecz implementacji analizatora, są umieszczane w `build` folderu.</span><span class="sxs-lookup"><span data-stu-id="71bd7-121">Props files, which are included to disable legacy FxCop rules in favor of the analyzer implementation, are placed in the `build` folder.</span></span>

<span data-ttu-id="71bd7-122">Instalowanie i odinstalowywanie skrypty, które obsługują projektów przy użyciu `packages.config` są umieszczane w `tools`.</span><span class="sxs-lookup"><span data-stu-id="71bd7-122">Install and uninstall scripts that support projects using `packages.config` are placed in `tools`.</span></span>

<span data-ttu-id="71bd7-123">Należy również zauważyć, że ponieważ ten pakiet nie ma specyficznego dla platformy wymagań, `platform` folderu zostanie pominięty.</span><span class="sxs-lookup"><span data-stu-id="71bd7-123">Also note that because this package has no platform-specific requirements, the `platform` folder is omitted.</span></span>


## <a name="analyzers-path-format"></a><span data-ttu-id="71bd7-124">Format ścieżki analizatorów</span><span class="sxs-lookup"><span data-stu-id="71bd7-124">Analyzers path format</span></span>

<span data-ttu-id="71bd7-125">Korzystanie z `analyzers` folder jest podobny do celów [platform docelowych](../create-packages/supporting-multiple-target-frameworks.md), z wyjątkiem Specyfikatory w ścieżce opisano programowanie hosta zależności, zamiast czas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="71bd7-125">The use of the `analyzers` folder is similar to that used for [target frameworks](../create-packages/supporting-multiple-target-frameworks.md), except the specifiers in the path describe development host dependencies instead of build-time.</span></span> <span data-ttu-id="71bd7-126">Ogólny format jest następujący:</span><span class="sxs-lookup"><span data-stu-id="71bd7-126">The general format is as follows:</span></span>

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}}/{analyzer_name}.dll

- <span data-ttu-id="71bd7-127">**framework_name**: *opcjonalne* powierzchni interfejsu API programu .NET Framework zawartej biblioteki DLL potrzebne do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="71bd7-127">**framework_name**: the *optional* API surface area of the .NET Framework that the contained DLLs need to run.</span></span> <span data-ttu-id="71bd7-128">`dotnet`nie ma obecnie jedyną prawidłową wartością ponieważ Roslyn jest tylko hosta, który można uruchomić analizatorów.</span><span class="sxs-lookup"><span data-stu-id="71bd7-128">`dotnet` is presently the only valid value because Roslyn is the only host that can run analyzers.</span></span> <span data-ttu-id="71bd7-129">Jeśli docelowy nie zostanie określony, biblioteki DLL uznaje się, że dotyczą *wszystkie* elementy docelowe.</span><span class="sxs-lookup"><span data-stu-id="71bd7-129">If no target is specified, DLLs are assumed to apply to *all* targets.</span></span>
- <span data-ttu-id="71bd7-130">**supported_language**: język, dla którego plik DLL, który ma zastosowanie, jeden z `cs` (C#) i `vb` (Visual Basic), a `fs` (F #).</span><span class="sxs-lookup"><span data-stu-id="71bd7-130">**supported_language**: the language for which the DLL applies, one of `cs` (C#) and `vb` (Visual Basic), and `fs` (F#).</span></span> <span data-ttu-id="71bd7-131">Język wskazuje, że analizatora powinny być ładowane tylko do projektu przy użyciu tego języka.</span><span class="sxs-lookup"><span data-stu-id="71bd7-131">The language indicates that the analyzer should be loaded only for a project using that language.</span></span> <span data-ttu-id="71bd7-132">Jeśli język nie zostanie określony, a następnie przyjęto, że biblioteka DLL dotyczą *wszystkie* języków, które obsługują analizatorów.</span><span class="sxs-lookup"><span data-stu-id="71bd7-132">If no language is specified then DLL is assumed to apply to *all* languages that support analyzers.</span></span>
- <span data-ttu-id="71bd7-133">**analyzer_name**: Określa bibliotek DLL analizatora.</span><span class="sxs-lookup"><span data-stu-id="71bd7-133">**analyzer_name**: specifies the DLLs of the analyzer.</span></span> <span data-ttu-id="71bd7-134">Jeśli potrzebujesz dodatkowych plików poza biblioteki DLL muszą być dodane przez pliki elementów docelowych lub właściwości.</span><span class="sxs-lookup"><span data-stu-id="71bd7-134">If you need additional files beyond DLLs, they must be included through a targets or properties files.</span></span>


## <a name="install-and-uninstall-scripts"></a><span data-ttu-id="71bd7-135">Instalowanie i odinstalowywanie skryptów</span><span class="sxs-lookup"><span data-stu-id="71bd7-135">Install and uninstall scripts</span></span>

<span data-ttu-id="71bd7-136">Jeśli projekt użytkownika jest za pomocą `packages.config`, skrypt MSBuild, który przejmuje analizatora nie jest dostarczany do gry, zaleca się `install.ps1` i `uninstall.ps1` w `tools` folder z zawartością, które są opisane poniżej.</span><span class="sxs-lookup"><span data-stu-id="71bd7-136">If the user's project is using `packages.config`, the MSBuild script that picks up the analyzer does not come into play, so you should `install.ps1` and `uninstall.ps1` in the `tools` folder with the contents that are described below.</span></span>

<span data-ttu-id="71bd7-137">**zawartość pliku Install.ps1**</span><span class="sxs-lookup"><span data-stu-id="71bd7-137">**install.ps1 file contents**</span></span>

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


<span data-ttu-id="71bd7-138">**zawartość pliku Uninstall.ps1**</span><span class="sxs-lookup"><span data-stu-id="71bd7-138">**uninstall.ps1 file contents**</span></span>

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
