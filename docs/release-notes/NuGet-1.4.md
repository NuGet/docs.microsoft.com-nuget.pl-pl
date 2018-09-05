---
title: Informacje o wersji 1.4 NuGet
description: Informacje o wersji programu NuGet 1.4 tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f4d712f83ea108a82a1bc4910c2a721a8c24d51
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550634"
---
# <a name="nuget-14-release-notes"></a>Informacje o wersji 1.4 NuGet

[Informacje o wersji NuGet 1.3](../release-notes/nuget-1.3.md) | [informacjach o wersji NuGet w wersji 1.5](../release-notes/nuget-1.5.md)

NuGet 1.4 został wydany 17 czerwca 2011.

## <a name="features"></a>Funkcje

### <a name="update-package-improvements"></a>Ulepszenia dotyczące pakietów aktualizacji
NuGet 1.4 wprowadzono wiele ulepszeń do polecenia pakiet aktualizacji, co ułatwia zapewnienie pakietów w tej samej wersji wielu projektów w rozwiązaniu. Na przykład podczas uaktualniania pakietu do najnowszej wersji, jest bardzo często mają wszystkie projekty z pakietu, aby zainstalować zaktualizowane do tej samej verision.

`Update-Package` Polecenia umożliwia teraz łatwiejsze do:

#### <a name="update-all-packages-in-a-single-project"></a>Aktualizuj wszystkie pakiety w jednym projekcie

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>Aktualizuj pakiet we wszystkich projektach

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>Aktualizuj wszystkie pakiety we wszystkich projektach

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>Przeprowadzania "bezpieczne" Aktualizuj wszystkie pakiety
`-Safe` Flagi ogranicza uaktualnienia do wersji tylko za pomocą tego samego składnika wersji głównych i pomocniczych. Na przykład, jeśli jest zainstalowana wersja 1.0.0 pakietu i wersji 1.0.1, 1.0.2 i 1.1 są dostępne w źródle danych `-Safe` flagi aktualizuje pakiet 1.0.2. Uaktualnianie bez `-Safe` flagi czy uaktualnić pakiet do najnowszej wersji 1.1.

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>Zarządzanie pakietami na poziomie rozwiązania
Przed NuGet 1.4 instalowania pakietu w wielu projektach było uciążliwe, korzystając z okna dialogowego. Wymaga ona, uruchamiając okno dialogowe raz na projekt.

NuGet 1.4 dodaje obsługi instalowania/odinstalowywania/aktualizowania pakietów w wielu projektach, w tym samym czasie. Po prostu uruchomić, klikając prawym przyciskiem myszy rozwiązanie i wybierając **Zarządzaj pakietami NuGet** opcji menu.

![Okno dialogowe poziom Zarządzaj pakietami NuGet rozwiązania](./media/manage-nuget-packages-solution-dialog.png)

Zwróć uwagę, że na pasku tytułu okna dialogowego nazwę rozwiązania jest wyświetlany, a nie nazwa projektu.
Operacje pakietu udostępniają teraz listy pól wyboru z listy projektów, których mają dotyczyć operacji.

![Zarządzanie wybór projektu pakiety NuGet](./media/manage-nuget-packages-project-selection.png)

Aby uzyskać więcej informacji, zobacz temat w [Zarządzanie pakietami dla rozwiązania](../tools/package-manager-ui.md#managing-packages-for-the-solution).

### <a name="constraining-upgrades-to-allowed-versions"></a>Ograniczając uaktualniania do wersji dozwolone
Domyślnie podczas uruchamiania `Update-Package` na pakiet (lub aktualizowanie pakietu za pomocą okna dialogowego), polecenia zostaną zaktualizowane do najnowszej wersji w źródle danych. Z nową obsługę aktualizacji wszystkich pakietów może być przypadki, w których chcesz zablokować pakietu do określonego zakresu wersji. Na przykład mogą wiedzieć z wyprzedzeniem, że aplikacja będzie działać tylko z 2.* wersji pakietu, ale nie 3.0 lub nowszej. Aby zapobiec przypadkowemu aktualizacja pakietu do 3, NuGet 1.4 dodaje obsługę ograniczając zakres wersji, które pakiety mogą być uaktualniane do, ręcznie edytując `packages.config` plików za pomocą nowego `allowedVersions` atrybutu.

Na przykład, poniższy przykład pokazuje, jak zablokować `SomePackage` pakietu wersji zakresu w wersji 2.0 — 3.0 (wyłącznie).
`allowedVersions` Atrybut akceptuje wartości za pomocą [formatu zakres wersji](../reference/package-versioning.md#version-ranges-and-wildcards).

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

Należy pamiętać, że 1.4, blokowanie pakietu do określonego zakresu wersji musi być ręcznie edytowany. W wersji 1.5 NuGet planujemy dodanie obsługi wprowadzania do tego zakresu, za pośrednictwem `Install-Package` polecenia.

### <a name="package-visualizer"></a>Pakiet wizualizatora
Wizualizator nowego pakietu, wyszukiwarce uruchamianej w **narzędzia** -> **Menedżer pakietów biblioteki** -> **pakiet wizualizatora** opcji menu pozwala na łatwo Wizualizuj wszystkich projektów i ich zależności pakietów w ramach rozwiązania.

_**Ważna Uwaga:** ta funkcja korzysta z pomocy technicznej DGML w programie Visual Studio. Tworzenie wizualizacji jest obsługiwana tylko w programie Visual Studio Ultimate. Wyświetlanie diagramu DGML jest obsługiwana tylko w Visual Studio Premium lub wyższego._

![Pakiet wizualizatora](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>Sprawdzanie aktualizacji automatycznych dla okna dialogowego NuGet
Niektóre wersje NuGet wprowadzać nowe funkcje, które wyrażone za pomocą `.nuspec` pliku, który jest niezrozumiały przez starsze wersje programu NuGet okna dialogowego.
Przykładem jest wprowadzenie 1.4 NuGet dla [określania zestawów framework](../release-notes/nuget-1.2.md#framework-assembly-refs).
W związku z tym należy używać najnowszej wersji pakietu NuGet, aby upewnić się, że możesz użyć pakietów, korzystając z zalet najnowszych funkcji.
Aby wprowadzić aktualizacje NuGet bardziej widoczne, okno dialogowe NuGet zawiera logikę do Podświetl, gdy dostępna jest nowsza wersja.

_**Uwaga**: sprawdzanie jest wykonywane tylko wtedy, gdy **Online** kartę został wybrany w bieżącej sesji._

![Zarządzanie pakietami NuGet dialog z dostępna nowa wersja](./media/manage-nuget-packages-update-notification.png)

Aby wyłączyć funkcję automatycznego sprawdzania aktualizacji, przejdź do okna dialogowego Ustawienia NuGet i usuń zaznaczenie pola wyboru **automatycznie sprawdzaj dostępność aktualizacji**.

![Ustawienia NuGet](./media/nuget-settings.png)

Ta funkcja rzeczywiście został dodany do programu NuGet 1.3, ale nie będzie widoczny, oczywiście, aż aktualizacja 1.3, takie jak NuGet 1.4, została udostępniona.

### <a name="package-manager-dialog-improvements"></a>Ulepszenia okna dialogowego Menedżera pakietów
* **Nazwy menu ulepszone**: Opcje Menu, aby uruchomić okno dialogowe zostały zmienione w celu uściślenia. Opcja menu jest teraz **Zarządzaj pakietami NuGet**.
* **Okienko szczegółów pokazuje Najpóźniejsza data aktualizacji**: NuGet, okno dialogowe wyświetla datę ostatniej aktualizacji w okienku szczegółów pakietu podczas **Online** lub **aktualizuje** wybrana jest karta.
* **Lista tagów wyświetlane**: tagi Wyświetla okno dialogowe Nuget.

### <a name="powershell-improvements"></a>Ulepszenia programu PowerShell
* **Podpisane skrypty programu PowerShell**: NuGet zawiera podpisanych skryptów programu Powershell umożliwiające użycie w środowiskach bardziej restrykcyjne.
* **Monitowanie pomocy technicznej**: konsoli Menedżera pakietów obsługuje teraz monitowania użytkownika za pośrednictwem `$host.ui.Prompt` i `$host.ui.PromptForChoice` poleceń.
* **Pakiet nazw źródeł**: podanie nazwy źródła pakietu jest obsługiwana w przypadku określania źródła pakietu przy użyciu `-Source` flagi.

### <a name="nugetexe-command-line-improvements"></a>ulepszenia wiersza polecenia nuget.exe
* **Niestandardowe polecenia NuGet**: nuget.exe jest rozszerzalny za pomocą polecenia niestandardowe za pomocą MEF.
* **Prostsze przepływu pracy do tworzenia pakietów symbol**: `-Symbols` flagi mogą być stosowane do normalnego oparte na Konwencji strukturę folderów, tworzenie pakietu symboli, umieszczając tylko źródła i `.pdb` pliki znajdujące się w folderze.
* **Określanie wielu źródeł**: `NuGet install` polecenie obsługuje Określanie wielu źródeł przy użyciu średników, jak ogranicznik lub określając `-Source` wiele razy.
* **Obsługuje uwierzytelnianie serwera proxy**: 1,4 NuGet dodaje obsługę monit o podanie poświadczeń użytkownika, gdy używasz serwera proxy, który wymaga uwierzytelniania za pomocą narzędzia NuGet.
* **nuget.exe aktualizacji zmiana powodująca niezgodność**: `-Self` flaga jest teraz wymagany nuget.exe samodzielne zaktualizowanie się. `nuget.exe Update` teraz przyjmuje ścieżkę do `packages.config` plik i spróbuje pakietów aktualizacji. Należy pamiętać, że ta aktualizacja jest ograniczony w tym, że nie będzie: ** zaktualizować, Dodaj, usuń zawartość w pliku projektu.
** Uruchamiania skryptów programu Powershell w pakiecie.

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>Obsługa serwera NuGet wypychania pakietów przy użyciu nuget.exe
NuGet zawiera prosty sposób hosta [uproszczone sieci web na podstawie repozytorium NuGet](../hosting-packages/nuget-server.md) za pośrednictwem `NuGet.Server` pakietu NuGet. NuGet 1.4 lekki serwer obsługuje wypychanie i usuwanie pakietów przy użyciu nuget.exe.
Najnowszą wersję `NuGet.Server` dodaje nowy `appSetting`o nazwie `apiKey`. Gdy klucz zostanie pominięty lub pole pozostanie puste, wypychanie pakietów do kanału informacyjnego jest wyłączona. Ustawienie apiKey wartości (najlepiej silne hasło) umożliwia wypychania pakietów przy użyciu nuget.exe.

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Obsługa wersji Mango narzędzi Windows Phone
NuGet jest teraz obsługiwana w wersji release candidate narzędzi Windows Phone dla Mango.
Obecnie narzędzia Windows Phone nie ma obsługi dla Menedżera rozszerzenia Visual Studio tak zainstalować narzędzia do dla Windows Phone NuGet, może być konieczne pobranie i uruchomienie VSIX ręcznie.

Aby odinstalować NuGet dla Windows Phone narzędzia, uruchom następujące polecenie.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>Poprawki błędów
NuGet 1.4 ma w sumie 88 stałej elementów roboczych. 71 tych zostały oznaczone jako błędy.

Aby uzyskać pełną listę prac elementy rozwiązane w NuGet 1.4, widok [NuGet narzędzie do śledzenia problemów w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Poprawki błędów warte odnotowania:

* [Problem 603](http://nuget.codeplex.com/workitem/603): zależności pakietów w różnych repozytoriach jest rozpoznawana jako poprawnie podczas określania źródła określonego pakietu.
* [Problem 1036](http://nuget.codeplex.com/workitem/1036): dodawanie `NuGet Pack SomeProject.csproj` na zdarzenie po kompilacji nie jest już powoduje nieskończoną pętlę.
* [Problem 961](http://nuget.codeplex.com/workitem/961): `-Source` flagi obsługuje ścieżki względne.

## <a name="nuget-14-update"></a>Aktualizacja NuGet 1.4
Wkrótce po wydaniu NuGet 1.4 znaleźliśmy kilka problemów, które były ważne rozwiązać problem.
Liczba określonych wersji tej aktualizacji 1.4 jest 1.4.20615.9020.

### <a name="bug-fixes"></a>Poprawki błędów
* [Problem 1220](http://nuget.codeplex.com/workitem/1220): pakiet aktualizacji nie jest wykonywany `install.ps1` / `uninstall.ps1` we wszystkich projektach w sytuacji, gdy istnieje więcej niż jeden projekt
* [Problem 1156](http://nuget.codeplex.com/workitem/1156): konsoli Menedżera pakietów została zablokowana na W2K3/XP (Jeśli nie zainstalowano programu Powershell 2)
