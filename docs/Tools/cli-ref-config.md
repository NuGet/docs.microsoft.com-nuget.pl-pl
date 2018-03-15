---
title: Polecenie konfiguracji interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Informacje dotyczące polecenia konfiguracyjnego nuget.exe"
keywords: "Odwołanie do konfiguracji nuget, config, polecenie"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7cf7c06000904a617752567ed7612c0c48042db9
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/15/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="aaa5e-104">polecenie konfiguracji (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="aaa5e-104">config command (NuGet CLI)</span></span>

<span data-ttu-id="aaa5e-105">**Dotyczy:** wszystkie &bullet; **obsługiwane wersje**: wszystkie</span><span class="sxs-lookup"><span data-stu-id="aaa5e-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="aaa5e-106">Pobiera lub ustawia wartości konfiguracji NuGet.</span><span class="sxs-lookup"><span data-stu-id="aaa5e-106">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="aaa5e-107">Aby uzyskać dodatkowe obciążenie, zobacz [Konfigurowanie zachowania NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="aaa5e-107">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="aaa5e-108">Szczegółowe informacje dotyczące nazwami kluczy, zapoznaj się [odwołania do pliku config NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="aaa5e-108">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="aaa5e-109">Użycie</span><span class="sxs-lookup"><span data-stu-id="aaa5e-109">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="aaa5e-110">gdzie `<name>` i `<value>` określ parę klucz wartość można ustawić w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="aaa5e-110">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="aaa5e-111">Można określić dowolną liczbę par zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="aaa5e-111">You can specify as many pairs as desired.</span></span> <span data-ttu-id="aaa5e-112">Aby usunąć wartość, określ nazwę i `=` logowania, ale żadnej wartości.</span><span class="sxs-lookup"><span data-stu-id="aaa5e-112">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="aaa5e-113">Dopuszczalne nazw kluczy, zobacz [odwołania do pliku config NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="aaa5e-113">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="aaa5e-114">W NuGet 3.4 + `<value>` można użyć [zmiennych środowiskowych](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="aaa5e-114">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="aaa5e-115">Opcje</span><span class="sxs-lookup"><span data-stu-id="aaa5e-115">Options</span></span>

| <span data-ttu-id="aaa5e-116">Opcja</span><span class="sxs-lookup"><span data-stu-id="aaa5e-116">Option</span></span> | <span data-ttu-id="aaa5e-117">Opis</span><span class="sxs-lookup"><span data-stu-id="aaa5e-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="aaa5e-118">AsPath</span><span class="sxs-lookup"><span data-stu-id="aaa5e-118">AsPath</span></span> | <span data-ttu-id="aaa5e-119">Zwraca wartość konfiguracji jako ścieżka, zignorowane, kiedy `-Set` jest używany.</span><span class="sxs-lookup"><span data-stu-id="aaa5e-119">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="aaa5e-120">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="aaa5e-120">ConfigFile</span></span> | <span data-ttu-id="aaa5e-121">Plik konfiguracji NuGet do zmodyfikowania.</span><span class="sxs-lookup"><span data-stu-id="aaa5e-121">The NuGet configuration file to modify.</span></span> <span data-ttu-id="aaa5e-122">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="aaa5e-122">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="aaa5e-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="aaa5e-123">ForceEnglishOutput</span></span> | <span data-ttu-id="aaa5e-124">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="aaa5e-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="aaa5e-125">Pomoc</span><span class="sxs-lookup"><span data-stu-id="aaa5e-125">Help</span></span> | <span data-ttu-id="aaa5e-126">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="aaa5e-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="aaa5e-127">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="aaa5e-127">NonInteractive</span></span> | <span data-ttu-id="aaa5e-128">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="aaa5e-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="aaa5e-129">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="aaa5e-129">Verbosity</span></span> | <span data-ttu-id="aaa5e-130">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="aaa5e-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="aaa5e-131">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="aaa5e-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="aaa5e-132">Przykłady</span><span class="sxs-lookup"><span data-stu-id="aaa5e-132">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
