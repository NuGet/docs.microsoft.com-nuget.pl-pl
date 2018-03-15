---
title: Polecenie delete interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Dokumentacja dla polecenia delete nuget.exe
keywords: "nuget usunąć odwołanie, usuń pakiet polecenia"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b5d53b83cdccaa8e284b844786b0ec27e7afb63a
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/15/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="9b483-104">Usuwanie polecenia (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="9b483-104">delete command (NuGet CLI)</span></span>

<span data-ttu-id="9b483-105">**Dotyczy:** publikowania pakietu &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="9b483-105">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="9b483-106">Usuwa lub unlists pakietu ze źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="9b483-106">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="9b483-107">Dla nuget.org, polecenia delete [unlists pakietu](../policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="9b483-107">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="9b483-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="9b483-108">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="9b483-109">gdzie `<packageID>` i `<packageVersion>` identyfikować dokładną pakiet do usunięcia lub unlist.</span><span class="sxs-lookup"><span data-stu-id="9b483-109">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="9b483-110">Dokładne zachowanie zależy od źródła.</span><span class="sxs-lookup"><span data-stu-id="9b483-110">The exact behavior depends on the source.</span></span> <span data-ttu-id="9b483-111">Foldery lokalne na przykład pakiet został usunięty; w przypadku nuget.org pakietu jest nieznajdujące się na liście.</span><span class="sxs-lookup"><span data-stu-id="9b483-111">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="9b483-112">Opcje</span><span class="sxs-lookup"><span data-stu-id="9b483-112">Options</span></span>

| <span data-ttu-id="9b483-113">Opcja</span><span class="sxs-lookup"><span data-stu-id="9b483-113">Option</span></span> | <span data-ttu-id="9b483-114">Opis</span><span class="sxs-lookup"><span data-stu-id="9b483-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9b483-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="9b483-115">ApiKey</span></span> | <span data-ttu-id="9b483-116">Klucz interfejsu API dla repozytorium docelowej.</span><span class="sxs-lookup"><span data-stu-id="9b483-116">The API key for the target repository.</span></span> <span data-ttu-id="9b483-117">Jeśli nie istnieje określony w pliku konfiguracji jest używany.</span><span class="sxs-lookup"><span data-stu-id="9b483-117">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="9b483-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="9b483-118">ConfigFile</span></span> | <span data-ttu-id="9b483-119">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="9b483-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="9b483-120">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="9b483-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="9b483-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="9b483-121">ForceEnglishOutput</span></span> | <span data-ttu-id="9b483-122">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="9b483-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="9b483-123">Pomoc</span><span class="sxs-lookup"><span data-stu-id="9b483-123">Help</span></span> | <span data-ttu-id="9b483-124">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="9b483-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="9b483-125">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="9b483-125">NonInteractive</span></span> | <span data-ttu-id="9b483-126">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="9b483-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="9b483-127">Źródło</span><span class="sxs-lookup"><span data-stu-id="9b483-127">Source</span></span> | <span data-ttu-id="9b483-128">Określa adres URL serwera.</span><span class="sxs-lookup"><span data-stu-id="9b483-128">Specifies the server URL.</span></span> <span data-ttu-id="9b483-129">Adres URL nuget.org jest `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="9b483-129">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="9b483-130">Dla prywatnych źródeł danych, zastąp nazwę hosta, na przykład *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="9b483-130">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="9b483-131">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="9b483-131">Verbosity</span></span> | <span data-ttu-id="9b483-132">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="9b483-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="9b483-133">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="9b483-133">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="9b483-134">Przykłady</span><span class="sxs-lookup"><span data-stu-id="9b483-134">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
