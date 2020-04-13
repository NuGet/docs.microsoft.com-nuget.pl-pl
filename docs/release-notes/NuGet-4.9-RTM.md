---
title: Informacje o wydaniu programu NuGet 4.9 RTM
description: Informacje o wersji dla NuGet 4.9, w tym znane problemy, poprawki błędów, nowe funkcje i dcrs.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: e0dea74fe179c0dce4996f3e498185bb3a491856
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496462"
---
# <a name="nuget-49-release-notes"></a>Informacje o wersji nuGet 4.9

Pojazdy dystrybucyjne NuGet:

| Wersja NuGet | Dostępne w wersji programu Visual Studio| Dostępne w plikach .NET SDK|
|:---|:---|:---|
| [**4.9.0**](https://nuget.org/downloads) | [Visual Studio 2017 w wersji 15.9.0](https://visualstudio.microsoft.com/downloads/) | [2.1.500, 2.2.100](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.1**](https://nuget.org/downloads) | Nie dotyczy | Nie dotyczy |
| [**4.9.2**](https://nuget.org/downloads) |[Visual Studio 2017 w wersji 15.9.4](https://visualstudio.microsoft.com/downloads/) | [2.1.502, 2.2.101](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.3**](https://nuget.org/downloads) |[Visual Studio 2017 w wersji 15.9.6](https://visualstudio.microsoft.com/downloads/) | [2.1.504, 2.2.104](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a>Krótki opis: Co nowego w 4.9.0

* Podpisywanie: Włącz ClientPolicies wymagać użycia zestawu zaufanych autorów i repozytoriów wymienionych w NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blogu](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)

* tworzenie plików ".snupkg" zawierają symbole w opakowaniu - poprawić push do zrozumienia protokołu nuget do akceptowania plików snupkg dla serwera symboli - [#6878](https://github.com/NuGet/Home/issues/6878), [blogu](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)

* Wtyczka poświadczeń NuGet V2 - [#6642](https://github.com/NuGet/Home/issues/6642)

* Samodzielne pakiety NuGet - Licencja - [#4628](https://github.com/NuGet/Home/issues/4628), [ogłoszenie](https://github.com/NuGet/Announcements/issues/32)

* Włącz metadane opt-in "GeneratePathProperty" na PackageReference, aby wygenerować właściwość na pakiet MSBuild do katalogu "Foo.Bar\1.0\" katalogu — [#6949](https://github.com/NuGet/Home/issues/6949)

* Zwiększ sukces klienta dzięki operacjom NuGet - [#7108](https://github.com/NuGet/Home/issues/7108)

* Włącz powtarzalne przywracanie pakietu za pomocą pliku blokady - [#5602](https://github.com/NuGet/Home/issues/5602), [ogłoszenie](https://github.com/NuGet/Announcements/issues/28), wpis [w blogu](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

* Ostrzeżenia podwyższone do błędów (za pośrednictwem WarnAsErrors) wywoływane przez PackageExtraction nigdy nie powinny pozostawiać wyodrębnionych pakietów wokół - [#7445](https://github.com/NuGet/Home/issues/7445)

* Źle podpisane pakiety nie powinny trafić do folderu pakietów globalnych - [#7423](https://github.com/NuGet/Home/issues/7423)

* generowanie przekierowania wiązania nie powinno pomijać zespołów elewacyjnych - [#7393](https://github.com/NuGet/Home/issues/7393)

* VersionRange Equals nie porównuje zakresów przestawnych — [#7324](https://github.com/NuGet/Home/issues/7324)

* Przywracanie: regresja wydajności przy użyciu nowego stosu HTTP .NET Core 2.1 - [#7314](https://github.com/NuGet/Home/issues/7314)

* Aktualizacja pakietu nie należy modyfikować PrivateAssets packageReference - [#7285](https://github.com/NuGet/Home/issues/7285)

* Podpisywanie: podpisywanie powinno zakończyć się niepowodzeniem, jeśli pakiet ma zbyt wiele wpisów pakietu (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)

* Ścieżka kodu "dotnet nuget push" powinna obsługiwać nowego dostawcę poświadczeń — [#7233](https://github.com/NuGet/Home/issues/7233)

* Obsługa wykonywania wtyczek z niezmienną kulturą (jak to się dzieje w docker) - [#7223](https://github.com/NuGet/Home/issues/7223)

* nuget sources add nie należy usuwać poświadczeń z pliku NuGet.config — [#7200](https://github.com/NuGet/Home/issues/7200)

* instalowanie devDependency PackageReference powinien domyślnie excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)

* fix migrator opcja, która ma być wyświetlana dla wszystkich projektów i pokazać błąd, jeśli projekt jest niezgodny - [#6958](https://github.com/NuGet/Home/issues/6958)

* "dotnet add package" powinien zatwierdzić przywracanie, które wykonuje w pliku zasobów - [#6928](https://github.com/NuGet/Home/issues/6928)

* Podpisywanie: ulepszanie komunikatów o błędach związanych z podpisywaniem — [#6906](https://github.com/NuGet/Home/issues/6906)

* [Błąd testu] [zh-TW] Ciąg "Konsola menedżera pakietów" nie lokalizuje się na konsoli Menedżera pakietów — [#6381](https://github.com/NuGet/Home/issues/6381)

* Komunikat o błędzie wokół "Nie można znaleźć informacji o projekcie" powinien być nieco bardziej szczegółowy wewnątrz VS — [#5350](https://github.com/NuGet/Home/issues/5350)

* Niepomocny komunikat o błędzie, gdy niepoprawnie przy użyciu nuspec tag wersji nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)

* DCR - Podpisywanie: obsługa protokołu NuGet: RepozytoriumSignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)

* DCR - plik .nupkg.metadata zostanie utworzony podczas wyodrębniania pakietu - zawiera "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)

* DCR - Pomiń weryfikację authenticode dla wtyczek podczas wykonywania na Mono - [#7222](https://github.com/NuGet/Home/issues/7222)

[Lista wszystkich problemów rozwiązanych w tej wersji 4.9.0](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a>Krótki opis: Co nowego w 4.9.1

* Dodaj obsługę czytania zapisu do nuget.config za pomocą nowego polecenia zaufanych sygnatariuszy - [#7480](https://github.com/NuGet/Home/issues/7480)

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

* Napraw generowanie łączy licencji - [#7515](https://github.com/NuGet/Home/issues/7515)

* Regresja kodów błędów do sprawdzania poprawności podpisów - [#7492](https://github.com/NuGet/Home/issues/7492)

* Pakiet NuGet.Build.Tasks.Pack nie zawiera informacji o licencji — [#7379](https://github.com/NuGet/Home/issues/7379)

[Lista wszystkich problemów rozwiązanych w tej wersji 4.9.1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a>Krótki opis: Co nowego w 4.9.2

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

* Narzędzie VS/dotnet.exe/nuget.exe/msbuild.exe przywracanie nie używa poświadczeń, gdy nazwa źródła zawiera odstęp - [#7517](https://github.com/NuGet/Home/issues/7517)

* LicenseAcceptanceWindow i LicenseFileWindow Problemy z dostępnością - [#7452](https://github.com/NuGet/Home/issues/7452)

* Fix FormatException w DateTime.Parse z DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)

[Lista wszystkich problemów rozwiązanych w tej wersji 4.9.2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a>Krótki opis: Co nowego w 4.9.3

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a>Problemy z "powtarzalnym pakietem przy użyciu pliku blokady"

* Tryb zablokowany nie działa jako skrót jest obliczany niepoprawnie dla wcześniej buforowanych pakietów - [#7682](https://github.com/NuGet/Home/issues/7682)

* Przywracanie rozwiązuje do innej wersji `packages.lock.json` niż zdefiniowane w pliku - [#7667](https://github.com/NuGet/Home/issues/7667)

* '--locked-mode / RestoreLockedMode' powoduje fałszywe błędy przywracania, gdy zaangażowane są wnioskowania projectreferences - [#7646](https://github.com/NuGet/Home/issues/7646)

* Program rozpoznawania nazw zestawu SDK msbuild próbuje zweryfikować sha dla pakietu zestawu SDK, który nie powiedzie się przywrócenie podczas korzystania z packages.lock.json - [#7599](https://github.com/NuGet/Home/issues/7599)

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a>Problemy "Blokowanie zależności przy użyciu konfigurowalnych zasad zaufania"
* dotnet.exe nie powinien oceniać zaufanych sygnatariuszy, gdy podpisane pakiety nie są obsługiwane - [#7574](https://github.com/NuGet/Home/issues/7574)

* Kolejność zaufanych podpisywzorów w pliku konfiguracyjnym wpływa na ocenę zaufania - [#7572](https://github.com/NuGet/Home/issues/7572)

* Nie można zaimplementować ustawień ISettings [Spowodowane przez refaktoryzowanie ustawień interfejsów API do obsługi funkcji zasad zaufania] - [#7614](https://github.com/NuGet/Home/issues/7614)

#### <a name="improved-debugging-experience-issues"></a>Problemy z "ulepszonym debugowaniem"

* Nie można opublikować pakietu symboli dla narzędzia globalnego .NET Core — [#7632](https://github.com/NuGet/Home/issues/7632)

#### <a name="self-contained-nuget-packages---license-issues"></a>Problemy z "samodzielnymi pakietami NuGet — licencja"

* Błąd podczas tworzenia symbolu .snupkg podczas korzystania z osadzonego pliku licencji - [#7591](https://github.com/NuGet/Home/issues/7591)

[Lista wszystkich problemów rozwiązanych w tej wersji 4.9.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")

## <a name="summary-whats-new-in-494"></a>Krótki opis: Co nowego w 4.9.4

* Poprawka zabezpieczeń: Uprawnienia do plików utworzonych wewnątrz ~/.nuget są zbyt otwarte [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)


## <a name="known-issues"></a>Znane problemy

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519"></a>dotnet nuget push --interactive daje błąd na komputerze Mac. - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>Problem
Argument `--interactive` nie jest przekazywany przez dotnet cli i powoduje błąd`error: Missing value for option 'interactive'`

#### <a name="workaround"></a>Obejście
Uruchom inne polecenie dotnet z opcją `dotnet restore --interactive` interaktywną, taką jak i uwierzytelnij. Uwierzytelnianie może być buforowane przez dostawcę poświadczeń. Następnie należy uruchomić polecenie `dotnet nuget push`.

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a>Pakiety w składach rezerwowych zainstalowanych przez pakiet .NET Core SDK są instalowane na zamówienie i nie można ich sprawdzania poprawności. - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>Problem
W przypadku korzystania z pliku dotnet.exe 2.x w celu przywrócenia projektu, który zawiera wiele celów netcoreapp 1.x i netcoreapp 2.x, folder rezerwowy jest traktowany jako plik danych. Oznacza to, że podczas przywracania NuGet wybierze pakiet z folderu rezerwowego i spróbuje zainstalować go w folderze pakietów globalnych i wykonaj zwykłe sprawdzanie poprawności podpisywania, które zakończy się niepowodzeniem.

#### <a name="workaround"></a>Obejście
Wyłącz użycie folderu rezerwowego, `RestoreAdditionalProjectSources` ustawiając na nic. `<RestoreAdditionalProjectSources/>`Użyj tego ostrożnie, ponieważ spowoduje to wiele pakietów do pobrania z NuGet.org które w przeciwnym razie zostałyby przywrócone z folderu rezerwowego.
