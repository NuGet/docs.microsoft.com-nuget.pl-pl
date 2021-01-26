---
title: Informacje o wersji narzędzia NuGet 5,2 RTM
description: Informacje o wersji programu NuGet 5,2, w tym nowe funkcje, poprawki błędów i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: 25fa1d09046a583fb987b9f3dd51a0099f4331a7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776205"
---
# <a name="nuget-52-release-notes"></a>Informacje o wersji narzędzia NuGet 5,2

Pojazdy dystrybucji NuGet:

| Wersja programu NuGet | Dostępne w wersji programu Visual Studio| Dostępne w zestawach SDK platformy .NET|
|:---|:---|:---|
| [**5.2.0**](https://nuget.org/downloads) | [Visual Studio 2019 w wersji 16,2](https://visualstudio.microsoft.com/downloads/) | [2.1.80 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Zainstalowane z programem Visual Studio 2019 przy użyciu obciążenia .NET Core 

<sup>2</sup> Dostępne jako opcjonalna instalacja z programem Visual Studio 2019 przy użyciu obciążenia .NET Core

## <a name="summary-whats-new-in-52"></a>Podsumowanie: co nowego w 5,2

* Rozwiązano błąd krytyczny, który spowodował sporadyczne niepowodzenia operacji NuGet ze względu na problemy z ścieżką w systemie Linux & Mac — [#7341](https://github.com/NuGet/Home/issues/7341)

* Ulepszona czas odpowiedzi interfejsu użytkownika podczas przeglądania pakietów przy użyciu interfejsu użytkownika Menedżera pakietów NuGet w programie Visual Studio, szczególnie zauważalne w przypadku wolnych źródeł — [#8039](https://github.com/NuGet/Home/issues/8039)

* Tony poprawek niezawodności dla pliku blokady ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114)[#7840](https://github.com/NuGet/Home/issues/7840)) i wtyczki uwierzytelniania ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198), #7845)[](https://github.com/NuGet/Home/issues/7845)

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

**Usterek**

* Wydajność: Konsola Menedżera pakietów: zaznaczono wartość pola kombi "Projekt domyślny" z opóźnieniem interfejsu użytkownika — [#8235](https://github.com/NuGet/Home/issues/8235)

* Wydajność: ulepszenia wydajności w interfejsie użytkownika PM — [#8039](https://github.com/NuGet/Home/issues/8039)

* Wydajność: opóźnienie interfejsu użytkownika podczas odczytywania domyślnego projektu w kryterium PMC- [#6824](https://github.com/NuGet/Home/issues/6824)

* Wydajność: [vsfeedback] karta aktualizacji NuGet zawiesza się dla lokalnego źródła pakietów — [#6470](https://github.com/NuGet/Home/issues/6470)

* Wtyczki: pakiet NuGet czeka na pełny limit czasu, jeśli wtyczka nie zostanie uruchomiona lub zakończy się wcześnie [#8300](https://github.com/NuGet/Home/issues/8300)

* Wtyczki: zwiększanie diagnozy niepowodzenia uruchamiania wtyczki — [#8271](https://github.com/NuGet/Home/issues/8271)

* Wtyczki: problem z nuget.exe odnajdywania wbudowanych wtyczek — [#8269](https://github.com/NuGet/Home/issues/8269)

* Wtyczki: plik pamięci podręcznej nigdy nie jest odczytywany [#8210](https://github.com/NuGet/Home/issues/8210)

* Wtyczki: "zadanie zostało anulowane." błędy przy użyciu wtyczki uwierzytelniania podczas przywracania [#8198](https://github.com/NuGet/Home/issues/8198)

* Buforowanie wtyczek nie jest sporadycznie wykrywalne na platformach z systemem Linux — [#7845](https://github.com/NuGet/Home/issues/7845)

* LockFile: z ATF, ma wartość false NU1004 z powodu nieprawidłowej kontroli równości platformy docelowej, [#8187](https://github.com/NuGet/Home/issues/8187)

* LockFile: Flaga przywracania "--locked-Mode" nie jest przestrzegana, jeśli plik blokady jest pusty lub źle sformułowany — [#8160](https://github.com/NuGet/Home/issues/8160)

* LockFile: nie małe projekty z niestandardowymi nazwami zestawów w pliku blokady pakietu — [#8114](https://github.com/NuGet/Home/issues/8114)

* LockFile: Zmień wielkość liter w odwołaniu do projektu w pliku blokady — [#7840](https://github.com/NuGet/Home/issues/7840)

* Przywracanie: Instalowanie podpisanego pakietu z naruszonymi wynikami w wielu nieudanych próbach instalacji (z powtórzonym wyjściem) — [#8175](https://github.com/NuGet/Home/issues/8175)

* VS: nie można deserializować opcji użytkownika rozwiązania po aktualizacji NuGet- [#8166](https://github.com/NuGet/Home/issues/8166)

* Pakiet dotnet-list-Package w projekcie testu jednostkowego zwraca błąd- [#8154](https://github.com/NuGet/Home/issues/8154)

* Utwórz grupę pakietów NuGet dla Instalatora programu VS — naprawianie niektórych problemów z instalacją VSIX — [#8033](https://github.com/NuGet/Home/issues/8033)

* GeneratePackageOnBuild nie powinna być ustawiona nobuild. - [#7801](https://github.com/NuGet/Home/issues/7801)

* Nowa opcja "-SymbolPackageFormat snupkg" generuje błąd, gdy plik. nuspec zawiera jawny element odwołania do zestawu — [#7638](https://github.com/NuGet/Home/issues/7638)

* NuGet. targets (498, 5): błąd: nie można odnaleźć części ścieżki "/tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341)

**DCR**

* Dodaj właściwość programu MSBuild, która wskazuje, że PackageDownload jest obsługiwana — [#8106](https://github.com/NuGet/Home/issues/8106)

* FrameworkReference Pomijaj przepływ zależności za pośrednictwem FrameworkReference. PrivateAssets- [#7988](https://github.com/NuGet/Home/issues/7988)

* Mechanizm dostarczania runtime.jsna zewnątrz pakietu [#7351](https://github.com/NuGet/Home/issues/7351)

**[Lista wszystkich problemów rozwiązanych w tym wydaniu — 5,2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**


