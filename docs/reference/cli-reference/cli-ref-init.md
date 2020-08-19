---
title: Polecenie init interfejsu wiersza polecenia NuGet
description: Odwołanie do nuget.exe polecenia init
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3b830d678a473c917b70bd46900bdb0206d3652e
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623087"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="a367f-103">init — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="a367f-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="a367f-104">**Dotyczy:** &bullet; **obsługiwane wersje:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="a367f-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="a367f-105">Kopiuje wszystkie pakiety z folderu płaskiego do folderu docelowego przy użyciu układu hierarchicznego zgodnie z opisem dla [polecenia Dodaj](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="a367f-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="a367f-106">Oznacza to, że użycie `init` jest równoważne użyciu `add` polecenia w każdym pakiecie w folderze.</span><span class="sxs-lookup"><span data-stu-id="a367f-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="a367f-107">Tak jak w przypadku `add` , miejsce docelowe musi być folderem lokalnym lub ścieżką UNC; Repozytoria pakietów HTTP, takie jak nuget.org lub serwery prywatne, nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="a367f-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="a367f-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="a367f-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="a367f-109">gdzie `<source>` folder zawiera pakiety i `<destination>` jest folderem lokalnym lub ŚCIEŻKą UNC, do której są kopiowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="a367f-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="a367f-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="a367f-110">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="a367f-111">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="a367f-111">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a367f-112">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="a367f-112">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="a367f-113">Dodaje wszystkie pliki w każdym pakiecie, które są dodawane do źródła pakietu; Analogicznie jak `-Expand` `add` polecenie.</span><span class="sxs-lookup"><span data-stu-id="a367f-113">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="a367f-114">*(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.</span><span class="sxs-lookup"><span data-stu-id="a367f-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="a367f-115">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="a367f-115">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="a367f-116">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a367f-116">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="a367f-117">Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .</span><span class="sxs-lookup"><span data-stu-id="a367f-117">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="a367f-118">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a367f-118">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a367f-119">Przykłady</span><span class="sxs-lookup"><span data-stu-id="a367f-119">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
