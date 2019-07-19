---
title: Polecenie konfiguracji interfejsu wiersza polecenia NuGet
description: Dokumentacja polecenia NuGet. exe config
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 51c4c9937483e7f8a57356515c06a60c0f9e6f62
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328358"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="0812b-103">config — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="0812b-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="0812b-104">**Dotyczy:** wszystkie &bullet; **obsługiwane wersje**: wszystkie</span><span class="sxs-lookup"><span data-stu-id="0812b-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="0812b-105">Pobiera lub ustawia wartości konfiguracji NuGet.</span><span class="sxs-lookup"><span data-stu-id="0812b-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="0812b-106">Aby uzyskać dodatkowe użycie, zobacz [typowe konfiguracje NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="0812b-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="0812b-107">Szczegółowe informacje na temat dozwolonych nazw kluczy można znaleźć w [dokumentacji pliku konfiguracji NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="0812b-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="0812b-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="0812b-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="0812b-109">gdzie `<name>` i`<value>` określić parę klucz-wartość, która ma zostać ustawiona w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0812b-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="0812b-110">Można określić dowolną liczbę par.</span><span class="sxs-lookup"><span data-stu-id="0812b-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="0812b-111">Aby usunąć wartość, określ nazwę i `=` znak, ale nie wartości.</span><span class="sxs-lookup"><span data-stu-id="0812b-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="0812b-112">Aby uzyskać dozwolone nazwy kluczy, zobacz [Dokumentacja pliku konfiguracji programu NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="0812b-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="0812b-113">W programie NuGet 3.4 + `<value>` można używać [zmiennych środowiskowych](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="0812b-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="0812b-114">Opcje</span><span class="sxs-lookup"><span data-stu-id="0812b-114">Options</span></span>

| <span data-ttu-id="0812b-115">Opcja</span><span class="sxs-lookup"><span data-stu-id="0812b-115">Option</span></span> | <span data-ttu-id="0812b-116">Opis</span><span class="sxs-lookup"><span data-stu-id="0812b-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0812b-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="0812b-117">AsPath</span></span> | <span data-ttu-id="0812b-118">Zwraca wartość konfiguracji jako ścieżkę, która jest ignorowana `-Set` , gdy jest używana.</span><span class="sxs-lookup"><span data-stu-id="0812b-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="0812b-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="0812b-119">ConfigFile</span></span> | <span data-ttu-id="0812b-120">Plik konfiguracji NuGet do zmodyfikowania.</span><span class="sxs-lookup"><span data-stu-id="0812b-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="0812b-121">Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="0812b-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="0812b-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="0812b-122">ForceEnglishOutput</span></span> | <span data-ttu-id="0812b-123">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="0812b-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="0812b-124">Help</span><span class="sxs-lookup"><span data-stu-id="0812b-124">Help</span></span> | <span data-ttu-id="0812b-125">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="0812b-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="0812b-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="0812b-126">NonInteractive</span></span> | <span data-ttu-id="0812b-127">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0812b-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="0812b-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="0812b-128">Verbosity</span></span> | <span data-ttu-id="0812b-129">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="0812b-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="0812b-130">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="0812b-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="0812b-131">Przykłady</span><span class="sxs-lookup"><span data-stu-id="0812b-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
