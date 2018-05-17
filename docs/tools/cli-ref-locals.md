---
title: Polecenie zmiennych lokalnych NuGet interfejsu wiersza polecenia
description: Dokumentacja dotycząca nuget.exe polecenia zmiennych lokalnych
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ac07dc306bc23c2fedd33c5627e8d34a6098387c
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="cd0bc-103">locals command, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="cd0bc-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="cd0bc-104">**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="cd0bc-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="cd0bc-105">Czyści lub wyświetla ich listę zasobów lokalnych NuGet takich jak *pamięci podręcznej http*, *globalne pakiety* folder i folderu tymczasowego.</span><span class="sxs-lookup"><span data-stu-id="cd0bc-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="cd0bc-106">`locals` Polecenia można również wyświetlić listę tych lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="cd0bc-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="cd0bc-107">Aby uzyskać więcej informacji, zobacz [Zarządzanie globalne pakietów i foldery pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="cd0bc-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="cd0bc-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="cd0bc-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="cd0bc-109">gdzie `<folder>` jest jednym z `all`, `http-cache`, `packages-cache` *(3.5 i wcześniejszymi)*, `global-packages`, i `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="cd0bc-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="cd0bc-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="cd0bc-110">Options</span></span>

| <span data-ttu-id="cd0bc-111">Opcja</span><span class="sxs-lookup"><span data-stu-id="cd0bc-111">Option</span></span> | <span data-ttu-id="cd0bc-112">Opis</span><span class="sxs-lookup"><span data-stu-id="cd0bc-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cd0bc-113">Wyczyść</span><span class="sxs-lookup"><span data-stu-id="cd0bc-113">Clear</span></span> | <span data-ttu-id="cd0bc-114">Usuwa określony folder.</span><span class="sxs-lookup"><span data-stu-id="cd0bc-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="cd0bc-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="cd0bc-115">ConfigFile</span></span> | <span data-ttu-id="cd0bc-116">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="cd0bc-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="cd0bc-117">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="cd0bc-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="cd0bc-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="cd0bc-118">ForceEnglishOutput</span></span> | <span data-ttu-id="cd0bc-119">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="cd0bc-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="cd0bc-120">Pomoc</span><span class="sxs-lookup"><span data-stu-id="cd0bc-120">Help</span></span> | <span data-ttu-id="cd0bc-121">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="cd0bc-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="cd0bc-122">Lista</span><span class="sxs-lookup"><span data-stu-id="cd0bc-122">List</span></span> | <span data-ttu-id="cd0bc-123">Wyświetla lokalizację określony folder lub lokalizacje wszystkich folderów, gdy jest używany z *wszystkich*.</span><span class="sxs-lookup"><span data-stu-id="cd0bc-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="cd0bc-124">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="cd0bc-124">NonInteractive</span></span> | <span data-ttu-id="cd0bc-125">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="cd0bc-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="cd0bc-126">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="cd0bc-126">Verbosity</span></span> | <span data-ttu-id="cd0bc-127">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="cd0bc-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="cd0bc-128">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="cd0bc-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="cd0bc-129">Przykłady</span><span class="sxs-lookup"><span data-stu-id="cd0bc-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="cd0bc-130">Aby uzyskać dodatkowe przykłady, zobacz [Zarządzanie globalne pakietów i foldery pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="cd0bc-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
