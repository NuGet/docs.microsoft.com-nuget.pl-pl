---
title: Informacje o wersji narzędzia NuGet 4,7 RTM
description: Informacje o wersji programu NuGet 4.7.0, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: 0c3c0380fe6efb3c58124ca5ba8bc1306a433340
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611350"
---
# <a name="nuget-47-release-notes"></a>Informacje o wersji narzędzia NuGet 4,7

[Program Visual Studio 2017 15,7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z pakietem [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe).

## <a name="summary-whats-new-in-470"></a>Podsumowanie: co nowego w programie 4.7.0

* W celu włączenia [podpisanych pakietów repozytorium](https://github.com/NuGet/Home/wiki/Repository-Signatures) zostanie rozszerzony podpis pakietu

* W programie Visual Studio w wersji 15,7 wprowadzono możliwość [migrowania istniejących projektów, które używają formatu Packages. config do używania PackageReference](https://docs.microsoft.com/nuget/consume-packages/migrate-packages-config-to-package-reference) zamiast tego.

## <a name="summary-whats-new-in-472"></a>Podsumowanie: co nowego w programie 4.7.2

* Poprawka zabezpieczeń: uprawnienia dla plików utworzonych wewnątrz ~/.NuGet są zbyt otwarte [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-473"></a>Podsumowanie: co nowego w programie 4.7.3

* Poprawka zabezpieczeń: pliki wewnątrz elementu NUPKGs mogą mieć ścieżkę względną powyżej katalogu NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Znane problemy

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

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemy z .NET Standard 2,0 z pakietem NuGet .NET Framework &

.NET Standard & narzędzia zostały zaprojektowane tak, aby projekty ukierunkowane na .NET Framework 4.6.1 mogły korzystać z pakietów NuGet & projekty przeznaczone do .NET Standard 2,0 lub wcześniejszych. [Ten dokument](https://github.com/dotnet/standard/issues/481) zawiera podsumowanie problemów związanych z tym scenariuszem, planu ich rozwiązywania oraz obejścia, które można wdrożyć przy użyciu dzisiejszego stanu narzędzi.

## <a name="top-issues-fixed-in-this-release"></a>Najczęstsze problemy rozwiązane w tej wersji

### <a name="bugs"></a>Usterki

* Pakiet NuGet przebiega w ramach systemu projektu .Net Core (Nowa regresja). - [#6733](https://github.com/NuGet/Home/issues/6733)
* Pakiet: PackagePath jest nieprawidłowo skonstruowany, jeśli TfmSpecificPackageFile jest używany z ścieżkami obsługi symboli wieloznacznych- [#6726](https://github.com/NuGet/Home/issues/6726)
* Pakiet: projekt interfejsu API sieci Web nie może utworzyć pakietu, chyba że jest on jawnie ustawiony. - [#6156](https://github.com/NuGet/Home/issues/6156)
* Interfejs użytkownika VS i PMC Weź fragmentach, aby zobaczyć nowy pakiet (NuGet. exe widzi go od razu) — [#6657](https://github.com/NuGet/Home/issues/6657)
* Podpisywanie: SignatureUtility. GetCertificateChain (...) nie sprawdza wszystkich stanów łańcucha — [#6565](https://github.com/NuGet/Home/issues/6565)
* Podpisywanie: ulepszanie obsługi algorytmu DER GeneralizedTime — [#6564](https://github.com/NuGet/Home/issues/6564)
* Podpisywanie: VS nie wyświetla błędu NU3002 podczas instalowania pakietu z naruszonymi zabezpieczeniami [#6337](https://github.com/NuGet/Home/issues/6337)
* lockFile. getlibrary uwzględnia wielkość liter — [#6500](https://github.com/NuGet/Home/issues/6500)
* Ścieżki przywracania i przywracania kodu nie są spójne — [#3471](https://github.com/NuGet/Home/issues/3471)
* Pole kombi wersji pakietu Packagemanager umożliwia wybranie separatora za pomocą klawiatury [#2606](https://github.com/NuGet/Home/issues/2606)
* Nie można załadować indeksu usługi dla źródła `https://www.myget.org/F/<id>`---> System .NET. http. HttpRequestexception: kod stanu odpowiedzi nie wskazuje sukcesu: 403 (zabronione) — [#2530](https://github.com/NuGet/Home/issues/2530)

### <a name="dcrs"></a>DCR

* Emituj nagłówek X-NuGet-Session-ID do skorelowania między żądaniami [propozycja funkcji]- [#5330](https://github.com/NuGet/Home/issues/5330)
* Uwidocznij sposób oczekiwania na uruchomienie operacji przywracania uruchomionej w programie Visual Studio za pośrednictwem interfejsów API użycie japońskich ideograficznych. - [#6029](https://github.com/NuGet/Home/issues/6029)
* NuGet. exe-noserviceendpoint zapobiega dołączeniu sufiksu adresu URL usługi [#6586](https://github.com/NuGet/Home/issues/6586)
* Dodaj skrót zatwierdzenia do wersji informacyjnej — [#6492](https://github.com/NuGet/Home/issues/6492)
* Podpisywanie: Włączanie usuwania sygnatury repozytorium/kontrpodpis — [#6646](https://github.com/NuGet/Home/issues/6646)
* Podpisywanie: interfejs API służący do oddzielania sygnatury/kontrpodpis — [#6589](https://github.com/NuGet/Home/issues/6589)
* Informacje o źródle dziennika w programie VS- [#6527](https://github.com/NuGet/Home/issues/6527)
* Filtruj/Tools tylko na TFM i RID, więc XML Settings można umieścić w folderze/Tools- [#6197](https://github.com/NuGet/Home/issues/6197)
* Ostrzegaj, gdy polecenie Pack wyklucza plik, który rozpoczyna się od.  - [#3308](https://github.com/NuGet/Home/issues/3308)

[Lista wszystkich problemów rozwiązanych w tej wersji](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
