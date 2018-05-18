---
title: Informacje o wersji RTM 4,7 NuGet
description: Informacje o wersji programu NuGet 4.7.0 tym — znane problemy, poprawki, dodatkowe funkcje i dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: f23cc2973fa6370d9b7513d415fd8151b822c104
ms.sourcegitcommit: 8f0bb8bb9cb91d27d660963ed9b0f32642f420fe
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/17/2018
---
# <a name="nuget-47-rtm-release-notes"></a>Informacje o wersji RTM 4,7 NuGet

[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe).

## <a name="summary-whats-new-in-this-release"></a>Podsumowanie: nowości w tej wersji

* Mamy podpisywania włączyć pakietu augemented [podpisany repozytorium pakietów](https://github.com/NuGet/Home/wiki/Repository-Signatures)

* Z 15.7 wersji programu Visual Studio, wprowadzono ma możliwość [migracji istniejących projektów, które używają formatu pliku packages.config, aby używać PackageReference](https://docs.microsoft.com/en-us/nuget/reference/migrate-packages-config-to-package-reference) zamiast tego.

## <a name="known-issues"></a>Znane problemy

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>`Migrate packages.config to PackageReference...` Opcja nie jest dostępne w menu kontekstowym kliknij prawym przyciskiem myszy

#### <a name="issue"></a>Problem

Przy pierwszym otwarciu projektu, NuGet może nie mieć zainicjować aż operacja NuGet jest wykonywana. Powoduje to możliwość migracji nie pojawiają się w menu kontekstowym kliknij prawym przyciskiem myszy na `packages.config` lub `References`.

#### <a name="workaround"></a>Obejście

Wykonać jedną z następujących akcji NuGet:
* Otwórz Menedżera pakietów interfejsu użytkownika — kliknij prawym przyciskiem myszy `References` i wybierz pozycję `Manage NuGet Packages...`
* Otwórz konsolę Menedżera pakietów — z `Tools > NuGet Package Manager`, wybierz pozycję `Package Manager Console`
* Uruchom NuGet Przywracanie — kliknij prawym przyciskiem myszy w węźle rozwiązania w Eksploratorze rozwiązań i wybierz `Restore NuGet Packages`
* Skompiluj projekt, który wyzwala również Przywracanie NuGet

Teraz można wyświetlić opcji migracji. Należy pamiętać, że ta opcja nie jest obsługiwane i nie będą widoczne dla typów projektów programu ASP.NET i C++.

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemy z platformą .NET 2.0 standardowe z .NET Framework & NuGet

.NET standard i jej narzędzi została zaprojektowana w taki sposób, że w projektach przeznaczonych dla platformy .NET Framework 4.6.1 może używać pakietów NuGet & projektach przeznaczonych dla platformy .NET Standard 2.0 lub starszym. [Ten dokument](https://github.com/dotnet/standard/issues/481) zawiera podsumowanie problemy dotyczące tego scenariusza, plan adresowania, a rozwiązania można wdrożyć ze stanem współczesnych narzędzi.

## <a name="top-issues-fixed-in-this-release"></a>Najważniejsze problemy rozwiązane w tej wersji

### <a name="bugs"></a>Usterki

* NuGet systemem do zakleszczenia w .net Core projektu (Regresja nowy). - [#6733](https://github.com/NuGet/Home/issues/6733)
* Pakiet: PackagePath jest tworzony nieprawidłowe użycie TfmSpecificPackageFile ze ścieżkami globbing - [#6726](https://github.com/NuGet/Home/issues/6726)
* Pakiet: projekt interfejsu api sieci web nie można utworzyć pakietu, chyba że ispackable jest jawnie ustawiona. - [#6156](https://github.com/NuGet/Home/issues/6156)
* Interfejs użytkownika programu VS i PMC potrwać 30min, aby wyświetlić nowy pakiet (nuget.exe widzi ona od razu) - [#6657](https://github.com/NuGet/Home/issues/6657)
* Podpisywanie: SignatureUtility.GetCertificateChain(...) nie sprawdza wszystkie stany łańcucha - [#6565](https://github.com/NuGet/Home/issues/6565)
* Podpisywanie: poprawy obsługi DER GeneralizedTime - [#6564](https://github.com/NuGet/Home/issues/6564)
* Podpisywanie: VS nie pokazuje błąd NU3002 podczas instalowania pakietu zmodyfikowany - [#6337](https://github.com/NuGet/Home/issues/6337)
* lockFile.GetLibrary uwzględniana jest wielkość liter - [#6500](https://github.com/NuGet/Home/issues/6500)
* Instalacja/aktualizacja przywracania kodu i ścieżek kodu przywracania nie są spójne - [#3471](https://github.com/NuGet/Home/issues/3471)
* Rozwiązanie PackageManager wersji ComboBox można wybrać separator za pomocą klawiatury - [#2606](https://github.com/NuGet/Home/issues/2606)
* Nie można załadować indeks usługi źródła `https://www.myget.org/F/<id>` ---> System.Net.Http.HttpRequestException: kod stanu odpowiedzi nie wskazuje powodzenia: 403 (Dostęp zabroniony) - [#2530](https://github.com/NuGet/Home/issues/2530)

### <a name="dcrs"></a>Dcr

* Nagłówek emitowanie X-NuGet-Session-Id do skorelowania żądań [funkcja propozycji] - [#5330](https://github.com/NuGet/Home/issues/5330)
* Udostępniać metodę oczekiwania na uruchamianie operacji przywracania uruchomiony w programie Visual Studio za pośrednictwem interfejsów API wektory inicjacji. - [#6029](https://github.com/NuGet/Home/issues/6029)
* NuGet.exe - NoServiceEndpoint zapobiegnie dołączanie adres url usługi sufiks - [#6586](https://github.com/NuGet/Home/issues/6586)
* Dodaj skrót zatwierdzenia do wersji informacyjną - [#6492](https://github.com/NuGet/Home/issues/6492)
* Podpisywanie: Włącz usuwanie podpisu repozytorium/kontrasygnatę - [#6646](https://github.com/NuGet/Home/issues/6646)
* Podpisywanie: Interfejs API dla Usuwanie repozytorium podpisu/kontrasygnatę- [#6589](https://github.com/NuGet/Home/issues/6589)
* Rejestrowanie źródła informacji w programie VS - [#6527](https://github.com/NuGet/Home/issues/6527)
* Filtruj /tools tylko TFM i identyfikatorów RID, więc ustawienia XML można umieścić w folderze /tools - [#6197](https://github.com/NuGet/Home/issues/6197)
* Ostrzegaj, gdy polecenie Pakiet wyklucza pliku, który rozpoczyna się od.  - [#3308](https://github.com/NuGet/Home/issues/3308)

[Lista wszystkich problemów rozwiązanych w tej wersji](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
