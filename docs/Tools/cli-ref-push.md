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
ms.openlocfilehash: 50883bc85ab96cba54fb4ce0bd344e8148c4fab1
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="6b417-104">polecenie wypychania (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="6b417-104">push command (NuGet CLI)</span></span>

<span data-ttu-id="6b417-105">**Dotyczy:** publikowania pakietu &bullet; **obsługiwane wersje:** wszystkie; 4.1.0+ wymagane dla nuget.org</span><span class="sxs-lookup"><span data-stu-id="6b417-105">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="6b417-106">Aby wysyłać pakietów do nuget.org należy użyć nuget.exe v4.1.0 +, która implementuje wymaganych [protokołów NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="6b417-106">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="6b417-107">Wypychanie pakietu do źródła pakietu i publikuje ją.</span><span class="sxs-lookup"><span data-stu-id="6b417-107">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="6b417-108">NuGet domyślnej konfiguracji są uzyskiwane przez ładowanie `%AppData%\NuGet\NuGet.Config`, a następnie ładowania `Nuget.Config` lub `.nuget\Nuget.Config` pliki, począwszy od katalogu głównego dysku i kończący się w bieżącym katalogu (zobacz [Konfigurowanie zachowania NuGet](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="6b417-108">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config`, then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="6b417-109">Użycie</span><span class="sxs-lookup"><span data-stu-id="6b417-109">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="6b417-110">gdzie `<packagePath>` identyfikuje pakiet do serwera.</span><span class="sxs-lookup"><span data-stu-id="6b417-110">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="6b417-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="6b417-111">Options</span></span>

| <span data-ttu-id="6b417-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="6b417-112">Option</span></span> | <span data-ttu-id="6b417-113">Opis</span><span class="sxs-lookup"><span data-stu-id="6b417-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6b417-114">apiKey</span><span class="sxs-lookup"><span data-stu-id="6b417-114">ApiKey</span></span> | <span data-ttu-id="6b417-115">Klucz interfejsu API dla repozytorium docelowej.</span><span class="sxs-lookup"><span data-stu-id="6b417-115">The API key for the target repository.</span></span> <span data-ttu-id="6b417-116">Jeśli nie występuje, określony w *%AppData%\NuGet\NuGet.Config* jest używany.</span><span class="sxs-lookup"><span data-stu-id="6b417-116">If not present,  the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="6b417-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="6b417-117">ConfigFile</span></span> | <span data-ttu-id="6b417-118">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="6b417-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="6b417-119">Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany.</span><span class="sxs-lookup"><span data-stu-id="6b417-119">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="6b417-120">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="6b417-120">DisableBuffering</span></span> | <span data-ttu-id="6b417-121">Wyłącza buforowanie przypadku wypychania do serwera HTTP (s), aby zmniejszyć użycia pamięci.</span><span class="sxs-lookup"><span data-stu-id="6b417-121">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="6b417-122">Uwaga: Jeśli ta opcja jest używana, zintegrowane uwierzytelnianie systemu Windows może nie działać.</span><span class="sxs-lookup"><span data-stu-id="6b417-122">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="6b417-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="6b417-123">ForceEnglishOutput</span></span> | <span data-ttu-id="6b417-124">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="6b417-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="6b417-125">Pomoc</span><span class="sxs-lookup"><span data-stu-id="6b417-125">Help</span></span> | <span data-ttu-id="6b417-126">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="6b417-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="6b417-127">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="6b417-127">NonInteractive</span></span> | <span data-ttu-id="6b417-128">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="6b417-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="6b417-129">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="6b417-129">NoSymbols</span></span> | <span data-ttu-id="6b417-130">*(3.5 +)*  Jeśli istnieje pakietu symboli, nie zostanie on przekazany do serwera symboli.</span><span class="sxs-lookup"><span data-stu-id="6b417-130">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="6b417-131">Źródło</span><span class="sxs-lookup"><span data-stu-id="6b417-131">Source</span></span> | <span data-ttu-id="6b417-132">Określa adres URL serwera.</span><span class="sxs-lookup"><span data-stu-id="6b417-132">Specifies the server URL.</span></span> <span data-ttu-id="6b417-133">NuGet identyfikuje UNC lub lokalny folder źródłowy i po prostu kopiuje plik zamiast wypychanie go przy użyciu protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="6b417-133">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="6b417-134">Ponadto, począwszy od NuGet 3.4.2, jest to parametr obowiązkowy chyba że `NuGet.Config` plik Określa *DefaultPushSource* wartość (zobacz [NuGet Konfigurowanie zachowania](../Consume-Packages/Configuring-NuGet-Behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="6b417-134">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md)).</span></span> |
| <span data-ttu-id="6b417-135">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="6b417-135">SymbolSource</span></span> | <span data-ttu-id="6b417-136">*(3.5 +)*  Określa adres URL serwera symboli; nuget.smbsrc.net jest używana w przypadku wypychania w nuget.org</span><span class="sxs-lookup"><span data-stu-id="6b417-136">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="6b417-137">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="6b417-137">SymbolApiKey</span></span> | <span data-ttu-id="6b417-138">*(3.5 +)*  Określa klucz interfejsu API dla adresu URL określonego w `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="6b417-138">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="6b417-139">Limit czasu</span><span class="sxs-lookup"><span data-stu-id="6b417-139">Timeout</span></span> | <span data-ttu-id="6b417-140">Określa limit czasu w sekundach, do wypychania do serwera.</span><span class="sxs-lookup"><span data-stu-id="6b417-140">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="6b417-141">Wartość domyślna to 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="6b417-141">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="6b417-142">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="6b417-142">Verbosity</span></span> | <span data-ttu-id="6b417-143">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="6b417-143">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="6b417-144">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="6b417-144">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="6b417-145">Przykłady</span><span class="sxs-lookup"><span data-stu-id="6b417-145">Examples</span></span>

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
