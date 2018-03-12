---
title: Pakiet aktualizacji NuGet w programie PowerShell | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Odwołanie do polecenia programu PowerShell pakietu aktualizacji w konsoli Menedżera pakietów NuGet w programie Visual Studio."
keywords: "NuGet konsoli Menedżera pakietów, poleceń programu NuGet Powershell NuGet w programie PowerShell, pakiet aktualizacji"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 293d9a7fdcce633eb5a97e5f76398deb5c13bdb4
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/08/2018
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Pakiet aktualizacji (Konsola Menedżera pakietów w programie Visual Studio)

*Dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio w systemie Windows.*

Aktualizuje pakiet i jego zależności lub wszystkie pakiety w projekcie do nowszej wersji.

## <a name="syntax"></a>Składnia

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

W NuGet 2.8 + `Update-Package` można obniżyć istniejący pakiet w projekcie. Na przykład jeśli masz zainstalowany 5.1.0-rc1 Microsoft.AspNet.MVC następujące polecenie spowoduje obniżyć go 5.0.0:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parametry

|  Parametr | Opis |
| --- | --- |
| Id | Identyfikator pakietu do zaktualizowania. Pominięcie aktualizuje wszystkie pakiety. Id przełącznika sam jest opcjonalna. |
| IgnoreDependencies | Pomija zależności pakietu aktualizacji. |
| ProjectName | Nazwa projektu zawierającego pakietów aktualizacji, domyślnie używany do wszystkich projektów. |
| Wersja | Wersja do użycia podczas uaktualniania, domyślnie używany do najnowszej wersji. W NuGet 3.0 + wartość wersji musi być jedną z *najniższy, najwyższa, HighestMinor*, lub *HighestPatch* (równoważne - bezpieczny). |
| Bezpieczne | Ogranicza uaktualnienia do wersji tylko z tej samej wersji głównej i pomocniczej jako aktualnie zainstalowany pakiet. |
| Źródło | Adres URL lub folder ścieżka do źródła pakietu do wyszukania. Ścieżki folderu lokalnego może być bezwzględny, lub względem bieżącego folderu. Pominięcie `Uninstall-Package` wyszukiwania w obecnie wybranym źródle pakietów. |
| IncludePrerelease | Zawiera pakiety wersji wstępnej aktualizacji. |
| Zainstaluj ponownie | Pakiety Resintalls przy użyciu ich obecnie zainstalowanej wersji. Zobacz [ponowne zainstalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md). |
| FileConflictAction | Akcja wykonywana po otrzymaniu monitu, aby zastąpić, lub przycisk Ignoruj istniejące pliki odwołuje się projekt. Możliwe wartości to *zastępowania, Ignoruj, brak OverwriteAll*, i *IgnoreAll* (3.0 +). |
| DependencyVersion | Wersja pakietów zależności do użycia, które może być jedną z następujących czynności:<br/><ul><li>*Najniższa* (domyślnie): Najniższa wersja</li><li>*HighestPatch*: wersja z najniższą głównych, najniższy niewielkie, najwyższy poziom poprawki</li><li>*HighestMinor*: wersja z najniższą głównych, najwyższy niewielkie, najwyższy poziom poprawki</li><li>*Najwyższy* (domyślnie pakiet aktualizacji bez parametrów): najnowsza wersja</li></ul>Można ustawić przy użyciu wartości domyślnej [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) w `Nuget.Config` pliku. |
| ToHighestPatch | Ogranicza uaktualnienia do tylko wersji z tej samej wersji pomocniczej jako aktualnie zainstalowany pakiet. |
| Tohighestminor powoduje aktualizację | Ogranicza uaktualnienia do tylko wersji z taką samą wersję główną jako aktualnie zainstalowany pakiet. |
| WhatIf | Pokazuje, co się stanie, uruchamiając polecenie bez rzeczywistego wykonania aktualizacji. |

Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.

### <a name="common-parameters"></a>Wspólne parametry

`Update-Package` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.

### <a name="examples"></a>Przykłady

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```