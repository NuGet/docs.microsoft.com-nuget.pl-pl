---
title: Dokumentacja programu NuGet Open-PackagePage PowerShell
description: Informacje dotyczące Open-PackagePage polecenia programu PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: ba90e09c017ec66d73c35a60025474bc77cf65a7
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238065"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (konsola Menedżera pakietów w programie Visual Studio)

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
| Element źródłowy | Źródło pakietu, które domyślnie jest wybrane źródło w liście rozwijanej Źródło. |
| Licencja | Otwiera przeglądarkę w adresie URL licencji pakietu. Jeśli nie określono parametru-License ani-ReportAbuse, przeglądarka otworzy adres URL projektu pakietu. |
| ReportAbuse | Otwiera przeglądarkę w adresie URL nadużycia raportu pakietu. Jeśli nie określono parametru-License ani-ReportAbuse, przeglądarka otworzy adres URL projektu pakietu. |
| PassThru | Wyświetla adres URL; Użyj with-WhatIf, aby pominąć otwieranie przeglądarki. |

Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.

## <a name="common-parameters"></a>Parametry wspólne

`Open-PackagePage` obsługuje następujące [typowe parametry programu PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debugowanie, Akcja błędu, ErrorVariable, wybuforuj, subvariable, PipelineVariable, verbose, WarningAction i WarningVariable.

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