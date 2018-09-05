---
title: Dokumentacja programu PowerShell NuGet Open-PackagePage
description: Dokumentacja polecenia PowerShell PackagePage otwarcie w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0325aa4ddd718a901dd6a09cdf86cae260e326ab
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547171"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (konsola menedżera pakietów w programie Visual Studio)

*Przestarzałe w 3.0 +; dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio na Windows.*

Uruchamia domyślną przeglądarkę z projektem, licencji lub adres URL do raportu nadużyć dla określonego pakietu.

## <a name="syntax"></a>Składnia

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Id | Identyfikator pakietu żądanego pakietu. — Identyfikator samym przełączniku jest opcjonalne. |
| Wersja | Wersja pakietu, ustawiając domyślnie do najnowszej wersji. |
| Źródło | Źródło pakietu przyjęty wybranego źródła w źródle listy rozwijanej. |
| Licencja | Zostanie otwarta w przeglądarce adres URL licencji pakietu. Jeśli określono - licencji ani - ReportAbuse przeglądarki otwiera adres URL projektu pakietu. |
| ReportAbuse | Zostanie otwarta w przeglądarce adres URL nadużyć raport pakietu. Jeśli określono - licencji ani - ReportAbuse przeglądarki otwiera adres URL projektu pakietu. |
| Przekazywanie | Wyświetla adres URL; za pomocą - WhatIf do pomijania otwierania przeglądarki. |

Żaden z tych parametrów akceptuje znaków potoku danych wejściowych lub symbol wieloznaczny.

## <a name="common-parameters"></a>Wspólne parametry

`Open-PackagePage` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja w przypadku błędu, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.

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