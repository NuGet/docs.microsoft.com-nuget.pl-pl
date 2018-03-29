---
title: Polecenie help NuGet interfejsu wiersza polecenia | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Dokumentacja dotycząca nuget.exe polecenie Pomoc
keywords: Dokumentacja pomocy nuget, polecenie Pomoc
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 440861e53b4a9ff73a9d3e8a2a3dad7dbddc9584
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="8eafe-104">Pomoc lub?</span><span class="sxs-lookup"><span data-stu-id="8eafe-104">help or ?</span></span> <span data-ttu-id="8eafe-105">polecenia (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8eafe-105">command (NuGet CLI)</span></span>

<span data-ttu-id="8eafe-106">**Dotyczy:** wszystkie &bullet; **obsługiwane wersje**: wszystkie</span><span class="sxs-lookup"><span data-stu-id="8eafe-106">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="8eafe-107">Przedstawia ogólne informacje i pomoc dotyczącą określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="8eafe-107">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="8eafe-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="8eafe-108">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="8eafe-109">gdzie [polecenie] identyfikuje danego polecenia, do których chcesz wyświetlić Pomoc.</span><span class="sxs-lookup"><span data-stu-id="8eafe-109">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="8eafe-110">W niektórych poleceniach zachować ostrożność, aby określić *pomocy* pierwszy jako z `nuget help install`, ponieważ istnieje pakiet o nazwie "help" w nuget.org. Jeśli polecenie `nuget install help`, nie będzie uzyskać pomoc dotyczącą polecenia instalacji, ale zamiast tego zostanie zainstalowany pakiet o nazwie pomocy.</span><span class="sxs-lookup"><span data-stu-id="8eafe-110">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="8eafe-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="8eafe-111">Options</span></span>

| <span data-ttu-id="8eafe-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="8eafe-112">Option</span></span> | <span data-ttu-id="8eafe-113">Opis</span><span class="sxs-lookup"><span data-stu-id="8eafe-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8eafe-114">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="8eafe-114">All</span></span> | <span data-ttu-id="8eafe-115">Drukowanie szczegółową pomoc dla dostępnych poleceń; ignorowane, jeśli podano określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="8eafe-115">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="8eafe-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8eafe-116">ConfigFile</span></span> | <span data-ttu-id="8eafe-117">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="8eafe-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8eafe-118">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="8eafe-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="8eafe-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8eafe-119">ForceEnglishOutput</span></span> | <span data-ttu-id="8eafe-120">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="8eafe-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8eafe-121">Pomoc</span><span class="sxs-lookup"><span data-stu-id="8eafe-121">Help</span></span> | <span data-ttu-id="8eafe-122">Wyświetla Pomoc dla samo polecenie Pomoc.</span><span class="sxs-lookup"><span data-stu-id="8eafe-122">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="8eafe-123">Język znaczników markdown</span><span class="sxs-lookup"><span data-stu-id="8eafe-123">Markdown</span></span> | <span data-ttu-id="8eafe-124">Drukowanie szczegółową pomoc w formacie markdown, gdy jest używany z `-All`.</span><span class="sxs-lookup"><span data-stu-id="8eafe-124">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="8eafe-125">W przeciwnym razie ignorowane.</span><span class="sxs-lookup"><span data-stu-id="8eafe-125">Ignored otherwise.</span></span> |
| <span data-ttu-id="8eafe-126">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="8eafe-126">NonInteractive</span></span> | <span data-ttu-id="8eafe-127">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="8eafe-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8eafe-128">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="8eafe-128">Verbosity</span></span> | <span data-ttu-id="8eafe-129">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="8eafe-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8eafe-130">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8eafe-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8eafe-131">Przykłady</span><span class="sxs-lookup"><span data-stu-id="8eafe-131">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
