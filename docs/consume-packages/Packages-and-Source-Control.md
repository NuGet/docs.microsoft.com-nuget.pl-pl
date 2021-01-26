---
title: Pakiety NuGet i kontrola źródła
description: Zagadnienia dotyczące sposobu traktowania pakietów NuGet w systemach kontroli wersji i kontroli źródła oraz jak pominąć pakiety za pomocą usługi git i TFVC.
author: JonDouglas
ms.author: jodou
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 9bae65573ca49c68d07250228c1923890e0f14ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775012"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="42118-103">Pomijanie pakietów NuGet w systemach kontroli źródła</span><span class="sxs-lookup"><span data-stu-id="42118-103">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="42118-104">Deweloperzy zwykle pomijają pakiety NuGet z ich repozytoriów kontroli źródła i polegają na [przywróceniu pakietu](package-restore.md) , aby ponownie zainstalować zależności projektu przed kompilacją.</span><span class="sxs-lookup"><span data-stu-id="42118-104">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="42118-105">Przyczyny związane z przywracaniem pakietu są następujące:</span><span class="sxs-lookup"><span data-stu-id="42118-105">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="42118-106">Rozproszone systemy kontroli wersji, takie jak Git, obejmują pełne kopie każdej wersji każdego pliku w repozytorium.</span><span class="sxs-lookup"><span data-stu-id="42118-106">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="42118-107">Pliki binarne, które są często aktualizowane, powodują znaczące przeładowanie i wydłużą czas klonowania repozytorium.</span><span class="sxs-lookup"><span data-stu-id="42118-107">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="42118-108">Gdy pakiety są zawarte w repozytorium, deweloperzy mogą dodawać odwołania bezpośrednio do zawartości pakietu na dysku, a nie odwołania do pakietów za pomocą NuGet, co może prowadzić do zakodowanych nazw ścieżek w projekcie.</span><span class="sxs-lookup"><span data-stu-id="42118-108">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="42118-109">Nieużywane foldery pakietów staną się trudniejsze do oczyszczenia, co jest konieczne, aby nie usuwać żadnych folderów pakietów, które są nadal używane.</span><span class="sxs-lookup"><span data-stu-id="42118-109">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="42118-110">Pominięcie pakietów spowoduje zachowanie czystych granic własności między kodem a pakietami od innych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="42118-110">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="42118-111">Wiele pakietów NuGet jest już przechowywanych w ich własnych repozytoriach kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="42118-111">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="42118-112">Chociaż przywracanie pakietów jest domyślnym zachowaniem w pakiecie NuGet, niektóre czynności ręczne są niezbędne do pominięcia pakietów &mdash; , czyli `packages` folderu w projekcie &mdash; z kontroli źródła, zgodnie z opisem w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="42118-112">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in this article.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="42118-113">Pomijanie pakietów w usłudze git</span><span class="sxs-lookup"><span data-stu-id="42118-113">Omitting packages with Git</span></span>

<span data-ttu-id="42118-114">Użyj [pliku. gitignore](https://git-scm.com/docs/gitignore) do ignorowania pakietów NuGet ( `.nupkg` ) `packages` folderu i `project.assets.json` , między innymi.</span><span class="sxs-lookup"><span data-stu-id="42118-114">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to ignore NuGet packages (`.nupkg`) the `packages` folder, and `project.assets.json`, among other things.</span></span> <span data-ttu-id="42118-115">Aby uzyskać informacje, zobacz [przykład `.gitignore` dla projektów programu Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span><span class="sxs-lookup"><span data-stu-id="42118-115">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span></span>

<span data-ttu-id="42118-116">Ważne części `.gitignore` pliku są następujące:</span><span class="sxs-lookup"><span data-stu-id="42118-116">The important parts of the `.gitignore` file are:</span></span>

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

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="42118-117">Pomijanie pakietów z Kontrola wersji serwera Team Foundation</span><span class="sxs-lookup"><span data-stu-id="42118-117">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="42118-118">Jeśli to możliwe, wykonaj te instrukcje *przed* dodaniem projektu do kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="42118-118">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="42118-119">W przeciwnym razie ręcznie usuń `packages` folder z repozytorium i Zaewidencjonuj tę zmianę przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="42118-119">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="42118-120">Aby wyłączyć integrację kontroli źródła z TFVC dla wybranych plików:</span><span class="sxs-lookup"><span data-stu-id="42118-120">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="42118-121">Utwórz folder o nazwie `.nuget` w folderze rozwiązania (w którym `.sln` znajduje się plik).</span><span class="sxs-lookup"><span data-stu-id="42118-121">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="42118-122">Porada: w systemie Windows Aby utworzyć ten folder w Eksploratorze Windows, użyj nazwy `.nuget.` *z* kropką końcową.</span><span class="sxs-lookup"><span data-stu-id="42118-122">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="42118-123">W tym folderze Utwórz plik o nazwie `NuGet.Config` i otwórz go do edycji.</span><span class="sxs-lookup"><span data-stu-id="42118-123">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="42118-124">Dodaj następujący tekst jako minimum, gdzie ustawienie [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) instruuje program Visual Studio, aby pominąć wszystkie elementy w `packages` folderze:</span><span class="sxs-lookup"><span data-stu-id="42118-124">Add the following text as a minimum, where the [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="42118-125">Jeśli używasz programu TFS 2010 lub starszego, zamaskowanie `packages` folderu w mapowaniu obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="42118-125">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="42118-126">Na serwerze TFS 2012 lub nowszym lub z Visual Studio Team Services Utwórz `.tfignore` plik zgodnie z opisem w temacie [Dodawanie plików do serwera](/vsts/tfvc/add-files-server?view=vsts#tfignore).</span><span class="sxs-lookup"><span data-stu-id="42118-126">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [Add Files to the Server](/vsts/tfvc/add-files-server?view=vsts#tfignore).</span></span> <span data-ttu-id="42118-127">W tym pliku Uwzględnij poniżej zawartość, aby jawnie zignorować modyfikacje w `\packages` folderze na poziomie repozytorium i kilku innych plikach pośrednich.</span><span class="sxs-lookup"><span data-stu-id="42118-127">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="42118-128">(Można utworzyć plik w Eksploratorze Windows przy użyciu nazwy a `.tfignore.` z kropką końcową, ale może być konieczne wyłączenie najpierw opcji "Ukryj znane rozszerzenia plików"):</span><span class="sxs-lookup"><span data-stu-id="42118-128">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

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

1. <span data-ttu-id="42118-129">Dodaj `NuGet.Config` i `.tfignore` do kontroli źródła i Zaewidencjonuj zmiany.</span><span class="sxs-lookup"><span data-stu-id="42118-129">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
