---
title: Interfejs wiersza polecenia NuGet Dodaj polecenie | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Dodaj odwołanie do nuget.exe — polecenie
keywords: Dodaj odwołanie nuget, należy dodać polecenie pakietu
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 48e093cbae2cecb1652e17a9b26920107aa8aef7
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="5472d-104">Dodawanie polecenia (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5472d-104">add command (NuGet CLI)</span></span>

<span data-ttu-id="5472d-105">**Dotyczy**: publikowanie pakietu &bullet; **obsługiwane wersje**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="5472d-105">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="5472d-106">Dodaje określony pakiet do źródła pakietu protokołu HTTP (folder lub ścieżka UNC) w układzie hierarchicznym, w którym są tworzone foldery numeru identyfikator i wersję pakietu.</span><span class="sxs-lookup"><span data-stu-id="5472d-106">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="5472d-107">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="5472d-107">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="5472d-108">Podczas przywracania lub aktualizowania źródle pakietu, hierarchiczna układ zapewnia znacznie wyższą wydajność.</span><span class="sxs-lookup"><span data-stu-id="5472d-108">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="5472d-109">Aby rozwinąć wszystkie pliki w pakiecie do docelowego źródła pakietu, należy użyć `-Expand` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="5472d-109">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="5472d-110">Zazwyczaj powoduje to dodatkowe podfolderów znajdujących się w lokalizacji docelowej, takie jak `tools` i `lib`.</span><span class="sxs-lookup"><span data-stu-id="5472d-110">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="5472d-111">Użycie</span><span class="sxs-lookup"><span data-stu-id="5472d-111">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="5472d-112">gdzie `<packagePath>` jest ścieżka do pakietu, aby dodać, a `<sourcePath>` określa źródła pakietu na podstawie folderu, do którego zostanie dodany pakiet.</span><span class="sxs-lookup"><span data-stu-id="5472d-112">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="5472d-113">Źródła HTTP nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="5472d-113">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="5472d-114">Opcje</span><span class="sxs-lookup"><span data-stu-id="5472d-114">Options</span></span>

| <span data-ttu-id="5472d-115">Opcja</span><span class="sxs-lookup"><span data-stu-id="5472d-115">Option</span></span> | <span data-ttu-id="5472d-116">Opis</span><span class="sxs-lookup"><span data-stu-id="5472d-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5472d-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5472d-117">ConfigFile</span></span> | <span data-ttu-id="5472d-118">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="5472d-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5472d-119">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="5472d-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5472d-120">Rozwiń węzeł</span><span class="sxs-lookup"><span data-stu-id="5472d-120">Expand</span></span> | <span data-ttu-id="5472d-121">Dodaje wszystkie pliki w pakiecie do źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="5472d-121">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="5472d-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5472d-122">ForceEnglishOutput</span></span> | <span data-ttu-id="5472d-123">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="5472d-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5472d-124">Pomoc</span><span class="sxs-lookup"><span data-stu-id="5472d-124">Help</span></span> | <span data-ttu-id="5472d-125">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="5472d-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="5472d-126">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="5472d-126">NonInteractive</span></span> | <span data-ttu-id="5472d-127">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="5472d-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5472d-128">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="5472d-128">Verbosity</span></span> | <span data-ttu-id="5472d-129">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="5472d-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="5472d-130">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5472d-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5472d-131">Przykłady</span><span class="sxs-lookup"><span data-stu-id="5472d-131">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
