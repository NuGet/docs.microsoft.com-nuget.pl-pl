---
title: Polecenie init interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Informacje dotyczące polecenia init nuget.exe
keywords: Odwołanie init nuget, init, polecenie
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 01a3553622020b5868e33ece09cd7555cb712fd3
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="08ae4-104">init polecenia (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="08ae4-104">init command (NuGet CLI)</span></span>

<span data-ttu-id="08ae4-105">**Dotyczy:** pakietu tworzenia &bullet; **obsługiwane wersje:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="08ae4-105">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="08ae4-106">Kopiuje wszystkie pakiety z płaskim folderu do folderu docelowego przy użyciu układzie hierarchicznym, zgodnie z opisem dla [Dodaj polecenie](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="08ae4-106">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="08ae4-107">Oznacza to, za pomocą `init` odpowiada za pomocą `add` na każdy pakiet w folderze.</span><span class="sxs-lookup"><span data-stu-id="08ae4-107">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="08ae4-108">Jak `add`, docelowy musi być folderem lokalnym lub ścieżką UNC; Repozytoriów pakietu HTTP, takie jak nuget.org lub prywatnej serwery nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="08ae4-108">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="08ae4-109">Użycie</span><span class="sxs-lookup"><span data-stu-id="08ae4-109">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="08ae4-110">gdzie `<source>` jest folder zawierający pakietów i `<destination>` jest lokalny folder lub ścieżka UNC, do której są kopiowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="08ae4-110">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="08ae4-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="08ae4-111">Options</span></span>

| <span data-ttu-id="08ae4-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="08ae4-112">Option</span></span> | <span data-ttu-id="08ae4-113">Opis</span><span class="sxs-lookup"><span data-stu-id="08ae4-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="08ae4-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="08ae4-114">ConfigFile</span></span> | <span data-ttu-id="08ae4-115">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="08ae4-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="08ae4-116">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="08ae4-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="08ae4-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="08ae4-117">ForceEnglishOutput</span></span> | <span data-ttu-id="08ae4-118">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="08ae4-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="08ae4-119">Rozwiń węzeł</span><span class="sxs-lookup"><span data-stu-id="08ae4-119">Expand</span></span> | <span data-ttu-id="08ae4-120">Dodaje wszystkie pliki w każdym pakiecie, który zostanie dodany do źródła pakietu; taki sam jak `-Expand` z `add` polecenia.</span><span class="sxs-lookup"><span data-stu-id="08ae4-120">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="08ae4-121">Pomoc</span><span class="sxs-lookup"><span data-stu-id="08ae4-121">Help</span></span> | <span data-ttu-id="08ae4-122">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="08ae4-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="08ae4-123">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="08ae4-123">NonInteractive</span></span> | <span data-ttu-id="08ae4-124">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="08ae4-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="08ae4-125">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="08ae4-125">Verbosity</span></span> | <span data-ttu-id="08ae4-126">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="08ae4-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="08ae4-127">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="08ae4-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="08ae4-128">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08ae4-128">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
