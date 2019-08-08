---
title: Polecenie push interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia push. exe wypychania
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 40b2b2970934bae82c46cbe69156948e90746f97
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328292"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="24d8a-103">Push — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="24d8a-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="24d8a-104">**Dotyczy:** **obsługiwane wersje** publikacji &bullet; pakietu: ALL; 4.1.0 + Required for NuGet.org</span><span class="sxs-lookup"><span data-stu-id="24d8a-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="24d8a-105">Aby wypchnąć pakiety do nuget.org należy użyć NuGet. exe v 4.1.0 +, który implementuje wymagane [Protokoły NuGet](../../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="24d8a-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../../api/nuget-protocols.md).</span></span>

<span data-ttu-id="24d8a-106">Wypchnij pakiet do źródła pakietu i opublikuje go.</span><span class="sxs-lookup"><span data-stu-id="24d8a-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="24d8a-107">Domyślna konfiguracja narzędzia NuGet jest uzyskiwana przez `%AppData%\NuGet\NuGet.Config` załadowanie (system `~/.nuget/NuGet/NuGet.Config` Windows) lub (Mac/Linux `Nuget.Config` ) `.nuget\Nuget.Config` , a następnie załadowanie plików z katalogu głównego dysku i zakończenie w bieżącym katalogu (zobacz [Common NuGet konfiguracje](../../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="24d8a-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="24d8a-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="24d8a-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="24d8a-109">gdzie `<packagePath>` identyfikuje pakiet do wypychania do serwera.</span><span class="sxs-lookup"><span data-stu-id="24d8a-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="24d8a-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="24d8a-110">Options</span></span>

| <span data-ttu-id="24d8a-111">Opcja</span><span class="sxs-lookup"><span data-stu-id="24d8a-111">Option</span></span> | <span data-ttu-id="24d8a-112">Opis</span><span class="sxs-lookup"><span data-stu-id="24d8a-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="24d8a-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="24d8a-113">ApiKey</span></span> | <span data-ttu-id="24d8a-114">Klucz interfejsu API repozytorium docelowego.</span><span class="sxs-lookup"><span data-stu-id="24d8a-114">The API key for the target repository.</span></span> <span data-ttu-id="24d8a-115">Jeśli nie istnieje, jest używany określony w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="24d8a-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="24d8a-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="24d8a-116">ConfigFile</span></span> | <span data-ttu-id="24d8a-117">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="24d8a-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="24d8a-118">Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="24d8a-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="24d8a-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="24d8a-119">DisableBuffering</span></span> | <span data-ttu-id="24d8a-120">Wyłącza buforowanie podczas wypychania do serwera HTTP (s) w celu zmniejszenia użycia pamięci.</span><span class="sxs-lookup"><span data-stu-id="24d8a-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="24d8a-121">Uwaga: Jeśli ta opcja jest używana, zintegrowane uwierzytelnianie systemu Windows może nie być możliwe.</span><span class="sxs-lookup"><span data-stu-id="24d8a-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="24d8a-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="24d8a-122">ForceEnglishOutput</span></span> | <span data-ttu-id="24d8a-123">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="24d8a-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="24d8a-124">Help</span><span class="sxs-lookup"><span data-stu-id="24d8a-124">Help</span></span> | <span data-ttu-id="24d8a-125">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="24d8a-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="24d8a-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="24d8a-126">NonInteractive</span></span> | <span data-ttu-id="24d8a-127">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="24d8a-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="24d8a-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="24d8a-128">NoSymbols</span></span> | <span data-ttu-id="24d8a-129">*(3.5 +)* Jeśli pakiet symboli istnieje, nie zostanie wypychany do serwera symboli.</span><span class="sxs-lookup"><span data-stu-id="24d8a-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="24d8a-130">Source</span><span class="sxs-lookup"><span data-stu-id="24d8a-130">Source</span></span> | <span data-ttu-id="24d8a-131">Określa adres URL serwera.</span><span class="sxs-lookup"><span data-stu-id="24d8a-131">Specifies the server URL.</span></span> <span data-ttu-id="24d8a-132">Pakiet NuGet identyfikuje źródło folderu UNC lub lokalnego i po prostu kopiuje plik, zamiast wypchnięcia go przy użyciu protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="24d8a-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="24d8a-133">Ponadto, rozpoczynając od 3.4.2 NuGet, jest to obowiązkowy parametr, chyba że `NuGet.Config` plik określa wartość *DefaultPushSource* (zobacz [Konfigurowanie zachowania NuGet](../../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="24d8a-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="24d8a-134">SkipDuplicate</span><span class="sxs-lookup"><span data-stu-id="24d8a-134">SkipDuplicate</span></span> | <span data-ttu-id="24d8a-135">*(5.1 +)* Jeśli pakiet i wersja już istnieją, Pomiń ją i przejdź do następnego pakietu w wypychaniu (jeśli istnieje).</span><span class="sxs-lookup"><span data-stu-id="24d8a-135">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span> |
| <span data-ttu-id="24d8a-136">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="24d8a-136">SymbolSource</span></span> | <span data-ttu-id="24d8a-137">*(3.5 +)* Określa adres URL serwera symboli; nuget.smbsrc.net jest używany podczas wypychania do nuget.org</span><span class="sxs-lookup"><span data-stu-id="24d8a-137">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="24d8a-138">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="24d8a-138">SymbolApiKey</span></span> | <span data-ttu-id="24d8a-139">*(3.5 +)* Określa klucz interfejsu API dla adresu URL określonego w `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="24d8a-139">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="24d8a-140">limit czasu</span><span class="sxs-lookup"><span data-stu-id="24d8a-140">Timeout</span></span> | <span data-ttu-id="24d8a-141">Określa limit czasu (w sekundach) wypychania do serwera.</span><span class="sxs-lookup"><span data-stu-id="24d8a-141">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="24d8a-142">Wartość domyślna to 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="24d8a-142">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="24d8a-143">Verbosity</span><span class="sxs-lookup"><span data-stu-id="24d8a-143">Verbosity</span></span> | <span data-ttu-id="24d8a-144">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="24d8a-144">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="24d8a-145">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="24d8a-145">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="24d8a-146">Przykłady</span><span class="sxs-lookup"><span data-stu-id="24d8a-146">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```