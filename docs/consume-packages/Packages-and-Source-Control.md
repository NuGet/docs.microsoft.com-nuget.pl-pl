---
title: Pakiety NuGet i kontrola źródła
description: Zagadnienia dotyczące traktowania pakietów NuGet w systemach kontroli wersji i kontroli źródła oraz pomijania pakietów za pomocą usług git i TFVC.
author: JonDouglas
ms.author: jodou
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: fa3ec6992002224c9fb56a53aee9096e6d2c6fbb
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901671"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="d3fcc-103">Pomijanie pakietów NuGet w systemach kontroli źródła</span><span class="sxs-lookup"><span data-stu-id="d3fcc-103">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="d3fcc-104">Deweloperzy zwykle pomijają pakiety NuGet ze swoich [](package-restore.md) repozytoriów kontroli źródła i polegają zamiast tego na przywracaniu pakietów, aby ponownie zainstalować zależności projektu przed kompilacją.</span><span class="sxs-lookup"><span data-stu-id="d3fcc-104">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="d3fcc-105">Powody, dla których można polegać na przywracaniu pakietów, są następujące:</span><span class="sxs-lookup"><span data-stu-id="d3fcc-105">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="d3fcc-106">Rozproszone systemy kontroli wersji, takie jak Git, obejmują pełne kopie każdej wersji każdego pliku w repozytorium.</span><span class="sxs-lookup"><span data-stu-id="d3fcc-106">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="d3fcc-107">Pliki binarne, które są często aktualizowane, prowadzą do znacznej ilości danych i wydłużają czas klonowania repozytorium.</span><span class="sxs-lookup"><span data-stu-id="d3fcc-107">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="d3fcc-108">Gdy pakiety są zawarte w repozytorium, deweloperzy są odpowiedzialne za dodawanie odwołań bezpośrednio do zawartości pakietu na dysku zamiast odwoływać się do pakietów za pośrednictwem narzędzia NuGet, co może prowadzić do zakodowanych nazw ścieżek w projekcie.</span><span class="sxs-lookup"><span data-stu-id="d3fcc-108">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="d3fcc-109">Czyszczenie rozwiązania z nieużywanych folderów pakietów staje się trudniejsze, ponieważ należy upewnić się, że żadne foldery pakietów nie są nadal używane.</span><span class="sxs-lookup"><span data-stu-id="d3fcc-109">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="d3fcc-110">Pominięcie pakietów pozwala zachować czyste granice własności między kodem a pakietami innych, od których zależysz.</span><span class="sxs-lookup"><span data-stu-id="d3fcc-110">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="d3fcc-111">Wiele pakietów NuGet jest już utrzymywanych we własnych repozytoriach kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="d3fcc-111">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="d3fcc-112">Chociaż przywracanie pakietów jest zachowaniem domyślnym w przypadku pakietu NuGet, niektóre działania ręczne są niezbędne do pominięcia pakietów, czyli folderu w projekcie, z kontroli źródła, zgodnie z opisem w &mdash; `packages` tym &mdash; artykule.</span><span class="sxs-lookup"><span data-stu-id="d3fcc-112">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in this article.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="d3fcc-113">Pomijanie pakietów za pomocą usługi Git</span><span class="sxs-lookup"><span data-stu-id="d3fcc-113">Omitting packages with Git</span></span>

<span data-ttu-id="d3fcc-114">Użyj pliku [.gitignore,](https://git-scm.com/docs/gitignore) aby zignorować między innymi pakiety NuGet ( `.nupkg` ), folder i `packages` `project.assets.json` .</span><span class="sxs-lookup"><span data-stu-id="d3fcc-114">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to ignore NuGet packages (`.nupkg`) the `packages` folder, and `project.assets.json`, among other things.</span></span> <span data-ttu-id="d3fcc-115">Aby uzyskać informacje, zobacz [przykład `.gitignore` dla Visual Studio projektów:](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)</span><span class="sxs-lookup"><span data-stu-id="d3fcc-115">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span></span>

<span data-ttu-id="d3fcc-116">Ważne elementy pliku `.gitignore` to:</span><span class="sxs-lookup"><span data-stu-id="d3fcc-116">The important parts of the `.gitignore` file are:</span></span>

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

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="d3fcc-117">Pomijanie pakietów za pomocą Kontrola wersji serwera Team Foundation</span><span class="sxs-lookup"><span data-stu-id="d3fcc-117">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="d3fcc-118">Jeśli to możliwe, postępuj zgodnie z tymi *instrukcjami* przed dodaniem projektu do kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="d3fcc-118">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="d3fcc-119">W przeciwnym razie ręcznie usuń `packages` folder z repozytorium i zaewidencjuj tę zmianę przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="d3fcc-119">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="d3fcc-120">Aby wyłączyć integrację kontroli źródła z programem TFVC dla wybranych plików:</span><span class="sxs-lookup"><span data-stu-id="d3fcc-120">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="d3fcc-121">Utwórz folder o `.nuget` nazwie w folderze rozwiązania (gdzie `.sln` znajduje się plik).</span><span class="sxs-lookup"><span data-stu-id="d3fcc-121">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="d3fcc-122">Porada: w systemie Windows, aby utworzyć ten folder w Eksplorator Windows, użyj nazwy z `.nuget.`  kropką na końcu.</span><span class="sxs-lookup"><span data-stu-id="d3fcc-122">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="d3fcc-123">W tym folderze utwórz plik o nazwie `NuGet.Config` i otwórz go do edycji.</span><span class="sxs-lookup"><span data-stu-id="d3fcc-123">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="d3fcc-124">Dodaj co najmniej następujący tekst, w którym ustawienie [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) Visual Studio pominięcie wszystkiego w `packages` folderze:</span><span class="sxs-lookup"><span data-stu-id="d3fcc-124">Add the following text as a minimum, where the [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="d3fcc-125">Jeśli używasz programu TFS 2010 lub starszego, skłoń `packages` folder w mapowania obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="d3fcc-125">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="d3fcc-126">Na serwerze TFS 2012 lub nowszym lub w Visual Studio Team Services utwórz plik zgodnie z opisem na stronie `.tfignore` Dodawanie plików do [serwera](/vsts/tfvc/add-files-server?view=vsts#tfignore&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="d3fcc-126">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [Add Files to the Server](/vsts/tfvc/add-files-server?view=vsts#tfignore&preserve-view=true).</span></span> <span data-ttu-id="d3fcc-127">W tym pliku dołącz zawartość poniżej, aby jawnie zignorować modyfikacje folderu na poziomie repozytorium i `\packages` kilku innych plików pośrednich.</span><span class="sxs-lookup"><span data-stu-id="d3fcc-127">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="d3fcc-128">(Plik można utworzyć w Eksplorator Windows przy użyciu nazwy a z kropką na końcowej kropce, ale może być konieczne najpierw wyłączenie opcji "Ukryj znane rozszerzenia `.tfignore.` plików"):</span><span class="sxs-lookup"><span data-stu-id="d3fcc-128">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

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

1. <span data-ttu-id="d3fcc-129">Dodaj `NuGet.Config` i do kontroli źródła i `.tfignore` zaewidencjlij zmiany.</span><span class="sxs-lookup"><span data-stu-id="d3fcc-129">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
