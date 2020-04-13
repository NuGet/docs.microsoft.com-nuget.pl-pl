---
title: Informacje o wersji nuGet 4.4 RTM
description: Informacje o wersji dla NuGet 4.3 RTM, w tym znane problemy, poprawki błędów, dodane funkcje i dcrs.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3be24a86cc92c4e6d07fcae1dc625a150f28d7b4
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498702"
---
# <a name="nuget-44-release-notes"></a>Informacje o wersji nuget 4.4

[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z NuGet 4.4 RTM.

## <a name="summary-whats-new-in-440"></a>Krótki opis: Co nowego w 4.4.0

## <a name="summary-whats-new-in-442"></a>Krótki opis: Co nowego w 4.4.2

* Poprawka zabezpieczeń: Uprawnienia do plików utworzonych wewnątrz ~/.nuget są zbyt otwarte [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-443"></a>Krótki opis: Co nowego w 4.4.3

* Poprawka zabezpieczeń: Pliki wewnątrz nupkgs może mieć względną ścieżkę powyżej katalogu NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Znane problemy

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemy z .NET Standard 2.0 z .NET Framework & NuGet 

.NET Standard & jego narzędzia został zaprojektowany w taki sposób, że projekty przeznaczone dla platformy .NET Framework 4.6.1 mogą korzystać z pakietów NuGet & projektów przeznaczonych dla .NET Standard 2.0 lub wcześniejszych. [W tym dokumencie](https://github.com/dotnet/standard/issues/481) podsumowano problemy związane z tym scenariuszem, plan ich rozwiązania i obejścia, które można wdrożyć przy dzisiejszym stanie narzędzia.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Podczas korzystania z konsoli Menedżera pakietów może nie działać klawisz „Enter”

#### <a name="issue"></a>Problem

Czasami klawisz Enter nie działa w konsoli Menedżera pakietów. Jeśli tak się dzieje, sprawdź postęp poprawki i podaj wszystkie przydatne informacje dodatkowe dotyczące kroków odtwarzania. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Obejście

Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania. Alternatywnie spróbuj usunąć `project.lock.json` i przywrócić ponownie.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Nie można wyświetlać, dodawać ani aktualizować dotNetCLITools przy użyciu Menedżera pakietów Nuget

#### <a name="issue"></a>Problem

Menedżer pakietów NuGet nie wyświetla składnika DotNetCLITools ani nie zezwala na jego dodawanie/aktualizowanie. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Obejście

Należy ręcznie edytować składnik DotNetCLIToolReferences w pliku projektu.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense

#### <a name="issue"></a>Problem

Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense w programie Visual Studio. Dzieje się tak w przypadku używania składnika PackageReferences jako formatu Menedżera pakietów. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Obejście

Wykonaj przywracanie ręczne.

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>Pakiet w projekcie .NET Core, który zawiera zestaw z nieprawidłowym podpisem, może spowodować pętlę nieskończoną przywracania

#### <a name="issue"></a>Problem

W przypadku użycia pakietu zawierającego zestaw z nieprawidłowym podpisem lub gdy wersja pakietu została ustawiona za pomocą znacznika „DateTime”, automatyczne przywracanie pakietu będzie czasem uruchamiane w pętli nieskończonej (dotnet/project-system#1457).

#### <a name="workaround"></a>Obejście

Obecnie nie istnieje obejście tego problemu.

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a>Naprawiono problemy w ramach czasowych NuGet 4.4 RTM

[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Wyświetla listę wszystkich problemów rozwiązanych dla NuGet 4.3 RTM

### <a name="features"></a>Funkcje

- Obsługa lekkiego ładowania rozwiązań w scenariuszach interfejsu użytkownika PM PM i NuGet - [#5180](https://github.com/NuGet/Home/issues/5180)

- Obiekt docelowy pakietu msbuild powinien mieć publiczny hak do uruchamiania obiektów docelowych użytkownika przed sobą — [#5143](https://github.com/NuGet/Home/issues/5143)

- Funkcja: Dodaj przełącznik konwersjiVersion do instalacji nuget - [#1806](https://github.com/NuGet/Home/issues/1806)

- uap10.0.TODO.0 powinien zostać zamapowana na .NET Standard 2.0 dla NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)

- Obsługa jednostki SKU narzędzi kompilacji programu Visual Studio za pomocą usługi msbuild /t:restore — [#5562](https://github.com/NuGet/Home/issues/5562)

- Podczas przywracania wygeneruj błąd, jeśli jest wymagana obsługa platformy .NET 4.6.1 dla platformy .NET Standard 2.0, ale nie zainstalowana — [#5325](https://github.com/NuGet/Home/issues/5325)

- Interfejs użytkownika klienta prefiksu identyfikatora pakietu — [#5572](https://github.com/NuGet/Home/issues/5572)

- dostarczać zlokalizowane składniki nuget do obsługi lokalizacji dotnet.exe - [#4336](https://github.com/NuGet/Home/issues/4336)

### <a name="bugs"></a>Usterki

- Różne wielkości liter ścieżki projektu może spowodować przywrócenie do utraty PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)

- Przenieś kody błędów z numerami ostrzeżeń do zakresu błędów - [#5824](https://github.com/NuGet/Home/issues/5824)

- Błąd wprowadzający w błąd, gdy nie wiadomo, że wersja .NET Standard jest zgodna z platformą docelową - [#5818](https://github.com/NuGet/Home/issues/5818)

- Pliki testowe z mylącymi licencjami - [#5776](https://github.com/NuGet/Home/issues/5776)

- Brak nagłówków licencji w szablonach testów EndToEnd — [#5774](https://github.com/NuGet/Home/issues/5774)

- packages.config restore pokazuje błędy jako NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)

- nuget.exe zainstalować powinien mieć DisableParallelProcessing na mono - [#5741](https://github.com/NuGet/Home/issues/5741)

- nuget.exe zainstalować niepoprawnie wyłącza buforowanie - [#5737](https://github.com/NuGet/Home/issues/5737)

- Vs Uruchomienie polecenia przywracania dla packages.config po wyłączeniu przywracania wyświetla niepoprawny komunikat - [#5718](https://github.com/NuGet/Home/issues/5718)

- VS; Uruchamianie polecenia przywracania po wyłączeniu przywracania wyświetla mylący komunikat - [#5659](https://github.com/NuGet/Home/issues/5659)

- GetRestoreDotnetCliToolsTask nie powiedzie się, gdy brakuje metadanych wersji - [#5716](https://github.com/NuGet/Home/issues/5716)

- dotnet
  - dotnetcore dodać pakiet można wyczyścić puste linie z csproj - [#5697](https://github.com/NuGet/Home/issues/5697)

- Nazwy źródeł ustawień poświadczeń w nuget.config są rozróżniane wielkość liter - [#5695](https://github.com/NuGet/Home/issues/5695)

- Włączenie GeneratePackageOnBuild usunął całą moją historię pakietów - [#5676](https://github.com/NuGet/Home/issues/5676)

- Przywracanie nie przywróci pakietów mono.cecil lub semver, ale wszystkie inne pakiety zostaną przywrócone. - [#5649](https://github.com/NuGet/Home/issues/5649)

- Błędy i ostrzeżenia — zły błąd, gdy źródło jest niedostępne.  - [#5644](https://github.com/NuGet/Home/issues/5644)

- [DesignConsistency] Tekst stanu instalacji NuGet nie wygląda poprawnie w ciemnym motywie. - [#5642](https://github.com/NuGet/Home/issues/5642)

- Aktualizuj pakiety w aktualizacjach/instalacjach rozwiązania dla wszystkich projektów - [#5508](https://github.com/NuGet/Home/issues/5508)

- dotnet
  - pakiet dotnetcore zachowuje się inaczej w zależności od TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)

- Dołączone biblioteki DLL wewnątrz folderu Tools rzucają ostrzeżenia - [#5020](https://github.com/NuGet/Home/issues/5020)

- NuGet.ContentModel zużywa zbyt dużo pamięci dla operacji ciągu - [#4714](https://github.com/NuGet/Home/issues/4714)

- RuntimeEnvironmentHelper.IsLinux zwraca wartość true dla OSX - [#4648](https://github.com/NuGet/Home/issues/4648)

- 'dotnet pack' stawia nuspec pod obj zamiast obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)

- Nuget bardzo powolne uaktualnienie pakietu - [#4534](https://github.com/NuGet/Home/issues/4534)

- CPS niezsynchronizowane z przywracanie z większych rozwiązań, które nie zostały włączone LSL (lekkie przywracanie rozwiązania) - [#4307](https://github.com/NuGet/Home/issues/4307)

- SemVer 2.0 - nuget pack z dostarczoną wersją ignoruje metadane (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)

- Nuget.exe (3.+) zainstalować pakiet z numerem wersji i ExcludeVersion flagi nie aktualizuje pakietu do nowszej wersji - [#2405](https://github.com/NuGet/Home/issues/2405)

- Przywracanie project.json powinien ostrzegać, gdy pakiety najwyższego poziomu naruszają ograniczenia - [#2358](https://github.com/NuGet/Home/issues/2358)

- -ConfigFile nie ustawia niestandardowego configu na komendzie install - [#1646](https://github.com/NuGet/Home/issues/1646)

- nuget.exe install nie honoruje przełącznika '-DisableParallelProcessing' - [#1556](https://github.com/NuGet/Home/issues/1556)

- Wyłączone źródła nadal używane przez DotNet.exe lub msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)

- Napraw zawiesza się w scenariuszu LSL - [#5685](https://github.com/NuGet/Home/issues/5685)

### <a name="dcrs"></a>DDR

- nuget.exe zainstalować Obsługę TargetFramework - [#5736](https://github.com/NuGet/Home/issues/5736)

- Dodaj różne parametry useragent zadania msbuild (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)

- PackagePathResolver.GetPackageDirectoryName powinien być wirtualny - [#5700](https://github.com/NuGet/Home/issues/5700)

- [DesignConsistency] Mylący komunikat podczas dodawania pakietu NuGet - [#5641](https://github.com/NuGet/Home/issues/5641)

- [Ostrzeżenia i błędy] NoWarn nie przepływa przechodnie przez odniesienia P2P - [#5501](https://github.com/NuGet/Home/issues/5501)

- Lekkie obciążenie rozwiązania: Wspólny rdzeń dla pm ui, PMC i IV- - [#5057](https://github.com/NuGet/Home/issues/5057)

- Lekkie obciążenie rozwiązania: Wsparcie - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)

- Dodaj obsługę wstępnie przywrócić obiekt docelowy MSBuild, który wyzwala program Visual Studio — [#4781](https://github.com/NuGet/Home/issues/4781)

- Dodaj publiczny obiekt docelowy do obiektów docelowych NuGet.targets, do których można się odwoływać przy użyciu beforetargets — [#4634](https://github.com/NuGet/Home/issues/4634)

- Miejsce docelowe pakietu nie może poprawnie utworzyć contentFiles z akcjami kompilacji — [#4166](https://github.com/NuGet/Home/issues/4166)

- RestoreOperationLogger.Do blokuje wątki puli gwintów - [#5663](https://github.com/NuGet/Home/issues/5663)

### <a name="docs"></a>Docs

- Flagi Docs for Install command DependencyVersion i Framework — [#5858](https://github.com/NuGet/Home/issues/5858)

- Aktualizacja do dokumentów na NuGet ostrzeżenia i błędy - [#5857](https://github.com/NuGet/Home/issues/5857)

## <a name="links-to-github-issues-fixed-in-44-rtm"></a>Poprawiono łącze do gitHub w 4.4 RTM

[Lista problemów 1](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[Lista problemów 2](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[Lista problemów 3](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
