---
title: Polecenie wypychania interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Informacje dotyczące polecenia wypychania nuget.exe"
keywords: "Odwołanie do wypychania nuget, polecenie wypychania"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 095e81406df3db5fbfc6c5202362894b2c6d7cf8
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/15/2018
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="4f896-104">polecenie wypychania (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="4f896-104">push command (NuGet CLI)</span></span>

<span data-ttu-id="4f896-105">**Dotyczy:** publikowania pakietu &bullet; **obsługiwane wersje:** wszystkie; 4.1.0+ wymagane dla nuget.org</span><span class="sxs-lookup"><span data-stu-id="4f896-105">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="4f896-106">Aby wysyłać pakietów do nuget.org należy użyć nuget.exe v4.1.0 +, która implementuje wymaganych [protokołów NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="4f896-106">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="4f896-107">Wypychanie pakietu do źródła pakietu i publikuje ją.</span><span class="sxs-lookup"><span data-stu-id="4f896-107">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="4f896-108">Konfiguracja domyślna NuGet są uzyskiwane przez załadowanie `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux), następnie ładowania żadnych `Nuget.Config` lub `.nuget\Nuget.Config` pliki, począwszy od katalogu głównego dysku i kończący się w bieżącym katalogu (zobacz [Konfigurowanie Zachowanie NuGet](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="4f896-108">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="4f896-109">Użycie</span><span class="sxs-lookup"><span data-stu-id="4f896-109">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="4f896-110">gdzie `<packagePath>` identyfikuje pakiet do serwera.</span><span class="sxs-lookup"><span data-stu-id="4f896-110">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="4f896-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="4f896-111">Options</span></span>

| <span data-ttu-id="4f896-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="4f896-112">Option</span></span> | <span data-ttu-id="4f896-113">Opis</span><span class="sxs-lookup"><span data-stu-id="4f896-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4f896-114">apiKey</span><span class="sxs-lookup"><span data-stu-id="4f896-114">ApiKey</span></span> | <span data-ttu-id="4f896-115">Klucz interfejsu API dla repozytorium docelowej.</span><span class="sxs-lookup"><span data-stu-id="4f896-115">The API key for the target repository.</span></span> <span data-ttu-id="4f896-116">Jeśli nie istnieje określony w pliku konfiguracji jest używany.</span><span class="sxs-lookup"><span data-stu-id="4f896-116">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="4f896-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="4f896-117">ConfigFile</span></span> | <span data-ttu-id="4f896-118">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="4f896-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="4f896-119">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="4f896-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="4f896-120">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="4f896-120">DisableBuffering</span></span> | <span data-ttu-id="4f896-121">Wyłącza buforowanie przypadku wypychania do serwera HTTP (s), aby zmniejszyć użycia pamięci.</span><span class="sxs-lookup"><span data-stu-id="4f896-121">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="4f896-122">Uwaga: Jeśli ta opcja jest używana, zintegrowane uwierzytelnianie systemu Windows może nie działać.</span><span class="sxs-lookup"><span data-stu-id="4f896-122">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="4f896-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="4f896-123">ForceEnglishOutput</span></span> | <span data-ttu-id="4f896-124">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="4f896-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="4f896-125">Pomoc</span><span class="sxs-lookup"><span data-stu-id="4f896-125">Help</span></span> | <span data-ttu-id="4f896-126">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="4f896-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="4f896-127">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="4f896-127">NonInteractive</span></span> | <span data-ttu-id="4f896-128">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="4f896-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="4f896-129">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="4f896-129">NoSymbols</span></span> | <span data-ttu-id="4f896-130">*(3.5 +)*  Jeśli istnieje pakietu symboli, nie zostanie on przekazany do serwera symboli.</span><span class="sxs-lookup"><span data-stu-id="4f896-130">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="4f896-131">Źródło</span><span class="sxs-lookup"><span data-stu-id="4f896-131">Source</span></span> | <span data-ttu-id="4f896-132">Określa adres URL serwera.</span><span class="sxs-lookup"><span data-stu-id="4f896-132">Specifies the server URL.</span></span> <span data-ttu-id="4f896-133">NuGet identyfikuje UNC lub lokalny folder źródłowy i po prostu kopiuje plik zamiast wypychanie go przy użyciu protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="4f896-133">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="4f896-134">Ponadto, począwszy od NuGet 3.4.2, jest to parametr obowiązkowy chyba że `NuGet.Config` plik Określa *DefaultPushSource* wartość (zobacz [NuGet Konfigurowanie zachowania](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="4f896-134">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="4f896-135">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="4f896-135">SymbolSource</span></span> | <span data-ttu-id="4f896-136">*(3.5 +)*  Określa adres URL serwera symboli; nuget.smbsrc.net jest używana w przypadku wypychania w nuget.org</span><span class="sxs-lookup"><span data-stu-id="4f896-136">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="4f896-137">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="4f896-137">SymbolApiKey</span></span> | <span data-ttu-id="4f896-138">*(3.5 +)*  Określa klucz interfejsu API dla adresu URL określonego w `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="4f896-138">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="4f896-139">Limit czasu</span><span class="sxs-lookup"><span data-stu-id="4f896-139">Timeout</span></span> | <span data-ttu-id="4f896-140">Określa limit czasu w sekundach, do wypychania do serwera.</span><span class="sxs-lookup"><span data-stu-id="4f896-140">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="4f896-141">Wartość domyślna to 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="4f896-141">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="4f896-142">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="4f896-142">Verbosity</span></span> | <span data-ttu-id="4f896-143">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="4f896-143">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="4f896-144">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="4f896-144">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="4f896-145">Przykłady</span><span class="sxs-lookup"><span data-stu-id="4f896-145">Examples</span></span>

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
