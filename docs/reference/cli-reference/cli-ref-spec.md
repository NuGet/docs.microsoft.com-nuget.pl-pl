---
title: Polecenie specyfikacji interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia nuget.exe spec
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17603fa30a75c7906f867c96c5d77f31732eaa59
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622567"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="0eef0-103">Spec — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="0eef0-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="0eef0-104">**Dotyczy:** &bullet; **obsługiwane wersje** tworzenia pakietów: wszystkie</span><span class="sxs-lookup"><span data-stu-id="0eef0-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="0eef0-105">Generuje `.nuspec` plik dla nowego pakietu.</span><span class="sxs-lookup"><span data-stu-id="0eef0-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="0eef0-106">W przypadku uruchomienia w tym samym folderze, w którym znajduje się plik projektu ( `.csproj` , `.vbproj` ,, `.fsproj` ), program `spec` tworzy plik z tokenami `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="0eef0-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="0eef0-107">Aby uzyskać dodatkowe informacje, zobacz [Tworzenie pakietu](../../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="0eef0-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="0eef0-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="0eef0-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="0eef0-109">gdzie `<packageID>` jest opcjonalnym identyfikatorem pakietu, który ma zostać zapisany w `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="0eef0-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="0eef0-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="0eef0-110">Options</span></span>

- **`-AssemblyPath`**

  <span data-ttu-id="0eef0-111">Określa ścieżkę do zestawu, który ma być używany dla metadanych.</span><span class="sxs-lookup"><span data-stu-id="0eef0-111">Specifies the path to the assembly to use for metadata.</span></span>

- **`-Force`**

  <span data-ttu-id="0eef0-112">Zastępuje istniejący `.nuspec` plik.</span><span class="sxs-lookup"><span data-stu-id="0eef0-112">Overwrites any existing `.nuspec` file.</span></span>


- **`-ForceEnglishOutput`**

  <span data-ttu-id="0eef0-113">*(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.</span><span class="sxs-lookup"><span data-stu-id="0eef0-113">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="0eef0-114">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="0eef0-114">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="0eef0-115">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0eef0-115">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="0eef0-116">Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .</span><span class="sxs-lookup"><span data-stu-id="0eef0-116">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="0eef0-117">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="0eef0-117">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="0eef0-118">Przykłady</span><span class="sxs-lookup"><span data-stu-id="0eef0-118">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
