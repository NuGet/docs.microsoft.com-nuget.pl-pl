---
title: Polecenie specyfikacji interfejsu wiersza polecenia NuGet
description: Dokumentacja polecenia NuGet. exe spec
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328274"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="8efd4-103">Spec — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="8efd4-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="8efd4-104">**Dotyczy:** **obsługiwane wersje** tworzenia &bullet; pakietów: wszystkie</span><span class="sxs-lookup"><span data-stu-id="8efd4-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="8efd4-105">`.nuspec` Generuje plik dla nowego pakietu.</span><span class="sxs-lookup"><span data-stu-id="8efd4-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="8efd4-106">W przypadku uruchomienia w tym samym folderze, w którym znajduje`.csproj`się plik `.fsproj`projektu ( `spec` , `.vbproj`,,) `.nuspec` , program tworzy plik z tokenami.</span><span class="sxs-lookup"><span data-stu-id="8efd4-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="8efd4-107">Aby uzyskać dodatkowe informacje, zobacz [Tworzenie pakietu](../../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="8efd4-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="8efd4-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="8efd4-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="8efd4-109">gdzie `<packageID>` jest opcjonalnym identyfikatorem pakietu, który ma `.nuspec` zostać zapisany w pliku.</span><span class="sxs-lookup"><span data-stu-id="8efd4-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="8efd4-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="8efd4-110">Options</span></span>

| <span data-ttu-id="8efd4-111">Opcja</span><span class="sxs-lookup"><span data-stu-id="8efd4-111">Option</span></span> | <span data-ttu-id="8efd4-112">Opis</span><span class="sxs-lookup"><span data-stu-id="8efd4-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8efd4-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="8efd4-113">AssemblyPath</span></span> | <span data-ttu-id="8efd4-114">Określa ścieżkę do zestawu, który ma być używany dla metadanych.</span><span class="sxs-lookup"><span data-stu-id="8efd4-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="8efd4-115">Moc</span><span class="sxs-lookup"><span data-stu-id="8efd4-115">Force</span></span> | <span data-ttu-id="8efd4-116">Zastępuje istniejący `.nuspec` plik.</span><span class="sxs-lookup"><span data-stu-id="8efd4-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="8efd4-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8efd4-117">ForceEnglishOutput</span></span> | <span data-ttu-id="8efd4-118">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="8efd4-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8efd4-119">Help</span><span class="sxs-lookup"><span data-stu-id="8efd4-119">Help</span></span> | <span data-ttu-id="8efd4-120">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="8efd4-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="8efd4-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="8efd4-121">NonInteractive</span></span> | <span data-ttu-id="8efd4-122">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8efd4-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8efd4-123">Verbosity</span><span class="sxs-lookup"><span data-stu-id="8efd4-123">Verbosity</span></span> | <span data-ttu-id="8efd4-124">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="8efd4-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8efd4-125">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8efd4-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8efd4-126">Przykłady</span><span class="sxs-lookup"><span data-stu-id="8efd4-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
