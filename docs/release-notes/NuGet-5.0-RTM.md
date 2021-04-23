---
title: Informacje o wersji NuGet 5.0 RTM
description: Informacje o wersji dla programu NuGet 5.0, w tym znane problemy, poprawki usterek, nowe funkcje i kontrolery domeny.
author: JonDouglas
ms.author: jodou
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 19173d2be7cd66b65651655385466b40f5e08352
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901749"
---
# <a name="nuget-50-release-notes"></a>Informacje o wersji nuGet 5.0

Pojazdy dystrybucji NuGet:

| Wersja nuGet | Dostępne w Visual Studio wersji| Dostępne w zestawach SDK platformy .NET|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 w wersji 16.0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1,</sup> [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |
| [**5.0.2**](https://nuget.org/downloads) | [Visual Studio 2019 w wersji 16.0.4](https://visualstudio.microsoft.com/downloads/) | [2.1.60x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1,</sup> [2.2.20x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Zainstalowane z programem Visual Studio 2019 z obciążeniem .NET Core 

<sup>2.</sup> Dostępna jako instalacja opcjonalna w programie Visual Studio 2019 z obciążeniem .NET Core

## <a name="summary-whats-new-in-50"></a>Podsumowanie: co nowego w 5.0

* Obsługa przywracania [filtrowanych rozwiązań w](/visualstudio/ide/filtered-solutions) programie Visual Studio 2019 — [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` folder umożliwia pakietom przechodnie współtwoście obiektów docelowych/propek w projekcie hosta [— #6091](https://github.com/NuGet/Home/issues/6091)
* Lepsza obsługa scenariuszy PackageReference w interfejsach API pakietów NuGet IVs [— #7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` jest przestarzała [— #7928](https://github.com/NuGet/Home/issues/7928)
* Wtyczka gen 1 Dostawca poświadczeń została zastąpiona przez gen [2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) i wkrótce zostanie wycofana [—](https://github.com/NuGet/Home/issues/7819) #7819

## <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

**Błędów**

* Podczas wykonywania przywracania NoOp należy unikać *.dgspec.jszapisu w katalogu obj — [#7854](https://github.com/NuGet/Home/issues/7854)

* Uprawnienia do plików utworzonych w pliku ~/.nuget są zbyt otwarte [— #7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` nie działa ze źródłami, które wymagają uwierzytelniania [— #7605](https://github.com/NuGet/Home/issues/7605)

* NuGet.VisualStudio.IVsPackageInstaller — wywoływanie w projekcie bez odwołań do pakietu zawsze używa packages.config, nawet jeśli wartość domyślna to PackageReference — [#7005](https://github.com/NuGet/Home/issues/7005)

* PMC: Update-Package ponownej instalacji nie powiedzie się ("Nie można odnaleźć pakietu") w pakietach wywłaszowanych. - [#7268](https://github.com/NuGet/Home/issues/7268)

* Dodawanie powiadomienia innej firmy w naszym repo i VSIX — [#7409](https://github.com/NuGet/Home/issues/7409)

* Pakiet NuGet.VisualStudio.IVsPackageInstaller.InstallPackage powinien zostać zainstalowany w najnowszej wersji, jeśli nie podano wersji — [#7493](https://github.com/NuGet/Home/issues/7493)

* --interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)

* Podczas przywracania przy użyciu pliku blokady nie powinno być wyświetlane ostrzeżenie NU1603. - [#7529](https://github.com/NuGet/Home/issues/7529)

* Program NuGet nie powinien drukować ścieżki projektu podczas przywracania przy minimalnym rejestrowaniu [— #7647](https://github.com/NuGet/Home/issues/7647)

* --interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)

* Dodaj ponownie element NuGet.Packaging.Core z elementem TypeForwardedTo attrs — [#7768](https://github.com/NuGet/Home/issues/7768)

* plugins_cache wymaga krótszej ścieżki do pracy — [#7770](https://github.com/NuGet/Home/issues/7770)

* Preferuj ścieżkę odnajdywania msbuild, jeśli użytkownik nie prosił o określoną wersję programu msbuild — [#7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` Powinien wyświetlić listę poprawnych wersji programu msbuild [— #7794](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5): błąd: Nie można odnaleźć części ścieżki '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)

* Przywróć niepotrzebnie wylicza zawartość wszystkich wersji przywoływanego pakietu w pamięci podręcznej maszyny [—](https://github.com/NuGet/Home/issues/7639) #7639

* Automatyczne wykrywanie w programie MSBuild zawsze wybiera 16.0 po zainstalowaniu programu VS 2019 (wersja [zapoznawcza)](https://github.com/NuGet/Home/issues/7621) — #7621

* Dotnet list package on a solution outputs duplicate entries for framework - #7607 (Pakiet dotnet list rozwiązania wyprowadza zduplikowane wpisy dla struktury [— #7607](https://github.com/NuGet/Home/issues/7607)

* Wyjątek "Pusta nazwa ścieżki nie jest legalna" podczas wywoływania funkcji IVsPackageInstaller.InstallPackage w starych projektach i folderze pakietów nie istnieje. - [#5936](https://github.com/NuGet/Home/issues/5936)

* Msbuild /t:restore minimalny poziom szczegółowości powinien być bardziej minimalny — [#4695](https://github.com/NuGet/Home/issues/4695)

* Interfejs użytkownika nuGet programu VS 16.0 ma nieczytelne karty z powodu problemów z kolorami [—](https://github.com/NuGet/Home/issues/7735) #7735

* Wyjaśnienie License.txt NuGet.Core & NuGet.Clients — [#7629](https://github.com/NuGet/Home/issues/7629)

* Przywróć niepotrzebnie wylicza globalny folder pakietu w celu określenia typu [—](https://github.com/NuGet/Home/issues/7596) #7596

* Błędy z wymuszania pliku blokady powinny być wyświetlane w oknie lista błędów [— #7429](https://github.com/NuGet/Home/issues/7429)

* Rozwiązywanie NuGet.Configproblemów z adresami [URL — #7326](https://github.com/NuGet/Home/issues/7326)

* Dostosowanie do aktualizacji lokalizacji instalacji programu MSBuild — [#7325](https://github.com/NuGet/Home/issues/7325)

* Pakiet NuGet.Build.Tasks.Pack powinien być zależnością deweloperska [— #7249](https://github.com/NuGet/Home/issues/7249)

* Dodawanie punktu rozszerzenia pakietu w celu uwzględnienia symboli debugowania [— #7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` należy zachować zakres wersji zależności w utworzonym nupkg (nawet jeśli jest używana wersja zmiennoprzecinkowa) — [#7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore` kończy się niepowodzeniem w uwierzytelnionym źródle, gdy konfiguracja na poziomie użytkownika również ma [źródło — #7209](https://github.com/NuGet/Home/issues/7209)

* Pakiet nie powinien ograniczać zestawu akcji BuildAction dla plików zawartości [— #7155](https://github.com/NuGet/Home/issues/7155)

* W przypadku użycia składnika ProjectReference, które wymaga powodzenia funkcji AssetTargetFallback, należy ostrzec. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Zakleszczenie z powodu problemów z wątkami podczas wywoływania do systemu CPS (CommonProjectSystem) [— #7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` nie używa poświadczeń z konfiguracji globalnej dla źródła określonego w konfiguracji lokalnej — [#6935](https://github.com/NuGet/Home/issues/6935)

* Problemy z wątkami dotyczące wywoływania mef w asynchronicznych ścieżkach kodu [— #6771](https://github.com/NuGet/Home/issues/6771)

* Podpisywanie: błąd zgłoszony dwukrotnie i bez stosu wywołań [— #6455](https://github.com/NuGet/Home/issues/6455)

* Instalowanie podpisanego pakietu z niezaufanymi certyfikatami podpisywania powinno pokazywać błąd [— #6318](https://github.com/NuGet/Home/issues/6318)

* Nieprawidłowe przywracanie NuGet NoOps, gdy 2 projekty współużytkują katalog obj — [#6114](https://github.com/NuGet/Home/issues/6114)

* Nie można użyć patu dostępu z `dotnet restore` w systemie Linux z pakietami z uwierzytelnionego źródła danych — [#5651](https://github.com/NuGet/Home/issues/5651)

* dotnet restore kończy się niepowodzeniem z powodu wyłączenia szerokiego źródła danych komputera [— #5410](https://github.com/NuGet/Home/issues/5410)

**DcRs (Kontrolery domeny)**

* Ostrzeganie o przyszłym usunięciu "pakietu dotnet project.jssię" — [#7928](https://github.com/NuGet/Home/issues/7928)
 
* Dodawanie ostrzeżenia o cofaniu pracy dla wtyczki poświadczeń Gen1 [— #7819](https://github.com/NuGet/Home/issues/7819)
 
* Podpisywanie: włączone repozytorium, aby wymagać weryfikacji klienta każdego pakietu jako podpisanego repozytorium — za pośrednictwem zasobu RepositorySignatures/5.0.0 [—](https://github.com/NuGet/Home/issues/7759) #7759

* ograniczanie liczby żądań HTTP na źródło za pośrednictwem NuGet.Config — [#4538](https://github.com/NuGet/Home/issues/4538)

* Program NuGet powinien być ukierunkowany na net472 (aby ułatwić oczyszczanie kompilacji 16.0 vsix) [— #7143](https://github.com/NuGet/Home/issues/7143)

* PMC: polecenie Remove OpenPackagePage — [#7384](https://github.com/NuGet/Home/issues/7384)

* Mapowanie aplikacji NetCoreApp 3.0 na netStandard 2.1 [— #7762](https://github.com/NuGet/Home/issues/7762)

* Dodanie obsługi netstandard2.0 do pakietów NuGet.* — [#6516](https://github.com/NuGet/Home/issues/6516)

* Zezwalaj autorom pakietów na definiowanie zachowania przechodniego zasobów kompilacji [— #6091](https://github.com/NuGet/Home/issues/6091)

* Obsługa funkcji filtru rozwiązań programu VS 2019. Obsługuje również projekt, który nie znajduje się w rozwiązaniu, lub niezaładowane projekty. Najpierw należy przywrócić kompletne rozwiązanie (za pośrednictwem interfejsu wiersza polecenia lub programu VS) [— #5820](https://github.com/NuGet/Home/issues/5820)

* Zestawy NuGet 5.0 wymagające programu .NET 4.7.2 (za pośrednictwem zmiany tfm) [— #7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData z nuGet.Packaging powinien być typem publicznym. Aktualizowanie metadanych licencji pozyskanych z pliku spdx. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Usuwanie przestarzałych interfejsów API ustawień [— #7294](https://github.com/NuGet/Home/issues/7294)

* Obejście limitów czasu przywracania w systemach z 1 procesorem CPU [— #6742](https://github.com/NuGet/Home/issues/6742)

* NuGet preferuje uwierzytelnianie NTLM, nawet jeśli istnieją poświadczenia w NuGet.config — dodaj opcję konfiguracji, aby filtrować typy uwierzytelniania dla poświadczeń — [#5286](https://github.com/NuGet/Home/issues/5286)

* Włączanie wartości EmbedInteropTypes dla funkcji PackageReference (dopasowywanie Packages.Config) — [#2365](https://github.com/NuGet/Home/issues/2365)

**[Lista wszystkich problemów rozwiązanych w tej wersji — 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="summary-whats-new-in-502"></a>Podsumowanie: co nowego w 5.0.2

* Zabezpieczenia (uruchamiane za pośrednictwem dotnet.exe lub mono.exe) — folder obj powinien [](https://github.com/NuGet/Home/issues/7908) zostać utworzony z prawidłowymi uprawnieniami #7908

* nuget.exe przywracania w systemie mono/MacOS kończy się niepowodzeniem z niestandardowymi nuget.config i `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)


## <a name="known-issues"></a>Znane problemy

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a>Pakiety w programie FallbackFolders zainstalowane przez zestaw .NET Core SDK są instalowane niestandardowo i walidacja podpisu nie powiedzie się. - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>Problem
W przypadku dotnet.exe 2.x w celu przywrócenia projektu, który zawiera wielo targets netcoreapp 1.x i netcoreapp 2.x, folder rezerwowy jest traktowany jako źródło danych plików. Oznacza to, że podczas przywracania program NuGet wybierze pakiet z folderu rezerwowego i spróbuje go zainstalować w globalnym folderze pakietów i przejmie standardową walidację podpisywania, co zakończy się niepowodzeniem.<br>
#### <a name="workaround"></a>Obejście
Wyłącz użycie folderu rezerwowego, ustawiając dla opcji `RestoreAdditionalProjectSources` wartości nothing:

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

Należy zachować ostrożność, ponieważ pakiety, które zostaną przywrócone z folderu rezerwowego, zostaną teraz pobrane z NuGet.org.