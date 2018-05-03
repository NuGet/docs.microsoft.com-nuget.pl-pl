---
title: Polecenie Usuń NuGet interfejsu wiersza polecenia
description: Dokumentacja dla polecenia delete nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 1db00a32d777f1c0247f855bf57a0dcf1c6734ae
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="87c54-103">Usuwanie polecenia (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="87c54-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="87c54-104">**Dotyczy:** publikowania pakietu &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="87c54-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="87c54-105">Usuwa lub unlists pakietu ze źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="87c54-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="87c54-106">Dla nuget.org, polecenia delete [unlists pakietu](../policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="87c54-106">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="87c54-107">Użycie</span><span class="sxs-lookup"><span data-stu-id="87c54-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="87c54-108">gdzie `<packageID>` i `<packageVersion>` identyfikować dokładną pakiet do usunięcia lub unlist.</span><span class="sxs-lookup"><span data-stu-id="87c54-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="87c54-109">Dokładne zachowanie zależy od źródła.</span><span class="sxs-lookup"><span data-stu-id="87c54-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="87c54-110">Foldery lokalne na przykład pakiet został usunięty; w przypadku nuget.org pakietu jest nieznajdujące się na liście.</span><span class="sxs-lookup"><span data-stu-id="87c54-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="87c54-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="87c54-111">Options</span></span>

| <span data-ttu-id="87c54-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="87c54-112">Option</span></span> | <span data-ttu-id="87c54-113">Opis</span><span class="sxs-lookup"><span data-stu-id="87c54-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="87c54-114">apiKey</span><span class="sxs-lookup"><span data-stu-id="87c54-114">ApiKey</span></span> | <span data-ttu-id="87c54-115">Klucz interfejsu API dla repozytorium docelowej.</span><span class="sxs-lookup"><span data-stu-id="87c54-115">The API key for the target repository.</span></span> <span data-ttu-id="87c54-116">Jeśli nie istnieje określony w pliku konfiguracji jest używany.</span><span class="sxs-lookup"><span data-stu-id="87c54-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="87c54-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="87c54-117">ConfigFile</span></span> | <span data-ttu-id="87c54-118">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="87c54-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="87c54-119">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="87c54-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="87c54-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="87c54-120">ForceEnglishOutput</span></span> | <span data-ttu-id="87c54-121">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="87c54-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="87c54-122">Pomoc</span><span class="sxs-lookup"><span data-stu-id="87c54-122">Help</span></span> | <span data-ttu-id="87c54-123">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="87c54-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="87c54-124">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="87c54-124">NonInteractive</span></span> | <span data-ttu-id="87c54-125">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="87c54-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="87c54-126">Źródło</span><span class="sxs-lookup"><span data-stu-id="87c54-126">Source</span></span> | <span data-ttu-id="87c54-127">Określa adres URL serwera.</span><span class="sxs-lookup"><span data-stu-id="87c54-127">Specifies the server URL.</span></span> <span data-ttu-id="87c54-128">Adres URL nuget.org jest `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="87c54-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="87c54-129">Dla prywatnych źródeł danych, zastąp nazwę hosta, na przykład *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="87c54-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="87c54-130">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="87c54-130">Verbosity</span></span> | <span data-ttu-id="87c54-131">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="87c54-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="87c54-132">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="87c54-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="87c54-133">Przykłady</span><span class="sxs-lookup"><span data-stu-id="87c54-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
