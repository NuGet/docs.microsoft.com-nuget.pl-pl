---
title: Informacje o wersji 1,7 NuGet
description: Informacje o wersji dla tym znanych problemów, poprawki, dodatkowe funkcje i dcr 1.7 NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 81db81642ac21b7dd41f5940dfba919d0871ec01
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="40ac3-103">Informacje o wersji 1,7 NuGet</span><span class="sxs-lookup"><span data-stu-id="40ac3-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="40ac3-104">[Informacje o wersji NuGet w wersji 1.6](../release-notes/nuget-1.6.md) | [NuGet 1.8 informacje o wersji](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="40ac3-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="40ac3-105">NuGet 1.7 został wydany 4 kwietnia 2012.</span><span class="sxs-lookup"><span data-stu-id="40ac3-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="40ac3-106">Znane problem</span><span class="sxs-lookup"><span data-stu-id="40ac3-106">Known Installation Issue</span></span>
<span data-ttu-id="40ac3-107">Jeśli korzystasz z VS 2010 z dodatkiem SP1, możesz napotkać błąd instalacji podczas próby uaktualnienia NuGet, jeśli masz starszą wersję zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="40ac3-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="40ac3-108">Obejście jest po prostu odinstalować NuGet, a następnie zainstaluj go z galerii rozszerzeń programu VS.</span><span class="sxs-lookup"><span data-stu-id="40ac3-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="40ac3-109">Zobacz [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="40ac3-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="40ac3-110">Uwaga: Jeśli program Visual Studio nie pozwalają na odinstalować rozszerzenia (przycisk Odinstaluj jest wyłączony), następnie prawdopodobnie konieczne ponowne uruchomienie programu Visual Studio za pomocą polecenia "Uruchom jako Administrator".</span><span class="sxs-lookup"><span data-stu-id="40ac3-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="40ac3-111">Funkcje</span><span class="sxs-lookup"><span data-stu-id="40ac3-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="40ac3-112">Obsługa, otwierając plik readme.txt po instalacji</span><span class="sxs-lookup"><span data-stu-id="40ac3-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="40ac3-113">Nowość w 1.7, jeśli pakiet zawiera `readme.txt` pliku w katalogu głównym pakietu NuGet automatycznie otworzyć ten plik, po zakończeniu instalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="40ac3-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="40ac3-114">Pokaż pakiety wersji wstępnej w oknie dialogowym pakiety zarządzania pakietami NuGet</span><span class="sxs-lookup"><span data-stu-id="40ac3-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="40ac3-115">Okno dialogowe Zarządzanie pakietami NuGet zawiera teraz listy rozwijanej, która udostępnia opcję, aby wyświetlić pakiety wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="40ac3-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![Wyświetlanie pakiety wersji wstępnej](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="40ac3-117">Pokaż przycisk Przywróć pakietu, gdy brakuje pliku pakietu</span><span class="sxs-lookup"><span data-stu-id="40ac3-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="40ac3-118">Po otwarciu konsoli Menedżera pakietów lub NuGet Menedżera pakietów okna dialogowego, NuGet sprawdzi, czy bieżące rozwiązanie ma włączony tryb przywracania pakietów i jeśli brakuje żadnych plików pakietu `packages` folderu.</span><span class="sxs-lookup"><span data-stu-id="40ac3-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="40ac3-119">Jeśli te dwa warunki są spełnione, NuGet powiadomi użytkownika i wyświetli wygodny przycisk Przywróć.</span><span class="sxs-lookup"><span data-stu-id="40ac3-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="40ac3-120">Kliknięcie tego przycisku spowoduje wyzwolenie NuGet, aby przywrócić brakujących pakietów.</span><span class="sxs-lookup"><span data-stu-id="40ac3-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![Przycisk przywracania pakietu w oknie dialogowym](./media/packagerestore-dialog.png)

![Przycisk przywracania pakietu w konsoli](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="40ac3-123">Dodaj plik rozwiązania na poziomie pliku packages.config</span><span class="sxs-lookup"><span data-stu-id="40ac3-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="40ac3-124">W poprzednich wersjach programu NuGet, każdy projekt ma `packages.config` pliku, który przechowuje informacje o pakietów NuGet, które są zainstalowane w tym projekcie.</span><span class="sxs-lookup"><span data-stu-id="40ac3-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="40ac3-125">Jednak nie było żadnych podobnych plików na poziomie rozwiązania do śledzenia rozwiązanie na poziomie pakietów.</span><span class="sxs-lookup"><span data-stu-id="40ac3-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="40ac3-126">W związku z tym nie było możliwości wykonania pod kątem przywracania pakietów poziomu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="40ac3-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="40ac3-127">Ta funkcja jest teraz implementowane w NuGet 1.7.</span><span class="sxs-lookup"><span data-stu-id="40ac3-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="40ac3-128">Poziom rozwiązania `packages.config` plik znajduje się w `.nuget` folder rozwiązania główny i zapisze tylko rozwiązanie na poziomie pakietów.</span><span class="sxs-lookup"><span data-stu-id="40ac3-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="40ac3-129">Usuń polecenie Nowy pakiet</span><span class="sxs-lookup"><span data-stu-id="40ac3-129">Remove New-Package command</span></span>
<span data-ttu-id="40ac3-130">Z powodu niskiej użycia polecenia New-Package został usunięty.</span><span class="sxs-lookup"><span data-stu-id="40ac3-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="40ac3-131">Deweloperzy są zalecane jest używanie nuget.exe lub przydatną Explorer pakiet NuGet do tworzenia pakietów.</span><span class="sxs-lookup"><span data-stu-id="40ac3-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="40ac3-132">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="40ac3-132">Bug Fixes</span></span>
<span data-ttu-id="40ac3-133">NuGet 1.7 poprawił wiele usterek wokół przywracania pakietów przepływu pracy i scenariusze sieci/kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="40ac3-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="40ac3-134">Pełną listę prac elementów ustalone w NuGet 1.7, sprawdź widok [NuGet Tracker problem w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="40ac3-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
