---
title: Dokumentacja programu PowerShell Update pakiet NuGet
description: Odniesienie do polecenia PowerShell pakietu aktualizacji w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a5b5a11ee11d9e2cf6a90d56ac63b1f7bad750ea
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496492"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Update-Package (konsola menedżera pakietów w programie Visual Studio)

*Dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio na Windows.*

Aktualizuje pakiet i jego zależności lub wszystkich pakietów w projekcie do nowszej wersji.

## <a name="syntax"></a>Składnia

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

W pakiecie NuGet 2.8 + `Update-Package` może służyć do obniżenia poziomu istniejący pakiet w projekcie. Na przykład w przypadku 5.1.0-rc1 Microsoft.AspNet.MVC zainstalowane następujące polecenie będzie obniżyć do 5.0.0:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parametry

|  Parametr | Opis |
| --- | --- |
| Id | Identyfikator pakiet do zaktualizowania. W przypadku pominięcia aktualizuje wszystkie pakiety. — Identyfikator samym przełączniku jest opcjonalne. |
| IgnoreDependencies | Pomija aktualizowanie zależności pakietów. |
| ProjectName | Nazwa projektu zawierający pakiety do aktualizacji, przyjęto wartość domyślną dla wszystkich projektów. |
| Wersja | Wersja do użycia podczas uaktualniania, ustawiając domyślnie do najnowszej wersji. Nuget 3.0 +, wartość wersji musi mieć jedną z *najniższy, najwyższa, HighestMinor*, lub *HighestPatch* (równoważne — bezpieczna). |
| Bezpieczne | Ogranicza uaktualnienia do wersji tylko przy użyciu tej samej wersji głównych i pomocniczych, co obecnie zainstalowanego pakietu. |
| Source | Adres URL lub folder ścieżka do źródła pakietu do wyszukania. Ścieżki folderu lokalnego, może być ścieżką bezwzględną, lub względną do bieżącego folderu. W przypadku pominięcia `Update-Package` przeszukuje źródło obecnie wybranego pakietu. |
| IncludePrerelease | Obejmuje pakiety w wersjach wstępnych dla aktualizacji. |
| Zainstaluj ponownie | Pakiety Resintalls przy użyciu ich obecnie zainstalowanej wersji. Zobacz [ponowne zainstalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md). |
| FileConflictAction | Akcja do wykonania po wyświetleniu monitu o zastąpienie lub zignorować istniejące pliki przywoływanego przez projekt. Możliwe wartości to *zastąpienia, Zignoruj, None, OverwriteAll*, i *IgnoreAll* (3.0 i nowsze). |
| DependencyVersion | Wersja pakietów zależności do użycia, które może być jedną z następujących czynności:<br/><ul><li>*Najniższy* (ustawienie domyślne): Najniższa wersja</li><li>*HighestPatch*: wersja przy najniższe główne, najniższą pomocnicza, najwyższy poziom poprawki</li><li>*HighestMinor*: wersji z najniższą główne, najwyższy pomocnicza, najwyższy poziom poprawki</li><li>*Najwyższy* (domyślnie dla pakietu aktualizacji bez parametrów): najwyższa wersja</li></ul>Można ustawić przy użyciu wartości domyślnej [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) ustawienie w `Nuget.Config` pliku. |
| ToHighestPatch | wartość równoważna — bezpieczne. |
| ToHighestMinor | Ogranicza uaktualnień tylko wersje z taką samą wersję główną jako aktualnie zainstalowany pakiet. |
| WhatIf | Pokazuje, co się stanie, podczas uruchamiania polecenia bez rzeczywistego wykonania aktualizacji. |

Żaden z tych parametrów akceptuje znaków potoku danych wejściowych lub symbol wieloznaczny.

### <a name="common-parameters"></a>Wspólne parametry

`Update-Package` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debugowanie, akcja w przypadku błędu, ErrorVariable, OutBuffer, OutVariable, PipelineVariable pełne, WarningAction i WarningVariable.

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
