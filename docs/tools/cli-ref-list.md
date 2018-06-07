---
title: Lista interfejsu wiersza polecenia NuGet — polecenie
description: Informacje dotyczące polecenia listy nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b0f144d8abbba7388fe39cd113e4eeddccbca2c6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818441"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="e7799-103">Lista polecenia (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e7799-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="e7799-104">**Dotyczy:** zużycie pakietu, publikowanie &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="e7799-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="e7799-105">Wyświetla listę pakietów z danego źródła.</span><span class="sxs-lookup"><span data-stu-id="e7799-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="e7799-106">Jeśli nie określono żadnych źródeł, wszystkie źródła zdefiniowane w pliku konfigurację globalną `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config`, są używane.</span><span class="sxs-lookup"><span data-stu-id="e7799-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="e7799-107">Jeśli `NuGet.Config` określa żadnych źródeł, następnie `list` korzysta z domyślnego źródła danych (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="e7799-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="e7799-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="e7799-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="e7799-109">gdzie terminy wyszukiwania opcjonalne będzie odfiltrowania wyświetlonej listy.</span><span class="sxs-lookup"><span data-stu-id="e7799-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="e7799-110">Terminy wyszukiwania są stosowane do nazwy pakietów, znaczników i opisy pakietu, tak jak za pomocą ich nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e7799-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="e7799-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="e7799-111">Options</span></span>

| <span data-ttu-id="e7799-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="e7799-112">Option</span></span> | <span data-ttu-id="e7799-113">Opis</span><span class="sxs-lookup"><span data-stu-id="e7799-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e7799-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="e7799-114">AllVersions</span></span> | <span data-ttu-id="e7799-115">Wyświetl listę wszystkich wersji pakietu.</span><span class="sxs-lookup"><span data-stu-id="e7799-115">List all versions of a package.</span></span> <span data-ttu-id="e7799-116">Domyślnie wyświetlane jest tylko najnowszą wersję pakietu.</span><span class="sxs-lookup"><span data-stu-id="e7799-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="e7799-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e7799-117">ConfigFile</span></span> | <span data-ttu-id="e7799-118">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="e7799-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e7799-119">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="e7799-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="e7799-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e7799-120">ForceEnglishOutput</span></span> | <span data-ttu-id="e7799-121">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="e7799-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e7799-122">Pomoc</span><span class="sxs-lookup"><span data-stu-id="e7799-122">Help</span></span> | <span data-ttu-id="e7799-123">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="e7799-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="e7799-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="e7799-124">IncludeDelisted</span></span> | <span data-ttu-id="e7799-125">*(3.2 +)*  Wyświetlanie nieznajdujące się na liście pakietów.</span><span class="sxs-lookup"><span data-stu-id="e7799-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="e7799-126">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="e7799-126">NonInteractive</span></span> | <span data-ttu-id="e7799-127">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="e7799-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e7799-128">Wydanie wstępne</span><span class="sxs-lookup"><span data-stu-id="e7799-128">PreRelease</span></span> | <span data-ttu-id="e7799-129">Zawiera pakiety wersji wstępnej na liście.</span><span class="sxs-lookup"><span data-stu-id="e7799-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="e7799-130">Źródło</span><span class="sxs-lookup"><span data-stu-id="e7799-130">Source</span></span> | <span data-ttu-id="e7799-131">Określa listę źródła pakietów do wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="e7799-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="e7799-132">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="e7799-132">Verbosity</span></span> | <span data-ttu-id="e7799-133">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="e7799-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="e7799-134">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e7799-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e7799-135">Przykłady</span><span class="sxs-lookup"><span data-stu-id="e7799-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
