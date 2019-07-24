---
title: Polecenie pomocy interfejsu wiersza polecenia NuGet
description: Dokumentacja polecenia pomocy NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328343"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="234bd-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="234bd-103">help or ?</span></span> <span data-ttu-id="234bd-104">command, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="234bd-104">command (NuGet CLI)</span></span>

<span data-ttu-id="234bd-105">**Dotyczy:** wszystkie &bullet; **obsługiwane wersje**: wszystkie</span><span class="sxs-lookup"><span data-stu-id="234bd-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="234bd-106">Wyświetla ogólne informacje pomocy i informacje pomocy dotyczące określonych poleceń.</span><span class="sxs-lookup"><span data-stu-id="234bd-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="234bd-107">Użycie</span><span class="sxs-lookup"><span data-stu-id="234bd-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="234bd-108">gdzie [polecenie] identyfikuje konkretne polecenie, dla którego ma zostać wyświetlona pomoc.</span><span class="sxs-lookup"><span data-stu-id="234bd-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="234bd-109">W przypadku niektórych poleceń należy zastanowić  się, jak w `nuget help install`pierwszej kolejności określić pomoc, ponieważ istnieje pakiet o nazwie "Help" w witrynie NuGet.org. Jeśli połączysz polecenie `nuget install help`, nie otrzymasz pomocy dotyczącej polecenia install, ale zamiast tego zainstalujemy pakiet o nazwie help.</span><span class="sxs-lookup"><span data-stu-id="234bd-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="234bd-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="234bd-110">Options</span></span>

| <span data-ttu-id="234bd-111">Opcja</span><span class="sxs-lookup"><span data-stu-id="234bd-111">Option</span></span> | <span data-ttu-id="234bd-112">Opis</span><span class="sxs-lookup"><span data-stu-id="234bd-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="234bd-113">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="234bd-113">All</span></span> | <span data-ttu-id="234bd-114">Drukuj szczegółową pomoc dotyczącą wszystkich dostępnych poleceń; ignorowany, jeśli podano określone polecenie.</span><span class="sxs-lookup"><span data-stu-id="234bd-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="234bd-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="234bd-115">ConfigFile</span></span> | <span data-ttu-id="234bd-116">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="234bd-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="234bd-117">Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="234bd-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="234bd-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="234bd-118">ForceEnglishOutput</span></span> | <span data-ttu-id="234bd-119">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="234bd-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="234bd-120">Help</span><span class="sxs-lookup"><span data-stu-id="234bd-120">Help</span></span> | <span data-ttu-id="234bd-121">Wyświetla informacje pomocy dotyczące samego polecenia pomocy.</span><span class="sxs-lookup"><span data-stu-id="234bd-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="234bd-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="234bd-122">Markdown</span></span> | <span data-ttu-id="234bd-123">Drukuj szczegółową pomoc w formacie promocji w przypadku `-All`korzystania z programu.</span><span class="sxs-lookup"><span data-stu-id="234bd-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="234bd-124">Zignorowane w przeciwnym razie.</span><span class="sxs-lookup"><span data-stu-id="234bd-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="234bd-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="234bd-125">NonInteractive</span></span> | <span data-ttu-id="234bd-126">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="234bd-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="234bd-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="234bd-127">Verbosity</span></span> | <span data-ttu-id="234bd-128">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="234bd-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="234bd-129">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="234bd-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="234bd-130">Przykłady</span><span class="sxs-lookup"><span data-stu-id="234bd-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
