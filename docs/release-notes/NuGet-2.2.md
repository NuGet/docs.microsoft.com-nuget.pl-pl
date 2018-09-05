---
title: Informacje o wersji 2,2 NuGet
description: Informacje o wersji programu NuGet 2.2, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a968ced3c58b7187a8bd9a8b14baa92f61f0140f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545995"
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="b83c5-103">Informacje o wersji 2,2 NuGet</span><span class="sxs-lookup"><span data-stu-id="b83c5-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="b83c5-104">[Informacje o wersji NuGet 2.1](../release-notes/nuget-2.1.md) | [informacjach o wersji NuGet 2.2.1](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="b83c5-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="b83c5-105">NuGet 2.2 został wydany 12 grudnia 2012.</span><span class="sxs-lookup"><span data-stu-id="b83c5-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="b83c5-106">Visual Studio Quick Launch</span><span class="sxs-lookup"><span data-stu-id="b83c5-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="b83c5-107">Jedną z nowych funkcji, które zostało dodane w programie Visual Studio 2012 [okno dialogowe Szybkie uruchamianie](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="b83c5-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="b83c5-108">NuGet 2.2 rozszerza to okno dialogowe, dzięki któremu zainicjować okno dialogowe Menedżer pakietów z wyszukiwane terminy wprowadzane w obszarze szybkiego uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="b83c5-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="b83c5-109">Na przykład wprowadzenie "jquery" w szybkie uruchamianie teraz obejmuje opcję w wynikach wyszukiwania pakietów NuGet dopasowania "jquery".</span><span class="sxs-lookup"><span data-stu-id="b83c5-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![NuGet w szybkiego uruchamiania programu Visual Studio](./media/quick-launch.png)

<span data-ttu-id="b83c5-111">Wybranie tej opcji spowoduje uruchomienie standardowego NuGet pakietu Menedżera środowisko wyszukiwania dla terminu "jquery".</span><span class="sxs-lookup"><span data-stu-id="b83c5-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Okno Menedżera pakietów NuGet wstępnie wypełnione](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="b83c5-113">Określ cały Folder zawartości pakietu</span><span class="sxs-lookup"><span data-stu-id="b83c5-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="b83c5-114">NuGet 2.2 umożliwia teraz określenie całego folderu w `<file>` elementu `.nuspec` pliku, aby uwzględnić wszystkie zawartość tego folderu.</span><span class="sxs-lookup"><span data-stu-id="b83c5-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="b83c5-115">Na przykład poniżej spowoduje, że wszystkie skrypty w folderze skrypty pakietu mają zostać dodane do folderu contents\scripts, po zainstalowaniu pakietu do projektu.</span><span class="sxs-lookup"><span data-stu-id="b83c5-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="b83c5-116">**Aktualizuj 6/24/16: puste foldery w folderze "treści" są ignorowane, podczas instalowania pakietu.**</span><span class="sxs-lookup"><span data-stu-id="b83c5-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="b83c5-117">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="b83c5-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="b83c5-118">Instalacja pakietu nie powiedzie się projekty języka F # przy użyciu konsoli Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="b83c5-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="b83c5-119">Podczas próby zainstalowania pakietu NuGet w projekcie programu F # za pomocą konsoli Menedżera pakietów, jest zgłaszany InvalidOperationException.</span><span class="sxs-lookup"><span data-stu-id="b83c5-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="b83c5-120">Aktywnie współpracujemy z zespołu F #, aby rozwiązać ten problem, ale w międzyczasie, obejście polega na instalowanie pakietów NuGet w projektach F # za pomocą okno dialogowe Menedżer pakietów NuGet, a nie w konsoli.</span><span class="sxs-lookup"><span data-stu-id="b83c5-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="b83c5-121">[Więcej informacji znajduje się w witrynie CodePlex](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="b83c5-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="b83c5-122">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="b83c5-122">Bug Fixes</span></span>
<span data-ttu-id="b83c5-123">NuGet 2.2 obejmuje wiele poprawek błędów.</span><span class="sxs-lookup"><span data-stu-id="b83c5-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="b83c5-124">Pełną listę prac elementy rozwiązane w NuGet 2.2, widok [NuGet narzędzie do śledzenia problemów w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="b83c5-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
