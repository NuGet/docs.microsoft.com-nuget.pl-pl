---
title: Open — PackagePage NuGet w programie PowerShell
description: Odwołanie do polecenia programu PowerShell PackagePage Otwórz w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e64a83c01a7baac330c99fe40ba52f328a2133b8
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817723"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (konsola menedżera pakietów w programie Visual Studio)

*Przestarzałe w 3.0 +; dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio w systemie Windows.*

Uruchamia domyślnej przeglądarki z projektu, licencji lub adresu URL programu report nadużyć dla określonego pakietu.

## <a name="syntax"></a>Składnia

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Id | Identyfikator pakietu żądanego pakietu. Id przełącznika sam jest opcjonalna. |
| Wersja | Wersja pakietu, domyślnie używany do najnowszej wersji. |
| Źródło | Źródło pakietu domyślnie wybrane źródło w lokalizacji źródłowej listy rozwijanej. |
| Licencji | Otwiera przeglądarkę, aby adres URL licencji pakietu. Jeśli nie - licencji - ReportAbuse określono ani, w przeglądarce zostanie otwarty adres URL projektu pakietu. |
| ReportAbuse | Otwiera przeglądarkę do adresu URL nadużycia raport pakietu. Jeśli nie - licencji - ReportAbuse określono ani, w przeglądarce zostanie otwarty adres URL projektu pakietu. |
| Przekazywanie | Wyświetla adres URL; za pomocą - WhatIf do pomijania otwierania przeglądarki. |

Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.

## <a name="common-parameters"></a>Wspólne parametry

`Open-PackagePage` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.

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