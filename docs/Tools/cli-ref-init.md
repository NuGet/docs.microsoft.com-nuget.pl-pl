---
title: Polecenie init NuGet interfejsu wiersza polecenia
description: Informacje dotyczące polecenia init nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f5e819d014637d1ebb0403d9d838f9362efb20f0
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="cbc58-103">init polecenia (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="cbc58-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="cbc58-104">**Dotyczy:** pakietu tworzenia &bullet; **obsługiwane wersje:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="cbc58-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="cbc58-105">Kopiuje wszystkie pakiety z płaskim folderu do folderu docelowego przy użyciu układzie hierarchicznym, zgodnie z opisem dla [Dodaj polecenie](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="cbc58-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="cbc58-106">Oznacza to, za pomocą `init` odpowiada za pomocą `add` na każdy pakiet w folderze.</span><span class="sxs-lookup"><span data-stu-id="cbc58-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="cbc58-107">Jak `add`, docelowy musi być folderem lokalnym lub ścieżką UNC; Repozytoriów pakietu HTTP, takie jak nuget.org lub prywatnej serwery nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="cbc58-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="cbc58-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="cbc58-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="cbc58-109">gdzie `<source>` jest folder zawierający pakietów i `<destination>` jest lokalny folder lub ścieżka UNC, do której są kopiowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="cbc58-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="cbc58-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="cbc58-110">Options</span></span>

| <span data-ttu-id="cbc58-111">Opcja</span><span class="sxs-lookup"><span data-stu-id="cbc58-111">Option</span></span> | <span data-ttu-id="cbc58-112">Opis</span><span class="sxs-lookup"><span data-stu-id="cbc58-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cbc58-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="cbc58-113">ConfigFile</span></span> | <span data-ttu-id="cbc58-114">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="cbc58-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="cbc58-115">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="cbc58-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="cbc58-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="cbc58-116">ForceEnglishOutput</span></span> | <span data-ttu-id="cbc58-117">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="cbc58-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="cbc58-118">Rozwiń węzeł</span><span class="sxs-lookup"><span data-stu-id="cbc58-118">Expand</span></span> | <span data-ttu-id="cbc58-119">Dodaje wszystkie pliki w każdym pakiecie, który zostanie dodany do źródła pakietu; taki sam jak `-Expand` z `add` polecenia.</span><span class="sxs-lookup"><span data-stu-id="cbc58-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="cbc58-120">Pomoc</span><span class="sxs-lookup"><span data-stu-id="cbc58-120">Help</span></span> | <span data-ttu-id="cbc58-121">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="cbc58-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="cbc58-122">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="cbc58-122">NonInteractive</span></span> | <span data-ttu-id="cbc58-123">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="cbc58-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="cbc58-124">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="cbc58-124">Verbosity</span></span> | <span data-ttu-id="cbc58-125">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="cbc58-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="cbc58-126">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="cbc58-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="cbc58-127">Przykłady</span><span class="sxs-lookup"><span data-stu-id="cbc58-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
