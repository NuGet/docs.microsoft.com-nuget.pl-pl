---
title: Polecenie help NuGet interfejsu wiersza polecenia | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 780d7f52-d6c6-45cd-8a62-218ff8c0b270
description: "Dokumentacja dotycząca nuget.exe polecenie Pomoc"
keywords: Dokumentacja pomocy nuget, polecenie Pomoc
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 55dc263fedd7ed5a3e48b76dbc9a3ccc220655cf
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="44d71-104">Pomoc lub?</span><span class="sxs-lookup"><span data-stu-id="44d71-104">help or ?</span></span> <span data-ttu-id="44d71-105">polecenia (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="44d71-105">command (NuGet CLI)</span></span>

<span data-ttu-id="44d71-106">**Dotyczy:** wszystkie &bullet; **obsługiwane wersje**: wszystkie</span><span class="sxs-lookup"><span data-stu-id="44d71-106">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="44d71-107">Przedstawia ogólne informacje i pomoc dotyczącą określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="44d71-107">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="44d71-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="44d71-108">Usage</span></span>

```
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="44d71-109">gdzie [polecenie] identyfikuje danego polecenia, do których chcesz wyświetlić Pomoc.</span><span class="sxs-lookup"><span data-stu-id="44d71-109">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="44d71-110">W niektórych poleceniach zachować ostrożność, aby określić *pomocy* pierwszy jako z `nuget help install`, ponieważ istnieje pakiet o nazwie "help" w nuget.org. Jeśli polecenie `nuget install help`, nie będzie uzyskać pomoc dotyczącą polecenia instalacji, ale zamiast tego zostanie zainstalowany pakiet o nazwie pomocy.</span><span class="sxs-lookup"><span data-stu-id="44d71-110">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you'll not get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="44d71-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="44d71-111">Options</span></span>

| <span data-ttu-id="44d71-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="44d71-112">Option</span></span> | <span data-ttu-id="44d71-113">Opis</span><span class="sxs-lookup"><span data-stu-id="44d71-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="44d71-114">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="44d71-114">All</span></span> | <span data-ttu-id="44d71-115">Drukowanie szczegółową pomoc dla dostępnych poleceń; ignorowane, jeśli podano określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="44d71-115">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="44d71-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="44d71-116">ConfigFile</span></span> | <span data-ttu-id="44d71-117">*(2.5 +)*  Pliku konfiguracji NuGet w celu zastosowania.</span><span class="sxs-lookup"><span data-stu-id="44d71-117">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="44d71-118">Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany.</span><span class="sxs-lookup"><span data-stu-id="44d71-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="44d71-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="44d71-119">ForceEnglishOutput</span></span> | <span data-ttu-id="44d71-120">*(3.5 +)*  Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="44d71-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="44d71-121">Pomoc</span><span class="sxs-lookup"><span data-stu-id="44d71-121">Help</span></span> | <span data-ttu-id="44d71-122">Wyświetla Pomoc dla samo polecenie Pomoc.</span><span class="sxs-lookup"><span data-stu-id="44d71-122">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="44d71-123">Język znaczników markdown</span><span class="sxs-lookup"><span data-stu-id="44d71-123">Markdown</span></span> | <span data-ttu-id="44d71-124">Drukowanie szczegółową pomoc w formacie markdown, gdy jest używany z `-All`.</span><span class="sxs-lookup"><span data-stu-id="44d71-124">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="44d71-125">W przeciwnym razie ignorowane.</span><span class="sxs-lookup"><span data-stu-id="44d71-125">Ignored otherwise.</span></span> |
| <span data-ttu-id="44d71-126">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="44d71-126">NonInteractive</span></span> | <span data-ttu-id="44d71-127">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="44d71-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="44d71-128">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="44d71-128">Verbosity</span></span> | <span data-ttu-id="44d71-129">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="44d71-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="44d71-130">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="44d71-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="44d71-131">Przykłady</span><span class="sxs-lookup"><span data-stu-id="44d71-131">Examples</span></span>

```
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
