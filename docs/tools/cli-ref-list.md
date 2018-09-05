---
title: Interfejs wiersza polecenia NuGet lista — polecenie
description: Dokumentacja dotycząca polecenia nuget.exe list
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549804"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="7f666-103">Lista, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="7f666-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="7f666-104">**Dotyczy:** zużycie pakietów, publikowania &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="7f666-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="7f666-105">Wyświetla listę pakietów z danego źródła.</span><span class="sxs-lookup"><span data-stu-id="7f666-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="7f666-106">Jeśli nie określono żadnych źródeł, wszystkich źródeł są zdefiniowane w pliku konfiguracji globalnej `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config`, są używane.</span><span class="sxs-lookup"><span data-stu-id="7f666-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="7f666-107">Jeśli `NuGet.Config` określa żadnych źródeł, następnie `list` korzysta z domyślnego źródła danych (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="7f666-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="7f666-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="7f666-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="7f666-109">gdzie opcjonalne wyszukiwane terminy będą odfiltrowania wyświetlonej listy.</span><span class="sxs-lookup"><span data-stu-id="7f666-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="7f666-110">Wyszukiwane terminy są stosowane do nazw pakietów, tagi i opisy pakietu, tak jak podczas korzystania z nich w witrynie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7f666-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="7f666-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="7f666-111">Options</span></span>

| <span data-ttu-id="7f666-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="7f666-112">Option</span></span> | <span data-ttu-id="7f666-113">Opis</span><span class="sxs-lookup"><span data-stu-id="7f666-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7f666-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="7f666-114">AllVersions</span></span> | <span data-ttu-id="7f666-115">Wyświetla listę wszystkich wersji pakietu.</span><span class="sxs-lookup"><span data-stu-id="7f666-115">List all versions of a package.</span></span> <span data-ttu-id="7f666-116">Domyślnie jest wyświetlana tylko najnowszą wersję pakietu.</span><span class="sxs-lookup"><span data-stu-id="7f666-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="7f666-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7f666-117">ConfigFile</span></span> | <span data-ttu-id="7f666-118">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="7f666-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7f666-119">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="7f666-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="7f666-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7f666-120">ForceEnglishOutput</span></span> | <span data-ttu-id="7f666-121">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="7f666-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7f666-122">Pomoc</span><span class="sxs-lookup"><span data-stu-id="7f666-122">Help</span></span> | <span data-ttu-id="7f666-123">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="7f666-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="7f666-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="7f666-124">IncludeDelisted</span></span> | <span data-ttu-id="7f666-125">*(3.2 +)*  Wyświetlić nieznajdujące się na liście pakietów.</span><span class="sxs-lookup"><span data-stu-id="7f666-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="7f666-126">Nieinterakcyjnym</span><span class="sxs-lookup"><span data-stu-id="7f666-126">NonInteractive</span></span> | <span data-ttu-id="7f666-127">Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="7f666-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7f666-128">Wersja wstępna</span><span class="sxs-lookup"><span data-stu-id="7f666-128">PreRelease</span></span> | <span data-ttu-id="7f666-129">Obejmuje pakiety w wersjach wstępnych, na liście.</span><span class="sxs-lookup"><span data-stu-id="7f666-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="7f666-130">Źródło</span><span class="sxs-lookup"><span data-stu-id="7f666-130">Source</span></span> | <span data-ttu-id="7f666-131">Określa listę źródeł pakietów do wyszukania.</span><span class="sxs-lookup"><span data-stu-id="7f666-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="7f666-132">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="7f666-132">Verbosity</span></span> | <span data-ttu-id="7f666-133">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="7f666-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="7f666-134">Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7f666-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7f666-135">Przykłady</span><span class="sxs-lookup"><span data-stu-id="7f666-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
