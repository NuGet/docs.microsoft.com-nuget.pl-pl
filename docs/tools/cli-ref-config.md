---
title: Polecenie konfiguracji interfejsu wiersza polecenia NuGet
description: Informacje dotyczące polecenia konfiguracyjnego nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 9deab9fcca740ea99da61b7d54700a29c1813e88
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818168"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="155fb-103">polecenie konfiguracji (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="155fb-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="155fb-104">**Dotyczy:** wszystkie &bullet; **obsługiwane wersje**: wszystkie</span><span class="sxs-lookup"><span data-stu-id="155fb-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="155fb-105">Pobiera lub ustawia wartości konfiguracji NuGet.</span><span class="sxs-lookup"><span data-stu-id="155fb-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="155fb-106">Aby uzyskać dodatkowe obciążenie, zobacz [Konfigurowanie zachowania NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="155fb-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="155fb-107">Szczegółowe informacje dotyczące nazwami kluczy, zapoznaj się [odwołania do pliku config NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="155fb-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="155fb-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="155fb-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="155fb-109">gdzie `<name>` i `<value>` określ parę klucz wartość można ustawić w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="155fb-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="155fb-110">Można określić dowolną liczbę par zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="155fb-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="155fb-111">Aby usunąć wartość, określ nazwę i `=` logowania, ale żadnej wartości.</span><span class="sxs-lookup"><span data-stu-id="155fb-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="155fb-112">Dopuszczalne nazw kluczy, zobacz [odwołania do pliku config NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="155fb-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="155fb-113">W NuGet 3.4 + `<value>` można użyć [zmiennych środowiskowych](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="155fb-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="155fb-114">Opcje</span><span class="sxs-lookup"><span data-stu-id="155fb-114">Options</span></span>

| <span data-ttu-id="155fb-115">Opcja</span><span class="sxs-lookup"><span data-stu-id="155fb-115">Option</span></span> | <span data-ttu-id="155fb-116">Opis</span><span class="sxs-lookup"><span data-stu-id="155fb-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="155fb-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="155fb-117">AsPath</span></span> | <span data-ttu-id="155fb-118">Zwraca wartość konfiguracji jako ścieżka, zignorowane, kiedy `-Set` jest używany.</span><span class="sxs-lookup"><span data-stu-id="155fb-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="155fb-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="155fb-119">ConfigFile</span></span> | <span data-ttu-id="155fb-120">Plik konfiguracji NuGet do zmodyfikowania.</span><span class="sxs-lookup"><span data-stu-id="155fb-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="155fb-121">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="155fb-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="155fb-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="155fb-122">ForceEnglishOutput</span></span> | <span data-ttu-id="155fb-123">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="155fb-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="155fb-124">Pomoc</span><span class="sxs-lookup"><span data-stu-id="155fb-124">Help</span></span> | <span data-ttu-id="155fb-125">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="155fb-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="155fb-126">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="155fb-126">NonInteractive</span></span> | <span data-ttu-id="155fb-127">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="155fb-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="155fb-128">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="155fb-128">Verbosity</span></span> | <span data-ttu-id="155fb-129">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="155fb-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="155fb-130">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="155fb-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="155fb-131">Przykłady</span><span class="sxs-lookup"><span data-stu-id="155fb-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
