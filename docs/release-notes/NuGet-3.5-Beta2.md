---
title: 3,5 beta2 — informacje o wersji
description: Informacje o wersji programu NuGet 3,5 Beta 2, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2aa92d4ef97acb2b4b70388cd4d580e7094aea45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776392"
---
# <a name="nuget-35-beta2-release-notes"></a>Informacje o wersji narzędzia NuGet 3,5 beta2

[NuGet 3,5 — informacje](../release-notes/nuget-3.5-Beta.md)  |  o wersji beta Pakiet [NuGet 3,5 — informacje o wersji RC](../release-notes/nuget-3.5-RC.md)

Pakiet NuGet 3,5 Beta 2 RTM został wydano 27 czerwca 2016 dla Visual Studio 2013 i nuget.exe

[Pełny dziennik zmian](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Lista problemów](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Poprawki błędów

* Zaktualizowano komunikat o błędzie w celu braku obsługi hasła decrpytion w programie .NET Core dla uwierzytelnionych kanałów informacyjnych — [#2942](https://github.com/NuGet/Home/issues/2942)

* Get-Package konsoli Menedżera pakietów kończy się niepowodzeniem, jeśli projekt .NET Core jest otwarty — [#2932](https://github.com/NuGet/Home/issues/2932)

* Naprawianie niepoprawnej obsługi 403 w poleceniu wypychania NuGet [#2910](https://github.com/NuGet/Home/issues/2910)

* Rozwiązywanie problemów podczas odinstalowywania pakietów w rozwiązaniu związanym z kontrolą źródła TFS, gdy disableSourceControlIntegration jest ustawiona na true — [#2739](https://github.com/NuGet/Home/issues/2739)

* Napraw aktualizację pakietu, aby wziąć pod uwagę Pakiety inne niż docelowe — [#2724](https://github.com/NuGet/Home/issues/2724)

* Poziom szczegółowości programu MSBuild umożliwia ustawianie poziomu rejestratora dla akcji interfejsu użytkownika Menedżera pakietów NuGet — [#2705](https://github.com/NuGet/Home/issues/2705)

* Naprawa konfiguracji NuGet jest nieprawidłowa w projektach witryny sieci Web — VS 2015 VSIX (v 3.4.3) — [#2667](https://github.com/NuGet/Home/issues/2667)

* Rozwiązywanie problemów z pakietami z `.csproj` uwzględnieniem plików zawartości — [#2658](https://github.com/NuGet/Home/issues/2658)

* DefaultPushSource w `NuGetDefaults.Config` ( `ProgramData\NuGet` ) nie działa — [#2653](https://github.com/NuGet/Home/issues/2653)

* Usuwanie problemu w programie NuGet 3.4.3 wersja nie może mieć wartości null podczas tworzenia pakietu- [#2648](https://github.com/NuGet/Home/issues/2648)

* Funkcja Restore używa przechowywanych poświadczeń z Nuget.Config dla źródeł danych VSTS — [#2647](https://github.com/NuGet/Home/issues/2647)

* Wydajność — napraw nadmierne alokacje w wersji comparsion Code- [#2632](https://github.com/NuGet/Home/issues/2632)

* Rozwiązywanie problemów, gdy wiele wystąpień nuget.exe próbuje zainstalować ten sam pakiet w równoległej [#2628](https://github.com/NuGet/Home/issues/2628)

* Wydajność — informacje o zależnościach pamięci podręcznej dla operacji wieloprojektowych — [#2619](https://github.com/NuGet/Home/issues/2619)

* Rozwiąż problem polegający na tym, że nie można źródła pakietów zostaną dodane z ustawień, gdy lista źródłowa jest pusta — [#2617](https://github.com/NuGet/Home/issues/2617)

* Naprawianie błędu mylącego podczas próby zainstalowania pakietu, który zależy od [#2594](https://github.com/NuGet/Home/issues/2594) fasad czasu projektowania

* Instalowanie pakietu z konsoli pakietu Packagemanager z ustawieniem "All" powoduje tylko próbę pierwszego źródła — [#2557](https://github.com/NuGet/Home/issues/2557)

* Rozwiązywanie problemów z pakietami zawierającymi pliki z godzinami zapisu w przyszłości (mono) — [#2518](https://github.com/NuGet/Home/issues/2518)

* Wyświetl wyjątek, jeśli wystąpił błąd podczas znajdowania projektów w ramach polecenia Update — [#2418](https://github.com/NuGet/Home/issues/2418)

* Zawartość pakietu nie jest przywracana poprawnie podczas instalowania pakietu z programu NuGet v 3.3 + ze źródła danych argument-nocache, gdy pakiet zawiera `.nupkg` pliki- [#2354](https://github.com/NuGet/Home/issues/2354)

* Rozwiązywanie problemu z instalacją pakietu (wszystkie źródła), gdy brakuje pakietu z 1 źródła — [#2322](https://github.com/NuGet/Home/issues/2322)

* Zainstaluj bloki w przypadku niepowodzenia autoryzacji pojedynczego źródła — [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` zakres wersji powinien przesłonić IncludeReferencedProjects wersji [#1983](https://github.com/NuGet/Home/issues/1983)

* Aktualizacja NuGet 3.3.0 kończy się niepowodzeniem z "dodatkowym ograniczeniem... zdefiniowane w packages.config uniemożliwia wykonanie tej operacji ". - [#1816](https://github.com/NuGet/Home/issues/1816)

* nuget.exe Update odrzuca silną nazwę i atrybut prywatny zestawu. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Rozwiązywanie problemów ze względną ścieżką pliku dla "DefaultPushSource" — [#1746](https://github.com/NuGet/Home/issues/1746)

* Optymalizowanie komunikatów o błędach rozwiązywania problemów dotyczących aktualizacji — [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Zmiany funkcji i zachowania

* nuget.exe parametr limitu czasu wypychania nie działa — [#2785](https://github.com/NuGet/Home/issues/2785)

* Przywracanie nuget.exe nie produkuje `.props` i `.targets` plików dla `.nuproj` projektów (regresja w v 3.4.3.855) — [#2711](https://github.com/NuGet/Home/issues/2711)

* Potrzebny interfejs API rozszerzalności do porównywania platform z importami — [#2633](https://github.com/NuGet/Home/issues/2633)

* Ukryj Opcje zależności przy użyciu `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Drukuj nagłówek nuget.exe wersji w szczegółowych danych wyjściowych — [#1887](https://github.com/NuGet/Home/issues/1887)

* Pakiet NuGet powinien dodać obsługę/Runtimes/{RID}/nativeassets/{TXM}/- [#2782](https://github.com/NuGet/Home/issues/2782)