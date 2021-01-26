---
title: Informacje o wersji narzędzia NuGet 4,4 RTM
description: Informacje o wersji dla programu NuGet 4,3 RTM, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 970a920a401b8a74c04d84cbad9933c54e3cd19e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776287"
---
# <a name="nuget-44-release-notes"></a>Informacje o wersji narzędzia NuGet 4,4

[Program Visual Studio 2017 15,4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z pakietem NuGet 4,4 RTM.

## <a name="summary-whats-new-in-440"></a>Podsumowanie: co nowego w programie 4.4.0

## <a name="summary-whats-new-in-442"></a>Podsumowanie: co nowego w programie 4.4.2

* Poprawka zabezpieczeń: uprawnienia dla plików utworzonych wewnątrz ~/.NuGet są zbyt otwarte [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-443"></a>Podsumowanie: co nowego w programie 4.4.3 moc

* Poprawka zabezpieczeń: pliki wewnątrz elementu NUPKGs mogą mieć ścieżkę względną powyżej katalogu NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Znane problemy

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemy z .NET Standard 2,0 z pakietem NuGet .NET Framework & 

.NET Standard & narzędzia zostały zaprojektowane tak, aby projekty ukierunkowane na .NET Framework 4.6.1 mogły korzystać z pakietów NuGet & projekty przeznaczone do .NET Standard 2,0 lub wcześniejszych. [Ten dokument](https://github.com/dotnet/standard/issues/481) zawiera podsumowanie problemów związanych z tym scenariuszem, planu ich rozwiązywania oraz obejścia, które można wdrożyć przy użyciu dzisiejszego stanu narzędzi.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Podczas korzystania z konsoli Menedżera pakietów może nie działać klawisz „Enter”

#### <a name="issue"></a>Problem

Czasami klawisz Enter nie działa w konsoli Menedżera pakietów. Jeśli tak się dzieje, sprawdź postęp poprawki i podaj wszystkie przydatne informacje dodatkowe dotyczące kroków odtwarzania. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Obejście

Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania. Alternatywnie spróbuj usunąć `project.lock.json` i przywrócić ponownie.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Nie można wyświetlać, dodawać ani aktualizować składnika dotnetclitools przy użyciu Menedżera pakietów NuGet

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

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a>Problemy rozwiązane w przedziale czasu NuGet 4,4 RTM

[Informacje o wersji programu nuget 4,3 RTM](../release-notes/nuget-4.3-RTM.md) — lista wszystkich problemów rozwiązanych w przypadku programu NuGet 4,3 RTM

### <a name="features"></a>Funkcje

- Obsługa uproszczonego ładowania rozwiązań w scenariuszach interfejsu użytkownika w programie PMC i NuGet — [#5180](https://github.com/NuGet/Home/issues/5180)

- Element docelowy pakietu MSBuild powinien mieć publiczny punkt zaczepienia dla uruchomionych obiektów docelowych użytkownika przed jego użyciem [#5143](https://github.com/NuGet/Home/issues/5143)

- Funkcja: Add dependencyVersion Switch to the NuGet Install- [#1806](https://github.com/NuGet/Home/issues/1806)

- UAP 10.0. wyk. 0 powinien mapować do .NET Standard 2,0 dla NuGet — [#5684](https://github.com/NuGet/Home/issues/5684)

- Obsługa Visual Studio Build Tools SKU przy użyciu programu MSBuild/t: Restore- [#5562](https://github.com/NuGet/Home/issues/5562)

- Podczas przywracania Generuj błąd, jeśli program .NET 4.6.1 obsługuje .NET Standard 2,0 jest wymagany, ale nie został zainstalowany — [#5325](https://github.com/NuGet/Home/issues/5325)

- Prefiks identyfikatora pakietu dla interfejsu użytkownika klienta rezerwacji [#5572](https://github.com/NuGet/Home/issues/5572)

- Dostarcz zlokalizowane składniki NuGet do obsługi lokalizacji dotnet.exe — [#4336](https://github.com/NuGet/Home/issues/4336)

### <a name="bugs"></a>Usterki

- Różne obudowy ścieżki projektu mogą spowodować utratę składnika packagereferences [#5855](https://github.com/NuGet/Home/issues/5855)

- Przenieś kody błędów z numerami ostrzegawczymi do zakresu błędu — [#5824](https://github.com/NuGet/Home/issues/5824)

- Błąd mylący, gdy wersja .NET Standard nie jest znana pod kątem zgodności z platformą docelową — [#5818](https://github.com/NuGet/Home/issues/5818)

- Pliki testowe z niemylącymi licencjami — [#5776](https://github.com/NuGet/Home/issues/5776)

- Brakujące nagłówki licencji w szablonach testów EndToEnd — [#5774](https://github.com/NuGet/Home/issues/5774)

- packages.config Restore wyświetla błędy jako NU1000- [#5743](https://github.com/NuGet/Home/issues/5743)

- Instalacja nuget.exe powinna mieć DisableParallelProcessing na mono- [#5741](https://github.com/NuGet/Home/issues/5741)

- nuget.exe instalacja niepoprawnie wyłącza buforowanie [#5737](https://github.com/NuGet/Home/issues/5737)

- A uruchomienie polecenia Restore dla packages.config, gdy polecenie Restore jest wyłączone wyświetla komunikat o niepoprawnym [#5718](https://github.com/NuGet/Home/issues/5718)

- LOKALNE Uruchomienie polecenia Restore, gdy przywracanie jest wyłączone, powoduje wyświetlenie komunikatu o pomyłki [#5659](https://github.com/NuGet/Home/issues/5659)

- GetRestoreDotnetCliToolsTask kończy się niepowodzeniem w przypadku braku metadanych wersji — [#5716](https://github.com/NuGet/Home/issues/5716)

- dotnet
  - dotnetcore Dodawanie pakietu może czyścić puste wiersze z csproj- [#5697](https://github.com/NuGet/Home/issues/5697)

- Nazwy źródłowe ustawień poświadczeń w NuGet.Config uwzględnia wielkość liter — [#5695](https://github.com/NuGet/Home/issues/5695)

- Włączenie GeneratePackageOnBuild usuniętej całej historii pakietów — [#5676](https://github.com/NuGet/Home/issues/5676)

- Polecenie Restore nie spowoduje przywrócenia pakietów mono. Cecil lub semver, ale wszystkie pozostałe pakiety zostaną przywrócone. - [#5649](https://github.com/NuGet/Home/issues/5649)

- Błędy i ostrzeżenia — zły błąd, jeśli źródło jest niedostępne.  - [#5644](https://github.com/NuGet/Home/issues/5644)

- [DesignConsistency] Tekst stanu instalacji pakietu NuGet nie jest obecnie prawidłowy dla ciemnego motywu. - [#5642](https://github.com/NuGet/Home/issues/5642)

- Aktualizuj pakiety w ramach aktualizacji rozwiązania/instalacji dla wszystkich projektów — [#5508](https://github.com/NuGet/Home/issues/5508)

- dotnet
  - Pakiet dotnetcore działa inaczej w zależności od TargetFramework vs TargetFrameworks- [#5281](https://github.com/NuGet/Home/issues/5281)

- Dołączone biblioteki DLL w folderze Tools throw Warnings- [#5020](https://github.com/NuGet/Home/issues/5020)

- NuGet. ContentModel zużywa zbyt dużo pamięci dla operacji na ciągach — [#4714](https://github.com/NuGet/Home/issues/4714)

- RuntimeEnvironmentHelper. islinux zwraca wartość true dla OSX- [#4648](https://github.com/NuGet/Home/issues/4648)

- element "dotnet Pack" umieszcza nuspec w obiekcie obj zamiast obj\Debug- [#4644](https://github.com/NuGet/Home/issues/4644)

- Uaktualnienie pakietu NuGet bardzo powolne — [#4534](https://github.com/NuGet/Home/issues/4534)

- Niezsynchronizowany serwer CPS z funkcją przywracania z większymi rozwiązaniami, które nie zostały włączone SKRÓCONO (uproszczone przywracanie rozwiązań) — [#4307](https://github.com/NuGet/Home/issues/4307)

- SemVer 2,0 — pakiet NuGet z podaną wersją ignoruje metadane (3.5.0-RTM-1938) — [#3643](https://github.com/NuGet/Home/issues/3643)

- Nuget.exe (3. +) pakiet instalacyjny z numerem wersji i flagą ExcludeVersion nie aktualizuje pakietu do nowszej wersji — [#2405](https://github.com/NuGet/Home/issues/2405)

- Project.jspodczas przywracania powinny ostrzegać, gdy pakiety najwyższego poziomu naruszają ograniczenia — [#2358](https://github.com/NuGet/Home/issues/2358)

- -ConfigFile nie ustawia niestandardowej konfiguracji przy instalacji polecenie- [#1646](https://github.com/NuGet/Home/issues/1646)

- nuget.exe instalacji nie honoruje przełącznika "-DisableParallelProcessing" — [#1556](https://github.com/NuGet/Home/issues/1556)

- Wyłączone źródła nadal używane przez DotNet.exe lub msbuild.exe [#5704](https://github.com/NuGet/Home/issues/5704)

- Rozwiązanie zawiesza się w scenariuszu SKRÓCONO — [#5685](https://github.com/NuGet/Home/issues/5685)

### <a name="dcrs"></a>DCR

- nuget.exe zainstalować obsługę TargetFramework — [#5736](https://github.com/NuGet/Home/issues/5736)

- Dodawanie różnych ciągów UserAgent zadań programu MSBuild (Visual Core vs Desktop MSBuild) — [#5709](https://github.com/NuGet/Home/issues/5709)

- PackagePathResolver. GetPackageDirectoryName powinna być wirtualna- [#5700](https://github.com/NuGet/Home/issues/5700)

- [DesignConsistency] Komunikat mylący podczas dodawania pakietu NuGet — [#5641](https://github.com/NuGet/Home/issues/5641)

- [Ostrzeżenia i błędy] Nowarn nie przepływ przechodnie za poorednictwem odwołań P2P- [#5501](https://github.com/NuGet/Home/issues/5501)

- Uproszczone ładowanie rozwiązań: wspólne rdzeń dla interfejsu użytkownika PM, PMC i użycie japońskich ideograficznych — [#5057](https://github.com/NuGet/Home/issues/5057)

- Uproszczone ładowanie rozwiązań: support-PMC- [#5053](https://github.com/NuGet/Home/issues/5053)

- Dodano obsługę przed przywróceniem elementu docelowego programu MSBuild, który jest wyzwalany przez program Visual Studio — [#4781](https://github.com/NuGet/Home/issues/4781)

- Dodaj publiczny cel do NuGet. targets, do których można odwoływać się za pomocą BeforeTargets- [#4634](https://github.com/NuGet/Home/issues/4634)

- Obiekt docelowy Pack nie może utworzyć contentFiles z akcją kompilacji prawidłowo — [#4166](https://github.com/NuGet/Home/issues/4166)

- Wątki puli wątków RestoreOperationLogger.Do Blocks — [#5663](https://github.com/NuGet/Home/issues/5663)

### <a name="docs"></a>Docs

- Dokumentacja dla poleceń Install DependencyVersion i Frameworks- [#5858](https://github.com/NuGet/Home/issues/5858)

- Aktualizowanie do dokumentów na temat ostrzeżeń i błędów narzędzia NuGet — [#5857](https://github.com/NuGet/Home/issues/5857)

## <a name="links-to-github-issues-fixed-in-44-rtm"></a>Linki do problemów z usługą GitHub rozwiązane w 4,4 RTM

[Lista problemów 1](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[Lista problemów 2](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[Lista problemów 3](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
