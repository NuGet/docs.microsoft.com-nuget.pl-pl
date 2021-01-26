---
title: Informacje o wersji narzędzia NuGet 1,4
description: Informacje o wersji programu NuGet 1,4, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e51083be308d97110be9fd67b68f6ba68ccd3df5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777146"
---
# <a name="nuget-14-release-notes"></a>Informacje o wersji narzędzia NuGet 1,4

Informacje o wersji narzędzia [NuGet 1,3](../release-notes/nuget-1.3.md)  |  [Informacje o wersji narzędzia NuGet 1,5](../release-notes/nuget-1.5.md)

Pakiet NuGet 1,4 został wydanych 17 czerwca 2011.

## <a name="features"></a>Funkcje

### <a name="update-package-improvements"></a>Udoskonalenia Update-Package
W pakiecie NuGet 1,4 wprowadzono wiele ulepszeń polecenia Update-Package ułatwiających utrzymywanie pakietów w tej samej wersji w wielu projektach w rozwiązaniu. Na przykład w przypadku uaktualniania pakietu do najnowszej wersji bardzo często zachodzi potrzeba aktualizacji wszystkich projektów z zainstalowanym pakietem do tego samego verision.

To `Update-Package` polecenie ułatwia teraz:

#### <a name="update-all-packages-in-a-single-project"></a>Aktualizuj wszystkie pakiety w pojedynczym projekcie

```
Update-Package -Project MvcApplication1
```

#### <a name="update-a-package-in-all-projects"></a>Aktualizowanie pakietu we wszystkich projektach

```
Update-Package PackageId
```

#### <a name="update-all-packages-in-all-projects"></a>Aktualizuj wszystkie pakiety we wszystkich projektach

```
Update-Package
```

#### <a name="perform-a-safe-update-on-all-packages"></a>Wykonaj "bezpieczną" aktualizację na wszystkich pakietach
`-Safe`Flaga ogranicza uaktualnienia do wersji tylko z tym samym składnikiem wersji głównej i pomocniczej. Na przykład jeśli zainstalowano wersję 1.0.0 pakietu, a w kanale informacyjnym są dostępne wersje 1.0.1, 1.0.2 i 1,1, `-Safe` Flaga aktualizuje pakiet do 1.0.2. Uaktualnienie bez `-Safe` flagi spowoduje uaktualnienie pakietu do najnowszej wersji, 1,1.

```
Update-Package -Safe
```

### <a name="managing-packages-at-the-solution-level"></a>Zarządzanie pakietami na poziomie rozwiązania
Przed pakietem NuGet 1,4 zainstalowanie pakietu w wielu projektach było bardzo uciążliwe przy użyciu okna dialogowego. Wymagane jest uruchomienie okna dialogowego raz dla każdego projektu.

Pakiet NuGet 1,4 dodaje obsługę instalowania/odinstalowywania/aktualizowania pakietów w wielu projektach w tym samym czasie. Wystarczy uruchomić aplikację, klikając rozwiązanie prawym przyciskiem myszy, a następnie wybierając opcję **Zarządzaj pakietami NuGet** .

![Okno dialogowe Zarządzanie pakietami NuGet na poziomie rozwiązania](./media/manage-nuget-packages-solution-dialog.png)

Zauważ, że na pasku tytułu okna dialogowego wyświetlana jest nazwa rozwiązania, a nie nazwa projektu.
Operacje na pakietach udostępniają teraz listę pól wyboru z listą projektów, do których operacja powinna zostać zastosowana.

![Zarządzaj wyborem projektu pakietów NuGet](./media/manage-nuget-packages-project-selection.png)

Aby uzyskać więcej informacji, zobacz temat dotyczący [zarządzania pakietami dla rozwiązania](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).

### <a name="constraining-upgrades-to-allowed-versions"></a>Ograniczanie uaktualnień do dozwolonych wersji
Domyślnie po uruchomieniu `Update-Package` polecenia w pakiecie (lub zaktualizowaniu pakietu przy użyciu okna dialogowego) zostanie ono zaktualizowane do najnowszej wersji w źródle danych. Dzięki nowej obsłudze aktualizacji wszystkich pakietów mogą wystąpić sytuacje, w których chcesz zablokować pakiet do określonego zakresu wersji. Na przykład może być wiadomo, że aplikacja będzie działała tylko w wersji 2. * pakietu, ale nie 3,0 i nowszych. Aby zapobiec przypadkowemu aktualizowaniu pakietu do wersji 3, program NuGet 1,4 dodaje obsługę ograniczania zakresu wersji, do których można uaktualnić pakiety, poprzez ręczne edytowanie `packages.config` pliku przy użyciu nowego `allowedVersions` atrybutu.

Na przykład poniższy przykład pokazuje, jak zablokować `SomePackage` pakiet do wersji 2,0 – 3,0 (wyłączne).
`allowedVersions`Atrybut akceptuje wartości przy użyciu [formatu zakresu wersji](../concepts/package-versioning.md#version-ranges).

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

Należy pamiętać, że w 1,4, blokowanie pakietu do określonego zakresu wersji musi być edytowane ręcznie. W programie NuGet 1,5 planujemy dodanie obsługi umieszczania tego zakresu za pośrednictwem `Install-Package` polecenia.

### <a name="package-visualizer"></a>Wizualizator pakietu
Nowy wizualizator pakietu, uruchamiany za pomocą   ->  opcji menu wizualizator pakietu **Menedżera pakietów biblioteki** narzędzi  ->   , umożliwia łatwe wizualizację wszystkich projektów i ich zależności pakietów w ramach rozwiązania.

_**Ważna Uwaga:** Ta funkcja wykorzystuje obsługę DGML w programie Visual Studio. Tworzenie wizualizacji jest obsługiwane tylko w Visual Studio Ultimate. Wyświetlanie diagramu DGML jest obsługiwane tylko w Visual Studio Premium lub wyższym._

![Wizualizator pakietu](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>Automatyczne sprawdzanie aktualizacji dla okna dialogowego Narzędzia NuGet
Niektóre wersje programu NuGet wprowadzają nowe funkcje wyrażone za pośrednictwem `.nuspec` pliku, które nie są rozpoznawane przez starsze wersje okna dialogowego Narzędzia NuGet.
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
* **Monitowanie o pomoc techniczną**: Konsola Menedżera pakietów obsługuje teraz monitowanie za pomocą `$host.ui.Prompt` `$host.ui.PromptForChoice` poleceń i.
* **Nazwy źródeł pakietów**: podanie nazwy źródła pakietu jest obsługiwane podczas określania źródła pakietu przy użyciu `-Source` flagi.

### <a name="nugetexe-command-line-improvements"></a>Udoskonalenia wiersza polecenia nuget.exe
* **Polecenia niestandardowe NuGet**: nuget.exe jest rozszerzalny za pośrednictwem poleceń niestandardowych przy użyciu MEF.
* **Prostsze przepływ pracy do tworzenia pakietów symboli**: `-Symbols` flagę można zastosować do normalnej Konwencji na podstawie struktury folderów tworzącej pakiet symboli, dołączając tylko źródło i `.pdb` pliki znajdujące się w folderze.
* **Określanie wielu źródeł**: `NuGet install` polecenie obsługuje określanie wielu źródeł przy użyciu średnika jako ogranicznika lub przez `-Source` wiele razy.
* **Obsługa uwierzytelniania serwera proxy**: pakiet NuGet 1,4 dodaje obsługę monitowania o poświadczenia użytkownika w przypadku korzystania z programu NuGet za serwerem proxy wymagającym uwierzytelniania.
* **Zmiana wnuget.exe aktualizacji**: `-Self` flaga jest teraz wymagana do nuget.exe do aktualizacji. `nuget.exe Update` teraz Pobiera ścieżkę do `packages.config` pliku i próbuje zaktualizować pakiety. Należy pamiętać, że ta aktualizacja jest ograniczona, ponieważ nie będzie: * * aktualizowanie, Dodawanie, usuwanie zawartości w pliku projektu.
* * Uruchamianie skryptów programu PowerShell w pakiecie.

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>Obsługa serwera NuGet na potrzeby wypychania pakietów przy użyciu nuget.exe
Pakiet NuGet zawiera prosty sposób hostowania [uproszczonego, opartego na sieci Web repozytorium NuGet](../hosting-packages/nuget-server.md) za pośrednictwem `NuGet.Server` pakietu NuGet. W programie NuGet 1,4 serwer uproszczony obsługuje wypychanie i usuwanie pakietów przy użyciu nuget.exe.
Najnowsza wersja programu `NuGet.Server` dodaje nową `appSetting` nazwę `apiKey` . Gdy klucz zostanie pominięty lub pozostawiono pusty, wypychanie pakietów do źródła danych jest wyłączone. Ustawienie apiKey na wartość (idealnym silnym hasłem) umożliwia wypychanie pakietów przy użyciu nuget.exe.

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

```
vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5
```

## <a name="bug-fixes"></a>Poprawki błędów
Pakiet NuGet 1,4 zawiera łącznie 88 elementów roboczych. 71 z tych elementów zostało oznaczonych jako błędy.

Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 1,4, zobacz [Śledzenie problemów NuGet dla tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Poprawki błędów warto zauważyć:

* [Problem 603](http://nuget.codeplex.com/workitem/603): zależności pakietów między różnymi repozytoriami są rozpoznawane poprawnie podczas określania określonego źródła pakietu.
* [Problem 1036](http://nuget.codeplex.com/workitem/1036): Dodawanie `NuGet Pack SomeProject.csproj` do zdarzenia po kompilacji nie powoduje już pętli nieskończonej.
* [Problem 961](http://nuget.codeplex.com/workitem/961): `-Source` Flaga obsługuje ścieżki względne.

## <a name="nuget-14-update"></a>Aktualizacja NuGet 1,4
Wkrótce po wydaniu programu NuGet 1,4 znaleźliśmy kilka problemów, które były ważne do rozwiązania.
Określony numer wersji tej aktualizacji do 1,4 to 1.4.20615.9020.

### <a name="bug-fixes"></a>Poprawki błędów
* [Problem 1220](http://nuget.codeplex.com/workitem/1220): Update-Package nie `install.ps1` / `uninstall.ps1` jest wykonywane we wszystkich projektach, gdy istnieje więcej niż jeden projekt
* [Problem 1156](http://nuget.codeplex.com/workitem/1156): Konsolidacja Menedżera pakietów została zablokowana na W2K3/XP (gdy program PowerShell 2 nie jest zainstalowany)
