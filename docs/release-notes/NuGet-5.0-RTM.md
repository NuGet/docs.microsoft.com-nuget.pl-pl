---
title: Informacje o wersji narzędzia NuGet 5,0 RTM
description: Informacje o wersji programu NuGet 5,0, w tym znane problemy, poprawki błędów, nowe funkcje i DCR.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: e4a6be7fb26e3cc4bd297eaf02999f6ac1389b77
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236805"
---
# <a name="nuget-50-release-notes"></a>Informacje o wersji narzędzia NuGet 5,0

Pojazdy dystrybucji NuGet:

| Wersja programu NuGet | Dostępne w wersji programu Visual Studio| Dostępne w zestawach SDK platformy .NET|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 w wersji 16,0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |
| [**5.0.2**](https://nuget.org/downloads) | [Visual Studio 2019 w wersji 16.0.4](https://visualstudio.microsoft.com/downloads/) | [2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Zainstalowane z programem Visual Studio 2019 przy użyciu obciążenia .NET Core 

<sup>2</sup> Dostępne jako opcjonalna instalacja z programem Visual Studio 2019 przy użyciu obciążenia .NET Core

## <a name="summary-whats-new-in-50"></a>Podsumowanie: co nowego w 5,0

* Obsługa przywracania [filtrowanych rozwiązań](/visualstudio/ide/filtered-solutions?view=vs-2019) w programie Visual Studio 2019 — [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` folder umożliwia pakietom przechodnie Współtworzenie elementów docelowych/props do projektu hosta — [#6091](https://github.com/NuGet/Home/issues/6091)
* Lepsza obsługa scenariuszy PackageReference w interfejsach API NuGet użycie japońskich ideograficznych — [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` jest przestarzałe — [#7928](https://github.com/NuGet/Home/issues/7928)
* Wtyczka dostawcy poświadczeń generacji 1 została zastąpiona przez [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) i wkrótce będzie przestarzała — [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

**Usterek**

* Podczas wykonywania operacji przywracania aktualizujący nie działa należy unikać * .dgspec.jsprzy zapisie w katalogu obj- [#7854](https://github.com/NuGet/Home/issues/7854)

* Uprawnienia dla plików utworzonych wewnątrz ~/.NuGet są zbyt otwarte- [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` nie działa ze źródłami, które wymagają uwierzytelniania [#7605](https://github.com/NuGet/Home/issues/7605)

* NuGet. VisualStudio. IVsPackageInstaller-calling dla projektu bez odwołań do pakietów zawsze używa packages.config, nawet jeśli wartość domyślna to PackageReference- [#7005](https://github.com/NuGet/Home/issues/7005)

* PMC: ponowne zainstalowanie Update-Package nie powiodło się ("nie można znaleźć pakietu") w odniesieniu do pakietów z listą. - [#7268](https://github.com/NuGet/Home/issues/7268)

* Dodaj powiadomienie innej firmy w naszym repozytorium i VSIX- [#7409](https://github.com/NuGet/Home/issues/7409)

* Pakiet NuGet. VisualStudio. IVsPackageInstaller. InstallPackage powinien instalować najnowszą wersję, gdy nie podaną w wersji — [#7493](https://github.com/NuGet/Home/issues/7493)

* --Interaktywna obsługa wypychania NuGet programu dotnet- [#7519](https://github.com/NuGet/Home/issues/7519)

* Podczas przywracania przy użyciu pliku blokady nie należy zgłaszać ostrzeżenia NU1603. - [#7529](https://github.com/NuGet/Home/issues/7529)

* Pakiet NuGet nie powinien drukować ścieżki projektu podczas przywracania przy minimalnym rejestrowaniu — [#7647](https://github.com/NuGet/Home/issues/7647)

* --Interaktywna pomoc techniczna dotycząca usuwania pakietu dotnet- [#7727](https://github.com/NuGet/Home/issues/7727)

* Dodaj wstecz NuGet. pakowanie. Core z TypeForwardedTo attrs- [#7768](https://github.com/NuGet/Home/issues/7768)

* plugins_cache potrzebuje krótszej ścieżki do prawidłowego działania — [#7770](https://github.com/NuGet/Home/issues/7770)

* Preferuj ścieżkę dla odnajdywania MSBuild, jeśli użytkownik nie poprosił o określoną wersję programu MSBuild — [#7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` należy wyświetlić listę prawidłowych wersji programu MSBuild — [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet. targets (498, 5): błąd: nie można odnaleźć części ścieżki "/tmp/NuGetScratch-on mono- [#7793](https://github.com/NuGet/Home/issues/7793)

* przywrócenie niepotrzebnie wylicza zawartość wszystkich wersji pakietu, do którego istnieje odwołanie w pamięci podręcznej maszyn — [#7639](https://github.com/NuGet/Home/issues/7639)

* Funkcja automatycznego wykrywania programu MSBuild zawsze wybiera 16,0 po zainstalowaniu programu VS 2019 w wersji zapoznawczej — [#7621](https://github.com/NuGet/Home/issues/7621)

* pakiet listy dotnet w rozwiązaniu wyprowadza zduplikowane wpisy dla struktury — [#7607](https://github.com/NuGet/Home/issues/7607)

* Wyjątek "pusta nazwa ścieżki nie jest dozwolona" podczas wywoływania IVsPackageInstaller. InstallPackage w starych projektach i folderze Packages nie istnieje. - [#5936](https://github.com/NuGet/Home/issues/5936)

* MSBuild/t: Przywróć minimalny poziom szczegółowości powinien być bardziej minimalny- [#4695](https://github.com/NuGet/Home/issues/4695)

* Interfejs użytkownika NuGet programu VS 16.0 zawiera nieczytelne karty z powodu problemów z kolorem — [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet. Core & NuGet. klienci License.txt Wyjaśnij — [#7629](https://github.com/NuGet/Home/issues/7629)

* Przywrócenie niekoniecznie wylicza folder pakietu globalnego podczas próby określenia typu [#7596](https://github.com/NuGet/Home/issues/7596)

* Błędy wymuszania blokady plików powinny być wyświetlane w Lista błędów oknie [#7429](https://github.com/NuGet/Home/issues/7429)

* Rozwiązywanie problemów z NuGet.Configwersja — [#7326](https://github.com/NuGet/Home/issues/7326)

* Dostosuj do programu MSBuild, aktualizując jego lokalizację instalacji — [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet. Build. Tasks. Pack musi być zależnością programistyczną — [#7249](https://github.com/NuGet/Home/issues/7249)

* Dodaj punkt rozszerzenia pakietu dla dołączania symboli debugowania — [#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` należy zachować zakres wersji zależności w utworzonym NUPKG (nawet jeśli używana jest wersja przestawna) — [#7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore`Niepowodzenie w przypadku uwierzytelnionego źródła, jeśli konfiguracja na poziomie użytkownika ma również [#7209](https://github.com/NuGet/Home/issues/7209) źródła

* Pakiet nie powinien ograniczać zestawu BuildActions dla plików zawartości — [#7155](https://github.com/NuGet/Home/issues/7155)

* Przy użyciu elementu ProjectReference, który wymaga pomyślnego AssetTargetFallback, powinno być wyświetlane ostrzeżenie. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Zakleszczenie ze względu na problemy z wątkami podczas wywoływania metody CPS (CommonProjectSystem) — [#7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` nie używa poświadczeń z konfiguracji globalnej dla źródła określonego w konfiguracji lokalnej — [#6935](https://github.com/NuGet/Home/issues/6935)

* Problemy z wątkami z MEFem wywoływane w asynchronicznych ścieżkach kodu — [#6771](https://github.com/NuGet/Home/issues/6771)

* Podpisywanie: zgłoszono błąd dwukrotnie i bez stosu wywołań — [#6455](https://github.com/NuGet/Home/issues/6455)

* W przypadku instalowania pakietu podpisanego z niezaufanym certyfikatem podpisywania powinien zostać wyświetlony komunikat o błędzie [#6318](https://github.com/NuGet/Home/issues/6318)

* Przywracanie NuGet nie NoOps prawidłowo, gdy 2 projekty współużytkują katalog obj- [#6114](https://github.com/NuGet/Home/issues/6114)

* Nie można użyć `dotnet restore` źródła danych z systemem Linux z pakietami ze uwierzytelnionego kanału informacyjnego — [#5651](https://github.com/NuGet/Home/issues/5651)

* dotnet restore nie powiodło się z powodu wyłączenia kanału informacyjnego całego komputera — [#5410](https://github.com/NuGet/Home/issues/5410)

**DCR**

* Ostrzegaj o przyszłym usunięciu elementu "dotnet Pack project.json"- [#7928](https://github.com/NuGet/Home/issues/7928)
 
* Dodaj ostrzeżenie o zaniechaniu wtyczki poświadczeń Gen1 — [#7819](https://github.com/NuGet/Home/issues/7819)
 
* Podpisywanie: włączone repozytorium, aby wymagać weryfikacji klienta każdego pakietu jako podpisanego przez repozytorium — za pośrednictwem RepositorySignatures/5.0.0 zasobu — [#7759](https://github.com/NuGet/Home/issues/7759)

* Ogranicz liczbę żądań HTTP na źródło za pośrednictwem NuGet.Config- [#4538](https://github.com/NuGet/Home/issues/4538)

* Pakiet NuGet powinien wskazywać Net472 (aby ułatwić czyszczenie kompilacji 16,0 w VSIX) — [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC: usuwanie OpenPackagePage polecenia [#7384](https://github.com/NuGet/Home/issues/7384)

* Tworzenie mapy NetCoreApp 3,0 w programie Standard 2,1 — [#7762](https://github.com/NuGet/Home/issues/7762)

* Dodaj obsługę programu Standard 2.0 do pakietu NuGet. * pakiety — [#6516](https://github.com/NuGet/Home/issues/6516)

* Zezwalaj autorom pakietów na definiowanie zachowania przechodniego zasobów kompilacji — [#6091](https://github.com/NuGet/Home/issues/6091)

* Obsługa funkcji filtrowania rozwiązań VS 2019. Program obsługuje również projekty, które nie są w rozwiązaniu lub nie zostały zwolnione. Należy przywrócić kompletne rozwiązanie (za pomocą interfejsu wiersza polecenia lub VS) jako pierwsze [#5820](https://github.com/NuGet/Home/issues/5820)

* Zestawy NuGet 5,0 wymagające programu .NET 4.7.2 (za pośrednictwem zmiany TFM) — [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData z NuGet. opakowanie powinno być typem publicznym. Aktualizowanie metadanych licencji pozyskanych z SPDX. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Usuwanie przestarzałych ustawień API- [#7294](https://github.com/NuGet/Home/issues/7294)

* Obejście limitów czasu przywracania w systemach z 1 [#6742](https://github.com/NuGet/Home/issues/6742) procesora CPU

* Pakiet NuGet preferuje uwierzytelnianie NTLM, nawet jeśli istnieją poświadczenia w opcji NuGet.config Dodaj konfigurację, aby filtrować typy uwierzytelniania dla poświadczeń — [#5286](https://github.com/NuGet/Home/issues/5286)

* Włącz funkcję EmbedInteropTypes dla PackageReference (zgodna Packages.Config) — [#2365](https://github.com/NuGet/Home/issues/2365)

**[Lista wszystkich problemów rozwiązanych w tym wydaniu — 5,0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="summary-whats-new-in-502"></a>Podsumowanie: co nowego w programie 5.0.2

* Zabezpieczenia (w przypadku uruchamiania przez dotnet.exe lub mono.exe) — folder obj powinien zostać utworzony z prawidłowymi uprawnieniami [#7908](https://github.com/NuGet/Home/issues/7908)

* nuget.exe przywracanie na platformie mono/MacOS kończy się niepowodzeniem z niestandardowym nuget.config i `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)


## <a name="known-issues"></a>Znane problemy

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a>Pakiety w FallbackFolders zainstalowane przez zestaw .NET Core SDK są zainstalowane niestandardowo i nie można zweryfikować podpisu. - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>Problem
W przypadku korzystania z dotnet.exe 2. x w celu przywrócenia projektu, który ma wiele obiektów docelowych netcoreapp 1. x i netcoreapp 2. x, folder rezerwowy jest traktowany jako źródło plików. Oznacza to, że podczas przywracania program NuGet wybierze pakiet z folderu rezerwowego i spróbuje go zainstalować w folderze pakiety globalne i wykonać zwykłą weryfikację podpisywania, która kończy się niepowodzeniem.<br>
#### <a name="workaround"></a>Obejście
Wyłącz użycie folderu rezerwowego, ustawiając wartość `RestoreAdditionalProjectSources` Nothing:

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

Należy to zrobić z ostrożnością, ponieważ pakiety, które zostałyby przywrócone z folderu rezerwowego, zostaną teraz pobrane z NuGet.org.