---
title: "Open — PackagePage NuGet w programie PowerShell | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: e9f84530-6b3d-43b0-a832-0acb2997f6fc
description: "Odwołanie do polecenia programu PowerShell PackagePage Otwórz w konsoli Menedżera pakietów NuGet w programie Visual Studio."
keywords: "NuGet konsoli Menedżera pakietów, poleceń programu NuGet Powershell NuGet w programie PowerShell, otwórz PackagePage"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ec4310ea9d13926b1cb3b227b17016742a70bc16
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open — PackagePage (Konsola Menedżera pakietów w programie Visual Studio)

*Przestarzałe w 3.0 +; dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](Package-Manager-Console.md) w programie Visual Studio w systemie Windows.*

Uruchamia domyślnej przeglądarki z projektu, licencji lub adresu URL programu report nadużyć dla określonego pakietu.

## <a name="syntax"></a>Składnia

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Identyfikator | Identyfikator pakietu żądanego pakietu. Id przełącznika sam jest opcjonalna. |
| Wersja | Wersja pakietu, domyślnie używany do najnowszej wersji. |
| Źródło | Źródło pakietu domyślnie wybrane źródło w lokalizacji źródłowej listy rozwijanej. |
| Licencji | Otwiera przeglądarkę, aby adres URL licencji pakietu. Jeśli nie - licencji - ReportAbuse określono ani, w przeglądarce zostanie otwarty adres URL projektu pakietu. |
| ReportAbuse | Otwiera przeglądarkę do adresu URL nadużycia raport pakietu. Jeśli nie - licencji - ReportAbuse określono ani, w przeglądarce zostanie otwarty adres URL projektu pakietu. |
| Przekazywanie | Wyświetla adres URL; za pomocą - WhatIf do pomijania otwierania przeglądarki. |

Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.

## <a name="common-parameters"></a>Wspólne parametry

`Open-PackagePage`obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.

## <a name="examples"></a>Przykłady

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```