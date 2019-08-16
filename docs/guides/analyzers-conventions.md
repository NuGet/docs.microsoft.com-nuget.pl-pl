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
# <a name="analyzer-nuget-formats"></a>Formaty NuGet analizatora

.NET Compiler Platform (znany również jako "Roslyn") umożliwia deweloperom tworzenie [analizatorów](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) , które analizują drzewo składni i semantykę kodu podczas jego pisania. Pozwala to deweloperom na tworzenie specyficznych dla domeny narzędzi do analizy, takich jak te, które mogłyby ułatwić korzystanie z konkretnego interfejsu API lub biblioteki. Więcej informacji można znaleźć na stronie wiki [platformy .NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub. Zobacz również artykuł Roslyn, [Aby napisać analizator kodu na żywo dla interfejsu API](https://msdn.microsoft.com/magazine/dn879356.aspx) w usłudze MSDN Magazine.

Analizatory są zwykle spakowane i dystrybuowane jako część pakietów NuGet implementujących dany interfejs API lub bibliotekę.

Aby uzyskać dobry przykład, zobacz pakiet [System. Runtime. analizatory](https://www.nuget.org/packages/System.Runtime.Analyzers) , który ma następującą zawartość:

- analyzers\dotnet\System.Runtime.Analyzers.dll
- analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll
- analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll
- build\System.Runtime.Analyzers.Common.props
- build\System.Runtime.Analyzers.props
- build\System.Runtime.CSharp.Analyzers.props
- build\System.Runtime.VisualBasic.Analyzers.props
- tools\install.ps1
- tools\uninstall.ps1

Jak widać, należy umieścić biblioteki DLL `analyzers` analizatora w folderze pakietu.

Pliki props, które są dołączone do wyłączania starszych reguł FxCop na korzyść implementacji analizatora, są umieszczane `build` w folderze.

Instalowanie i odinstalowywanie skryptów, które obsługują `packages.config` projekty przy użyciu `tools`programu, są umieszczane w temacie.

Należy również zauważyć, że ponieważ ten pakiet nie ma wymagań specyficznych dla `platform` platformy, folder zostanie pominięty.


## <a name="analyzers-path-format"></a>Format ścieżki analizatorów

Użycie `analyzers` folderu jest podobne do programu, który jest używany dla [platform docelowych](../create-packages/supporting-multiple-target-frameworks.md), z wyjątkiem specyfikatorów w ścieżce opisują zależności hosta deweloperskiego, a nie czas kompilacji. Format ogólny jest następujący:

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- **framework_name**: *opcjonalny* obszar powierzchni interfejsu API .NET Framework należy uruchomić zawarte w niej biblioteki DLL. `dotnet`jest obecnie jedyną prawidłową wartością, ponieważ Roslyn jest jedynym hostem, który może uruchamiać analizatory. Jeśli nie określono elementu docelowego, zakłada się, że biblioteki DLL są stosowane do *wszystkich* elementów docelowych.
- **supported_language**: język, dla którego stosowana jest biblioteka DLL, jedna `cs` zC#() `vb` i (Visual Basic) i `fs` (F#). Język wskazuje, że analizator powinien być załadowany tylko dla projektu używającego tego języka. Jeśli nie określono żadnego języka, przyjęto, że biblioteka DLL ma zastosowanie do *wszystkich* języków, które obsługują analizatory.
- **analyzer_name**: określa biblioteki DLL analizatora. Jeśli potrzebujesz dodatkowych plików poza biblioteką DLL, muszą one być dołączone do plików obiektów docelowych lub właściwości.


## <a name="install-and-uninstall-scripts"></a>Instalowanie i odinstalowywanie skryptów

Jeśli używany `packages.config`jest projekt użytkownika, skrypt programu MSBuild, który pobiera Analizator, nie jest odtwarzany, dlatego należy umieścić `install.ps1` i `uninstall.ps1` w `tools` folderze z zawartością, która jest opisana poniżej.

**zawartość pliku Install. ps1**

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


**Odinstaluj zawartość pliku. ps1**

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
