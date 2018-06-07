---
title: Polecenie zmiennych lokalnych NuGet interfejsu wiersza polecenia
description: Dokumentacja dotycząca nuget.exe polecenia zmiennych lokalnych
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 90e8c85e7a3e0e9520933e2ddd6dd84447475f2b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818204"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="8aa35-103">locals command, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="8aa35-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="8aa35-104">**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="8aa35-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="8aa35-105">Czyści lub wyświetla ich listę zasobów lokalnych NuGet takich jak *pamięci podręcznej http*, *globalne pakiety* folder i folderu tymczasowego.</span><span class="sxs-lookup"><span data-stu-id="8aa35-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="8aa35-106">`locals` Polecenia można również wyświetlić listę tych lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="8aa35-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="8aa35-107">Aby uzyskać więcej informacji, zobacz [Zarządzanie globalne pakietów i foldery pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="8aa35-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="8aa35-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="8aa35-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="8aa35-109">gdzie `<folder>` jest jednym z `all`, `http-cache`, `packages-cache` *(3.5 i wcześniejszymi)*, `global-packages`, i `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="8aa35-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="8aa35-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="8aa35-110">Options</span></span>

| <span data-ttu-id="8aa35-111">Opcja</span><span class="sxs-lookup"><span data-stu-id="8aa35-111">Option</span></span> | <span data-ttu-id="8aa35-112">Opis</span><span class="sxs-lookup"><span data-stu-id="8aa35-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8aa35-113">Wyczyść</span><span class="sxs-lookup"><span data-stu-id="8aa35-113">Clear</span></span> | <span data-ttu-id="8aa35-114">Usuwa określony folder.</span><span class="sxs-lookup"><span data-stu-id="8aa35-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="8aa35-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8aa35-115">ConfigFile</span></span> | <span data-ttu-id="8aa35-116">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="8aa35-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8aa35-117">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="8aa35-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="8aa35-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8aa35-118">ForceEnglishOutput</span></span> | <span data-ttu-id="8aa35-119">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="8aa35-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8aa35-120">Pomoc</span><span class="sxs-lookup"><span data-stu-id="8aa35-120">Help</span></span> | <span data-ttu-id="8aa35-121">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="8aa35-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="8aa35-122">Lista</span><span class="sxs-lookup"><span data-stu-id="8aa35-122">List</span></span> | <span data-ttu-id="8aa35-123">Wyświetla lokalizację określony folder lub lokalizacje wszystkich folderów, gdy jest używany z *wszystkich*.</span><span class="sxs-lookup"><span data-stu-id="8aa35-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="8aa35-124">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="8aa35-124">NonInteractive</span></span> | <span data-ttu-id="8aa35-125">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="8aa35-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8aa35-126">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="8aa35-126">Verbosity</span></span> | <span data-ttu-id="8aa35-127">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="8aa35-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8aa35-128">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8aa35-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8aa35-129">Przykłady</span><span class="sxs-lookup"><span data-stu-id="8aa35-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="8aa35-130">Aby uzyskać dodatkowe przykłady, zobacz [Zarządzanie globalne pakietów i foldery pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="8aa35-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
