---
title: Dokumentacja pakietu NuGet Open-PackagePage programu PowerShell
description: Odwołanie do polecenia programu PowerShell open-PackagePage w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 39199ebfc37756ed40158a1c07afca7709067350
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384431"
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
| Obiekt źródłowy | Źródło pakietu, które domyślnie jest wybrane źródło w liście rozwijanej Źródło. |
| Licencja | Otwiera przeglądarkę w adresie URL licencji pakietu. Jeśli nie określono parametru-License ani-ReportAbuse, przeglądarka otworzy adres URL projektu pakietu. |
| ReportAbuse | Otwiera przeglądarkę w adresie URL nadużycia raportu pakietu. Jeśli nie określono parametru-License ani-ReportAbuse, przeglądarka otworzy adres URL projektu pakietu. |
| PassThru | Wyświetla adres URL; Użyj with-WhatIf, aby pominąć otwieranie przeglądarki. |

Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.

## <a name="common-parameters"></a>Parametry wspólne

`Open-PackagePage` obsługuje następujące [typowe parametry programu PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debugowanie, Akcja błędu, ErrorVariable, buforowanie, subvariable, PipelineVariable, verbose, WarningAction i WarningVariable.

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