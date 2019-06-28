---
title: Polecenie konfiguracji interfejsu wiersza polecenia NuGet
description: Dokumentacja dotycząca poleceń konfiguracji nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c0497c7b99a2de6bee37d6d0ead8b055578e60b7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426076"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="bcfbf-103">polecenie config (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="bcfbf-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="bcfbf-104">**Dotyczy:** wszystkich &bullet; **obsługiwane wersje**: wszystkie</span><span class="sxs-lookup"><span data-stu-id="bcfbf-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="bcfbf-105">Pobiera lub ustawia wartości konfiguracji NuGet.</span><span class="sxs-lookup"><span data-stu-id="bcfbf-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="bcfbf-106">Aby uzyskać dodatkowe użycie, zobacz [NuGet typowe konfiguracje](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="bcfbf-106">For additional usage, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="bcfbf-107">Szczegółowe informacje dotyczące dopuszczalny rozmiar nazwy kluczy, można znaleźć [odwołanie do pliku config NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="bcfbf-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="bcfbf-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="bcfbf-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="bcfbf-109">gdzie `<name>` i `<value>` określ parę klucz wartość należy ustawić w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bcfbf-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="bcfbf-110">Można określić dowolną liczbę par zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="bcfbf-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="bcfbf-111">Aby usunąć wartość, określ nazwę i `=` logowania, ale bez wartości.</span><span class="sxs-lookup"><span data-stu-id="bcfbf-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="bcfbf-112">Dopuszczalny rozmiar klucza nazwy opisano w artykule [odwołanie do pliku config NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="bcfbf-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="bcfbf-113">W pakiecie NuGet 3.4 + `<value>` służy [zmienne środowiskowe](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="bcfbf-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="bcfbf-114">Opcje</span><span class="sxs-lookup"><span data-stu-id="bcfbf-114">Options</span></span>

| <span data-ttu-id="bcfbf-115">Opcja</span><span class="sxs-lookup"><span data-stu-id="bcfbf-115">Option</span></span> | <span data-ttu-id="bcfbf-116">Opis</span><span class="sxs-lookup"><span data-stu-id="bcfbf-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bcfbf-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="bcfbf-117">AsPath</span></span> | <span data-ttu-id="bcfbf-118">Zwraca wartość konfiguracji w postaci ścieżki, ignorowane, gdy `-Set` jest używany.</span><span class="sxs-lookup"><span data-stu-id="bcfbf-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="bcfbf-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="bcfbf-119">ConfigFile</span></span> | <span data-ttu-id="bcfbf-120">Plik konfiguracyjny NuGet do zmodyfikowania.</span><span class="sxs-lookup"><span data-stu-id="bcfbf-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="bcfbf-121">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="bcfbf-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="bcfbf-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="bcfbf-122">ForceEnglishOutput</span></span> | <span data-ttu-id="bcfbf-123">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="bcfbf-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="bcfbf-124">Help</span><span class="sxs-lookup"><span data-stu-id="bcfbf-124">Help</span></span> | <span data-ttu-id="bcfbf-125">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="bcfbf-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="bcfbf-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="bcfbf-126">NonInteractive</span></span> | <span data-ttu-id="bcfbf-127">Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="bcfbf-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="bcfbf-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="bcfbf-128">Verbosity</span></span> | <span data-ttu-id="bcfbf-129">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="bcfbf-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="bcfbf-130">Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="bcfbf-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="bcfbf-131">Przykłady</span><span class="sxs-lookup"><span data-stu-id="bcfbf-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
