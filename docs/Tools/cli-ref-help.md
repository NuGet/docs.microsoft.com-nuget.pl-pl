---
title: Polecenie help NuGet interfejsu wiersza polecenia | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Dokumentacja dotycząca nuget.exe polecenie Pomoc"
keywords: Dokumentacja pomocy nuget, polecenie Pomoc
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 281c6ccc7c58d153280441430be063d9ee89955d
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/15/2018
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="c9807-104">Pomoc lub?</span><span class="sxs-lookup"><span data-stu-id="c9807-104">help or ?</span></span> <span data-ttu-id="c9807-105">polecenia (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c9807-105">command (NuGet CLI)</span></span>

<span data-ttu-id="c9807-106">**Dotyczy:** wszystkie &bullet; **obsługiwane wersje**: wszystkie</span><span class="sxs-lookup"><span data-stu-id="c9807-106">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="c9807-107">Przedstawia ogólne informacje i pomoc dotyczącą określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="c9807-107">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="c9807-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="c9807-108">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="c9807-109">gdzie [polecenie] identyfikuje danego polecenia, do których chcesz wyświetlić Pomoc.</span><span class="sxs-lookup"><span data-stu-id="c9807-109">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="c9807-110">W niektórych poleceniach zachować ostrożność, aby określić *pomocy* pierwszy jako z `nuget help install`, ponieważ istnieje pakiet o nazwie "help" w nuget.org. Jeśli polecenie `nuget install help`, nie będzie uzyskać pomoc dotyczącą polecenia instalacji, ale zamiast tego zostanie zainstalowany pakiet o nazwie pomocy.</span><span class="sxs-lookup"><span data-stu-id="c9807-110">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="c9807-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="c9807-111">Options</span></span>

| <span data-ttu-id="c9807-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="c9807-112">Option</span></span> | <span data-ttu-id="c9807-113">Opis</span><span class="sxs-lookup"><span data-stu-id="c9807-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c9807-114">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="c9807-114">All</span></span> | <span data-ttu-id="c9807-115">Drukowanie szczegółową pomoc dla dostępnych poleceń; ignorowane, jeśli podano określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="c9807-115">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="c9807-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c9807-116">ConfigFile</span></span> | <span data-ttu-id="c9807-117">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="c9807-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c9807-118">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="c9807-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="c9807-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c9807-119">ForceEnglishOutput</span></span> | <span data-ttu-id="c9807-120">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="c9807-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c9807-121">Pomoc</span><span class="sxs-lookup"><span data-stu-id="c9807-121">Help</span></span> | <span data-ttu-id="c9807-122">Wyświetla Pomoc dla samo polecenie Pomoc.</span><span class="sxs-lookup"><span data-stu-id="c9807-122">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="c9807-123">Język znaczników markdown</span><span class="sxs-lookup"><span data-stu-id="c9807-123">Markdown</span></span> | <span data-ttu-id="c9807-124">Drukowanie szczegółową pomoc w formacie markdown, gdy jest używany z `-All`.</span><span class="sxs-lookup"><span data-stu-id="c9807-124">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="c9807-125">W przeciwnym razie ignorowane.</span><span class="sxs-lookup"><span data-stu-id="c9807-125">Ignored otherwise.</span></span> |
| <span data-ttu-id="c9807-126">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="c9807-126">NonInteractive</span></span> | <span data-ttu-id="c9807-127">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="c9807-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c9807-128">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="c9807-128">Verbosity</span></span> | <span data-ttu-id="c9807-129">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="c9807-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="c9807-130">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c9807-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c9807-131">Przykłady</span><span class="sxs-lookup"><span data-stu-id="c9807-131">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
