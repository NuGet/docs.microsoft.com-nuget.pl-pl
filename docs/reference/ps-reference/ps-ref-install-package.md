---
title: Informacje o programie PowerShell Install-Package NuGet
description: Informacje dotyczące Install-Package programu PowerShell w konsoli Menedżer pakietów NuGet w programie Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: ad551b8701cfc2061f7721fb050ed9b5a4fede32
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901697"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (konsola Menedżer pakietów w programie Visual Studio)

*W tym temacie opisano polecenie w konsoli [Menedżer pakietów w](../../consume-packages/install-use-packages-powershell.md) Visual Studio w systemie Windows. Aby uzyskać ogólne polecenie Install-Package Programu PowerShell, zobacz informacje dotyczące polecenia [PackageManagement programu PowerShell.](/powershell/module/packagemanagement)*

Instaluje pakiet i jego zależności w projekcie.

## <a name="syntax"></a>Składnia

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

W programie NuGet 2.8+ można obniżyć poziom istniejącego `Install-Package` pakietu w projekcie. Jeśli na przykład masz zainstalowaną wersję Microsoft.AspNet.MVC 5.1.0-rc1, następujące polecenie obniży ją do wersji 5.0.0:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Id | (Wymagane) Identyfikator pakietu do zainstalowania. (*3.0+*) Identyfikator może być ścieżką lub adresem URL `packages.config` pliku lub `.nupkg` pliku. Sam przełącznik -Id jest opcjonalny. |
| IgnoreDependencies | Zainstaluj tylko ten pakiet, a nie jego zależności. |
| ProjectName | Projekt, w którym ma być instalowany pakiet , domyślnie domyślny projekt. |
| Element źródłowy | Adres URL lub ścieżka folderu dla źródła pakietu do wyszukania. Ścieżki folderów lokalnych mogą być bezwzględne lub względne względem bieżącego folderu. W przypadku pominięcia `Install-Package` program wyszukuje aktualnie wybrane źródło pakietu. |
| Wersja | Wersja pakietu do zainstalowania, domyślnie najnowsza wersja. |
| IncludePrerelease | Uwzględnia pakiety w wstępną aktualizację dla instalacji. W przypadku pominięcia są rozważane tylko stabilne pakiety. |
| FileConflictAction | Akcja do podjęcia po prośbie o zastąpienie lub zignorowanie istniejących plików, do których odwołuje się projekt. Możliwe wartości to *Overwrite, Ignore, None, OverwriteAll* i *(3.0+)* *IgnoreAll.* |
| DependencyVersion | Wersja pakietów zależności do użycia, która może być jedną z następujących wersji:<br/><ul><li>*Najniższa* (domyślna): najniższa wersja</li><li>*HighestPatch:* wersja z najniższą wersją główną, najmniejszą wersją pomocniczą, najwyższą poprawką</li><li>*HighestMinor:* wersja z najniższą wersją główną, najwyższą wersją pomocniczą, najwyższą poprawką</li><li>*Najwyższy* (domyślnie dla Update-Package bez parametrów): najwyższa wersja</li></ul>Wartość domyślną można ustawić przy [`dependencyVersion`](../nuget-config-file.md#config-section) użyciu ustawienia w pliku `Nuget.Config` . |
| Instrukcja WhatIf | Pokazuje, co się stanie w przypadku uruchomienia polecenia bez przeprowadzania instalacji. |

Żaden z tych parametrów nie akceptuje znaków wejściowych potoku ani symboli wieloznacznych.

## <a name="common-parameters"></a>Typowe parametry

`Install-Package` obsługuje następujące typowe [parametry programu PowerShell:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction i WarningVariable.

## <a name="examples"></a>Przykłady

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```