---
title: Rejestr NuGet — Dokumentacja programu PowerShell TabExpansion
description: Dokumentacja polecenia Register-TabExpansion programu PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 37aed96760e642b03c02bf31fe47a54f0e3cb74a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384457"
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
| Definicja | Potrzeb Obiekt opisujący argument w składni `@{'<parameter>' = {'<value1>', '<value2>', ...}}` gdzie `<parameter>` jest nazwą parametru do zmodyfikowania, a każda `<value>` zapewnia określone rozszerzenie. Akceptowane są zarówno cudzysłowy pojedyncze, jak i podwójne. |

Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.

## <a name="common-parameters"></a>Parametry wspólne

`Register-TabExpansion` obsługuje następujące [typowe parametry programu PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debugowanie, Akcja błędu, ErrorVariable, buforowanie, subvariable, PipelineVariable, verbose, WarningAction i WarningVariable.

## <a name="examples"></a>Przykłady

Rozważmy rozwiązanie, które zawiera trzy projekty nazwy EventManager, Utilities i SpecialParser. Deweloper często używa polecenia `Update-Package` w różnym czasie z każdym z tych projektów. Uzna, że wygodnie ma mieć `Update-Package` polecenie zapewnia rozszerzenie Autouzupełniania dla argumentu `-ProjectName`, dzięki czemu nie trzeba wpisywać nazwy projektu za każdym razem. 

Poniższe polecenie, następnie rejestruje te trzy nazwy projektu jako rozwinięcie dla `-ProjectName` parametru:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Deweloper może następnie wpisać `Update-Package -ProjectName `, nacisnąć klawisz Tab i wyświetlić rozszerzenia oferowane jako opcje Autouzupełniania:

![Przykład użycia polecenia Register-TabExpansion](media/Register-TabExpansion-Example.png)
