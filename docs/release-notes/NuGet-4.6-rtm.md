---
title: Informacje o wydaniu programu NuGet 4.6 RTM
description: Informacje o wersji dla NuGet 4.6.0, w tym znane problemy, poprawki błędów, dodane funkcje i BDR.
author: anangaur
ms.author: anangaur
ms.date: 3/7/2018
ms.topic: conceptual
ms.openlocfilehash: eacd29d4c9340a0f015fcdf6c5b9dd41bf781419
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498682"
---
# <a name="nuget-46-release-notes"></a>Informacje o wersji nuGet 4.6

[Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z [NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe).

## <a name="summary-whats-new-in-460"></a>Krótki opis: Co nowego w 4.6.0

* Dodaliśmy obsługę [podpisywania pakietów](../create-packages/sign-a-package.md).
* Visual Studio 2017 i nuget.exe teraz weryfikuje integralność pakietu przed zainstalowaniem, przywracając pakiety dla [podpisanych pakietów](../reference/signed-packages-reference.md).
* Poprawiliśmy wydajność kolejnych przywracań.

## <a name="summary-whats-new-in-463"></a>Krótki opis: Co nowego w 4.6.3

* Poprawka zabezpieczeń: Uprawnienia do plików utworzonych wewnątrz ~/.nuget są zbyt otwarte [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-464"></a>Krótki opis: Co nowego w 4.6.4

* Poprawka zabezpieczeń: Pliki wewnątrz nupkgs może mieć względną ścieżkę powyżej katalogu NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Znane problemy

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemy z .NET Standard 2.0 z .NET Framework & NuGet 

.NET Standard & jego narzędzia został zaprojektowany w taki sposób, że projekty przeznaczone dla platformy .NET Framework 4.6.1 mogą korzystać z pakietów NuGet & projektów przeznaczonych dla .NET Standard 2.0 lub wcześniejszych. [W tym dokumencie](https://github.com/dotnet/standard/issues/481) podsumowano problemy związane z tym scenariuszem, plan ich rozwiązania i obejścia, które można wdrożyć przy dzisiejszym stanie narzędzia.

## <a name="top-issues-fixed-in-this-release"></a>Najważniejsze problemy rozwiązane w tej wersji

**Poprawki wydajności**

* Nie zapisuj plików zasobów, gdy nie ma żadnych zmian - [#6491](https://github.com/NuGet/Home/issues/6491)
* Przywracanie powoduje dodatkowe MSBuild ocen, gdy TFM projektów podrzędnych nie są zgodne z projektu nadrzędnego — [#6311](https://github.com/NuGet/Home/issues/6311)
* Popraw przywracanie noop perf, optymalizując tworzenie specyfikacji wykresu zależności - [#6252](https://github.com/NuGet/Home/issues/6252)

**Błędów**

* Push do folderu lokalnego pozostawia nupkg zablokowane - [#6325](https://github.com/NuGet/Home/issues/6325)
* Implementacja wtyczki NuGet: wiele problemów - [#6149](https://github.com/NuGet/Home/issues/6149)
* UIHang — usuń wywołanie usługi kwerendy z inicjowania MEF w programie VSSolutionManager — [#6110](https://github.com/NuGet/Home/issues/6110)
* Wyjątek raportowania błędów dla anulowane zadanie pobierania pakietu - [#6096](https://github.com/NuGet/Home/issues/6096)
* NuGet.exe zastępuje "+" "%2B" w nazwie zestawu - [#5956](https://github.com/NuGet/Home/issues/5956)
* Fn+F1 nie ma odpowiedniej strony pomocy dla pm ui i konsoli - [#5912](https://github.com/NuGet/Home/issues/5912)
* Vs NuGet zapisuje ścieżki bezwzględne do plików projektu w określonych okolicznościach - [#5888](https://github.com/NuGet/Home/issues/5888)
* Poprawka regresja 4.3 - Symbole zastępcze $product$ i $AssemblyGuid$ nie zostały zastąpione w contentfile poprzez transformację - [#5880](https://github.com/NuGet/Home/issues/5880)
* przywracanie dotnet z wieloma źródłami ulega awarii - [#5817](https://github.com/NuGet/Home/issues/5817)
* Pakiet powinien ponownie ocenić wersje projektu, aby umożliwić przechowywanie wersji git - [#4790](https://github.com/NuGet/Home/issues/4790)
* Popraw trudne do zrozumienia błędy podczas instalowania niezgodnego pakietu - [#4555](https://github.com/NuGet/Home/issues/4555)
* TemplateWizard potrzebuje opcji, aby zainstalować pakiety jako PackageReferences - [#4549](https://github.com/NuGet/Home/issues/4549)
* Pliki rekwizytów dostarczonych przez pakiet są ignorowane, gdy program MSBuild.exe jest uruchamiany spoza wiersza polecenia dewelopera — [#4530](https://github.com/NuGet/Home/issues/4530)
* Napraw komunikat o błędzie problemu podczas odwoływania się do biblioteki standardowej platformy .NET, która nie ma zastosowania do projektu — [#4423](https://github.com/NuGet/Home/issues/4423)
* dotnet dodać pakiet nie powiedzie się dla pakietu kierowania profil przenośny z mało wskazówek - [#4349](https://github.com/NuGet/Home/issues/4349)
* dotnet pack - brakujący sufiks wersji w Programie ProjectReference - [#4337](https://github.com/NuGet/Home/issues/4337)
* Błędy kompilacji i awaria programu VS z szablonem .NET Core — [#3973](https://github.com/NuGet/Home/issues/3973)
* Nie można załadować indeksu usługi dla źródła https:* — [#3681](https://github.com/NuGet/Home/issues/3681)
* nuget.exe list -allversions nie działa - [#3441](https://github.com/NuGet/Home/issues/3441)
* Komunikat o błędzie rozpoznawania zależności wprowadzający w błąd — [#2984](https://github.com/NuGet/Home/issues/2984)
* nuget.exe restore nie tworzy .props i .targets plików dla .msbuildproj (regresja w wersji 3.3.0-3.4.4 upgrade) - [#2921](https://github.com/NuGet/Home/issues/2921)
* Opóźnienie interfejsu użytkownika podczas aktualizowania pakietu NuGet z otwartym plikiem XAML — [#2878](https://github.com/NuGet/Home/issues/2878)
* Projekt witryny web z usług IIS kończy się niepowodzeniem z nielegalnymi znakami w ścieżce - [#2798](https://github.com/NuGet/Home/issues/2798)
* Nuget add zawiesza się na CentOS - [#2708](https://github.com/NuGet/Home/issues/2708)
* Przywracanie z packagesavemode -nupkg kończy się niepowodzeniem dla json.net - [#2706](https://github.com/NuGet/Home/issues/2706)
* Filtr Menedżera pakietów nie jest dostępny w oknie vs output dla polecenia przywracania - [#2704](https://github.com/NuGet/Home/issues/2704)

[Lista wszystkich problemów rozwiązanych w tej wersji](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.6")
