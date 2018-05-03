---
title: Lista interfejsu wiersza polecenia NuGet — polecenie
description: Informacje dotyczące polecenia listy nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4a44c70937e7cb49e472c53e9857e9f44d269f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="c7f29-103">Lista polecenia (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c7f29-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="c7f29-104">**Dotyczy:** zużycie pakietu, publikowanie &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="c7f29-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="c7f29-105">Wyświetla listę pakietów z danego źródła.</span><span class="sxs-lookup"><span data-stu-id="c7f29-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="c7f29-106">Jeśli nie określono żadnych źródeł, wszystkie źródła zdefiniowane w pliku konfigurację globalną `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config`, są używane.</span><span class="sxs-lookup"><span data-stu-id="c7f29-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="c7f29-107">Jeśli `NuGet.Config` określa żadnych źródeł, następnie `list` korzysta z domyślnego źródła danych (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="c7f29-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="c7f29-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="c7f29-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="c7f29-109">gdzie terminy wyszukiwania opcjonalne będzie odfiltrowania wyświetlonej listy.</span><span class="sxs-lookup"><span data-stu-id="c7f29-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="c7f29-110">Terminy wyszukiwania są stosowane do nazwy pakietów, znaczników i opisy pakietu, tak jak za pomocą ich nuget.org.</span><span class="sxs-lookup"><span data-stu-id="c7f29-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="c7f29-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="c7f29-111">Options</span></span>

| <span data-ttu-id="c7f29-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="c7f29-112">Option</span></span> | <span data-ttu-id="c7f29-113">Opis</span><span class="sxs-lookup"><span data-stu-id="c7f29-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c7f29-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="c7f29-114">AllVersions</span></span> | <span data-ttu-id="c7f29-115">Wyświetl listę wszystkich wersji pakietu.</span><span class="sxs-lookup"><span data-stu-id="c7f29-115">List all versions of a package.</span></span> <span data-ttu-id="c7f29-116">Domyślnie wyświetlane jest tylko najnowszą wersję pakietu.</span><span class="sxs-lookup"><span data-stu-id="c7f29-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="c7f29-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c7f29-117">ConfigFile</span></span> | <span data-ttu-id="c7f29-118">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="c7f29-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c7f29-119">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="c7f29-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="c7f29-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c7f29-120">ForceEnglishOutput</span></span> | <span data-ttu-id="c7f29-121">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="c7f29-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c7f29-122">Pomoc</span><span class="sxs-lookup"><span data-stu-id="c7f29-122">Help</span></span> | <span data-ttu-id="c7f29-123">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="c7f29-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="c7f29-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="c7f29-124">IncludeDelisted</span></span> | <span data-ttu-id="c7f29-125">*(3.2 +)*  Wyświetlanie nieznajdujące się na liście pakietów.</span><span class="sxs-lookup"><span data-stu-id="c7f29-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="c7f29-126">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="c7f29-126">NonInteractive</span></span> | <span data-ttu-id="c7f29-127">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="c7f29-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c7f29-128">Wydanie wstępne</span><span class="sxs-lookup"><span data-stu-id="c7f29-128">PreRelease</span></span> | <span data-ttu-id="c7f29-129">Zawiera pakiety wersji wstępnej na liście.</span><span class="sxs-lookup"><span data-stu-id="c7f29-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="c7f29-130">Źródło</span><span class="sxs-lookup"><span data-stu-id="c7f29-130">Source</span></span> | <span data-ttu-id="c7f29-131">Określa listę źródła pakietów do wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="c7f29-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="c7f29-132">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="c7f29-132">Verbosity</span></span> | <span data-ttu-id="c7f29-133">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="c7f29-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="c7f29-134">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c7f29-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c7f29-135">Przykłady</span><span class="sxs-lookup"><span data-stu-id="c7f29-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
