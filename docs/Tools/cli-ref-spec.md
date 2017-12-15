---
title: Polecenie specyfikacji interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 85611449-87e6-489b-8c6c-fe1d7be76c13
description: "Informacje dotyczące polecenia specyfikacji nuget.exe"
keywords: "Odwołanie specyfikacji nuget, specyfikacji polecenie"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c32b23e66c8eb4db1c8fa6dc615589219c00239f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="3d9c1-104">Specyfikacja polecenia (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3d9c1-104">spec command (NuGet CLI)</span></span>

<span data-ttu-id="3d9c1-105">**Dotyczy:** pakietu tworzenia &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="3d9c1-105">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="3d9c1-106">Generuje `.nuspec` plików dla nowego pakietu.</span><span class="sxs-lookup"><span data-stu-id="3d9c1-106">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="3d9c1-107">Jeśli uruchomione w tym samym folderze co plik projektu (`.csproj`, `.vbproj`, `.fsproj`), `spec` tworzy tokenami `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="3d9c1-107">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="3d9c1-108">Aby uzyskać dodatkowe informacje, zobacz [utworzenie pakietu](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="3d9c1-108">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="3d9c1-109">Użycie</span><span class="sxs-lookup"><span data-stu-id="3d9c1-109">Usage</span></span>

```
nuget spec [<packageID>] [options]
```

<span data-ttu-id="3d9c1-110">gdzie `<packageID>` jest identyfikatorem opcjonalny pakiet do zapisania w `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="3d9c1-110">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="3d9c1-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="3d9c1-111">Options</span></span>

| <span data-ttu-id="3d9c1-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="3d9c1-112">Option</span></span> | <span data-ttu-id="3d9c1-113">Opis</span><span class="sxs-lookup"><span data-stu-id="3d9c1-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3d9c1-114">Zestawu AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="3d9c1-114">AssemblyPath</span></span> | <span data-ttu-id="3d9c1-115">Określa ścieżkę do zestawu do użycia na potrzeby metadanych.</span><span class="sxs-lookup"><span data-stu-id="3d9c1-115">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="3d9c1-116">Wymuś</span><span class="sxs-lookup"><span data-stu-id="3d9c1-116">Force</span></span> | <span data-ttu-id="3d9c1-117">Zastępuje istniejące `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="3d9c1-117">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="3d9c1-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3d9c1-118">ForceEnglishOutput</span></span> | <span data-ttu-id="3d9c1-119">*(3.5 +)*  Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="3d9c1-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3d9c1-120">Pomoc</span><span class="sxs-lookup"><span data-stu-id="3d9c1-120">Help</span></span> | <span data-ttu-id="3d9c1-121">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="3d9c1-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="3d9c1-122">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="3d9c1-122">NonInteractive</span></span> | <span data-ttu-id="3d9c1-123">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="3d9c1-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3d9c1-124">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="3d9c1-124">Verbosity</span></span> | <span data-ttu-id="3d9c1-125">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="3d9c1-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="3d9c1-126">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3d9c1-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3d9c1-127">Przykłady</span><span class="sxs-lookup"><span data-stu-id="3d9c1-127">Examples</span></span>

```
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
