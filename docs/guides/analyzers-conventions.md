---
title: Formaty analizatora .NET Compiler Platform dla narzędzia NuGet
description: Konwencje dla analizatorów .NET spakowane i dystrybuowane z pakietami NuGet, które implementują interfejs API lub bibliotekę.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: f1e9bb96fc7acc73ec37cebcdc8015081fafb307
ms.sourcegitcommit: 650c08f8bc3d48dfd206a111e5e2aaca3001f569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97523412"
---
# <a name="analyzer-nuget-formats"></a><span data-ttu-id="d50d8-103">Formaty NuGet analizatora</span><span class="sxs-lookup"><span data-stu-id="d50d8-103">Analyzer NuGet formats</span></span>

<span data-ttu-id="d50d8-104">.NET Compiler Platform (znany również jako "Roslyn") umożliwia deweloperom tworzenie [analizatorów](https://github.com/dotnet/roslyn/blob/master/docs/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix.md) , które analizują drzewo składni i semantykę kodu podczas jego pisania.</span><span class="sxs-lookup"><span data-stu-id="d50d8-104">The .NET Compiler Platform (also known as "Roslyn") allows developers to create [analyzers](https://github.com/dotnet/roslyn/blob/master/docs/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix.md) that examine the syntax tree and semantics of code as it's being written.</span></span> <span data-ttu-id="d50d8-105">Pozwala to deweloperom na tworzenie specyficznych dla domeny narzędzi do analizy, takich jak te, które mogłyby ułatwić korzystanie z konkretnego interfejsu API lub biblioteki.</span><span class="sxs-lookup"><span data-stu-id="d50d8-105">This provides developers with a way to create domain-specific analysis tools, such as those that would help guide the use of a particular API or library.</span></span> <span data-ttu-id="d50d8-106">Więcej informacji można znaleźć na stronie wiki [platformy .NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub.</span><span class="sxs-lookup"><span data-stu-id="d50d8-106">You can find more information on the [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span></span> <span data-ttu-id="d50d8-107">Zobacz również artykuł Roslyn, [Aby napisać analizator kodu na żywo dla interfejsu API](/archive/msdn-magazine/2014/special-issue/csharp-and-visual-basic-use-roslyn-to-write-a-live-code-analyzer-for-your-api) w usłudze MSDN Magazine.</span><span class="sxs-lookup"><span data-stu-id="d50d8-107">Also see the article, [Use Roslyn to Write a Live Code Analyzer for your API](/archive/msdn-magazine/2014/special-issue/csharp-and-visual-basic-use-roslyn-to-write-a-live-code-analyzer-for-your-api) in MSDN Magazine.</span></span>

<span data-ttu-id="d50d8-108">Analizatory są zwykle spakowane i dystrybuowane jako część pakietów NuGet implementujących dany interfejs API lub bibliotekę.</span><span class="sxs-lookup"><span data-stu-id="d50d8-108">Analyzers themselves are typically packaged and distributed as part of the NuGet packages that implement the API or library in question.</span></span>

<span data-ttu-id="d50d8-109">Aby uzyskać dobry przykład, zobacz pakiet [System. Runtime. analizatory](https://www.nuget.org/packages/System.Runtime.Analyzers) , który ma następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="d50d8-109">For a good example, see the [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) package, which has the following contents:</span></span>

- <span data-ttu-id="d50d8-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="d50d8-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span></span>
- <span data-ttu-id="d50d8-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="d50d8-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span></span>
- <span data-ttu-id="d50d8-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="d50d8-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span></span>
- <span data-ttu-id="d50d8-113">build\System.Runtime.Analyzers.Common.props</span><span class="sxs-lookup"><span data-stu-id="d50d8-113">build\System.Runtime.Analyzers.Common.props</span></span>
- <span data-ttu-id="d50d8-114">build\System.Runtime.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="d50d8-114">build\System.Runtime.Analyzers.props</span></span>
- <span data-ttu-id="d50d8-115">build\System.Runtime.CSharp.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="d50d8-115">build\System.Runtime.CSharp.Analyzers.props</span></span>
- <span data-ttu-id="d50d8-116">build\System.Runtime.VisualBasic.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="d50d8-116">build\System.Runtime.VisualBasic.Analyzers.props</span></span>
- <span data-ttu-id="d50d8-117">tools\install.ps1</span><span class="sxs-lookup"><span data-stu-id="d50d8-117">tools\install.ps1</span></span>
- <span data-ttu-id="d50d8-118">tools\uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="d50d8-118">tools\uninstall.ps1</span></span>

<span data-ttu-id="d50d8-119">Jak widać, należy umieścić biblioteki DLL analizatora w `analyzers` folderze pakietu.</span><span class="sxs-lookup"><span data-stu-id="d50d8-119">As you can see, you place the analyzer DLLs into an `analyzers` folder in the package.</span></span>

<span data-ttu-id="d50d8-120">Pliki props, które są dołączone do wyłączania starszych reguł FxCop na korzyść implementacji analizatora, są umieszczane w `build` folderze.</span><span class="sxs-lookup"><span data-stu-id="d50d8-120">Props files, which are included to disable legacy FxCop rules in favor of the analyzer implementation, are placed in the `build` folder.</span></span>

<span data-ttu-id="d50d8-121">Instalowanie i odinstalowywanie skryptów, które obsługują projekty przy użyciu programu, `packages.config` są umieszczane w temacie `tools` .</span><span class="sxs-lookup"><span data-stu-id="d50d8-121">Install and uninstall scripts that support projects using `packages.config` are placed in `tools`.</span></span>

<span data-ttu-id="d50d8-122">Należy również zauważyć, że ponieważ ten pakiet nie ma wymagań specyficznych dla platformy, `platform` folder zostanie pominięty.</span><span class="sxs-lookup"><span data-stu-id="d50d8-122">Also note that because this package has no platform-specific requirements, the `platform` folder is omitted.</span></span>


## <a name="analyzers-path-format"></a><span data-ttu-id="d50d8-123">Format ścieżki analizatorów</span><span class="sxs-lookup"><span data-stu-id="d50d8-123">Analyzers path format</span></span>

<span data-ttu-id="d50d8-124">Użycie `analyzers` folderu jest podobne do programu, który jest używany dla [platform docelowych](../create-packages/supporting-multiple-target-frameworks.md), z wyjątkiem specyfikatorów w ścieżce opisują zależności hosta deweloperskiego, a nie czas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="d50d8-124">The use of the `analyzers` folder is similar to that used for [target frameworks](../create-packages/supporting-multiple-target-frameworks.md), except the specifiers in the path describe development host dependencies instead of build-time.</span></span> <span data-ttu-id="d50d8-125">Format ogólny jest następujący:</span><span class="sxs-lookup"><span data-stu-id="d50d8-125">The general format is as follows:</span></span>

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- <span data-ttu-id="d50d8-126">**framework_name** i **wersja**: *opcjonalny* obszar powierzchni interfejsu API .NET Framework, które muszą zostać uruchomione w zawartych bibliotekach DLL.</span><span class="sxs-lookup"><span data-stu-id="d50d8-126">**framework_name** and **version**: the *optional* API surface area of the .NET Framework that the contained DLLs need to run.</span></span> <span data-ttu-id="d50d8-127">`dotnet` jest obecnie jedyną prawidłową wartością, ponieważ Roslyn jest jedynym hostem, który może uruchamiać analizatory.</span><span class="sxs-lookup"><span data-stu-id="d50d8-127">`dotnet` is presently the only valid value because Roslyn is the only host that can run analyzers.</span></span> <span data-ttu-id="d50d8-128">Jeśli nie określono elementu docelowego, zakłada się, że biblioteki DLL są stosowane do *wszystkich* elementów docelowych.</span><span class="sxs-lookup"><span data-stu-id="d50d8-128">If no target is specified, DLLs are assumed to apply to *all* targets.</span></span>
- <span data-ttu-id="d50d8-129">**supported_language**: język, dla którego jest stosowana Biblioteka DLL, jeden z `cs` (C#) i `vb` (Visual Basic) i `fs` (F #).</span><span class="sxs-lookup"><span data-stu-id="d50d8-129">**supported_language**: the language for which the DLL applies, one of `cs` (C#) and `vb` (Visual Basic), and `fs` (F#).</span></span> <span data-ttu-id="d50d8-130">Język wskazuje, że analizator powinien być załadowany tylko dla projektu używającego tego języka.</span><span class="sxs-lookup"><span data-stu-id="d50d8-130">The language indicates that the analyzer should be loaded only for a project using that language.</span></span> <span data-ttu-id="d50d8-131">Jeśli nie określono żadnego języka, przyjęto, że biblioteka DLL ma zastosowanie do *wszystkich* języków, które obsługują analizatory.</span><span class="sxs-lookup"><span data-stu-id="d50d8-131">If no language is specified then the DLL is assumed to apply to *all* languages that support analyzers.</span></span>
- <span data-ttu-id="d50d8-132">**analyzer_name**: określa biblioteki DLL analizatora.</span><span class="sxs-lookup"><span data-stu-id="d50d8-132">**analyzer_name**: specifies the DLLs of the analyzer.</span></span> <span data-ttu-id="d50d8-133">Jeśli potrzebujesz dodatkowych plików poza biblioteką DLL, muszą one być dołączone do plików obiektów docelowych lub właściwości.</span><span class="sxs-lookup"><span data-stu-id="d50d8-133">If you need additional files beyond DLLs, they must be included through a targets or properties files.</span></span>


## <a name="install-and-uninstall-scripts"></a><span data-ttu-id="d50d8-134">Instalowanie i odinstalowywanie skryptów</span><span class="sxs-lookup"><span data-stu-id="d50d8-134">Install and uninstall scripts</span></span>

<span data-ttu-id="d50d8-135">Jeśli używany jest projekt użytkownika `packages.config` , skrypt programu MSBuild, który pobiera Analizator, nie jest odtwarzany, dlatego należy umieścić `install.ps1` i `uninstall.ps1` w `tools` folderze z zawartością, która jest opisana poniżej.</span><span class="sxs-lookup"><span data-stu-id="d50d8-135">If the user's project is using `packages.config`, the MSBuild script that picks up the analyzer does not come into play, so you should place `install.ps1` and `uninstall.ps1` in the `tools` folder with the contents that are described below.</span></span>

<span data-ttu-id="d50d8-136">**Zawartość plikuinstall.ps1**</span><span class="sxs-lookup"><span data-stu-id="d50d8-136">**install.ps1 file contents**</span></span>

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


<span data-ttu-id="d50d8-137">**Zawartość plikuuninstall.ps1**</span><span class="sxs-lookup"><span data-stu-id="d50d8-137">**uninstall.ps1 file contents**</span></span>

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
