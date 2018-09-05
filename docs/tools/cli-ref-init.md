---
title: Polecenie init interfejs wiersza polecenia NuGet
description: Dokumentacja dotycząca poleceń init nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551413"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="af526-103">polecenie init (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="af526-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="af526-104">**Dotyczy:** Tworzenie pakietu &bullet; **obsługiwane wersje:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="af526-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="af526-105">Kopiuje wszystkie pakiety z prostego folderu do folderu docelowego przy użyciu układzie hierarchicznym, zgodnie z opisem dla [Dodaj polecenie](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="af526-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="af526-106">Oznacza to, za pomocą `init` jest równoważne użyciu `add` polecenie każdego pakietu, w tym folderze.</span><span class="sxs-lookup"><span data-stu-id="af526-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="af526-107">Podobnie jak w przypadku `add`, miejsce docelowe musi być folderem lokalnym lub ścieżką UNC; Repozytoriów pakietów protokołu HTTP, np. nuget.org lub serwery prywatne nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="af526-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="af526-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="af526-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="af526-109">gdzie `<source>` jest folder zawierający pakiety i `<destination>` jest lokalny folder lub ścieżka UNC, do której są kopiowane pakietów.</span><span class="sxs-lookup"><span data-stu-id="af526-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="af526-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="af526-110">Options</span></span>

| <span data-ttu-id="af526-111">Opcja</span><span class="sxs-lookup"><span data-stu-id="af526-111">Option</span></span> | <span data-ttu-id="af526-112">Opis</span><span class="sxs-lookup"><span data-stu-id="af526-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="af526-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="af526-113">ConfigFile</span></span> | <span data-ttu-id="af526-114">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="af526-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="af526-115">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="af526-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="af526-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="af526-116">ForceEnglishOutput</span></span> | <span data-ttu-id="af526-117">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="af526-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="af526-118">Rozwiń węzeł</span><span class="sxs-lookup"><span data-stu-id="af526-118">Expand</span></span> | <span data-ttu-id="af526-119">Dodaje wszystkie pliki w każdym pakiecie, który zostanie dodany do źródła pakietu; taki sam jak `-Expand` z `add` polecenia.</span><span class="sxs-lookup"><span data-stu-id="af526-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="af526-120">Pomoc</span><span class="sxs-lookup"><span data-stu-id="af526-120">Help</span></span> | <span data-ttu-id="af526-121">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="af526-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="af526-122">Nieinterakcyjnym</span><span class="sxs-lookup"><span data-stu-id="af526-122">NonInteractive</span></span> | <span data-ttu-id="af526-123">Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="af526-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="af526-124">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="af526-124">Verbosity</span></span> | <span data-ttu-id="af526-125">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="af526-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="af526-126">Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="af526-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="af526-127">Przykłady</span><span class="sxs-lookup"><span data-stu-id="af526-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
