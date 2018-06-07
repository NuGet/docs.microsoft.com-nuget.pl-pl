---
title: Polecenie specyfikacji interfejsu wiersza polecenia NuGet
description: Informacje dotyczące polecenia specyfikacji nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17d3c5fc083f52fd9ab4a854ad358995bc55293b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817089"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="a5e1b-103">Specyfikacja polecenia (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a5e1b-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="a5e1b-104">**Dotyczy:** pakietu tworzenia &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="a5e1b-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="a5e1b-105">Generuje `.nuspec` plików dla nowego pakietu.</span><span class="sxs-lookup"><span data-stu-id="a5e1b-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="a5e1b-106">Jeśli uruchomione w tym samym folderze co plik projektu (`.csproj`, `.vbproj`, `.fsproj`), `spec` tworzy tokenami `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="a5e1b-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="a5e1b-107">Aby uzyskać dodatkowe informacje, zobacz [utworzenie pakietu](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="a5e1b-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="a5e1b-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="a5e1b-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="a5e1b-109">gdzie `<packageID>` jest identyfikatorem opcjonalny pakiet do zapisania w `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="a5e1b-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="a5e1b-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="a5e1b-110">Options</span></span>

| <span data-ttu-id="a5e1b-111">Opcja</span><span class="sxs-lookup"><span data-stu-id="a5e1b-111">Option</span></span> | <span data-ttu-id="a5e1b-112">Opis</span><span class="sxs-lookup"><span data-stu-id="a5e1b-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a5e1b-113">Zestawu AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="a5e1b-113">AssemblyPath</span></span> | <span data-ttu-id="a5e1b-114">Określa ścieżkę do zestawu do użycia na potrzeby metadanych.</span><span class="sxs-lookup"><span data-stu-id="a5e1b-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="a5e1b-115">Wymuś</span><span class="sxs-lookup"><span data-stu-id="a5e1b-115">Force</span></span> | <span data-ttu-id="a5e1b-116">Zastępuje istniejące `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="a5e1b-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="a5e1b-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a5e1b-117">ForceEnglishOutput</span></span> | <span data-ttu-id="a5e1b-118">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="a5e1b-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a5e1b-119">Pomoc</span><span class="sxs-lookup"><span data-stu-id="a5e1b-119">Help</span></span> | <span data-ttu-id="a5e1b-120">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="a5e1b-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="a5e1b-121">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="a5e1b-121">NonInteractive</span></span> | <span data-ttu-id="a5e1b-122">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="a5e1b-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a5e1b-123">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="a5e1b-123">Verbosity</span></span> | <span data-ttu-id="a5e1b-124">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="a5e1b-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a5e1b-125">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a5e1b-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a5e1b-126">Przykłady</span><span class="sxs-lookup"><span data-stu-id="a5e1b-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
