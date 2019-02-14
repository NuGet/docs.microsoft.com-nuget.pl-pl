---
title: Informacje o wersji 4.9 RTM NuGet
description: Informacje o wersji programu NuGet 4.9 łącznie znane problemy, poprawki, nowe funkcje i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: aa9bf87504477506dbb1e9ac10d5c1d5841c224f
ms.sourcegitcommit: 885973352d31808e3ddbb45da6d6e54d1e4fca9d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/13/2019
ms.locfileid: "56224947"
---
# <a name="nuget-49-release-notes"></a>4.9 wersji NuGet

NuGet pojazdów dystrybucji:

| NuGet w wersji | Dostępne w wersji programu Visual Studio| Dostępne w zestawów SDK platformy .NET|
|:---|:---|:---|
| [**4.9.0**](https://nuget.org/downloads) | [Visual Studio 2017 w wersji 15.9.0](https://visualstudio.microsoft.com/downloads/) | [2.1.500, 2.2.100](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.1**](https://nuget.org/downloads) | n/d | n/d |
| [**4.9.2**](https://nuget.org/downloads) |[Visual Studio 2017 w wersji 15.9.4](https://visualstudio.microsoft.com/downloads/) | [2.1.502, 2.2.101](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.3**](https://nuget.org/downloads) |[Visual Studio 2017 w wersji 15.9.6](https://visualstudio.microsoft.com/downloads/) | [2.1.504, 2.2.104](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a>Podsumowanie: What's New in 4.9.0

* Signing: Włącz ClientPolicies wymagać korzystanie z zestawu zaufanych autorzy i repozytoriów, wymienione w pliku NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [wpis w blogu](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)

* Tworzenie plików ".snupkg" zawierają symbole w pakiecie — Zwiększ wypchnięcie, aby zrozumieć nuget protokołu do akceptowania plików snupkg do serwera symboli - [#6878](https://github.com/NuGet/Home/issues/6878), [wpis w blogu](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)

* Wtyczka poświadczeń NuGet w wersji 2 - [#6642](https://github.com/NuGet/Home/issues/6642)

* Pakiety NuGet niezależna - License - [#4628](https://github.com/NuGet/Home/issues/4628), [anonsu](https://github.com/NuGet/Announcements/issues/32)

* Włącz zoptymalizowany pod kątem w metadanych "GeneratePathProperty" na PackageReference do wygenerowania dla właściwości MSBuild pakietu na "Foo.Bar\1.0\" katalogu — [#6949](https://github.com/NuGet/Home/issues/6949)

* Zwiększyć sukces klientów przy użyciu operacji NuGet — [#7108](https://github.com/NuGet/Home/issues/7108)

* Włącz Przywracanie pakietów powtarzalne przy użyciu blokady pliku — [#5602](https://github.com/NuGet/Home/issues/5602), [ogłoszenie](https://github.com/NuGet/Announcements/issues/28), [wpis w blogu](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

* Ostrzeżenia z podwyższonym poziomem uprawnień na błędy (za pośrednictwem WarnAsErrors), które zostały wygenerowane przez PackageExtraction nigdy nie należy pozostawić wyodrębniony pakiet wokół - [#7445](https://github.com/NuGet/Home/issues/7445)

* Nieprawidłowo podpisanych pakietów nie powinna kończyć w folderze globalnymi pakietami - [#7423](https://github.com/NuGet/Home/issues/7423)

* Powiązanie generowania przekierowania nie należy pomijać zestawy fasady - [#7393](https://github.com/NuGet/Home/issues/7393)

* Jest równe VersionRange nie porównania zmiennoprzecinkowy zakresów — [#7324](https://github.com/NuGet/Home/issues/7324)

* Przywracanie: stos regresji wydajności przy użyciu protokołu HTTP nowej platformy .NET Core 2.1 — [#7314](https://github.com/NuGet/Home/issues/7314)

* Aktualizacja pakietu nie należy modyfikować PrivateAssets PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)

* Podpisywanie: podpisywanie powinna zakończyć się niepowodzeniem Jeżeli pakiet zawiera zbyt wiele wpisów pakietu (> 65534)- [#7248](https://github.com/NuGet/Home/issues/7248)

* prefiksu "dotnet nuget wypychania" powinien obsługiwać nowego dostawcę poświadczeń - [#7233](https://github.com/NuGet/Home/issues/7233)

* Obsługuje wykonywanie wtyczek przy użyciu niezmiennej kultury (tak jak wykonywane na platformie docker) - [#7223](https://github.com/NuGet/Home/issues/7223)

* Dodaj źródła nuget, nie należy usuwać poświadczenia w pliku NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)

* Instalowanie devDependency PackageReference powinny domyślnie excludeassets = kompilacji - [#7084](https://github.com/NuGet/Home/issues/7084)

* Usuń opcję migrator ma być wyświetlany dla wszystkich projektów i Pokaż błąd, jeśli projekt jest niezgodny - [#6958](https://github.com/NuGet/Home/issues/6958)

* "dotnet Dodaj pakiet" powinien zużywać przywracania sprawdzi się w pliku zasobów - [#6928](https://github.com/NuGet/Home/issues/6928)

* Podpisywanie: poprawa podpisywania pokrewne komunikaty o błędach - [#6906](https://github.com/NuGet/Home/issues/6906)

* [Niepowodzenie testu] [zh-TW] Ciąg "Konsola Menedżera pakietów" nie zlokalizować w konsoli Menedżera pakietów - [#6381](https://github.com/NuGet/Home/issues/6381)

* Komunikat o błędzie wokół "Nie można odnaleźć informacji o projekcie" powinna być nieco bardziej szczegółowe wewnątrz VS - [#5350](https://github.com/NuGet/Home/issues/5350)

* Komunikat o błędzie zbędny, korzystając z niepoprawnie nuspec tag wersji pakietu nuget — [#2714](https://github.com/NuGet/Home/issues/2714)

* DCR - podpisywania: obsługują protokół NuGet: Zasób RepositorySignatures/4.9.0 - [#7421](https://github.com/NuGet/Home/issues/7421)

* DCR —. zostanie teraz utworzony plik nupkg.metadata podczas wyodrębniania pakietu - zawiera "zawartość hash" - [#7283](https://github.com/NuGet/Home/issues/7283)

* DCR - pomijania weryfikacji authenticode dla wtyczek podczas wykonywania w Mono - [#7222](https://github.com/NuGet/Home/issues/7222)

[Lista wszystkie problemy rozwiązane w tej wersji 4.9.0](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a>Podsumowanie: What's New in 4.9.1

* Dodano obsługę odczytu zapisu do pliku nuget.config, za pomocą nowego polecenia zaufanych — które podpisały - [#7480](https://github.com/NuGet/Home/issues/7480)

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

* Napraw Generowanie konsolidacji licencji - [#7515](https://github.com/NuGet/Home/issues/7515)

* Kody błędów regresji do weryfikowania podpisów- [#7492](https://github.com/NuGet/Home/issues/7492)

* Pakiet NuGet.Build.Tasks.Pack nie ma informacji o licencjach - [#7379](https://github.com/NuGet/Home/issues/7379)

[Lista wszystkie problemy rozwiązane w tej wersji 4.9.1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a>Podsumowanie: What's New in 4.9.2

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

* VS/dotnet.exe/nuget.exe/msbuild.exe przywracania nie używa poświadczeń, gdy nazwa źródła zawiera odstępem - [#7517](https://github.com/NuGet/Home/issues/7517)

* Problemy dotyczące LicenseAcceptanceWindow i dostępności LicenseFileWindow — [#7452](https://github.com/NuGet/Home/issues/7452)

* Usuń formatexception — na przykład DateTime.Parse z DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)

[Lista wszystkie problemy rozwiązane w tej wersji 4.9.2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a>Podsumowanie: What's New in 4.9.3

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a>Problemy z "Pozycji powtarzalne pakietu za pomocą pliku blokady"

* Zablokowany tryb nie działa zgodnie z wyznaczania wartości skrótu jest obliczana niepoprawnie dla wcześniej pamięci podręcznej pakietów - [#7682](https://github.com/NuGet/Home/issues/7682)

* Przywracanie jest rozpoznawana jako do innej wersji niż zdefiniowana w `packages.lock.json` pliku — [#7667](https://github.com/NuGet/Home/issues/7667)

* "--Tryb zablokowany / RestoreLockedMode" powoduje, że fałszywe błędy przywracania w przypadku odwołania do projektu - [#7646](https://github.com/NuGet/Home/issues/7646)

* Mechanizm rozpoznawania zestawu SDK programu MSBuild próbuje zweryfikować SHA dla pakietu SDK, który zakończy się niepowodzeniem przywracania przy użyciu packages.lock.json — [#7599](https://github.com/NuGet/Home/issues/7599)

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a>"Zablokować zależności za pomocą zasad można skonfigurować zaufanie" problemów
* DotNet.exe nie należy ocenić zaufane osoby podpisujące podpisanych pakietów nie są obsługiwane - [#7574](https://github.com/NuGet/Home/issues/7574)

* Kolejność trustedSigners w pliku konfiguracji ma wpływ na ocenę zaufania - [#7572](https://github.com/NuGet/Home/issues/7572)

* Nie można zaimplementować ISettings [spowodowany refaktoryzacją ustawienia interfejsów API do obsługi funkcji zasady zaufania]- [#7614](https://github.com/NuGet/Home/issues/7614)

#### <a name="improved-debugging-experience-issues"></a>"Improved środowisko debugowania" problemów

* Nie można opublikować pakietu symboli dla platformy .NET Core globalnego narzędzia - [#7632](https://github.com/NuGet/Home/issues/7632)

#### <a name="self-contained-nuget-packages---license-issues"></a>Problemy z "Pakiety NuGet niezależna - licencji"

* Wystąpił błąd podczas tworzenia pakietu .snupkg symboli, korzystając z osadzonych pliku licencji - [#7591](https://github.com/NuGet/Home/issues/7591)

[Lista wszystkie problemy rozwiązane w tej wersji 4.9.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")
## <a name="known-issues"></a>Znane problemy

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a>DotNet nuget push--interaktywne powoduje błąd na komputerze Mac. - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>Problem
`--interactive` Argument nie są przekazywane przez interfejs wiersza polecenia platformy dotnet i powoduje błąd `error: Missing value for option 'interactive'`

#### <a name="workaround"></a>Obejście
Aby możliwe było uruchamianie dowolnego polecenia dotnet z opcją interaktywnych, takich jak `dotnet restore --interactive` i uwierzytelniania. Uwierzytelnianie, program może być buforowane przez dostawcę poświadczeń. Następnie uruchom `dotnet nuget push`.

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>Pakiety w FallbackFolders instalowane przez zestaw .NET Core SDK są zainstalowane niestandardowe i wystąpi niepowodzenie weryfikacji podpisu. - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>Problem
Korzystając z dotnet.exe 2.x można przywrócić tego netcoreapp wiele elementów docelowych projektu 1.x i netcoreapp 2.x, rezerwowy folderu jest traktowany jako plik źródła danych. Oznacza to, podczas przywracania, NuGet spowoduje pobranie pakietu z rezerwowego folderu i spróbuj zainstalować go w folderze globalnymi pakietami i są zwykle podpisywania sprawdzania poprawności, który kończy się niepowodzeniem.

#### <a name="workaround"></a>Obejście
Wyłącz użycie folderu rezerwowy, ustawiając `RestoreAdditionalProjectSources` na wartość nothing. `<RestoreAdditionalProjectSources/>` Korzystanie z rozwagą, ponieważ spowoduje to wiele pakietów, które mają być pobrane z repozytorium NuGet.org, które w przeciwnym razie byłoby zostały przywrócone z folderu rezerwowego.
