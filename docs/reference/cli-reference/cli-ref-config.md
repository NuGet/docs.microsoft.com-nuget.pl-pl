---
title: Polecenie konfiguracji interfejsu wiersza polecenia NuGet
description: Informacje dotyczące polecenia nuget.exe config
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7d0c1c51f40cba9a5b69f209ffbd995451bfeb9f
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622879"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="cc234-103">config — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="cc234-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="cc234-104">**Dotyczy:** wszystkie &bullet; **obsługiwane wersje**: wszystkie</span><span class="sxs-lookup"><span data-stu-id="cc234-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="cc234-105">Pobiera lub ustawia wartości konfiguracji NuGet.</span><span class="sxs-lookup"><span data-stu-id="cc234-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="cc234-106">Aby uzyskać dodatkowe użycie, zobacz [typowe konfiguracje NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="cc234-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="cc234-107">Szczegółowe informacje na temat dozwolonych nazw kluczy można znaleźć w [dokumentacji pliku konfiguracji NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="cc234-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="cc234-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="cc234-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="cc234-109">gdzie `<name>` i `<value>` określić parę klucz-wartość, która ma zostać ustawiona w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="cc234-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="cc234-110">Można określić dowolną liczbę par.</span><span class="sxs-lookup"><span data-stu-id="cc234-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="cc234-111">Aby usunąć wartość, określ nazwę i `=` znak, ale nie wartości.</span><span class="sxs-lookup"><span data-stu-id="cc234-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="cc234-112">Aby uzyskać dozwolone nazwy kluczy, zobacz [Dokumentacja pliku konfiguracji programu NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="cc234-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="cc234-113">W programie NuGet 3.4 + `<value>` można używać [zmiennych środowiskowych](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="cc234-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="cc234-114">Opcje</span><span class="sxs-lookup"><span data-stu-id="cc234-114">Options</span></span>


- **`AsPath`**

  <span data-ttu-id="cc234-115">Zwraca wartość konfiguracji jako ścieżkę, która jest ignorowana, gdy `-Set` jest używana.</span><span class="sxs-lookup"><span data-stu-id="cc234-115">Returns the config value as a path, ignored when `-Set` is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="cc234-116">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="cc234-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="cc234-117">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="cc234-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="cc234-118">*(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.</span><span class="sxs-lookup"><span data-stu-id="cc234-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="cc234-119">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="cc234-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="cc234-120">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cc234-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-Set`**

  <span data-ttu-id="cc234-121">Jeden na więcej par klucz-wartość, które mają być ustawiane w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="cc234-121">One on more key-value pairs to be set in config.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="cc234-122">Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .</span><span class="sxs-lookup"><span data-stu-id="cc234-122">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="cc234-123">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="cc234-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="cc234-124">Przykłady</span><span class="sxs-lookup"><span data-stu-id="cc234-124">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
