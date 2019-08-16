---
title: Formaty analizatora .NET Compiler Platform dla narzędzia NuGet
description: Konwencje dla analizatorów .NET spakowane i dystrybuowane z pakietami NuGet, które implementują interfejs API lub bibliotekę.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 0a8db9f6c55b7e79f9b338119e0b3ac6cb7a1e35
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/15/2019
ms.locfileid: "69520595"
---
# <a name="analyzer-nuget-formats"></a><span data-ttu-id="5a83a-103">Formaty NuGet analizatora</span><span class="sxs-lookup"><span data-stu-id="5a83a-103">Analyzer NuGet formats</span></span>

<span data-ttu-id="5a83a-104">.NET Compiler Platform (znany również jako "Roslyn") umożliwia deweloperom tworzenie [analizatorów](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) , które analizują drzewo składni i semantykę kodu podczas jego pisania.</span><span class="sxs-lookup"><span data-stu-id="5a83a-104">The .NET Compiler Platform (also known as "Roslyn") allows developers to create [analyzers](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) that examine the syntax tree and semantics of code as it's being written.</span></span> <span data-ttu-id="5a83a-105">Pozwala to deweloperom na tworzenie specyficznych dla domeny narzędzi do analizy, takich jak te, które mogłyby ułatwić korzystanie z konkretnego interfejsu API lub biblioteki.</span><span class="sxs-lookup"><span data-stu-id="5a83a-105">This provides developers with a way to create domain-specific analysis tools, such as those that would help guide the use of a particular API or library.</span></span> <span data-ttu-id="5a83a-106">Więcej informacji można znaleźć na stronie wiki [platformy .NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub.</span><span class="sxs-lookup"><span data-stu-id="5a83a-106">You can find more information on the [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span></span> <span data-ttu-id="5a83a-107">Zobacz również artykuł Roslyn, [Aby napisać analizator kodu na żywo dla interfejsu API](https://msdn.microsoft.com/magazine/dn879356.aspx) w usłudze MSDN Magazine.</span><span class="sxs-lookup"><span data-stu-id="5a83a-107">Also see the article, [Use Roslyn to Write a Live Code Analyzer for your API](https://msdn.microsoft.com/magazine/dn879356.aspx) in MSDN Magazine.</span></span>

<span data-ttu-id="5a83a-108">Analizatory są zwykle spakowane i dystrybuowane jako część pakietów NuGet implementujących dany interfejs API lub bibliotekę.</span><span class="sxs-lookup"><span data-stu-id="5a83a-108">Analyzers themselves are typically packaged and distributed as part of the NuGet packages that implement the API or library in question.</span></span>

<span data-ttu-id="5a83a-109">Aby uzyskać dobry przykład, zobacz pakiet [System. Runtime. analizatory](https://www.nuget.org/packages/System.Runtime.Analyzers) , który ma następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="5a83a-109">For a good example, see the [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) package, which has the following contents:</span></span>

- <span data-ttu-id="5a83a-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="5a83a-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span></span>
- <span data-ttu-id="5a83a-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="5a83a-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span></span>
- <span data-ttu-id="5a83a-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="5a83a-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span></span>
- <span data-ttu-id="5a83a-113">build\System.Runtime.Analyzers.Common.props</span><span class="sxs-lookup"><span data-stu-id="5a83a-113">build\System.Runtime.Analyzers.Common.props</span></span>
- <span data-ttu-id="5a83a-114">build\System.Runtime.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="5a83a-114">build\System.Runtime.Analyzers.props</span></span>
- <span data-ttu-id="5a83a-115">build\System.Runtime.CSharp.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="5a83a-115">build\System.Runtime.CSharp.Analyzers.props</span></span>
- <span data-ttu-id="5a83a-116">build\System.Runtime.VisualBasic.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="5a83a-116">build\System.Runtime.VisualBasic.Analyzers.props</span></span>
- <span data-ttu-id="5a83a-117">tools\install.ps1</span><span class="sxs-lookup"><span data-stu-id="5a83a-117">tools\install.ps1</span></span>
- <span data-ttu-id="5a83a-118">tools\uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="5a83a-118">tools\uninstall.ps1</span></span>

<span data-ttu-id="5a83a-119">Jak widać, należy umieścić biblioteki DLL `analyzers` analizatora w folderze pakietu.</span><span class="sxs-lookup"><span data-stu-id="5a83a-119">As you can see, you place the analyzer DLLs into an `analyzers` folder in the package.</span></span>

<span data-ttu-id="5a83a-120">Pliki props, które są dołączone do wyłączania starszych reguł FxCop na korzyść implementacji analizatora, są umieszczane `build` w folderze.</span><span class="sxs-lookup"><span data-stu-id="5a83a-120">Props files, which are included to disable legacy FxCop rules in favor of the analyzer implementation, are placed in the `build` folder.</span></span>

<span data-ttu-id="5a83a-121">Instalowanie i odinstalowywanie skryptów, które obsługują `packages.config` projekty przy użyciu `tools`programu, są umieszczane w temacie.</span><span class="sxs-lookup"><span data-stu-id="5a83a-121">Install and uninstall scripts that support projects using `packages.config` are placed in `tools`.</span></span>

<span data-ttu-id="5a83a-122">Należy również zauważyć, że ponieważ ten pakiet nie ma wymagań specyficznych dla `platform` platformy, folder zostanie pominięty.</span><span class="sxs-lookup"><span data-stu-id="5a83a-122">Also note that because this package has no platform-specific requirements, the `platform` folder is omitted.</span></span>


## <a name="analyzers-path-format"></a><span data-ttu-id="5a83a-123">Format ścieżki analizatorów</span><span class="sxs-lookup"><span data-stu-id="5a83a-123">Analyzers path format</span></span>

<span data-ttu-id="5a83a-124">Użycie `analyzers` folderu jest podobne do programu, który jest używany dla [platform docelowych](../create-packages/supporting-multiple-target-frameworks.md), z wyjątkiem specyfikatorów w ścieżce opisują zależności hosta deweloperskiego, a nie czas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="5a83a-124">The use of the `analyzers` folder is similar to that used for [target frameworks](../create-packages/supporting-multiple-target-frameworks.md), except the specifiers in the path describe development host dependencies instead of build-time.</span></span> <span data-ttu-id="5a83a-125">Format ogólny jest następujący:</span><span class="sxs-lookup"><span data-stu-id="5a83a-125">The general format is as follows:</span></span>

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- <span data-ttu-id="5a83a-126">**framework_name**: *opcjonalny* obszar powierzchni interfejsu API .NET Framework należy uruchomić zawarte w niej biblioteki DLL.</span><span class="sxs-lookup"><span data-stu-id="5a83a-126">**framework_name**: the *optional* API surface area of the .NET Framework that the contained DLLs need to run.</span></span> <span data-ttu-id="5a83a-127">`dotnet`jest obecnie jedyną prawidłową wartością, ponieważ Roslyn jest jedynym hostem, który może uruchamiać analizatory.</span><span class="sxs-lookup"><span data-stu-id="5a83a-127">`dotnet` is presently the only valid value because Roslyn is the only host that can run analyzers.</span></span> <span data-ttu-id="5a83a-128">Jeśli nie określono elementu docelowego, zakłada się, że biblioteki DLL są stosowane do *wszystkich* elementów docelowych.</span><span class="sxs-lookup"><span data-stu-id="5a83a-128">If no target is specified, DLLs are assumed to apply to *all* targets.</span></span>
- <span data-ttu-id="5a83a-129">**supported_language**: język, dla którego stosowana jest biblioteka DLL, jedna `cs` zC#() `vb` i (Visual Basic) i `fs` (F#).</span><span class="sxs-lookup"><span data-stu-id="5a83a-129">**supported_language**: the language for which the DLL applies, one of `cs` (C#) and `vb` (Visual Basic), and `fs` (F#).</span></span> <span data-ttu-id="5a83a-130">Język wskazuje, że analizator powinien być załadowany tylko dla projektu używającego tego języka.</span><span class="sxs-lookup"><span data-stu-id="5a83a-130">The language indicates that the analyzer should be loaded only for a project using that language.</span></span> <span data-ttu-id="5a83a-131">Jeśli nie określono żadnego języka, przyjęto, że biblioteka DLL ma zastosowanie do *wszystkich* języków, które obsługują analizatory.</span><span class="sxs-lookup"><span data-stu-id="5a83a-131">If no language is specified then the DLL is assumed to apply to *all* languages that support analyzers.</span></span>
- <span data-ttu-id="5a83a-132">**analyzer_name**: określa biblioteki DLL analizatora.</span><span class="sxs-lookup"><span data-stu-id="5a83a-132">**analyzer_name**: specifies the DLLs of the analyzer.</span></span> <span data-ttu-id="5a83a-133">Jeśli potrzebujesz dodatkowych plików poza biblioteką DLL, muszą one być dołączone do plików obiektów docelowych lub właściwości.</span><span class="sxs-lookup"><span data-stu-id="5a83a-133">If you need additional files beyond DLLs, they must be included through a targets or properties files.</span></span>


## <a name="install-and-uninstall-scripts"></a><span data-ttu-id="5a83a-134">Instalowanie i odinstalowywanie skryptów</span><span class="sxs-lookup"><span data-stu-id="5a83a-134">Install and uninstall scripts</span></span>

<span data-ttu-id="5a83a-135">Jeśli używany `packages.config`jest projekt użytkownika, skrypt programu MSBuild, który pobiera Analizator, nie jest odtwarzany, dlatego należy umieścić `install.ps1` i `uninstall.ps1` w `tools` folderze z zawartością, która jest opisana poniżej.</span><span class="sxs-lookup"><span data-stu-id="5a83a-135">If the user's project is using `packages.config`, the MSBuild script that picks up the analyzer does not come into play, so you should place `install.ps1` and `uninstall.ps1` in the `tools` folder with the contents that are described below.</span></span>

<span data-ttu-id="5a83a-136">**zawartość pliku Install. ps1**</span><span class="sxs-lookup"><span data-stu-id="5a83a-136">**install.ps1 file contents**</span></span>

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


<span data-ttu-id="5a83a-137">**Odinstaluj zawartość pliku. ps1**</span><span class="sxs-lookup"><span data-stu-id="5a83a-137">**uninstall.ps1 file contents**</span></span>

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
