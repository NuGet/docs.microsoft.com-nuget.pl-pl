---
title: Informacje o wersji NuGet 1.7 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informacje o wersji dla tym znanych problemów, poprawki, dodatkowe funkcje i dcr 1.7 NuGet."
keywords: NuGet 1.7 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7b16bea8c6bcc77f814dd32a43b895b5e656c95d
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-17-release-notes"></a>Informacje o wersji 1,7 NuGet

[Informacje o wersji NuGet w wersji 1.6](../release-notes/nuget-1.6.md) | [NuGet 1.8 informacje o wersji](../release-notes/nuget-1.8.md)

NuGet 1.7 został wydany 4 kwietnia 2012.

## <a name="known-installation-issue"></a>Znane problem
Jeśli korzystasz z VS 2010 z dodatkiem SP1, możesz napotkać błąd instalacji podczas próby uaktualnienia NuGet, jeśli masz starszą wersję zainstalowane.

Obejście jest po prostu odinstalować NuGet, a następnie zainstaluj go z galerii rozszerzeń programu VS.  Zobacz [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) Aby uzyskać więcej informacji.

Uwaga: Jeśli program Visual Studio nie pozwalają na odinstalować rozszerzenia (przycisk Odinstaluj jest wyłączony), następnie prawdopodobnie konieczne ponowne uruchomienie programu Visual Studio za pomocą polecenia "Uruchom jako Administrator".

## <a name="features"></a>Funkcje

### <a name="support-opening-readmetxt-file-after-installation"></a>Obsługa, otwierając plik readme.txt po instalacji
Nowość w 1.7, jeśli pakiet zawiera `readme.txt` pliku w katalogu głównym pakietu NuGet automatycznie otworzyć ten plik, po zakończeniu instalowania pakietu.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Pokaż pakiety wersji wstępnej w oknie dialogowym pakiety zarządzania pakietami NuGet
Okno dialogowe Zarządzanie pakietami NuGet zawiera teraz listy rozwijanej, która udostępnia opcję, aby wyświetlić pakiety wersji wstępnej.

![Wyświetlanie pakiety wersji wstępnej](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Pokaż przycisk Przywróć pakietu, gdy brakuje pliku pakietu
Po otwarciu konsoli Menedżera pakietów lub NuGet Menedżera pakietów okna dialogowego, NuGet sprawdzi, czy bieżące rozwiązanie ma włączony tryb przywracania pakietów i jeśli brakuje żadnych plików pakietu `packages` folderu. Jeśli te dwa warunki są spełnione, NuGet powiadomi użytkownika i wyświetli wygodny przycisk Przywróć. Kliknięcie tego przycisku spowoduje wyzwolenie NuGet, aby przywrócić brakujących pakietów.

![Przycisk przywracania pakietu w oknie dialogowym](./media/packagerestore-dialog.png)

![Przycisk przywracania pakietu w konsoli](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Dodaj plik rozwiązania na poziomie pliku packages.config
W poprzednich wersjach programu NuGet, każdy projekt ma `packages.config` pliku, który przechowuje informacje o pakietów NuGet, które są zainstalowane w tym projekcie. Jednak nie było żadnych podobnych plików na poziomie rozwiązania do śledzenia rozwiązanie na poziomie pakietów. W związku z tym nie było możliwości wykonania pod kątem przywracania pakietów poziomu rozwiązania.
Ta funkcja jest teraz implementowane w NuGet 1.7. Poziom rozwiązania `packages.config` plik znajduje się w `.nuget` folder rozwiązania główny i zapisze tylko rozwiązanie na poziomie pakietów.

### <a name="remove-new-package-command"></a>Usuń polecenie Nowy pakiet
Z powodu niskiej użycia polecenia New-Package został usunięty. Deweloperzy są zalecane jest używanie nuget.exe lub przydatną Explorer pakiet NuGet do tworzenia pakietów.

## <a name="bug-fixes"></a>Poprawki błędów
NuGet 1.7 poprawił wiele usterek wokół przywracania pakietów przepływu pracy i scenariusze sieci/kontroli wersji.

Pełną listę prac elementów ustalone w NuGet 1.7, sprawdź widok [NuGet Tracker problem w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
