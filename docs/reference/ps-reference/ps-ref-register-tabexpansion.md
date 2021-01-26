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
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="5c5b3-103">Register-TabExpansion (konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="5c5b3-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="5c5b3-104">*Dostępne tylko w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="5c5b3-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="5c5b3-105">Rejestruje rozwinięcie tabulatora dla parametrów określonego polecenia, na przykład gdy karta jest używana podczas wprowadzania polecenia, rozwinięte wartości są wyświetlane jako dostępne opcje dla danego parametru.</span><span class="sxs-lookup"><span data-stu-id="5c5b3-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="5c5b3-106">Wszystkie poprzednie rozszerzenia dla polecenia są zastępowane.</span><span class="sxs-lookup"><span data-stu-id="5c5b3-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="5c5b3-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="5c5b3-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="5c5b3-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="5c5b3-108">Parameters</span></span>

| <span data-ttu-id="5c5b3-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="5c5b3-109">Parameter</span></span> | <span data-ttu-id="5c5b3-110">Opis</span><span class="sxs-lookup"><span data-stu-id="5c5b3-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5c5b3-111">Nazwa</span><span class="sxs-lookup"><span data-stu-id="5c5b3-111">Name</span></span> | <span data-ttu-id="5c5b3-112">Potrzeb Polecenie, do którego mają zostać zarejestrowane rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="5c5b3-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="5c5b3-113">Sam przełącznik-Name jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="5c5b3-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="5c5b3-114">Definicja</span><span class="sxs-lookup"><span data-stu-id="5c5b3-114">Definition</span></span> | <span data-ttu-id="5c5b3-115">Potrzeb Obiekt opisujący argument w składni, `@{'<parameter>' = {'<value1>', '<value2>', ...}}` gdzie `<parameter>` jest nazwą parametru do zmodyfikowania, a każda z nich `<value>` zawiera określone rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="5c5b3-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="5c5b3-116">Akceptowane są zarówno cudzysłowy pojedyncze, jak i podwójne.</span><span class="sxs-lookup"><span data-stu-id="5c5b3-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="5c5b3-117">Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="5c5b3-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="5c5b3-118">Parametry wspólne</span><span class="sxs-lookup"><span data-stu-id="5c5b3-118">Common Parameters</span></span>

<span data-ttu-id="5c5b3-119">`Register-TabExpansion` obsługuje następujące [typowe parametry programu PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debugowanie, Akcja błędu, ErrorVariable, wybuforuj, subvariable, PipelineVariable, verbose, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="5c5b3-119">`Register-TabExpansion` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="5c5b3-120">Przykłady</span><span class="sxs-lookup"><span data-stu-id="5c5b3-120">Examples</span></span>

<span data-ttu-id="5c5b3-121">Rozważmy rozwiązanie, które zawiera trzy projekty nazwy EventManager, Utilities i SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="5c5b3-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="5c5b3-122">Deweloper często używa `Update-Package` polecenia w różnym czasie z każdym z tych projektów.</span><span class="sxs-lookup"><span data-stu-id="5c5b3-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="5c5b3-123">Uzna, że jest to wygodne, aby `Update-Package` polecenie zapewniało rozszerzenie Autouzupełniania dla `-ProjectName` argumentu, aby nie wymagało każdorazowego wpisywania nazwy projektu.</span><span class="sxs-lookup"><span data-stu-id="5c5b3-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="5c5b3-124">Poniższe polecenie, następnie rejestruje te trzy nazwy projektu jako rozszerzenie dla `-ProjectName` parametru:</span><span class="sxs-lookup"><span data-stu-id="5c5b3-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="5c5b3-125">Deweloper może następnie wpisać `Update-Package -ProjectName ` , nacisnąć klawisz Tab, aby zobaczyć rozszerzenia oferowane jako opcje Autouzupełniania:</span><span class="sxs-lookup"><span data-stu-id="5c5b3-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Przykład użycia Register-TabExpansion](media/Register-TabExpansion-Example.png)