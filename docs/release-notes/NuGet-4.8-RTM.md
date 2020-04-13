---
title: Informacje o wydaniu programu NuGet 4.8 RTM
description: Informacje o wersji dla NuGet 4.8.1, w tym znane problemy, poprawki błędów, dodane funkcje i BDR.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: e6f6d9f703dd4761236d166f3772618c100aca09
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "76813770"
---
# <a name="nuget-48-release-notes"></a>Informacje o wersji nuGet 4.8

[Visual Studio 2017 15.8 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest wyposażony w funkcje NuGet 4.8.


Dostępne są również wersje wiersza polecenia tej samej funkcji:
* NuGet.exe 4.8 - [nuget.org/downloads](https://nuget.org/downloads)
* DotNet.exe - [.NET Core SDK 2.1.400](https://www.microsoft.com/net/download/visual-studio-sdks)


## <a name="summary-whats-new-in-480"></a>Krótki opis: Co nowego w 4.8.0
* NuGet.exe obsługuje teraz longfilemes w systemie Windows 10 - [#6937](https://github.com/NuGet/Home/issues/6937)
* Wtyczki uwierzytelniania działają teraz w msbuild, DotNet.exe, NuGet.exe i Visual Studio, w tym na wielu platformach. Pierwsza generacja wtyczek uwierzytelniania nie były obsługiwane w MsBuild, DotNet.exe. Uwaga: Kompilacje w wersji zapoznawczej VS 2017 15.9 mają włączony włączono wtyczkę uwierzytelniania VSTS. [#6486](https://github.com/NuGet/Home/issues/6486)
* MsBuild's SDK Resolver teraz buduje jako część NuGet i instaluje za pomocą narzędzi NuGet dla VS. Pozwoli to uniknąć wersji wychodzenia z synchronizacji. [#6799](https://github.com/NuGet/Home/issues/6799)
* PackageReference obsługuje teraz metadane rozwojuzależności — [#4125](https://github.com/NuGet/Home/issues/4125)

## <a name="summary-whats-new-in-482"></a>Krótki opis: Co nowego w 4.8.2

* Poprawka zabezpieczeń: Uprawnienia do plików utworzonych wewnątrz ~/.nuget są zbyt otwarte [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="known-issues"></a>Znane problemy
### <a name="installing-signed-packages-on-a-ci-machine-or-in-an-offline-environment-takes-longer-than-usual"></a>Instalowanie podpisanych pakietów na komputerze ciągłej integracji lub w środowisku offline trwa dłużej niż zwykle

#### <a name="issue"></a>Problem
Jeśli urządzenie ma ograniczony dostęp do Internetu (na przykład komputer kompilacji w scenariuszu ciągłej integracji/ciągłego wdrażania), zainstalowanie/przywrócenie podpisanego pakietu nuget spowoduje ostrzeżenie[(NU3028),](../reference/errors-and-warnings/nu3028.md)ponieważ serwery odwołania nie są osiągalne. Jest to oczekiwane. Jednak w niektórych przypadkach może to mieć niezamierzone poczęcia, takie jak instalacja/przywracanie pakietu trwa dłużej niż zwykle.

#### <a name="workaround"></a>Obejście
Aktualizacja do programu Visual Studio 15.8.4 i NuGet.exe 4.8.1, gdzie wprowadziliśmy zmienną środowiskową, aby przełączyć tryb sprawdzania odwołania.
Ustawienie `NUGET_CERT_REVOCATION_MODE` zmiennej `offline` środowiskowej wymusi nuget sprawdzić stan odwołania certyfikatu tylko na liście odwołania buforowanego certyfikatu, a NuGet nie będzie próbował uzyskać dostępu do serwerów odwołania. Gdy tryb sprawdzania odwołania jest `offline`ustawiony na , ostrzeżenie zostanie obniżone do informacji.

> [!Warning]
> Nie zaleca się przełączania trybu sprawdzania odwołania do trybu offline w normalnych cirumstances. Spowoduje to, że NuGet pominąć sprawdzanie odwołania online i wykonać tylko sprawdzanie odwołania w trybie offline względem listy odwołania certyfikatu w pamięci podręcznej, które mogą być nieaktualne. Oznacza to, że pakiety, w których certyfikat podpisywania mógł zostać odwołany, będą nadal instalowane/przywracane, co w przeciwnym razie nie powiodłoby się i nie zostałoby zainstalowane.

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>Opcja `Migrate packages.config to PackageReference...` ta nie jest dostępna w menu kontekstowym po kliknięciu prawym przyciskiem myszy

#### <a name="issue"></a>Problem

Po pierwszym otwarciu projektu NuGet może nie zainicjować, dopóki nie zostanie wykonana operacja NuGet. Powoduje to, że opcja migracji nie jest chlubna w menu kontekstowym po kliknięciu prawym przyciskiem myszy lub `packages.config` `References`.

#### <a name="workaround"></a>Obejście

Wykonaj dowolną z następujących akcji NuGet:
* Otwórz interfejs użytkownika Menedżera pakietów `References` — kliknij prawym przyciskiem myszy i wybierz pozycję`Manage NuGet Packages...`
* Otwórz konsolę Menedżera `Tools > NuGet Package Manager`pakietów — od , wybierz`Package Manager Console`
* Uruchom przywracanie NuGet - Kliknij prawym przyciskiem myszy węzeł rozwiązania w Eksploratorze rozwiązań i wybierz pozycję`Restore NuGet Packages`
* Tworzenie projektu, który również wyzwala przywracanie NuGet

Teraz powinna być widoczna opcja migracji. Należy zauważyć, że ta opcja nie jest obsługiwana i nie będzie wyświetlana dla typów projektów ASP.NET i C++.
Uwaga: Naprawiono to w wersji zapoznawczej VS 2017 15.9 Preview 3

## <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

### <a name="bugs"></a>Usterki
#### <a name="signing"></a>Podpisywanie
* Podpisywanie: Instalowanie podpisanego pakietu w środowisku offline [#7008](https://github.com/NuGet/Home/issues/7008) — poprawiono w 4.8.1
* Podpisywanie: niepoprawne sprawdzanie adresu URL - [#7174](https://github.com/NuGet/Home/issues/7174)
* Podpisywanie: sprawdź integralność pakietu w RepozytoriumSignatureVerifier, gdy pakiet jest kontrasygnowany repozytorium - [#6926](https://github.com/NuGet/Home/issues/6926)
* "Sprawdzanie integralności pakietu nie powiodło się." powinien mieć identyfikator pakietu w komunikacie (i kod błędu) - [#6944](https://github.com/NuGet/Home/issues/6944)
* Weryfikacja pakietu podpisanego przez repozytorium umożliwia pakiety podpisane przez różne certyfikaty - [#6884](https://github.com/NuGet/Home/issues/6884)
* NuGet - Podpisywanie - Adres URL sygnatury czasowej nie może być https:// ? - [#6871](https://github.com/NuGet/Home/issues/6871)
* Nie NullRef w scenariuszu pakowania NuSpec, również poprawić opcje - [#6866](https://github.com/NuGet/Home/issues/6866)
* Pamięć jest nieprawidłowa podczas aktualizowania informacji o sygnatariuszu podczas dodawania sygnatury czasowej do kontrasygnatury - [#6840](https://github.com/NuGet/Home/issues/6840)
* Podpisywanie: usuwanie wyjątków CTL - [#6794](https://github.com/NuGet/Home/issues/6794)
* Podpisywanie: contentUrl MUSI być HTTPS - [#6777](https://github.com/NuGet/Home/issues/6777)
* Podpisywanie: SignedPackageVerifierSettings.VSClientDefaultPolicy jest nieużywane - [#6601](https://github.com/NuGet/Home/issues/6601)


#### <a name="pack"></a>Dodatkiem service pack
* przywracanie i kompilacja nie powinny być potrzebne podczas korzystania z dotnet.exe do pakowania nuspec - [#6866](https://github.com/NuGet/Home/issues/6866)
* Zezwalaj na puste tokeny zastępcze w NuspecProperties - [#6722](https://github.com/NuGet/Home/issues/6722)
* PackTask zgłasza NullReferenceException, gdy nuspecProperties jest określony - [#4649](https://github.com/NuGet/Home/issues/4649)

#### <a name="accessibility"></a>Ułatwienia dostępu
* [Dostępność] Ciąg "Prerelease" pod przyciskiem pakietu jest objęty opisem pakietu w pm ui - [#4504](https://github.com/NuGet/Home/issues/4504)
* [Dostępność] Przycisk rozwijany źródła pakietu i ustawienia obcięty podczas wybierania opcji "Pakiety trybu offline programu Microsoft Visual Studio" w interfejsie pm ui — [#4502](https://github.com/NuGet/Home/issues/4502)

#### <a name="powershell-management-console-pmc"></a>Konsola zarządzania programem Powershell (PMC)
* `Update-Package`ignoruje zakres wersji PackageReference - [#6775](https://github.com/NuGet/Home/issues/6775)
* `Update-Package -reinstall`rozwiązanie szerokiego problemu - [#3127](https://github.com/NuGet/Home/issues/3127)
* `Update-Package [packagename] -reinstall`ponownie instaluje wszystkie pakiety, a nie tylko o nazwie - [#737](https://github.com/NuGet/Home/issues/737)
* Można zaktualizować do niepublicznych nuget pakietu z konsoli Menedżera pakietów - [#4553](https://github.com/NuGet/Home/issues/4553)

#### <a name="misc"></a>Różne
* Aby `NuGet update self` naprawić NuGet.Commandline nupkg nie powinno być semver2.0 - [#7116](https://github.com/NuGet/Home/issues/7116)
* Usprawnij jakość pracy dzięki błędom instalacji NU1107 - [#7107](https://github.com/NuGet/Home/issues/7107)
* Serializacja GetAuthenticationCredentialRequest jest niepoprawna - [#6983](https://github.com/NuGet/Home/issues/6983)
* NuGet Visual Studio AsyncPackage nie można załadować po zainicjowaniu wątku interfejsu użytkownika — [#6976](https://github.com/NuGet/Home/issues/6976)
* Przywracanie zgłasza mylące błędy stwierdzające, że project.json jest potrzebny - [#6959](https://github.com/NuGet/Home/issues/6959)
* Interfejs menedżera pakietów : podgląd zmian, przycisk ok nie jest automatycznie używany przez klawiaturę - [#6893](https://github.com/NuGet/Home/issues/6893)
* RestoreSources są ignorowane dla projektu z odwołaniami p2p - [#6776](https://github.com/NuGet/Home/issues/6776)
* Tworzenie projektu testu jednostkowego przy użyciu szablonu programu .NET Framework spowoduje otwarcie starszego modelu projektu z packages.config — [#6736](https://github.com/NuGet/Home/issues/6736)
* zezwalaj na odwołanie do projektu, aby zastąpić zależność pakietu - [#6536](https://github.com/NuGet/Home/issues/6536)
* Uwidacznianie NoDefaultExcludes w msbuild zadanie - [#6450](https://github.com/NuGet/Home/issues/6450)
* Komunikat o stanie dla "Wyczyść wszystkie pamięci podręczne NuGet" mogą być ukryte przy rozmiarze okna — [#5938](https://github.com/NuGet/Home/issues/5938)


[Lista wszystkich problemów rozwiązanych w tej wersji](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.8")
