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
ms.openlocfilehash: 3890e33ab0fc425e1c2ee39631ade57ea9b92bc9
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="fca98-104">Usuwanie polecenia (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="fca98-104">delete command (NuGet CLI)</span></span>

<span data-ttu-id="fca98-105">**Dotyczy:** publikowania pakietu &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="fca98-105">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="fca98-106">Usuwa lub unlists pakietu ze źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="fca98-106">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="fca98-107">Dla nuget.org, polecenia delete [unlists pakietu](../policies/Deleting-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="fca98-107">For nuget.org, the delete command [unlists the package](../policies/Deleting-Packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="fca98-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="fca98-108">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="fca98-109">gdzie `<packageID>` i `<packageVersion>` identyfikować dokładną pakiet do usunięcia lub unlist.</span><span class="sxs-lookup"><span data-stu-id="fca98-109">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="fca98-110">Dokładne zachowanie zależy od źródła.</span><span class="sxs-lookup"><span data-stu-id="fca98-110">The exact behavior depends on the source.</span></span> <span data-ttu-id="fca98-111">Foldery lokalne na przykład pakiet został usunięty; w przypadku nuget.org pakietu jest nieznajdujące się na liście.</span><span class="sxs-lookup"><span data-stu-id="fca98-111">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="fca98-112">Opcje</span><span class="sxs-lookup"><span data-stu-id="fca98-112">Options</span></span>

| <span data-ttu-id="fca98-113">Opcja</span><span class="sxs-lookup"><span data-stu-id="fca98-113">Option</span></span> | <span data-ttu-id="fca98-114">Opis</span><span class="sxs-lookup"><span data-stu-id="fca98-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fca98-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="fca98-115">ApiKey</span></span> | <span data-ttu-id="fca98-116">Klucz interfejsu API dla repozytorium docelowej.</span><span class="sxs-lookup"><span data-stu-id="fca98-116">The API key for the target repository.</span></span> <span data-ttu-id="fca98-117">Jeśli nie występuje, określony w *%AppData%\NuGet\NuGet.Config* jest używany.</span><span class="sxs-lookup"><span data-stu-id="fca98-117">If not present, the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="fca98-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="fca98-118">ConfigFile</span></span> | <span data-ttu-id="fca98-119">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="fca98-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="fca98-120">Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany.</span><span class="sxs-lookup"><span data-stu-id="fca98-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="fca98-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="fca98-121">ForceEnglishOutput</span></span> | <span data-ttu-id="fca98-122">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="fca98-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="fca98-123">Pomoc</span><span class="sxs-lookup"><span data-stu-id="fca98-123">Help</span></span> | <span data-ttu-id="fca98-124">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="fca98-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="fca98-125">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="fca98-125">NonInteractive</span></span> | <span data-ttu-id="fca98-126">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="fca98-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="fca98-127">Źródło</span><span class="sxs-lookup"><span data-stu-id="fca98-127">Source</span></span> | <span data-ttu-id="fca98-128">Określa adres URL serwera.</span><span class="sxs-lookup"><span data-stu-id="fca98-128">Specifies the server URL.</span></span> <span data-ttu-id="fca98-129">Adres URL nuget.org jest `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="fca98-129">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="fca98-130">Dla prywatnych źródeł danych, zastąp nazwę hosta, na przykład *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="fca98-130">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="fca98-131">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="fca98-131">Verbosity</span></span> | <span data-ttu-id="fca98-132">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="fca98-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="fca98-133">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="fca98-133">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="fca98-134">Przykłady</span><span class="sxs-lookup"><span data-stu-id="fca98-134">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
