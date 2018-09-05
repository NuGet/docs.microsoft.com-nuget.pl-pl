---
title: Formaty Analizatora platformy .NET kompilatora, NuGet
description: Konwencje analizatorów .NET, które spakowany i rozpowszechniać za pomocą pakietów NuGet, które implementują interfejs API lub biblioteki.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: a5ccbba5fbc189eb59acfdeb86a4a03dcf907a9a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547634"
---
# <a name="analyzer-nuget-formats"></a>Formaty NuGet analizatora

Platforma kompilatora .NET (znany także jako "Roslyn") umożliwiają deweloperom tworzenie [analizatory](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) który bada drzewa składnia i semantyka kod jest zapisywany. To zapewnia deweloperom sposób tworzenia i narzędziami do analizowania specyficznego dla domeny, takich jak te, które może pomóc Przewodnik użytkowania konkretnego interfejsu API lub biblioteki. Więcej informacji można znaleźć na [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) witryny typu wiki w witrynie GitHub. Zobacz też artykuł [Roslyn użycia do zapisania na żywo analizator kodu dla interfejsu API](https://msdn.microsoft.com/magazine/dn879356.aspx) w MSDN Magazine.

Analizatory się zwykle są spakowane i dystrybuowanych jako część pakietów NuGet, które implementują interfejs API lub biblioteki w danym.

Aby uzyskać dobrym przykładem, zobacz [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) pakiet, który ma następującą zawartość:

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

Właściwości plików, wchodzące w skład wyłączyć starszych reguł programu FxCop na rzecz implementacji analizatora, są umieszczane w `build` folderu.

Instalowanie i odinstalowywanie skrypty, które obsługują projektów przy użyciu `packages.config` są umieszczane w `tools`.

Należy również zauważyć, że ponieważ ten pakiet nie ma żadnych wymagań specyficznych dla platformy `platform` folderu zostanie pominięty.


## <a name="analyzers-path-format"></a>Format ścieżki analizatorów

Korzystanie z `analyzers` folderu jest podobny do celów [ustalać platformy docelowe](../create-packages/supporting-multiple-target-frameworks.md), z wyjątkiem specyfikatorów w ścieżce opisano zależności hosta development zamiast czas kompilacji. Ogólny format jest następujący:

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- **framework_name**: *opcjonalne* obszarze powierzchni interfejsu API programu .NET Framework zawartej bibliotek DLL, trzeba uruchomić program. `dotnet` nie ma obecnie jedyną prawidłową wartością ponieważ tylko hosta, który można uruchomić analizatory Roslyn. Jeśli żadne miejsce docelowe nie jest określony, biblioteki DLL są zakłada się, że dotyczą *wszystkich* elementów docelowych.
- **supported_language**: języka, dla której Biblioteka DLL ma zastosowanie, jeden z `cs` (C#) i `vb` (Visual Basic) i `fs` (F #). Język wskazuje, że analizator powinien być ładowany tylko do projektu przy użyciu tego języka. Jeśli język nie zostanie określony, a następnie przyjęto, że biblioteka DLL dotyczą *wszystkich* języki, które obsługują analizatorów.
- **analyzer_name**: Określa pliki DLL analizatora. Jeśli potrzebujesz dodatkowych plików innych niż bibliotek DLL, muszą być dołączone za pomocą plików elementów docelowych lub właściwości.


## <a name="install-and-uninstall-scripts"></a>Instalowanie i odinstalowywanie skryptów

Jeśli użytkownik projekcie są używani `packages.config`, skrypt programu MSBuild, który przejmuje Analizator nie dochodzą do głosu, więc należy `install.ps1` i `uninstall.ps1` w `tools` folder z zawartością, które są opisane poniżej.

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
