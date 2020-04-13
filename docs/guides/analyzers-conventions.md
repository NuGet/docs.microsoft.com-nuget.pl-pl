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
# <a name="analyzer-nuget-formats"></a>Formaty Analizatora NuGet

Platforma kompilatora .NET (znany również jako "Roslyn") umożliwia deweloperom tworzenie [analizatorów,](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) które badają drzewa składni i semantyki kodu, jak jest zapisywany. Dzięki temu deweloperzy mogą tworzyć narzędzia analizy specyficzne dla domeny, takie jak te, które pomogą w korzystaniu z określonego interfejsu API lub biblioteki. Więcej informacji można znaleźć na wiki [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub. Zobacz także [artykuł, Użyj Roslyn napisać analizator kodu na żywo dla interfejsu API](https://msdn.microsoft.com/magazine/dn879356.aspx) w MSDN Magazine.

Same analizatory są zazwyczaj pakowane i dystrybuowane jako część pakietów NuGet, które implementują interfejs API lub biblioteki, o których mowa.

Dobrym przykładem jest pakiet [System.Runtime.Analyzers,](https://www.nuget.org/packages/System.Runtime.Analyzers) który zawiera następującą zawartość:

- analizatory\dotnet\System.Runtime.Analyzers.dll
- analizatory\dotnet\cs\System.Runtime.CSharp.Analyzers.dll
- analizatory\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll
- build\System.Runtime.Analyzers.Common.props
- build\System.Runtime.Analyzers.props
- build\System.Runtime.CSharp.Analyzers.props
- kompilacja\System.Runtime.VisualBasic.Analyzers.props
- narzędzia\install.ps1
- narzędzia\odinstaluj.ps1

Jak widać, umieszczasz biblioteki DLL analizatora w folderze `analyzers` w pakiecie.

Pliki rekwizytów, które są dołączone do wyłączenia starszych reguł FxCop na `build` rzecz implementacji analizatora, są umieszczane w folderze.

Instalowanie i odinstalowywanie `packages.config` skryptów, które obsługują projekty, które są używane, są umieszczane w pliku `tools`.

Należy również zauważyć, że ponieważ ten pakiet `platform` nie ma wymagań specyficznych dla platformy, folder jest pomijany.


## <a name="analyzers-path-format"></a>Format ścieżki analizatorów

Użycie folderu `analyzers` jest podobny do używanego dla [struktur docelowych](../create-packages/supporting-multiple-target-frameworks.md), z wyjątkiem specyfikatorów w ścieżce opisują zależności hosta rozwoju zamiast czasu kompilacji. Ogólny format jest następujący:

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- **framework_name** i **wersja:** *opcjonalny* obszar powierzchni interfejsu API programu .NET Framework, który zawiera biblioteki DLL muszą być uruchamiane. `dotnet`jest obecnie jedyną prawidłową wartością, ponieważ Roslyn jest jedynym hostem, który może uruchamiać analizatory. Jeśli nie określono celu, zakłada się, że biblioteki DLL mają zastosowanie do *wszystkich* obiektów docelowych.
- **supported_language**: język, dla którego jest stosowana biblioteka `cs` DLL, `vb` jeden z (C#) i (Visual Basic) i `fs` (F#). Język wskazuje, że analizator powinien być ładowany tylko dla projektu przy użyciu tego języka. Jeśli nie określono języka, zakłada się, że biblioteka DLL będzie stosowana do *wszystkich* języków, które obsługują analizatory.
- **analyzer_name**: określa biblioteki DLL analizatora. Jeśli potrzebujesz dodatkowych plików poza bibliotekami DLL, muszą one zostać uwzględnione za pośrednictwem plików docelowych lub właściwości.


## <a name="install-and-uninstall-scripts"></a>Instalowanie i odinstalowywanie skryptów

Jeśli używany jest projekt `packages.config`użytkownika, skrypt MSBuild, który odbiera analizator, nie wchodzi w `install.ps1` `uninstall.ps1` grę, `tools` dlatego należy umieścić i w folderze z zawartością, która jest opisana poniżej.

**zawartość pliku install.ps1**

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


**odinstalowywanie.ps1 zawartość pliku**

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
