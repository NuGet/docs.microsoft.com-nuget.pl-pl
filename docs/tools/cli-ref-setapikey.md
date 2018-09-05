---
title: Polecenie setapikey interfejs wiersza polecenia NuGet
description: Dokumentacja dotycząca poleceń setapikey nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549223"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="26ccb-103">polecenie setapikey (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="26ccb-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="26ccb-104">**Dotyczy:** zużycie pakietów, publikowania &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="26ccb-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="26ccb-105">Zapisuje klucz interfejsu API dla danego serwera adresu URL do `NuGet.Config` tak, aby nie trzeba wprowadzić używane przy kolejnych poleceniach.</span><span class="sxs-lookup"><span data-stu-id="26ccb-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="26ccb-106">Użycie</span><span class="sxs-lookup"><span data-stu-id="26ccb-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="26ccb-107">gdzie `<source>` identyfikuje serwer i `<key>` jest klucz lub hasło, aby zapisać.</span><span class="sxs-lookup"><span data-stu-id="26ccb-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="26ccb-108">Jeśli `<source>` jest pominięty, zakłada nuget.org.</span><span class="sxs-lookup"><span data-stu-id="26ccb-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="26ccb-109">Opcje</span><span class="sxs-lookup"><span data-stu-id="26ccb-109">Options</span></span>

| <span data-ttu-id="26ccb-110">Opcja</span><span class="sxs-lookup"><span data-stu-id="26ccb-110">Option</span></span> | <span data-ttu-id="26ccb-111">Opis</span><span class="sxs-lookup"><span data-stu-id="26ccb-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="26ccb-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="26ccb-112">ConfigFile</span></span> | <span data-ttu-id="26ccb-113">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="26ccb-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="26ccb-114">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="26ccb-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="26ccb-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="26ccb-115">ForceEnglishOutput</span></span> | <span data-ttu-id="26ccb-116">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="26ccb-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="26ccb-117">Pomoc</span><span class="sxs-lookup"><span data-stu-id="26ccb-117">Help</span></span> | <span data-ttu-id="26ccb-118">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="26ccb-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="26ccb-119">Nieinterakcyjnym</span><span class="sxs-lookup"><span data-stu-id="26ccb-119">NonInteractive</span></span> | <span data-ttu-id="26ccb-120">Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="26ccb-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="26ccb-121">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="26ccb-121">Verbosity</span></span> | <span data-ttu-id="26ccb-122">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="26ccb-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="26ccb-123">Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="26ccb-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="26ccb-124">Przykłady</span><span class="sxs-lookup"><span data-stu-id="26ccb-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
