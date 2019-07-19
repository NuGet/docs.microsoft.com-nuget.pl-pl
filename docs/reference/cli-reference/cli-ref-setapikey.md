---
title: Polecenie setapikey interfejsu wiersza polecenia NuGet
description: Dokumentacja polecenia NuGet. exe setapikey
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328286"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="7fe8f-103">setapikey — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="7fe8f-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="7fe8f-104">**Dotyczy:** użycie pakietu, publikowanie &bullet; **obsługiwanych wersji:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="7fe8f-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="7fe8f-105">Zapisuje klucz interfejsu API dla danego adresu URL serwera w `NuGet.Config` taki sposób, aby nie trzeba było go wprowadzać do kolejnych poleceń.</span><span class="sxs-lookup"><span data-stu-id="7fe8f-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="7fe8f-106">Użycie</span><span class="sxs-lookup"><span data-stu-id="7fe8f-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="7fe8f-107">gdzie `<source>` identyfikuje serwer i `<key>` jest kluczem lub hasłem do zapisania.</span><span class="sxs-lookup"><span data-stu-id="7fe8f-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="7fe8f-108">W `<source>` przypadku pominięcia zostanie założono NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="7fe8f-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="7fe8f-109">Opcje</span><span class="sxs-lookup"><span data-stu-id="7fe8f-109">Options</span></span>

| <span data-ttu-id="7fe8f-110">Opcja</span><span class="sxs-lookup"><span data-stu-id="7fe8f-110">Option</span></span> | <span data-ttu-id="7fe8f-111">Opis</span><span class="sxs-lookup"><span data-stu-id="7fe8f-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7fe8f-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7fe8f-112">ConfigFile</span></span> | <span data-ttu-id="7fe8f-113">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="7fe8f-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7fe8f-114">Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="7fe8f-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="7fe8f-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7fe8f-115">ForceEnglishOutput</span></span> | <span data-ttu-id="7fe8f-116">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="7fe8f-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7fe8f-117">Help</span><span class="sxs-lookup"><span data-stu-id="7fe8f-117">Help</span></span> | <span data-ttu-id="7fe8f-118">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="7fe8f-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="7fe8f-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="7fe8f-119">NonInteractive</span></span> | <span data-ttu-id="7fe8f-120">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7fe8f-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7fe8f-121">Verbosity</span><span class="sxs-lookup"><span data-stu-id="7fe8f-121">Verbosity</span></span> | <span data-ttu-id="7fe8f-122">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="7fe8f-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="7fe8f-123">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7fe8f-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7fe8f-124">Przykłady</span><span class="sxs-lookup"><span data-stu-id="7fe8f-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
