---
title: Informacje o wydaniu programu NuGet 4.7 RTM
description: Informacje o wersji dla NuGet 4.7.0, w tym znane problemy, poprawki błędów, dodane funkcje i BDR.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: 2290025d42dcd5704b6b019c17346201fe6a990d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "76813796"
---
# <a name="nuget-47-release-notes"></a>Informacje o wersji nuget 4.7

[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe).

## <a name="summary-whats-new-in-470"></a>Krótki opis: Co nowego w 4.7.0

* Powiększyliśmy podpisywanie pakietów, aby włączyć [pakiety podpisane repozytorium](https://github.com/NuGet/Home/wiki/Repository-Signatures)

* W programie Visual Studio w wersji 15.7 wprowadziliśmy możliwość [migracji istniejących projektów, które używają formatu packages.config do używania packageReference](../consume-packages/migrate-packages-config-to-package-reference.md) zamiast tego.

## <a name="summary-whats-new-in-472"></a>Krótki opis: Co nowego w 4.7.2

* Poprawka zabezpieczeń: Uprawnienia do plików utworzonych wewnątrz ~/.nuget są zbyt otwarte [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-473"></a>Krótki opis: Co nowego w 4.7.3

* Poprawka zabezpieczeń: Pliki wewnątrz nupkgs może mieć względną ścieżkę powyżej katalogu NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Znane problemy

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

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemy z .NET Standard 2.0 z .NET Framework & NuGet

.NET Standard & jego narzędzia został zaprojektowany w taki sposób, że projekty przeznaczone dla platformy .NET Framework 4.6.1 mogą korzystać z pakietów NuGet & projektów przeznaczonych dla .NET Standard 2.0 lub wcześniejszych. [W tym dokumencie](https://github.com/dotnet/standard/issues/481) podsumowano problemy związane z tym scenariuszem, plan ich rozwiązania i obejścia, które można wdrożyć przy dzisiejszym stanie narzędzia.

## <a name="top-issues-fixed-in-this-release"></a>Najważniejsze problemy rozwiązane w tej wersji

### <a name="bugs"></a>Usterki

* NuGet wpada w zakleszczenie w systemie projektu .Net Core (nowa regresja). - [#6733](https://github.com/NuGet/Home/issues/6733)
* Pack: PackagePath jest skonstruowany niepoprawnie, jeśli TfmSpecificPackageFile jest używany ze ścieżkami globbing - [#6726](https://github.com/NuGet/Home/issues/6726)
* Pakiet: projekt interfejsu api sieci web nie może utworzyć pakietu, chyba że jest onpakowany jawnie. - [#6156](https://github.com/NuGet/Home/issues/6156)
* VS UI i PMC wziąć 30min, aby zobaczyć nowy pakiet (nuget.exe widzi go od razu) - [#6657](https://github.com/NuGet/Home/issues/6657)
* Podpisanie: SignatureUtility.GetCertificateChain(...) nie sprawdza wszystkich statusów łańcucha - [#6565](https://github.com/NuGet/Home/issues/6565)
* Podpisanie: poprawa obsługi DER GeneralizedTime - [#6564](https://github.com/NuGet/Home/issues/6564)
* Podpisywanie: VS nie pokazuje błędu NU3002 podczas instalowania zmodyfikowanego pakietu - [#6337](https://github.com/NuGet/Home/issues/6337)
* lockFile.GetLibrary jest rozróżniana wielkość liter - [#6500](https://github.com/NuGet/Home/issues/6500)
* Zainstaluj/aktualizuj kod przywracania i przywróć ścieżki kodu nie są spójne - [#3471](https://github.com/NuGet/Home/issues/3471)
* Rozwiązanie PackageManager Version ComboBox można wybrać separator za pomocą klawiatury - [#2606](https://github.com/NuGet/Home/issues/2606)
* Nie można załadować indeksu usługi dla źródła `https://www.myget.org/F/<id>` ---> System.Net.http.http.httpRequestException: Kod stanu odpowiedzi nie wskazuje sukcesu: 403 (Zabronione) - [#2530](https://github.com/NuGet/Home/issues/2530)

### <a name="dcrs"></a>DDR

* Emituj nagłówek X-NuGet-Session-Id, aby skorelować żądania [propozycja funkcji] — [#5330](https://github.com/NuGet/Home/issues/5330)
* Uwidacznia sposób oczekiwania na uruchomienie operacji przywracania uruchomiony w programie Visual Studio za pośrednictwem iVs apis. - [#6029](https://github.com/NuGet/Home/issues/6029)
* NuGet.exe -NoServiceEndpoint pozwoli uniknąć dołączania sufiksu adresu URL usługi — [#6586](https://github.com/NuGet/Home/issues/6586)
* dodawanie skrótu zatwierdzania do wersji informacyjnej - [#6492](https://github.com/NuGet/Home/issues/6492)
* Podpisywanie: umożliwia usunięcie podpisu/kontrasygnaty repozytorium - [#6646](https://github.com/NuGet/Home/issues/6646)
* Podpisywanie: INTERFEJS API do usuwania podpisu/kontrasygnatury repozytorium - [#6589](https://github.com/NuGet/Home/issues/6589)
* Rejestrowanie informacji źródłowych w programie VS — [#6527](https://github.com/NuGet/Home/issues/6527)
* Filtruj /narzędzia tylko na TFM i RID, więc ustawienia XML można umieścić w folderze /tools - [#6197](https://github.com/NuGet/Home/issues/6197)
* Ostrzegaj, gdy polecenie Pack wyklucza plik rozpoczynający się od pliku .  - [#3308](https://github.com/NuGet/Home/issues/3308)

[Lista wszystkich problemów rozwiązanych w tej wersji](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
