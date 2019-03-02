---
title: Informacje o wersji zapoznawczej 5.0 pakietów NuGet
description: Informacje o wersji dotyczące wersji zapoznawczych NuGet w wersji 5.0 łącznie znane problemy, poprawki, nowe funkcje i DCRs.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 4b05dcb9a2960c1e3231e81d4b4c122d3a518753
ms.sourcegitcommit: 571644118e3c5a2fd818891d305b4b8de8ef21de
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2019
ms.locfileid: "57225891"
---
# <a name="nuget-50-preview-release-notes"></a>Informacje o wersji programu NuGet 5.0 (wersja zapoznawcza)

## <a name="nuget-50-preview-releases"></a>Wersje zapoznawcze NuGet 5.0

* 27 lutego 2019 - [NuGet w wersji 5.0 w wersji zapoznawczej 4](#whats-new-in-nuget-50-preview-4)
* 13 lutego 2019 - [NuGet w wersji 5.0 (wersja zapoznawcza) 3](#whats-new-in-nuget-50-preview-3)
* 23 stycznia 2019 - [NuGet w wersji 5.0 Preview 2](#whats-new-in-nuget-50-preview-2)

## <a name="whats-new-in-nuget-50-preview-4"></a>Co nowego w wersji zapoznawczej NuGet w wersji 5.0 4

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

**Błędy**

* NuGet.VisualStudio.IVsPackageInstaller — wywoływania nad projektem przy użyciu pakietu nie odwołuje się zawsze używa pliku packages.config, nawet wtedy, gdy są ustawione wartości domyślne do elementu PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)

* PMC: Pakiet aktualizacji na pakiety delisted ponownie zainstalować kończy się niepowodzeniem ("nie można odnaleźć pakietu"). - [#7268](https://github.com/NuGet/Home/issues/7268)

* Dodaj uwagi dotyczące innych firm w naszym repozytorium i VSIX — [#7409](https://github.com/NuGet/Home/issues/7409)

* NuGet.VisualStudio.IVsPackageInstaller.InstallPackage należy zainstalować najnowszą wersję, gdy nie została zainstalowana wersja podane - [#7493](https://github.com/NuGet/Home/issues/7493)

* — interakcyjne obsługę wypychania nuget dotnet - [#7519](https://github.com/NuGet/Home/issues/7519)

* Podczas przywracania przy użyciu pliku blokady, nie należy wygenerowany NU1603 ostrzeżenie. - [#7529](https://github.com/NuGet/Home/issues/7529)

* NuGet nie powinno wyświetlić ścieżkę projektu podczas przywracania z minimalnym rejestrowaniem - [#7647](https://github.com/NuGet/Home/issues/7647)

* — interakcyjne pomocy technicznej dla platformy dotnet, usuń pakiet - [#7727](https://github.com/NuGet/Home/issues/7727)

* Dodaj kopię NuGet.Packaging.Core z TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)

* plugins_cache musi krótszą ścieżkę, aby działać prawidłowo - [#7770](https://github.com/NuGet/Home/issues/7770)

* Preferuj ścieżki programu msbuild odnajdywania, jeśli użytkownik przychodzą msbuild określonych wersji — [#7786](https://github.com/NuGet/Home/issues/7786)

**DCRs**

* Ogranicz liczbę żądań http na źródłowym za pośrednictwem pliku NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet powinien dotyczyć Net472 (ułatwiające oczyszczania 16,0 kompilacji VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC: Usuń polecenie OpenPackagePage - [#7384](https://github.com/NuGet/Home/issues/7384)

* Marka NetCoreApp 3.0 mapę, aby NetStandard 2.1 — [#7762](https://github.com/NuGet/Home/issues/7762)

* Dodanie obsługi netstandard2.0 do pakietów NuGet.* - [#6516](https://github.com/NuGet/Home/issues/6516)


## <a name="whats-new-in-nuget-50-preview-3"></a>Co nowego w wersji zapoznawczej NuGet w wersji 5.0 3

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji 

**Błędy**

* nuget.exe /? pomysłem jest wystawienie msbuild poprawne wersje — [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5): błąd: Nie można odnaleźć części ścieżki "/ tmp/NuGetScratch — na mono - [#7793](https://github.com/NuGet/Home/issues/7793)

* Przywracanie niepotrzebnie uwzględnia zawartość wszystkich wersji pakietu odwołanie w pamięci podręcznej maszyny — [#7639](https://github.com/NuGet/Home/issues/7639)

* Po instalacji programu VS 2019 r w wersji zapoznawczej — automatyczne wykrywanie MSBuild zawsze wybiera 16.0 [#7621](https://github.com/NuGet/Home/issues/7621)

* DotNet wyświetlenia listy pakietów na rozwiązanie generuje zduplikowanych wpisów dla framework - [#7607](https://github.com/NuGet/Home/issues/7607)

* Wyjątek "Nazwa pustej ścieżki jest niedozwolona" podczas wywoływania IVsPackageInstaller.InstallPackage na starym projektów, a następnie umieszcza folder nie istnieje. - [#5936](https://github.com/NuGet/Home/issues/5936)

* minimalny poziom szczegółowości MSBuild /t:restore powinny być mniejsze - [#4695](https://github.com/NuGet/Home/issues/4695)

**DCRs**

* Umożliwia autorom pakietów do definiowania zachowania przechodnie zasoby kompilacji - [#6091](https://github.com/NuGet/Home/issues/6091)

* Włączanie funkcji przywracania w programie VS się powieść, jeśli projekt nie jest częścią rozwiązania lub nie jest załadowany, ale została wcześniej przywrócona - [#5820](https://github.com/NuGet/Home/issues/5820)


## <a name="whats-new-in-nuget-50-preview-2"></a>Co nowego w wersji zapoznawczej NuGet w wersji 5.0 2

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

**Błędy**

* VS firmy 16.0 NuGet interfejsu użytkownika ma nie można go odczytać karty z powodu problemów z kolorem - [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet.Core & wyjaśnienie NuGet.Clients License.txt - [#7629](https://github.com/NuGet/Home/issues/7629)

* Przywracanie niepotrzebnie uwzględnia folderu pakietu globalne próbę określenia typu — [#7596](https://github.com/NuGet/Home/issues/7596)

* Błędy z wymuszania pliku blokady powinny być teraz widoczne w oknie Lista błędów - [#7429](https://github.com/NuGet/Home/issues/7429)

* Rozwiązywanie problemów z NuGet.Configuration - [#7326](https://github.com/NuGet/Home/issues/7326)

* Dostosowanie do aktualizowania MSBuild go w lokalizacji instalacji.  - [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet.Build.Tasks.Pack powinny być zależnością programistyczną - [#7249](https://github.com/NuGet/Home/issues/7249)

* Dodaj pakiet rozszerzenia punktu, w tym debugowania symbole - [#7234](https://github.com/NuGet/Home/issues/7234)

* pakietu DotNet powinno zachować zależności zakres wersji w nupkg utworzony. (nawet jeśli jest używana wersja zmiennoprzecinkowego) - [#7232](https://github.com/NuGet/Home/issues/7232)

* DotNet restore kończy się niepowodzeniem w źródle uwierzytelnionego podczas konfiguracji na poziomie użytkownika ma również źródłem — [#7209](https://github.com/NuGet/Home/issues/7209)

* Pakiet, nie należy ograniczyć zestaw BuildActions dla plików zawartości — [#7155](https://github.com/NuGet/Home/issues/7155)

* Za pomocą elementu projectreference, co wymaga AssetTargetFallback została wykonana pomyślnie, należy ostrzec. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Zakleszczenie spowodowane wątkowości problemy podczas wywoływania w systemie CPS (CommonProjectSystem) — [#7103](https://github.com/NuGet/Home/issues/7103)

* polecenia DotNet Dodaj pakiet nie używać poświadczeń z globalnej konfiguracji dla źródła, określony w konfiguracji lokalnej — [#6935](https://github.com/NuGet/Home/issues/6935)

* Wątkowość problemy związane z MEF jest wywoływana dla ścieżek codepath async - [#6771](https://github.com/NuGet/Home/issues/6771)

* Podpisywania: zgłoszony dwa razy i bez stosu wywołań — błąd [#6455](https://github.com/NuGet/Home/issues/6455)

* Instalowanie pakietu podpisane za pomocą niezaufanego certyfikatu podpisywania powinien zostać wyświetlony błąd - [#6318](https://github.com/NuGet/Home/issues/6318)

* Przywracanie NuGet nieprawidłowo NoOps podczas udostępniania katalogu - 2 projektów [#6114](https://github.com/NuGet/Home/issues/6114)

* Nie można używać osobisty token dostępu z przywracania dotnet w systemie Linux przy użyciu pakietów uwierzytelnionego - [#5651](https://github.com/NuGet/Home/issues/5651)

* DotNet restore kończy się niepowodzeniem z powodu wyłączenia maszyny szerokiego źródła danych — [#5410](https://github.com/NuGet/Home/issues/5410)

**DCRs**

* Zestawy NuGet w wersji 5.0, będą musieli .NET 4.7.2 (za pośrednictwem elementu TFM zmiana) - [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData z NuGet.Packaging powinien być typem publicznym. Zaktualizuj metadane licencji pozyskanych z spdx. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Usuń przestarzałe ustawienia interfejsy API — [#7294](https://github.com/NuGet/Home/issues/7294)

* Obejście problemu Przywróć przekroczeń limitu czasu w systemach z 1 procesor cpu — [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet preferuje uwierzytelniania NTLM, nawet jeśli występują poświadczenia w pliku NuGet.config — dodaj opcję konfiguracji do filtrowania typów uwierzytelniania, aby uzyskać poświadczenia — [#5286](https://github.com/NuGet/Home/issues/5286)

* Włącz EmbedInteropTypes dla funkcji PackageReference (pasującego pliku Packages.Config możliwość) - [#2365](https://github.com/NuGet/Home/issues/2365)

[Lista wszystkie problemy rozwiązane w tej wersji 5.0.0-preview2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a>Znane problemy

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>Pakiety w FallbackFolders instalowane przez zestaw .NET Core SDK są zainstalowane niestandardowe i wystąpi niepowodzenie weryfikacji podpisu. - [#7414](https://github.com/NuGet/Home/issues/7414)
**Problem** przy użyciu dotnet.exe 2.x można przywrócić tego netcoreapp wiele elementów docelowych projektu 1.x i netcoreapp 2.x, rezerwowy folderu jest traktowany jako plik źródła danych. Oznacza to, podczas przywracania, NuGet spowoduje pobranie pakietu z rezerwowego folderu i spróbuj zainstalować go w folderze globalnymi pakietami i są zwykle podpisywania sprawdzania poprawności, który kończy się niepowodzeniem.
**Obejście** wyłączyć użycie folderu rezerwowego przez ustawienie `RestoreAdditionalProjectSources` na wartość nothing. `<RestoreAdditionalProjectSources/>` Korzystanie z rozwagą, ponieważ spowoduje to wiele pakietów, które mają być pobrane z repozytorium NuGet.org, które w przeciwnym razie byłoby zostały przywrócone z folderu rezerwowego.
