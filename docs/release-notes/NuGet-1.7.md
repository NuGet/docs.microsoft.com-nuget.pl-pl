---
title: Informacje o wersji 1.7 pakietów NuGet
description: Informacje o wersji programu NuGet 1.7, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 07cd541ef215d2a1bacc45995a22dadb6dfeac6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551470"
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="ad302-103">Informacje o wersji 1.7 pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="ad302-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="ad302-104">[Informacje o wersji NuGet w wersji 1.6](../release-notes/nuget-1.6.md) | [informacjach o wersji NuGet 1.8](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="ad302-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="ad302-105">NuGet 1.7 został wydany 4 kwietnia 2012 r.</span><span class="sxs-lookup"><span data-stu-id="ad302-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="ad302-106">Problem z instalacją znane</span><span class="sxs-lookup"><span data-stu-id="ad302-106">Known Installation Issue</span></span>
<span data-ttu-id="ad302-107">Jeśli używasz programu VS 2010 z dodatkiem SP1, możesz napotkać błąd instalacji podczas próby uaktualnienia NuGet, jeśli masz starszą wersję zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="ad302-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="ad302-108">Obejście polega na po prostu Odinstaluj NuGet, a następnie zainstalować go z galerii rozszerzeń programu VS.</span><span class="sxs-lookup"><span data-stu-id="ad302-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="ad302-109">Zobacz [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="ad302-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="ad302-110">Uwaga: Jeśli program Visual Studio nie pozwalają na odinstalować rozszerzenie (przycisk Odinstaluj jest wyłączony), prawdopodobnie musisz ponownie program Visual Studio za pomocą polecenia "Uruchom jako Administrator".</span><span class="sxs-lookup"><span data-stu-id="ad302-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="ad302-111">Funkcje</span><span class="sxs-lookup"><span data-stu-id="ad302-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="ad302-112">Obsługa otwierania pliku readme.txt po zakończeniu instalacji</span><span class="sxs-lookup"><span data-stu-id="ad302-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="ad302-113">Nowe w wersji 1.7, jeśli pakiet zawiera `readme.txt` pliku w katalogu głównym pakietu NuGet automatycznie otworzyć ten plik, po zakończeniu instalacji pakietu.</span><span class="sxs-lookup"><span data-stu-id="ad302-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="ad302-114">Pokaż pakiety w wersjach wstępnych, w oknie dialogowym pakiety zarządzania pakietami NuGet</span><span class="sxs-lookup"><span data-stu-id="ad302-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="ad302-115">Okno dialogowe Zarządzanie pakietami NuGet teraz zawiera listę rozwijaną, która zapewnia opcję, aby wyświetlać pakiety w wersjach wstępnych.</span><span class="sxs-lookup"><span data-stu-id="ad302-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![Wyświetlanie pakiety w wersjach wstępnych](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="ad302-117">Pokaż przycisk Przywróć pakiet, gdy brakuje plików pakietu</span><span class="sxs-lookup"><span data-stu-id="ad302-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="ad302-118">Po otwarciu konsoli Menedżera pakietów lub pakietów programu Manager NuGet okna dialogowego, NuGet sprawdzi, czy bieżące rozwiązanie ma włączony tryb Przywracanie pakietów, a jeśli brakuje dowolnej pliki pakietu `packages` folderu.</span><span class="sxs-lookup"><span data-stu-id="ad302-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="ad302-119">Jeśli te dwa warunki są spełnione, powiadomi użytkownika i wyświetli wygodne przycisk przywracania NuGet.</span><span class="sxs-lookup"><span data-stu-id="ad302-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="ad302-120">Kliknięcie tego przycisku spowoduje wyzwolenie pakietu NuGet, aby przywrócić wszystkie brakujące pakiety.</span><span class="sxs-lookup"><span data-stu-id="ad302-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![Przycisk przywracania pakietów w oknie dialogowym](./media/packagerestore-dialog.png)

![Przycisk Przywróć pakiet w konsoli](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="ad302-123">Dodawanie pliku packages.config na poziomie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="ad302-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="ad302-124">W poprzednich wersjach programu NuGet, każdy projekt ma `packages.config` pliku, który śledzi informacje o pakietów NuGet, które są zainstalowane w tym projekcie.</span><span class="sxs-lookup"><span data-stu-id="ad302-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="ad302-125">Jednak nie było żadnych podobnych plików na poziomie rozwiązania do śledzenia pakietów poziomie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ad302-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="ad302-126">W rezultacie nie było możliwości można przywrócić pakietów poziomie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ad302-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="ad302-127">Ta funkcja jest teraz implementowane w wersji 1.7 NuGet.</span><span class="sxs-lookup"><span data-stu-id="ad302-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="ad302-128">Poziom rozwiązania `packages.config` plik zostanie umieszczony w obszarze `.nuget` folder, w ramach rozwiązania główny i będzie przechowywać pakiety tylko poziomie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ad302-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="ad302-129">Usuń polecenie New-Package</span><span class="sxs-lookup"><span data-stu-id="ad302-129">Remove New-Package command</span></span>
<span data-ttu-id="ad302-130">Z powodu niskiej użycia polecenia New-Package zostało usunięte.</span><span class="sxs-lookup"><span data-stu-id="ad302-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="ad302-131">Deweloperom zaleca się używać nuget.exe lub przydatną Eksplorator pakietów NuGet do tworzenia pakietów.</span><span class="sxs-lookup"><span data-stu-id="ad302-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="ad302-132">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="ad302-132">Bug Fixes</span></span>
<span data-ttu-id="ad302-133">NuGet 1.7 ma ustaloną wiele błędów wokół scenariuszy kontroli sieci/źródła i przywracanie pakietów przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="ad302-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="ad302-134">Aby uzyskać pełną listę prac elementy rozwiązane w NuGet 1.7, widok [NuGet narzędzie do śledzenia problemów w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="ad302-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
