---
title: 3.5 informacje o wersji Beta2
description: Informacje o wersji programu NuGet 3.5 Beta 2 tym znanych problemów, poprawki, dodatkowe funkcje i dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 08bbae00a3e63c2a1ff42d5cc04981eb02966850
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822347"
---
# <a name="nuget-35-beta2-release-notes"></a>Informacje o wersji 3.5 Beta2 NuGet

[Informacje o wersji 3.5 Beta NuGet](../release-notes/nuget-3.5-Beta.md) | [informacje o wersji 3.5 RC NuGet](../release-notes/nuget-3.5-RC.md)

NuGet 3.5 Beta 2 RTM wydania dla programu Visual Studio 2013 i nuget.exe 27 czerwca 2016 r.

[Pełny wykaz zmian](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Lista problemów](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Poprawki błędów

* Błąd zaktualizowane wiadomości do Brak obsługi decrpytion hasła w .NET Core dla źródeł uwierzytelnionych - [#2942](https://github.com/NuGet/Home/issues/2942)

* Get-pakiet konsoli Menedżera pakietów nie powiedzie się, jeśli projekt .NET Core jest otwarty — [#2932](https://github.com/NuGet/Home/issues/2932)

* Usuń nieprawidłowa obsługa 403 w poleceniu wypychania NuGet [#2910](https://github.com/NuGet/Home/issues/2910)

* Rozwiązywanie problemów w odinstalowanie pakietów w rozwiązaniu powiązany do kontroli źródła TFS, gdy disableSourceControlIntegration jest ustawiona na true - [#2739](https://github.com/NuGet/Home/issues/2739)

* Napraw pakiet aktualizacji do pakietów niebędące kontem — [#2724](https://github.com/NuGet/Home/issues/2724)

* Użyj poziom szczegółowości MSBuild, aby ustawić poziom rejestrowania Menedżera pakietów Nuget akcji UI - [#2705](https://github.com/NuGet/Home/issues/2705)

* Konfiguracja nuget projektu poprawka jest nieprawidłowy błąd w projektach witryny sieci Web - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* Rozwiązywanie problemów z dodatkiem Service pack z `.csproj` gdy pliki zawartości są uwzględnione - [#2658](https://github.com/NuGet/Home/issues/2658)

* DefaultPushSource w `NuGetDefaults.Config` (`ProgramData\NuGet`) nie działa — [#2653](https://github.com/NuGet/Home/issues/2653)

* Rozwiąż problem w wersji Nuget 3.4.3 - wartość nie może być pusty w tworzeniu pakietu - [#2648](https://github.com/NuGet/Home/issues/2648)

* Przywracanie używa przechowywanych poświadczeń z pliku Nuget.Config dla źródła danych programu VSTS — [#2647](https://github.com/NuGet/Home/issues/2647)

* Wydajność — poprawka alokacje nadmierne w kodzie porównania wersji — [#2632](https://github.com/NuGet/Home/issues/2632)

* Rozwiązywanie problemów, gdy wiele wystąpień nuget.exe próbuje zainstalować tego samego pakietu równolegle - [#2628](https://github.com/NuGet/Home/issues/2628)

* Wydajność — pamięć podręczna informacji o zależnościach wielu projektów operacji - [#2619](https://github.com/NuGet/Home/issues/2619)

* Rozwiąż problem w przypadku, gdy pakiet źródła można dodać z ustawień, gdy lista źródła jest pusty — [#2617](https://github.com/NuGet/Home/issues/2617)

* Usuń błąd Misleading, podczas próby zainstalowania pakietu, który jest zależny od czasu projektowania fasad - [#2594](https://github.com/NuGet/Home/issues/2594)

* Instalowanie pakietu z konsoli PackageManager, ustawienie "All" próbuje tylko pierwsze źródło - [#2557](https://github.com/NuGet/Home/issues/2557)

* Rozwiązywanie problemów z pakietami, które plików razy zapisu w przyszłości (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)

* Wyświetl wyjątku, gdy nastąpiło uszkodzenie projektów znajdowanie polecenia update - [#2418](https://github.com/NuGet/Home/issues/2418)

* Zawartość pakietu jest nie została poprawnie przywrócona podczas instalowania pakietu z v3.3 nuget + źródła danych z argumentem - NoCache, jeśli pakiet zawiera `.nupkg` pliki - [#2354](https://github.com/NuGet/Home/issues/2354)

* Usuń problem z pakietem instalacji (wszystkie źródła), gdy źródło 1 - brakuje pakietu [#2322](https://github.com/NuGet/Home/issues/2322)

* Zainstaluj bloków, jeśli pojedyncze źródło odmawia autoryzacji - [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` Wersja zakresu powinny zastępować wersja - IncludeReferencedProjects - [#1983](https://github.com/NuGet/Home/issues/1983)

* Aktualizacja NuGet 3.3.0 "... dodatkowe ograniczenie zdefiniowane w pliku packages.config uniemożliwia wykonanie tej operacji." - [#1816](https://github.com/NuGet/Home/issues/1816)

* Aktualizacja nuget.exe porzuca silna nazwa zestawu i atrybut Private. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Rozwiązywanie problemów z względna ścieżka do pliku dla "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)

* Poprawy aktualizacji komunikaty o błędach rozpoznawania - [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Funkcje i zmiany sposobu działania

* nuget.exe push - parametr limitu czasu nie działa — [#2785](https://github.com/NuGet/Home/issues/2785)

* nie tworzy przywracania nuget.exe `.props` i `.targets` pliki `.nuproj` projektów (Regresja w v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)

* Należy rozszerzeń interfejsu API, aby porównać struktury z Importy — [#2633](https://github.com/NuGet/Home/issues/2633)

* Ukryj opcje zależności, korzystając z `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Wydrukować nagłówka wersji nuget.exe w szczegółowych danych wyjściowych - [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet należy dodać obsługę /nativeassets/ /runtimes/ {rid} {txm} / - [#2782](https://github.com/NuGet/Home/issues/2782)