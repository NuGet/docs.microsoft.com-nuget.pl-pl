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
# <a name="nuget-17-release-notes"></a>Informacje o wersji 1.7 pakietów NuGet

[Informacje o wersji NuGet w wersji 1.6](../release-notes/nuget-1.6.md) | [informacjach o wersji NuGet 1.8](../release-notes/nuget-1.8.md)

NuGet 1.7 został wydany 4 kwietnia 2012 r.

## <a name="known-installation-issue"></a>Problem z instalacją znane
Jeśli używasz programu VS 2010 z dodatkiem SP1, możesz napotkać błąd instalacji podczas próby uaktualnienia NuGet, jeśli masz starszą wersję zainstalowane.

Obejście polega na po prostu Odinstaluj NuGet, a następnie zainstalować go z galerii rozszerzeń programu VS.  Zobacz [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Aby uzyskać więcej informacji.

Uwaga: Jeśli program Visual Studio nie pozwalają na odinstalować rozszerzenie (przycisk Odinstaluj jest wyłączony), prawdopodobnie musisz ponownie program Visual Studio za pomocą polecenia "Uruchom jako Administrator".

## <a name="features"></a>Funkcje

### <a name="support-opening-readmetxt-file-after-installation"></a>Obsługa otwierania pliku readme.txt po zakończeniu instalacji
Nowe w wersji 1.7, jeśli pakiet zawiera `readme.txt` pliku w katalogu głównym pakietu NuGet automatycznie otworzyć ten plik, po zakończeniu instalacji pakietu.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Pokaż pakiety w wersjach wstępnych, w oknie dialogowym pakiety zarządzania pakietami NuGet
Okno dialogowe Zarządzanie pakietami NuGet teraz zawiera listę rozwijaną, która zapewnia opcję, aby wyświetlać pakiety w wersjach wstępnych.

![Wyświetlanie pakiety w wersjach wstępnych](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Pokaż przycisk Przywróć pakiet, gdy brakuje plików pakietu
Po otwarciu konsoli Menedżera pakietów lub pakietów programu Manager NuGet okna dialogowego, NuGet sprawdzi, czy bieżące rozwiązanie ma włączony tryb Przywracanie pakietów, a jeśli brakuje dowolnej pliki pakietu `packages` folderu. Jeśli te dwa warunki są spełnione, powiadomi użytkownika i wyświetli wygodne przycisk przywracania NuGet. Kliknięcie tego przycisku spowoduje wyzwolenie pakietu NuGet, aby przywrócić wszystkie brakujące pakiety.

![Przycisk przywracania pakietów w oknie dialogowym](./media/packagerestore-dialog.png)

![Przycisk Przywróć pakiet w konsoli](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Dodawanie pliku packages.config na poziomie rozwiązania
W poprzednich wersjach programu NuGet, każdy projekt ma `packages.config` pliku, który śledzi informacje o pakietów NuGet, które są zainstalowane w tym projekcie. Jednak nie było żadnych podobnych plików na poziomie rozwiązania do śledzenia pakietów poziomie rozwiązania. W rezultacie nie było możliwości można przywrócić pakietów poziomie rozwiązania.
Ta funkcja jest teraz implementowane w wersji 1.7 NuGet. Poziom rozwiązania `packages.config` plik zostanie umieszczony w obszarze `.nuget` folder, w ramach rozwiązania główny i będzie przechowywać pakiety tylko poziomie rozwiązania.

### <a name="remove-new-package-command"></a>Usuń polecenie New-Package
Z powodu niskiej użycia polecenia New-Package zostało usunięte. Deweloperom zaleca się używać nuget.exe lub przydatną Eksplorator pakietów NuGet do tworzenia pakietów.

## <a name="bug-fixes"></a>Poprawki błędów
NuGet 1.7 ma ustaloną wiele błędów wokół scenariuszy kontroli sieci/źródła i przywracanie pakietów przepływu pracy.

Aby uzyskać pełną listę prac elementy rozwiązane w NuGet 1.7, widok [NuGet narzędzie do śledzenia problemów w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
