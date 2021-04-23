---
title: Informacje o wersji nuGet 4.4 RTM
description: Informacje o wersji nuGet 4.4 RTM, w tym znane problemy, poprawki błędów, dodane funkcje i dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 980afffcd4202e019ffa87de5dccf947300a9c13
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901710"
---
# <a name="nuget-44-release-notes"></a>Informacje o wersji nuGet 4.4

[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z programem NuGet 4.4 RTM.

## <a name="summary-whats-new-in-440"></a>Podsumowanie: co nowego w 4.4.0

## <a name="summary-whats-new-in-442"></a>Podsumowanie: co nowego w programie 4.4.2

* Poprawka zabezpieczeń: Uprawnienia do plików utworzonych wewnątrz pliku ~/.nuget są zbyt [otwarte #7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-443"></a>Podsumowanie: co nowego w 4.4.3

* Poprawka zabezpieczeń: Pliki wewnątrz NUPKG mogą mieć ścieżkę względną powyżej katalogu NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Znane problemy

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemy z .NET Standard 2.0 za pomocą .NET Framework & NuGet 

.NET Standard & narzędzia zostały zaprojektowane w taki sposób, że projekty przeznaczone dla wersji .NET Framework 4.6.1 mogą korzystać z pakietów NuGet & projektów przeznaczonych dla wersji .NET Standard 2.0 lub starszej. [Ten dokument](https://github.com/dotnet/standard/issues/481) zawiera podsumowanie problemów związanych z tym scenariuszem, plan ich rozwiązania oraz obejścia, które można wdrożyć przy użyciu dzisiejszego stanu narzędzi.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Podczas korzystania z konsoli Menedżera pakietów może nie działać klawisz „Enter”

#### <a name="issue"></a>Problem

Czasami klawisz Enter nie działa w konsoli Menedżera pakietów. Jeśli tak się dzieje, sprawdź postęp poprawki i podaj wszystkie przydatne informacje dodatkowe dotyczące kroków odtwarzania. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Obejście

Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania. Alternatywnie spróbuj usunąć i `project.lock.json` przywrócić ponownie.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Nie można wyświetlić, dodać ani zaktualizować aplikacji DotNetCLITools przy użyciu narzędzia Nuget Menedżer pakietów

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

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a>Problemy rozwiązane w harmonogramie NuGet 4.4 RTM

[Informacje o wersji NuGet 4.3 RTM](../release-notes/nuget-4.3-RTM.md) — lista wszystkich problemów rozwiązanych dla wersji NuGet 4.3 RTM

### <a name="features"></a>Funkcje

- Obsługa uproszczonego ładowania rozwiązań w scenariuszach interfejsu użytkownika PMC i NuGet PM — [#5180](https://github.com/NuGet/Home/issues/5180)

- Element docelowy pakietu msbuild powinien mieć publiczny element zaczepienia do uruchamiania obiektów docelowych użytkownika przed samym [sobą — #5143](https://github.com/NuGet/Home/issues/5143)

- Funkcja: Dodawanie przełącznika dependencyVersion do instalacji nuget [— #1806](https://github.com/NuGet/Home/issues/1806)

- uap10.0.TODO.0 powinien być mapowy do .NET Standard 2.0 dla nuGet — [#5684](https://github.com/NuGet/Home/issues/5684)

- Obsługa Visual Studio Build Tools SKU za pomocą msbuild /t:restore — [#5562](https://github.com/NuGet/Home/issues/5562)

- Podczas przywracania wygeneruj błąd, jeśli obsługa platform .NET 4.6.1 dla .NET Standard 2.0 jest wymagana, ale nie jest zainstalowana — [#5325](https://github.com/NuGet/Home/issues/5325)

- Interfejs użytkownika klienta rezerwacji prefiksu pakietu [— #5572](https://github.com/NuGet/Home/issues/5572)

- dostarczanie zlokalizowanych składników nuget do dotnet.exe lokalizacji — [#4336](https://github.com/NuGet/Home/issues/4336)

### <a name="bugs"></a>Usterki

- Różne wielkości obudowy ścieżek projektu mogą spowodować utratę odszukań packageReferences — [#5855](https://github.com/NuGet/Home/issues/5855)

- Przenoszenie kodów błędów z numerami ostrzegawczymi do zakresu błędów [— #5824](https://github.com/NuGet/Home/issues/5824)

- Mylący błąd, .NET Standard wersja nie jest zgodna z platformą docelową — [#5818](https://github.com/NuGet/Home/issues/5818)

- Pliki testowe z mylącymi licencjami [— #5776](https://github.com/NuGet/Home/issues/5776)

- Brak nagłówków licencji w szablonach testowych EndToEnd [— #5774](https://github.com/NuGet/Home/issues/5774)

- packages.config przywracania są błędy jako NU1000 [— #5743](https://github.com/NuGet/Home/issues/5743)

- nuget.exe instalacji powinna mieć ustawienie DisableParallelProcessing na mono [— #5741](https://github.com/NuGet/Home/issues/5741)

- nuget.exe nieprawidłowo wyłącza buforowanie — [#5737](https://github.com/NuGet/Home/issues/5737)

- Program VS uruchamia polecenie przywracania dla packages.config gdy przywracanie jest wyłączone, wyświetla niepoprawny [komunikat — #5718](https://github.com/NuGet/Home/issues/5718)

- VS; Uruchomienie polecenia przywracania, gdy przywracanie jest wyłączone, powoduje wyświetlenie mylącego [komunikatu — #5659](https://github.com/NuGet/Home/issues/5659)

- GetRestoreDotnetCliToolsTask kończy się niepowodzeniem, gdy brakuje metadanych wersji — [#5716](https://github.com/NuGet/Home/issues/5716)

- dotnet
  - Dotnetcore add package can clear empty lines from a csproj - [#5697](https://github.com/NuGet/Home/issues/5697)

- W nazwach źródeł ustawień poświadczeń w NuGet.Config jest zróżnicowa wielkość [liter — #5695](https://github.com/NuGet/Home/issues/5695)

- Włączenie funkcji GeneratePackageOnBuild usunęła całą historię pakietów [— #5676](https://github.com/NuGet/Home/issues/5676)

- Przywracanie nie spowoduje przywrócenia pakietów mono.debianil ani semver, ale wszystkie inne pakiety zostaną przywrócone. - [#5649](https://github.com/NuGet/Home/issues/5649)

- Błędy i ostrzeżenia — zły błąd, gdy źródło jest niedostępne.  - [#5644](https://github.com/NuGet/Home/issues/5644)

- [DesignConsistency] Tekst stanu instalacji nuGet obecnie nie wygląda poprawnie w ciemnym motywie. - [#5642](https://github.com/NuGet/Home/issues/5642)

- Aktualizowanie pakietów przy aktualizacjach/instalacjach rozwiązań dla wszystkich projektów — [#5508](https://github.com/NuGet/Home/issues/5508)

- dotnet
  - Dotnetcore pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)

- Uwzględnione biblioteki DLL w folderze Tools zgłaszają ostrzeżenia [— #5020](https://github.com/NuGet/Home/issues/5020)

- Model NuGet.ContentModel zużywa zbyt dużo pamięci na operacje na ciągach [— #4714](https://github.com/NuGet/Home/issues/4714)

- RuntimeEnvironmentHelper.IsLinux zwraca wartość true dla systemu OSX [— #4648](https://github.com/NuGet/Home/issues/4648)

- Polecenie "dotnet pack" umieszcza nuspec w obszarze obj zamiast obj\Debug — [#4644](https://github.com/NuGet/Home/issues/4644)

- Bardzo powolne uaktualnianie pakietu Nuget [— #4534](https://github.com/NuGet/Home/issues/4534)

- CpS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)

- SemVer 2.0 — pakiet NuGet z podaną wersją ignoruje metadane (3.5.0-rtm-1938) [— #3643](https://github.com/NuGet/Home/issues/3643)

- Nuget.exe (3.+) z numerem wersji i flagą ExcludeVersion nie aktualizuje pakietu do nowszej wersji [—](https://github.com/NuGet/Home/issues/2405) #2405

- Project.jsprzywracania powinien być ostrzegany, gdy pakiety najwyższego poziomu naruszają ograniczenia — [#2358](https://github.com/NuGet/Home/issues/2358)

- -ConfigFile nie jest ustawienie niestandardowej konfiguracji polecenia instalacji — [#1646](https://github.com/NuGet/Home/issues/1646)

- nuget.exe nie honoruje przełącznika "-DisableParallelProcessing" — [#1556](https://github.com/NuGet/Home/issues/1556)

- Wyłączone źródła nadal używane przez DotNet.exe lub msbuild.exe — [#5704](https://github.com/NuGet/Home/issues/5704)

- Rozwiązywanie problemów z zawiesza się w scenariuszu LSL [— #5685](https://github.com/NuGet/Home/issues/5685)

### <a name="dcrs"></a>Kontrolery domeny

- nuget.exe zainstalować obsługę obiektu TargetFramework [— #5736](https://github.com/NuGet/Home/issues/5736)

- Dodawanie różnych ciągów UserAgent zadania msbuild (netcore a desktop msbuild) — [#5709](https://github.com/NuGet/Home/issues/5709)

- Parametr PackagePathResolver.GetPackageDirectoryName powinien być wirtualny — [#5700](https://github.com/NuGet/Home/issues/5700)

- [DesignConsistency] Mylący komunikat podczas dodawania pakietu NuGet [— #5641](https://github.com/NuGet/Home/issues/5641)

- [Ostrzeżenia i błędy] NoWarn nie przepływa przechodnie przez odwołania P2P — [#5501](https://github.com/NuGet/Home/issues/5501)

- Uproszczone ładowanie rozwiązań: Podstawowe funkcje interfejsu użytkownika PM, PMC i IV — [#5057](https://github.com/NuGet/Home/issues/5057)

- Uproszczone ładowanie rozwiązań: obsługa — PMC [— #5053](https://github.com/NuGet/Home/issues/5053)

- Dodawania obsługi wstępnego przywracania obiektu docelowego MSBuild, Visual Studio wyzwalaczy — [#4781](https://github.com/NuGet/Home/issues/4781)

- Dodawanie publicznego obiektu docelowego do obiektu NuGet.targets, do których można się odwoływać przy użyciu funkcji BeforeTargets — [#4634](https://github.com/NuGet/Home/issues/4634)

- Element docelowy pakietu nie może poprawnie tworzyć plików z akcjami kompilacji — [#4166](https://github.com/NuGet/Home/issues/4166)

- RestoreOperationLogger.Do bloków wątków puli wątków [— #5663](https://github.com/NuGet/Home/issues/5663)

### <a name="docs"></a>Docs

- Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)

- Aktualizacja do dokumentów dotyczących ostrzeżeń i błędów nuGet — [#5857](https://github.com/NuGet/Home/issues/5857)

## <a name="links-to-github-issues-fixed-in-44-rtm"></a>Linki do problemów z serwisem GitHub rozwiązanych w wersji 4.4 RTM

[Lista problemów 1](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[Lista problemów 2](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[Lista problemów 3](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
