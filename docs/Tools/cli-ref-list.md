---
title: Polecenie listy interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Informacje dotyczące polecenia listy nuget.exe"
keywords: "Odwołanie do listy nuget, lista pakietów — polecenie"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5a1f68aaffd26a0f903aa3a7a4a450a0121191c3
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="4bad1-104">Lista polecenia (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="4bad1-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="4bad1-105">**Dotyczy:** zużycie pakietu, publikowanie &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="4bad1-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="4bad1-106">Wyświetla listę pakietów z danego źródła.</span><span class="sxs-lookup"><span data-stu-id="4bad1-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="4bad1-107">Jeśli nie określono żadnych źródeł, wszystkie źródła zdefiniowane w pliku konfigurację globalną `%AppData%\NuGet\NuGet.Config`, są używane.</span><span class="sxs-lookup"><span data-stu-id="4bad1-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="4bad1-108">Jeśli `NuGet.Config` określa żadnych źródeł, następnie `list` korzysta z domyślnego źródła danych (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="4bad1-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="4bad1-109">Użycie</span><span class="sxs-lookup"><span data-stu-id="4bad1-109">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="4bad1-110">gdzie terminy wyszukiwania opcjonalne będzie odfiltrowania wyświetlonej listy.</span><span class="sxs-lookup"><span data-stu-id="4bad1-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="4bad1-111">Terminy wyszukiwania są stosowane do nazwy pakietów, znaczników i opisy pakietu.</span><span class="sxs-lookup"><span data-stu-id="4bad1-111">Search terms are applied to the names of packages, tags, and package descriptions.</span></span>

## <a name="options"></a><span data-ttu-id="4bad1-112">Opcje</span><span class="sxs-lookup"><span data-stu-id="4bad1-112">Options</span></span>

| <span data-ttu-id="4bad1-113">Opcja</span><span class="sxs-lookup"><span data-stu-id="4bad1-113">Option</span></span> | <span data-ttu-id="4bad1-114">Opis</span><span class="sxs-lookup"><span data-stu-id="4bad1-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4bad1-115">AllVersions</span><span class="sxs-lookup"><span data-stu-id="4bad1-115">AllVersions</span></span> | <span data-ttu-id="4bad1-116">Wyświetl listę wszystkich wersji pakietu.</span><span class="sxs-lookup"><span data-stu-id="4bad1-116">List all versions of a package.</span></span> <span data-ttu-id="4bad1-117">Domyślnie wyświetlane jest tylko najnowszą wersję pakietu.</span><span class="sxs-lookup"><span data-stu-id="4bad1-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="4bad1-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="4bad1-118">ConfigFile</span></span> | <span data-ttu-id="4bad1-119">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="4bad1-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="4bad1-120">Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany.</span><span class="sxs-lookup"><span data-stu-id="4bad1-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="4bad1-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="4bad1-121">ForceEnglishOutput</span></span> | <span data-ttu-id="4bad1-122">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="4bad1-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="4bad1-123">Pomoc</span><span class="sxs-lookup"><span data-stu-id="4bad1-123">Help</span></span> | <span data-ttu-id="4bad1-124">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="4bad1-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="4bad1-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="4bad1-125">IncludeDelisted</span></span> | <span data-ttu-id="4bad1-126">*(3.2 +)*  Wyświetlanie nieznajdujące się na liście pakietów.</span><span class="sxs-lookup"><span data-stu-id="4bad1-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="4bad1-127">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="4bad1-127">NonInteractive</span></span> | <span data-ttu-id="4bad1-128">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="4bad1-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="4bad1-129">Wydanie wstępne</span><span class="sxs-lookup"><span data-stu-id="4bad1-129">PreRelease</span></span> | <span data-ttu-id="4bad1-130">Zawiera pakiety wersji wstępnej na liście.</span><span class="sxs-lookup"><span data-stu-id="4bad1-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="4bad1-131">Źródło</span><span class="sxs-lookup"><span data-stu-id="4bad1-131">Source</span></span> | <span data-ttu-id="4bad1-132">Określa listę źródła pakietów do wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="4bad1-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="4bad1-133">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="4bad1-133">Verbosity</span></span> | <span data-ttu-id="4bad1-134">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="4bad1-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="4bad1-135">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="4bad1-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="4bad1-136">Przykłady</span><span class="sxs-lookup"><span data-stu-id="4bad1-136">Examples</span></span>

```cli
nuget list

nuget list -Verbosity detailed -AllVersions
```
