---
title: Informacje o wersji narzędzia NuGet 1,7
description: Informacje o wersji programu NuGet 1,7, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a98da76038582202396c8da96f8eae166e6096f6
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383322"
---
# <a name="nuget-17-release-notes"></a>Informacje o wersji narzędzia NuGet 1,7

[Informacje o wersji pakietu nuget 1,6](../release-notes/nuget-1.6.md) | [Informacje o wersji narzędzia NuGet 1,8](../release-notes/nuget-1.8.md)

Pakiet NuGet 1,7 został wydaną 4 kwietnia 2012.

## <a name="known-installation-issue"></a>Znany problem z instalacją
W przypadku korzystania z programu VS 2010 z dodatkiem SP1 można napotkać błąd instalacji podczas próby uaktualnienia narzędzia NuGet, jeśli jest zainstalowana starsza wersja.

Obejście polega na prostu odinstalować pakiet NuGet, a następnie zainstalować go z galerii rozszerzeń programu VS.  Aby uzyskać więcej informacji, zobacz <https://support.microsoft.com/kb/2581019>.

Uwaga: Jeśli program Visual Studio nie zezwoli na odinstalowanie rozszerzenia (przycisk Odinstaluj jest wyłączony), prawdopodobnie trzeba będzie ponownie uruchomić program Visual Studio za pomocą polecenia "Uruchom jako administrator".

## <a name="features"></a>Funkcje

### <a name="support-opening-readmetxt-file-after-installation"></a>Obsługa otwierania pliku Readme. txt po instalacji
Nowość w 1,7, jeśli pakiet zawiera plik `readme.txt` w folderze głównym pakietu, pakiet NuGet automatycznie otworzy ten plik po zakończeniu instalacji pakietu.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Pokaż pakiety wersji wstępnej w oknie dialogowym Zarządzanie pakietami NuGet
Okno dialogowe Zarządzanie pakietami NuGet zawiera teraz listę rozwijaną, która zawiera opcję wyświetlania pakietów wersji wstępnej.

![Wyświetlanie pakietów wersji wstępnej](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Pokaż przycisk przywracania pakietu, gdy brakuje plików pakietu
Po otwarciu konsoli Menedżera pakietów lub okna dialogowego pakiety NuGet Menedżera NuGet sprawdzi, czy bieżące rozwiązanie włączyło tryb przywracania pakietu i jeśli brakuje plików pakietu w folderze `packages`. Jeśli te dwa warunki są spełnione, pakiet NuGet wyświetli powiadomienie i wyświetli wygodny przycisk przywracania. Kliknięcie tego przycisku spowoduje wyzwolenie programu NuGet na przywrócenie wszystkich brakujących pakietów.

![Przycisk przywracania pakietu w oknie dialogowym](./media/packagerestore-dialog.png)

![Przycisk Przywróć pakiet w konsoli](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Dodaj plik config pakietów na poziomie rozwiązania
W poprzednich wersjach programu NuGet każdy projekt zawiera plik `packages.config`, który śledzi, jakie pakiety NuGet są zainstalowane w tym projekcie. Jednak na poziomie rozwiązania nie ma podobnego pliku do śledzenia pakietów na poziomie rozwiązania. W związku z tym nie było możliwości przywrócenia pakietów na poziomie rozwiązania.
Ta funkcja jest teraz zaimplementowana w programie NuGet 1,7. Plik `packages.config` na poziomie rozwiązania zostanie umieszczony w folderze `.nuget` w obszarze katalogu głównego rozwiązania i będzie przechowywać tylko pakiety na poziomie rozwiązania.

### <a name="remove-new-package-command"></a>Usuń polecenie New-Package
Ze względu na niskie użycie polecenie New-Package zostało usunięte. Deweloperzy są zalecani do tworzenia pakietów przy użyciu programu NuGet. exe lub narzędzia z Eksploratorem pakietów NuGet.

## <a name="bug-fixes"></a>Poprawki błędów
W pakiecie NuGet 1,7 rozwiązano wiele usterek wokół przepływu pracy przywracania pakietów i scenariuszy kontroli sieci/źródła.

Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 1,7, zobacz [Śledzenie problemów NuGet dla tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
