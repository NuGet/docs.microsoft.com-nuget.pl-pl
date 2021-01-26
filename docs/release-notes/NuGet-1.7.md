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
# <a name="nuget-17-release-notes"></a>Informacje o wersji narzędzia NuGet 1,7

Informacje o wersji narzędzia [NuGet 1,6](../release-notes/nuget-1.6.md)  |  [Informacje o wersji narzędzia NuGet 1,8](../release-notes/nuget-1.8.md)

Pakiet NuGet 1,7 został wydaną 4 kwietnia 2012.

## <a name="known-installation-issue"></a>Znany problem z instalacją
W przypadku korzystania z programu VS 2010 z dodatkiem SP1 można napotkać błąd instalacji podczas próby uaktualnienia narzędzia NuGet, jeśli jest zainstalowana starsza wersja.

Obejście polega na prostu odinstalować pakiet NuGet, a następnie zainstalować go z galerii rozszerzeń programu VS.  Aby uzyskać więcej informacji, zobacz <https://support.microsoft.com/kb/2581019>.

Uwaga: Jeśli program Visual Studio nie zezwoli na odinstalowanie rozszerzenia (przycisk Odinstaluj jest wyłączony), prawdopodobnie trzeba będzie ponownie uruchomić program Visual Studio za pomocą polecenia "Uruchom jako administrator".

## <a name="features"></a>Funkcje

### <a name="support-opening-readmetxt-file-after-installation"></a>Obsługa otwierania pliku readme.txt po instalacji
Nowość w 1,7, jeśli pakiet zawiera `readme.txt` plik w katalogu głównym pakietu, pakiet NuGet automatycznie otworzy ten plik po zakończeniu instalacji pakietu.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Pokaż pakiety wersji wstępnej w oknie dialogowym Zarządzanie pakietami NuGet
Okno dialogowe Zarządzanie pakietami NuGet zawiera teraz listę rozwijaną, która zawiera opcję wyświetlania pakietów wersji wstępnej.

![Wyświetlanie pakietów wersji wstępnej](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Pokaż przycisk przywracania pakietu, gdy brakuje plików pakietu
Po otwarciu konsoli Menedżera pakietów lub okna dialogowego pakiety NuGet Menedżera program NuGet sprawdzi, czy bieżące rozwiązanie włączyło tryb przywracania pakietu, a w przypadku braku plików pakietu w `packages` folderze. Jeśli te dwa warunki są spełnione, pakiet NuGet wyświetli powiadomienie i wyświetli wygodny przycisk przywracania. Kliknięcie tego przycisku spowoduje wyzwolenie programu NuGet na przywrócenie wszystkich brakujących pakietów.

![Przycisk przywracania pakietu w oknie dialogowym](./media/packagerestore-dialog.png)

![Przycisk Przywróć pakiet w konsoli](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Dodaj plik packages.config na poziomie rozwiązania
W poprzednich wersjach programu NuGet każdy projekt zawiera plik, `packages.config` który śledzi, jakie pakiety NuGet są zainstalowane w tym projekcie. Jednak na poziomie rozwiązania nie ma podobnego pliku do śledzenia pakietów na poziomie rozwiązania. W związku z tym nie było możliwości przywrócenia pakietów na poziomie rozwiązania.
Ta funkcja jest teraz zaimplementowana w programie NuGet 1,7. Plik poziomu rozwiązania `packages.config` zostanie umieszczony w `.nuget` folderze w katalogu głównym rozwiązania i będzie przechowywać tylko pakiety na poziomie rozwiązania.

### <a name="remove-new-package-command"></a>Usuń New-Package polecenie
Ze względu na niskie użycie polecenie New-Package zostało usunięte. Deweloperzy są zalecani do tworzenia pakietów przy użyciu nuget.exe lub narzędziowego Eksploratora pakietów NuGet.

## <a name="bug-fixes"></a>Poprawki błędów
W pakiecie NuGet 1,7 rozwiązano wiele usterek wokół przepływu pracy przywracania pakietów i scenariuszy kontroli sieci/źródła.

Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 1,7, zobacz [Śledzenie problemów NuGet dla tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
