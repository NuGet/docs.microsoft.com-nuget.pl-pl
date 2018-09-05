---
title: Polecenie specyfikacji interfejsu wiersza polecenia NuGet
description: Dokumentacja dotycząca poleceń specyfikacji nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68b165751ab6794d2a01d7e466619b1ce4d7ed72
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546452"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="8d619-103">Specyfikacja polecenia (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="8d619-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="8d619-104">**Dotyczy:** Tworzenie pakietu &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="8d619-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="8d619-105">Generuje `.nuspec` pliku dla nowego pakietu.</span><span class="sxs-lookup"><span data-stu-id="8d619-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="8d619-106">Jeśli w tym samym folderze co plik projektu (`.csproj`, `.vbproj`, `.fsproj`), `spec` tworzy tokenami `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="8d619-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="8d619-107">Aby uzyskać więcej informacji, zobacz [Tworzenie pakietu](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="8d619-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="8d619-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="8d619-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="8d619-109">gdzie `<packageID>` jest identyfikatorem pakietu opcjonalnego można zapisać w `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="8d619-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="8d619-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="8d619-110">Options</span></span>

| <span data-ttu-id="8d619-111">Opcja</span><span class="sxs-lookup"><span data-stu-id="8d619-111">Option</span></span> | <span data-ttu-id="8d619-112">Opis</span><span class="sxs-lookup"><span data-stu-id="8d619-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8d619-113">Ścieżkazestawu</span><span class="sxs-lookup"><span data-stu-id="8d619-113">AssemblyPath</span></span> | <span data-ttu-id="8d619-114">Określa ścieżkę do zestawu do użycia dla metadanych.</span><span class="sxs-lookup"><span data-stu-id="8d619-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="8d619-115">Wymuś</span><span class="sxs-lookup"><span data-stu-id="8d619-115">Force</span></span> | <span data-ttu-id="8d619-116">Powoduje zastąpienie wszystkich istniejących `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="8d619-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="8d619-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8d619-117">ForceEnglishOutput</span></span> | <span data-ttu-id="8d619-118">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="8d619-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8d619-119">Pomoc</span><span class="sxs-lookup"><span data-stu-id="8d619-119">Help</span></span> | <span data-ttu-id="8d619-120">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="8d619-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="8d619-121">Nieinterakcyjnym</span><span class="sxs-lookup"><span data-stu-id="8d619-121">NonInteractive</span></span> | <span data-ttu-id="8d619-122">Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="8d619-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8d619-123">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="8d619-123">Verbosity</span></span> | <span data-ttu-id="8d619-124">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="8d619-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8d619-125">Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8d619-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8d619-126">Przykłady</span><span class="sxs-lookup"><span data-stu-id="8d619-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
