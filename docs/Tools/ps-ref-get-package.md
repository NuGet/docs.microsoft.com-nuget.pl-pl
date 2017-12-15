---
title: Get pakiet NuGet w programie PowerShell | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 42476008-64b3-480e-a966-98b2fa38b681
description: "Dokumentacja dotycząca polecenia PowerShell Get-pakietu w konsoli Menedżera pakietów NuGet w programie Visual Studio."
keywords: "NuGet konsoli Menedżera pakietów, poleceń programu NuGet Powershell NuGet w programie PowerShell, Pobierz pakiet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3f93ab82e9fb769ee20070aa39ba8e3e05953839
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (Konsola Menedżera pakietów w programie Visual Studio)

*W tym temacie opisano polecenia w [Konsola Menedżera pakietów NuGet](Package-Manager-Console.md) w programie Visual Studio w systemie Windows. Ogólny polecenia PowerShell Get-Package, zobacz [odwołania programu PowerShell PackageManagement](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6).*

Pobiera listę pakietów zainstalowanych w lokalnym repozytorium, zawiera listę pakietów dostępnych ze źródła pakietu, gdy jest używany z flagą - ListAvailable przełącznika lub wymieniono dostępne aktualizacje, gdy jest używany z przełącznikiem - Update.

## <a name="syntax"></a>Składnia

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Bez parametrów `Get-Package` Wyświetla listę pakietów zainstalowanych w projekcie domyślnym.

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Źródło | Ścieżka adresu URL lub folderu pakietu. Ścieżki folderu lokalnego może być bezwzględny, lub względem bieżącego folderu. Pominięcie `Get-Package` wyszukiwania w obecnie wybranym źródle pakietów. W przypadku korzystania z flagą-ListAvailable, wartość domyślna to nuget.org. |
| Flagą ListAvailable | Wyświetla listę dostępnych pakietów ze źródła pakietu przyjęty nuget.org. Pokazuje domyślnie 50 pakietów, chyba że określono - PageSize i/lub - pierwszy. |
| Aktualizacje | Wyświetla listę pakietów, które mają jest dostępna aktualizacja w źródle pakietów. |
| ProjectName | Projekt, z którego ma zostać pobrane zainstalowane pakiety. Pominięcie zwraca zainstalowane projekty dla całego rozwiązania. |
| Filtr | Ciąg filtru używany do zawężania listy pakietów, uwzględniając identyfikator pakietu, opisie i tagach. |
| pierwszy | Liczba pakietów do zwrócenia z początku listy. Jeśli nie zostanie określony, domyślnie 50. |
| Skip | Pominięto pierwszy &lt;int&gt; pakiety z wyświetlonej listy.  |
| AllVersions | Wyświetla wszystkie dostępne wersje każdego pakietu, a nie tylko najnowszą wersję. |
| IncludePrerelease | Zawiera pakiety wersji wstępnej w wynikach. |
| Wartość PageSize | *(3.0 +)*  Podczas używane z flagą-ListAvailable (wymagane), liczba pakietów, aby wyświetlić listę przed przekazaniem wiersza, aby kontynuować. |

Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.

## <a name="common-parameters"></a>Wspólne parametry

`Get-Package`obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.

## <a name="examples"></a>Przykłady

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```

