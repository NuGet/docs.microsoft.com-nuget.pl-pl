---
title: Polecenie lokalne interfejs wiersza polecenia NuGet
description: Dokumentacja dotycząca polecenia nuget.exe zmiennych lokalnych
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ea216c4651ba9619bc3b6a7ab52546fd299b0bb6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545031"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="792e2-103">locals command, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="792e2-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="792e2-104">**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="792e2-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="792e2-105">Usuwa lub wyświetla ich listę zasobów lokalnych NuGet takich jak *pamięci podręcznej http*, *globalnymi pakietami* folder i folderu tymczasowego.</span><span class="sxs-lookup"><span data-stu-id="792e2-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="792e2-106">`locals` Polecenia można również wyświetlić listę tych lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="792e2-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="792e2-107">Aby uzyskać więcej informacji, zobacz [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="792e2-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="792e2-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="792e2-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="792e2-109">gdzie `<folder>` jest jednym z `all`, `http-cache`, `packages-cache` *(3.5 i starszych)*, `global-packages`, `temp` *(3.4 i nowsze)*, i `plugins-cache` *(4.8 +)*.</span><span class="sxs-lookup"><span data-stu-id="792e2-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="792e2-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="792e2-110">Options</span></span>

| <span data-ttu-id="792e2-111">Opcja</span><span class="sxs-lookup"><span data-stu-id="792e2-111">Option</span></span> | <span data-ttu-id="792e2-112">Opis</span><span class="sxs-lookup"><span data-stu-id="792e2-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="792e2-113">Usuń zaznaczenie</span><span class="sxs-lookup"><span data-stu-id="792e2-113">Clear</span></span> | <span data-ttu-id="792e2-114">Usuwa określony folder.</span><span class="sxs-lookup"><span data-stu-id="792e2-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="792e2-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="792e2-115">ConfigFile</span></span> | <span data-ttu-id="792e2-116">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="792e2-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="792e2-117">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="792e2-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="792e2-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="792e2-118">ForceEnglishOutput</span></span> | <span data-ttu-id="792e2-119">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="792e2-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="792e2-120">Pomoc</span><span class="sxs-lookup"><span data-stu-id="792e2-120">Help</span></span> | <span data-ttu-id="792e2-121">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="792e2-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="792e2-122">Lista</span><span class="sxs-lookup"><span data-stu-id="792e2-122">List</span></span> | <span data-ttu-id="792e2-123">Wyświetla listę lokalizacji wskazanym folderze lub lokalizacje wszystkich folderów, gdy jest używane z *wszystkich*.</span><span class="sxs-lookup"><span data-stu-id="792e2-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="792e2-124">Nieinterakcyjnym</span><span class="sxs-lookup"><span data-stu-id="792e2-124">NonInteractive</span></span> | <span data-ttu-id="792e2-125">Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="792e2-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="792e2-126">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="792e2-126">Verbosity</span></span> | <span data-ttu-id="792e2-127">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="792e2-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="792e2-128">Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="792e2-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="792e2-129">Przykłady</span><span class="sxs-lookup"><span data-stu-id="792e2-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="792e2-130">Aby uzyskać więcej przykładów, zobacz [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="792e2-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
