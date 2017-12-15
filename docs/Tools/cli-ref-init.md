---
title: Polecenie init interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d413e4f3-1b41-4a92-8df8-87d21b542bd3
description: "Informacje dotyczące polecenia init nuget.exe"
keywords: "Odwołanie init nuget, init, polecenie"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f63a3cbcca1aeff02995f23afd217c76e534b3be
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="a2f3a-104">init polecenia (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a2f3a-104">init command (NuGet CLI)</span></span>

<span data-ttu-id="a2f3a-105">**Dotyczy:** pakietu tworzenia &bullet; **obsługiwane wersje:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="a2f3a-105">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="a2f3a-106">Kopiuje wszystkie pakiety z płaskim folderu do folderu docelowego przy użyciu układzie hierarchicznym, zgodnie z opisem dla [Dodaj polecenie](#add) powyżej.</span><span class="sxs-lookup"><span data-stu-id="a2f3a-106">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](#add) above.</span></span> <span data-ttu-id="a2f3a-107">Oznacza to, za pomocą `init` odpowiada za pomocą `add` na każdy pakiet w folderze.</span><span class="sxs-lookup"><span data-stu-id="a2f3a-107">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="a2f3a-108">Jak `add`, docelowy musi być folderem lokalnym lub ścieżką UNC; Repozytoriów pakietu HTTP, takie jak nuget.org lub prywatnej serwery nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="a2f3a-108">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="a2f3a-109">Użycie</span><span class="sxs-lookup"><span data-stu-id="a2f3a-109">Usage</span></span>

```
nuget init <source> <destination> [options]
```

<span data-ttu-id="a2f3a-110">gdzie `<source>` jest folder zawierający pakietów i `<destination>` jest folder lokalny lub nazwa ścieżki UNC, do którego zostaną skopiowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="a2f3a-110">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages will be copied.</span></span>

## <a name="options"></a><span data-ttu-id="a2f3a-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="a2f3a-111">Options</span></span>

| <span data-ttu-id="a2f3a-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="a2f3a-112">Option</span></span> | <span data-ttu-id="a2f3a-113">Opis</span><span class="sxs-lookup"><span data-stu-id="a2f3a-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a2f3a-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a2f3a-114">ConfigFile</span></span> | <span data-ttu-id="a2f3a-115">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="a2f3a-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a2f3a-116">Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany.</span><span class="sxs-lookup"><span data-stu-id="a2f3a-116">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="a2f3a-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a2f3a-117">ForceEnglishOutput</span></span> | <span data-ttu-id="a2f3a-118">*(3.5 +)*  Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="a2f3a-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a2f3a-119">Rozwiń węzeł</span><span class="sxs-lookup"><span data-stu-id="a2f3a-119">Expand</span></span> | <span data-ttu-id="a2f3a-120">Dodaje wszystkie pliki w każdym pakiecie, który zostanie dodany do źródła pakietu; taki sam jak `-Expand` z `add` polecenia.</span><span class="sxs-lookup"><span data-stu-id="a2f3a-120">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="a2f3a-121">Pomoc</span><span class="sxs-lookup"><span data-stu-id="a2f3a-121">Help</span></span> | <span data-ttu-id="a2f3a-122">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="a2f3a-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="a2f3a-123">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="a2f3a-123">NonInteractive</span></span> | <span data-ttu-id="a2f3a-124">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="a2f3a-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a2f3a-125">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="a2f3a-125">Verbosity</span></span> | <span data-ttu-id="a2f3a-126">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="a2f3a-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="a2f3a-127">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a2f3a-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a2f3a-128">Przykłady</span><span class="sxs-lookup"><span data-stu-id="a2f3a-128">Examples</span></span>

```
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
