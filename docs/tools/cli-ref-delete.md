---
title: Polecenie Usuń interfejs wiersza polecenia NuGet
description: Dokumentacja dotycząca polecenie Usuń nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 11eea6e806d7bfe364587db9c7ef8374da1819f9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548513"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="32500-103">Usuń polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="32500-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="32500-104">**Dotyczy:** pakietu publikowania &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="32500-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="32500-105">Usuwa lub unlists pakietu ze źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="32500-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="32500-106">Dla nuget.org, polecenie Usuń [unlists pakietu](../policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="32500-106">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="32500-107">Użycie</span><span class="sxs-lookup"><span data-stu-id="32500-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="32500-108">gdzie `<packageID>` i `<packageVersion>` zidentyfikować dokładny pakiet do usunięcia lub wyrejestrowanie.</span><span class="sxs-lookup"><span data-stu-id="32500-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="32500-109">Dokładne zachowanie zależy od źródła.</span><span class="sxs-lookup"><span data-stu-id="32500-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="32500-110">Foldery lokalne na przykład pakiet jest usunięty; w przypadku nuget.org pakietu jest nieobecne na liście.</span><span class="sxs-lookup"><span data-stu-id="32500-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="32500-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="32500-111">Options</span></span>

| <span data-ttu-id="32500-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="32500-112">Option</span></span> | <span data-ttu-id="32500-113">Opis</span><span class="sxs-lookup"><span data-stu-id="32500-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="32500-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="32500-114">ApiKey</span></span> | <span data-ttu-id="32500-115">Klucz interfejsu API w repozytorium docelowym.</span><span class="sxs-lookup"><span data-stu-id="32500-115">The API key for the target repository.</span></span> <span data-ttu-id="32500-116">Jeśli nie występuje, określony w pliku konfiguracji jest używany.</span><span class="sxs-lookup"><span data-stu-id="32500-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="32500-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="32500-117">ConfigFile</span></span> | <span data-ttu-id="32500-118">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="32500-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="32500-119">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="32500-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="32500-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="32500-120">ForceEnglishOutput</span></span> | <span data-ttu-id="32500-121">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="32500-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="32500-122">Help</span><span class="sxs-lookup"><span data-stu-id="32500-122">Help</span></span> | <span data-ttu-id="32500-123">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="32500-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="32500-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="32500-124">NonInteractive</span></span> | <span data-ttu-id="32500-125">Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="32500-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="32500-126">Source</span><span class="sxs-lookup"><span data-stu-id="32500-126">Source</span></span> | <span data-ttu-id="32500-127">Określa adres URL serwera.</span><span class="sxs-lookup"><span data-stu-id="32500-127">Specifies the server URL.</span></span> <span data-ttu-id="32500-128">Adres URL repozytorium nuget.org jest `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="32500-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="32500-129">Dla prywatnych źródeł danych, zastąp nazwę hosta, na przykład *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="32500-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="32500-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="32500-130">Verbosity</span></span> | <span data-ttu-id="32500-131">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="32500-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="32500-132">Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="32500-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="32500-133">Przykłady</span><span class="sxs-lookup"><span data-stu-id="32500-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
