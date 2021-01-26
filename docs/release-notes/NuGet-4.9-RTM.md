---
title: Informacje o wersji narzędzia NuGet 4,9 RTM
description: Informacje o wersji programu NuGet 4,9, w tym znane problemy, poprawki błędów, nowe funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 429218fa4968d572ef187ef1dbfacac8a3bde2b4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780148"
---
# <a name="nuget-49-release-notes"></a>Informacje o wersji narzędzia NuGet 4,9

Pojazdy dystrybucji NuGet:

| Wersja programu NuGet | Dostępne w wersji programu Visual Studio| Dostępne w zestawach SDK platformy .NET|
|:---|:---|:---|
| [**4.9.0**](https://nuget.org/downloads) | [Visual Studio 2017 w wersji 15.9.0](https://visualstudio.microsoft.com/downloads/) | [2.1.500, 2.2.100](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.1**](https://nuget.org/downloads) | nie dotyczy | nie dotyczy |
| [**4.9.2**](https://nuget.org/downloads) |[Visual Studio 2017 w wersji 15.9.4](https://visualstudio.microsoft.com/downloads/) | [2.1.502, 2.2.101](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.3**](https://nuget.org/downloads) |[Visual Studio 2017 w wersji 15.9.6](https://visualstudio.microsoft.com/downloads/) | [2.1.504, 2.2.104](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a>Podsumowanie: co nowego w programie 4.9.0

* Podpisywanie: Włącz ClientPolicies, aby wymagać użycia zestawu zaufanych autorów i repozytoriów wymienionych w NuGet.Config- [#6961](https://github.com/NuGet/Home/issues/6961), [wpis w blogu](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)

* Utwórz pliki ". snupkg", aby zawierały symbole w pakiecie — ulepszanie wypychania, aby zrozumieć protokół NuGet, aby akceptować pliki snupkg dla serwera symboli — [#6878](https://github.com/NuGet/Home/issues/6878), [wpis w blogu](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)

* Wtyczka poświadczeń NuGet v2- [#6642](https://github.com/NuGet/Home/issues/6642)

* Self-Contained pakietów NuGet — licencja [#4628](https://github.com/NuGet/Home/issues/4628), [ogłoszenie](https://github.com/NuGet/Announcements/issues/32)

* Włącz opcję "GeneratePathProperty" metadanych na PackageReference, aby wygenerować Właściwość programu MSBuild dla pakietu na "foo. Bar\1.0 \" Directory- [#6949](https://github.com/NuGet/Home/issues/6949)

* Popraw sukces klientów dzięki operacjom NuGet — [#7108](https://github.com/NuGet/Home/issues/7108)

* Włącz przywracanie Powtórzonego pakietu przy użyciu pliku blokady — [#5602](https://github.com/NuGet/Home/issues/5602), [ogłoszenie](https://github.com/NuGet/Announcements/issues/28), [wpis w blogu](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

* Ostrzeżenia z błędami (przez WarnAsErrors) wywoływane przez PackageExtraction nigdy nie powinny opuszczać wyodrębnionego pakietu [#7445](https://github.com/NuGet/Home/issues/7445)

* Nieprawidłowo podpisane pakiety nie powinny kończyć się w folderze pakietów globalnych — [#7423](https://github.com/NuGet/Home/issues/7423)

* Generowanie powiązania powiązań nie powinno pomijać zestawów elewacji — [#7393](https://github.com/NuGet/Home/issues/7393)

* VersionRange Equals nie porównują zakresów zmiennoprzecinkowych — [#7324](https://github.com/NuGet/Home/issues/7324)

* Przywracanie: regresja wydajności przy użyciu nowego stosu HTTP programu .NET Core 2,1 — [#7314](https://github.com/NuGet/Home/issues/7314)

* Aktualizacja pakietu nie powinna modyfikować PrivateAssets PackageReference- [#7285](https://github.com/NuGet/Home/issues/7285)

* Podpisywanie: podpisywanie powinno zakończyć się niepowodzeniem, jeśli pakiet ma zbyt wiele wpisów pakietów (>65534) — [#7248](https://github.com/NuGet/Home/issues/7248)

* "wypychanie NuGet" dotnet "prefiksu powinien obsługiwać nowego dostawcę poświadczeń — [#7233](https://github.com/NuGet/Home/issues/7233)

* Obsługa wykonywania wtyczek z niezmienną kulturą (w przypadku platformy Docker) — [#7223](https://github.com/NuGet/Home/issues/7223)

* Dodawanie źródeł NuGet nie powinno usuwać poświadczeń z NuGet.config- [#7200](https://github.com/NuGet/Home/issues/7200)

* Instalowanie devDependency PackageReference powinno domyślnie mieć wartość excludeassets = Kompiluj- [#7084](https://github.com/NuGet/Home/issues/7084)

* Napraw opcję Migrator, która ma być wyświetlana dla wszystkich projektów i Pokaż błąd, jeśli projekt jest niezgodny — [#6958](https://github.com/NuGet/Home/issues/6958)

* "do dodania pakietu dotnet" należy zatwierdzić przywracanie wykonywane do pliku zasobów — [#6928](https://github.com/NuGet/Home/issues/6928)

* Podpisywanie: ulepszanie podpisywania komunikatów o błędach — [#6906](https://github.com/NuGet/Home/issues/6906)

* [Niepowodzenie testu] [zh-TW] Ciąg "Konsola Menedżera pakietów" nie jest zlokalizowany w konsoli Menedżera pakietów — [#6381](https://github.com/NuGet/Home/issues/6381)

* Komunikat o błędzie "nie można znaleźć informacji o projekcie" powinien być nieco bardziej szczegółowy w programie VS- [#5350](https://github.com/NuGet/Home/issues/5350)

* Niepomocny komunikat o błędzie podczas nieprawidłowego używania tagu Version nuspec pakietu NuGet Pack — [#2714](https://github.com/NuGet/Home/issues/2714)

* Podpisywanie DCR: obsługa protokołu NuGet: RepositorySignatures/4.9.0 Resource- [#7421](https://github.com/NuGet/Home/issues/7421)

* Plik DCR-. nupkg. Metadata zostanie teraz utworzony podczas wyodrębniania pakietu — zawiera ciąg "Content-hash"- [#7283](https://github.com/NuGet/Home/issues/7283)

* DCR — Pomiń weryfikację Authenticode dla wtyczek podczas wykonywania na mono- [#7222](https://github.com/NuGet/Home/issues/7222)

[Lista wszystkich problemów rozwiązanych w tej wersji 4.9.0](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a>Podsumowanie: co nowego w programie 4.9.1

* Dodaj obsługę odczytywania zapisu do nuget.config za pośrednictwem nowego polecenia zaufane osoby podpisujące — [#7480](https://github.com/NuGet/Home/issues/7480)

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

* Napraw Generowanie łącza licencji — [#7515](https://github.com/NuGet/Home/issues/7515)

* Regresja kodów błędów dla walidacji sygnatur — [#7492](https://github.com/NuGet/Home/issues/7492)

* Pakiet NuGet. Build. Tasks. Pack nie ma informacji o licencji — [#7379](https://github.com/NuGet/Home/issues/7379)

[Lista wszystkich problemów rozwiązanych w tej wersji 4.9.1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a>Podsumowanie: co nowego w programie 4.9.2

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

* Program VS/dotnet.exe/nuget.exe/msbuild.exe Restore nie używa poświadczeń, gdy nazwa źródła zawiera spację — [#7517](https://github.com/NuGet/Home/issues/7517)

* Problemy z ułatwieniami dostępu LicenseAcceptanceWindow i LicenseFileWindow — [#7452](https://github.com/NuGet/Home/issues/7452)

* Naprawianie FormatException w elemencie DateTime. Przeanalizuj z DateTimeConverter- [#7539](https://github.com/NuGet/Home/issues/7539)

[Lista wszystkich problemów rozwiązanych w tej wersji 4.9.2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a>Podsumowanie: co nowego w programie 4.9.3

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a>"Powtarzające się pakiety są przywracane przy użyciu pliku blokady"

* Tryb zablokowany nie działa, ponieważ wartość skrótu jest obliczana niepoprawnie dla wcześniej buforowanych pakietów — [#7682](https://github.com/NuGet/Home/issues/7682)

* Przywracanie jest rozpoznawane jako inna wersja niż zdefiniowana w `packages.lock.json` [#7667](https://github.com/NuGet/Home/issues/7667) pliku

* Tryb "--locked-Mode/RestoreLockedMode" powoduje błędy przywracania fałszywe, gdy [#7646](https://github.com/NuGet/Home/issues/7646) zawierających

* Program rozpoznawania SDK programu MSBuild próbuje sprawdzić poprawność agenta SHA dla pakietu zestawu SDK, którego przywracanie nie powiodło się podczas korzystania z packages.lock.js[#7599](https://github.com/NuGet/Home/issues/7599)

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a>Problemy "Zablokuj zależności przy użyciu konfigurowalnych zasad zaufania"
* dotnet.exe nie należy szacować nadawców zaufanych, gdy podpisane pakiety nie są obsługiwane — [#7574](https://github.com/NuGet/Home/issues/7574)

* Kolejność trustedSigners w pliku konfiguracji ma wpływ na ocenę zaufania — [#7572](https://github.com/NuGet/Home/issues/7572)

* Nie można zaimplementować ISettings [spowodowane przez refaktoryzację ustawień interfejsów API do obsługi zasad zaufania]- [#7614](https://github.com/NuGet/Home/issues/7614)

#### <a name="improved-debugging-experience-issues"></a>Problemy "Ulepszone środowisko debugowania"

* Nie można opublikować pakietu symboli dla narzędzia globalnego platformy .NET Core — [#7632](https://github.com/NuGet/Home/issues/7632)

#### <a name="self-contained-nuget-packages---license-issues"></a>"Problemy związane z własnymi pakietami NuGet — licencje"

* Wystąpił błąd podczas kompilowania pakietu symboli. snupkg podczas korzystania z pliku licencji osadzonej — [#7591](https://github.com/NuGet/Home/issues/7591)

[Lista wszystkich problemów rozwiązanych w tej wersji 4.9.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")

## <a name="summary-whats-new-in-494"></a>Podsumowanie: co nowego w programie 4.9.4

* Poprawka zabezpieczeń: uprawnienia dla plików utworzonych wewnątrz ~/.NuGet są zbyt otwarte [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)


## <a name="known-issues"></a>Znane problemy

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519"></a>wypychanie NuGet programu dotnet — interaktywny błąd na komputerze Mac. - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>Problem
`--interactive`Argument nie jest przesyłany dalej przez interfejs wiersza polecenia dotnet i powoduje błąd`error: Missing value for option 'interactive'`

#### <a name="workaround"></a>Obejście
Uruchom dowolne inne polecenie dotnet przy użyciu opcji Interactive, takiej jak `dotnet restore --interactive` i uwierzytelniania. Uwierzytelnianie może zostać zapisane w pamięci podręcznej przez dostawcę poświadczeń. Następnie należy uruchomić polecenie `dotnet nuget push`.

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a>Pakiety w FallbackFolders zainstalowane przez zestaw .NET Core SDK są zainstalowane niestandardowo i nie można zweryfikować podpisu. - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>Problem
W przypadku korzystania z dotnet.exe 2. x w celu przywrócenia projektu, który ma wiele obiektów docelowych netcoreapp 1. x i netcoreapp 2. x, folder rezerwowy jest traktowany jako źródło plików. Oznacza to, że podczas przywracania program NuGet wybierze pakiet z folderu rezerwowego i spróbuje go zainstalować w folderze pakiety globalne i wykonać zwykłą weryfikację podpisywania, która kończy się niepowodzeniem.

#### <a name="workaround"></a>Obejście
Wyłącz użycie folderu rezerwowego, ustawiając wartość `RestoreAdditionalProjectSources` Nothing. `<RestoreAdditionalProjectSources/>` Należy to zrobić z ostrożnością, ponieważ spowoduje to pobranie wielu pakietów z NuGet.org, które w przeciwnym razie zostałyby przywrócone z folderu rezerwowego.
