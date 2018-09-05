---
title: Dokumentacja programu PowerShell Get pakiet NuGet
description: Odniesienie do polecenia PowerShell Get-pakiet w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a28b29614dfe5abdeb24438b3451d96634a120db
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551445"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (konsola menedżera pakietów w programie Visual Studio)

*W tym temacie opisano polecenia w ramach [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio na Windows. Ogólne polecenia PowerShell Get-Package, zobacz [dokumentacja programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Pobranie listy pakietów zainstalowanych w lokalnym repozytorium, zawiera listę pakietów, które są dostępne ze źródła pakietu, gdy jest używana z opcją - ListAvailable lub wyświetla ich listę dostępnych aktualizacji, gdy jest używana z przełącznikiem - Update.

## <a name="syntax"></a>Składnia

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Bez parametrów `Get-Package` umożliwia wyświetlenie listy pakietów zainstalowanych w projekt domyślny.

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Źródło | Ścieżka adresu URL lub folder pakietu. Ścieżki folderu lokalnego, może być ścieżką bezwzględną, lub względną do bieżącego folderu. W przypadku pominięcia `Get-Package` przeszukuje źródło obecnie wybranego pakietu. Gdy jest używane z - ListAvailable, wartość domyślna to nuget.org. |
| ListAvailable | Zawiera listę pakietów, które są dostępne ze źródła pakietu przyjęty adres nuget.org. Pokazuje domyślne pakietów 50, chyba że określono - PageSize i/lub - pierwszy. |
| Aktualizacje | Zawiera listę pakietów, które mają dostępną aktualizację ze źródła pakietu. |
| ProjectName | Projekt, z którego można pobrać zainstalowanych pakietów. Jeśli argument jest pominięty, zwraca zainstalowane projektów dla całego rozwiązania. |
| Filtr | Ciąg filtru, w celu zawężenia listy pakietów, stosując identyfikator pakietu, opis i tagów. |
| pierwszy | Liczba pakietów do zwrócenia z początku listy. Jeśli nie zostanie określony, wartość domyślna to 50. |
| Skip | Pomija pierwszy &lt;int&gt; pakiety z wyświetlonej listy.  |
| AllVersions | Wyświetla wszystkie dostępne wersje każdego pakietu, a nie tylko najnowszą wersję. |
| IncludePrerelease | Obejmuje pakiety w wersjach wstępnych, w wynikach. |
| PageSize | *(3.0 +)*  Stosowania przy użyciu - ListAvailable (wymagane), liczba pakietów na liście przed przekazaniem wiersz, aby kontynuować. |

Żaden z tych parametrów akceptuje znaków potoku danych wejściowych lub symbol wieloznaczny.

## <a name="common-parameters"></a>Wspólne parametry

`Get-Package` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja w przypadku błędu, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.

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
