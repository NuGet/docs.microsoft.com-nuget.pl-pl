---
title: Polecenie help NuGet interfejsu wiersza polecenia
description: Dokumentacja dotycząca nuget.exe polecenie Pomoc
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: dbfc803e24c824d30e128d6e86cfa3c43660668f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="eaf9a-103">Pomoc lub?</span><span class="sxs-lookup"><span data-stu-id="eaf9a-103">help or ?</span></span> <span data-ttu-id="eaf9a-104">command, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="eaf9a-104">command (NuGet CLI)</span></span>

<span data-ttu-id="eaf9a-105">**Dotyczy:** wszystkie &bullet; **obsługiwane wersje**: wszystkie</span><span class="sxs-lookup"><span data-stu-id="eaf9a-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="eaf9a-106">Przedstawia ogólne informacje i pomoc dotyczącą określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="eaf9a-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="eaf9a-107">Użycie</span><span class="sxs-lookup"><span data-stu-id="eaf9a-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="eaf9a-108">gdzie [polecenie] identyfikuje danego polecenia, do których chcesz wyświetlić Pomoc.</span><span class="sxs-lookup"><span data-stu-id="eaf9a-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="eaf9a-109">W niektórych poleceniach zachować ostrożność, aby określić *pomocy* pierwszy jako z `nuget help install`, ponieważ istnieje pakiet o nazwie "help" w nuget.org. Jeśli polecenie `nuget install help`, nie będzie uzyskać pomoc dotyczącą polecenia instalacji, ale zamiast tego zostanie zainstalowany pakiet o nazwie pomocy.</span><span class="sxs-lookup"><span data-stu-id="eaf9a-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="eaf9a-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="eaf9a-110">Options</span></span>

| <span data-ttu-id="eaf9a-111">Opcja</span><span class="sxs-lookup"><span data-stu-id="eaf9a-111">Option</span></span> | <span data-ttu-id="eaf9a-112">Opis</span><span class="sxs-lookup"><span data-stu-id="eaf9a-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="eaf9a-113">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="eaf9a-113">All</span></span> | <span data-ttu-id="eaf9a-114">Drukowanie szczegółową pomoc dla dostępnych poleceń; ignorowane, jeśli podano określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="eaf9a-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="eaf9a-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="eaf9a-115">ConfigFile</span></span> | <span data-ttu-id="eaf9a-116">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="eaf9a-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="eaf9a-117">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="eaf9a-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="eaf9a-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="eaf9a-118">ForceEnglishOutput</span></span> | <span data-ttu-id="eaf9a-119">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="eaf9a-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="eaf9a-120">Pomoc</span><span class="sxs-lookup"><span data-stu-id="eaf9a-120">Help</span></span> | <span data-ttu-id="eaf9a-121">Wyświetla Pomoc dla samo polecenie Pomoc.</span><span class="sxs-lookup"><span data-stu-id="eaf9a-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="eaf9a-122">Język znaczników markdown</span><span class="sxs-lookup"><span data-stu-id="eaf9a-122">Markdown</span></span> | <span data-ttu-id="eaf9a-123">Drukowanie szczegółową pomoc w formacie markdown, gdy jest używany z `-All`.</span><span class="sxs-lookup"><span data-stu-id="eaf9a-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="eaf9a-124">W przeciwnym razie ignorowane.</span><span class="sxs-lookup"><span data-stu-id="eaf9a-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="eaf9a-125">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="eaf9a-125">NonInteractive</span></span> | <span data-ttu-id="eaf9a-126">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="eaf9a-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="eaf9a-127">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="eaf9a-127">Verbosity</span></span> | <span data-ttu-id="eaf9a-128">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="eaf9a-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="eaf9a-129">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="eaf9a-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="eaf9a-130">Przykłady</span><span class="sxs-lookup"><span data-stu-id="eaf9a-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
