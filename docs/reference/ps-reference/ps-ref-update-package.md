---
title: Aktualizacja NuGet — Dokumentacja programu PowerShell pakietu
description: Dokumentacja polecenia Update-Package programu PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e1bff9d4b7391d8be87afa4b8f2fbd51ae922140
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384859"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Update-Package (konsola menedżera pakietów w programie Visual Studio)

*Dostępne tylko w [konsoli Menedżera pakietów NuGet](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows.*

Aktualizuje pakiet i jego zależności lub wszystkie pakiety w projekcie do nowszej wersji.

## <a name="syntax"></a>Składnia

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

W programie NuGet 2.8 +, `Update-Package` może służyć do obniżenia poziomu istniejącego pakietu w projekcie. Na przykład jeśli masz zainstalowany plik Microsoft. AspNet. MVC 5.1.0-RC1, następujące polecenie obniży go do 5.0.0:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parametry

|  Parametr | Opis |
| --- | --- |
| Id | Identyfikator pakietu do zaktualizowania. W przypadku pominięcia program aktualizuje wszystkie pakiety. Przełącznik-ID jest opcjonalny. |
| IgnoreDependencies | Pomija aktualizowanie zależności pakietu. |
| ProjectName | Nazwa projektu zawierającego pakiety do zaktualizowania, domyślnie dla wszystkich projektów. |
| Wersja | Wersja, która ma zostać użyta do uaktualnienia, domyślna dla najnowszej wersji. W programie NuGet 3.0 + wartość wersji musi mieć jedną z *najniższych, najwyższego, HighestMinor*lub *HighestPatch* (równoważne z bezpiecznym). |
| Sejf | Ogranicza uaktualnienia do wersji tylko z tą samą wersją główną i pomocniczą jak aktualnie zainstalowany pakiet. |
| Obiekt źródłowy | Ścieżka adresu URL lub folderu dla źródła pakietu do przeszukania. Ścieżki folderu lokalnego mogą być bezwzględne lub względne w stosunku do bieżącego folderu. W przypadku pominięcia `Update-Package` przeszukuje aktualnie wybrane źródło pakietu. |
| IncludePrerelease | Obejmuje pakiety wersji wstępnej dla aktualizacji. |
| Ponowna instalacja | Resintalls pakiety przy użyciu ich aktualnie zainstalowanych wersji. Zobacz [ponowne instalowanie i aktualizowanie pakietów](../../consume-packages/reinstalling-and-updating-packages.md). |
| FileConflictAction | Akcja, która ma zostać podjęta po wyświetleniu monitu o zastąpienie lub zignorowanie istniejących plików, do których odwołuje się projekt. Możliwe wartości to *overwrite, IGNORE, None, OverwriteAll*i *IgnoreAll* (3.0 +). |
| DependencyVersion | Wersja pakietów zależności do użycia, która może być jedną z następujących:<br/><ul><li>*Najniższy* (domyślny): najniższa wersja</li><li>*HighestPatch*: wersja z najniższą główną, najmniejszą niewielką lub najwyższą poprawką</li><li>*HighestMinor*: wersja z najmniejszą główną, najwyższą niewielką lub najwyższą poprawką</li><li>*Najwyższe* (domyślnie dla pakietu aktualizacji bez parametrów): najwyższa wersja</li></ul>Wartość domyślną można ustawić przy użyciu ustawienia [`dependencyVersion`](../nuget-config-file.md#config-section) w pliku `Nuget.Config`. |
| ToHighestPatch | równoważne z bezpiecznym. |
| ToHighestMinor | Ogranicza uaktualnienia do wersji tylko z tą samą wersją główną jak aktualnie zainstalowany pakiet. |
| Instrukcja WhatIf | Pokazuje, co się stanie po uruchomieniu polecenia bez jego faktycznego wykonania. |

Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.

### <a name="common-parameters"></a>Parametry wspólne

`Update-Package` obsługuje następujące [typowe parametry programu PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debugowanie, Akcja błędu, ErrorVariable, buforowanie, subvariable, PipelineVariable, verbose, WarningAction i WarningVariable.

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
