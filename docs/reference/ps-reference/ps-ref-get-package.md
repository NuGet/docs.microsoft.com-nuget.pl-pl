---
title: Dokumentacja poleceń Get-Package programu NuGet
description: Dokumentacja polecenia Get-Package programu PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 431e5f292f069ad5eb0c9f7f511d6b06810c8760
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328208"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (konsola menedżera pakietów w programie Visual Studio)

*W tym temacie opisano polecenie w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows. Aby zapoznać się z ogólnym poleceniem Get-Package programu PowerShell, zobacz [informacje dotyczące programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Pobiera listę pakietów zainstalowanych w repozytorium lokalnym, wyświetla listę pakietów dostępnych ze źródła pakietów, gdy jest używany z przełącznikiem-ListAvailable lub wyświetla listę dostępnych aktualizacji, gdy jest używany z przełącznikiem-Update.

## <a name="syntax"></a>Składnia

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Bez parametrów, `Get-Package` wyświetla listę pakietów zainstalowanych w domyślnym projekcie.

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Source | Ścieżka adresu URL lub folderu dla pakietu. Ścieżki folderu lokalnego mogą być bezwzględne lub względne w stosunku do bieżącego folderu. W przypadku pominięcia program `Get-Package` przeszukuje aktualnie wybrane źródło pakietu. W przypadku użycia z opcją-ListAvailable wartość domyślna to nuget.org. |
| ListAvailable | Wyświetla listę pakietów dostępnych ze źródła pakietów, domyślnie nuget.org. Wyświetla domyślnie 50 pakietów, chyba że są określone wartości-PageSize i/lub-First. |
| Aktualizacje | Wyświetla listę pakietów z aktualizacją dostępną w źródle pakietu. |
| ProjectName | Projekt, z którego mają zostać pobrane zainstalowane pakiety. W przypadku pominięcia zwraca zainstalowane projekty dla całego rozwiązania. |
| Filtr | Ciąg filtru służący do zawężenia listy pakietów przez zastosowanie jej do identyfikatora pakietu, opisu i tagów. |
| pierwszego | Liczba pakietów do zwrócenia od początku listy. Jeśli nie zostanie określony, wartość domyślna to 50. |
| Skip | Pomija pierwsze &lt;pakiety int&gt; z wyświetlonej listy.  |
| AllVersions | Wyświetla wszystkie dostępne wersje każdego pakietu, a nie tylko najnowszą wersję. |
| IncludePrerelease | Zawiera pakiety wersji wstępnej w wynikach. |
| PageSize | *(3.0 +)* Jeśli jest używany z-ListAvailable (required), liczba pakietów do wyświetlenia przed podawaniem monitu o kontynuowanie. |

Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.

## <a name="common-parameters"></a>Parametry wspólne

`Get-Package`Program obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debugowanie, Akcja błędu, ErrorVariable, wybuforuj, niezmienna, PipelineVariable, verbose, WarningAction i WarningVariable.

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
