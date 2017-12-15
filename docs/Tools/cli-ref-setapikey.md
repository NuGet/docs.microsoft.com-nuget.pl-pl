---
title: Polecenie setapikey interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a64c0462-973d-4100-ba3f-8902a2b127f7
description: "Informacje dotyczące polecenia setapikey nuget.exe"
keywords: "polecenie setapikey nuget setapikey odwołania"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a07c35b8bdd57157391e391e04a90204342b1d5c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
## <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="7b548-104">polecenie setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7b548-104">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="7b548-105">**Dotyczy:** zużycie pakietu, publikowanie &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="7b548-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="7b548-106">Zapisuje klucz interfejsu API dla danego adresu URL podanego serwera do `NuGet.Config` tak, aby nie trzeba wprowadzać dla kolejnych poleceń.</span><span class="sxs-lookup"><span data-stu-id="7b548-106">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="7b548-107">Użycie</span><span class="sxs-lookup"><span data-stu-id="7b548-107">Usage</span></span>

```
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="7b548-108">gdzie `<source>` identyfikuje serwer i `<key>` to klucz lub hasło, aby zapisać.</span><span class="sxs-lookup"><span data-stu-id="7b548-108">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="7b548-109">Jeśli `<source>` jest pominięty, zakłada nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7b548-109">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="7b548-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="7b548-110">Options</span></span>

| <span data-ttu-id="7b548-111">Opcja</span><span class="sxs-lookup"><span data-stu-id="7b548-111">Option</span></span> | <span data-ttu-id="7b548-112">Opis</span><span class="sxs-lookup"><span data-stu-id="7b548-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7b548-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7b548-113">ConfigFile</span></span> | <span data-ttu-id="7b548-114">*(2.5 +)*  NuGet pliku konfiguracji do zmodyfikowania.</span><span class="sxs-lookup"><span data-stu-id="7b548-114">*(2.5+)* The NuGet configuration file to modify.</span></span> <span data-ttu-id="7b548-115">Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany.</span><span class="sxs-lookup"><span data-stu-id="7b548-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="7b548-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7b548-116">ForceEnglishOutput</span></span> | <span data-ttu-id="7b548-117">*(3.5 +)*  Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="7b548-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7b548-118">Pomoc</span><span class="sxs-lookup"><span data-stu-id="7b548-118">Help</span></span> | <span data-ttu-id="7b548-119">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="7b548-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="7b548-120">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="7b548-120">NonInteractive</span></span> | <span data-ttu-id="7b548-121">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="7b548-121">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7b548-122">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="7b548-122">Verbosity</span></span> | <span data-ttu-id="7b548-123">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="7b548-123">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="7b548-124">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7b548-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7b548-125">Przykłady</span><span class="sxs-lookup"><span data-stu-id="7b548-125">Examples</span></span>

```
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
