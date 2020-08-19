---
title: Polecenie dublowania interfejsu wiersza polecenia NuGet
description: Odwołanie do nuget.exe polecenia dublowania
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a7247aeb21418e78dbfe9be15c2e7cd152aa3f4a
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622970"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="f941a-103">Mirror — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="f941a-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="f941a-104">**Dotyczy:** &bullet; **wersje obsługiwane** przez publikowanie pakietów: przestarzałe w 3.2 +</span><span class="sxs-lookup"><span data-stu-id="f941a-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="f941a-105">Odzwierciedla pakiet i jego zależności z określonych repozytoriów źródłowych do repozytorium docelowego.</span><span class="sxs-lookup"><span data-stu-id="f941a-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="f941a-106">NuGet.ServerExtensions.dll i NuGet-Signed.exe, które wcześniej obsługiwały to polecenie w programie NuGet 2. x (poprzez zmianę nazwy NuGet-Signed.exe na nuget.exe) nie są już dostępne do pobrania.</span><span class="sxs-lookup"><span data-stu-id="f941a-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="f941a-107">Aby użyć polecenia podobnego do tego, wypróbuj [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span><span class="sxs-lookup"><span data-stu-id="f941a-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="f941a-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="f941a-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="f941a-109">gdzie `<packageID>` jest pakiet do dublowania lub `<configFilePath>` identyfikuje plik, `packages.config` który zawiera listę pakietów do dublowania.</span><span class="sxs-lookup"><span data-stu-id="f941a-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="f941a-110">`<listUrlTarget>`Określa repozytorium źródłowe i `<publishUrlTarget>` określa repozytorium docelowe.</span><span class="sxs-lookup"><span data-stu-id="f941a-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="f941a-111">Jeśli repozytorium docelowe znajduje się na komputerze, na którym jest `https://machine/repo` uruchomiony program [NuGet. Server](../../hosting-packages/nuget-server.md), lista i adresy URL wypychania będą `https://machine/repo/nuget` `https://machine/repo/api/v2/package` odpowiednio i.</span><span class="sxs-lookup"><span data-stu-id="f941a-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="f941a-112">Opcje</span><span class="sxs-lookup"><span data-stu-id="f941a-112">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="f941a-113">Klucz interfejsu API repozytorium docelowego.</span><span class="sxs-lookup"><span data-stu-id="f941a-113">The API key for the target repository.</span></span> <span data-ttu-id="f941a-114">Jeśli nie istnieje, jest używany określony w pliku konfiguracyjnym ( `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="f941a-114">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span>

- **`-Help`**

  <span data-ttu-id="f941a-115">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="f941a-115">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="f941a-116">Uniemożliwia narzędziu NuGet używanie buforowanych pakietów.</span><span class="sxs-lookup"><span data-stu-id="f941a-116">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="f941a-117">Zobacz [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="f941a-117">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-Noop`**

  <span data-ttu-id="f941a-118">Rejestruje co robić, ale nie wykonuje akcji; przyjęto założenie sukcesu dla operacji wypychania.</span><span class="sxs-lookup"><span data-stu-id="f941a-118">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="f941a-119">Obejmuje pakiety wersji wstępnej w operacji dublowania.</span><span class="sxs-lookup"><span data-stu-id="f941a-119">Includes prerelease packages in the mirroring operation.</span></span>

- **`-Source`**

  <span data-ttu-id="f941a-120">Lista źródeł pakietów do dublowania.</span><span class="sxs-lookup"><span data-stu-id="f941a-120">A list of package sources to mirror.</span></span> <span data-ttu-id="f941a-121">Jeśli nie określono żadnych źródeł, są one zdefiniowane w pliku konfiguracyjnym (zobacz ApiKey powyżej), jeśli nie określono żadnego z nich.</span><span class="sxs-lookup"><span data-stu-id="f941a-121">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span>

- **`-Timeout`**

  <span data-ttu-id="f941a-122">Określa limit czasu (w sekundach) wypychania do serwera.</span><span class="sxs-lookup"><span data-stu-id="f941a-122">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="f941a-123">Wartość domyślna to 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="f941a-123">The default is 300 seconds (5 minutes).</span></span>

- **`-Version`**

  <span data-ttu-id="f941a-124">Wersja pakietu do zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="f941a-124">The version of the package to install.</span></span> <span data-ttu-id="f941a-125">Jeśli nie zostanie określony, Najnowsza wersja jest dublowana.</span><span class="sxs-lookup"><span data-stu-id="f941a-125">If not specified, the latest version is mirrored.</span></span>

<span data-ttu-id="f941a-126">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f941a-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f941a-127">Przykłady</span><span class="sxs-lookup"><span data-stu-id="f941a-127">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
