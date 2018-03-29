---
title: Polecenie listy interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Informacje dotyczące polecenia listy nuget.exe
keywords: Odwołanie do listy nuget, lista pakietów — polecenie
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 61ad02eb99d6c56968c38841498df8aa9f74159d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="9bf73-104">Lista polecenia (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="9bf73-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="9bf73-105">**Dotyczy:** zużycie pakietu, publikowanie &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="9bf73-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="9bf73-106">Wyświetla listę pakietów z danego źródła.</span><span class="sxs-lookup"><span data-stu-id="9bf73-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="9bf73-107">Jeśli nie określono żadnych źródeł, wszystkie źródła zdefiniowane w pliku konfigurację globalną `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config`, są używane.</span><span class="sxs-lookup"><span data-stu-id="9bf73-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="9bf73-108">Jeśli `NuGet.Config` określa żadnych źródeł, następnie `list` korzysta z domyślnego źródła danych (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="9bf73-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="9bf73-109">Użycie</span><span class="sxs-lookup"><span data-stu-id="9bf73-109">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="9bf73-110">gdzie terminy wyszukiwania opcjonalne będzie odfiltrowania wyświetlonej listy.</span><span class="sxs-lookup"><span data-stu-id="9bf73-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="9bf73-111">Terminy wyszukiwania są stosowane do nazwy pakietów, znaczników i opisy pakietu, tak jak za pomocą ich nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9bf73-111">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="9bf73-112">Opcje</span><span class="sxs-lookup"><span data-stu-id="9bf73-112">Options</span></span>

| <span data-ttu-id="9bf73-113">Opcja</span><span class="sxs-lookup"><span data-stu-id="9bf73-113">Option</span></span> | <span data-ttu-id="9bf73-114">Opis</span><span class="sxs-lookup"><span data-stu-id="9bf73-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9bf73-115">AllVersions</span><span class="sxs-lookup"><span data-stu-id="9bf73-115">AllVersions</span></span> | <span data-ttu-id="9bf73-116">Wyświetl listę wszystkich wersji pakietu.</span><span class="sxs-lookup"><span data-stu-id="9bf73-116">List all versions of a package.</span></span> <span data-ttu-id="9bf73-117">Domyślnie wyświetlane jest tylko najnowszą wersję pakietu.</span><span class="sxs-lookup"><span data-stu-id="9bf73-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="9bf73-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="9bf73-118">ConfigFile</span></span> | <span data-ttu-id="9bf73-119">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="9bf73-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="9bf73-120">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="9bf73-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="9bf73-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="9bf73-121">ForceEnglishOutput</span></span> | <span data-ttu-id="9bf73-122">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="9bf73-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="9bf73-123">Pomoc</span><span class="sxs-lookup"><span data-stu-id="9bf73-123">Help</span></span> | <span data-ttu-id="9bf73-124">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="9bf73-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="9bf73-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="9bf73-125">IncludeDelisted</span></span> | <span data-ttu-id="9bf73-126">*(3.2 +)*  Wyświetlanie nieznajdujące się na liście pakietów.</span><span class="sxs-lookup"><span data-stu-id="9bf73-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="9bf73-127">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="9bf73-127">NonInteractive</span></span> | <span data-ttu-id="9bf73-128">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="9bf73-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="9bf73-129">Wydanie wstępne</span><span class="sxs-lookup"><span data-stu-id="9bf73-129">PreRelease</span></span> | <span data-ttu-id="9bf73-130">Zawiera pakiety wersji wstępnej na liście.</span><span class="sxs-lookup"><span data-stu-id="9bf73-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="9bf73-131">Źródło</span><span class="sxs-lookup"><span data-stu-id="9bf73-131">Source</span></span> | <span data-ttu-id="9bf73-132">Określa listę źródła pakietów do wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="9bf73-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="9bf73-133">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="9bf73-133">Verbosity</span></span> | <span data-ttu-id="9bf73-134">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="9bf73-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="9bf73-135">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="9bf73-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="9bf73-136">Przykłady</span><span class="sxs-lookup"><span data-stu-id="9bf73-136">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
