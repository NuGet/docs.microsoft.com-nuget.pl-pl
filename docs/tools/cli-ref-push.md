---
title: Polecenie wypychania interfejs wiersza polecenia NuGet
description: Dokumentacja dotycząca poleceń wypychania nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b4f73e2b816d8a93e123d6de83ad0a15fbb24d18
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425934"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="e3387-103">polecenie wypychania (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="e3387-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="e3387-104">**Dotyczy:** pakietu publikowania &bullet; **obsługiwane wersje:** wszystkie; 4.1.0+ wymagane dla repozytorium nuget.org</span><span class="sxs-lookup"><span data-stu-id="e3387-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="e3387-105">Aby wypychania pakietów na stronie nuget.org należy użyć nuget.exe verze 4.1.0 +, która implementuje wymagane [protokołów NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="e3387-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="e3387-106">Wypychanie pakietu do źródła pakietu i publikuje go.</span><span class="sxs-lookup"><span data-stu-id="e3387-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="e3387-107">NuGet domyślnej konfiguracji można uzyskać przez ładowanie `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), następnie ładowania wszelkie `Nuget.Config` lub `.nuget\Nuget.Config` plików od głównego dysku i kończący się w bieżącym katalogu (zobacz [wspólnej NuGet konfiguracje](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="e3387-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="e3387-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="e3387-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="e3387-109">gdzie `<packagePath>` identyfikuje pakiet do wypychania do serwera.</span><span class="sxs-lookup"><span data-stu-id="e3387-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="e3387-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="e3387-110">Options</span></span>

| <span data-ttu-id="e3387-111">Opcja</span><span class="sxs-lookup"><span data-stu-id="e3387-111">Option</span></span> | <span data-ttu-id="e3387-112">Opis</span><span class="sxs-lookup"><span data-stu-id="e3387-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e3387-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="e3387-113">ApiKey</span></span> | <span data-ttu-id="e3387-114">Klucz interfejsu API w repozytorium docelowym.</span><span class="sxs-lookup"><span data-stu-id="e3387-114">The API key for the target repository.</span></span> <span data-ttu-id="e3387-115">Jeśli nie występuje, określony w pliku konfiguracji jest używany.</span><span class="sxs-lookup"><span data-stu-id="e3387-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="e3387-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e3387-116">ConfigFile</span></span> | <span data-ttu-id="e3387-117">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="e3387-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e3387-118">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="e3387-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="e3387-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="e3387-119">DisableBuffering</span></span> | <span data-ttu-id="e3387-120">Wyłącza buforowanie podczas wypychania do serwera HTTP (s) w celu zmniejszenia użycia pamięci.</span><span class="sxs-lookup"><span data-stu-id="e3387-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="e3387-121">Uwaga: Jeśli ta opcja jest używana, zintegrowane uwierzytelnianie Windows może nie działać.</span><span class="sxs-lookup"><span data-stu-id="e3387-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="e3387-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e3387-122">ForceEnglishOutput</span></span> | <span data-ttu-id="e3387-123">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="e3387-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e3387-124">Help</span><span class="sxs-lookup"><span data-stu-id="e3387-124">Help</span></span> | <span data-ttu-id="e3387-125">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="e3387-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="e3387-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="e3387-126">NonInteractive</span></span> | <span data-ttu-id="e3387-127">Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="e3387-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e3387-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="e3387-128">NoSymbols</span></span> | <span data-ttu-id="e3387-129">*(3.5 +)*  Jeżeli istnieje pakiet symboli, nie będą jej wypychane do serwera symboli.</span><span class="sxs-lookup"><span data-stu-id="e3387-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="e3387-130">Source</span><span class="sxs-lookup"><span data-stu-id="e3387-130">Source</span></span> | <span data-ttu-id="e3387-131">Określa adres URL serwera.</span><span class="sxs-lookup"><span data-stu-id="e3387-131">Specifies the server URL.</span></span> <span data-ttu-id="e3387-132">NuGet identyfikuje UNC lub lokalny folder źródłowy i po prostu kopiuje plik zamiast wypychanie go przy użyciu protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="e3387-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="e3387-133">Ponadto, począwszy od NuGet 3.4.2, jest to parametr obowiązkowy chyba że `NuGet.Config` plik Określa *DefaultPushSource* wartości (zobacz [zachowania programu NuGet Konfigurowanie](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="e3387-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="e3387-134">SkipDuplicate</span><span class="sxs-lookup"><span data-stu-id="e3387-134">SkipDuplicate</span></span> | <span data-ttu-id="e3387-135">*(5.1 +)*  Jeśli pakiet i wersji już istnieje, Pomiń je i Kontynuuj następnego pakietu wypychanie, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="e3387-135">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span> |
| <span data-ttu-id="e3387-136">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="e3387-136">SymbolSource</span></span> | <span data-ttu-id="e3387-137">*(3.5 +)*  Określa adres URL serwera symboli; nuget.smbsrc.net jest używany podczas wypychania do repozytorium nuget.org</span><span class="sxs-lookup"><span data-stu-id="e3387-137">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="e3387-138">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="e3387-138">SymbolApiKey</span></span> | <span data-ttu-id="e3387-139">*(3.5 +)*  Określa klucz interfejsu API dla adresu URL określonego w `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="e3387-139">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="e3387-140">limit czasu</span><span class="sxs-lookup"><span data-stu-id="e3387-140">Timeout</span></span> | <span data-ttu-id="e3387-141">Określa limit czasu w sekundach, wypychania do serwera.</span><span class="sxs-lookup"><span data-stu-id="e3387-141">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="e3387-142">Wartość domyślna to 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="e3387-142">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="e3387-143">Verbosity</span><span class="sxs-lookup"><span data-stu-id="e3387-143">Verbosity</span></span> | <span data-ttu-id="e3387-144">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="e3387-144">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="e3387-145">Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e3387-145">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e3387-146">Przykłady</span><span class="sxs-lookup"><span data-stu-id="e3387-146">Examples</span></span>

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
