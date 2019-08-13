---
title: Polecenie dublowania interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia dublowania NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 81866172bfbf55c42ee96c213c0117f1f986235c
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959709"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="455c3-103">mirror command, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="455c3-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="455c3-104">**Dotyczy:** **wersje obsługiwane** przez &bullet; publikowanie pakietów: przestarzałe w 3.2 +</span><span class="sxs-lookup"><span data-stu-id="455c3-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="455c3-105">Odzwierciedla pakiet i jego zależności z określonych repozytoriów źródłowych do repozytorium docelowego.</span><span class="sxs-lookup"><span data-stu-id="455c3-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="455c3-106">Pliki NuGet. ServerExtensions. dll i NuGet-Signed. exe, które wcześniej obsługiwały to polecenie w programie NuGet 2. x (przez zmianę nazwy NuGet-Signed. exe na NuGet. exe), nie są już dostępne do pobrania.</span><span class="sxs-lookup"><span data-stu-id="455c3-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="455c3-107">Aby użyć polecenia podobnego do tego, wypróbuj [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span><span class="sxs-lookup"><span data-stu-id="455c3-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="455c3-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="455c3-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="455c3-109">gdzie `<packageID>` jest pakiet do dublowania lub `<configFilePath>` identyfikuje `packages.config` plik, który zawiera listę pakietów do dublowania.</span><span class="sxs-lookup"><span data-stu-id="455c3-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="455c3-110">Określa repozytorium źródłowe i `<publishUrlTarget>` określa repozytorium docelowe. `<listUrlTarget>`</span><span class="sxs-lookup"><span data-stu-id="455c3-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="455c3-111">Jeśli repozytorium docelowe znajduje się na `https://machine/repo` komputerze, na którym jest uruchomiony program [NuGet. Server](../../hosting-packages/nuget-server.md), lista i adresy `https://machine/repo/nuget` URL `https://machine/repo/api/v2/package`wypychania będą odpowiednio i.</span><span class="sxs-lookup"><span data-stu-id="455c3-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="455c3-112">Opcje</span><span class="sxs-lookup"><span data-stu-id="455c3-112">Options</span></span>

| <span data-ttu-id="455c3-113">Opcja</span><span class="sxs-lookup"><span data-stu-id="455c3-113">Option</span></span> | <span data-ttu-id="455c3-114">Opis</span><span class="sxs-lookup"><span data-stu-id="455c3-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="455c3-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="455c3-115">ApiKey</span></span> | <span data-ttu-id="455c3-116">Klucz interfejsu API repozytorium docelowego.</span><span class="sxs-lookup"><span data-stu-id="455c3-116">The API key for the target repository.</span></span> <span data-ttu-id="455c3-117">Jeśli nie istnieje, jest używany określony w pliku konfiguracyjnym (`%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="455c3-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="455c3-118">Help</span><span class="sxs-lookup"><span data-stu-id="455c3-118">Help</span></span> | <span data-ttu-id="455c3-119">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="455c3-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="455c3-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="455c3-120">NoCache</span></span> | <span data-ttu-id="455c3-121">Uniemożliwia narzędziu NuGet używanie buforowanych pakietów.</span><span class="sxs-lookup"><span data-stu-id="455c3-121">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="455c3-122">Zobacz [Zarządzanie pakietami globalnymi i folderami pamięci](../../consume-packages/managing-the-global-packages-and-cache-folders.md)podręcznej.</span><span class="sxs-lookup"><span data-stu-id="455c3-122">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="455c3-123">Aktualizujący nie działa</span><span class="sxs-lookup"><span data-stu-id="455c3-123">Noop</span></span> | <span data-ttu-id="455c3-124">Rejestruje co robić, ale nie wykonuje akcji; przyjęto założenie sukcesu dla operacji wypychania.</span><span class="sxs-lookup"><span data-stu-id="455c3-124">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="455c3-125">Wersja wstępna</span><span class="sxs-lookup"><span data-stu-id="455c3-125">PreRelease</span></span> | <span data-ttu-id="455c3-126">Obejmuje pakiety wersji wstępnej w operacji dublowania.</span><span class="sxs-lookup"><span data-stu-id="455c3-126">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="455c3-127">Source</span><span class="sxs-lookup"><span data-stu-id="455c3-127">Source</span></span> | <span data-ttu-id="455c3-128">Lista źródeł pakietów do dublowania.</span><span class="sxs-lookup"><span data-stu-id="455c3-128">A list of package sources to mirror.</span></span> <span data-ttu-id="455c3-129">Jeśli nie określono żadnych źródeł, są one zdefiniowane w pliku konfiguracyjnym (zobacz ApiKey powyżej), jeśli nie określono żadnego z nich.</span><span class="sxs-lookup"><span data-stu-id="455c3-129">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="455c3-130">limit czasu</span><span class="sxs-lookup"><span data-stu-id="455c3-130">Timeout</span></span> | <span data-ttu-id="455c3-131">Określa limit czasu (w sekundach) wypychania do serwera.</span><span class="sxs-lookup"><span data-stu-id="455c3-131">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="455c3-132">Wartość domyślna to 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="455c3-132">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="455c3-133">Wersja</span><span class="sxs-lookup"><span data-stu-id="455c3-133">Version</span></span> | <span data-ttu-id="455c3-134">Wersja pakietu do zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="455c3-134">The version of the package to install.</span></span> <span data-ttu-id="455c3-135">Jeśli nie zostanie określony, Najnowsza wersja jest dublowana.</span><span class="sxs-lookup"><span data-stu-id="455c3-135">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="455c3-136">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="455c3-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="455c3-137">Przykłady</span><span class="sxs-lookup"><span data-stu-id="455c3-137">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
