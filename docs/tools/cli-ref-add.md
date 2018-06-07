---
title: Interfejs wiersza polecenia NuGet Dodaj — polecenie
description: Dodaj odwołanie do nuget.exe — polecenie
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f229ca100463c556f9c4cefc49f52724a9c4ba77
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817613"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="b82b5-103">add command, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="b82b5-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="b82b5-104">**Dotyczy**: publikowanie pakietu &bullet; **obsługiwane wersje**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="b82b5-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="b82b5-105">Dodaje określony pakiet do źródła pakietu protokołu HTTP (folder lub ścieżka UNC) w układzie hierarchicznym, w którym są tworzone foldery numeru identyfikator i wersję pakietu.</span><span class="sxs-lookup"><span data-stu-id="b82b5-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="b82b5-106">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="b82b5-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="b82b5-107">Podczas przywracania lub aktualizowania źródle pakietu, hierarchiczna układ zapewnia znacznie wyższą wydajność.</span><span class="sxs-lookup"><span data-stu-id="b82b5-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="b82b5-108">Aby rozwinąć wszystkie pliki w pakiecie do docelowego źródła pakietu, należy użyć `-Expand` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="b82b5-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="b82b5-109">Zazwyczaj powoduje to dodatkowe podfolderów znajdujących się w lokalizacji docelowej, takie jak `tools` i `lib`.</span><span class="sxs-lookup"><span data-stu-id="b82b5-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="b82b5-110">Użycie</span><span class="sxs-lookup"><span data-stu-id="b82b5-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="b82b5-111">gdzie `<packagePath>` jest ścieżka do pakietu, aby dodać, a `<sourcePath>` określa źródła pakietu na podstawie folderu, do którego zostanie dodany pakiet.</span><span class="sxs-lookup"><span data-stu-id="b82b5-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="b82b5-112">Źródła HTTP nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="b82b5-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="b82b5-113">Opcje</span><span class="sxs-lookup"><span data-stu-id="b82b5-113">Options</span></span>

| <span data-ttu-id="b82b5-114">Opcja</span><span class="sxs-lookup"><span data-stu-id="b82b5-114">Option</span></span> | <span data-ttu-id="b82b5-115">Opis</span><span class="sxs-lookup"><span data-stu-id="b82b5-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b82b5-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b82b5-116">ConfigFile</span></span> | <span data-ttu-id="b82b5-117">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="b82b5-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b82b5-118">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="b82b5-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b82b5-119">Rozwiń węzeł</span><span class="sxs-lookup"><span data-stu-id="b82b5-119">Expand</span></span> | <span data-ttu-id="b82b5-120">Dodaje wszystkie pliki w pakiecie do źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="b82b5-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="b82b5-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b82b5-121">ForceEnglishOutput</span></span> | <span data-ttu-id="b82b5-122">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="b82b5-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b82b5-123">Pomoc</span><span class="sxs-lookup"><span data-stu-id="b82b5-123">Help</span></span> | <span data-ttu-id="b82b5-124">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="b82b5-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="b82b5-125">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="b82b5-125">NonInteractive</span></span> | <span data-ttu-id="b82b5-126">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="b82b5-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b82b5-127">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="b82b5-127">Verbosity</span></span> | <span data-ttu-id="b82b5-128">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="b82b5-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b82b5-129">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b82b5-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b82b5-130">Przykłady</span><span class="sxs-lookup"><span data-stu-id="b82b5-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
