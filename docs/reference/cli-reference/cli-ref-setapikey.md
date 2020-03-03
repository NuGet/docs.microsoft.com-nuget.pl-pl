---
title: Polecenie setapikey interfejsu wiersza polecenia NuGet
description: Dokumentacja polecenia NuGet. exe setapikey
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e06cfb5b355dfae8104090db7babdecdf9e9fec1
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231230"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="c659e-103">setapikey — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="c659e-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="c659e-104">**Dotyczy:** użycie pakietu, publikowanie &bullet; **obsługiwanych wersji:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="c659e-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="c659e-105">Zapisuje klucz interfejsu API dla danego adresu URL serwera w `NuGet.Config`, aby nie trzeba było go wprowadzać do kolejnych poleceń.</span><span class="sxs-lookup"><span data-stu-id="c659e-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="c659e-106">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="c659e-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="c659e-107">gdzie `<source>` identyfikuje serwer, a `<key>` jest kluczem do zapisania.</span><span class="sxs-lookup"><span data-stu-id="c659e-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="c659e-108">W przypadku pominięcia `<source>` zostanie przyjęty nuget.org.</span><span class="sxs-lookup"><span data-stu-id="c659e-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="c659e-109">Klucz interfejsu API nie jest używany do uwierzytelniania w prywatnym źródle danych.</span><span class="sxs-lookup"><span data-stu-id="c659e-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="c659e-110">Zapoznaj się z [`nuget sources` polecenie](../cli-reference/cli-ref-sources.md) , aby zarządzać poświadczeniami do uwierzytelniania ze źródłem.</span><span class="sxs-lookup"><span data-stu-id="c659e-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="c659e-111">Klucze interfejsu API można uzyskać z poszczególnych serwerów NuGet.</span><span class="sxs-lookup"><span data-stu-id="c659e-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="c659e-112">Aby utworzyć i zarządzać APIKeys for nuget.org, zobacz temat [Publikowanie-API-Key](../../quickstart/includes/publish-api-key.md)</span><span class="sxs-lookup"><span data-stu-id="c659e-112">To create and manage APIKeys for nuget.org refer to [publish-api-key](../../quickstart/includes/publish-api-key.md)</span></span>

## <a name="options"></a><span data-ttu-id="c659e-113">Opcje</span><span class="sxs-lookup"><span data-stu-id="c659e-113">Options</span></span>

| <span data-ttu-id="c659e-114">Opcja</span><span class="sxs-lookup"><span data-stu-id="c659e-114">Option</span></span> | <span data-ttu-id="c659e-115">Opis</span><span class="sxs-lookup"><span data-stu-id="c659e-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c659e-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c659e-116">ConfigFile</span></span> | <span data-ttu-id="c659e-117">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="c659e-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c659e-118">Jeśli nie zostanie określony, używany jest `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="c659e-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="c659e-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c659e-119">ForceEnglishOutput</span></span> | <span data-ttu-id="c659e-120">*(3.5 +)* Wymusza uruchomienie NuGet. exe przy użyciu niezmiennej, opartej na języku angielskim kultury.</span><span class="sxs-lookup"><span data-stu-id="c659e-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c659e-121">Pomoc</span><span class="sxs-lookup"><span data-stu-id="c659e-121">Help</span></span> | <span data-ttu-id="c659e-122">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="c659e-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="c659e-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="c659e-123">NonInteractive</span></span> | <span data-ttu-id="c659e-124">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c659e-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c659e-125">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="c659e-125">Verbosity</span></span> | <span data-ttu-id="c659e-126">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="c659e-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="c659e-127">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c659e-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c659e-128">Przykłady</span><span class="sxs-lookup"><span data-stu-id="c659e-128">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
