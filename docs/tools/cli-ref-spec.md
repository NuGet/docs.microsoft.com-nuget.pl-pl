---
title: Polecenie specyfikacji interfejsu wiersza polecenia NuGet
description: Dokumentacja dotycząca poleceń specyfikacji nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: cd1dc66676898e2be1c64698886a5ba29a07f88f
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794154"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="53e5c-103">Specyfikacja polecenia (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="53e5c-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="53e5c-104">**Dotyczy:** Tworzenie pakietu &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="53e5c-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="53e5c-105">Generuje `.nuspec` pliku dla nowego pakietu.</span><span class="sxs-lookup"><span data-stu-id="53e5c-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="53e5c-106">Jeśli w tym samym folderze co plik projektu (`.csproj`, `.vbproj`, `.fsproj`), `spec` tworzy tokenami `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="53e5c-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="53e5c-107">Aby uzyskać więcej informacji, zobacz [Tworzenie pakietu](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="53e5c-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="53e5c-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="53e5c-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="53e5c-109">gdzie `<packageID>` jest identyfikatorem pakietu opcjonalnego można zapisać w `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="53e5c-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="53e5c-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="53e5c-110">Options</span></span>

| <span data-ttu-id="53e5c-111">Opcja</span><span class="sxs-lookup"><span data-stu-id="53e5c-111">Option</span></span> | <span data-ttu-id="53e5c-112">Opis</span><span class="sxs-lookup"><span data-stu-id="53e5c-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="53e5c-113">Ścieżkazestawu</span><span class="sxs-lookup"><span data-stu-id="53e5c-113">AssemblyPath</span></span> | <span data-ttu-id="53e5c-114">Określa ścieżkę do zestawu do użycia dla metadanych.</span><span class="sxs-lookup"><span data-stu-id="53e5c-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="53e5c-115">Wymuś</span><span class="sxs-lookup"><span data-stu-id="53e5c-115">Force</span></span> | <span data-ttu-id="53e5c-116">Powoduje zastąpienie wszystkich istniejących `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="53e5c-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="53e5c-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="53e5c-117">ForceEnglishOutput</span></span> | <span data-ttu-id="53e5c-118">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="53e5c-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="53e5c-119">Pomoc</span><span class="sxs-lookup"><span data-stu-id="53e5c-119">Help</span></span> | <span data-ttu-id="53e5c-120">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="53e5c-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="53e5c-121">Nieinterakcyjnym</span><span class="sxs-lookup"><span data-stu-id="53e5c-121">NonInteractive</span></span> | <span data-ttu-id="53e5c-122">Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="53e5c-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="53e5c-123">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="53e5c-123">Verbosity</span></span> | <span data-ttu-id="53e5c-124">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="53e5c-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="53e5c-125">Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="53e5c-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="53e5c-126">Przykłady</span><span class="sxs-lookup"><span data-stu-id="53e5c-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
