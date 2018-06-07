---
title: Polecenie dublowanie NuGet interfejsu wiersza polecenia
description: Informacje dotyczące polecenia dublowanie nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4cec854f05fcd207bb15a50ea4ebdc201fdb3ac6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818155"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="55ed2-103">mirror command, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="55ed2-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="55ed2-104">**Dotyczy:** publikowania pakietu &bullet; **obsługiwane wersje:** uznane za przestarzałe w wersji 3.2 +</span><span class="sxs-lookup"><span data-stu-id="55ed2-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="55ed2-105">Odzwierciedla pakiet i jego zależności z repozytoriami określonego źródła w repozytorium docelowej.</span><span class="sxs-lookup"><span data-stu-id="55ed2-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="55ed2-106">Aby włączyć to polecenie dla wersji NuGet przed 3.2, przejdź do [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases)wybierz najnowsza stabilna wersja, Pobierz `NuGet.ServerExtensions.dll` i `Nuget-Signed.exe` na dysku lokalnym i Zmień nazwę `Nuget-Signed.exe` do `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="55ed2-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="55ed2-107">Użycie</span><span class="sxs-lookup"><span data-stu-id="55ed2-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="55ed2-108">gdzie `<packageID>` jest pakietem dotyczącą tworzenia duplikatów, lub `<configFilePath>` identyfikuje `packages.config` pliku, który zawiera listę pakietów dublowanego.</span><span class="sxs-lookup"><span data-stu-id="55ed2-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="55ed2-109">`<listUrlTarget>` Określa repozytorium źródłowe i `<publishUrlTarget>` określa repozytorium docelowe.</span><span class="sxs-lookup"><span data-stu-id="55ed2-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="55ed2-110">Jeśli repozytorium docelowy znajduje się na `https://machine/repo` systemem [NuGet.Server](../hosting-packages/nuget-server.md), listy i wypychania adresów URL będzie `https://machine/repo/nuget` i `https://machine/repo/api/v2/package`odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="55ed2-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="55ed2-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="55ed2-111">Options</span></span>

| <span data-ttu-id="55ed2-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="55ed2-112">Option</span></span> | <span data-ttu-id="55ed2-113">Opis</span><span class="sxs-lookup"><span data-stu-id="55ed2-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="55ed2-114">apiKey</span><span class="sxs-lookup"><span data-stu-id="55ed2-114">ApiKey</span></span> | <span data-ttu-id="55ed2-115">Klucz interfejsu API dla repozytorium docelowej.</span><span class="sxs-lookup"><span data-stu-id="55ed2-115">The API key for the target repository.</span></span> <span data-ttu-id="55ed2-116">Jeśli nie występuje, określony w pliku konfiguracyjnym jest używana (`%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="55ed2-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="55ed2-117">Pomoc</span><span class="sxs-lookup"><span data-stu-id="55ed2-117">Help</span></span> | <span data-ttu-id="55ed2-118">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="55ed2-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="55ed2-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="55ed2-119">NoCache</span></span> | <span data-ttu-id="55ed2-120">Zapobiega przy użyciu pamięci podręcznej pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="55ed2-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="55ed2-121">Zobacz [Zarządzanie globalne pakietów i foldery pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="55ed2-121">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="55ed2-122">Operacja</span><span class="sxs-lookup"><span data-stu-id="55ed2-122">Noop</span></span> | <span data-ttu-id="55ed2-123">Rejestruje co będą wykonywane, ale nie wykonuje akcji; Założono powodzenie operacji wypychania.</span><span class="sxs-lookup"><span data-stu-id="55ed2-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="55ed2-124">Wydanie wstępne</span><span class="sxs-lookup"><span data-stu-id="55ed2-124">PreRelease</span></span> | <span data-ttu-id="55ed2-125">Zawiera pakiety wersji wstępnej w operacji dublowania.</span><span class="sxs-lookup"><span data-stu-id="55ed2-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="55ed2-126">Źródło</span><span class="sxs-lookup"><span data-stu-id="55ed2-126">Source</span></span> | <span data-ttu-id="55ed2-127">Lista źródła pakietów w celu utworzenia duplikatów.</span><span class="sxs-lookup"><span data-stu-id="55ed2-127">A list of package sources to mirror.</span></span> <span data-ttu-id="55ed2-128">Jeśli nie określono żadnych źródeł, te zdefiniowane w pliku konfiguracyjnym (zobacz powyżej ApiKey) są używane, przyjęty nuget.org, jeśli żaden nie jest określony.</span><span class="sxs-lookup"><span data-stu-id="55ed2-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="55ed2-129">Limit czasu</span><span class="sxs-lookup"><span data-stu-id="55ed2-129">Timeout</span></span> | <span data-ttu-id="55ed2-130">Określa limit czasu w sekundach, do wypychania do serwera.</span><span class="sxs-lookup"><span data-stu-id="55ed2-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="55ed2-131">Wartość domyślna to 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="55ed2-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="55ed2-132">Wersja</span><span class="sxs-lookup"><span data-stu-id="55ed2-132">Version</span></span> | <span data-ttu-id="55ed2-133">Wersja pakietu do zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="55ed2-133">The version of the package to install.</span></span> <span data-ttu-id="55ed2-134">Jeśli nie zostanie określony, jest dublowany najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="55ed2-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="55ed2-135">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="55ed2-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="55ed2-136">Przykłady</span><span class="sxs-lookup"><span data-stu-id="55ed2-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
