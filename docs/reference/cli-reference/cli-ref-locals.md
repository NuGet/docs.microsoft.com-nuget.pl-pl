---
title: Polecenie locale interfejsu wiersza polecenia NuGet
description: Informacje dotyczące polecenia Locals NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328346"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="1f1e5-103">locals command, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="1f1e5-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="1f1e5-104">**Dotyczy:** **obsługiwane wersje** pakietów &bullet; : 3.3+</span><span class="sxs-lookup"><span data-stu-id="1f1e5-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="1f1e5-105">Czyści lub wyświetla lokalne zasoby NuGet, takie jak folder *http pamięci*podręcznej, *pakiety globalne* i folder tymczasowy.</span><span class="sxs-lookup"><span data-stu-id="1f1e5-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="1f1e5-106">Można również użyć polecenia, aby wyświetlić listę tych lokalizacji. `locals`</span><span class="sxs-lookup"><span data-stu-id="1f1e5-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="1f1e5-107">Aby uzyskać więcej informacji, zobacz [Zarządzanie pakietami globalnymi i folderami pamięci](../../consume-packages/managing-the-global-packages-and-cache-folders.md)podręcznej.</span><span class="sxs-lookup"><span data-stu-id="1f1e5-107">For more information, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="1f1e5-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="1f1e5-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="1f1e5-109">gdzie `<folder>` jest jedną z `all`, `http-cache` `global-packages` `temp` `plugins-cache` , `packages-cache` *(3,5 i wcześniejszą)* ,, *(3.4 +)* i *(4.8 +)* .</span><span class="sxs-lookup"><span data-stu-id="1f1e5-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="1f1e5-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="1f1e5-110">Options</span></span>

| <span data-ttu-id="1f1e5-111">Opcja</span><span class="sxs-lookup"><span data-stu-id="1f1e5-111">Option</span></span> | <span data-ttu-id="1f1e5-112">Opis</span><span class="sxs-lookup"><span data-stu-id="1f1e5-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1f1e5-113">Clear</span><span class="sxs-lookup"><span data-stu-id="1f1e5-113">Clear</span></span> | <span data-ttu-id="1f1e5-114">Czyści określony folder.</span><span class="sxs-lookup"><span data-stu-id="1f1e5-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="1f1e5-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1f1e5-115">ConfigFile</span></span> | <span data-ttu-id="1f1e5-116">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="1f1e5-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1f1e5-117">Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="1f1e5-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="1f1e5-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1f1e5-118">ForceEnglishOutput</span></span> | <span data-ttu-id="1f1e5-119">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="1f1e5-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1f1e5-120">Help</span><span class="sxs-lookup"><span data-stu-id="1f1e5-120">Help</span></span> | <span data-ttu-id="1f1e5-121">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="1f1e5-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="1f1e5-122">Lista</span><span class="sxs-lookup"><span data-stu-id="1f1e5-122">List</span></span> | <span data-ttu-id="1f1e5-123">Wyświetla lokalizację określonego folderu lub lokalizacje wszystkich folderów, jeśli są używane ze *wszystkimi*.</span><span class="sxs-lookup"><span data-stu-id="1f1e5-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="1f1e5-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="1f1e5-124">NonInteractive</span></span> | <span data-ttu-id="1f1e5-125">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1f1e5-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1f1e5-126">Verbosity</span><span class="sxs-lookup"><span data-stu-id="1f1e5-126">Verbosity</span></span> | <span data-ttu-id="1f1e5-127">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="1f1e5-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="1f1e5-128">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1f1e5-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1f1e5-129">Przykłady</span><span class="sxs-lookup"><span data-stu-id="1f1e5-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="1f1e5-130">Aby uzyskać więcej przykładów, zobacz [Zarządzanie pakietami globalnymi i folderami pamięci](../../consume-packages/managing-the-global-packages-and-cache-folders.md)podręcznej.</span><span class="sxs-lookup"><span data-stu-id="1f1e5-130">For additional examples, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
