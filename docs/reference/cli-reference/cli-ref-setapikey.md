---
title: Polecenie setapikey interfejsu wiersza polecenia NuGet
description: Dokumentacja polecenia NuGet. exe setapikey
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e2119953e6d07cd3571f156fa0b2665de49f963
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383972"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="9b928-103">setapikey — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="9b928-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="9b928-104">**Dotyczy:** użycie pakietu, publikowanie &bullet; **obsługiwanych wersji:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="9b928-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="9b928-105">Zapisuje klucz interfejsu API dla danego adresu URL serwera w `NuGet.Config`, aby nie trzeba było go wprowadzać do kolejnych poleceń.</span><span class="sxs-lookup"><span data-stu-id="9b928-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="9b928-106">Pomiar</span><span class="sxs-lookup"><span data-stu-id="9b928-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="9b928-107">gdzie `<source>` identyfikuje serwer, a `<key>` jest kluczem lub hasłem do zapisania.</span><span class="sxs-lookup"><span data-stu-id="9b928-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="9b928-108">W przypadku pominięcia `<source>` zostanie przyjęty nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9b928-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

> [!NOTE]
> <span data-ttu-id="9b928-109">Klucz interfejsu API nie jest używany do uwierzytelniania w prywatnym źródle danych.</span><span class="sxs-lookup"><span data-stu-id="9b928-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="9b928-110">Zapoznaj się z [`nuget sources` polecenie](../cli-reference/cli-ref-sources.md) , aby zarządzać poświadczeniami do uwierzytelniania ze źródłem.</span><span class="sxs-lookup"><span data-stu-id="9b928-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>

## <a name="options"></a><span data-ttu-id="9b928-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="9b928-111">Options</span></span>

| <span data-ttu-id="9b928-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="9b928-112">Option</span></span> | <span data-ttu-id="9b928-113">Opis</span><span class="sxs-lookup"><span data-stu-id="9b928-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9b928-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="9b928-114">ConfigFile</span></span> | <span data-ttu-id="9b928-115">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="9b928-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="9b928-116">Jeśli nie zostanie określony, używany jest `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="9b928-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="9b928-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="9b928-117">ForceEnglishOutput</span></span> | <span data-ttu-id="9b928-118">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="9b928-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="9b928-119">Pomoc</span><span class="sxs-lookup"><span data-stu-id="9b928-119">Help</span></span> | <span data-ttu-id="9b928-120">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="9b928-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="9b928-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="9b928-121">NonInteractive</span></span> | <span data-ttu-id="9b928-122">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9b928-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="9b928-123">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="9b928-123">Verbosity</span></span> | <span data-ttu-id="9b928-124">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="9b928-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="9b928-125">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="9b928-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="9b928-126">Przykłady</span><span class="sxs-lookup"><span data-stu-id="9b928-126">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
