---
title: Polecenie dublowanie interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Informacje dotyczące polecenia dublowanie nuget.exe
keywords: nuget duplikatu odniesienia, polecenie dublowanie
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 512bd72d568cda81eb7c6a1555c36ead66b5c438
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="ec6e5-104">polecenie dublowanie (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ec6e5-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="ec6e5-105">**Dotyczy:** publikowania pakietu &bullet; **obsługiwane wersje:** uznane za przestarzałe w wersji 3.2 +</span><span class="sxs-lookup"><span data-stu-id="ec6e5-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="ec6e5-106">Odzwierciedla pakiet i jego zależności z repozytoriami określonego źródła w repozytorium docelowej.</span><span class="sxs-lookup"><span data-stu-id="ec6e5-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="ec6e5-107">Aby włączyć to polecenie dla wersji NuGet przed 3.2, przejdź do [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases)wybierz najnowsza stabilna wersja, Pobierz `NuGet.ServerExtensions.dll` i `Nuget-Signed.exe` na dysku lokalnym i Zmień nazwę `Nuget-Signed.exe` do `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="ec6e5-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="ec6e5-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="ec6e5-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="ec6e5-109">gdzie `<packageID>` jest pakietem dotyczącą tworzenia duplikatów, lub `<configFilePath>` identyfikuje `packages.config` pliku, który zawiera listę pakietów dublowanego.</span><span class="sxs-lookup"><span data-stu-id="ec6e5-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="ec6e5-110">`<listUrlTarget>` Określa repozytorium źródłowe i `<publishUrlTarget>` określa repozytorium docelowe.</span><span class="sxs-lookup"><span data-stu-id="ec6e5-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="ec6e5-111">Jeśli repozytorium docelowy znajduje się na `https://machine/repo` systemem [NuGet.Server](../hosting-packages/nuget-server.md), listy i wypychania adresów URL będzie `https://machine/repo/nuget` i `https://machine/repo/api/v2/package`odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="ec6e5-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="ec6e5-112">Opcje</span><span class="sxs-lookup"><span data-stu-id="ec6e5-112">Options</span></span>

| <span data-ttu-id="ec6e5-113">Opcja</span><span class="sxs-lookup"><span data-stu-id="ec6e5-113">Option</span></span> | <span data-ttu-id="ec6e5-114">Opis</span><span class="sxs-lookup"><span data-stu-id="ec6e5-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ec6e5-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="ec6e5-115">ApiKey</span></span> | <span data-ttu-id="ec6e5-116">Klucz interfejsu API dla repozytorium docelowej.</span><span class="sxs-lookup"><span data-stu-id="ec6e5-116">The API key for the target repository.</span></span> <span data-ttu-id="ec6e5-117">Jeśli nie występuje, określony w pliku konfiguracyjnym jest używana (`%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="ec6e5-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="ec6e5-118">Pomoc</span><span class="sxs-lookup"><span data-stu-id="ec6e5-118">Help</span></span> | <span data-ttu-id="ec6e5-119">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="ec6e5-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="ec6e5-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="ec6e5-120">NoCache</span></span> | <span data-ttu-id="ec6e5-121">Zapobiega przy użyciu pamięci podręcznej pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="ec6e5-121">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="ec6e5-122">Zobacz [Zarządzanie globalne pakietów i foldery pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="ec6e5-122">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="ec6e5-123">Operacja</span><span class="sxs-lookup"><span data-stu-id="ec6e5-123">Noop</span></span> | <span data-ttu-id="ec6e5-124">Rejestruje co będą wykonywane, ale nie wykonuje akcji; Założono powodzenie operacji wypychania.</span><span class="sxs-lookup"><span data-stu-id="ec6e5-124">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="ec6e5-125">Wydanie wstępne</span><span class="sxs-lookup"><span data-stu-id="ec6e5-125">PreRelease</span></span> | <span data-ttu-id="ec6e5-126">Zawiera pakiety wersji wstępnej w operacji dublowania.</span><span class="sxs-lookup"><span data-stu-id="ec6e5-126">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="ec6e5-127">Źródło</span><span class="sxs-lookup"><span data-stu-id="ec6e5-127">Source</span></span> | <span data-ttu-id="ec6e5-128">Lista źródła pakietów w celu utworzenia duplikatów.</span><span class="sxs-lookup"><span data-stu-id="ec6e5-128">A list of package sources to mirror.</span></span> <span data-ttu-id="ec6e5-129">Jeśli nie określono żadnych źródeł, te zdefiniowane w pliku konfiguracyjnym (zobacz powyżej ApiKey) są używane, przyjęty nuget.org, jeśli żaden nie jest określony.</span><span class="sxs-lookup"><span data-stu-id="ec6e5-129">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="ec6e5-130">Limit czasu</span><span class="sxs-lookup"><span data-stu-id="ec6e5-130">Timeout</span></span> | <span data-ttu-id="ec6e5-131">Określa limit czasu w sekundach, do wypychania do serwera.</span><span class="sxs-lookup"><span data-stu-id="ec6e5-131">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="ec6e5-132">Wartość domyślna to 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="ec6e5-132">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="ec6e5-133">Wersja</span><span class="sxs-lookup"><span data-stu-id="ec6e5-133">Version</span></span> | <span data-ttu-id="ec6e5-134">Wersja pakietu do zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="ec6e5-134">The version of the package to install.</span></span> <span data-ttu-id="ec6e5-135">Jeśli nie zostanie określony, jest dublowany najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="ec6e5-135">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="ec6e5-136">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ec6e5-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ec6e5-137">Przykłady</span><span class="sxs-lookup"><span data-stu-id="ec6e5-137">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
