---
title: Polecenie specyfikacji interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Informacje dotyczące polecenia specyfikacji nuget.exe"
keywords: "Odwołanie specyfikacji nuget, specyfikacji polecenie"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cc7e772e737a0f74929d13e2b126f7796b6d0dc7
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/02/2018
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="d380f-104">Specyfikacja polecenia (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d380f-104">spec command (NuGet CLI)</span></span>

<span data-ttu-id="d380f-105">**Dotyczy:** pakietu tworzenia &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="d380f-105">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d380f-106">Generuje `.nuspec` plików dla nowego pakietu.</span><span class="sxs-lookup"><span data-stu-id="d380f-106">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="d380f-107">Jeśli uruchomione w tym samym folderze co plik projektu (`.csproj`, `.vbproj`, `.fsproj`), `spec` tworzy tokenami `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="d380f-107">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="d380f-108">Aby uzyskać dodatkowe informacje, zobacz [utworzenie pakietu](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="d380f-108">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="d380f-109">Użycie</span><span class="sxs-lookup"><span data-stu-id="d380f-109">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="d380f-110">gdzie `<packageID>` jest identyfikatorem opcjonalny pakiet do zapisania w `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="d380f-110">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="d380f-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="d380f-111">Options</span></span>

| <span data-ttu-id="d380f-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="d380f-112">Option</span></span> | <span data-ttu-id="d380f-113">Opis</span><span class="sxs-lookup"><span data-stu-id="d380f-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d380f-114">Zestawu AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="d380f-114">AssemblyPath</span></span> | <span data-ttu-id="d380f-115">Określa ścieżkę do zestawu do użycia na potrzeby metadanych.</span><span class="sxs-lookup"><span data-stu-id="d380f-115">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="d380f-116">Wymuś</span><span class="sxs-lookup"><span data-stu-id="d380f-116">Force</span></span> | <span data-ttu-id="d380f-117">Zastępuje istniejące `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="d380f-117">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="d380f-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d380f-118">ForceEnglishOutput</span></span> | <span data-ttu-id="d380f-119">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="d380f-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d380f-120">Pomoc</span><span class="sxs-lookup"><span data-stu-id="d380f-120">Help</span></span> | <span data-ttu-id="d380f-121">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="d380f-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="d380f-122">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="d380f-122">NonInteractive</span></span> | <span data-ttu-id="d380f-123">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="d380f-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d380f-124">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="d380f-124">Verbosity</span></span> | <span data-ttu-id="d380f-125">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="d380f-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d380f-126">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d380f-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d380f-127">Przykłady</span><span class="sxs-lookup"><span data-stu-id="d380f-127">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
