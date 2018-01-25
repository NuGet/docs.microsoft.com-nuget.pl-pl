---
title: "Pakiety NuGet i kontroli źródła | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Zagadnienia dotyczące sposobu traktowania pakietów NuGet w ramach systemów kontroli źródła i kontroli wersji oraz sposób Pomiń pakiety z usługi git i TFVC."
keywords: "Repozytoria kontrolę NuGet do kontroli źródła, NuGet kontroli wersji, NuGet i git, NuGet i TFS, NuGet i TFVC, pomijając pakietów, repozytoria kontroli źródła, wersja"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 274492f2b1d05c781dadaab70cdc7d281549d002
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="c7f2e-104">Pominięcie pakietów NuGet w systemów kontroli źródła</span><span class="sxs-lookup"><span data-stu-id="c7f2e-104">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="c7f2e-105">Deweloperzy zazwyczaj Pomiń pakietów NuGet z ich repozytoria kontroli źródła i zamiast tego zależne [Przywracanie pakietów](../consume-packages/package-restore.md) ponowna instalacja zależności projektu przed kompilacji.</span><span class="sxs-lookup"><span data-stu-id="c7f2e-105">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](../consume-packages/package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="c7f2e-106">Dostępne są następujące przyczyny polegania na Przywracanie pakietu:</span><span class="sxs-lookup"><span data-stu-id="c7f2e-106">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="c7f2e-107">Systemów kontroli wersji rozproszonej, np. Git, obejmują pełne kopie każdej wersji wszystkich plików w repozytorium.</span><span class="sxs-lookup"><span data-stu-id="c7f2e-107">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="c7f2e-108">Pliki binarne, które są często aktualizowane, prowadzić do znaczących rozrostu i powoduje nieznaczne wydłużenie czasu, potrzebnego do klonowania repozytorium.</span><span class="sxs-lookup"><span data-stu-id="c7f2e-108">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="c7f2e-109">Gdy pakiety są zawarte w repozytorium, deweloperzy mogą dodać odwołań bezpośrednio do zawartości pakietu na dysku, a nie odwołujący się pakiety za pośrednictwem pakietu NuGet, co może prowadzić do nazwy ścieżek ustalony w projekcie.</span><span class="sxs-lookup"><span data-stu-id="c7f2e-109">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="c7f2e-110">Staje się on trudniejsze do czyszczenia rozwiązania do pakietu nieużywanych folderów, jak należy upewnić się, że nie usuwaj pakietu foldery nadal w użyciu.</span><span class="sxs-lookup"><span data-stu-id="c7f2e-110">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="c7f2e-111">Pomijając pakietów, możesz zachować między kodu i pakiety od innych, zależnych od czystą granice własności.</span><span class="sxs-lookup"><span data-stu-id="c7f2e-111">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="c7f2e-112">Wiele pakietów NuGet są już obsługiwane w ich własnych repozytoria kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="c7f2e-112">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="c7f2e-113">Mimo że Przywracanie pakietu nuget zachowanie domyślne, niektóre czynności ręcznych jest niezbędne pominąć pakiety&mdash;mianowicie `packages` folder w projekcie&mdash;z kontroli źródła, zgodnie z opisem w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="c7f2e-113">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in the following sections.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="c7f2e-114">Pominięcie pakietów za pomocą narzędzia Git</span><span class="sxs-lookup"><span data-stu-id="c7f2e-114">Omitting packages with Git</span></span>

<span data-ttu-id="c7f2e-115">Użyj [pliku .gitignore](https://git-scm.com/docs/gitignore) Aby uniknąć, włączając `packages` folderem w kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="c7f2e-115">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to avoid including the `packages` folder in source control.</span></span> <span data-ttu-id="c7f2e-116">Aby informacje, zobacz [próbki `.gitignore` dla projektów programu Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="c7f2e-116">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="c7f2e-117">Ważne części `.gitignore` plików są:</span><span class="sxs-lookup"><span data-stu-id="c7f2e-117">The important parts of the `.gitignore` file are:</span></span>

```gitignore
# Ignore NuGet Packages
*.nupkg

# Ignore the packages folder
**/packages/*

# Include packages/build/, which is used as an MSBuild target
!**/packages/build/

# Uncomment if necessary; generally it's regenerated when needed
#!**/packages/repositories.config

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json; project.assets.json is used in conjunction with the PackageReference format.
project.lock.json
project.assets.json
*.nuget.props
```

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="c7f2e-118">Pominięcie pakiety z Team Foundation Version Control</span><span class="sxs-lookup"><span data-stu-id="c7f2e-118">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="c7f2e-119">Jeśli to możliwe, wykonaj następujące instrukcje *przed* Dodawanie projektu do kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="c7f2e-119">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="c7f2e-120">W przeciwnym razie Usuń ręcznie `packages` folder z repozytorium i wyboru w tej zmiany przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="c7f2e-120">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="c7f2e-121">Aby wyłączyć integracji kontroli źródła z TFVC dla wybranych plików:</span><span class="sxs-lookup"><span data-stu-id="c7f2e-121">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="c7f2e-122">Utwórz folder o nazwie `.nuget` w folderze rozwiązania (gdzie `.sln` pliku).</span><span class="sxs-lookup"><span data-stu-id="c7f2e-122">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="c7f2e-123">Porada: w systemie Windows, aby utworzyć ten folder w Eksploratorze Windows, należy użyć nazwy `.nuget.` *z* końcową kropkę.</span><span class="sxs-lookup"><span data-stu-id="c7f2e-123">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="c7f2e-124">W tym folderze utwórz plik o nazwie `NuGet.Config` i otworzyć do edycji.</span><span class="sxs-lookup"><span data-stu-id="c7f2e-124">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="c7f2e-125">Dodaj poniższy tekst jako minimum, gdzie [disableSourceControlIntegration](../Schema/nuget-config-file.md#solution-section) ustawienie powoduje, że Visual Studio, aby pominąć wszystkie elementy `packages` folderu:</span><span class="sxs-lookup"><span data-stu-id="c7f2e-125">Add the following text as a minimum, where the [disableSourceControlIntegration](../Schema/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="c7f2e-126">Jeśli używasz programu TFS 2010 lub starszy, zamaskować `packages` folderu w mapowania obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="c7f2e-126">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="c7f2e-127">Na TFS 2012 lub nowszym, lub z programu Visual Studio Team Services, utworzyć `.tfignore` plików zgodnie z opisem na [AddFiles na serwerze](https://www.visualstudio.com/en-us/docs/tfvc/add-files-server#tfignore).</span><span class="sxs-lookup"><span data-stu-id="c7f2e-127">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [AddFiles to the Server](https://www.visualstudio.com/en-us/docs/tfvc/add-files-server#tfignore).</span></span> <span data-ttu-id="c7f2e-128">W tym pliku, należy uwzględnić zawartość poniżej, aby jawnie Ignoruj modyfikacje `\packages` folderu na poziomie repozytorium i kilka innych plików pośrednich.</span><span class="sxs-lookup"><span data-stu-id="c7f2e-128">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="c7f2e-129">(Należy utworzyć plik w Eksploratorze Windows, przy użyciu nazwy `.tfignore.` końcową kropkę, ale może należy wyłączyć "Ukryj znanego rozszerzenia" opcja najpierw.):</span><span class="sxs-lookup"><span data-stu-id="c7f2e-129">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Include package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. <span data-ttu-id="c7f2e-130">Dodaj `NuGet.Config` i `.tfignore` do kontroli źródła i zaewidencjonować zmiany.</span><span class="sxs-lookup"><span data-stu-id="c7f2e-130">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
