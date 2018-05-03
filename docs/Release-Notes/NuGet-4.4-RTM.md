---
title: Informacje o wersji 4.4 RTM NuGet
description: Informacje o tym znanych problemów, poprawki, dodatkowe funkcje i dcr RTM 4.3 NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3e969274e69de03ca9851d31a627919dcc46bb7d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-44-rtm-release-notes"></a>Informacje o wersji 4.4 RTM NuGet

[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z NuGet 4.4 RTM.

## <a name="known-issues"></a>Znane problemy

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemy z platformą .NET 2.0 standardowe z .NET Framework & NuGet 

.NET standard i jej narzędzi została zaprojektowana w taki sposób, że w projektach przeznaczonych dla platformy .NET Framework 4.6.1 może używać pakietów NuGet & projektach przeznaczonych dla platformy .NET Standard 2.0 lub starszym. [Ten dokument](https://github.com/dotnet/standard/issues/481) zawiera podsumowanie problemy dotyczące tego scenariusza, plan adresowania, a rozwiązania można wdrożyć ze stanem współczesnych narzędzi.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Podczas korzystania z konsoli Menedżera pakietów może nie działać klawisz „Enter”

#### <a name="issue"></a>Problem

Czasami klawisz Enter nie działa w konsoli Menedżera pakietów. Jeśli tak się dzieje, sprawdź postęp poprawki i podaj wszystkie przydatne informacje dodatkowe dotyczące kroków odtwarzania. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Obejście

Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania. Alternatywnie, spróbuj usunąć `project.lock.json` i przywracanie ponownie.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Nie można wyświetlić, dodać lub zaktualizować DotNetCLITools, za pomocą Menedżera pakietów Nuget

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

Od czasu do czasu gdy używasz pakietu, który zawiera zestaw z nieprawidłowym podpisem lub wersja pakietu jest ustawiona z typu "DateTime" znacznika powoduje Przywracanie automatycznego pakietu do uruchamiania w nieskończonej pętli (dotnet/project — system #1457).

#### <a name="workaround"></a>Obejście

Obecnie nie istnieje obejście tego problemu.

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a>Problemy, które usunięto w wersji RTM programu NuGet 4.4 przedziale czasu

[NuGet 4.3 RTM informacje o wersji](../release-notes/nuget-4.3-RTM.md) -Wyświetla wszystkie problemy, które są rozwiązywane RTM 4.3 NuGet

### <a name="features"></a>Funkcje

- Obsługa protokołu Lightweight ładowania rozwiązania w scenariuszach PMC i NuGet PM interfejsu użytkownika — [#5180](https://github.com/NuGet/Home/issues/5180)

- Element docelowy programu msbuild pakietu powinien mieć publicznego punktu zaczepienia dla uruchomionego celów użytkownika przed sam - [#5143](https://github.com/NuGet/Home/issues/5143)

- Funkcja: Dodać przełącznik dependencyVersion nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)

- uap10.0.ToDo.0 powinny być mapowane na .NET 2.0 standardowy programu NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)

- Obsługuje SKU z narzędzia kompilacji programu Visual Studio z msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)

- Podczas przywracania, generuje błąd, jeśli .NET 4.6.1 Obsługa .NET 2.0 standardowe jest wymagana, ale nie jest zainstalowany - [#5325](https://github.com/NuGet/Home/issues/5325)

- Interfejs użytkownika — klienta rezerwacji prefiks Identyfikatora pakietu [#5572](https://github.com/NuGet/Home/issues/5572)

- dostarczanie składników zlokalizowanych nuget w celu obsługi lokalizacja dotnet.exe — [#4336](https://github.com/NuGet/Home/issues/4336)

### <a name="bugs"></a>Usterki

- Obudowy ścieżki inny projekt może spowodować utratę PackageReferences — po ukończeniu przywracania [#5855](https://github.com/NuGet/Home/issues/5855)

- Przenieś kodów błędów z numerów ostrzeżeń, które zakresowi błąd - [#5824](https://github.com/NuGet/Home/issues/5824)

- Błąd błąd, gdy wersja platformy .NET Standard nie jest znany aby był zgodny z platformy docelowej - [#5818](https://github.com/NuGet/Home/issues/5818)

- Testowanie plików z licencjami mylące - [#5776](https://github.com/NuGet/Home/issues/5776)

- Brak nagłówków licencji w EndToEnd testowanie szablonów - [#5774](https://github.com/NuGet/Home/issues/5774)

- Przywracanie pliku Packages.config pokazuje błędy jako NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)

- Zainstaluj nuget.exe powinny mieć DisableParallelProcessing na mono - [#5741](https://github.com/NuGet/Home/issues/5741)

- Zainstaluj nuget.exe niepoprawnie wyłącza buforowanie - [#5737](https://github.com/NuGet/Home/issues/5737)

- VS polecenia przywracania dla pliku packages.config podczas przywracania jest wyłączona, zostanie wyświetlony komunikat niepoprawne - [#5718](https://github.com/NuGet/Home/issues/5718)

- VS; Polecenia restore podczas przywracania jest wyłączona, zostanie wyświetlony komunikat mylące - [#5659](https://github.com/NuGet/Home/issues/5659)

- GetRestoreDotnetCliToolsTask ulegnie awarii, gdy brak metadanych wersji - [#5716](https://github.com/NuGet/Home/issues/5716)

- DotNet
  - Dodaj dotnetcore pakietu można wyczyścić puste wiersze z csproj - [#5697](https://github.com/NuGet/Home/issues/5697)

- Nazwy źródeł ustawień poświadczeń w pliku NuGet.Config jest uwzględniana wielkość liter - [#5695](https://github.com/NuGet/Home/issues/5695)

- Włączanie GeneratePackageOnBuild usunięte Moje całej historii pakiety - [#5676](https://github.com/NuGet/Home/issues/5676)

- Przywracanie nie przywróci mono.cecil lub programu semver pakietów, ale inne pakiety pobrać przywrócony. - [#5649](https://github.com/NuGet/Home/issues/5649)

- Błędy i ostrzeżenia - zły błąd podczas źródła niedostępne.  - [#5644](https://github.com/NuGet/Home/issues/5644)

- [DesignConsistency] Obecnie nie wygląda prawidłowe na ciemny motyw tekst stanu instalacji NuGet. - [#5642](https://github.com/NuGet/Home/issues/5642)

- Aktualizowanie pakietów w aktualizacji rozwiązania/instaluje we wszystkich projektach — [#5508](https://github.com/NuGet/Home/issues/5508)

- DotNet
  - Pakiet dotnetcore zachowuje się inaczej w zależności od vs TargetFramework TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)

- Objąć biblioteki DLL narzędzia folderu throw ostrzeżenia - [#5020](https://github.com/NuGet/Home/issues/5020)

- NuGet.ContentModel zużywa zbyt dużej ilości pamięci dla operacji na ciągach - [#4714](https://github.com/NuGet/Home/issues/4714)

- RuntimeEnvironmentHelper.IsLinux zwraca wartość true dla systemu OS x - [#4648](https://github.com/NuGet/Home/issues/4648)

- "pakiet dotnet" umieszcza nuspec w obszarze obj zamiast obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)

- Nuget bardzo wolno uaktualniania pakietu - [#4534](https://github.com/NuGet/Home/issues/4534)

- Zsynchronizowane procedury CPS przywracania większe rozwiązania, których nie włączono LSL (Przywracanie lekkie rozwiązanie) - [#4307](https://github.com/NuGet/Home/issues/4307)

- Programu SemVer 2.0 — nuget pakietu z warunkiem wersja ignoruje metadanych (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)

- Nuget.exe (3 +) zainstaluj pakiet o numerze wersji i flagi ExcludeVersion nie powoduje aktualizacji pakietu do nowszej wersji — [#2405](https://github.com/NuGet/Home/issues/2405)

- Przywracanie Project.JSON powinien Ostrzegaj, gdy pakiety najwyższego poziomu narusza ograniczenia — [#2358](https://github.com/NuGet/Home/issues/2358)

- -ConfigFile nie jest ustawienie niestandardowej konfiguracji polecenia install - [#1646](https://github.com/NuGet/Home/issues/1646)

- Zainstaluj nuget.exe honoruje "-DisableParallelProcessing" przełącznika - [#1556](https://github.com/NuGet/Home/issues/1556)

- Wyłączone źródeł nadal używane przez DotNet.exe lub msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)

- Usuń zawiesza się na scenariuszu LSL - [#5685](https://github.com/NuGet/Home/issues/5685)

### <a name="dcrs"></a>Dcr

- nuget.exe Zainstaluj obsługę TargetFramework - [#5736](https://github.com/NuGet/Home/issues/5736)

- Dodaj inny msbuild zadania agenta użytkownika ciągi (msbuild pulpitu netcore vs) - [#5709](https://github.com/NuGet/Home/issues/5709)

- PackagePathResolver.GetPackageDirectoryName powinny być wirtualna - [#5700](https://github.com/NuGet/Home/issues/5700)

- [DesignConsistency] Skomplikowana komunikat podczas dodawania pakietu NuGet - [#5641](https://github.com/NuGet/Home/issues/5641)

- [Ostrzeżeń i błędów] NoWarn nie przechodnie przepływać przez odwołania P2P - [#5501](https://github.com/NuGet/Home/issues/5501)

- Ładowania rozwiązania lekkie: Core wspólnego PM interfejsu użytkownika, PMC i wektory inicjacji-- [#5057](https://github.com/NuGet/Home/issues/5057)

- Obciążenia lekkie rozwiązanie: Obsługuje - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)

- Dodaj obsługę wstępnie przywrócić docelowy programu MSBuild, który wyzwala Visual Studio — [#4781](https://github.com/NuGet/Home/issues/4781)

- Dodaj publiczny docelowych do NuGet.targets, który można odwoływać się przy użyciu BeforeTargets- [#4634](https://github.com/NuGet/Home/issues/4634)

- Docelowy pakiet nie można utworzyć pliki z akcjami kompilacji nieprawidłowo — [#4166](https://github.com/NuGet/Home/issues/4166)

- RestoreOperationLogger.Do blokuje wątków z puli wątków - [#5663](https://github.com/NuGet/Home/issues/5663)

### <a name="docs"></a>Docs

- Dokumentacja instalacji poleceń flagi DependencyVersion i Framework — [#5858](https://github.com/NuGet/Home/issues/5858)

- Aktualizacja do dokumentów na NuGet ostrzeżeń i błędów - [#5857](https://github.com/NuGet/Home/issues/5857)

## <a name="links-to-github-issues-fixed-in-44-rtm"></a>Łącza do usunięto w wersji 4.4 RTM zagadnienia GitHub

[Listę problemów 1](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[Listę problemów 2](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[Listę problemów 3](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
