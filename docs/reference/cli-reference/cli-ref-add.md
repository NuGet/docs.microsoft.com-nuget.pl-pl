---
title: Polecenie Add interfejsu wiersza polecenia NuGet
description: Odwołanie do nuget.exe Dodaj polecenie
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 89d268946243e8eae07e482db48e809a15260c38
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622905"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="a8845-103">Add — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="a8845-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="a8845-104">**Dotyczy**: &bullet; **obsługiwane wersje**publikowania pakietów: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="a8845-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="a8845-105">Dodaje określony pakiet do źródła pakietów innego niż HTTP (folderu lub ścieżki UNC) w układzie hierarchicznym, w którym foldery są tworzone dla identyfikatora pakietu i numeru wersji.</span><span class="sxs-lookup"><span data-stu-id="a8845-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="a8845-106">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="a8845-106">For example:</span></span>

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

<span data-ttu-id="a8845-107">W przypadku przywracania lub aktualizowania względem źródła pakietu układ hierarchiczny zapewnia znacznie lepszą wydajność.</span><span class="sxs-lookup"><span data-stu-id="a8845-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="a8845-108">Aby rozwinąć wszystkie pliki w pakiecie do źródła pakietu docelowego, użyj `-Expand` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="a8845-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="a8845-109">Zwykle powoduje to dodanie dodatkowych podfolderów w miejscu docelowym, takich jak `tools` i `lib` .</span><span class="sxs-lookup"><span data-stu-id="a8845-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="a8845-110">Użycie</span><span class="sxs-lookup"><span data-stu-id="a8845-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="a8845-111">gdzie `<packagePath>` jest ścieżką do pakietu do dodania i `<sourcePath>` określa źródło pakietu, do którego zostanie dodany pakiet.</span><span class="sxs-lookup"><span data-stu-id="a8845-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="a8845-112">Źródła HTTP nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="a8845-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="a8845-113">Opcje</span><span class="sxs-lookup"><span data-stu-id="a8845-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="a8845-114">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="a8845-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a8845-115">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="a8845-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="a8845-116">Dodaje wszystkie pliki w pakiecie do źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="a8845-116">Adds all the files in the package to the package source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="a8845-117">*(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.</span><span class="sxs-lookup"><span data-stu-id="a8845-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>
<span data-ttu-id="a8845-118">Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.</span><span class="sxs-lookup"><span data-stu-id="a8845-118">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="a8845-119">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="a8845-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="a8845-120">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a8845-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

   <span data-ttu-id="a8845-121">Określa źródło pakietu, które jest folderem lub udziałem UNC, do którego zostanie dodany NUPKG.</span><span class="sxs-lookup"><span data-stu-id="a8845-121">Specifies the package source, which is a folder or UNC share, to which the nupkg will be added.</span></span> <span data-ttu-id="a8845-122">Źródła http nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="a8845-122">Http sources are not supported.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="a8845-123">Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .</span><span class="sxs-lookup"><span data-stu-id="a8845-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="a8845-124">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a8845-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a8845-125">Przykłady</span><span class="sxs-lookup"><span data-stu-id="a8845-125">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
