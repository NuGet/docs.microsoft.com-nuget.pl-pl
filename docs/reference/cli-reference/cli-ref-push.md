---
title: Polecenie push interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia nuget.exe push
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 54a09361173ae10040433b05fcfae7304e39452e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779181"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="4c81b-103">Push — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="4c81b-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="4c81b-104">**Dotyczy:** &bullet; **obsługiwane wersje** publikacji pakietu: ALL; 4.1.0 + Required for NuGet.org</span><span class="sxs-lookup"><span data-stu-id="4c81b-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="4c81b-105">Aby wypchnąć pakiety do nuget.org należy użyć nuget.exe v 4.1.0 +, które implementuje wymagane [Protokoły NuGet](../../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="4c81b-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../../api/nuget-protocols.md).</span></span>

<span data-ttu-id="4c81b-106">Wypchnij pakiet do źródła pakietu i opublikuje go.</span><span class="sxs-lookup"><span data-stu-id="4c81b-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="4c81b-107">Domyślna konfiguracja narzędzia NuGet jest uzyskiwana przez załadowanie `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), a następnie załadowanie `Nuget.Config` `.nuget\Nuget.Config` plików z katalogu głównego dysku i zakończenie w bieżącym katalogu (zobacz [typowe konfiguracje NuGet](../../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="4c81b-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="4c81b-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="4c81b-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="4c81b-109">gdzie `<packagePath>` identyfikuje pakiet do wypychania do serwera.</span><span class="sxs-lookup"><span data-stu-id="4c81b-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="4c81b-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="4c81b-110">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="4c81b-111">Klucz interfejsu API repozytorium docelowego.</span><span class="sxs-lookup"><span data-stu-id="4c81b-111">The API key for the target repository.</span></span> <span data-ttu-id="4c81b-112">Jeśli nie istnieje, jest używany określony w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4c81b-112">If not present,  the one specified in the config file is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="4c81b-113">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="4c81b-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="4c81b-114">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="4c81b-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DisableBuffering`**

  <span data-ttu-id="4c81b-115">Wyłącza buforowanie podczas wypychania do serwera HTTP (s) w celu zmniejszenia użycia pamięci.</span><span class="sxs-lookup"><span data-stu-id="4c81b-115">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="4c81b-116">Uwaga: Jeśli ta opcja jest używana, zintegrowane uwierzytelnianie systemu Windows może nie być możliwe.</span><span class="sxs-lookup"><span data-stu-id="4c81b-116">Caution: when this option is used, integrated Windows authentication might not work.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="4c81b-117">*(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.</span><span class="sxs-lookup"><span data-stu-id="4c81b-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="4c81b-118">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="4c81b-118">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="4c81b-119">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4c81b-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-NoServiceEndpoint`**

  <span data-ttu-id="4c81b-120">Nie dołącza `api/v2/packages` do źródłowego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="4c81b-120">Does not append `api/v2/packages` to the source URL.</span></span>

- **`-NoSymbols`**

  <span data-ttu-id="4c81b-121">*(3.5 +)* Jeśli pakiet symboli istnieje, nie zostanie wypychany do serwera symboli.</span><span class="sxs-lookup"><span data-stu-id="4c81b-121">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="4c81b-122">Określa adres URL serwera.</span><span class="sxs-lookup"><span data-stu-id="4c81b-122">Specifies the server URL.</span></span> <span data-ttu-id="4c81b-123">Pakiet NuGet identyfikuje źródło folderu UNC lub lokalnego i po prostu kopiuje plik, zamiast wypchnięcia go przy użyciu protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="4c81b-123">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="4c81b-124">Ponadto, rozpoczynając od 3.4.2 NuGet, jest to obowiązkowy parametr, chyba że `NuGet.Config` plik określa wartość *DefaultPushSource* (zobacz [Konfigurowanie zachowania NuGet](../../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="4c81b-124">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md)).</span></span>

- **`-SkipDuplicate`**

  <span data-ttu-id="4c81b-125">*(5.1 +)* Jeśli pakiet i wersja już istnieją, Pomiń ją i przejdź do następnego pakietu w wypychaniu (jeśli istnieje).</span><span class="sxs-lookup"><span data-stu-id="4c81b-125">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span>

- **`-SymbolSource`**

  <span data-ttu-id="4c81b-126">*(3.5 +)* Określa adres URL serwera symboli; nuget.smbsrc.net jest używany podczas wypychania do nuget.org</span><span class="sxs-lookup"><span data-stu-id="4c81b-126">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span>

- **`-SymbolApiKey`**

  <span data-ttu-id="4c81b-127">*(3.5 +)* Określa klucz interfejsu API dla adresu URL określonego w `-SymbolSource` .</span><span class="sxs-lookup"><span data-stu-id="4c81b-127">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span>

- **`-Timeout`**

  <span data-ttu-id="4c81b-128">Określa limit czasu (w sekundach) wypychania do serwera.</span><span class="sxs-lookup"><span data-stu-id="4c81b-128">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="4c81b-129">Wartość domyślna to 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="4c81b-129">The default is 300 seconds (5 minutes).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="4c81b-130">Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .</span><span class="sxs-lookup"><span data-stu-id="4c81b-130">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


<span data-ttu-id="4c81b-131">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="4c81b-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="4c81b-132">Przykłady</span><span class="sxs-lookup"><span data-stu-id="4c81b-132">Examples</span></span>

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
