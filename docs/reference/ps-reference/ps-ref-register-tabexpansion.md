---
title: Rejestr NuGet — Dokumentacja programu PowerShell TabExpansion
description: Dokumentacja polecenia Register-TabExpansion programu PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 14cda695677e1052c78169fda097b72b460a9d43
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328193"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="a393a-103">Register-TabExpansion (konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="a393a-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="a393a-104">*Dostępne tylko w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="a393a-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="a393a-105">Rejestruje rozwinięcie tabulatora dla parametrów określonego polecenia, na przykład gdy karta jest używana podczas wprowadzania polecenia, rozwinięte wartości są wyświetlane jako dostępne opcje dla danego parametru.</span><span class="sxs-lookup"><span data-stu-id="a393a-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="a393a-106">Wszystkie poprzednie rozszerzenia dla polecenia są zastępowane.</span><span class="sxs-lookup"><span data-stu-id="a393a-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="a393a-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="a393a-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="a393a-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="a393a-108">Parameters</span></span>

| <span data-ttu-id="a393a-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="a393a-109">Parameter</span></span> | <span data-ttu-id="a393a-110">Opis</span><span class="sxs-lookup"><span data-stu-id="a393a-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a393a-111">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a393a-111">Name</span></span> | <span data-ttu-id="a393a-112">Potrzeb Polecenie, do którego mają zostać zarejestrowane rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="a393a-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="a393a-113">Sam przełącznik-Name jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="a393a-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="a393a-114">Definicja</span><span class="sxs-lookup"><span data-stu-id="a393a-114">Definition</span></span> | <span data-ttu-id="a393a-115">Potrzeb Obiekt opisujący argument w składni `@{'<parameter>' = {'<value1>', '<value2>', ...}}` , gdzie `<parameter>` jest nazwą parametru do zmodyfikowania, a każda z nich `<value>` zawiera określone rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="a393a-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="a393a-116">Akceptowane są zarówno cudzysłowy pojedyncze, jak i podwójne.</span><span class="sxs-lookup"><span data-stu-id="a393a-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="a393a-117">Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="a393a-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="a393a-118">Parametry wspólne</span><span class="sxs-lookup"><span data-stu-id="a393a-118">Common Parameters</span></span>

<span data-ttu-id="a393a-119">`Register-TabExpansion`Program obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debugowanie, Akcja błędu, ErrorVariable, wybuforuj, niezmienna, PipelineVariable, verbose, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="a393a-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="a393a-120">Przykłady</span><span class="sxs-lookup"><span data-stu-id="a393a-120">Examples</span></span>

<span data-ttu-id="a393a-121">Rozważmy rozwiązanie, które zawiera trzy projekty nazwy EventManager, Utilities i SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="a393a-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="a393a-122">Deweloper często używa `Update-Package` polecenia w różnym czasie z każdym z tych projektów.</span><span class="sxs-lookup"><span data-stu-id="a393a-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="a393a-123">Uzna, że jest to wygodne, `Update-Package` aby polecenie zapewniało rozszerzenie autouzupełniania `-ProjectName` dla argumentu, aby nie wymagało każdorazowego wpisywania nazwy projektu.</span><span class="sxs-lookup"><span data-stu-id="a393a-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="a393a-124">Poniższe polecenie, następnie rejestruje te trzy nazwy projektu jako rozszerzenie dla `-ProjectName` parametru:</span><span class="sxs-lookup"><span data-stu-id="a393a-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="a393a-125">Deweloper może następnie wpisać `Update-Package -ProjectName `, nacisnąć klawisz Tab, aby zobaczyć rozszerzenia oferowane jako opcje Autouzupełniania:</span><span class="sxs-lookup"><span data-stu-id="a393a-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Przykład użycia polecenia Register-TabExpansion](media/Register-TabExpansion-Example.png)
