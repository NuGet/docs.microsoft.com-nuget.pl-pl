---
title: Interfejs wiersza polecenia NuGet polecenia Pomoc
description: Dokumentacja dotycząca pomocy polecenia nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546566"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="223c0-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="223c0-103">help or ?</span></span> <span data-ttu-id="223c0-104">command, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="223c0-104">command (NuGet CLI)</span></span>

<span data-ttu-id="223c0-105">**Dotyczy:** wszystkich &bullet; **obsługiwane wersje**: wszystkie</span><span class="sxs-lookup"><span data-stu-id="223c0-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="223c0-106">Wyświetla ogólne informacje i pomoc dotyczącą określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="223c0-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="223c0-107">Użycie</span><span class="sxs-lookup"><span data-stu-id="223c0-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="223c0-108">gdzie [polecenie] identyfikuje określonego polecenia, dla którego chcesz wyświetlić Pomoc.</span><span class="sxs-lookup"><span data-stu-id="223c0-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="223c0-109">W niektórych poleceniach zachować ostrożność, aby określić *pomocy* najpierw, przy użyciu `nuget help install`, ponieważ pakiet o nazwie "help" w witrynie nuget.org. Jeśli nadasz polecenie `nuget install help`, nie będzie uzyskać pomoc dotyczącą polecenia instalacji, ale zamiast tego zostanie zainstalowany pakiet o nazwie pomocy.</span><span class="sxs-lookup"><span data-stu-id="223c0-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="223c0-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="223c0-110">Options</span></span>

| <span data-ttu-id="223c0-111">Opcja</span><span class="sxs-lookup"><span data-stu-id="223c0-111">Option</span></span> | <span data-ttu-id="223c0-112">Opis</span><span class="sxs-lookup"><span data-stu-id="223c0-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="223c0-113">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="223c0-113">All</span></span> | <span data-ttu-id="223c0-114">Drukuj szczegółową pomoc dotyczącą wszystkich dostępnych poleceń; ignorowane, jeśli podano określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="223c0-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="223c0-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="223c0-115">ConfigFile</span></span> | <span data-ttu-id="223c0-116">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="223c0-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="223c0-117">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="223c0-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="223c0-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="223c0-118">ForceEnglishOutput</span></span> | <span data-ttu-id="223c0-119">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="223c0-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="223c0-120">Pomoc</span><span class="sxs-lookup"><span data-stu-id="223c0-120">Help</span></span> | <span data-ttu-id="223c0-121">Wyświetla Pomoc dla niej samo polecenie Pomoc.</span><span class="sxs-lookup"><span data-stu-id="223c0-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="223c0-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="223c0-122">Markdown</span></span> | <span data-ttu-id="223c0-123">Drukuj szczegółową pomoc w formacie markdown, gdy jest używane z `-All`.</span><span class="sxs-lookup"><span data-stu-id="223c0-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="223c0-124">Ignorowany w innych przypadkach.</span><span class="sxs-lookup"><span data-stu-id="223c0-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="223c0-125">Nieinterakcyjnym</span><span class="sxs-lookup"><span data-stu-id="223c0-125">NonInteractive</span></span> | <span data-ttu-id="223c0-126">Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="223c0-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="223c0-127">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="223c0-127">Verbosity</span></span> | <span data-ttu-id="223c0-128">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="223c0-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="223c0-129">Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="223c0-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="223c0-130">Przykłady</span><span class="sxs-lookup"><span data-stu-id="223c0-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
