---
title: Informacje o wersji NuGet 1.4 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: e4856d0a-b408-4c60-ac51-f80ea06d9f79
description: "Informacje o wersji dla tym znanych problemów, poprawki, dodatkowe funkcje i dcr 1.4 NuGet."
keywords: NuGet 1.4 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c4c27861c8697c75a06712b8ca6243b3b206cbb3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-14-release-notes"></a>Informacje o wersji 1.4 NuGet

[Informacje o wersji NuGet 1.3](../release-notes/nuget-1.3.md) | [NuGet w wersji 1.5 informacje o wersji](../release-notes/nuget-1.5.md)

NuGet 1.4 został wydany 17 czerwca 2011.

## <a name="features"></a>Funkcje

### <a name="update-package-improvements"></a>Ulepszenia pakietu aktualizacji
NuGet 1.4 wprowadzono wiele ulepszeń polecenia pakiet aktualizacji, co ułatwia utrzymanie pakietów na tej samej wersji wielu projektów w rozwiązaniu. Na przykład podczas uaktualniania pakietu do najnowszej wersji, jest często mają wszystkie projekty z tym pakietem zainstalowanych aktualizacji do tej samej verision.

`Update-Package` Polecenia teraz ułatwia:

#### <a name="update-all-packages-in-a-single-project"></a>Zaktualizuj wszystkie pakiety w pojedynczego projektu

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>Zaktualizować pakiet we wszystkich projektach

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>Zaktualizuj wszystkie pakiety we wszystkich projektach

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>Wykonaj "bezpiecznej" aktualizacji na wszystkie pakiety
`-Safe` Flagi ogranicza uaktualnienia do wersji tylko z tym samym składnikiem wersji głównej i pomocniczej. Na przykład, jeśli jest zainstalowana wersja 1.0.0 pakietu, i są dostępne w źródle danych, wersje 1.0.1, 1.0.2 i 1.1 `-Safe` flagi aktualizację pakietu do wersji 1.0.2. Uaktualnianie bez `-Safe` flagi spowoduje uaktualnienie pakietu do najnowszej wersji 1.1.

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>Zarządzanie pakietami na poziomie rozwiązania
Przed NuGet 1.4 instalowania pakietu w wielu projektach było skomplikowane, korzystając z okna dialogowego. Wymaga ona uruchamianie okna dialogowego raz na projekt.

NuGet 1.4 dodaje obsługę Instalowanie/Odinstalowywanie/aktualizowanie pakietów w wielu projektach, w tym samym czasie. Wystarczy uruchomić przez kliknięcie prawym przyciskiem myszy rozwiązanie i wybierając **Zarządzaj pakietami NuGet** opcji menu.

![Okno dialogowe poziom Zarządzaj pakietami NuGet rozwiązania](./media/manage-nuget-packages-solution-dialog.png)

Powiadomienie, że na pasku tytułu okna dialogowego rozwiązania jest wyświetlana nazwa, a nie nazwa projektu.
Pakiet operations zapewnia teraz listy pól wyboru z listy projektów, które dotyczą operacji.

![Zarządzanie wybór projektu pakietów NuGet](./media/manage-nuget-packages-project-selection.png)

Aby uzyskać więcej informacji, zobacz temat na [Zarządzanie pakietami dla rozwiązania](../tools/package-manager-ui.md#managing-packages-for-the-solution).

### <a name="constraining-upgrades-to-allowed-versions"></a>Ograniczający uaktualnienia do wersji dozwolone
Domyślnie podczas uruchamiania `Update-Package` polecenia dla pakietu (lub aktualizowanie pakietu za pomocą okna dialogowego), zostaną zaktualizowane do najnowszej wersji w źródle danych. Z nowego Obsługa wszystkich pakietów aktualizacji może być przypadki, w których chcesz zablokować pakietu do zakresu określonej wersji. Na przykład możesz może wiedzieć z wyprzedzeniem, że aplikacja będzie działać tylko z 2.* wersji pakietu, ale nie 3.0 i nowszych. Aby zapobiec przypadkowemu aktualizacji pakietu na 3, NuGet 1.4 dodaje obsługę ograniczając zakres wersji, które pakiety można uaktualnić do edycji strony `packages.config` plik za pomocą nowej `allowedVersions` atrybutu.

Na przykład poniższy przykład przedstawia sposób zablokować `SomePackage` pakietu wersji zakresu 2.0-3.0 (na wyłączność).
`allowedVersions` Atrybutu akceptuje wartości przy użyciu [formatu zakres wersji](../reference/package-versioning.md#version-ranges-and-wildcards).

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

Należy pamiętać, że 1.4, blokowanie pakietu do zakresu określonej wersji musi być edytowane ręcznie. W wersji 1.5 NuGet planujemy dodać obsługę wprowadzania do tego zakresu za pośrednictwem `Install-Package` polecenia.

### <a name="package-visualizer"></a>Wizualizator pakietu
Wizualizatora nowego pakietu, uruchomiony za pośrednictwem **narzędzia** -> **Menedżer pakietów biblioteki** -> **wizualizatora pakietu** opcji menu, pozwala na łatwo przedstawić wizualnie wszystkich projektów i ich zależności pakietów w ramach rozwiązania.

_**Ważna Uwaga:** ta funkcja korzysta z pomocy technicznej DGML w programie Visual Studio. Tworzenie wizualizacji jest obsługiwana tylko w programie Visual Studio Ultimate. Wyświetlanie diagramu DGML jest obsługiwana tylko w programie Visual Studio Premium lub wyższego._

![Wizualizator pakietu](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>Sprawdzanie aktualizacji automatycznych dla okna dialogowego NuGet
Niektóre wersje programu NuGet wprowadzać nowe funkcje, wyrażona za pomocą `.nuspec` pliku, który nie jest rozpoznawany przez starsze wersje NuGet okna dialogowego.
Przykładem jest wprowadzenie 1.4 NuGet dla [określanie zestawów struktury](../release-notes/nuget-1.2.md#framework-assembly-refs).
W związku z tym należy używać najnowszej wersji programu NuGet, aby upewnić się, że można użyć pakietów korzystanie z zalet najnowszych funkcji.
Aby zaktualizować NuGet bardziej widoczne, okno dialogowe NuGet zawiera logiki, aby wyróżnić, gdy dostępna jest nowsza wersja.

_**Uwaga**: sprawdzanie jest wykonywane tylko wtedy, gdy **Online** karta została wybrana w bieżącej sesji._

![Okno dialogowe pakiety NuGet z dostępna jest nowa wersja Zarządzanie](./media/manage-nuget-packages-update-notification.png)

Aby wyłączyć funkcję automatycznego sprawdzania aktualizacji, przejdź do okna dialogowego Ustawienia NuGet i usuń zaznaczenie pola wyboru **automatyczne sprawdzenie dostępności aktualizacji**.

![Ustawienia NuGet](./media/nuget-settings.png)

Ta funkcja faktycznie został dodany w NuGet 1.3, ale nie jest widoczna, dopóki aktualizacja 1.3, takich jak NuGet 1.4, została udostępniona.

### <a name="package-manager-dialog-improvements"></a>Ulepszenia okno Menedżera pakietów
* **Nazwy menu ulepszone**: zmieniono opcji Menu, aby uruchomić okno dialogowe z myślą o przejrzystości. Opcja menu jest teraz **Zarządzaj pakietami NuGet**.
* **Okienku szczegółów zostaną wyświetlone najnowszych aktualizacji daty**: NuGet w oknie dialogowym Wyświetla datę ostatniej aktualizacji w okienku szczegółów pakietu podczas **Online** lub **aktualizuje** wybrana karta.
* **Listy tagów wyświetlane**: tagów wyświetla okno dialogowe Nuget.

### <a name="powershell-improvements"></a>Ulepszenia środowiska PowerShell
* **Podpisana skryptów programu PowerShell**: NuGet zawiera podpisanych skryptów programu Powershell umożliwiające użycie w środowiskach bardziej restrykcyjne.
* **Obsługa monitowania**: konsola Menedżera pakietów jest teraz obsługuje monitowania za pośrednictwem `$host.ui.Prompt` i `$host.ui.PromptForChoice` poleceń.
* **Pakiet nazw**: podanie nazwy źródła pakietu jest obsługiwana w przypadku określania źródła pakietu przy użyciu `-Source` flagi.

### <a name="nugetexe-command-line-improvements"></a>ulepszenia wiersza polecenia nuget.exe
* **Niestandardowe polecenia NuGet**: nuget.exe jest rozszerzalny za pomocą polecenia niestandardowych za pomocą MEF.
* **Prostsze przepływu pracy do tworzenia pakietów symbol**: `-Symbols` flagi można zastosować do normalnej oparte na Konwencji strukturę folderów tworzenia pakietu symboli tylko w tym źródle i `.pdb` plików znajdujących się w folderze.
* **Określanie wielu źródeł**: `NuGet install` polecenie obsługuje określania wielu źródeł przy użyciu średników jako ogranicznik lub określając `-Source` wiele razy.
* **Obsługuje uwierzytelnianie serwera proxy**: NuGet 1.4 dodaje obsługę monit o podanie poświadczeń użytkownika, gdy używasz serwera proxy wymagającego uwierzytelniania przy użyciu narzędzia NuGet.
* **nuget.exe zaktualizować fundamentalne zmiany**: `-Self` flaga jest teraz wymagane dla nuget.exe zaktualizowanie się. `nuget.exe Update`teraz przyjmuje ścieżkę do `packages.config` plik i spróbuje pakietów aktualizacji. Należy pamiętać, że ta aktualizacja jest ograniczona, w tym nie będzie: ** zaktualizować, Dodaj, usuń zawartość w pliku projektu.
** Uruchamiać skrypty programu Powershell w pakiecie.

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>Obsługa serwera NuGet wypychanie pakietów przy użyciu nuget.exe
Prosty sposób hosta zawiera NuGet [lekkie internetowe repozytorium NuGet](../hosting-packages/NuGet-Server.md) za pośrednictwem `NuGet.Server` pakietu NuGet. Dzięki NuGet 1.4 lekkie serwer obsługuje wypychanie i usuwanie pakietów przy użyciu nuget.exe.
Najnowszą wersję `NuGet.Server` dodaje nowy `appSetting`o nazwie `apiKey`. Gdy klucz jest pominięty lub pole pozostanie puste, wypychania pakietów w źródle danych jest wyłączona. Ustawienie apiKey wartość (najlepiej silne hasło) umożliwia położenia pakiety przy użyciu nuget.exe.

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Obsługa wersji Mango narzędzia Windows Phone
NuGet jest teraz obsługiwana w wersji narzędzi Windows Phone dla Mango kandydata.
Obecnie narzędzia Windows Phone nie ma obsługi dla Menedżera rozszerzenia usługi Visual Studio tak zainstalować narzędzia do dla Windows Phone NuGet, konieczne może być pobieranie i uruchamianie pliku VSIX ręcznie.

Aby odinstalować program NuGet dla Windows Phone narzędzia, uruchom następujące polecenie.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>Poprawki błędów
NuGet 1.4 miał łącznie 88 stałej elementów roboczych. 71 tych zostały oznaczone jako usterki.

Pełną listę prac elementów usunięto w wersji NuGet 1.4, sprawdź widok [NuGet Tracker problem w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Warto zauważyć, poprawki:

* [Problem 603](http://nuget.codeplex.com/workitem/603): zależności pakietów w różnych repozytoria poprawnie rozpoznaje podczas określania źródła określonego pakietu.
* [Problem 1036](http://nuget.codeplex.com/workitem/1036): dodawanie `NuGet Pack SomeProject.csproj` do po kompilacji już zdarzeń powoduje nieskończoną pętlę.
* [Problem 961](http://nuget.codeplex.com/workitem/961): `-Source` flagi obsługuje ścieżek względnych.

# <a name="nuget-14-update"></a>Aktualizacja NuGet 1.4
Wkrótce po wersji NuGet 1.4 znaleziono kilka problemów, które są ważne rozwiązać problem.
Numer wersji tej aktualizacji 1.4 jest 1.4.20615.9020.

## <a name="bug-fixes"></a>Poprawki błędów
* [Problem 1220](http://nuget.codeplex.com/workitem/1220): pakiet aktualizacji nie jest wykonywana `install.ps1` / `uninstall.ps1` we wszystkich projektach, jeśli istnieje więcej niż jednego projektu
* [Problem 1156](http://nuget.codeplex.com/workitem/1156): konsoli Menedżera pakietów jest zablokowany na W2K3/XP (Jeśli nie zainstalowano programu Powershell 2)
