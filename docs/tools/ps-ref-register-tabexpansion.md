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
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="27566-103">Register-TabExpansion (Konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="27566-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="27566-104">*Dostępne tylko w obrębie [Konsola Menedżera pakietów](package-manager-console.md) w programie Visual Studio na Windows.*</span><span class="sxs-lookup"><span data-stu-id="27566-104">*Available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="27566-105">Rejestruje rozwijania karcie Parametry określone polecenie w taki sposób, że gdy karta jest używana, po wprowadzeniu polecenia, rozwinięte wartości są wyświetlane jako opcje dostępne dla danego parametru.</span><span class="sxs-lookup"><span data-stu-id="27566-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="27566-106">Wszelkie poprzednie rozszerzeń dla polecenia zostaną zastąpione.</span><span class="sxs-lookup"><span data-stu-id="27566-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="27566-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="27566-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="27566-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="27566-108">Parameters</span></span>

| <span data-ttu-id="27566-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="27566-109">Parameter</span></span> | <span data-ttu-id="27566-110">Opis</span><span class="sxs-lookup"><span data-stu-id="27566-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="27566-111">Nazwa</span><span class="sxs-lookup"><span data-stu-id="27566-111">Name</span></span> | <span data-ttu-id="27566-112">(Wymagane) Polecenie, do którego ma zostać zarejestrowany rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="27566-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="27566-113">-Name samym przełączniku jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="27566-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="27566-114">Definicja</span><span class="sxs-lookup"><span data-stu-id="27566-114">Definition</span></span> | <span data-ttu-id="27566-115">(Wymagane) Obiekt opisujący argument w składni `@{'<parameter>' = {'<value1>', '<value2>', ...}}` gdzie `<parameter>` jest nazwą parametru, aby zmodyfikować, a każdy `<value>` zawiera określone rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="27566-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="27566-116">Pojedyncze i podwójne cudzysłowy są akceptowane.</span><span class="sxs-lookup"><span data-stu-id="27566-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="27566-117">Żaden z tych parametrów akceptuje znaków potoku danych wejściowych lub symbol wieloznaczny.</span><span class="sxs-lookup"><span data-stu-id="27566-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="27566-118">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="27566-118">Common Parameters</span></span>

<span data-ttu-id="27566-119">`Register-TabExpansion` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debugowanie, akcja w przypadku błędu, ErrorVariable, OutBuffer, OutVariable, PipelineVariable pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="27566-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="27566-120">Przykłady</span><span class="sxs-lookup"><span data-stu-id="27566-120">Examples</span></span>

<span data-ttu-id="27566-121">Należy wziąć pod uwagę rozwiązanie, które zawiera trzy nazwy projektów EventManager, narzędzia i SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="27566-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="27566-122">Deweloper często używane `Update-Package` polecenia w różnym czasie z każdą z tych projektów.</span><span class="sxs-lookup"><span data-stu-id="27566-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="27566-123">Odnajduje on wygodne mają `Update-Package` polecenia zapewniają rozszerzeń automatycznego uzupełniania dla `-ProjectName` argumentu, więc nie potrzebuje do wpisywania nazwy projektu każdorazowo.</span><span class="sxs-lookup"><span data-stu-id="27566-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="27566-124">Następujące polecenie, następnie rejestruje te nazwy trzy projektu jako rozszerzenie dla `-ProjectName` parametru:</span><span class="sxs-lookup"><span data-stu-id="27566-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="27566-125">Deweloper może następnie wpisz `Update-Package -ProjectName `, a następnie naciśnij klawisz Tab i Zobacz rozszerzenia przedstawiane jako opcje automatycznego uzupełniania:</span><span class="sxs-lookup"><span data-stu-id="27566-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Przykład użycia TabExpansion rejestru](media/Register-TabExpansion-Example.png)
