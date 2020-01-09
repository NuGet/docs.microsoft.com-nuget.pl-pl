---
title: Dokumentacja programu NuGet Find-Package PowerShell
description: Dokumentacja polecenia Znajdź pakiet programu PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4118b5a38f80a2300b3945738315d56bda096f9a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384636"
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
| &gt; &lt;identyfikatorów słów kluczowych | Potrzeb Słowa kluczowe, które mają być używane podczas wyszukiwania źródła pakietu. Użyj-ExactMatch, aby zwrócić tylko te pakiety, których identyfikator pakietu pasuje do słów kluczowych. Jeśli nie podano słów kluczowych, `Find-Package` zwraca listę 20 najważniejszych pakietów przez pobieranie lub numer określony przez-First. Należy pamiętać, że-ID jest opcjonalne i No-op. |
| Obiekt źródłowy | Ścieżka adresu URL lub folderu dla źródła pakietu do przeszukania. Ścieżki folderu lokalnego mogą być bezwzględne lub względne w stosunku do bieżącego folderu. W przypadku pominięcia `Find-Package` przeszukuje aktualnie wybrane źródło pakietu. |
| AllVersions | Wyświetla wszystkie dostępne wersje każdego pakietu, a nie tylko najnowszą wersję. |
| Pierwsze | Liczba pakietów do zwrócenia od początku listy; wartość domyślna to 20. |
| Skip | Pomija pierwsze &lt;pakietów&gt; int z wyświetlonej listy.  |
| IncludePrerelease | Zawiera pakiety wersji wstępnej w wynikach. |
| ExactMatch | Określono używanie &lt;słów&gt; kluczowych jako identyfikatora pakietu z uwzględnieniem wielkości liter. |
| StartWith | Zwraca pakiety, których identyfikator pakietu rozpoczyna się od &lt;słów kluczowych&gt;. |

Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.

## <a name="common-parameters"></a>Parametry wspólne

`Find-Package` obsługuje następujące [typowe parametry programu PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debugowanie, Akcja błędu, ErrorVariable, buforowanie, subvariable, PipelineVariable, verbose, WarningAction i WarningVariable.

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
