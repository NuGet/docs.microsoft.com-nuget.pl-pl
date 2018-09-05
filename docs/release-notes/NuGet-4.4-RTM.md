---
title: Informacje o wersji 4.4 RTM NuGet
description: Informacje o wersji programu NuGet 4.3 RTM, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 9ea11ad5476b02940b171fdc69ac0bf56598418d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548417"
---
# <a name="nuget-44-rtm-release-notes"></a>Informacje o wersji 4.4 RTM NuGet

[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z NuGet w wersji 4.4 RTM.

## <a name="known-issues"></a>Znane problemy

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemy z platformą .NET Standard 2.0 przy użyciu platformy .NET Framework i NuGet 

.NET standard i jego narzędzia zaprojektowano w taki sposób, że projekty przeznaczone dla platformy .NET Framework 4.6.1 może zużywać pakietów NuGet i projekty przeznaczone dla .NET Standard 2.0 lub wcześniejszej. [W tym dokumencie](https://github.com/dotnet/standard/issues/481) znajduje się podsumowanie problemy dotyczące tego scenariusza, planowanie adresowania, a rozwiązania można wdrożyć ze stanem współczesnych narzędzi.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Podczas korzystania z konsoli Menedżera pakietów może nie działać klawisz „Enter”

#### <a name="issue"></a>Problem

Czasami klawisz Enter nie działa w konsoli Menedżera pakietów. Jeśli tak się dzieje, sprawdź postęp poprawki i podaj wszystkie przydatne informacje dodatkowe dotyczące kroków odtwarzania. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Obejście

Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania. Alternatywnie, spróbuj usunąć `project.lock.json` i przywrócić go ponownie.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Nie można wyświetlić, dodać ani zaktualizować składnika DotNetCLITools przy użyciu Menedżera pakietów Nuget

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

Od czasu do czasu gdy używasz pakietu zawierającego zestaw z nieprawidłowym podpisem lub gdy wersja pakietu została ustawiona za pomocą znacznika "DateTime", powoduje automatyczne przywracanie pakietu do działania w pętli nieskończonej (dotnet/project-system #1457).

#### <a name="workaround"></a>Obejście

Obecnie nie istnieje obejście tego problemu.

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a>Problemy rozwiązane w wersji RTM w wersji 4.4 NuGet przedział czasu

[4.3 RTM informacjach o wersji NuGet](../release-notes/nuget-4.3-RTM.md) — Wyświetla listę wszystkich problemów naprawione w wersji RTM 4.3 NuGet

### <a name="features"></a>Funkcje

- Obsługa uproszczonego ładowania rozwiązań w scenariuszach PMC i NuGet PM interfejsu użytkownika — [#5180](https://github.com/NuGet/Home/issues/5180)

- Element docelowy programu msbuild pakiet powinien mieć publicznego punktu zaczepienia dla uruchomionej docelowi przed sam - [#5143](https://github.com/NuGet/Home/issues/5143)

- Funkcja: Dodanie przełącznika dependencyVersion instalacji nuget — [#1806](https://github.com/NuGet/Home/issues/1806)

- uap10.0.ToDo.0 powinny być mapowane na .NET Standard 2.0 dla NuGet — [#5684](https://github.com/NuGet/Home/issues/5684)

- Obsługuje program Visual Studio narzędziach do kompilacji SKU z msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)

- Podczas przywracania, generuje błąd, jeśli .NET 4.6.1 Pomoc techniczna dla platformy .NET Standard 2.0 jest wymagana, ale nie jest zainstalowany - [#5325](https://github.com/NuGet/Home/issues/5325)

- Interfejs użytkownika — klienta rezerwacji prefiks Identyfikatora pakietu [#5572](https://github.com/NuGet/Home/issues/5572)

- dostarczanie składników zlokalizowanej nuget w celu obsługi lokalizacji dotnet.exe - [#4336](https://github.com/NuGet/Home/issues/4336)

### <a name="bugs"></a>Usterki

- Obudowy ścieżki innego projektu może spowodować, że przywracanie utratę PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)

- Przenieś kodów błędów z numery ostrzeżeń do zakres błędów — [#5824](https://github.com/NuGet/Home/issues/5824)

- Mylące błąd, gdy .NET Standard w wersji nie jest znany ma być kompatybilna platformę docelową — [#5818](https://github.com/NuGet/Home/issues/5818)

- Pliki z licencjami mylące - testu [#5776](https://github.com/NuGet/Home/issues/5776)

- Brak nagłówków licencji EndToEnd testowanie szablonów — [#5774](https://github.com/NuGet/Home/issues/5774)

- błędy w pliku Packages.config przywracania jest wyświetlany jako NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)

- Zainstaluj nuget.exe powinna mieć DisableParallelProcessing na mono — [#5741](https://github.com/NuGet/Home/issues/5741)

- Zainstaluj nuget.exe niepoprawnie wyłącza buforowanie - [#5737](https://github.com/NuGet/Home/issues/5737)

- VS polecenia przywracania dla pliku packages.config po wyłączeniu przywracania Wyświetla niepoprawny komunikat - [#5718](https://github.com/NuGet/Home/issues/5718)

- VS; Uruchomienie polecenia przywracania po wyłączeniu przywracania wyświetla komunikat mylące - [#5659](https://github.com/NuGet/Home/issues/5659)

- GetRestoreDotnetCliToolsTask ulegnie awarii, gdy brak metadanych wersji - [#5716](https://github.com/NuGet/Home/issues/5716)

- polecenia DotNet
  - dotnetcore Dodawanie pakietów można wyczyścić puste wiersze z pliku csproj - [#5697](https://github.com/NuGet/Home/issues/5697)

- Źródło nazwy ustawienia poświadczeń w pliku NuGet.Config jest uwzględniana wielkość liter — [#5695](https://github.com/NuGet/Home/issues/5695)

- Włączanie GeneratePackageOnBuild usunięte całej historii pakietów - [#5676](https://github.com/NuGet/Home/issues/5676)

- Przywracanie nie spowoduje przywrócenia pakietów mono.cecil lub semver, ale inne pakiety pobrać przywrócony. - [#5649](https://github.com/NuGet/Home/issues/5649)

- Błędy i ostrzeżenia — zła podczas źródło niedostępne.  - [#5644](https://github.com/NuGet/Home/issues/5644)

- [DesignConsistency] Obecnie tekst stanu instalacji NuGet wygląda prawidłowe na ciemny. - [#5642](https://github.com/NuGet/Home/issues/5642)

- Aktualizowanie pakietów w rozwiązaniu aktualizacji/instalacje dla wszystkich projektów — [#5508](https://github.com/NuGet/Home/issues/5508)

- polecenia DotNet
  - Pakiet dotnetcore zachowuje się inaczej w zależności od tego, vs TargetFramework TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)

- Uwzględnione biblioteki DLL wewnątrz ostrzeżenia throw folderu narzędzia - [#5020](https://github.com/NuGet/Home/issues/5020)

- NuGet.ContentModel zużywa zbyt dużej ilości pamięci dla operacji na ciągach - [#4714](https://github.com/NuGet/Home/issues/4714)

- RuntimeEnvironmentHelper.IsLinux zwraca wartość true dla systemu OSX - [#4648](https://github.com/NuGet/Home/issues/4648)

- "pakietu dotnet" umieszcza nuspec w obszarze obj zamiast obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)

- Nuget bardzo wolno uaktualnienie pakietu - [#4534](https://github.com/NuGet/Home/issues/4534)

- Dokument CPS zsynchronizowany przy użyciu przywracania z większych rozwiązania, które nie zostały włączone LSL (Przywracanie uproszczone ładowanie rozwiązań) — [#4307](https://github.com/NuGet/Home/issues/4307)

- SemVer 2.0 - nuget pakietu z podana wersja ignoruje metadanych (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)

- Nuget.exe (3 i nowsze): Zainstaluj pakiet przy użyciu numeru wersji i Flaga ExcludeVersion nie powoduje aktualizacji pakietu do nowszej wersji — [#2405](https://github.com/NuGet/Home/issues/2405)

- Przywracanie pliku Project.JSON powinien Ostrzegaj, gdy najwyższego pakiety narusza ograniczenia - [#2358](https://github.com/NuGet/Home/issues/2358)

- -ConfigFile nie jest ustawienie niestandardowej konfiguracji polecenia install - [#1646](https://github.com/NuGet/Home/issues/1646)

- Zainstaluj nuget.exe nie uznaje "-DisableParallelProcessing" przełącznika - [#1556](https://github.com/NuGet/Home/issues/1556)

- Wyłączone źródła nadal używany przez DotNet.exe lub msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)

- Usuń zawiesza się na scenariusz LSL — [#5685](https://github.com/NuGet/Home/issues/5685)

### <a name="dcrs"></a>DCRs

- nuget.exe nainstalovat podporu TargetFramework - [#5736](https://github.com/NuGet/Home/issues/5736)

- Dodaj inny msbuild zadań UserAgent ciągi (msbuild pulpitu netcore vs) - [#5709](https://github.com/NuGet/Home/issues/5709)

- PackagePathResolver.GetPackageDirectoryName powinny być wirtualne — [#5700](https://github.com/NuGet/Home/issues/5700)

- [DesignConsistency] Mylenie komunikat podczas dodawania pakietów NuGet — [#5641](https://github.com/NuGet/Home/issues/5641)

- [Ostrzeżenia i błędy] NoWarn nie przekazywane, realizowane w sposób przechodni odwołania P2P - [#5501](https://github.com/NuGet/Home/issues/5501)

- Uproszczone ładowanie rozwiązania: Typowych podstawowe dla interfejsu użytkownika PM, konsolę zarządzania Pakietami, a następnie wektory - [#5057](https://github.com/NuGet/Home/issues/5057)

- Uproszczone ładowanie rozwiązania: Obsługi - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)

- Dodano obsługę wstępnie przywrócić docelowy programu MSBuild, która powoduje uruchomienie programu Visual Studio — [#4781](https://github.com/NuGet/Home/issues/4781)

- Dodanie elementu docelowego publicznej do NuGet.targets, która może znajdować się za pomocą BeforeTargets- [#4634](https://github.com/NuGet/Home/issues/4634)

- Pakiet docelowy nie może utworzyć pliki za pomocą akcji kompilacji nieprawidłowo — [#4166](https://github.com/NuGet/Home/issues/4166)

- RestoreOperationLogger.Do blokuje wątków z puli wątków - [#5663](https://github.com/NuGet/Home/issues/5663)

### <a name="docs"></a>Docs

- Dokumenty dotyczące instalacji polecenie DependencyVersion i struktury flagi - [#5858](https://github.com/NuGet/Home/issues/5858)

- Aktualizacja do dokumentów w ostrzeżenia i błędy - NuGet [#5857](https://github.com/NuGet/Home/issues/5857)

## <a name="links-to-github-issues-fixed-in-44-rtm"></a>Linki na problemy usługi GitHub, rozwiązane w wersji 4.4 lub RTM

[Problemy z listy 1](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[Problemy z listy 2](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[Problemy z listy 3](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
