---
title: Pakiety NuGet i kontrola źródła
description: Zagadnienia dotyczące sposobu leczenia pakietów NuGet w ramach kontroli wersji i systemów kontroli źródła oraz sposobu pominięcia pakietów z git i TFVC.
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 9d9ea10ccd32bb65ad0d62b591f5e2cb58ea3427
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "69019978"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="a57da-103">Pomijanie pakietów NuGet w systemach kontroli źródła</span><span class="sxs-lookup"><span data-stu-id="a57da-103">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="a57da-104">Deweloperzy zazwyczaj pominąć pakiety NuGet z ich repozytoriów kontroli źródła i zamiast tego polegać na [przywracanie pakietu,](package-restore.md) aby ponownie zainstalować zależności projektu przed kompilacją.</span><span class="sxs-lookup"><span data-stu-id="a57da-104">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="a57da-105">Powody, dla których warto polegać na przywracaniu pakietu, są następujące:</span><span class="sxs-lookup"><span data-stu-id="a57da-105">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="a57da-106">Rozproszone systemy kontroli wersji, takie jak Git, zawierają pełne kopie każdej wersji każdego pliku w repozytorium.</span><span class="sxs-lookup"><span data-stu-id="a57da-106">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="a57da-107">Pliki binarne, które są często aktualizowane prowadzić do znacznego uwędzić i wydłuża czas potrzebny do sklonowania repozytorium.</span><span class="sxs-lookup"><span data-stu-id="a57da-107">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="a57da-108">Gdy pakiety są zawarte w repozytorium, deweloperzy są umienia dodać odwołania bezpośrednio do zawartości pakietu na dysku, a nie odwoływanie się do pakietów za pośrednictwem NuGet, co może prowadzić do zakodowanych nazw ścieżek w projekcie.</span><span class="sxs-lookup"><span data-stu-id="a57da-108">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="a57da-109">Staje się trudniejsze do czyszczenia rozwiązania nieużywanych folderów pakietu, jak trzeba upewnić się, że nie usuwać żadnych folderów pakietu nadal w użyciu.</span><span class="sxs-lookup"><span data-stu-id="a57da-109">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="a57da-110">Pomijając pakiety, należy zachować czyste granice własności między kodem a pakietami od innych, od których zależy.</span><span class="sxs-lookup"><span data-stu-id="a57da-110">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="a57da-111">Wiele pakietów NuGet są już obsługiwane we własnych repozytoriach kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="a57da-111">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="a57da-112">Chociaż przywracanie pakietu jest domyślnym zachowaniem z NuGet,&mdash;niektóre ręczne prace są niezbędne do pominięcia pakietów, a mianowicie `packages` folder w projekcie&mdash;z kontroli źródła, zgodnie z opisem w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="a57da-112">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in this article.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="a57da-113">Pomijanie pakietów z Git</span><span class="sxs-lookup"><span data-stu-id="a57da-113">Omitting packages with Git</span></span>

<span data-ttu-id="a57da-114">Użyj [pliku gitignore,](https://git-scm.com/docs/gitignore) aby zignorować`.nupkg`pakiety NuGet ( ) `packages` folder i `project.assets.json`, między innymi.</span><span class="sxs-lookup"><span data-stu-id="a57da-114">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to ignore NuGet packages (`.nupkg`) the `packages` folder, and `project.assets.json`, among other things.</span></span> <span data-ttu-id="a57da-115">Aby uzyskać odwołanie, zobacz [przykład dla `.gitignore` projektów programu Visual Studio:](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)</span><span class="sxs-lookup"><span data-stu-id="a57da-115">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span></span>

<span data-ttu-id="a57da-116">Ważnymi częściami `.gitignore` pliku są:</span><span class="sxs-lookup"><span data-stu-id="a57da-116">The important parts of the `.gitignore` file are:</span></span>

```gitignore
# Ignore NuGet Packages
*.nupkg

# The packages folder can be ignored because of Package Restore
**/[Pp]ackages/*

# except build/, which is used as an MSBuild target.
!**/[Pp]ackages/build/

# Uncomment if necessary however generally it will be regenerated when needed
#!**/[Pp]ackages/repositories.config

# NuGet v3's project.json files produces more ignorable files
*.nuget.props
*.nuget.targets

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json (NuGet v3); project.assets.json is used in conjunction with the PackageReference
# format (NuGet v4 and .NET Core).
project.lock.json
project.assets.json
```

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="a57da-117">Pomijanie pakietów z kontrolą wersji Team Foundation</span><span class="sxs-lookup"><span data-stu-id="a57da-117">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="a57da-118">Postępuj zgodnie z tymi instrukcjami, jeśli to możliwe *przed* dodaniem projektu do kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="a57da-118">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="a57da-119">W przeciwnym razie `packages` ręcznie usuń folder z repozytorium i zaewidencjonuj tę zmianę przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="a57da-119">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="a57da-120">Aby wyłączyć integrację kontroli źródła z TFVC dla wybranych plików:</span><span class="sxs-lookup"><span data-stu-id="a57da-120">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="a57da-121">Utwórz folder `.nuget` wywoływany w folderze rozwiązania (w którym znajduje się `.sln` plik).</span><span class="sxs-lookup"><span data-stu-id="a57da-121">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="a57da-122">Wskazówka: w systemie Windows, aby utworzyć ten `.nuget.` folder w Eksploratorze Windows, użyj nazwy *z* końcową kropką.</span><span class="sxs-lookup"><span data-stu-id="a57da-122">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="a57da-123">W tym folderze utwórz plik o nazwie `NuGet.Config` i otwórz go do edycji.</span><span class="sxs-lookup"><span data-stu-id="a57da-123">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="a57da-124">Dodaj następujący tekst jako minimum, gdzie [ustawienie disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) nakazuje programowi Visual Studio pominąć wszystko w folderze: `packages`</span><span class="sxs-lookup"><span data-stu-id="a57da-124">Add the following text as a minimum, where the [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="a57da-125">Jeśli używasz TFS 2010 lub wcześniej, zamaskuj `packages` folder w mapowaniach obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="a57da-125">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="a57da-126">W programie TFS 2012 lub nowszym lub `.tfignore` w programie Visual Studio Team Services należy utworzyć plik zgodnie z opisem w programie [Dodaj pliki do serwera](/vsts/tfvc/add-files-server?view=vsts#tfignore).</span><span class="sxs-lookup"><span data-stu-id="a57da-126">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [Add Files to the Server](/vsts/tfvc/add-files-server?view=vsts#tfignore).</span></span> <span data-ttu-id="a57da-127">W tym pliku dołącz poniższą zawartość, aby `\packages` jawnie zignorować modyfikacje folderu na poziomie repozytorium i kilku innych plików pośrednich.</span><span class="sxs-lookup"><span data-stu-id="a57da-127">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="a57da-128">(Plik można utworzyć w Eksploratorze `.tfignore.` Windows przy użyciu nazwy a z końcową kropką, ale może być konieczne wyłączenie opcji "Ukryj znane rozszerzenia plików".</span><span class="sxs-lookup"><span data-stu-id="a57da-128">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. <span data-ttu-id="a57da-129">Dodaj `NuGet.Config` `.tfignore` i do kontroli źródła i zaewidencjonuj zmiany.</span><span class="sxs-lookup"><span data-stu-id="a57da-129">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
