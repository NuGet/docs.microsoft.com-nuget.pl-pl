---
title: Informacje o wersji RTM 4,8 NuGet
description: Informacje o wersji programu NuGet 4.8.1 tym — znane problemy, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: cf15c4f6a2e3e9f6ce7b6acb2304648041043685
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324828"
---
# <a name="nuget-48-rtm-release-notes"></a>Informacje o wersji RTM 4,8 NuGet

[Visual Studio 2017 15.8 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) pochodzi z funkcjonalnością NuGet 4.8.


Dostępne są wersje wiersza polecenia funkcji:
* 4.8 - NuGet.exe [nuget.org/downloads](https://nuget.org/downloads)
* DotNet.exe - [platformy .NET Core SDK 2.1.400](https://www.microsoft.com/net/download/visual-studio-sdks)


## <a name="summary-whats-new-in-this-release"></a>Podsumowanie: Nowości w tej wersji
* NuGet.exe obsługuje teraz longfilenames w systemie Windows 10 — [#6937](https://github.com/NuGet/Home/issues/6937)
* Wtyczki uwierzytelniania działa teraz w MsBuild, DotNet.exe, NuGet.exe i Visual Studio, w tym dla wielu platform. Pierwsza generacja wtyczki uwierzytelniania nie są obsługiwane w programie MsBuild DotNet.exe. Uwaga: (Wersja zapoznawcza) w programie VS 2017 15.9 kompilacje mają wtyczka uwierzytelniania usługi VSTS uwzględnione. [#6486](https://github.com/NuGet/Home/issues/6486)
* Mechanizm rozpoznawania zestawu SDK w MsBuild teraz kompilacji w ramach pakietu nuget i instaluje się za pomocą narzędzi NuGet dla programu VS. Należy unikać wersje wprowadzenie limitu synchronizacji. [#6799](https://github.com/NuGet/Home/issues/6799)
* PackageReference obsługuje teraz metadane DevelopmentDependency — [#4125](https://github.com/NuGet/Home/issues/4125)

## <a name="known-issues"></a>Znane problemy
### <a name="installing-signed-packages-on-a-ci-machine-or-in-an-offline-environment-takes-longer-than-usual"></a>Instalowanie pakietów podpisem, na komputerze ciągłą Integrację lub w trybie offline środowiska trwa dłużej niż zwykle

#### <a name="issue"></a>Problem
Maszyny ma ograniczony dostęp do Internetu (na przykład maszynę kompilacji w przypadku ciągłej integracji/ciągłego Dostarczania), instalowania/Przywracanie pakietów nuget podpisem spowoduje ostrzeżenia ([NU3028](https://docs.microsoft.com/en-us/nuget/reference/errors-and-warnings/nu3028)) od czasu serwery odwołań są niedostępne. To normalne zachowanie. Jednak w niektórych przypadkach może to mieć niezamierzone concequences, takich jak pakiet instalacji/przywracania trwa dłużej niż zwykle.

#### <a name="workaround"></a>Obejście
Aktualizowanie programu Visual Studio, 15.8.4 i NuGet.exe 4.8.1, w którym wprowadzono zmiennej środowiskowej, aby przełączyć tryb wyboru odwołania.
Ustawienie `NUGET_CERT_REVOCATION_MODE` zmiennej środowiskowej, aby `offline` wymusi pakietu NuGet, aby sprawdzić stanu odwołania certyfikatu wyłącznie w odniesieniu do listy odwołania certyfikatów z pamięci podręcznej, a nie próbuje skontaktować się z serwerami odwołań NuGet. Gdy tryb wyboru odwołania jest ustawiony na `offline`, ostrzeżenie będzie można zmienić na starszą wersję informacji.

> [!Warning]
> Przełącz tryb wyboru odwołania do trybu offline w ramach normalnych okoliczności jest niezalecane. To spowoduje, że rozszerzenie NuGet, aby pominąć sprawdzanie odwołań w trybie online i wykonywać tylko w trybie offline odwołania sprawdzenie listy odwołania certyfikatów pamięci podręcznej, które mogą być nieaktualne. To oznacza, że pakiety, gdzie certyfikat podpisywania został odwołany, będzie nadal zainstalowany/przywrócona, które w przeciwnym wypadku nie powiodłoby się sprawdzanie odwołań i nie będzie został zainstalowany.

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>`Migrate packages.config to PackageReference...` Opcja nie jest dostępna w menu kontekstowym kliknij prawym przyciskiem myszy

#### <a name="issue"></a>Problem

Przy pierwszym otwarciu projektu, NuGet może nie mieć zainicjowany, dopóki nie jest wykonywana operacja NuGet. Powoduje to możliwość migracji nie pojawiają się w menu kontekstowym kliknij prawym przyciskiem myszy na `packages.config` lub `References`.

#### <a name="workaround"></a>Obejście

Wykonaj jeden z następujących akcji NuGet:
* Otwórz interfejs użytkownika Menedżera pakietów — kliknij prawym przyciskiem myszy `References` i wybierz pozycję `Manage NuGet Packages...`
* Otwórz konsolę Menedżera pakietów — z `Tools > NuGet Package Manager`, wybierz opcję `Package Manager Console`
* Uruchom Przywracanie pakietów NuGet — kliknij prawym przyciskiem myszy na węzeł rozwiązania w Eksploratorze rozwiązań i wybierz pozycję `Restore NuGet Packages`
* Skompiluj projekt, który wyzwala również Przywracanie pakietów NuGet

Teraz można wyświetlić opcji migracji. Należy zauważyć, że ta opcja nie jest obsługiwane i nie będzie widoczna dla typów projektów platformy ASP.NET i C++.
Uwaga: Ten problem został rozwiązany w programie VS 2017 15.9 3 (wersja zapoznawcza)

## <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

### <a name="bugs"></a>Usterki
#### <a name="signing"></a>podpisywanie
* Signing: Instalowanie podpisany pakiet w trybie offline środowiska [#7008](https://github.com/NuGet/Home/issues/7008) — rozwiązane w 4.8.1
* Podpisywania:: niepoprawna Sprawdź adres URL — [#7174](https://github.com/NuGet/Home/issues/7174)
* Podpisywania: gdy pakiet jest repozytorium podpisane - Sprawdź integralność pakietu w RepositorySignatureVerifier [#6926](https://github.com/NuGet/Home/issues/6926)
* "Podczas sprawdzania integralności pakietu nie powiodło się." powinna mieć identyfikator pakietu w wiadomości (i kod błędu) - [#6944](https://github.com/NuGet/Home/issues/6944)
* Repozytorium podpisany weryfikacji pakietu zezwala na pakiety podpisane przez innego certyfikatu — [#6884](https://github.com/NuGet/Home/issues/6884)
* Adres URL sygnatury czasowej — podpisywania - NuGet nie może być https://? - [#6871](https://github.com/NuGet/Home/issues/6871)
* Nie NullRef w scenariuszu pakowania NuSpec, również zwiększyć opcji - [#6866](https://github.com/NuGet/Home/issues/6866)
* Pamięć jest nieprawidłowy podczas aktualizowania informacji o osoby podpisującej podczas dodawania sygnatury czasowej do kontrasygnaturze - [#6840](https://github.com/NuGet/Home/issues/6840)
* Podpisywanie: usuwanie wyjątków CTL — [#6794](https://github.com/NuGet/Home/issues/6794)
* Podpisywanie: contentUrl musi być typu HTTPS - [#6777](https://github.com/NuGet/Home/issues/6777)
* Signing:  SignedPackageVerifierSettings.VSClientDefaultPolicy jest nieużywana - [#6601](https://github.com/NuGet/Home/issues/6601)


#### <a name="pack"></a>pakiet
* Przywracanie i kompilacja powinna być niepotrzebne w przypadku używania dotnet.exe do pakietu nuspec - [#6866](https://github.com/NuGet/Home/issues/6866)
* Zezwalaj na pusty zastąpienia tokenów w NuspecProperties - [#6722](https://github.com/NuGet/Home/issues/6722)
* PackTask zgłasza obiektu NullReferenceException, gdy określona jest NuspecProperties - [#4649](https://github.com/NuGet/Home/issues/4649)

#### <a name="accessibility"></a>Ułatwienia dostępu
* [Ułatwień dostępu.] Ciąg "Wersja wstępna" pod przyciskiem pakiet jest objęta jego opis pakietu w interfejsie użytkownika PM - [#4504](https://github.com/NuGet/Home/issues/4504)
* [Ułatwień dostępu.] Pakiet źródła listy rozwijanej i przycisk Ustawienia obcięte podczas wybierania "Microsoft Visual Studio w tryb Offline pakietami" w interfejsie użytkownika PM - [#4502](https://github.com/NuGet/Home/issues/4502)

#### <a name="powershell-management-console-pmc"></a>Konsola zarządzania programu PowerShell (PMC)
* `Update-Package` powoduje ignorowanie zakresu wersji PackageReference - [#6775](https://github.com/NuGet/Home/issues/6775)
* `Update-Package -reinstall` rozwiązanie problemu szerokiego — [#3127](https://github.com/NuGet/Home/issues/3127)
* `Update-Package [packagename] -reinstall` Ponownie instaluje wszystkie pakiety, a nie tylko jedno nazwane - [#737](https://github.com/NuGet/Home/issues/737)
* Można zaktualizować do pakietu NuGet nieznajdujące się na liście za pomocą konsoli Menedżera pakietów - [#4553](https://github.com/NuGet/Home/issues/4553)

#### <a name="misc"></a>Różne
* Aby naprawić `NuGet update self` NuGet.Commandline nupkg nie powinny być semver2.0 - [#7116](https://github.com/NuGet/Home/issues/7116)
* Ulepszenie środowiska z błędami instalacji NU1107 - [#7107](https://github.com/NuGet/Home/issues/7107)
* Serializacja GetAuthenticationCredentialRequest jest niepoprawna — [#6983](https://github.com/NuGet/Home/issues/6983)
* NuGet programu Visual Studio AsyncPackage ładuje się po zainicjowaniu wyłączone przez wątek interfejsu użytkownika — [#6976](https://github.com/NuGet/Home/issues/6976)
* Przywracanie zgłasza potrzeb mylące błędy z informacją project.json — [#6959](https://github.com/NuGet/Home/issues/6959)
* Interfejs użytkownika Menedżera pakietów: podgląd zmian, przycisk ok, które nie są automatycznie użyteczny, klawiatura — [#6893](https://github.com/NuGet/Home/issues/6893)
* RestoreSources są ignorowane w przypadku projektu z odwołania p2p - [#6776](https://github.com/NuGet/Home/issues/6776)
* Tworzenie projektu testu jednostkowego przy użyciu .NET Framework szablon zostanie otwarty starszego modelu projektu z pliku packages.config - [#6736](https://github.com/NuGet/Home/issues/6736)
* Zezwalaj na odwołanie do projektu do zastąpienia zależność pakietu - [#6536](https://github.com/NuGet/Home/issues/6536)
* Udostępnianie NoDefaultExcludes w zadaniu programu MSBuild - [#6450](https://github.com/NuGet/Home/issues/6450)
* Komunikat o stanie dla "Wyczyść wszystkie NuGet Cache(s)" mogą być ukrywane przy zmianie rozmiaru okna - [#5938](https://github.com/NuGet/Home/issues/5938)


[Lista wszystkie problemy rozwiązane w tej wersji](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.8")
