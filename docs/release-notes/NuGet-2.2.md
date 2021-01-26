---
title: Informacje o wersji narzędzia NuGet 2,2
description: Informacje o wersji programu NuGet 2,2, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780431"
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="fb255-103">Informacje o wersji narzędzia NuGet 2,2</span><span class="sxs-lookup"><span data-stu-id="fb255-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="fb255-104">Informacje o wersji narzędzia [NuGet 2,1](../release-notes/nuget-2.1.md)  |  [Informacje o wersji pakietu NuGet 2.2.1](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="fb255-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="fb255-105">Pakiet NuGet 2,2 został opublikowany 12 grudnia 2012.</span><span class="sxs-lookup"><span data-stu-id="fb255-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="fb255-106">Szybkie uruchamianie programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fb255-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="fb255-107">Jedną z nowych funkcji, które zostały dodane w programie Visual Studio 2012, jest [okno dialogowe szybkiego uruchamiania](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="fb255-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="fb255-108">Program NuGet 2,2 rozszerza to okno dialogowe, umożliwiając mu zainicjowanie okna dialogowego Menedżera pakietów z warunkami wyszukiwania wprowadzonymi w ramach szybkiego uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="fb255-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="fb255-109">Na przykład wprowadzenie "jQuery" w szybkim uruchomieniu zawiera teraz opcję w wynikach wyszukiwania pakietów NuGet pasujących do "jQuery".</span><span class="sxs-lookup"><span data-stu-id="fb255-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![Pakiet NuGet w programie Visual Studio — Szybki Start](./media/quick-launch.png)

<span data-ttu-id="fb255-111">Wybranie tej opcji spowoduje uruchomienie standardowego środowiska wyszukiwania Menedżera pakietów NuGet dla terminu "jQuery".</span><span class="sxs-lookup"><span data-stu-id="fb255-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Wstępnie wypełnione okno dialogowe Menedżera pakietów NuGet](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="fb255-113">Określ cały folder dla zawartości pakietu</span><span class="sxs-lookup"><span data-stu-id="fb255-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="fb255-114">Pakiet NuGet 2,2 umożliwia teraz określenie całego folderu w `<file>` elemencie `.nuspec` pliku w celu uwzględnienia całej zawartości tego folderu.</span><span class="sxs-lookup"><span data-stu-id="fb255-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="fb255-115">Na przykład poniższe elementy spowodują dodanie wszystkich skryptów w folderze skryptów pakietu do folderu contents\scripts, gdy pakiet zostanie zainstalowany w projekcie.</span><span class="sxs-lookup"><span data-stu-id="fb255-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="fb255-116">**Aktualizacja 6/24/16: puste foldery w folderze "Content" są ignorowane podczas instalacji pakietu.**</span><span class="sxs-lookup"><span data-stu-id="fb255-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="fb255-117">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="fb255-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="fb255-118">Instalacja pakietu kończy się niepowodzeniem dla projektów języka F # w przypadku korzystania z konsoli Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="fb255-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="fb255-119">Podczas próby zainstalowania pakietu NuGet w projekcie języka F # przy użyciu konsoli Menedżera pakietów jest zgłaszany InvalidOperationException.</span><span class="sxs-lookup"><span data-stu-id="fb255-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="fb255-120">Aktywnie pracujemy z zespołem F # w celu rozwiązania problemu, ale w międzyczasie obejście polega na zainstalowaniu pakietów NuGet w projektach języka F # za pośrednictwem okna dialogowego Menedżera pakietów NuGet, a nie konsoli programu.</span><span class="sxs-lookup"><span data-stu-id="fb255-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="fb255-121">[Więcej informacji można znaleźć w witrynie CodePlex](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="fb255-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="fb255-122">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="fb255-122">Bug Fixes</span></span>
<span data-ttu-id="fb255-123">Pakiet NuGet 2,2 zawiera wiele poprawek błędów.</span><span class="sxs-lookup"><span data-stu-id="fb255-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="fb255-124">Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 2,2, zobacz [Śledzenie problemów NuGet dla tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="fb255-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
