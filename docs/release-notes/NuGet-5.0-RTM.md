---
title: Informacje o wersji 5.0 RTM NuGet
description: Informacje o wersji programu NuGet 5.0 łącznie znane problemy, poprawki, nowe funkcje i DCRs.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 5e48ff19ea5c4908d7eb0a3cb19a31b738e348eb
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/18/2019
ms.locfileid: "58921588"
---
# <a name="nuget-50-release-notes"></a>Informacje o wersji 5.0 NuGet

NuGet pojazdów dystrybucji:

| NuGet w wersji | Dostępne w wersji programu Visual Studio| Dostępne w zestawów SDK platformy .NET|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 version 16.0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>instalowane z Visual Studio 2019 r przy użyciu obciążenia platformy .NET Core 

<sup>2</sup>jest dostępna jako opcjonalna instalacja przy użyciu programu Visual Studio 2019 r przy użyciu obciążenia platformy .NET Core

## <a name="summary-whats-new-in-50"></a>Podsumowanie: Co nowego w wersji 5.0

* Obsługa przywracania [filtrowane rozwiązania](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) w programie Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` folder umożliwia pakietów została przechodnio współtworzyć celów/arkuszy właściwości do projektu hosta — [#6091](https://github.com/NuGet/Home/issues/6091)
* Lepsza obsługa scenariuszy PackageReference w interfejsach API wektory NuGet — [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` jest przestarzała - [#7928](https://github.com/NuGet/Home/issues/7928)
* Dodatek dostawcy poświadczeń Gen 1 została zastąpiona przez [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) i zostanie wkrótce staną się przestarzałe — [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

**Błędy**

* W trakcie przywracania aktualizujący nie działa, należy unikać *. dgspec.json zapisu w katalogu obj — [#7854](https://github.com/NuGet/Home/issues/7854)

* Uprawnień do plików utworzony wewnątrz ~/.nuget są zbyt otwarte — [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` nie działa ze źródeł, które wymagają uwierzytelniania - [#7605](https://github.com/NuGet/Home/issues/7605)

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

* `nuget.exe /?` pomysłem jest wystawienie msbuild poprawne wersje — [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5): błąd: Nie można odnaleźć części ścieżki "/ tmp/NuGetScratch — na mono - [#7793](https://github.com/NuGet/Home/issues/7793)

* Przywracanie niepotrzebnie uwzględnia zawartość wszystkich wersji pakietu odwołanie w pamięci podręcznej maszyny — [#7639](https://github.com/NuGet/Home/issues/7639)

* Po instalacji programu VS 2019 r w wersji zapoznawczej — automatyczne wykrywanie MSBuild zawsze wybiera 16.0 [#7621](https://github.com/NuGet/Home/issues/7621)

* DotNet wyświetlenia listy pakietów na rozwiązanie generuje zduplikowanych wpisów dla framework - [#7607](https://github.com/NuGet/Home/issues/7607)

* Wyjątek "Nazwa pustej ścieżki jest niedozwolona" podczas wywoływania IVsPackageInstaller.InstallPackage na starym projektów, a następnie umieszcza folder nie istnieje. - [#5936](https://github.com/NuGet/Home/issues/5936)

* minimalny poziom szczegółowości MSBuild /t:restore powinny być mniejsze - [#4695](https://github.com/NuGet/Home/issues/4695)

* VS firmy 16.0 NuGet interfejsu użytkownika ma nie można go odczytać karty z powodu problemów z kolorem - [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet.Core & wyjaśnienie NuGet.Clients License.txt - [#7629](https://github.com/NuGet/Home/issues/7629)

* Przywracanie niepotrzebnie uwzględnia folderu pakietu globalne próbę określenia typu — [#7596](https://github.com/NuGet/Home/issues/7596)

* Błędy z wymuszania pliku blokady powinny być teraz widoczne w oknie Lista błędów - [#7429](https://github.com/NuGet/Home/issues/7429)

* Rozwiązywanie problemów z NuGet.Configuration - [#7326](https://github.com/NuGet/Home/issues/7326)

* Dostosowanie do aktualizowania swoich instalacji programu MSBuild lokalizacji — [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet.Build.Tasks.Pack powinny być zależnością programistyczną - [#7249](https://github.com/NuGet/Home/issues/7249)

* Dodaj pakiet rozszerzenia punktu, w tym debugowania symbole - [#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` zakres wersji zależności w utworzonej nupkg powinno zachować (nawet jeśli jest używana wersja zmiennoprzecinkowego) - [#7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore` kończy się niepowodzeniem w źródle uwierzytelnionego podczas konfiguracji na poziomie użytkownika ma również źródłem — [#7209](https://github.com/NuGet/Home/issues/7209)

* Pakiet, nie należy ograniczyć zestaw BuildActions dla plików zawartości — [#7155](https://github.com/NuGet/Home/issues/7155)

* Za pomocą elementu ProjectReference, co wymaga AssetTargetFallback została wykonana pomyślnie, należy ostrzec. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Zakleszczenie spowodowane wątkowości problemy podczas wywoływania w systemie CPS (CommonProjectSystem) — [#7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` nie używa poświadczeń z globalnej konfiguracji dla źródła, określony w konfiguracji lokalnej — [#6935](https://github.com/NuGet/Home/issues/6935)

* Wątkowości problemy związane z MEF wywoływane na asynchronicznej kodu ścieżki - [#6771](https://github.com/NuGet/Home/issues/6771)

* Podpisywania: zgłoszony dwa razy i bez stosu wywołań — błąd [#6455](https://github.com/NuGet/Home/issues/6455)

* Instalowanie pakietu podpisane za pomocą niezaufanego certyfikatu podpisywania powinien zostać wyświetlony błąd - [#6318](https://github.com/NuGet/Home/issues/6318)

* Przywracanie NuGet nieprawidłowo NoOps podczas udostępniania katalogu - 2 projektów [#6114](https://github.com/NuGet/Home/issues/6114)

* Nie można użyć osobisty token dostępu z `dotnet restore` w systemie Linux przy użyciu pakietów uwierzytelnionego - [#5651](https://github.com/NuGet/Home/issues/5651)

* DotNet restore kończy się niepowodzeniem z powodu wyłączenia maszyny szerokiego źródła danych — [#5410](https://github.com/NuGet/Home/issues/5410)

**DCRs**

* Ostrzega o usunięcia "pakietu dotnet project.json" — w przyszłości [#7928](https://github.com/NuGet/Home/issues/7928)
 
* Dodaj ostrzeżenie o zakończeniu obsługi dla wtyczki poświadczeń Gen1 - [#7819](https://github.com/NuGet/Home/issues/7819)
 
* Signing: Włączone repozytorium, aby wymagać weryfikacji klienta dla każdego pakietu jako repozytorium podpisane — za pośrednictwem zasobów RepositorySignatures/5.0.0 - [#7759](https://github.com/NuGet/Home/issues/7759)

* Ogranicz liczbę żądań http na źródłowym za pośrednictwem pliku NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet powinien dotyczyć Net472 (ułatwiające oczyszczania 16,0 kompilacji VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC: Usuń polecenie OpenPackagePage - [#7384](https://github.com/NuGet/Home/issues/7384)

* Marka NetCoreApp 3.0 mapę, aby NetStandard 2.1 — [#7762](https://github.com/NuGet/Home/issues/7762)

* Dodanie obsługi netstandard2.0 do pakietów NuGet.* - [#6516](https://github.com/NuGet/Home/issues/6516)

* Umożliwia autorom pakietów do definiowania zachowania przechodnie zasoby kompilacji - [#6091](https://github.com/NuGet/Home/issues/6091)

* Obsługa funkcji Filtr rozwiązania 2019 programu VS. Obsługuje również projektu nie w rozwiązaniu lub zwolnione projektów. Konieczność jego przywrócenia kompletnego rozwiązania (za pośrednictwem interfejsu wiersza polecenia lub programu VS), najpierw - [#5820](https://github.com/NuGet/Home/issues/5820)

* Zestawy NuGet w wersji 5.0, będą musieli .NET 4.7.2 (za pośrednictwem elementu TFM zmiana) - [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData z NuGet.Packaging powinien być typem publicznym. Zaktualizuj metadane licencji pozyskanych z spdx. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Usuń przestarzałe ustawienia interfejsy API — [#7294](https://github.com/NuGet/Home/issues/7294)

* Obejście problemu Przywróć przekroczeń limitu czasu w systemach z 1 procesor cpu — [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet preferuje uwierzytelniania NTLM, nawet jeśli występują poświadczenia w pliku NuGet.config — dodaj opcję konfiguracji do filtrowania typów uwierzytelniania, aby uzyskać poświadczenia — [#5286](https://github.com/NuGet/Home/issues/5286)

* Włącz EmbedInteropTypes dla funkcji PackageReference (pasującego pliku Packages.Config możliwość) - [#2365](https://github.com/NuGet/Home/issues/2365)

**[Lista wszystkie problemy rozwiązane w tej wersji - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="known-issues"></a>Znane problemy

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>Pakiety w FallbackFolders instalowane przez zestaw .NET Core SDK są zainstalowane niestandardowe i wystąpi niepowodzenie weryfikacji podpisu. - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>Problem
Korzystając z dotnet.exe 2.x można przywrócić tego netcoreapp wiele elementów docelowych projektu 1.x i netcoreapp 2.x, rezerwowy folderu jest traktowany jako plik źródła danych. Oznacza to, podczas przywracania, NuGet spowoduje pobranie pakietu z rezerwowego folderu i spróbuj zainstalować go w folderze globalnymi pakietami i są zwykle podpisywania sprawdzania poprawności, który kończy się niepowodzeniem.<br>
#### <a name="workaround"></a>Obejście
Wyłącz użycie folderu rezerwowy, ustawiając `RestoreAdditionalProjectSources` na wartość nothing:

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

Korzystaj z niej ostrożnie jak pakiety, które zostaną przywrócone z folderu rezerwowego teraz zostaną pobrane z witryny NuGet.org.
