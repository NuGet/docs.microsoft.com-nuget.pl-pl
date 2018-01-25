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
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="1bb6b-104">Register-TabExpansion (Konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="1bb6b-104">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="1bb6b-105">*Dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](Package-Manager-Console.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="1bb6b-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="1bb6b-106">Rejestruje rozszerzenie kartę parametrów określone polecenie tak, aby w przypadku karty po wprowadzeniu polecenia rozwinięte wartości są wyświetlane jako dostępne opcje dla danego parametru.</span><span class="sxs-lookup"><span data-stu-id="1bb6b-106">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="1bb6b-107">Wszelkie poprzednie rozszerzenia dla polecenia zostaną zastąpione.</span><span class="sxs-lookup"><span data-stu-id="1bb6b-107">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="1bb6b-108">Składnia</span><span class="sxs-lookup"><span data-stu-id="1bb6b-108">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="1bb6b-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="1bb6b-109">Parameters</span></span>

| <span data-ttu-id="1bb6b-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="1bb6b-110">Parameter</span></span> | <span data-ttu-id="1bb6b-111">Opis</span><span class="sxs-lookup"><span data-stu-id="1bb6b-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1bb6b-112">Nazwa</span><span class="sxs-lookup"><span data-stu-id="1bb6b-112">Name</span></span> | <span data-ttu-id="1bb6b-113">(Wymagane) Polecenie, do którego ma zostać zarejestrowany rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="1bb6b-113">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="1bb6b-114">-Name przełącznika sam jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="1bb6b-114">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="1bb6b-115">Definicja</span><span class="sxs-lookup"><span data-stu-id="1bb6b-115">Definition</span></span> | <span data-ttu-id="1bb6b-116">(Wymagane) Obiekt opisujący argument w składni `@{'<parameter>' = {'<value1>', '<value2>', ...}}` gdzie `<parameter>` jest nazwą parametru do modyfikowania i każdego `<value>` zawiera określone rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="1bb6b-116">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="1bb6b-117">Pojedyncze i podwójne cudzysłowy są akceptowane.</span><span class="sxs-lookup"><span data-stu-id="1bb6b-117">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="1bb6b-118">Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.</span><span class="sxs-lookup"><span data-stu-id="1bb6b-118">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="1bb6b-119">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="1bb6b-119">Common Parameters</span></span>

<span data-ttu-id="1bb6b-120">`Register-TabExpansion`obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="1bb6b-120">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="1bb6b-121">Przykłady</span><span class="sxs-lookup"><span data-stu-id="1bb6b-121">Examples</span></span>

<span data-ttu-id="1bb6b-122">Należy wziąć pod uwagę rozwiązanie, które zawiera trzy projekty nazwy EventManager, narzędzia i SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="1bb6b-122">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="1bb6b-123">Deweloper często używa `Update-Package` polecenia w różnym czasie z każdym z tych projektów.</span><span class="sxs-lookup"><span data-stu-id="1bb6b-123">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="1bb6b-124">Użytkownik uzna wygodny mają `Update-Package` polecenia podaj rozszerzenia automatycznego uzupełniania dla `-ProjectName` argumentu, więc nie musi ona przeprowadzać wpisywania nazwy projektu zawsze.</span><span class="sxs-lookup"><span data-stu-id="1bb6b-124">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="1bb6b-125">Następujące polecenie, następnie rejestruje nazwy tych trzech projektu jako rozszerzenia dla `-ProjectName` parametru:</span><span class="sxs-lookup"><span data-stu-id="1bb6b-125">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="1bb6b-126">Deweloper może następnie wpisz `Update-Package -ProjectName `, a następnie naciśnij klawisz Tab i rozszerzenia przedstawiane jako opcje automatycznego uzupełniania w temacie:</span><span class="sxs-lookup"><span data-stu-id="1bb6b-126">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Przykład użycia TabExpansion rejestru](media/Register-TabExpansion-Example.png)
