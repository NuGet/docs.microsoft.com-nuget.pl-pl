---
title: Informacje o wersji NuGet 2.2 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 25389d8c-e7db-4920-ab5e-cff20cebee7e
description: "Informacje o wersji dla tym znanych problemów, poprawki, dodatkowe funkcje i dcr 2.2 NuGet."
keywords: NuGet 2.2 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 1f6080e01777431c4dfb2278db167bd3bc9a67ea
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="f4403-104">Informacje o wersji 2,2 NuGet</span><span class="sxs-lookup"><span data-stu-id="f4403-104">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="f4403-105">[Informacje o wersji NuGet 2.1](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 informacje o wersji](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="f4403-105">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="f4403-106">NuGet 2.2 został wydany 12 grudnia 2012.</span><span class="sxs-lookup"><span data-stu-id="f4403-106">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="f4403-107">Szybkie uruchamianie programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f4403-107">Visual Studio Quick Launch</span></span>
<span data-ttu-id="f4403-108">Jedną z nowych funkcji, które dodano w programie Visual Studio 2012 został [okno dialogowe Szybkie uruchamianie](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="f4403-108">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="f4403-109">NuGet 2.2 rozszerza tego okna dialogowego, dzięki któremu można zainicjować okno dialogowe menedżera pakietu z warunkami wyszukiwania w szybkie uruchamianie.</span><span class="sxs-lookup"><span data-stu-id="f4403-109">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="f4403-110">Na przykład wprowadź "jquery" Szybkie uruchamianie teraz zawiera opcję w wynikach wyszukiwania dopasowania "jquery" pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="f4403-110">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![NuGet w szybkiego uruchamiania programu Visual Studio](./media/quick-launch.png)

<span data-ttu-id="f4403-112">Wybranie tej opcji spowoduje uruchomienie NuGet pakietu Menedżera wyszukiwania standardowo terminu "jquery".</span><span class="sxs-lookup"><span data-stu-id="f4403-112">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Okno dialogowe Menedżera pakietów NuGet wstępnie wypełnione](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="f4403-114">Określ cały Folder zawartości pakietu</span><span class="sxs-lookup"><span data-stu-id="f4403-114">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="f4403-115">NuGet 2.2 można teraz określić cały folder w `<file>` elementu `.nuspec` pliku, aby uwzględnić wszystkie zawartość tego folderu.</span><span class="sxs-lookup"><span data-stu-id="f4403-115">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="f4403-116">Na przykład następujące spowoduje, że wszystkie skrypty w folderze skryptów pakietu do dodania do folderu contents\scripts podczas instalowania pakietu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="f4403-116">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="f4403-117">**Zaktualizuj 6/24/16: puste foldery w folderze "zawartość" są ignorowane, podczas instalowania pakietu.**</span><span class="sxs-lookup"><span data-stu-id="f4403-117">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="f4403-118">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="f4403-118">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="f4403-119">Instalacja pakietu nie powiedzie się dla projektów języka F # przy użyciu konsoli Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="f4403-119">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="f4403-120">Podczas próby zainstalowania pakietu NuGet w projekcie F # za pomocą konsoli Menedżera pakietów, jest zgłaszany wyjątku InvalidOperationException.</span><span class="sxs-lookup"><span data-stu-id="f4403-120">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="f4403-121">Obecnie pracujemy z team F #, aby rozwiązać ten problem, ale do tego czasu jest obejście można zainstalować pakietów NuGet do projektów F # za pomocą okna dialogowego Menedżera pakietów NuGet, a nie w konsoli programu.</span><span class="sxs-lookup"><span data-stu-id="f4403-121">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="f4403-122">[Więcej informacji znajduje się w witrynie CodePlex](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="f4403-122">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="f4403-123">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="f4403-123">Bug Fixes</span></span>
<span data-ttu-id="f4403-124">NuGet 2.2 zawiera wiele poprawek usterek.</span><span class="sxs-lookup"><span data-stu-id="f4403-124">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="f4403-125">Pełną listę prac elementów usunięto w wersji NuGet 2.2, sprawdź widok [NuGet Tracker problem w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="f4403-125">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
