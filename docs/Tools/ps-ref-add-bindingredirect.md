---
title: NuGet BindingRedirect w programie PowerShell | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 90f4dcb0-6e5a-4948-8ea9-62e0d061d95a
description: "Odwołanie do polecenia programu PowerShell Dodaj BindingRedirect w konsoli Menedżera pakietów NuGet w programie Visual Studio."
keywords: "NuGet konsoli Menedżera pakietów, poleceń programu NuGet Powershell NuGet w programie PowerShell, Dodaj BindingRedirect"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7bf8cdb938195f4747932b38ef0d5bb6c34b9137
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Dodaj BindingRedirect (Konsola Menedżera pakietów w programie Visual Studio)

*Dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](Package-Manager-Console.md) w programie Visual Studio w systemie Windows.*

Sprawdza wszystkie zestawy w ścieżce wyjściowej dla projektu i dodaje przekierowania powiązania do pliku konfiguracji aplikacji lub sieci web, w miarę potrzeby. To polecenie jest uruchamiane automatycznie podczas instalowania pakietu.

Aby uzyskać szczegółowe informacje na powiązanie przekierowania i dlaczego ich użycia, zobacz [przekierowywanie wersji zestawu](https://docs.microsoft.com/dotnet/framework/configure-apps/redirect-assembly-versions) w dokumentacji programu .NET.

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

`Add-BindingRedirect`obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.

## <a name="examples"></a>Przykłady

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```