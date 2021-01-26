---
title: Dokumentacja programu NuGet Get-Package PowerShell
description: Informacje dotyczące Get-Package polecenia programu PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8394f888ec3d5e57eacd351a4867173da1070ead
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777499"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (konsola Menedżera pakietów w programie Visual Studio)

*W tym temacie opisano polecenie w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows. Ogólne polecenie programu PowerShell Get-Package można znaleźć w [dokumentacji programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

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
| Element źródłowy | Ścieżka adresu URL lub folderu dla pakietu. Ścieżki folderu lokalnego mogą być bezwzględne lub względne w stosunku do bieżącego folderu. W przypadku pominięcia program `Get-Package` przeszukuje aktualnie wybrane źródło pakietu. W przypadku użycia z opcją-ListAvailable wartość domyślna to nuget.org. |
| ListAvailable | Wyświetla listę pakietów dostępnych ze źródła pakietów, domyślnie nuget.org. Wyświetla domyślnie 50 pakietów, chyba że są określone wartości-PageSize i/lub-First. |
| Aktualizacje | Wyświetla listę pakietów z aktualizacją dostępną w źródle pakietu. |
| ProjectName | Projekt, z którego mają zostać pobrane zainstalowane pakiety. W przypadku pominięcia zwraca zainstalowane projekty dla całego rozwiązania. |
| Filtr | Ciąg filtru służący do zawężenia listy pakietów przez zastosowanie jej do identyfikatora pakietu, opisu i tagów. |
| Pierwsze | Liczba pakietów do zwrócenia od początku listy. Jeśli nie zostanie określony, wartość domyślna to 50. |
| Pomiń | Pomija pierwsze &lt; &gt; pakiety int z wyświetlonej listy.  |
| AllVersions | Wyświetla wszystkie dostępne wersje każdego pakietu, a nie tylko najnowszą wersję. |
| IncludePrerelease | Zawiera pakiety wersji wstępnej w wynikach. |
| PageSize | *(3.0 +)* Jeśli jest używany z-ListAvailable (required), liczba pakietów do wyświetlenia przed podawaniem monitu o kontynuowanie. |

Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.

## <a name="common-parameters"></a>Parametry wspólne

`Get-Package` obsługuje następujące [typowe parametry programu PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debugowanie, Akcja błędu, ErrorVariable, wybuforuj, subvariable, PipelineVariable, verbose, WarningAction i WarningVariable.

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