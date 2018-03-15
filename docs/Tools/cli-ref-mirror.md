---
title: Polecenie dublowanie interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Informacje dotyczące polecenia dublowanie nuget.exe"
keywords: nuget duplikatu odniesienia, polecenie dublowanie
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0c1969cc04b2e2cead5e9dadf9739fdabdf65f6c
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/15/2018
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="fefc6-104">polecenie dublowanie (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="fefc6-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="fefc6-105">**Dotyczy:** publikowania pakietu &bullet; **obsługiwane wersje:** uznane za przestarzałe w wersji 3.2 +</span><span class="sxs-lookup"><span data-stu-id="fefc6-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="fefc6-106">Odzwierciedla pakiet i jego zależności z repozytoriami określonego źródła w repozytorium docelowej.</span><span class="sxs-lookup"><span data-stu-id="fefc6-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="fefc6-107">Aby włączyć to polecenie dla wersji NuGet przed 3.2, przejdź do [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases)wybierz najnowsza stabilna wersja, Pobierz `NuGet.ServerExtensions.dll` i `Nuget-Signed.exe` na dysku lokalnym i Zmień nazwę `Nuget-Signed.exe` do `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="fefc6-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="fefc6-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="fefc6-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="fefc6-109">gdzie `<packageID>` jest pakietem dotyczącą tworzenia duplikatów, lub `<configFilePath>` identyfikuje `packages.config` pliku, który zawiera listę pakietów dublowanego.</span><span class="sxs-lookup"><span data-stu-id="fefc6-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="fefc6-110">`<listUrlTarget>` Określa repozytorium źródłowe i `<publishUrlTarget>` określa repozytorium docelowe.</span><span class="sxs-lookup"><span data-stu-id="fefc6-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="fefc6-111">Jeśli repozytorium docelowy znajduje się na `https://machine/repo` systemem [NuGet.Server](../hosting-packages/nuget-server.md), listy i wypychania adresów URL będzie `https://machine/repo/nuget` i `https://machine/repo/api/v2/package`odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="fefc6-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="fefc6-112">Opcje</span><span class="sxs-lookup"><span data-stu-id="fefc6-112">Options</span></span>

| <span data-ttu-id="fefc6-113">Opcja</span><span class="sxs-lookup"><span data-stu-id="fefc6-113">Option</span></span> | <span data-ttu-id="fefc6-114">Opis</span><span class="sxs-lookup"><span data-stu-id="fefc6-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fefc6-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="fefc6-115">ApiKey</span></span> | <span data-ttu-id="fefc6-116">Klucz interfejsu API dla repozytorium docelowej.</span><span class="sxs-lookup"><span data-stu-id="fefc6-116">The API key for the target repository.</span></span> <span data-ttu-id="fefc6-117">Jeśli nie występuje, określony w pliku konfiguracyjnym jest używana (`%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="fefc6-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="fefc6-118">Pomoc</span><span class="sxs-lookup"><span data-stu-id="fefc6-118">Help</span></span> | <span data-ttu-id="fefc6-119">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="fefc6-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="fefc6-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="fefc6-120">NoCache</span></span> | <span data-ttu-id="fefc6-121">Zapobiega z pamięci podręcznej komputera lokalnego za pomocą pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="fefc6-121">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="fefc6-122">Operacja</span><span class="sxs-lookup"><span data-stu-id="fefc6-122">Noop</span></span> | <span data-ttu-id="fefc6-123">Rejestruje co będą wykonywane, ale nie wykonuje akcji; Założono powodzenie operacji wypychania.</span><span class="sxs-lookup"><span data-stu-id="fefc6-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="fefc6-124">Wydanie wstępne</span><span class="sxs-lookup"><span data-stu-id="fefc6-124">PreRelease</span></span> | <span data-ttu-id="fefc6-125">Zawiera pakiety wersji wstępnej w operacji dublowania.</span><span class="sxs-lookup"><span data-stu-id="fefc6-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="fefc6-126">Źródło</span><span class="sxs-lookup"><span data-stu-id="fefc6-126">Source</span></span> | <span data-ttu-id="fefc6-127">Lista źródła pakietów w celu utworzenia duplikatów.</span><span class="sxs-lookup"><span data-stu-id="fefc6-127">A list of package sources to mirror.</span></span> <span data-ttu-id="fefc6-128">Jeśli nie określono żadnych źródeł, te zdefiniowane w pliku konfiguracyjnym (zobacz powyżej ApiKey) są używane, przyjęty nuget.org, jeśli żaden nie jest określony.</span><span class="sxs-lookup"><span data-stu-id="fefc6-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="fefc6-129">Limit czasu</span><span class="sxs-lookup"><span data-stu-id="fefc6-129">Timeout</span></span> | <span data-ttu-id="fefc6-130">Określa limit czasu w sekundach, do wypychania do serwera.</span><span class="sxs-lookup"><span data-stu-id="fefc6-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="fefc6-131">Wartość domyślna to 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="fefc6-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="fefc6-132">Wersja</span><span class="sxs-lookup"><span data-stu-id="fefc6-132">Version</span></span> | <span data-ttu-id="fefc6-133">Wersja pakietu do zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="fefc6-133">The version of the package to install.</span></span> <span data-ttu-id="fefc6-134">Jeśli nie zostanie określony, jest dublowany najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="fefc6-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="fefc6-135">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="fefc6-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="fefc6-136">Przykłady</span><span class="sxs-lookup"><span data-stu-id="fefc6-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
