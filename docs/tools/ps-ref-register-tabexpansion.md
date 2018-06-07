---
title: NuGet Register-TabExpansion w programie PowerShell
description: Odwołanie do polecenia programu PowerShell rejestrowanie TabExpansion w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8011c0e6aa951a32114d460803c493810964a7e0
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818421"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="8490a-103">Register-TabExpansion (Konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="8490a-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="8490a-104">*Dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="8490a-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="8490a-105">Rejestruje rozszerzenie kartę parametrów określone polecenie tak, aby w przypadku karty po wprowadzeniu polecenia rozwinięte wartości są wyświetlane jako dostępne opcje dla danego parametru.</span><span class="sxs-lookup"><span data-stu-id="8490a-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="8490a-106">Wszelkie poprzednie rozszerzenia dla polecenia zostaną zastąpione.</span><span class="sxs-lookup"><span data-stu-id="8490a-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="8490a-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="8490a-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="8490a-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="8490a-108">Parameters</span></span>

| <span data-ttu-id="8490a-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="8490a-109">Parameter</span></span> | <span data-ttu-id="8490a-110">Opis</span><span class="sxs-lookup"><span data-stu-id="8490a-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8490a-111">Nazwa</span><span class="sxs-lookup"><span data-stu-id="8490a-111">Name</span></span> | <span data-ttu-id="8490a-112">(Wymagane) Polecenie, do którego ma zostać zarejestrowany rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="8490a-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="8490a-113">-Name przełącznika sam jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="8490a-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="8490a-114">Definicja</span><span class="sxs-lookup"><span data-stu-id="8490a-114">Definition</span></span> | <span data-ttu-id="8490a-115">(Wymagane) Obiekt opisujący argument w składni `@{'<parameter>' = {'<value1>', '<value2>', ...}}` gdzie `<parameter>` jest nazwą parametru do modyfikowania i każdego `<value>` zawiera określone rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="8490a-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="8490a-116">Pojedyncze i podwójne cudzysłowy są akceptowane.</span><span class="sxs-lookup"><span data-stu-id="8490a-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="8490a-117">Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.</span><span class="sxs-lookup"><span data-stu-id="8490a-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="8490a-118">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="8490a-118">Common Parameters</span></span>

<span data-ttu-id="8490a-119">`Register-TabExpansion` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="8490a-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="8490a-120">Przykłady</span><span class="sxs-lookup"><span data-stu-id="8490a-120">Examples</span></span>

<span data-ttu-id="8490a-121">Należy wziąć pod uwagę rozwiązanie, które zawiera trzy projekty nazwy EventManager, narzędzia i SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="8490a-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="8490a-122">Deweloper często używa `Update-Package` polecenia w różnym czasie z każdym z tych projektów.</span><span class="sxs-lookup"><span data-stu-id="8490a-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="8490a-123">Użytkownik uzna wygodny mają `Update-Package` polecenia podaj rozszerzenia automatycznego uzupełniania dla `-ProjectName` argumentu, więc nie musi ona przeprowadzać wpisywania nazwy projektu zawsze.</span><span class="sxs-lookup"><span data-stu-id="8490a-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="8490a-124">Następujące polecenie, następnie rejestruje nazwy tych trzech projektu jako rozszerzenia dla `-ProjectName` parametru:</span><span class="sxs-lookup"><span data-stu-id="8490a-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="8490a-125">Deweloper może następnie wpisz `Update-Package -ProjectName `, a następnie naciśnij klawisz Tab i rozszerzenia przedstawiane jako opcje automatycznego uzupełniania w temacie:</span><span class="sxs-lookup"><span data-stu-id="8490a-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Przykład użycia TabExpansion rejestru](media/Register-TabExpansion-Example.png)
