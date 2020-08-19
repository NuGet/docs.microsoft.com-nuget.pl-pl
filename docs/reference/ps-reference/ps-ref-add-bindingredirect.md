---
title: Dokumentacja programu PowerShell Add-BindingRedirect
description: Dokumentacja polecenia Add-BindingRedirect środowiska PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: f5ba4bd8140fa8cac7da8bf1351ad5448671b768
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623126"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (konsola Menedżera pakietów w programie Visual Studio)

*Dostępne tylko w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows.*

Bada wszystkie zestawy w ścieżce wyjściowej projektu i dodaje przekierowania powiązań do pliku konfiguracji aplikacji lub sieci Web, jeśli jest to konieczne. To polecenie jest uruchamiane automatycznie podczas instalowania pakietu.

> [!NOTE]
> Dotyczy to tylko scenariuszy korzystających z pliku packages.config. Aby uzyskać więcej informacji, zobacz [Dokumentacja pliku packages.config NuGet](~/reference/packages-config.md).

Aby uzyskać szczegółowe informacje o przekierowaniach powiązań i o tym, dlaczego są używane, zobacz [przekierowywanie wersji zestawu](/dotnet/framework/configure-apps/redirect-assembly-versions) w dokumentacji programu .NET.

## <a name="syntax"></a>Składnia

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| ProjectName | Potrzeb Projekt, do którego mają zostać dodane przekierowania powiązań. Przełącznik-ProjectName jest opcjonalny. |

Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.

## <a name="common-parameters"></a>Parametry wspólne

`Add-BindingRedirect` obsługuje następujące [typowe parametry programu PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debugowanie, Akcja błędu, ErrorVariable, wybuforuj, subvariable, PipelineVariable, verbose, WarningAction i WarningVariable.

## <a name="examples"></a>Przykłady

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```
