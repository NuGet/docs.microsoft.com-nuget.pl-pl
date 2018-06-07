---
title: Polecenie init NuGet interfejsu wiersza polecenia
description: Informacje dotyczące polecenia init nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4fda33aabd51fbbf0e5559baaa42af065366ba4
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817821"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="a02b7-103">init polecenia (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a02b7-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="a02b7-104">**Dotyczy:** pakietu tworzenia &bullet; **obsługiwane wersje:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="a02b7-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="a02b7-105">Kopiuje wszystkie pakiety z płaskim folderu do folderu docelowego przy użyciu układzie hierarchicznym, zgodnie z opisem dla [Dodaj polecenie](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="a02b7-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="a02b7-106">Oznacza to, za pomocą `init` odpowiada za pomocą `add` na każdy pakiet w folderze.</span><span class="sxs-lookup"><span data-stu-id="a02b7-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="a02b7-107">Jak `add`, docelowy musi być folderem lokalnym lub ścieżką UNC; Repozytoriów pakietu HTTP, takie jak nuget.org lub prywatnej serwery nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="a02b7-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="a02b7-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="a02b7-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="a02b7-109">gdzie `<source>` jest folder zawierający pakietów i `<destination>` jest lokalny folder lub ścieżka UNC, do której są kopiowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="a02b7-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="a02b7-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="a02b7-110">Options</span></span>

| <span data-ttu-id="a02b7-111">Opcja</span><span class="sxs-lookup"><span data-stu-id="a02b7-111">Option</span></span> | <span data-ttu-id="a02b7-112">Opis</span><span class="sxs-lookup"><span data-stu-id="a02b7-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a02b7-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a02b7-113">ConfigFile</span></span> | <span data-ttu-id="a02b7-114">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="a02b7-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a02b7-115">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="a02b7-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="a02b7-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a02b7-116">ForceEnglishOutput</span></span> | <span data-ttu-id="a02b7-117">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="a02b7-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a02b7-118">Rozwiń węzeł</span><span class="sxs-lookup"><span data-stu-id="a02b7-118">Expand</span></span> | <span data-ttu-id="a02b7-119">Dodaje wszystkie pliki w każdym pakiecie, który zostanie dodany do źródła pakietu; taki sam jak `-Expand` z `add` polecenia.</span><span class="sxs-lookup"><span data-stu-id="a02b7-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="a02b7-120">Pomoc</span><span class="sxs-lookup"><span data-stu-id="a02b7-120">Help</span></span> | <span data-ttu-id="a02b7-121">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="a02b7-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="a02b7-122">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="a02b7-122">NonInteractive</span></span> | <span data-ttu-id="a02b7-123">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="a02b7-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a02b7-124">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="a02b7-124">Verbosity</span></span> | <span data-ttu-id="a02b7-125">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="a02b7-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a02b7-126">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a02b7-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a02b7-127">Przykłady</span><span class="sxs-lookup"><span data-stu-id="a02b7-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
