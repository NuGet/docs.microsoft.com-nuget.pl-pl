---
title: Polecenie pomocy interfejsu wiersza polecenia NuGet
description: Odwołanie do nuget.exe polecenia pomocy
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 12776b7c16aeef223a0b682ee2468edec8ea3295
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623113"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="ba39c-103">help lub ?</span><span class="sxs-lookup"><span data-stu-id="ba39c-103">help or ?</span></span> <span data-ttu-id="ba39c-104">polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="ba39c-104">command (NuGet CLI)</span></span>

<span data-ttu-id="ba39c-105">**Dotyczy:** wszystkie &bullet; **obsługiwane wersje**: wszystkie</span><span class="sxs-lookup"><span data-stu-id="ba39c-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="ba39c-106">Wyświetla ogólne informacje pomocy i informacje pomocy dotyczące określonych poleceń.</span><span class="sxs-lookup"><span data-stu-id="ba39c-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="ba39c-107">Użycie</span><span class="sxs-lookup"><span data-stu-id="ba39c-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="ba39c-108">gdzie [polecenie] identyfikuje konkretne polecenie, dla którego ma zostać wyświetlona pomoc.</span><span class="sxs-lookup"><span data-stu-id="ba39c-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="ba39c-109">W przypadku niektórych poleceń należy zastanowić się, jak w pierwszej kolejności określić *Pomoc* , `nuget help install` ponieważ istnieje pakiet o nazwie "Help" w witrynie NuGet.org. Jeśli połączysz polecenie `nuget install help` , nie otrzymasz pomocy dotyczącej polecenia install, ale zamiast tego zainstalujemy pakiet o nazwie help.</span><span class="sxs-lookup"><span data-stu-id="ba39c-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="ba39c-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="ba39c-110">Options</span></span>

- **`-All`**

  <span data-ttu-id="ba39c-111">Drukuj szczegółową pomoc dotyczącą wszystkich dostępnych poleceń; ignorowany, jeśli podano określone polecenie.</span><span class="sxs-lookup"><span data-stu-id="ba39c-111">Print detailed help for all available commands; ignored if a specific command is given.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="ba39c-112">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="ba39c-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ba39c-113">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="ba39c-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="ba39c-114">*(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.</span><span class="sxs-lookup"><span data-stu-id="ba39c-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="ba39c-115">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="ba39c-115">Displays help information for the command.</span></span>

- **`-Markdown`**

  <span data-ttu-id="ba39c-116">Drukuj szczegółową pomoc w formacie promocji w przypadku korzystania z programu `-All` .</span><span class="sxs-lookup"><span data-stu-id="ba39c-116">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="ba39c-117">Zignorowane w przeciwnym razie.</span><span class="sxs-lookup"><span data-stu-id="ba39c-117">Ignored otherwise.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="ba39c-118">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ba39c-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="ba39c-119">Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .</span><span class="sxs-lookup"><span data-stu-id="ba39c-119">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="ba39c-120">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ba39c-120">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ba39c-121">Przykłady</span><span class="sxs-lookup"><span data-stu-id="ba39c-121">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
