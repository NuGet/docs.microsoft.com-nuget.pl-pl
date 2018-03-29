---
title: Polecenie setapikey interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Informacje dotyczące polecenia setapikey nuget.exe
keywords: polecenie setapikey nuget setapikey odwołania
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 696ccf9df5af487d3bf75925c1c1e0d1d1bf7f7b
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="ca1b6-104">polecenie setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ca1b6-104">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="ca1b6-105">**Dotyczy:** zużycie pakietu, publikowanie &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="ca1b6-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ca1b6-106">Zapisuje klucz interfejsu API dla danego adresu URL podanego serwera do `NuGet.Config` tak, aby nie trzeba wprowadzać dla kolejnych poleceń.</span><span class="sxs-lookup"><span data-stu-id="ca1b6-106">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="ca1b6-107">Użycie</span><span class="sxs-lookup"><span data-stu-id="ca1b6-107">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="ca1b6-108">gdzie `<source>` identyfikuje serwer i `<key>` to klucz lub hasło, aby zapisać.</span><span class="sxs-lookup"><span data-stu-id="ca1b6-108">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="ca1b6-109">Jeśli `<source>` jest pominięty, zakłada nuget.org.</span><span class="sxs-lookup"><span data-stu-id="ca1b6-109">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="ca1b6-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="ca1b6-110">Options</span></span>

| <span data-ttu-id="ca1b6-111">Opcja</span><span class="sxs-lookup"><span data-stu-id="ca1b6-111">Option</span></span> | <span data-ttu-id="ca1b6-112">Opis</span><span class="sxs-lookup"><span data-stu-id="ca1b6-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ca1b6-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ca1b6-113">ConfigFile</span></span> | <span data-ttu-id="ca1b6-114">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="ca1b6-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ca1b6-115">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="ca1b6-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="ca1b6-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ca1b6-116">ForceEnglishOutput</span></span> | <span data-ttu-id="ca1b6-117">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="ca1b6-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ca1b6-118">Pomoc</span><span class="sxs-lookup"><span data-stu-id="ca1b6-118">Help</span></span> | <span data-ttu-id="ca1b6-119">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="ca1b6-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="ca1b6-120">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="ca1b6-120">NonInteractive</span></span> | <span data-ttu-id="ca1b6-121">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="ca1b6-121">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ca1b6-122">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="ca1b6-122">Verbosity</span></span> | <span data-ttu-id="ca1b6-123">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="ca1b6-123">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="ca1b6-124">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ca1b6-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ca1b6-125">Przykłady</span><span class="sxs-lookup"><span data-stu-id="ca1b6-125">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
