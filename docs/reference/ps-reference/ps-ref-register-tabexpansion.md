---
title: Dokumentacja programu NuGet Register-TabExpansion PowerShell
description: Informacje dotyczące Register-TabExpansion polecenia programu PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 6ad0da0e84fc2e31499c06bde013d2a256987d9a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777457"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (konsola Menedżera pakietów w programie Visual Studio)

*Dostępne tylko w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows.*

Rejestruje rozwinięcie tabulatora dla parametrów określonego polecenia, na przykład gdy karta jest używana podczas wprowadzania polecenia, rozwinięte wartości są wyświetlane jako dostępne opcje dla danego parametru. Wszystkie poprzednie rozszerzenia dla polecenia są zastępowane.

## <a name="syntax"></a>Składnia

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Nazwa | Potrzeb Polecenie, do którego mają zostać zarejestrowane rozszerzenia. Sam przełącznik-Name jest opcjonalny. |
| Definicja | Potrzeb Obiekt opisujący argument w składni, `@{'<parameter>' = {'<value1>', '<value2>', ...}}` gdzie `<parameter>` jest nazwą parametru do zmodyfikowania, a każda z nich `<value>` zawiera określone rozszerzenie. Akceptowane są zarówno cudzysłowy pojedyncze, jak i podwójne. |

Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.

## <a name="common-parameters"></a>Parametry wspólne

`Register-TabExpansion` obsługuje następujące [typowe parametry programu PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debugowanie, Akcja błędu, ErrorVariable, wybuforuj, subvariable, PipelineVariable, verbose, WarningAction i WarningVariable.

## <a name="examples"></a>Przykłady

Rozważmy rozwiązanie, które zawiera trzy projekty nazwy EventManager, Utilities i SpecialParser. Deweloper często używa `Update-Package` polecenia w różnym czasie z każdym z tych projektów. Uzna, że jest to wygodne, aby `Update-Package` polecenie zapewniało rozszerzenie Autouzupełniania dla `-ProjectName` argumentu, aby nie wymagało każdorazowego wpisywania nazwy projektu. 

Poniższe polecenie, następnie rejestruje te trzy nazwy projektu jako rozszerzenie dla `-ProjectName` parametru:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Deweloper może następnie wpisać `Update-Package -ProjectName ` , nacisnąć klawisz Tab, aby zobaczyć rozszerzenia oferowane jako opcje Autouzupełniania:

![Przykład użycia Register-TabExpansion](media/Register-TabExpansion-Example.png)