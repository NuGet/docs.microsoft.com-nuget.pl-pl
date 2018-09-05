---
title: 3.5 informacje o wersji Beta2
description: Informacje o wersji programu NuGet 3.5 Beta 2, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b47939e2fafc11823c41a849b3c58bbf0800ada
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551994"
---
# <a name="nuget-35-beta2-release-notes"></a>Informacje o wersji programu NuGet 3.5 Beta2.

[Informacje o wersji 3.5 Beta NuGet](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5 RC wersji](../release-notes/nuget-3.5-RC.md)

NuGet 3.5 Beta 2 RTM została opublikowana 27 czerwca 2016 r dla programu Visual Studio 2013 i nuget.exe

[Pełny dziennik zmian](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Lista problemów](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Poprawki błędów

* Komunikat o błędzie zaktualizowane na brak obsługi decrpytion hasła w programie .NET Core dla uwierzytelnione kanały informacyjne - [#2942](https://github.com/NuGet/Home/issues/2942)

* Konsola Menedżera pakietów Get-Package zakończy się niepowodzeniem, jeśli projekt .NET Core jest otwarty — [#2932](https://github.com/NuGet/Home/issues/2932)

* Napraw nieprawidłowa obsługa 403 w poleceniu wypychania NuGet [#2910](https://github.com/NuGet/Home/issues/2910)

* Rozwiązywanie problemów w odinstalowywanie pakietów w rozwiązaniu powiązany do kontroli źródła programu TFS, gdy disableSourceControlIntegration jest ustawiona na wartość true - [#2739](https://github.com/NuGet/Home/issues/2739)

* Napraw aktualizacji pakietu uwzględniać konto pakiety-target - [#2724](https://github.com/NuGet/Home/issues/2724)

* Użyj poziom szczegółowości MSBuild, aby ustawić poziom rejestrowania dla Menedżera pakietów Nuget, akcje interfejsu użytkownika — [#2705](https://github.com/NuGet/Home/issues/2705)

* Konfiguracja NuGet poprawka jest nieprawidłowy w projektów witryny sieci Web — VS 2015 VSIX (v3.4.3) — [#2667](https://github.com/NuGet/Home/issues/2667)

* Rozwiązywanie problemów z dodatkiem Service pack z `.csproj` gdy pliki zawartości są uwzględnione - [#2658](https://github.com/NuGet/Home/issues/2658)

* DefaultPushSource w `NuGetDefaults.Config` (`ProgramData\NuGet`) nie działa — [#2653](https://github.com/NuGet/Home/issues/2653)

* Rozwiązać problem w wersji programu Nuget 3.4.3 - wartość nie może być pusta przy tworzeniu pakietu - [#2648](https://github.com/NuGet/Home/issues/2648)

* Przywracania przy użyciu przechowywanych poświadczeń z pliku Nuget.Config dla źródeł danych usługi VSTS — [#2647](https://github.com/NuGet/Home/issues/2647)

* Wyników — poprawki alokacje nadmierne w kodzie porównania wersji - [#2632](https://github.com/NuGet/Home/issues/2632)

* Rozwiązywanie problemów, gdy wiele wystąpień programu nuget.exe próbuje zainstalować ten sam pakiet równolegle - [#2628](https://github.com/NuGet/Home/issues/2628)

* Wydajność — pamięć podręczna informacji o zależnościach dla operacji obejmujących wiele projektów — [#2619](https://github.com/NuGet/Home/issues/2619)

* Rozwiąż problem w przypadku, gdy nie można źródeł pakietów można dodać z ustawień, gdy lista źródłowa jest pusta — [#2617](https://github.com/NuGet/Home/issues/2617)

* Napraw błąd Misleading, podczas próby zainstalowania pakietu, który zależy od czasu projektowania fasad - [#2594](https://github.com/NuGet/Home/issues/2594)

* Instalowanie pakietu z poziomu konsoli PackageManager z ustawieniem "All" próbuje tylko pierwsze źródło - [#2557](https://github.com/NuGet/Home/issues/2557)

* Rozwiązywanie problemów z pakietami, które znajdują się pliki z czasem zapisu w przyszłości (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)

* Wyświetlanie wyjątku, gdy wystąpi awaria znajdowanie projektów w polecenia update - [#2418](https://github.com/NuGet/Home/issues/2418)

* Zawartość pakietu jest nie została poprawnie przywrócona podczas instalowania pakietu z v3.3 nuget + źródła danych z argumentem - Właściwość NoCache Jeśli pakiet zawiera `.nupkg` plików — [#2354](https://github.com/NuGet/Home/issues/2354)

* Rozwiązanie problemu z pakietu instalacji (wszystkich źródeł), gdy brak pakietu ze źródła 1 - [#2322](https://github.com/NuGet/Home/issues/2322)

* Zainstaluj bloków, jeśli pojedyncze źródło odmawia autoryzacji - [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` zakres powinien przesłonić - IncludeReferencedProjects wersja — wersja [#1983](https://github.com/NuGet/Home/issues/1983)

* Aktualizacji NuGet 3.3.0 kończy się niepowodzeniem z "… dodatkowe ograniczenia zdefiniowane w pliku packages.config zapobiega tej operacji." - [#1816](https://github.com/NuGet/Home/issues/1816)

* Aktualizacja nuget.exe spada, silna nazwa zestawu i atrybut Private. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Rozwiązywanie problemów z względna ścieżka do pliku dla "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)

* Poprawić komunikaty o błędach rozpoznawania Update - [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Funkcje i zmiany sposobu działania

* wypychane nuget.exe — parametr limitu czasu nie działa — [#2785](https://github.com/NuGet/Home/issues/2785)

* Przywracanie nuget.exe nie generuje `.props` i `.targets` pliki `.nuproj` projektów (Regresja w v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)

* Potrzebujesz rozszerzeń interfejsu API, aby porównać platform z import - [#2633](https://github.com/NuGet/Home/issues/2633)

* Ukryj opcje zależność, korzystając z `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Wydrukować nuget.exe nagłówka wersji w szczegółowe dane wyjściowe — [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet należy dodać obsługę /nativeassets/ /runtimes/ {rid} {txm} / - [#2782](https://github.com/NuGet/Home/issues/2782)