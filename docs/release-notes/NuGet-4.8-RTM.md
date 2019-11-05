---
title: Informacje o wersji narzędzia NuGet 4,8 RTM
description: Informacje o wersji programu NuGet 4.8.1, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: 6e352fef9fc36646f6feedbc390f847119cb00bf
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611366"
---
# <a name="nuget-48-release-notes"></a>Informacje o wersji narzędzia NuGet 4,8

[Program Visual Studio 2017 15,8 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) zawiera funkcje NuGet 4,8.


Dostępne są również wersje wiersza polecenia o tej samej funkcji:
* NuGet. exe 4,8- [NuGet.org/downloads](https://nuget.org/downloads)
* DotNet. exe- [zestaw .NET Core SDK 2.1.400](https://www.microsoft.com/net/download/visual-studio-sdks)


## <a name="summary-whats-new-in-480"></a>Podsumowanie: co nowego w programie 4.8.0
* NuGet. exe obsługuje teraz LONGFILENAMES w systemie Windows 10 — [#6937](https://github.com/NuGet/Home/issues/6937)
* Wtyczki uwierzytelniania działają teraz między MsBuild, DotNet. exe, NuGet. exe i Visual Studio, w tym między platformą. Pierwsze generowanie wtyczek uwierzytelniania nie było obsługiwane w programie MsBuild, DotNet. exe. Uwaga: kompilacje w wersji zapoznawczej programu VS 2017 15,9 są dołączone do wtyczki uwierzytelniania VSTS. [#6486](https://github.com/NuGet/Home/issues/6486)
* Narzędzie do rozwiązywania konfliktów SDK programu MsBuild jest teraz kompilacją w ramach programu NuGet i instalowane przy użyciu narzędzi NuGet Tools for VS. Spowoduje to uniknięcie synchronizacji wersji. [#6799](https://github.com/NuGet/Home/issues/6799)
* PackageReference obsługuje teraz metadane DevelopmentDependency — [#4125](https://github.com/NuGet/Home/issues/4125)

## <a name="summary-whats-new-in-482"></a>Podsumowanie: co nowego w programie 4.8.2

* Poprawka zabezpieczeń: uprawnienia dla plików utworzonych wewnątrz ~/.NuGet są zbyt otwarte [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="known-issues"></a>Znane problemy
### <a name="installing-signed-packages-on-a-ci-machine-or-in-an-offline-environment-takes-longer-than-usual"></a>Instalowanie podpisanych pakietów na maszynie elementu konfiguracji lub w środowisku offline trwa dłużej niż zwykle

#### <a name="issue"></a>Problem
Jeśli komputer ma ograniczoną dostęp do Internetu (na przykład maszynę kompilacji w scenariuszu ciągłej integracji/ciągłego wdrażania), zainstalowanie/przywrócenie podpisanego pakietu NuGet spowoduje ostrzeżenie ([NU3028](https://docs.microsoft.com/nuget/reference/errors-and-warnings/nu3028)), ponieważ serwery odwołań są niedostępne. To normalne zachowanie. Jednak w niektórych przypadkach może to mieć niezamierzone concequences, takie jak instalacja/przywracanie pakietu trwa dłużej niż zwykle.

#### <a name="workaround"></a>Obejście
Aktualizacja do programu Visual Studio 15.8.4 i NuGet. exe 4.8.1, gdzie została wprowadzona zmienna środowiskowa do przełączania trybu sprawdzania odwołania.
Ustawienie zmiennej środowiskowej `NUGET_CERT_REVOCATION_MODE` na `offline` spowoduje wymuszenie, że pakiet NuGet będzie sprawdzać stan odwołania certyfikatu tylko względem buforowanej listy odwołania certyfikatów, a pakiet NuGet nie podejmie próby dostępu do serwerów odwołania. Gdy tryb sprawdzania odwołania jest ustawiony na `offline`, ostrzeżenie zostanie obniżone do informacji.

> [!Warning]
> Nie zaleca się przełączania trybu sprawdzania odwołania do trybu offline w normalnych cirumstances. Spowoduje to, że program NuGet pominie sprawdzanie odwołań online i wykona tylko sprawdzenie odwołania w trybie offline względem buforowanej listy odwołania certyfikatów, która może być nieaktualna. Oznacza to, że pakiety, w przypadku których certyfikat podpisywania został odwołany, będą nadal instalowane/przywracane, co w przeciwnym razie nie mogło sprawdzić odwołania i nie zostało zainstalowane.

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>Opcja `Migrate packages.config to PackageReference...` nie jest dostępna w menu kontekstowym po kliknięciu prawym przyciskiem myszy

#### <a name="issue"></a>Problem

Po pierwszym otwarciu projektu, pakiet NuGet może nie zostać zainicjowany do momentu wykonania operacji NuGet. Powoduje to, że opcja migracji nie jest wyświetlana w menu kontekstowym prawym przyciskiem myszy w `packages.config` lub `References`.

#### <a name="workaround"></a>Obejście

Wykonaj jedną z następujących akcji NuGet:
* Otwórz interfejs użytkownika Menedżera pakietów — kliknij prawym przyciskiem myszy `References` a następnie wybierz `Manage NuGet Packages...`
* Otwórz konsolę Menedżera pakietów — w obszarze `Tools > NuGet Package Manager`wybierz pozycję `Package Manager Console`
* Uruchom przywracanie NuGet — kliknij prawym przyciskiem myszy węzeł rozwiązania w Eksplorator rozwiązań a następnie wybierz pozycję `Restore NuGet Packages`
* Kompiluj projekt, który również wyzwala przywracanie NuGet

Teraz powinno być możliwe sprawdzenie opcji migracji. Należy zauważyć, że ta opcja nie jest obsługiwana i nie będzie wyświetlana dla ASP.NET C++ i typów projektów.
Uwaga: ten problem został rozwiązany w programie VS 2017 15,9 (wersja zapoznawcza 3)

## <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

### <a name="bugs"></a>Usterki
#### <a name="signing"></a>Pisywać
* Podpisywanie: Instalowanie pakietu podpisanego w środowisku offline [#7008](https://github.com/NuGet/Home/issues/7008) --naprawione w 4.8.1
* Podpisywanie: nieprawidłowe sprawdzanie adresu URL — [#7174](https://github.com/NuGet/Home/issues/7174)
* Podpisywanie: Sprawdź integralność pakietu w RepositorySignatureVerifier, gdy pakiet jest repozytorium podpisane — [#6926](https://github.com/NuGet/Home/issues/6926)
* "Sprawdzanie integralności pakietu nie powiodło się". Identyfikator pakietu powinien znajdować się w komunikacie (i kodzie błędu) — [#6944](https://github.com/NuGet/Home/issues/6944)
* Weryfikacja pakietu podpisanego przez repozytorium zezwala na pakiety podpisane przy użyciu innego certyfikatu — [#6884](https://github.com/NuGet/Home/issues/6884)
* Nie można https://adresu URL podpisywania i sygnatur czasowych NuGet? - [#6871](https://github.com/NuGet/Home/issues/6871)
* Nie NullRef w scenariuszu pakowania NuSpec, Popraw również opcje — [#6866](https://github.com/NuGet/Home/issues/6866)
* Pamięć jest nieprawidłowa podczas aktualizowania informacji dotyczących osoby podpisującej podczas dodawania sygnatury czasowej do kontrpodpis- [#6840](https://github.com/NuGet/Home/issues/6840)
* Podpisywanie: usuwanie wyjątków CTL — [#6794](https://github.com/NuGet/Home/issues/6794)
* Podpisywanie: contentUrl musi być HTTPS- [#6777](https://github.com/NuGet/Home/issues/6777)
* Podpisywanie: SignedPackageVerifierSettings. VSClientDefaultPolicy jest nieużywane — [#6601](https://github.com/NuGet/Home/issues/6601)


#### <a name="pack"></a>Pack
* Przywracanie i kompilowanie nie powinno być konieczne w przypadku używania programu dotnet. exe do pakowania nuspec- [#6866](https://github.com/NuGet/Home/issues/6866)
* Zezwalaj na puste tokeny zastępcze w NuspecProperties — [#6722](https://github.com/NuGet/Home/issues/6722)
* PackTask generuje NullReferenceException, jeśli określono NuspecProperties- [#4649](https://github.com/NuGet/Home/issues/4649)

#### <a name="accessibility"></a>Ułatwienia dostępu
* U Ciąg "wersja wstępna" w obszarze przycisku pakiet jest objęty jego opisem pakietu w interfejsie użytkownika PM — [#4504](https://github.com/NuGet/Home/issues/4504)
* U Przycisk rozwijania i ustawienia źródła pakietu został obcięty podczas wybierania opcji "Microsoft Visual Studio pakietów offline" w interfejsie użytkownika PM — [#4502](https://github.com/NuGet/Home/issues/4502)

#### <a name="powershell-management-console-pmc"></a>Konsola zarządzania programu PowerShell (PMC)
* `Update-Package` ignoruje zakres wersji PackageReference — [#6775](https://github.com/NuGet/Home/issues/6775)
* problem z `Update-Package -reinstall` całym rozwiązaniem — [#3127](https://github.com/NuGet/Home/issues/3127)
* `Update-Package [packagename] -reinstall` ponownie instaluje wszystkie pakiety, a nie tylko nazwane, [#737](https://github.com/NuGet/Home/issues/737)
* Można zaktualizować do nieznajdującego się na liście pakietów NuGet z poziomu konsoli Menedżera pakietów — [#4553](https://github.com/NuGet/Home/issues/4553)

#### <a name="misc"></a>Różne
* Aby naprawić `NuGet update self` NuGet. wiersz polecenia NUPKG nie powinien być semver 2.0- [#7116](https://github.com/NuGet/Home/issues/7116)
* Ulepszanie środowisk z niepowodzeńmi instalacji NU1107 — [#7107](https://github.com/NuGet/Home/issues/7107)
* Serializacja GetAuthenticationCredentialRequest jest niepoprawna- [#6983](https://github.com/NuGet/Home/issues/6983)
* Nie można załadować programu NuGet Visual Studio AsyncPackage po zainicjowaniu wątku interfejsu użytkownika — [#6976](https://github.com/NuGet/Home/issues/6976)
* Przywracanie zgłasza błędne potencjalne błędy podczas określania pliku Project. JSON, który jest wymagany — [#6959](https://github.com/NuGet/Home/issues/6959)
* Interfejs użytkownika Menedżera pakietów: Podgląd zmian, przycisk OK nie jest automatycznie użyteczny przez klawiaturę — [#6893](https://github.com/NuGet/Home/issues/6893)
* RestoreSources są ignorowane dla projektu z odwołaniami P2P- [#6776](https://github.com/NuGet/Home/issues/6776)
* Tworzenie projektu testu jednostkowego przy użyciu szablonu .NET Framework spowoduje otwarcie starszego modelu projektu z pakietem Packages. config — [#6736](https://github.com/NuGet/Home/issues/6736)
* Zezwalaj na odwołanie do projektu w celu przesłaniania zależności pakietu — [#6536](https://github.com/NuGet/Home/issues/6536)
* Uwidacznianie NoDefaultExcludes w programie MSBuild — [#6450](https://github.com/NuGet/Home/issues/6450)
* Komunikat o stanie "Wyczyść wszystkie pamięci podręczne NuGet" może być ukryty w przypadku zmiany rozmiaru okna [#5938](https://github.com/NuGet/Home/issues/5938)


[Lista wszystkich problemów rozwiązanych w tej wersji](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.8")
