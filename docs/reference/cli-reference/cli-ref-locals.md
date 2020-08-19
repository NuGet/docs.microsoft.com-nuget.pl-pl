---
title: Polecenie locale interfejsu wiersza polecenia NuGet
description: Informacje dotyczące nuget.exe lokalnych polecenia
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: cdc2b760021ffc4a9e02edacb45beac01cc99bf1
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623061"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="47b5b-103">locale — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="47b5b-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="47b5b-104">**Dotyczy:** &bullet; **obsługiwane wersje pakietów:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="47b5b-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="47b5b-105">Czyści lub wyświetla lokalne zasoby NuGet, takie jak folder *http pamięci podręcznej*, *pakiety globalne* i folder tymczasowy.</span><span class="sxs-lookup"><span data-stu-id="47b5b-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="47b5b-106">`locals`Można również użyć polecenia, aby wyświetlić listę tych lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="47b5b-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="47b5b-107">Aby uzyskać więcej informacji, zobacz [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="47b5b-107">For more information, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="47b5b-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="47b5b-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="47b5b-109">gdzie `<folder>` jest jedną z `all` , `http-cache` , `packages-cache` *(3,5 i wcześniejszą)*, `global-packages` , `temp` *(3.4 +)* i `plugins-cache` *(4.8 +)*.</span><span class="sxs-lookup"><span data-stu-id="47b5b-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="47b5b-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="47b5b-110">Options</span></span>

- **`-Clear`**

  <span data-ttu-id="47b5b-111">Czyści określony folder.</span><span class="sxs-lookup"><span data-stu-id="47b5b-111">Clears the specified folder.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="47b5b-112">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="47b5b-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="47b5b-113">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="47b5b-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="47b5b-114">*(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.</span><span class="sxs-lookup"><span data-stu-id="47b5b-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="47b5b-115">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="47b5b-115">Displays help information for the command.</span></span>

- **`-List`**

  <span data-ttu-id="47b5b-116">Wyświetla lokalizację określonego folderu lub lokalizacje wszystkich folderów, jeśli są używane ze *wszystkimi*.</span><span class="sxs-lookup"><span data-stu-id="47b5b-116">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="47b5b-117">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="47b5b-117">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="47b5b-118">Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .</span><span class="sxs-lookup"><span data-stu-id="47b5b-118">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="47b5b-119">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="47b5b-119">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="47b5b-120">Przykłady</span><span class="sxs-lookup"><span data-stu-id="47b5b-120">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="47b5b-121">Aby uzyskać więcej przykładów, zobacz [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="47b5b-121">For additional examples, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
