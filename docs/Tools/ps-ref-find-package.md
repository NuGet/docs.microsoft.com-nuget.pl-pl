---
title: "Znajdź pakiet NuGet w programie PowerShell | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 2f7b8847-8259-4366-98c0-13cab88d6e1b
description: "Odwołanie do polecenia programu PowerShell Znajdź pakiet w konsoli Menedżera pakietów NuGet w programie Visual Studio."
keywords: "NuGet konsoli Menedżera pakietów, poleceń programu NuGet Powershell NuGet w programie PowerShell, Znajdź pakiet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b6af6098da9c00e47b81ac9ec37bd5210a99a9fe
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Znajdź pakiet (Konsola Menedżera pakietów w programie Visual Studio)

*W wersji 3.0 +; w tym temacie opisano polecenia w [Konsola Menedżera pakietów NuGet](Package-Manager-Console.md) w programie Visual Studio w systemie Windows. Ogólny polecenia pakiet Znajdź PowerShell, zobacz [odwołania programu PowerShell PackageManagement](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6).*

Pobiera zestaw pakietów zdalnych z określonym Identyfikatorem lub słowa kluczowe w źródle pakietów.

## <a name="syntax"></a>Składnia

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Identyfikator &lt;słowa kluczowe&gt; | (Wymagane) Słowa kluczowe używane podczas wyszukiwania w źródle pakietów. Użyj - ExactMatch mają być zwracane tylko pakiety o identyfikatorze pakietu pasuje słów kluczowych. Jeśli podano słów kluczowych, `Find-Package` zwraca listę pakietów pierwsza 20. wg pliki do pobrania lub numer określony przez — jako pierwszy. Należy pamiętać, że - Id jest opcjonalna i zerowa. |
| Źródło | Adres URL lub folder ścieżka do źródła pakietu do wyszukania. Ścieżki folderu lokalnego może być bezwzględny, lub względem bieżącego folderu. Pominięcie `Find-Package` wyszukiwania w obecnie wybranym źródle pakietów. |
| AllVersions | Wyświetla wszystkie dostępne wersje każdego pakietu, a nie tylko najnowszą wersję. |
| pierwszy | Liczba pakietów do zwrócenia z początku listy; Wartość domyślna to 20. |
| Skip | Pominięto pierwszy &lt;int&gt; pakiety z wyświetlonej listy.  |
| IncludePrerelease | Zawiera pakiety wersji wstępnej w wynikach. |
| ExactMatch | Określona do użycia &lt;słowa kluczowe&gt; jako identyfikatora pakietu z uwzględnieniem wielkości liter. |
| StartWith | Zwraca pakiety pakiet, którego rozpoczyna się od Identyfikatora &lt;słowa kluczowe&gt;. |

Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.

## <a name="common-parameters"></a>Wspólne parametry

`Find-Package`obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.

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
