---
title: Dokumentacja programu NuGet Find-Package PowerShell
description: Dokumentacja polecenia Znajdź pakiet programu PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4bb6d090b97dd55fc1be0625855aab27a0d181c4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328220"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (konsola menedżera pakietów w programie Visual Studio)

*Wersja 3.0 +; w tym temacie opisano polecenie w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows. Aby zapoznać się z ogólnym poleceniem Znajdź pakiet programu PowerShell, zobacz [informacje dotyczące programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Pobiera zestaw pakietów zdalnych o określonym IDENTYFIKATORze lub słowach kluczowych ze źródła pakietu.

## <a name="syntax"></a>Składnia

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Słowa &lt;kluczowe identyfikatora&gt; | Potrzeb Słowa kluczowe, które mają być używane podczas wyszukiwania źródła pakietu. Użyj-ExactMatch, aby zwrócić tylko te pakiety, których identyfikator pakietu pasuje do słów kluczowych. Jeśli nie podano słów kluczowych `Find-Package` , funkcja zwraca listę 20 najważniejszych pakietów przez pobieranie lub numer określony przez-First. Należy pamiętać, że-ID jest opcjonalne i No-op. |
| Source | Ścieżka adresu URL lub folderu dla źródła pakietu do przeszukania. Ścieżki folderu lokalnego mogą być bezwzględne lub względne w stosunku do bieżącego folderu. W przypadku pominięcia program `Find-Package` przeszukuje aktualnie wybrane źródło pakietu. |
| AllVersions | Wyświetla wszystkie dostępne wersje każdego pakietu, a nie tylko najnowszą wersję. |
| pierwszego | Liczba pakietów do zwrócenia od początku listy; wartość domyślna to 20. |
| Skip | Pomija pierwsze &lt;pakiety int&gt; z wyświetlonej listy.  |
| IncludePrerelease | Zawiera pakiety wersji wstępnej w wynikach. |
| ExactMatch | Określono, aby &lt;używać&gt; słów kluczowych jako identyfikatora pakietu z uwzględnieniem wielkości liter. |
| StartWith | Zwraca pakiety, których identyfikator pakietu rozpoczyna &lt;się&gt;od słów kluczowych. |

Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.

## <a name="common-parameters"></a>Parametry wspólne

`Find-Package`Program obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debugowanie, Akcja błędu, ErrorVariable, wybuforuj, niezmienna, PipelineVariable, verbose, WarningAction i WarningVariable.

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
