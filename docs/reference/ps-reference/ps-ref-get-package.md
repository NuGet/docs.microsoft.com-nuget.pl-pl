---
title: Informacje o programie PowerShell Get-Package NuGet
description: Informacje dotyczące Get-Package programu PowerShell w konsoli Menedżer pakietów NuGet w programie Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 7c91faecaac2967c7a01dd81e72b9097e7bd6cae
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901736"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (konsola Menedżer pakietów w programie Visual Studio)

*W tym temacie opisano polecenie w konsoli [Menedżer pakietów w](../../consume-packages/install-use-packages-powershell.md) Visual Studio w systemie Windows. Aby uzyskać ogólne polecenie Get-Package Programu PowerShell, zobacz informacje dotyczące polecenia [PackageManagement programu PowerShell.](/powershell/module/packagemanagement)*

Pobiera listę pakietów zainstalowanych w repozytorium lokalnym, wyświetla listę pakietów dostępnych ze źródła pakietu, gdy są używane z przełącznikiem -ListAvailable, lub wyświetla listę dostępnych aktualizacji w przypadku korzystania z przełącznika -Update.

## <a name="syntax"></a>Składnia

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Bez parametrów program `Get-Package` wyświetla listę pakietów zainstalowanych w projekcie domyślnym.

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Element źródłowy | Adres URL lub ścieżka folderu dla pakietu . Ścieżki folderów lokalnych mogą być bezwzględne lub względne względem bieżącego folderu. W przypadku pominięcia `Get-Package` program wyszukuje aktualnie wybrane źródło pakietu. W przypadku korzystania z -ListAvailable wartość domyślna to nuget.org. |
| ListAvailable | Wyświetla listę pakietów dostępnych ze źródła pakietu, domyślnie nuget.org. Przedstawia domyślną wartość 50 pakietów, chyba że określono -PageSize i/lub -First. |
| Aktualizacje | Wyświetla listę pakietów, które mają aktualizację dostępną ze źródła pakietu. |
| ProjectName | Projekt, z którego mają zostać zainstalowane pakiety. W przypadku pominięcia funkcja zwraca zainstalowane projekty dla całego rozwiązania. |
| Filtr | Ciąg filtru używany do zawężenia listy pakietów przez zastosowanie go do identyfikatora pakietu, opisu i tagów. |
| Pierwsze | Liczba pakietów, które mają być zwracane od początku listy. Jeśli nie zostanie określony, wartość domyślna to 50. |
| Pomiń | Pomija pierwsze pakiety &lt; int &gt; z wyświetlonej listy.  |
| AllVersions | Wyświetla wszystkie dostępne wersje każdego pakietu, a nie tylko najnowszą wersję. |
| IncludePrerelease | Zawiera pakiety wytłaczania wstępnego w wynikach. |
| PageSize | *(3.0+)* W przypadku korzystania z polecenia z ciągiem -ListAvailable (wymagane) — liczba pakietów, które należy wyświetlić przed monitem o kontynuowanie. |

Żaden z tych parametrów nie akceptuje znaków wejściowych potoku ani symboli wieloznacznych.

## <a name="common-parameters"></a>Typowe parametry

`Get-Package` obsługuje następujące typowe [parametry programu PowerShell:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction i WarningVariable.

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