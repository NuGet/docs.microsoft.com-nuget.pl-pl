---
title: Informacje o wersji programu NuGet wersji 4.7 RTM
description: Informacje o wersji programu NuGet 4.7.0 tym — znane problemy, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: 79be74f9c54e27bf2c08e83c7adf81d1f96ce79a
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508166"
---
# <a name="nuget-47-rtm-release-notes"></a>Informacje o wersji programu NuGet wersji 4.7 RTM

[Visual Studio 2017 wersji 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) dołączono [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe).

## <a name="summary-whats-new-in-this-release"></a>Podsumowanie: nowości w tej wersji

* Firma Microsoft ma rozszerzone podpisywania umożliwić pakietu [podpisany repozytorium pakietów](https://github.com/NuGet/Home/wiki/Repository-Signatures)

* Za pomocą programu Visual Studio w wersji 15.7, firma Microsoft wprowadza możliwość [Migrowanie istniejących projektów korzystające z formatu pliku packages.config do użycia funkcji PackageReference](https://docs.microsoft.com/en-us/nuget/reference/migrate-packages-config-to-package-reference) zamiast tego.

## <a name="known-issues"></a>Znane problemy

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>`Migrate packages.config to PackageReference...` Opcja nie jest dostępna w menu kontekstowym kliknij prawym przyciskiem myszy

#### <a name="issue"></a>Problem

Przy pierwszym otwarciu projektu, NuGet może nie mieć zainicjowany, dopóki nie jest wykonywana operacja NuGet. Powoduje to możliwość migracji nie pojawiają się w menu kontekstowym kliknij prawym przyciskiem myszy na `packages.config` lub `References`.

#### <a name="workaround"></a>Obejście

Wykonaj jeden z następujących akcji NuGet:
* Otwórz interfejs użytkownika Menedżera pakietów — kliknij prawym przyciskiem myszy `References` i wybierz pozycję `Manage NuGet Packages...`
* Otwórz konsolę Menedżera pakietów — z `Tools > NuGet Package Manager`, wybierz opcję `Package Manager Console`
* Uruchom Przywracanie pakietów NuGet — kliknij prawym przyciskiem myszy na węzeł rozwiązania w Eksploratorze rozwiązań i wybierz pozycję `Restore NuGet Packages`
* Skompiluj projekt, który wyzwala również Przywracanie pakietów NuGet

Teraz można wyświetlić opcji migracji. Należy zauważyć, że ta opcja nie jest obsługiwane i nie będzie widoczna dla typów projektów platformy ASP.NET i C++.

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemy z platformą .NET Standard 2.0 przy użyciu platformy .NET Framework i NuGet

.NET standard i jego narzędzia zaprojektowano w taki sposób, że projekty przeznaczone dla platformy .NET Framework 4.6.1 może zużywać pakietów NuGet i projekty przeznaczone dla .NET Standard 2.0 lub wcześniejszej. [W tym dokumencie](https://github.com/dotnet/standard/issues/481) znajduje się podsumowanie problemy dotyczące tego scenariusza, planowanie adresowania, a rozwiązania można wdrożyć ze stanem współczesnych narzędzi.

## <a name="top-issues-fixed-in-this-release"></a>Najważniejsze problemy rozwiązane w tej wersji

### <a name="bugs"></a>Usterki

* NuGet jest uruchamiany w zakleszczenie w.Net Core system projektu (Regresja nowe). - [#6733](https://github.com/NuGet/Home/issues/6733)
* Pakiet: PackagePath są konstruowane niepoprawnie użycie TfmSpecificPackageFile dzięki określeniu ścieżki symboli wieloznacznych - [#6726](https://github.com/NuGet/Home/issues/6726)
* Pakiet: projekt interfejsu api sieci web nie można utworzyć pakietu, chyba że jawnie ustawione ispackable. - [#6156](https://github.com/NuGet/Home/issues/6156)
* Interfejs użytkownika programu VS i PMC potrwać 30 minut, aby wyświetlić nowy pakiet (nuget.exe widzi ona następnie od razu) - [#6657](https://github.com/NuGet/Home/issues/6657)
* Podpisywanie: SignatureUtility.GetCertificateChain(...) nie sprawdza wszystkie stany łańcucha - [#6565](https://github.com/NuGet/Home/issues/6565)
* Podpisywanie: poprawy obsługi DER GeneralizedTime - [#6564](https://github.com/NuGet/Home/issues/6564)
* Podpisywania: VS nie jest wyświetlany błąd NU3002 podczas instalowania pakietu zmodyfikowany - [#6337](https://github.com/NuGet/Home/issues/6337)
* lockFile.GetLibrary jest rozróżniana wielkość liter — [#6500](https://github.com/NuGet/Home/issues/6500)
* Kod przywracania instalacji/aktualizacji i ścieżek kodu przywracania nie są spójne - [#3471](https://github.com/NuGet/Home/issues/3471)
* ComboBox wersji PackageManager rozwiązania można wybrać separatora za pośrednictwem klawiatury - [#2606](https://github.com/NuGet/Home/issues/2606)
* Nie można załadować indeks usług dla źródła `https://www.myget.org/F/<id>` ---> System.Net.Http.HttpRequestException: kod stanu odpowiedzi nie wskazuje Powodzenie: 403 (zabronione) - [#2530](https://github.com/NuGet/Home/issues/2530)

### <a name="dcrs"></a>DCRs

* Nagłówek emitowanie X-NuGet-sesji-Id, aby korelowanie żądań [funkcja propozycji] - [#5330](https://github.com/NuGet/Home/issues/5330)
* Udostępnianego sposobu czekać na uruchamianie operacji przywracania, uruchomiony w programie Visual Studio za pośrednictwem interfejsów API wektory. - [#6029](https://github.com/NuGet/Home/issues/6029)
* NuGet.exe - NoServiceEndpoint zapobiegnie dołączanie adres url usługi sufiksu - [#6586](https://github.com/NuGet/Home/issues/6586)
* Dodaj skrót zatwierdzenia do wersji - [#6492](https://github.com/NuGet/Home/issues/6492)
* Podpisywanie: Włącz usuwanie repozytorium podpisu/kontrasygnaturze - [#6646](https://github.com/NuGet/Home/issues/6646)
* Podpisywanie: Interfejs API na potrzeby obcięcie repozytorium podpisu/kontrasygnaturze- [#6589](https://github.com/NuGet/Home/issues/6589)
* Zaloguj się w programie VS — informacje o źródle [#6527](https://github.com/NuGet/Home/issues/6527)
* Filtruj /tools tylko TFM i identyfikatorów RID, dzięki czemu kod XML ustawień, które można umieścić w folderze /tools - [#6197](https://github.com/NuGet/Home/issues/6197)
* Ostrzegaj, gdy polecenie Pakiet wyklucza pliku, który rozpoczyna się od.  - [#3308](https://github.com/NuGet/Home/issues/3308)

[Lista wszystkie problemy rozwiązane w tej wersji](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
