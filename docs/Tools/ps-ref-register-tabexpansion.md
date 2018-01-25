---
title: NuGet Register-TabExpansion w programie PowerShell | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Odwołanie do polecenia programu PowerShell rejestrowanie TabExpansion w konsoli Menedżera pakietów NuGet w programie Visual Studio."
keywords: "NuGet konsoli Menedżera pakietów, poleceń programu NuGet Powershell NuGet w programie PowerShell, TabExpansion rejestru"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5691c07f9efef4bfd12680421f3b02c5a523eb6f
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (Konsola Menedżera pakietów w programie Visual Studio)

*Dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](Package-Manager-Console.md) w programie Visual Studio w systemie Windows.*

Rejestruje rozszerzenie kartę parametrów określone polecenie tak, aby w przypadku karty po wprowadzeniu polecenia rozwinięte wartości są wyświetlane jako dostępne opcje dla danego parametru. Wszelkie poprzednie rozszerzenia dla polecenia zostaną zastąpione.

## <a name="syntax"></a>Składnia

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Nazwa | (Wymagane) Polecenie, do którego ma zostać zarejestrowany rozszerzenia. -Name przełącznika sam jest opcjonalna. |
| Definicja | (Wymagane) Obiekt opisujący argument w składni `@{'<parameter>' = {'<value1>', '<value2>', ...}}` gdzie `<parameter>` jest nazwą parametru do modyfikowania i każdego `<value>` zawiera określone rozszerzenia. Pojedyncze i podwójne cudzysłowy są akceptowane. |

Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.

## <a name="common-parameters"></a>Wspólne parametry

`Register-TabExpansion`obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.

## <a name="examples"></a>Przykłady

Należy wziąć pod uwagę rozwiązanie, które zawiera trzy projekty nazwy EventManager, narzędzia i SpecialParser. Deweloper często używa `Update-Package` polecenia w różnym czasie z każdym z tych projektów. Użytkownik uzna wygodny mają `Update-Package` polecenia podaj rozszerzenia automatycznego uzupełniania dla `-ProjectName` argumentu, więc nie musi ona przeprowadzać wpisywania nazwy projektu zawsze. 

Następujące polecenie, następnie rejestruje nazwy tych trzech projektu jako rozszerzenia dla `-ProjectName` parametru:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Deweloper może następnie wpisz `Update-Package -ProjectName `, a następnie naciśnij klawisz Tab i rozszerzenia przedstawiane jako opcje automatycznego uzupełniania w temacie:

![Przykład użycia TabExpansion rejestru](media/Register-TabExpansion-Example.png)
