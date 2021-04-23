---
title: Informacje o programie PowerShell Find-Package NuGet
description: Informacje dotyczące Find-Package programu PowerShell w konsoli Menedżer pakietów NuGet w programie Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 263835da64340a13737b32ab54ab057cb640a080
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901762"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (konsola Menedżer pakietów w programie Visual Studio)

*Wersja 3.0 lub nowsza; W tym temacie opisano polecenie w konsoli [Menedżer pakietów w](../../consume-packages/install-use-packages-powershell.md) Visual Studio w systemie Windows. Aby uzyskać ogólne polecenie Find-Package Programu PowerShell, zobacz informacje dotyczące polecenia [PackageManagement programu PowerShell.](/powershell/module/packagemanagement)*

Pobiera zestaw pakietów zdalnych z określonym identyfikatorem lub słowami kluczowymi ze źródła pakietu.

## <a name="syntax"></a>Składnia

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Słowa kluczowe &lt; identyfikatora&gt; | (Wymagane) Słowa kluczowe do użycia podczas wyszukiwania źródła pakietu. Użyj -ExactMatch, aby zwrócić tylko te pakiety, których identyfikator pakietu jest taki sam jak słowa kluczowe. Jeśli nie podano żadnych słów kluczowych, program zwraca listę 20 pierwszych pakietów według plików do pobrania lub liczbę `Find-Package` określoną przez wartość -First. Pamiętaj, że parametr -Id jest opcjonalny i nie jest dostępny. |
| Element źródłowy | Adres URL lub ścieżka folderu dla źródła pakietu do wyszukania. Ścieżki folderów lokalnych mogą być bezwzględne lub względne względem bieżącego folderu. W przypadku pominięcia `Find-Package` program wyszukuje aktualnie wybrane źródło pakietu. |
| AllVersions | Wyświetla wszystkie dostępne wersje każdego pakietu, a nie tylko najnowszą wersję. |
| Pierwsze | Liczba pakietów, które mają być zwracane od początku listy; Wartość domyślna to 20. |
| Pomiń | Pomija pierwsze pakiety &lt; int &gt; z wyświetlonej listy.  |
| IncludePrerelease | Zawiera pakiety wytłaczania wstępnego w wynikach. |
| ExactMatch | Określana w celu &lt; &gt; używania słów kluczowych jako identyfikatora pakietu zróżnicowego wielkości liter. |
| StartWith | Zwraca pakiety, których identyfikator pakietu zaczyna się od &lt; słów kluczowych &gt; . |

Żaden z tych parametrów nie akceptuje znaków wejściowych potoku ani symboli wieloznacznych.

## <a name="common-parameters"></a>Typowe parametry

`Find-Package` obsługuje następujące typowe [parametry programu PowerShell:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction i WarningVariable.

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