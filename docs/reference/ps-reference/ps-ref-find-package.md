---
title: Dokumentacja programu NuGet Find-Package PowerShell
description: Informacje dotyczące Find-Package polecenia programu PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 83d0d62bbda07d07ea1e3b58e531447e2001b680
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777515"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (konsola Menedżera pakietów w programie Visual Studio)

*Wersja 3.0 +; w tym temacie opisano polecenie w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows. Ogólne polecenie programu PowerShell Find-Package można znaleźć w [dokumentacji programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Pobiera zestaw pakietów zdalnych o określonym IDENTYFIKATORze lub słowach kluczowych ze źródła pakietu.

## <a name="syntax"></a>Składnia

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| &lt;Słowa kluczowe identyfikatora&gt; | Potrzeb Słowa kluczowe, które mają być używane podczas wyszukiwania źródła pakietu. Użyj-ExactMatch, aby zwrócić tylko te pakiety, których identyfikator pakietu pasuje do słów kluczowych. Jeśli nie podano słów kluczowych, `Find-Package` Funkcja zwraca listę 20 najważniejszych pakietów przez pobieranie lub numer określony przez-First. Należy pamiętać, że-ID jest opcjonalne i No-op. |
| Element źródłowy | Ścieżka adresu URL lub folderu dla źródła pakietu do przeszukania. Ścieżki folderu lokalnego mogą być bezwzględne lub względne w stosunku do bieżącego folderu. W przypadku pominięcia program `Find-Package` przeszukuje aktualnie wybrane źródło pakietu. |
| AllVersions | Wyświetla wszystkie dostępne wersje każdego pakietu, a nie tylko najnowszą wersję. |
| Pierwsze | Liczba pakietów do zwrócenia od początku listy; wartość domyślna to 20. |
| Pomiń | Pomija pierwsze &lt; &gt; pakiety int z wyświetlonej listy.  |
| IncludePrerelease | Zawiera pakiety wersji wstępnej w wynikach. |
| ExactMatch | Określono, aby używać &lt; słów kluczowych &gt; jako identyfikatora pakietu z uwzględnieniem wielkości liter. |
| StartWith | Zwraca pakiety, których identyfikator pakietu rozpoczyna się od &lt; słów kluczowych &gt; . |

Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.

## <a name="common-parameters"></a>Parametry wspólne

`Find-Package` obsługuje następujące [typowe parametry programu PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debugowanie, Akcja błędu, ErrorVariable, wybuforuj, subvariable, PipelineVariable, verbose, WarningAction i WarningVariable.

## <a name="examples"></a>Przykłady

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```