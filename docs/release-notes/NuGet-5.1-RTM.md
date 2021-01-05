---
title: Informacje o wersji narzędzia NuGet 5,1 RTM
description: Informacje o wersji programu NuGet 5,1, w tym nowe funkcje, poprawki błędów i DCR.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 2a94360dc375ba90b90c1045f4acbcfca81fea5b
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699862"
---
# <a name="nuget-51-release-notes"></a>Informacje o wersji narzędzia NuGet 5,1

Pojazdy dystrybucji NuGet:

| Wersja programu NuGet | Dostępne w wersji programu Visual Studio| Dostępne w zestawach SDK platformy .NET|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019 w wersji 16,1](https://visualstudio.microsoft.com/downloads/) | [2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Zainstalowane z programem Visual Studio 2019 przy użyciu obciążenia .NET Core 

<sup>2</sup> Dostępne jako opcjonalna instalacja z programem Visual Studio 2019 przy użyciu obciążenia .NET Core

## <a name="summary-whats-new-in-51"></a>Podsumowanie: co nowego w 5,1

* Obsługa pominięcia wypychania pakietu, jeśli już istnieje, aby umożliwić lepszą integrację z przepływami pracy ciągłej integracji/ciągłego wdrażania — [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* Program Visual Studio udostępnia teraz wygodny link do strony galerii nuget.org pakietu — [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* Obsługa nowych zasobów platformy .NET Core 3,0, takich jak [pakiety docelowe](https://github.com/dotnet/cli/issues/10006) i [pakiety środowiska uruchomieniowego](https://github.com/dotnet/cli/issues/10007)
  * Pakiet NuGet i obsługa przywracania dla FrameworkReferences w celu włączenia elementów docelowych i odwołań do pakietów środowiska uruchomieniowego — [#7342](https://github.com/NuGet/Home/issues/7342)
  * Obsługa scenariusza pakietu "tylko pobieranie" z PackageDownload- [#7339](https://github.com/NuGet/Home/issues/7339)
  * Wyklucz środowisko uruchomieniowe i pakiety docelowe z wyników wyszukiwania & przywracanie wykresu przy użyciu elementu PackageType — [#7337](https://github.com/NuGet/Home/issues/7337)

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

**Usterek**

* Wtyczki: Szczegóły wyjątku utracone podczas tworzenia wtyczki — [#8057](https://github.com/NuGet/Home/issues/8057)

* Zakres PackageReference z wyłącznym dolnym ograniczeniem nie działa, jeśli Dolna granica jest obecna w jednym ze źródeł. - [#8054](https://github.com/NuGet/Home/issues/8054)

* Ulepszanie komunikatu IsPackableFalseError — [#8021](https://github.com/NuGet/Home/issues/8021)

* Zablokuj plik — Wygeneruj ponownie plik blokady podczas zmiany grafu projektu — [#8019](https://github.com/NuGet/Home/issues/8019)

* Usterka współdzielone: pakiety NuGet do pobrania są usuwane [#8017](https://github.com/NuGet/Home/issues/8017)

* Dodaj obiekt docelowy do zwrócenia FrameworkReference podobnego do CollectPackageDownloads i CollectPackageReferences- [#8005](https://github.com/NuGet/Home/issues/8005)

* Pamięć podręczna HTTP: zasób RepositoryResources nie jest buforowany w sposób [#7997](https://github.com/NuGet/Home/issues/7997)

* Rejestrowanie: wyjątek stosy wywołań nie jest raportowany ze szczegółowym szczegółowośćem — [#7955](https://github.com/NuGet/Home/issues/7955)

* Zmień adresy URL wszystkich dokumentów NuGet, aby używały protokołu HTTPS [#7950](https://github.com/NuGet/Home/issues/7950)

* Ulepsz komunikat ostrzegawczy NU3024 — [#7933](https://github.com/NuGet/Home/issues/7933)

* Zablokuj plik nie jest aktualizowany po usunięciu packagereference — [#7930](https://github.com/NuGet/Home/issues/7930)

* Popraw obsługę wielkości liter podczas sprawdzania poprawności elementu licenseurl i licencji w nuspec- [#7915](https://github.com/NuGet/Home/issues/7915)

* Interfejs użytkownika PM — kliknij prawym przyciskiem myszy nagłówek karty i kliknięcie pozycji "Otwórz lokalizację pliku" spowoduje błąd — [#7913](https://github.com/NuGet/Home/issues/7913)

* Wtyczki: log po zakończeniu procesu wtyczki — [#7907](https://github.com/NuGet/Home/issues/7907)

* Wtyczki: współczynnik dużej kolizji w wartościach DateTime rejestrowania — [#7899](https://github.com/NuGet/Home/issues/7899)

* Manifest. ReadFrom kończy się niepowodzeniem na żadnym nuspec z LicenseExpression- [#7894](https://github.com/NuGet/Home/issues/7894)

* RestoreLockedMode: nieoczekiwany NU1004, gdy elementu ProjectReference odwołuje się do projektu z niestandardowym elementem AssemblyName [#7889](https://github.com/NuGet/Home/issues/7889)

* Lepszy komunikat o błędzie podczas uruchamiania wtyczki kończy się niepowodzeniem z wyjątkiem [#7857](https://github.com/NuGet/Home/issues/7857)

* Podczas wykonywania operacji przywracania aktualizujący nie działa należy unikać * .dgspec.jsprzy zapisie w katalogu obj- [#7854](https://github.com/NuGet/Home/issues/7854)

* GeneratePathProperty = true nie można wygenerować właściwości w przypadku niezgodności przypadków — [#7843](https://github.com/NuGet/Home/issues/7843)

* Ustawienia: niedozwolony znak w ścieżce źródłowej pakietu może ulec awarii i [#7820](https://github.com/NuGet/Home/issues/7820)

* Jeśli plik blokady zostanie usunięty, instrukcja RESTORE nie generuje pliku blokady na aktualizujący nie działa- [#7807](https://github.com/NuGet/Home/issues/7807)

* Adres URL i licencja licencji powodują błąd odczytu w metadanych — [#7547](https://github.com/NuGet/Home/issues/7547)

* Nieobsłużone wyjątki w V2FeedParser — [#7523](https://github.com/NuGet/Home/issues/7523)

* nuget.exe zwraca kod zakończenia zero dla nieprawidłowych argumentów — [#7178](https://github.com/NuGet/Home/issues/7178)

* Aktualizowanie błędów i dokumentów ostrzeżeń w celu odzwierciedlenia scenariuszy związanych z podpisywaniem — [#6498](https://github.com/NuGet/Home/issues/6498)

* Plik zasobów powinien używać ścieżek względnych, aby łatwiej przenosić projekty [#4582](https://github.com/NuGet/Home/issues/4582)

**DCR**

* Wtyczki: Włączanie rejestrowania diagnostycznego — [#7859](https://github.com/NuGet/Home/issues/7859)

* Utwórz mapę Tizen 6 do standardu 2,1- [#7773](https://github.com/NuGet/Home/issues/7773)

**[Lista wszystkich problemów rozwiązanych w tym wydaniu — 5,1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
