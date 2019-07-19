---
title: Polecenie Add interfejsu wiersza polecenia NuGet
description: Dokumentacja polecenia Add dla NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328361"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="ec539-103">add command, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="ec539-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="ec539-104">**Dotyczy**: **obsługiwane wersje**publikowania &bullet; pakietów: 3.3+</span><span class="sxs-lookup"><span data-stu-id="ec539-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="ec539-105">Dodaje określony pakiet do źródła pakietów innego niż HTTP (folderu lub ścieżki UNC) w układzie hierarchicznym, w którym foldery są tworzone dla identyfikatora pakietu i numeru wersji.</span><span class="sxs-lookup"><span data-stu-id="ec539-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="ec539-106">Przykład:</span><span class="sxs-lookup"><span data-stu-id="ec539-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="ec539-107">W przypadku przywracania lub aktualizowania względem źródła pakietu układ hierarchiczny zapewnia znacznie lepszą wydajność.</span><span class="sxs-lookup"><span data-stu-id="ec539-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="ec539-108">Aby rozwinąć wszystkie pliki w pakiecie do źródła pakietu docelowego, użyj `-Expand` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="ec539-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="ec539-109">Zwykle powoduje to dodanie dodatkowych podfolderów w miejscu docelowym, takich `tools` jak `lib`i.</span><span class="sxs-lookup"><span data-stu-id="ec539-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="ec539-110">Użycie</span><span class="sxs-lookup"><span data-stu-id="ec539-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="ec539-111">gdzie `<packagePath>` jest ścieżką do pakietu do dodania i `<sourcePath>` określa źródło pakietu, do którego zostanie dodany pakiet.</span><span class="sxs-lookup"><span data-stu-id="ec539-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="ec539-112">Źródła HTTP nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="ec539-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="ec539-113">Opcje</span><span class="sxs-lookup"><span data-stu-id="ec539-113">Options</span></span>

| <span data-ttu-id="ec539-114">Opcja</span><span class="sxs-lookup"><span data-stu-id="ec539-114">Option</span></span> | <span data-ttu-id="ec539-115">Opis</span><span class="sxs-lookup"><span data-stu-id="ec539-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ec539-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ec539-116">ConfigFile</span></span> | <span data-ttu-id="ec539-117">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="ec539-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ec539-118">Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="ec539-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="ec539-119">Expand</span><span class="sxs-lookup"><span data-stu-id="ec539-119">Expand</span></span> | <span data-ttu-id="ec539-120">Dodaje wszystkie pliki w pakiecie do źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="ec539-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="ec539-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ec539-121">ForceEnglishOutput</span></span> | <span data-ttu-id="ec539-122">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="ec539-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ec539-123">Help</span><span class="sxs-lookup"><span data-stu-id="ec539-123">Help</span></span> | <span data-ttu-id="ec539-124">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="ec539-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="ec539-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="ec539-125">NonInteractive</span></span> | <span data-ttu-id="ec539-126">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ec539-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ec539-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="ec539-127">Verbosity</span></span> | <span data-ttu-id="ec539-128">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="ec539-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="ec539-129">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ec539-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ec539-130">Przykłady</span><span class="sxs-lookup"><span data-stu-id="ec539-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
