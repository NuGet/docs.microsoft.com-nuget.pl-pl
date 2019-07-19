---
title: Polecenie usunięcia interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia Delete programu NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5185bc8b89f645a0a0f4d3241b5fa04e09560ede
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328355"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="d63ed-103">DELETE — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="d63ed-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="d63ed-104">**Dotyczy:** **obsługiwane wersje** publikowania &bullet; pakietów: wszystkie</span><span class="sxs-lookup"><span data-stu-id="d63ed-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d63ed-105">Usuwa pakiet ze źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="d63ed-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="d63ed-106">W przypadku nuget.org polecenie Delete wystawia [pakiet](../../nuget-org/policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="d63ed-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="d63ed-107">Użycie</span><span class="sxs-lookup"><span data-stu-id="d63ed-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="d63ed-108">gdzie `<packageID>` i`<packageVersion>` Zidentyfikuj dokładny pakiet do usunięcia lub Wycofaj listy.</span><span class="sxs-lookup"><span data-stu-id="d63ed-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="d63ed-109">Dokładne zachowanie zależy od źródła.</span><span class="sxs-lookup"><span data-stu-id="d63ed-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="d63ed-110">Na przykład dla folderów lokalnych pakiet jest usuwany; dla nuget.org pakiet nie znajduje się na liście.</span><span class="sxs-lookup"><span data-stu-id="d63ed-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="d63ed-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="d63ed-111">Options</span></span>

| <span data-ttu-id="d63ed-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="d63ed-112">Option</span></span> | <span data-ttu-id="d63ed-113">Opis</span><span class="sxs-lookup"><span data-stu-id="d63ed-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d63ed-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="d63ed-114">ApiKey</span></span> | <span data-ttu-id="d63ed-115">Klucz interfejsu API repozytorium docelowego.</span><span class="sxs-lookup"><span data-stu-id="d63ed-115">The API key for the target repository.</span></span> <span data-ttu-id="d63ed-116">Jeśli nie istnieje, jest używany określony w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d63ed-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="d63ed-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d63ed-117">ConfigFile</span></span> | <span data-ttu-id="d63ed-118">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="d63ed-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d63ed-119">Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="d63ed-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d63ed-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d63ed-120">ForceEnglishOutput</span></span> | <span data-ttu-id="d63ed-121">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="d63ed-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d63ed-122">Help</span><span class="sxs-lookup"><span data-stu-id="d63ed-122">Help</span></span> | <span data-ttu-id="d63ed-123">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="d63ed-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="d63ed-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="d63ed-124">NonInteractive</span></span> | <span data-ttu-id="d63ed-125">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d63ed-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d63ed-126">Source</span><span class="sxs-lookup"><span data-stu-id="d63ed-126">Source</span></span> | <span data-ttu-id="d63ed-127">Określa adres URL serwera.</span><span class="sxs-lookup"><span data-stu-id="d63ed-127">Specifies the server URL.</span></span> <span data-ttu-id="d63ed-128">Adres URL nuget.org ma `https://api.nuget.org/v3/index.json`wartość.</span><span class="sxs-lookup"><span data-stu-id="d63ed-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="d63ed-129">W przypadku prywatnych kanałów informacyjnych należy zastąpić nazwę hosta, na przykład *% hostname%/API/v3*.</span><span class="sxs-lookup"><span data-stu-id="d63ed-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="d63ed-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="d63ed-130">Verbosity</span></span> | <span data-ttu-id="d63ed-131">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="d63ed-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d63ed-132">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d63ed-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d63ed-133">Przykłady</span><span class="sxs-lookup"><span data-stu-id="d63ed-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
