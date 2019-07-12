---
title: Dokumentacja programu NuGet Register-TabExpansion programu PowerShell
description: Dokumentacja polecenia PowerShell TabExpansion Zarejestruj się w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8adb80af85e2e32fa8c35e5272cf90ff0c0ddcbb
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842482"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (Konsola Menedżera pakietów w programie Visual Studio)

*Dostępne tylko w obrębie [Konsola Menedżera pakietów](package-manager-console.md) w programie Visual Studio na Windows.*

Rejestruje rozwijania karcie Parametry określone polecenie w taki sposób, że gdy karta jest używana, po wprowadzeniu polecenia, rozwinięte wartości są wyświetlane jako opcje dostępne dla danego parametru. Wszelkie poprzednie rozszerzeń dla polecenia zostaną zastąpione.

## <a name="syntax"></a>Składnia

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Nazwa | (Wymagane) Polecenie, do którego ma zostać zarejestrowany rozszerzenia. -Name samym przełączniku jest opcjonalne. |
| Definicja | (Wymagane) Obiekt opisujący argument w składni `@{'<parameter>' = {'<value1>', '<value2>', ...}}` gdzie `<parameter>` jest nazwą parametru, aby zmodyfikować, a każdy `<value>` zawiera określone rozszerzenia. Pojedyncze i podwójne cudzysłowy są akceptowane. |

Żaden z tych parametrów akceptuje znaków potoku danych wejściowych lub symbol wieloznaczny.

## <a name="common-parameters"></a>Wspólne parametry

`Register-TabExpansion` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debugowanie, akcja w przypadku błędu, ErrorVariable, OutBuffer, OutVariable, PipelineVariable pełne, WarningAction i WarningVariable.

## <a name="examples"></a>Przykłady

Należy wziąć pod uwagę rozwiązanie, które zawiera trzy nazwy projektów EventManager, narzędzia i SpecialParser. Deweloper często używane `Update-Package` polecenia w różnym czasie z każdą z tych projektów. Odnajduje on wygodne mają `Update-Package` polecenia zapewniają rozszerzeń automatycznego uzupełniania dla `-ProjectName` argumentu, więc nie potrzebuje do wpisywania nazwy projektu każdorazowo. 

Następujące polecenie, następnie rejestruje te nazwy trzy projektu jako rozszerzenie dla `-ProjectName` parametru:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Deweloper może następnie wpisz `Update-Package -ProjectName `, a następnie naciśnij klawisz Tab i Zobacz rozszerzenia przedstawiane jako opcje automatycznego uzupełniania:

![Przykład użycia TabExpansion rejestru](media/Register-TabExpansion-Example.png)
