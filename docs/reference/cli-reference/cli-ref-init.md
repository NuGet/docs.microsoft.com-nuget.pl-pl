---
title: Polecenie init interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia init programu NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328337"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="aa127-103">init — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="aa127-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="aa127-104">**Dotyczy:** **obsługiwane wersje** tworzenia &bullet; pakietów: 3.3+</span><span class="sxs-lookup"><span data-stu-id="aa127-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="aa127-105">Kopiuje wszystkie pakiety z folderu płaskiego do folderu docelowego przy użyciu układu hierarchicznego zgodnie z opisem dla [polecenia Dodaj](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="aa127-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="aa127-106">Oznacza to, że `init` użycie jest równoważne `add` użyciu polecenia w każdym pakiecie w folderze.</span><span class="sxs-lookup"><span data-stu-id="aa127-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="aa127-107">Tak jak `add`w przypadku, miejsce docelowe musi być folderem lokalnym lub ścieżką UNC; Repozytoria pakietów HTTP, takie jak nuget.org lub serwery prywatne, nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="aa127-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="aa127-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="aa127-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="aa127-109">gdzie `<source>` folder zawiera pakiety i `<destination>` jest folderem lokalnym lub ścieżką UNC, do której są kopiowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="aa127-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="aa127-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="aa127-110">Options</span></span>

| <span data-ttu-id="aa127-111">Opcja</span><span class="sxs-lookup"><span data-stu-id="aa127-111">Option</span></span> | <span data-ttu-id="aa127-112">Opis</span><span class="sxs-lookup"><span data-stu-id="aa127-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="aa127-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="aa127-113">ConfigFile</span></span> | <span data-ttu-id="aa127-114">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="aa127-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="aa127-115">Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="aa127-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="aa127-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="aa127-116">ForceEnglishOutput</span></span> | <span data-ttu-id="aa127-117">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="aa127-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="aa127-118">Expand</span><span class="sxs-lookup"><span data-stu-id="aa127-118">Expand</span></span> | <span data-ttu-id="aa127-119">Dodaje wszystkie pliki w każdym pakiecie, które są dodawane do źródła pakietu; Analogicznie `-Expand` jak `add` polecenie.</span><span class="sxs-lookup"><span data-stu-id="aa127-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="aa127-120">Help</span><span class="sxs-lookup"><span data-stu-id="aa127-120">Help</span></span> | <span data-ttu-id="aa127-121">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="aa127-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="aa127-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="aa127-122">NonInteractive</span></span> | <span data-ttu-id="aa127-123">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="aa127-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="aa127-124">Verbosity</span><span class="sxs-lookup"><span data-stu-id="aa127-124">Verbosity</span></span> | <span data-ttu-id="aa127-125">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="aa127-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="aa127-126">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="aa127-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="aa127-127">Przykłady</span><span class="sxs-lookup"><span data-stu-id="aa127-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
