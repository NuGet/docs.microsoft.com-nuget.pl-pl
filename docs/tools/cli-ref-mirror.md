---
title: Polecenie dublowanie interfejs wiersza polecenia NuGet
description: Dokumentacja dotycząca polecenia dublowanie nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d3a322e16c4ba212a856e9bf4d2eaab2872c31b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550209"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="5ea5c-103">mirror command, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="5ea5c-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="5ea5c-104">**Dotyczy:** pakietu publikowania &bullet; **obsługiwane wersje:** uznane za przestarzałe w 3.2 +</span><span class="sxs-lookup"><span data-stu-id="5ea5c-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="5ea5c-105">Odzwierciedla pakietu oraz jego zależności z repozytoriów określone źródło do repozytorium docelowego.</span><span class="sxs-lookup"><span data-stu-id="5ea5c-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="5ea5c-106">Aby włączyć to polecenie dla wersji NuGet przed 3.2, przejdź do [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases)wybierz najnowszej stabilnej wersji, Pobierz `NuGet.ServerExtensions.dll` i `Nuget-Signed.exe` do zmiany nazwy i dysku lokalnego, na których `Nuget-Signed.exe` do `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="5ea5c-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="5ea5c-107">Użycie</span><span class="sxs-lookup"><span data-stu-id="5ea5c-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="5ea5c-108">gdzie `<packageID>` to pakiet duplikatów, lub `<configFilePath>` identyfikuje `packages.config` pliku, który zawiera listę pakietów w celu utworzenia duplikatów.</span><span class="sxs-lookup"><span data-stu-id="5ea5c-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="5ea5c-109">`<listUrlTarget>` Określa repozytorium źródłowe i `<publishUrlTarget>` określa repozytorium docelowego.</span><span class="sxs-lookup"><span data-stu-id="5ea5c-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="5ea5c-110">Jeśli Twoje repozytorium docelowym znajduje się na `https://machine/repo` uruchomionym [NuGet.Server](../hosting-packages/nuget-server.md), listy i wypychania adresy URL będą `https://machine/repo/nuget` i `https://machine/repo/api/v2/package`odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="5ea5c-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="5ea5c-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="5ea5c-111">Options</span></span>

| <span data-ttu-id="5ea5c-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="5ea5c-112">Option</span></span> | <span data-ttu-id="5ea5c-113">Opis</span><span class="sxs-lookup"><span data-stu-id="5ea5c-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5ea5c-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="5ea5c-114">ApiKey</span></span> | <span data-ttu-id="5ea5c-115">Klucz interfejsu API w repozytorium docelowym.</span><span class="sxs-lookup"><span data-stu-id="5ea5c-115">The API key for the target repository.</span></span> <span data-ttu-id="5ea5c-116">Jeśli nie występuje, określony w pliku konfiguracji jest używana (`%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="5ea5c-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="5ea5c-117">Pomoc</span><span class="sxs-lookup"><span data-stu-id="5ea5c-117">Help</span></span> | <span data-ttu-id="5ea5c-118">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="5ea5c-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="5ea5c-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="5ea5c-119">NoCache</span></span> | <span data-ttu-id="5ea5c-120">Uniemożliwia korzystania z pamięci podręcznej pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="5ea5c-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="5ea5c-121">Zobacz [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="5ea5c-121">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="5ea5c-122">Aktualizujący nie działa</span><span class="sxs-lookup"><span data-stu-id="5ea5c-122">Noop</span></span> | <span data-ttu-id="5ea5c-123">Rejestruje, jakie będą wykonywane, ale nie wykonuje akcji; przyjęto założenie, Powodzenie operacji wypychania.</span><span class="sxs-lookup"><span data-stu-id="5ea5c-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="5ea5c-124">Wersja wstępna</span><span class="sxs-lookup"><span data-stu-id="5ea5c-124">PreRelease</span></span> | <span data-ttu-id="5ea5c-125">Obejmuje pakiety w wersjach wstępnych w ramach operacji dublowania.</span><span class="sxs-lookup"><span data-stu-id="5ea5c-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="5ea5c-126">Źródło</span><span class="sxs-lookup"><span data-stu-id="5ea5c-126">Source</span></span> | <span data-ttu-id="5ea5c-127">Lista źródeł pakietów w celu utworzenia duplikatów.</span><span class="sxs-lookup"><span data-stu-id="5ea5c-127">A list of package sources to mirror.</span></span> <span data-ttu-id="5ea5c-128">Jeśli nie określono żadnych źródeł, te zdefiniowane w pliku konfiguracji (patrz powyżej ApiKey) są używane, przyjęty adres nuget.org, jeśli żaden nie jest określony.</span><span class="sxs-lookup"><span data-stu-id="5ea5c-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="5ea5c-129">limit czasu</span><span class="sxs-lookup"><span data-stu-id="5ea5c-129">Timeout</span></span> | <span data-ttu-id="5ea5c-130">Określa limit czasu w sekundach, wypychania do serwera.</span><span class="sxs-lookup"><span data-stu-id="5ea5c-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="5ea5c-131">Wartość domyślna to 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="5ea5c-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="5ea5c-132">Wersja</span><span class="sxs-lookup"><span data-stu-id="5ea5c-132">Version</span></span> | <span data-ttu-id="5ea5c-133">Wersja pakietu do zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="5ea5c-133">The version of the package to install.</span></span> <span data-ttu-id="5ea5c-134">Jeśli nie zostanie określony, znajduje odzwierciedlenie najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="5ea5c-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="5ea5c-135">Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5ea5c-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5ea5c-136">Przykłady</span><span class="sxs-lookup"><span data-stu-id="5ea5c-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
