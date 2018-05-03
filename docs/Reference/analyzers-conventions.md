---
title: Formaty Analizatora platformy .NET kompilatora, NuGet
description: Konwencje dotyczące analizatorów .NET, które są umieszczone i rozpowszechnianej za pomocą pakietów NuGet, które implementują interfejs API lub biblioteki.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 57ab485c8062b0515c292b68ecb5a3628b6e3e9d
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2018
---
# <a name="analyzer-nuget-formats"></a>Analizator NuGet formatów

Kompilator platformy .NET (znanej także jako "Roslyn") umożliwiają deweloperom tworzenie [analizatorów](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) który bada drzewa składni i semantyki kod jest zapisywany. To zapewnia deweloperom sposób tworzenia i narzędzi analizy specyficznego dla domeny, takich jak te, które mogłyby ułatwić Podręcznik użycia określonego interfejsu API lub biblioteki. Więcej informacji można znaleźć na [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) typu wiki w witrynie GitHub. Zobacz również artykuł, [Roslyn używany do zapisywania na żywo analizator kodu dla interfejsu API](https://msdn.microsoft.com/magazine/dn879356.aspx) w witrynie MSDN Magazine.

Analizatory samych zazwyczaj są umieszczone i rozproszonych w ramach pakietów NuGet, które implementują interfejs API lub biblioteki w.

Aby uzyskać przykład, zobacz [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) pakiet, który ma następującą zawartość:

- analyzers\dotnet\System.Runtime.Analyzers.dll
- analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll
- analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll
- build\System.Runtime.Analyzers.Common.props
- build\System.Runtime.Analyzers.props
- build\System.Runtime.CSharp.Analyzers.props
- build\System.Runtime.VisualBasic.Analyzers.props
- tools\install.ps1
- tools\uninstall.ps1

Jak widać, umieść biblioteki DLL analizatora do `analyzers` folderu w pakiecie.

Pliki właściwości, które są włączone, aby je wyłączyć starszej wersji programu FxCop na rzecz implementacji analizatora, są umieszczane w `build` folderu.

Instalowanie i odinstalowywanie skrypty, które obsługują projektów przy użyciu `packages.config` są umieszczane w `tools`.

Należy również zauważyć, że ponieważ ten pakiet nie ma specyficznego dla platformy wymagań, `platform` folderu zostanie pominięty.


## <a name="analyzers-path-format"></a>Format ścieżki analizatorów

Korzystanie z `analyzers` folder jest podobny do celów [platform docelowych](../create-packages/supporting-multiple-target-frameworks.md), z wyjątkiem Specyfikatory w ścieżce opisano programowanie hosta zależności, zamiast czas kompilacji. Ogólny format jest następujący:

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}}/{analyzer_name}.dll

- **framework_name**: *opcjonalne* powierzchni interfejsu API programu .NET Framework zawartej biblioteki DLL potrzebne do uruchomienia. `dotnet` nie ma obecnie jedyną prawidłową wartością ponieważ Roslyn jest tylko hosta, który można uruchomić analizatorów. Jeśli docelowy nie zostanie określony, biblioteki DLL uznaje się, że dotyczą *wszystkie* elementy docelowe.
- **supported_language**: język, dla którego plik DLL, który ma zastosowanie, jeden z `cs` (C#) i `vb` (Visual Basic), a `fs` (F #). Język wskazuje, że analizatora powinny być ładowane tylko do projektu przy użyciu tego języka. Jeśli język nie zostanie określony, a następnie przyjęto, że biblioteka DLL dotyczą *wszystkie* języków, które obsługują analizatorów.
- **analyzer_name**: Określa bibliotek DLL analizatora. Jeśli potrzebujesz dodatkowych plików poza biblioteki DLL muszą być dodane przez pliki elementów docelowych lub właściwości.


## <a name="install-and-uninstall-scripts"></a>Instalowanie i odinstalowywanie skryptów

Jeśli projekt użytkownika jest za pomocą `packages.config`, skrypt MSBuild, który przejmuje analizatora nie jest dostarczany do gry, zaleca się `install.ps1` i `uninstall.ps1` w `tools` folder z zawartością, które są opisane poniżej.

**zawartość pliku Install.ps1**

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


**zawartość pliku Uninstall.ps1**

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
