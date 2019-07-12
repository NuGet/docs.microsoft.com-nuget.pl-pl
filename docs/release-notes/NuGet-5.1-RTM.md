---
title: Informacje o wersji 5.1 RTM NuGet
description: Informacje o wersji programu NuGet 5.1 obejmuje nowe funkcje, poprawki błędów i DCRs.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 384145947b19af6577dc1255985df1a361c72bb5
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842582"
---
# <a name="nuget-51-release-notes"></a>Informacje o wersji 5.1 NuGet

NuGet pojazdów dystrybucji:

| NuGet w wersji | Dostępne w wersji programu Visual Studio| Dostępne w zestawów SDK platformy .NET|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019 version 16.1](https://visualstudio.microsoft.com/downloads/) | [2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>instalowane z Visual Studio 2019 r przy użyciu obciążenia platformy .NET Core 

<sup>2</sup>jest dostępna jako opcjonalna instalacja przy użyciu programu Visual Studio 2019 r przy użyciu obciążenia platformy .NET Core

## <a name="summary-whats-new-in-51"></a>Podsumowanie: What's New in 5.1

* Pomocy technicznej, aby pominąć powiadomienie wypychane pakietu, jeśli już istnieje, aby umożliwić lepszą integrację z przepływami pracy ciągłej integracji/ciągłego wdrażania — [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* Program Visual Studio teraz oferuje wygodny link do strony galerii nuget.org pakietu - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* Obsługa nowe zasoby platformy .NET Core 3.0, takie jak [pakietów przeznaczonych dla](https://github.com/dotnet/cli/issues/10006) i [pakiety środowiska uruchomieniowego](https://github.com/dotnet/cli/issues/10007)
  * Pakiet NuGet i przywracanie Obsługa FrameworkReferences umożliwia określanie wartości docelowej i środowisko uruchomieniowe odwołania do pakietu - [#7342](https://github.com/NuGet/Home/issues/7342)
  * Obsługa "Pobierz tylko" pakiet scenariusz PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)
  * Środowisko uruchomieniowe Exlcude i kierowania pakietów z wyników wyszukiwania i ich przywracanie grafu przy użyciu PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

**Błędy**

* Wtyczki: Szczegóły wyjątku utracone podczas tworzenia wtyczki - [#8057](https://github.com/NuGet/Home/issues/8057)

* Zakres PackageReference się wyłączności dolna granica nie działa, jeśli dolna granica jest obecny w jedno ze źródeł. - [#8054](https://github.com/NuGet/Home/issues/8054)

* Poprawić komunikatu IsPackableFalseError — [#8021](https://github.com/NuGet/Home/issues/8021)

* Pakiety blokady pliku — ponowne generowanie blokady po zmianie projektów programu graph — [#8019](https://github.com/NuGet/Home/issues/8019)

* Współdzielone usterka: Pakiety Nuget wprowadzenie automatycznie usunięte - [#8017](https://github.com/NuGet/Home/issues/8017)

* Dodanie elementu docelowego w celu zwrócenia FrameworkReference przypominające CollectPackageDownloads i CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)

* Pamięć podręczna HTTP:  RepositoryResources zasobu nie jest buforowana w sposób wersjonowany - [#7997](https://github.com/NuGet/Home/issues/7997)

* Rejestrowanie: stosy wywołań wyjątków nie są zgłaszane wraz z szczegółowy poziom szczegółowości - [#7955](https://github.com/NuGet/Home/issues/7955)

* Zmień wszystkie adresy URL Docs NuGet do używania protokołu HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)

* Poprawa komunikat ostrzegawczy NU3024 - [#7933](https://github.com/NuGet/Home/issues/7933)

* plik blokady nie aktualizuje, gdy packagereference usunięte - [#7930](https://github.com/NuGet/Home/issues/7930)

* Poprawa obsługi przypadków błędów podczas weryfikowania elementu licenseurl i licencji w nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)

* Kliknij prawym przyciskiem myszy w nagłówku kartę i kliknięcie przycisku "Otwórz lokalizację pliku" powoduje błąd — PM interfejsu użytkownika — [#7913](https://github.com/NuGet/Home/issues/7913)

* Wtyczki: dziennika podczas procesu wtyczki zamyka - [#7907](https://github.com/NuGet/Home/issues/7907)

* Wtyczki: współczynnik kolizji wysokiej rejestrowanie wartości daty/godziny — [#7899](https://github.com/NuGet/Home/issues/7899)

* Manifest.ReadFrom zakończy się niepowodzeniem w dowolnym nuspec z LicenseExpression — [#7894](https://github.com/NuGet/Home/issues/7894)

* RestoreLockedMode: Nieoczekiwany NU1004 elementu ProjectReference odwołuje się do projektu przy użyciu niestandardowych AssemblyName — [#7889](https://github.com/NuGet/Home/issues/7889)

* Udoskonalony komunikat o błędzie podczas uruchamiania wtyczki zakończy się niepowodzeniem z powodu wyjątku - [#7857](https://github.com/NuGet/Home/issues/7857)

* W trakcie przywracania aktualizujący nie działa, należy unikać *. dgspec.json zapisu w katalogu obj — [#7854](https://github.com/NuGet/Home/issues/7854)

* GeneratePathProperty = true kończy się niepowodzeniem, można wygenerować właściwości w przypadku niezgodność - [#7843](https://github.com/NuGet/Home/issues/7843)

* Ustawienia: niedozwolony znak w ścieżce źródła pakietu może ulec awarii VS - [#7820](https://github.com/NuGet/Home/issues/7820)

* Usunięcie pliku blokady przywracania nie generuje pliku blokady na aktualizujący nie działa — [#7807](https://github.com/NuGet/Home/issues/7807)

* Adres URL licencji i licencji powoduje błąd z metadanymi - odczytu [#7547](https://github.com/NuGet/Home/issues/7547)

* Nieobsługiwane wyjątki w V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)

* nuget.exe zwróci kod zakończenia zero w przypadku podania nieprawidłowych argumentów - [#7178](https://github.com/NuGet/Home/issues/7178)

* Zaktualizuj błędy i ostrzeżenia docs, aby odzwierciedlały podpisywania scenariusze pokrewne - [#6498](https://github.com/NuGet/Home/issues/6498)

* Plik zasobów należy użyć ścieżek względnych umożliwiające łatwiejsze — przenoszenie projektów [#4582](https://github.com/NuGet/Home/issues/4582)

**DCRs**

* Wtyczki: Włączanie rejestrowania diagnostycznego - [#7859](https://github.com/NuGet/Home/issues/7859)

* Utwórz Tizen 6 mapę, aby NetStandard 2.1 — [#7773](https://github.com/NuGet/Home/issues/7773)

**[Lista wszystkie problemy rozwiązane w tej wersji — 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
