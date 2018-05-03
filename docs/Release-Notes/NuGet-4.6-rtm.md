---
title: Informacje o wersji 4.6 RTM NuGet
description: Informacje o wersji programu NuGet 4.6.0 tym — znane problemy, poprawki, dodatkowe funkcje i dcr.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 3/7/2018
ms.topic: conceptual
ms.openlocfilehash: d8fc374167e5c7f601c41887c4844854d0177ccb
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-46-rtm-release-notes"></a>Informacje o wersji 4.6 RTM NuGet

[Visual Studio 2017 15,6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z [NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe).

## <a name="summary-whats-new-in-this-release"></a>Podsumowanie: nowości w tej wersji
* Dodaliśmy obsługę [podpisywania pakietów](https://docs.microsoft.com/en-us/nuget/create-packages/sign-a-package).  
* Visual Studio 2017 i nuget.exe teraz weryfikuje integralność pakietu przed instalacją, przywracanie pakietów dla [podpisanych pakietów](https://docs.microsoft.com/en-us/nuget/reference/signed-packages-reference).
* Firma Microsoft ulepszyła wydajności kolejnych operacji przywracania.

## <a name="known-issues"></a>Znane problemy
### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemy z platformą .NET 2.0 standardowe z .NET Framework & NuGet 

.NET standard i jej narzędzi została zaprojektowana w taki sposób, że w projektach przeznaczonych dla platformy .NET Framework 4.6.1 może używać pakietów NuGet & projektach przeznaczonych dla platformy .NET Standard 2.0 lub starszym. [Ten dokument](https://github.com/dotnet/standard/issues/481) zawiera podsumowanie problemy dotyczące tego scenariusza, plan adresowania, a rozwiązania można wdrożyć ze stanem współczesnych narzędzi.

## <a name="top-issues-fixed-in-this-release"></a>Najważniejsze problemy rozwiązane w tej wersji

**Poprawki wydajności**
* Nie zapisywać pliki zasobów, gdy nie została zmieniona - [#6491](https://github.com/NuGet/Home/issues/6491)
* Przywracanie powoduje dodatkowe obliczanie MSBuild podczas TFM projekty podrzędne nie są zgodne z nadrzędnego projektu - [#6311](https://github.com/NuGet/Home/issues/6311)
* Zwiększanie operacja przywracania wydajności dzięki optymalizacji zależności programu graph specyfikacji tworzenie - [#6252](https://github.com/NuGet/Home/issues/6252)

**Usterki**
* Powiadomień wypychanych do folderu lokalnego pozostawia nupkg zablokowany - [#6325](https://github.com/NuGet/Home/issues/6325)
* Implementacja NuGet wtyczki: wiele problemów — [#6149](https://github.com/NuGet/Home/issues/6149)
* UIHang - Usuń zapytania wywołania usługi od zainicjowania MEF w VSSolutionManager - [#6110](https://github.com/NuGet/Home/issues/6110)
* Wyjątek dla raportowania błędów anulowane zadania pobierania pakietu - [#6096](https://github.com/NuGet/Home/issues/6096)
* Zastępuje NuGet.exe "+" z "% 2B" w nazwie zestawu - [#5956](https://github.com/NuGet/Home/issues/5956)
* FN + F1 nie przejść do strony właściwą pomoc dla interfejsu użytkownika PM i konsola — [#5912](https://github.com/NuGet/Home/issues/5912)
* VS NuGet zapisuje bezwzględnej ścieżki do plików projektu w określonych okolicznościach - [#5888](https://github.com/NuGet/Home/issues/5888)
* Usuń 4.3 regresji — symbole zastępcze $product$ i $ $AssemblyGuid nie jest wymieniony w contentfile za pomocą przekształcania - [#5880](https://github.com/NuGet/Home/issues/5880)
* Przywracanie DotNet z wielu źródeł awarii (Crash) - [#5817](https://github.com/NuGet/Home/issues/5817)
* Pakiet należy ponownie oceń wersji projektu umożliwia przechowywanie wersji git - [#4790](https://github.com/NuGet/Home/issues/4790)
* Twarde zwiększyć zrozumienie błędy podczas instalowania pakietu niezgodny - [#4555](https://github.com/NuGet/Home/issues/4555)
* TemplateWizard należy zainstalować pakiety jako PackageReferences - [#4549](https://github.com/NuGet/Home/issues/4549)
* Pliki dostarczone pakietu właściwości ignorowane MSBuild.exe jest uruchamiany z poza wierszem polecenia dewelopera - [#4530](https://github.com/NuGet/Home/issues/4530)
* Napraw błąd niską podczas odwoływania się do biblioteki standardowej .NET, który nie ma zastosowania do projektu - [#4423](https://github.com/NuGet/Home/issues/4423)
* Dodaj DotNet pakietu nie powiedzie się dla pakietu docelowy profil przenośnych małego wskazówki — [#4349](https://github.com/NuGet/Home/issues/4349)
* Pakiet DotNet - sufiks wersji brakuje elementu ProjectReference - [#4337](https://github.com/NuGet/Home/issues/4337)
* Tworzenie błędów i awarii w PORÓWNANIU z szablonu .NET Core - [#3973](https://github.com/NuGet/Home/issues/3973)
* Nie można załadować indeks usługi https:* źródła - [#3681](https://github.com/NuGet/Home/issues/3681)
* nie działa nuget.exe listy - allversions - [#3441](https://github.com/NuGet/Home/issues/3441)
* Błąd zależności rozpoznawania komunikat o błędzie — [#2984](https://github.com/NuGet/Home/issues/2984)
* Przywracanie nuget.exe nie tworzy pliki .props i .targets dla .msbuildproj (regresji przy uaktualnianiu v3.3.0 3.4.4) - [#2921](https://github.com/NuGet/Home/issues/2921)
* Opóźnienie reakcji interfejsu użytkownika podczas aktualizowania pakietu NuGet z XAML plik otwarty - [#2878](https://github.com/NuGet/Home/issues/2878)
* Projekt witryny sieci Web za pomocą programu IIS nie powiodło się niedozwolone znaki w ścieżce - [#2798](https://github.com/NuGet/Home/issues/2798)
* Nuget Dodaj zawiesza się na CentOS - [#2708](https://github.com/NuGet/Home/issues/2708)
* Przywracanie z packagesavemode - nupkg nie powiedzie się dla struktury json.net - [#2706](https://github.com/NuGet/Home/issues/2706)
* W oknie polecenie restore - output filtru Menedżera pakietów nie jest dostępna w programie vs [#2704](https://github.com/NuGet/Home/issues/2704)


[Lista wszystkich problemów rozwiązanych w tej wersji](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.6")
