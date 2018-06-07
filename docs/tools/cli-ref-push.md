---
title: Polecenie wypychania NuGet interfejsu wiersza polecenia
description: Informacje dotyczące polecenia wypychania nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 05cafa981ecf42829d1b3d8b8988ed51449d9d86
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817194"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="b0082-103">polecenie wypychania (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b0082-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="b0082-104">**Dotyczy:** publikowania pakietu &bullet; **obsługiwane wersje:** wszystkie; 4.1.0+ wymagane dla nuget.org</span><span class="sxs-lookup"><span data-stu-id="b0082-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="b0082-105">Aby wysyłać pakietów do nuget.org należy użyć nuget.exe v4.1.0 +, która implementuje wymaganych [protokołów NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="b0082-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="b0082-106">Wypychanie pakietu do źródła pakietu i publikuje ją.</span><span class="sxs-lookup"><span data-stu-id="b0082-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="b0082-107">Konfiguracja domyślna NuGet są uzyskiwane przez załadowanie `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux), następnie ładowania żadnych `Nuget.Config` lub `.nuget\Nuget.Config` pliki, począwszy od katalogu głównego dysku i kończący się w bieżącym katalogu (zobacz [Konfigurowanie Zachowanie NuGet](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="b0082-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="b0082-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="b0082-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="b0082-109">gdzie `<packagePath>` identyfikuje pakiet do serwera.</span><span class="sxs-lookup"><span data-stu-id="b0082-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="b0082-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="b0082-110">Options</span></span>

| <span data-ttu-id="b0082-111">Opcja</span><span class="sxs-lookup"><span data-stu-id="b0082-111">Option</span></span> | <span data-ttu-id="b0082-112">Opis</span><span class="sxs-lookup"><span data-stu-id="b0082-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b0082-113">apiKey</span><span class="sxs-lookup"><span data-stu-id="b0082-113">ApiKey</span></span> | <span data-ttu-id="b0082-114">Klucz interfejsu API dla repozytorium docelowej.</span><span class="sxs-lookup"><span data-stu-id="b0082-114">The API key for the target repository.</span></span> <span data-ttu-id="b0082-115">Jeśli nie istnieje określony w pliku konfiguracji jest używany.</span><span class="sxs-lookup"><span data-stu-id="b0082-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="b0082-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b0082-116">ConfigFile</span></span> | <span data-ttu-id="b0082-117">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="b0082-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b0082-118">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="b0082-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b0082-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="b0082-119">DisableBuffering</span></span> | <span data-ttu-id="b0082-120">Wyłącza buforowanie przypadku wypychania do serwera HTTP (s), aby zmniejszyć użycia pamięci.</span><span class="sxs-lookup"><span data-stu-id="b0082-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="b0082-121">Uwaga: Jeśli ta opcja jest używana, zintegrowane uwierzytelnianie systemu Windows może nie działać.</span><span class="sxs-lookup"><span data-stu-id="b0082-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="b0082-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b0082-122">ForceEnglishOutput</span></span> | <span data-ttu-id="b0082-123">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="b0082-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b0082-124">Pomoc</span><span class="sxs-lookup"><span data-stu-id="b0082-124">Help</span></span> | <span data-ttu-id="b0082-125">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="b0082-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="b0082-126">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="b0082-126">NonInteractive</span></span> | <span data-ttu-id="b0082-127">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="b0082-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b0082-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="b0082-128">NoSymbols</span></span> | <span data-ttu-id="b0082-129">*(3.5 +)*  Jeśli istnieje pakietu symboli, nie zostanie on przekazany do serwera symboli.</span><span class="sxs-lookup"><span data-stu-id="b0082-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="b0082-130">Źródło</span><span class="sxs-lookup"><span data-stu-id="b0082-130">Source</span></span> | <span data-ttu-id="b0082-131">Określa adres URL serwera.</span><span class="sxs-lookup"><span data-stu-id="b0082-131">Specifies the server URL.</span></span> <span data-ttu-id="b0082-132">NuGet identyfikuje UNC lub lokalny folder źródłowy i po prostu kopiuje plik zamiast wypychanie go przy użyciu protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="b0082-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="b0082-133">Ponadto, począwszy od NuGet 3.4.2, jest to parametr obowiązkowy chyba że `NuGet.Config` plik Określa *DefaultPushSource* wartość (zobacz [NuGet Konfigurowanie zachowania](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="b0082-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="b0082-134">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="b0082-134">SymbolSource</span></span> | <span data-ttu-id="b0082-135">*(3.5 +)*  Określa adres URL serwera symboli; nuget.smbsrc.net jest używana w przypadku wypychania w nuget.org</span><span class="sxs-lookup"><span data-stu-id="b0082-135">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="b0082-136">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="b0082-136">SymbolApiKey</span></span> | <span data-ttu-id="b0082-137">*(3.5 +)*  Określa klucz interfejsu API dla adresu URL określonego w `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="b0082-137">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="b0082-138">Limit czasu</span><span class="sxs-lookup"><span data-stu-id="b0082-138">Timeout</span></span> | <span data-ttu-id="b0082-139">Określa limit czasu w sekundach, do wypychania do serwera.</span><span class="sxs-lookup"><span data-stu-id="b0082-139">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="b0082-140">Wartość domyślna to 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="b0082-140">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="b0082-141">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="b0082-141">Verbosity</span></span> | <span data-ttu-id="b0082-142">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="b0082-142">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b0082-143">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b0082-143">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b0082-144">Przykłady</span><span class="sxs-lookup"><span data-stu-id="b0082-144">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
