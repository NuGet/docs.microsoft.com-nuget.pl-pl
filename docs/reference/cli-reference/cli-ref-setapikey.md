---
title: Polecenie setapikey interfejsu wiersza polecenia NuGet
description: Odwołanie do nuget.exe setapikey polecenia
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3e0c2f84e336e0a642b1b5e815e74a1fb0878467
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780018"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="c5bdd-103">setapikey — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="c5bdd-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="c5bdd-104">**Dotyczy:** użycie pakietu, publikowanie &bullet; **obsługiwanych wersji:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="c5bdd-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="c5bdd-105">Zapisuje klucz interfejsu API dla danego adresu URL serwera w `NuGet.Config` taki sposób, aby nie trzeba było go wprowadzać do kolejnych poleceń.</span><span class="sxs-lookup"><span data-stu-id="c5bdd-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="c5bdd-106">Użycie</span><span class="sxs-lookup"><span data-stu-id="c5bdd-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="c5bdd-107">gdzie `<source>` identyfikuje serwer i `<key>` jest kluczem do zapisania.</span><span class="sxs-lookup"><span data-stu-id="c5bdd-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="c5bdd-108">`<source>`W przypadku pominięcia zostanie założono NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="c5bdd-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="c5bdd-109">Klucz interfejsu API nie jest używany do uwierzytelniania w prywatnym źródle danych.</span><span class="sxs-lookup"><span data-stu-id="c5bdd-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="c5bdd-110">Zapoznaj się z [ `nuget sources` poleceniem](../cli-reference/cli-ref-sources.md) , aby zarządzać poświadczeniami do uwierzytelniania ze źródłem.</span><span class="sxs-lookup"><span data-stu-id="c5bdd-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="c5bdd-111">Klucze interfejsu API można uzyskać z poszczególnych serwerów NuGet.</span><span class="sxs-lookup"><span data-stu-id="c5bdd-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="c5bdd-112">Aby utworzyć i zarządzać APIKeys for nuget.org, zobacz temat [pozyskiwanie-a-API-Key](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)</span><span class="sxs-lookup"><span data-stu-id="c5bdd-112">To create and manage APIKeys for nuget.org refer to [acquire-an-api-key](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)</span></span>

## <a name="options"></a><span data-ttu-id="c5bdd-113">Opcje</span><span class="sxs-lookup"><span data-stu-id="c5bdd-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="c5bdd-114">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="c5bdd-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c5bdd-115">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="c5bdd-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="c5bdd-116">*(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.</span><span class="sxs-lookup"><span data-stu-id="c5bdd-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="c5bdd-117">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="c5bdd-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="c5bdd-118">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c5bdd-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="c5bdd-119">Adres URL serwera, na którym klucz interfejsu API jest prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="c5bdd-119">Server URL where the API key is valid.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="c5bdd-120">Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .</span><span class="sxs-lookup"><span data-stu-id="c5bdd-120">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="c5bdd-121">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c5bdd-121">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c5bdd-122">Przykłady</span><span class="sxs-lookup"><span data-stu-id="c5bdd-122">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
