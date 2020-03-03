---
title: Informacje o wersji narzędzia NuGet 1,4
description: Informacje o wersji programu NuGet 1,4, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b31c02b9251d6d45d952fdf8b111493495d57ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230710"
---
# <a name="nuget-14-release-notes"></a>Informacje o wersji narzędzia NuGet 1,4

[Informacje o wersji pakietu nuget 1,3](../release-notes/nuget-1.3.md) | [Informacje o wersji narzędzia NuGet 1,5](../release-notes/nuget-1.5.md)

Pakiet NuGet 1,4 został wydanych 17 czerwca 2011.

## <a name="features"></a>Funkcje

### <a name="update-package-improvements"></a>Udoskonalenia aktualizacji pakietu
W pakiecie NuGet 1,4 wprowadzono wiele ulepszeń polecenia Update-Package, dzięki czemu można łatwiej utrzymywać pakiety w tej samej wersji w wielu projektach w rozwiązaniu. Na przykład w przypadku uaktualniania pakietu do najnowszej wersji bardzo często zachodzi potrzeba aktualizacji wszystkich projektów z zainstalowanym pakietem do tego samego verision.

`Update-Package` polecenie teraz ułatwia:

#### <a name="update-all-packages-in-a-single-project"></a>Aktualizuj wszystkie pakiety w pojedynczym projekcie

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>Aktualizowanie pakietu we wszystkich projektach

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>Aktualizuj wszystkie pakiety we wszystkich projektach

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>Wykonaj "bezpieczną" aktualizację na wszystkich pakietach
Flaga `-Safe` ogranicza uaktualnienia do wersji tylko z tym samym składnikiem wersji głównej i pomocniczej. Na przykład jeśli jest zainstalowana wersja 1.0.0 pakietu, a w kanale informacyjnym są dostępne wersje 1.0.1, 1.0.2 i 1,1, flaga `-Safe` aktualizuje pakiet do 1.0.2. Uaktualnienie bez flagi `-Safe` uaktualni pakiet do najnowszej wersji, 1,1.

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>Zarządzanie pakietami na poziomie rozwiązania
Przed pakietem NuGet 1,4 zainstalowanie pakietu w wielu projektach było bardzo uciążliwe przy użyciu okna dialogowego. Wymagane jest uruchomienie okna dialogowego raz dla każdego projektu.

Pakiet NuGet 1,4 dodaje obsługę instalowania/odinstalowywania/aktualizowania pakietów w wielu projektach w tym samym czasie. Wystarczy uruchomić aplikację, klikając rozwiązanie prawym przyciskiem myszy, a następnie wybierając opcję **Zarządzaj pakietami NuGet** .

![Okno dialogowe Zarządzanie pakietami NuGet na poziomie rozwiązania](./media/manage-nuget-packages-solution-dialog.png)

Zauważ, że na pasku tytułu okna dialogowego wyświetlana jest nazwa rozwiązania, a nie nazwa projektu.
Operacje na pakietach udostępniają teraz listę pól wyboru z listą projektów, do których operacja powinna zostać zastosowana.

![Zarządzaj wyborem projektu pakietów NuGet](./media/manage-nuget-packages-project-selection.png)

Aby uzyskać więcej informacji, zobacz temat dotyczący [zarządzania pakietami dla rozwiązania](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).

### <a name="constraining-upgrades-to-allowed-versions"></a>Ograniczanie uaktualnień do dozwolonych wersji
Domyślnie po uruchomieniu polecenia `Update-Package` w pakiecie (lub zaktualizowaniu pakietu przy użyciu okna dialogowego) zostanie on zaktualizowany do najnowszej wersji w źródle danych. Dzięki nowej obsłudze aktualizacji wszystkich pakietów mogą wystąpić sytuacje, w których chcesz zablokować pakiet do określonego zakresu wersji. Na przykład może być wiadomo, że aplikacja będzie działała tylko w wersji 2. * pakietu, ale nie 3,0 i nowszych. Aby zapobiec przypadkowemu aktualizowaniu pakietu do 3, program NuGet 1,4 dodaje obsługę ograniczania zakresu wersji, do których można uaktualnić pakiety, poprzez ręczne edytowanie pliku `packages.config` przy użyciu nowego atrybutu `allowedVersions`.

Na przykład poniższy przykład pokazuje, jak zablokować pakiet `SomePackage` wersja zakresu 2,0 – 3,0 (na wyłączność).
Atrybut `allowedVersions` akceptuje wartości przy użyciu [formatu zakresu wersji](../concepts/package-versioning.md#version-ranges).

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

Należy pamiętać, że w 1,4, blokowanie pakietu do określonego zakresu wersji musi być edytowane ręcznie. W programie NuGet 1,5 planujemy dodanie obsługi umieszczania tego zakresu za pośrednictwem polecenia `Install-Package`.

### <a name="package-visualizer"></a>Wizualizator pakietu
Nowy wizualizator pakietu, uruchamiany za pośrednictwem opcji **narzędzia** -> **biblioteka Menedżer pakietów** -> menu **wizualizator pakietu** , pozwala łatwo wizualizować wszystkie projekty i ich zależności pakietu w ramach rozwiązania.

_**Ważna Uwaga:** Ta funkcja wykorzystuje obsługę DGML w programie Visual Studio. Tworzenie wizualizacji jest obsługiwane tylko w Visual Studio Ultimate. Wyświetlanie diagramu DGML jest obsługiwane tylko w Visual Studio Premium lub wyższym._

![Wizualizator pakietu](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>Automatyczne sprawdzanie aktualizacji dla okna dialogowego Narzędzia NuGet
Niektóre wersje programu NuGet wprowadzają nowe funkcje wyrażone za pośrednictwem pliku `.nuspec`, które nie są rozpoznawane przez starsze wersje okna dialogowego Narzędzia NuGet.
Przykładem jest wprowadzenie w programie NuGet 1,4 do [określania zestawów struktury](../release-notes/nuget-1.2.md#framework-assembly-refs).
Z tego względu należy użyć najnowszej wersji programu NuGet, aby upewnić się, że można używać pakietów korzystających z najnowszych funkcji.
Aby aktualizacje NuGet były bardziej widoczne, okno dialogowe NuGet zawiera logikę do wyróżnienia, gdy dostępna jest nowsza wersja.

_**Uwaga**: sprawdzanie jest wykonywane tylko wtedy, gdy w bieżącej sesji została wybrana karta **online** ._

![Okno dialogowe zarządzania pakietami NuGet z dostępną nową wersją](./media/manage-nuget-packages-update-notification.png)

Aby wyłączyć automatyczne sprawdzanie aktualizacji, przejdź do okna dialogowego Ustawienia NuGet i usuń zaznaczenie pola **wyboru Automatycznie sprawdzaj dostępność aktualizacji**.

![Ustawienia narzędzia NuGet](./media/nuget-settings.png)

Ta funkcja została faktycznie dodana w programie NuGet 1,3, ale nie będzie widoczna, oczywiście dopóki nie zostanie udostępniona aktualizacja 1,3, taka jak NuGet 1,4.

### <a name="package-manager-dialog-improvements"></a>Ulepszenia okna dialogowego Menedżera pakietów
* **Ulepszone nazwy menu**: opcje menu umożliwiające uruchomienie okna dialogowego zostały zmienione pod kątem przejrzystości. Opcja menu umożliwia teraz **Zarządzanie pakietami NuGet**.
* W **okienku szczegółów jest wyświetlana Najnowsza Data aktualizacji**: w oknie dialogowym narzędzia NuGet jest wyświetlana data najnowszej aktualizacji w okienku szczegółów pakietu po wybraniu karty **online** lub **aktualizacje** .
* **Lista wyświetlanych tagów**: w oknie dialogowym NuGet są wyświetlane tagi.

### <a name="powershell-improvements"></a>Ulepszenia programu PowerShell
* **Podpisane skrypty programu PowerShell**: pakiet NuGet obejmuje podpisane skrypty programu PowerShell umożliwiające użycie w bardziej restrykcyjnych środowiskach.
* **Monitowanie o pomoc techniczną**: Konsola Menedżera pakietów obsługuje teraz monitowanie za pomocą poleceń `$host.ui.Prompt` i `$host.ui.PromptForChoice`.
* **Nazwy źródeł pakietów**: podanie nazwy źródła pakietu jest obsługiwane podczas określania źródła pakietu przy użyciu flagi `-Source`.

### <a name="nugetexe-command-line-improvements"></a>udoskonalenia wiersza polecenia NuGet. exe
* **Polecenia niestandardowe NuGet**: NuGet. exe jest rozszerzalny za pośrednictwem poleceń niestandardowych przy użyciu MEF.
* **Prostsze przepływ pracy do tworzenia pakietów symboli**: Flaga `-Symbols` może być stosowana do normalnej struktury folderów opartej na Konwencji tworzącej pakiet symboli, dołączając tylko pliki źródłowe i `.pdb` w folderze.
* **Określanie wielu źródeł**: polecenie `NuGet install` obsługuje określanie wielu źródeł przy użyciu średnika jako ogranicznika lub przez określenie `-Source` wiele razy.
* **Obsługa uwierzytelniania serwera proxy**: pakiet NuGet 1,4 dodaje obsługę monitowania o poświadczenia użytkownika w przypadku korzystania z programu NuGet za serwerem proxy wymagającym uwierzytelniania.
* **nieprzerwana Aktualizacja programu NuGet. exe**: Flaga `-Self` jest teraz wymagana dla narzędzia NuGet. exe, aby można było zaktualizować siebie. `nuget.exe Update` teraz przyjmuje ścieżkę do pliku `packages.config` i spróbuje zaktualizować pakiety. Należy pamiętać, że ta aktualizacja jest ograniczona, ponieważ nie będzie: * * aktualizowanie, Dodawanie, usuwanie zawartości w pliku projektu.
* * Uruchamianie skryptów programu PowerShell w pakiecie.

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>Obsługa serwera NuGet na potrzeby wypychania pakietów przy użyciu NuGet. exe
Pakiet NuGet zawiera prosty sposób hostowania [uproszczonego, opartego na sieci Web repozytorium NuGet](../hosting-packages/nuget-server.md) za pośrednictwem pakietu NuGet `NuGet.Server`. W programie NuGet 1,4 serwer uproszczony obsługuje wypychanie i usuwanie pakietów przy użyciu programu NuGet. exe.
Najnowsza wersja `NuGet.Server` dodaje nowe `appSetting`o nazwie `apiKey`. Gdy klucz zostanie pominięty lub pozostawiono pusty, wypychanie pakietów do źródła danych jest wyłączone. Ustawienie apiKey na wartość (idealnym silnym hasłem) umożliwia wypychanie pakietów przy użyciu NuGet. exe.

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Obsługa narzędzi Windows Phone Tools mango Edition
Pakiet NuGet jest teraz obsługiwany w wersji Release Candidate narzędzi Windows Phone Tools for mango.
Obecnie narzędzia Windows Phone nie obsługują Menedżera rozszerzeń programu Visual Studio, więc aby można było zainstalować pakiet NuGet dla Windows Phone narzędzi, może być konieczne ręczne pobranie i uruchomienie VSIX.

Aby odinstalować pakiet NuGet dla narzędzi Windows Phone, uruchom następujące polecenie.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>Poprawki błędów
Pakiet NuGet 1,4 zawiera łącznie 88 elementów roboczych. 71 z tych elementów zostało oznaczonych jako błędy.

Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 1,4, zobacz [Śledzenie problemów NuGet dla tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Poprawki błędów warto zauważyć:

* [Problem 603](http://nuget.codeplex.com/workitem/603): zależności pakietów między różnymi repozytoriami są rozpoznawane poprawnie podczas określania określonego źródła pakietu.
* [Problem 1036](http://nuget.codeplex.com/workitem/1036): Dodawanie `NuGet Pack SomeProject.csproj` do zdarzenia po kompilacji nie powoduje już pętli nieskończonej.
* [Problem 961](http://nuget.codeplex.com/workitem/961): Flaga `-Source` obsługuje ścieżki względne.

## <a name="nuget-14-update"></a>Aktualizacja NuGet 1,4
Wkrótce po wydaniu programu NuGet 1,4 znaleźliśmy kilka problemów, które były ważne do rozwiązania.
Określony numer wersji tej aktualizacji do 1,4 to 1.4.20615.9020.

### <a name="bug-fixes"></a>Poprawki błędów
* [Problem 1220](http://nuget.codeplex.com/workitem/1220): pakiet aktualizacji nie jest wykonywany `install.ps1`/`uninstall.ps1` we wszystkich projektach, gdy istnieje więcej niż jeden projekt
* [Problem 1156](http://nuget.codeplex.com/workitem/1156): Konsolidacja Menedżera pakietów została zablokowana na W2K3/XP (gdy program PowerShell 2 nie jest zainstalowany)
