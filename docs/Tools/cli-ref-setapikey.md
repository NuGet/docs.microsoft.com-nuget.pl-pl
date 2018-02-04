---
title: Polecenie setapikey interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Informacje dotyczące polecenia setapikey nuget.exe"
keywords: "polecenie setapikey nuget setapikey odwołania"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ca6caddbf1404bcaa1ca068c9556f7cf0c651947
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/02/2018
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="f8326-104">polecenie setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f8326-104">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="f8326-105">**Dotyczy:** zużycie pakietu, publikowanie &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="f8326-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="f8326-106">Zapisuje klucz interfejsu API dla danego adresu URL podanego serwera do `NuGet.Config` tak, aby nie trzeba wprowadzać dla kolejnych poleceń.</span><span class="sxs-lookup"><span data-stu-id="f8326-106">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="f8326-107">Użycie</span><span class="sxs-lookup"><span data-stu-id="f8326-107">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="f8326-108">gdzie `<source>` identyfikuje serwer i `<key>` to klucz lub hasło, aby zapisać.</span><span class="sxs-lookup"><span data-stu-id="f8326-108">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="f8326-109">Jeśli `<source>` jest pominięty, zakłada nuget.org.</span><span class="sxs-lookup"><span data-stu-id="f8326-109">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="f8326-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="f8326-110">Options</span></span>

| <span data-ttu-id="f8326-111">Opcja</span><span class="sxs-lookup"><span data-stu-id="f8326-111">Option</span></span> | <span data-ttu-id="f8326-112">Opis</span><span class="sxs-lookup"><span data-stu-id="f8326-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f8326-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f8326-113">ConfigFile</span></span> | <span data-ttu-id="f8326-114">Plik konfiguracji NuGet do zmodyfikowania.</span><span class="sxs-lookup"><span data-stu-id="f8326-114">The NuGet configuration file to modify.</span></span> <span data-ttu-id="f8326-115">Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany.</span><span class="sxs-lookup"><span data-stu-id="f8326-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="f8326-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f8326-116">ForceEnglishOutput</span></span> | <span data-ttu-id="f8326-117">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="f8326-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f8326-118">Pomoc</span><span class="sxs-lookup"><span data-stu-id="f8326-118">Help</span></span> | <span data-ttu-id="f8326-119">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="f8326-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="f8326-120">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="f8326-120">NonInteractive</span></span> | <span data-ttu-id="f8326-121">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="f8326-121">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f8326-122">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="f8326-122">Verbosity</span></span> | <span data-ttu-id="f8326-123">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="f8326-123">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f8326-124">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f8326-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f8326-125">Przykłady</span><span class="sxs-lookup"><span data-stu-id="f8326-125">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
