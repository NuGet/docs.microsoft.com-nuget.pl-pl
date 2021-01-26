---
title: Informacje o wersji narzędzia NuGet 1,7
description: Informacje o wersji programu NuGet 1,7, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 50eb326c5ada4f74685b07c0d1b0f84b14e547ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777069"
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="e3fc4-103">Informacje o wersji narzędzia NuGet 1,7</span><span class="sxs-lookup"><span data-stu-id="e3fc4-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="e3fc4-104">Informacje o wersji narzędzia [NuGet 1,6](../release-notes/nuget-1.6.md)  |  [Informacje o wersji narzędzia NuGet 1,8](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="e3fc4-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="e3fc4-105">Pakiet NuGet 1,7 został wydaną 4 kwietnia 2012.</span><span class="sxs-lookup"><span data-stu-id="e3fc4-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="e3fc4-106">Znany problem z instalacją</span><span class="sxs-lookup"><span data-stu-id="e3fc4-106">Known Installation Issue</span></span>
<span data-ttu-id="e3fc4-107">W przypadku korzystania z programu VS 2010 z dodatkiem SP1 można napotkać błąd instalacji podczas próby uaktualnienia narzędzia NuGet, jeśli jest zainstalowana starsza wersja.</span><span class="sxs-lookup"><span data-stu-id="e3fc4-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="e3fc4-108">Obejście polega na prostu odinstalować pakiet NuGet, a następnie zainstalować go z galerii rozszerzeń programu VS.</span><span class="sxs-lookup"><span data-stu-id="e3fc4-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="e3fc4-109">Aby uzyskać więcej informacji, zobacz <https://support.microsoft.com/kb/2581019>.</span><span class="sxs-lookup"><span data-stu-id="e3fc4-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="e3fc4-110">Uwaga: Jeśli program Visual Studio nie zezwoli na odinstalowanie rozszerzenia (przycisk Odinstaluj jest wyłączony), prawdopodobnie trzeba będzie ponownie uruchomić program Visual Studio za pomocą polecenia "Uruchom jako administrator".</span><span class="sxs-lookup"><span data-stu-id="e3fc4-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="e3fc4-111">Funkcje</span><span class="sxs-lookup"><span data-stu-id="e3fc4-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="e3fc4-112">Obsługa otwierania pliku readme.txt po instalacji</span><span class="sxs-lookup"><span data-stu-id="e3fc4-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="e3fc4-113">Nowość w 1,7, jeśli pakiet zawiera `readme.txt` plik w katalogu głównym pakietu, pakiet NuGet automatycznie otworzy ten plik po zakończeniu instalacji pakietu.</span><span class="sxs-lookup"><span data-stu-id="e3fc4-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="e3fc4-114">Pokaż pakiety wersji wstępnej w oknie dialogowym Zarządzanie pakietami NuGet</span><span class="sxs-lookup"><span data-stu-id="e3fc4-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="e3fc4-115">Okno dialogowe Zarządzanie pakietami NuGet zawiera teraz listę rozwijaną, która zawiera opcję wyświetlania pakietów wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="e3fc4-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![Wyświetlanie pakietów wersji wstępnej](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="e3fc4-117">Pokaż przycisk przywracania pakietu, gdy brakuje plików pakietu</span><span class="sxs-lookup"><span data-stu-id="e3fc4-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="e3fc4-118">Po otwarciu konsoli Menedżera pakietów lub okna dialogowego pakiety NuGet Menedżera program NuGet sprawdzi, czy bieżące rozwiązanie włączyło tryb przywracania pakietu, a w przypadku braku plików pakietu w `packages` folderze.</span><span class="sxs-lookup"><span data-stu-id="e3fc4-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="e3fc4-119">Jeśli te dwa warunki są spełnione, pakiet NuGet wyświetli powiadomienie i wyświetli wygodny przycisk przywracania.</span><span class="sxs-lookup"><span data-stu-id="e3fc4-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="e3fc4-120">Kliknięcie tego przycisku spowoduje wyzwolenie programu NuGet na przywrócenie wszystkich brakujących pakietów.</span><span class="sxs-lookup"><span data-stu-id="e3fc4-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![Przycisk przywracania pakietu w oknie dialogowym](./media/packagerestore-dialog.png)

![Przycisk Przywróć pakiet w konsoli](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="e3fc4-123">Dodaj plik packages.config na poziomie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="e3fc4-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="e3fc4-124">W poprzednich wersjach programu NuGet każdy projekt zawiera plik, `packages.config` który śledzi, jakie pakiety NuGet są zainstalowane w tym projekcie.</span><span class="sxs-lookup"><span data-stu-id="e3fc4-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="e3fc4-125">Jednak na poziomie rozwiązania nie ma podobnego pliku do śledzenia pakietów na poziomie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="e3fc4-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="e3fc4-126">W związku z tym nie było możliwości przywrócenia pakietów na poziomie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="e3fc4-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="e3fc4-127">Ta funkcja jest teraz zaimplementowana w programie NuGet 1,7.</span><span class="sxs-lookup"><span data-stu-id="e3fc4-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="e3fc4-128">Plik poziomu rozwiązania `packages.config` zostanie umieszczony w `.nuget` folderze w katalogu głównym rozwiązania i będzie przechowywać tylko pakiety na poziomie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="e3fc4-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="e3fc4-129">Usuń New-Package polecenie</span><span class="sxs-lookup"><span data-stu-id="e3fc4-129">Remove New-Package command</span></span>
<span data-ttu-id="e3fc4-130">Ze względu na niskie użycie polecenie New-Package zostało usunięte.</span><span class="sxs-lookup"><span data-stu-id="e3fc4-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="e3fc4-131">Deweloperzy są zalecani do tworzenia pakietów przy użyciu nuget.exe lub narzędziowego Eksploratora pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="e3fc4-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="e3fc4-132">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="e3fc4-132">Bug Fixes</span></span>
<span data-ttu-id="e3fc4-133">W pakiecie NuGet 1,7 rozwiązano wiele usterek wokół przepływu pracy przywracania pakietów i scenariuszy kontroli sieci/źródła.</span><span class="sxs-lookup"><span data-stu-id="e3fc4-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="e3fc4-134">Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 1,7, zobacz [Śledzenie problemów NuGet dla tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="e3fc4-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
