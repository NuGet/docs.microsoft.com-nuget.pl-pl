---
title: NuGet BindingRedirect w programie PowerShell
description: Odwołanie do polecenia programu PowerShell Dodaj BindingRedirect w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: f3addd95b64d78eac201deeb2c64915ea935cd71
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817626"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (konsola menedżera pakietów w programie Visual Studio)

*Dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio w systemie Windows.*

Sprawdza wszystkie zestawy w ścieżce wyjściowej dla projektu i dodaje przekierowania powiązania do pliku konfiguracji aplikacji lub sieci web, w miarę potrzeby. To polecenie jest uruchamiane automatycznie podczas instalowania pakietu.

Aby uzyskać szczegółowe informacje na powiązanie przekierowania i dlaczego ich użycia, zobacz [przekierowywanie wersji zestawu](/dotnet/framework/configure-apps/redirect-assembly-versions) w dokumentacji programu .NET.

## <a name="syntax"></a>Składnia

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| ProjectName | (Wymagane) Projekt, do którego mają zostać dodane przekierowania wiązań. Przełącznika - NazwaProjektu sam jest opcjonalna. |

Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.

## <a name="common-parameters"></a>Wspólne parametry

`Add-BindingRedirect` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.

## <a name="examples"></a>Przykłady

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```