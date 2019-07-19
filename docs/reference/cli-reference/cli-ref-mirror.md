---
title: Polecenie dublowania interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia dublowania NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 076d7a480e2f07149e4ec7ac58c7ab37040e7a8f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328304"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="14922-103">mirror command, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="14922-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="14922-104">**Dotyczy:** **wersje obsługiwane** przez &bullet; publikowanie pakietów: przestarzałe w 3.2 +</span><span class="sxs-lookup"><span data-stu-id="14922-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="14922-105">Odzwierciedla pakiet i jego zależności z określonych repozytoriów źródłowych do repozytorium docelowego.</span><span class="sxs-lookup"><span data-stu-id="14922-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="14922-106">Aby włączyć to polecenie dla wersji NuGet przed 3,2, przejdź do [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), wybierz najnowszą stabilną wersję, Pobierz `NuGet.ServerExtensions.dll` i `Nuget-Signed.exe` na dysk lokalny, a następnie `Nuget-Signed.exe` Zmień `nuget.exe` nazwę na.</span><span class="sxs-lookup"><span data-stu-id="14922-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="14922-107">Użycie</span><span class="sxs-lookup"><span data-stu-id="14922-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="14922-108">gdzie `<packageID>` jest pakiet do dublowania lub `<configFilePath>` identyfikuje `packages.config` plik, który zawiera listę pakietów do dublowania.</span><span class="sxs-lookup"><span data-stu-id="14922-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="14922-109">Określa repozytorium źródłowe i `<publishUrlTarget>` określa repozytorium docelowe. `<listUrlTarget>`</span><span class="sxs-lookup"><span data-stu-id="14922-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="14922-110">Jeśli repozytorium docelowe znajduje się na `https://machine/repo` komputerze, na którym jest uruchomiony program [NuGet. Server](../../hosting-packages/nuget-server.md), lista i adresy `https://machine/repo/nuget` URL `https://machine/repo/api/v2/package`wypychania będą odpowiednio i.</span><span class="sxs-lookup"><span data-stu-id="14922-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="14922-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="14922-111">Options</span></span>

| <span data-ttu-id="14922-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="14922-112">Option</span></span> | <span data-ttu-id="14922-113">Opis</span><span class="sxs-lookup"><span data-stu-id="14922-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="14922-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="14922-114">ApiKey</span></span> | <span data-ttu-id="14922-115">Klucz interfejsu API repozytorium docelowego.</span><span class="sxs-lookup"><span data-stu-id="14922-115">The API key for the target repository.</span></span> <span data-ttu-id="14922-116">Jeśli nie istnieje, jest używany określony w pliku konfiguracyjnym (`%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="14922-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="14922-117">Help</span><span class="sxs-lookup"><span data-stu-id="14922-117">Help</span></span> | <span data-ttu-id="14922-118">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="14922-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="14922-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="14922-119">NoCache</span></span> | <span data-ttu-id="14922-120">Uniemożliwia narzędziu NuGet używanie buforowanych pakietów.</span><span class="sxs-lookup"><span data-stu-id="14922-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="14922-121">Zobacz [Zarządzanie pakietami globalnymi i folderami pamięci](../../consume-packages/managing-the-global-packages-and-cache-folders.md)podręcznej.</span><span class="sxs-lookup"><span data-stu-id="14922-121">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="14922-122">Aktualizujący nie działa</span><span class="sxs-lookup"><span data-stu-id="14922-122">Noop</span></span> | <span data-ttu-id="14922-123">Rejestruje co robić, ale nie wykonuje akcji; przyjęto założenie sukcesu dla operacji wypychania.</span><span class="sxs-lookup"><span data-stu-id="14922-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="14922-124">Wersja wstępna</span><span class="sxs-lookup"><span data-stu-id="14922-124">PreRelease</span></span> | <span data-ttu-id="14922-125">Obejmuje pakiety wersji wstępnej w operacji dublowania.</span><span class="sxs-lookup"><span data-stu-id="14922-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="14922-126">Source</span><span class="sxs-lookup"><span data-stu-id="14922-126">Source</span></span> | <span data-ttu-id="14922-127">Lista źródeł pakietów do dublowania.</span><span class="sxs-lookup"><span data-stu-id="14922-127">A list of package sources to mirror.</span></span> <span data-ttu-id="14922-128">Jeśli nie określono żadnych źródeł, są one zdefiniowane w pliku konfiguracyjnym (zobacz ApiKey powyżej), jeśli nie określono żadnego z nich.</span><span class="sxs-lookup"><span data-stu-id="14922-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="14922-129">limit czasu</span><span class="sxs-lookup"><span data-stu-id="14922-129">Timeout</span></span> | <span data-ttu-id="14922-130">Określa limit czasu (w sekundach) wypychania do serwera.</span><span class="sxs-lookup"><span data-stu-id="14922-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="14922-131">Wartość domyślna to 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="14922-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="14922-132">Wersja</span><span class="sxs-lookup"><span data-stu-id="14922-132">Version</span></span> | <span data-ttu-id="14922-133">Wersja pakietu do zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="14922-133">The version of the package to install.</span></span> <span data-ttu-id="14922-134">Jeśli nie zostanie określony, Najnowsza wersja jest dublowana.</span><span class="sxs-lookup"><span data-stu-id="14922-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="14922-135">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="14922-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="14922-136">Przykłady</span><span class="sxs-lookup"><span data-stu-id="14922-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
