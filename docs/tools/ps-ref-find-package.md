---
title: Dokumentacja programu PowerShell Znajdź — pakiet NuGet
description: Odniesienie do polecenia PowerShell Znajdź pakiet w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: fee0ad0496f27d0796eddf177edc235bcb10da70
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842521"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (konsola menedżera pakietów w programie Visual Studio)

*W wersji 3.0 +; w tym temacie opisano polecenia w ramach [Konsola Menedżera pakietów](package-manager-console.md) w programie Visual Studio na Windows. Ogólne polecenia programu PowerShell Znajdź-Package, zobacz [dokumentacja programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Pobiera zbiór pakiety zdalne przy użyciu określonego Identyfikatora lub słowa kluczowe ze źródła pakietu.

## <a name="syntax"></a>Składnia

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Identyfikator &lt;słów kluczowych&gt; | (Wymagane) Słowa kluczowe do użycia podczas wyszukiwania źródła pakietu. Użyj - ExactMatch, aby zwrócić tylko pakiety o identyfikatorze pakietu dopasowuje słowa kluczowe. Jeśli zostanie podany żadnych słów kluczowych, `Find-Package` zwraca listę pakietów 20 najpopularniejszych przez pliki do pobrania lub liczba określone przez — najpierw. Należy pamiętać, że - Id jest opcjonalna i pusta. |
| Source | Adres URL lub folder ścieżka do źródła pakietu do wyszukania. Ścieżki folderu lokalnego, może być ścieżką bezwzględną, lub względną do bieżącego folderu. W przypadku pominięcia `Find-Package` przeszukuje źródło obecnie wybranego pakietu. |
| AllVersions | Wyświetla wszystkie dostępne wersje każdego pakietu, a nie tylko najnowszą wersję. |
| pierwszy | Liczba pakietów do zwrócenia z początku listy; Wartość domyślna to 20. |
| Skip | Pomija pierwszy &lt;int&gt; pakiety z wyświetlonej listy.  |
| IncludePrerelease | Obejmuje pakiety w wersjach wstępnych, w wynikach. |
| ExactMatch | Określony do użycia &lt;słowa kluczowe&gt; jako identyfikator pakietu jest wielkość liter. |
| StartWith | Zwraca pakiety pakiet, którego identyfikator rozpoczyna się od &lt;słowa kluczowe&gt;. |

Żaden z tych parametrów akceptuje znaków potoku danych wejściowych lub symbol wieloznaczny.

## <a name="common-parameters"></a>Wspólne parametry

`Find-Package` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debugowanie, akcja w przypadku błędu, ErrorVariable, OutBuffer, OutVariable, PipelineVariable pełne, WarningAction i WarningVariable.

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
