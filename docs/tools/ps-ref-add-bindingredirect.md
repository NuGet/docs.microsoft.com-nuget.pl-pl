---
title: Dokumentacja programu PowerShell NuGet BindingRedirect
description: Dokumentacja poleceń programu PowerShell Dodaj BindingRedirect w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: dec7db04c5cf239863b9c00e9f5bc0dde42c7e47
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551660"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (konsola menedżera pakietów w programie Visual Studio)

*Dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio na Windows.*

Sprawdza, czy wszystkie zestawy w ramach ścieżki wyjściowej dla projektu, a następnie dodaje przekierowania powiązań do pliku konfiguracji sieci web lub aplikacji, gdy jest to konieczne. To polecenie jest wykonywane automatycznie podczas instalowania pakietu.

Aby uzyskać szczegółowe informacje dotyczące powiązania przekierowania i dlaczego są one używane, zobacz [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) w dokumentacji platformy .NET.

## <a name="syntax"></a>Składnia

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| ProjectName | (Wymagane) Projekt, do którego chcesz dodać przekierowania powiązań. Sam przełącznik - ProjectName jest opcjonalne. |

Żaden z tych parametrów akceptuje znaków potoku danych wejściowych lub symbol wieloznaczny.

## <a name="common-parameters"></a>Wspólne parametry

`Add-BindingRedirect` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja w przypadku błędu, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.

## <a name="examples"></a>Przykłady

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```