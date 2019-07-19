---
title: Dokumentacja pakietu NuGet Open-PackagePage programu PowerShell
description: Odwołanie do polecenia programu PowerShell open-PackagePage w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0237c23d81000a1d58264cc0ab48c73d819d0e5a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328217"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (konsola menedżera pakietów w programie Visual Studio)

*Przestarzałe w wersji 3.0 +; dostępne tylko w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows.*

Uruchamia domyślną przeglądarkę z adresem URL nadużycia projektu, licencji lub raportu dla określonego pakietu.

## <a name="syntax"></a>Składnia

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Id | Identyfikator pakietu żądanego pakietu. Przełącznik-ID jest opcjonalny. |
| Wersja | Wersja pakietu, domyślna dla najnowszej wersji. |
| Source | Źródło pakietu, które domyślnie jest wybrane źródło w liście rozwijanej Źródło. |
| Licencja | Otwiera przeglądarkę w adresie URL licencji pakietu. Jeśli nie określono parametru-License ani-ReportAbuse, przeglądarka otworzy adres URL projektu pakietu. |
| ReportAbuse | Otwiera przeglądarkę w adresie URL nadużycia raportu pakietu. Jeśli nie określono parametru-License ani-ReportAbuse, przeglądarka otworzy adres URL projektu pakietu. |
| PassThru | Wyświetla adres URL; Użyj with-WhatIf, aby pominąć otwieranie przeglądarki. |

Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.

## <a name="common-parameters"></a>Parametry wspólne

`Open-PackagePage`Program obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debugowanie, Akcja błędu, ErrorVariable, wybuforuj, niezmienna, PipelineVariable, verbose, WarningAction i WarningVariable.

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