---
title: Dokumentacja programu NuGet Open-PackagePage PowerShell
description: Informacje dotyczące Open-PackagePage polecenia programu PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d34a91007197f8004e4923deedb1cdb26d662d53
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780412"
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