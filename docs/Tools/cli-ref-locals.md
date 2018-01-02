---
title: Polecenie zmiennych lokalnych interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 7f672c7c-74c9-4296-bc27-4d47882b541c
description: "Dokumentacja dotycząca nuget.exe polecenia zmiennych lokalnych"
keywords: "Odwołanie do zmiennych lokalnych nuget, polecenie zmiennych lokalnych"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8cc06eedc20507e2bdd210e40c471ff551b89563
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
## <a name="locals-command-nuget-cli"></a><span data-ttu-id="a527e-104">Zmienne lokalne polecenia (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a527e-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="a527e-105">**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="a527e-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="a527e-106">Czyści lub wyświetla ich listę zasobów lokalnych NuGet pamięci podręcznej żądania http, pakiety w pamięci podręcznej i folderu pakietów globalne dla komputera.</span><span class="sxs-lookup"><span data-stu-id="a527e-106">Clears or lists local NuGet resources such as the http-request cache, packages cache, and the machine-wide global packages folder.</span></span> <span data-ttu-id="a527e-107">`locals` Polecenia można również wyświetlić listę tych lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="a527e-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="a527e-108">Aby uzyskać więcej informacji, zobacz [Zarządzanie pamięci podręcznej NuGet](../consume-packages/managing-the-nuget-cache.md).</span><span class="sxs-lookup"><span data-stu-id="a527e-108">For more information, see [Managing the NuGet Cache](../consume-packages/managing-the-nuget-cache.md).</span></span>

## <a name="usage"></a><span data-ttu-id="a527e-109">Użycie</span><span class="sxs-lookup"><span data-stu-id="a527e-109">Usage</span></span>

```
nuget locals <cache> [options]
```

<span data-ttu-id="a527e-110">gdzie `<cache>` jest jednym z `all`, `http-cache`, `packages-cache`, `global-packages`, i `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="a527e-110">where `<cache>` is one of `all`, `http-cache`, `packages-cache`, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="a527e-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="a527e-111">Options</span></span>

| <span data-ttu-id="a527e-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="a527e-112">Option</span></span> | <span data-ttu-id="a527e-113">Opis</span><span class="sxs-lookup"><span data-stu-id="a527e-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a527e-114">Wyczyść</span><span class="sxs-lookup"><span data-stu-id="a527e-114">Clear</span></span> | <span data-ttu-id="a527e-115">Usuwa określony pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="a527e-115">Clears the specified cache.</span></span> |
| <span data-ttu-id="a527e-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a527e-116">ConfigFile</span></span> | <span data-ttu-id="a527e-117">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="a527e-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a527e-118">Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany.</span><span class="sxs-lookup"><span data-stu-id="a527e-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="a527e-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a527e-119">ForceEnglishOutput</span></span> | <span data-ttu-id="a527e-120">*(3.5 +) * Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="a527e-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a527e-121">Pomoc</span><span class="sxs-lookup"><span data-stu-id="a527e-121">Help</span></span> | <span data-ttu-id="a527e-122">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="a527e-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="a527e-123">Lista</span><span class="sxs-lookup"><span data-stu-id="a527e-123">List</span></span> | <span data-ttu-id="a527e-124">Wyświetla lokalizację pamięci podręcznej określony lub lokalizacje wszystkich usług pamięć podręczna w przypadku użycia z *wszystkich*.</span><span class="sxs-lookup"><span data-stu-id="a527e-124">Lists the location of the specified cache, or the locations of all caches when used with *all*.</span></span> |
| <span data-ttu-id="a527e-125">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="a527e-125">NonInteractive</span></span> | <span data-ttu-id="a527e-126">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="a527e-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a527e-127">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="a527e-127">Verbosity</span></span> | <span data-ttu-id="a527e-128">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="a527e-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a527e-129">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a527e-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a527e-130">Przykłady</span><span class="sxs-lookup"><span data-stu-id="a527e-130">Examples</span></span>

```
nuget locals all -list
nuget locals http-cache -clear
```
