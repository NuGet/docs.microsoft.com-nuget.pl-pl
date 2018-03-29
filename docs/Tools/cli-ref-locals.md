---
title: Polecenie zmiennych lokalnych interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Dokumentacja dotycząca nuget.exe polecenia zmiennych lokalnych
keywords: Odwołanie do zmiennych lokalnych nuget, polecenie zmiennych lokalnych
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0122c79e55b12838bd123cf91bfcbc5dbbd2a65c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="08072-104">Zmienne lokalne polecenia (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="08072-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="08072-105">**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="08072-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="08072-106">Czyści lub wyświetla ich listę zasobów lokalnych NuGet takich jak *pamięci podręcznej http*, *globalne pakiety* folder i folderu tymczasowego.</span><span class="sxs-lookup"><span data-stu-id="08072-106">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="08072-107">`locals` Polecenia można również wyświetlić listę tych lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="08072-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="08072-108">Aby uzyskać więcej informacji, zobacz [Zarządzanie globalne pakietów i foldery pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="08072-108">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="08072-109">Użycie</span><span class="sxs-lookup"><span data-stu-id="08072-109">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="08072-110">gdzie `<folder>` jest jednym z `all`, `http-cache`, `packages-cache` *(3.5 i wcześniejszymi)*, `global-packages`, i `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="08072-110">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="08072-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="08072-111">Options</span></span>

| <span data-ttu-id="08072-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="08072-112">Option</span></span> | <span data-ttu-id="08072-113">Opis</span><span class="sxs-lookup"><span data-stu-id="08072-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="08072-114">Wyczyść</span><span class="sxs-lookup"><span data-stu-id="08072-114">Clear</span></span> | <span data-ttu-id="08072-115">Usuwa określony folder.</span><span class="sxs-lookup"><span data-stu-id="08072-115">Clears the specified folder.</span></span> |
| <span data-ttu-id="08072-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="08072-116">ConfigFile</span></span> | <span data-ttu-id="08072-117">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="08072-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="08072-118">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="08072-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="08072-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="08072-119">ForceEnglishOutput</span></span> | <span data-ttu-id="08072-120">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="08072-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="08072-121">Pomoc</span><span class="sxs-lookup"><span data-stu-id="08072-121">Help</span></span> | <span data-ttu-id="08072-122">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="08072-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="08072-123">Lista</span><span class="sxs-lookup"><span data-stu-id="08072-123">List</span></span> | <span data-ttu-id="08072-124">Wyświetla lokalizację określony folder lub lokalizacje wszystkich folderów, gdy jest używany z *wszystkich*.</span><span class="sxs-lookup"><span data-stu-id="08072-124">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="08072-125">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="08072-125">NonInteractive</span></span> | <span data-ttu-id="08072-126">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="08072-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="08072-127">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="08072-127">Verbosity</span></span> | <span data-ttu-id="08072-128">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="08072-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="08072-129">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="08072-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="08072-130">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08072-130">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="08072-131">Aby uzyskać dodatkowe przykłady, zobacz [Zarządzanie globalne pakietów i foldery pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="08072-131">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
