---
title: Informacje o wersji nuGet 5.7
description: Informacje o wersji dla programu NuGet 5.7, w tym nowe funkcje, poprawki błędów i dcr.
author: chgill-msft
ms.author: chgill
ms.date: 8/14/2020
ms.topic: conceptual
ms.openlocfilehash: 58ab481f0c6a6cb5549c269788170b8c3ff6002f
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508790"
---
# <a name="nuget-57-release-notes"></a>Informacje o wersji nuGet 5.7

Pojazdy dystrybucji NuGet:

| Wersja pakietu NuGet | Dostępne w Visual Studio wersji | Dostępne w zestawach SDK platformy .NET |
|:---|:---|:---|
| [**5.7.0**](https://nuget.org/downloads) | [Visual Studio 2019 w wersji 16.7](https://visualstudio.microsoft.com/downloads/) | [3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |
| [**5.7.1**](https://nuget.org/downloads) | [Visual Studio 2019 w wersji 16.7](https://visualstudio.microsoft.com/downloads/) | [3.1.408](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1 Zainstalowano</sup> z programem Visual Studio 2019 z obciążeniem .NET Core

## <a name="summary-whats-new-in-57"></a>Podsumowanie: Co nowego w 5.7

### <a name="features-added-in-this-release"></a>Funkcje dodane w tej wersji

* Dodano obsługę zewnętrznego aliasu dla odwołań do pakietów NuGet [— #4989](https://github.com/NuGet/Home/issues/4989)

* Przyspieszyliśmy przełączanie między kartami Zainstalowane i Aktualizacje, umożliwiając im udostępnianie źródła [](https://github.com/NuGet/Home/issues/8294) danych i zmniejszając ponowne #8294

* Szybsze przywracanie — przyspieszanie ocen przez wywołanie interfejsów API programu MSBuild Static Graph (dotnet.exe) — [#9644](https://github.com/NuGet/Home/issues/9644)

* Dodano Visual Studio częściowe przywracanie dla projektów PackageReference (no-op++) — [#9513](https://github.com/NuGet/Home/issues/9513)

* Visual Studio Menedżer pakietów użytkownika będzie rzadziej ulegać awarii podczas wyszukiwania nieprawidłowo zachowujących się źródeł pakietów, które zwracają więcej wyników niż żądana liczba wyników na żądanie HTTP. - [#8478](https://github.com/NuGet/Home/issues/8478)

* Dodano integrację informacji PackageVersion dla projektów w stylu innych niż zestaw SDK w przywracaniu programu VS — [#9236](https://github.com/NuGet/Home/issues/9236)

* Dodano obsługę nuget.exe aktualizacji `-self -Source` https://feed  -  [#1783](https://github.com/NuGet/Home/issues/1783)

* Dodano obsługę wielu plików konfiguracji w katalogu %APPDATA%\NuGet — [#9394](https://github.com/NuGet/Home/issues/9394)

* Ścieżka DeterministicSourcePaths uwzględnia teraz pakiety źródłowe NuGet [—](https://github.com/NuGet/Home/issues/9431) #9431

* Dodano interfejs API rozszerzalności INuGetProjectService.GetInstalledPackagesAsync — [#9702](https://github.com/NuGet/Home/issues/9702)

* Dodano interfejs API międzyoptyku do wyliczania folderów rezerwowych bez konieczności użycia [rozwiązania/projektu — #9395](https://github.com/NuGet/Home/issues/9395)

* Dodano `latest` opcję `-MSBuildVersion`  -  [dla #8808](https://github.com/NuGet/Home/issues/8808)

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

**Błędy:**

* Podczas przywracania interfejsu wiersza polecenia dotnet podczas uruchamiania wtyczek poświadczeń wypróbuj interfejs wiersza polecenia dotnet w ścieżce systemowej, jeśli zmienna `DOTNET_HOST_PATH`  środowiskowa nie jest zdefiniowana. - [#7438](https://github.com/NuGet/Home/issues/7438)

* nuget.exe generuje tag praw autorskich z zakodowanym tekstem Copyright YYYY Zamiast `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)

* NuGet.exe zgłasza wyjątek "wymagani autorzy" podczas pakowania pliku csproj ignorując symbole zastępcze i atrybuty assemblyinfo, jeśli nazwa zestawu zostanie zmieniona [—](https://github.com/NuGet/Home/issues/4234) #4234

* Funkcja HttpRequestMessage jest ponownie wielokrotnie wielokrotnie, co nie jest obsługiwane w przypadku funkcji SocketHttpHandler [— #8661](https://github.com/NuGet/Home/issues/8661)

* NuGet.Indexing 5.6.0 (wersja zapoznawcza 3) i nowsze używają innego tokenu klucza publicznego [—](https://github.com/NuGet/Home/issues/9481) #9481

* Honoruj wartości TreatWarningsAsErrors podczas tworzenia pakietu NuGet — [#7404](https://github.com/NuGet/Home/issues/7404)

* [CPVM] Spurious package downgrades for multiple p2p projects - [#9549](https://github.com/NuGet/Home/issues/9549)

* Karta "Przeglądaj" nie jest wyrównana do lewej z polem wyszukiwania [— #9559](https://github.com/NuGet/Home/issues/9559)

* Zainstalowana wersja jest niespójna z ikoną osadzoną w interfejsie użytkownika pm poziomu rozwiązania dla jednego identyfikatora pakietu z zainstalowanymi wieloma [wersjami —](https://github.com/NuGet/Home/issues/9321) #9321

* Przeciek: PartCreationPolicy(CreationPolicy.NonShared) NuGet.SolutionRestoreManager.RestoreOperationLogger [— #9595](https://github.com/NuGet/Home/issues/9595)

* Unikaj odczytywania pliku assets w przypadku przywracania bez [#9693](https://github.com/NuGet/Home/issues/9693)

* Protokół NuGet.Protocol nie obsługuje pobierania liczby pobierania wersji z wyszukiwania — [#9086](https://github.com/NuGet/Home/issues/9086)

* Zwiększ wydajność pamięci właściwości PackageMetadataResourceV3, zmniejszając zależności JObject — [#9719](https://github.com/NuGet/Home/issues/9719)

**Projektowanie żądań zmiany:**

* Pominięto `<owners>` element, gdy jest nadmiarowy — [#5134](https://github.com/NuGet/Home/issues/5134)

* Log IntervalTrackers as ETW events - #9593 (Śledzenie interwałów dzienników jako zdarzenia ETW [— #9593](https://github.com/NuGet/Home/issues/9593)

* Dodano komunikat informacyjny na temat przywracania, aby poinformować użytkowników protokołu CPVM, że funkcja jest w wersji zapoznawczej — [#9340](https://github.com/NuGet/Home/issues/9340)

* Wypełnij Eksplorator rozwiązań pakietów/projektów przechodnie z pliku assets — [#9580](https://github.com/NuGet/Home/issues/9580)

* Karta Zainstalowane pakiety nie powinna stronicować listy pakietów [—](https://github.com/NuGet/Home/issues/6995) #6995

**[Lista wszystkich problemów rozwiązanych w tej wersji — 5.7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**

### <a name="community-contributions"></a>Materiały przekazywane przez społeczność

Dziękujemy wszystkim współautorom, którzy pomogli w dosyć świetnym wydaniu nuGet!

|Który|Prs|Problemy|
|----|----|----|
|[campersau](https://github.com/campersau)|[3433,](https://github.com/NuGet/NuGet.Client/pull/3433) [3120](https://github.com/NuGet/NuGet.Client/pull/3120)|Protokół NuGet.Protocol nie obsługuje pobierania liczby pobierania wersji z wyszukiwania — [#9086](https://github.com/NuGet/Home/issues/9086) </br>Funkcja HttpRequestMessage jest ponownie wielokrotnie wielokrotnie, co nie jest obsługiwane w przypadku funkcji SocketHttpHandler [— #8661](https://github.com/NuGet/Home/issues/8661)|
|[Joseph Musser (jnm2)](https://github.com/jnm2)|[3241](https://github.com/NuGet/NuGet.Client/pull/3241)|Pominięto `<owners>` element, gdy jest nadmiarowy — [#5134](https://github.com/NuGet/Home/issues/5134)|
|[Volodymyr Shkolka (BlackGad)](https://github.com/BlackGad)|[3273](https://github.com/NuGet/NuGet.Client/pull/3273)|Nie można przywrócić programu NuGet ze źródeł HTTPS, które wymagają certyfikatów klienta — [#5773](https://github.com/NuGet/Home/issues/5773)|
|[Majan Ungureanu (Therzok)](https://github.com/Therzok)|[3357](https://github.com/NuGet/NuGet.Client/pull/3357)|HttpSourceAuthenticationHandler SemaphoreSlim — przyszłe [weryfikacje — #9463](https://github.com/NuGet/Home/issues/9463)|
|[Sunner (SuNNjek)](https://github.com/SuNNjek)|[3088](https://github.com/NuGet/NuGet.Client/pull/3088)|nuget.exe generuje tag praw autorskich z zakodowanym tekstem Copyright YYYY Zamiast `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)|
|[Olivier Spinelli (olivier-spinelli)](https://github.com/olivier-spinelli)|[3335](https://github.com/NuGet/NuGet.Client/pull/3335)|W przywróceniu interfejsu wiersza polecenia dotnet podczas uruchamiania wtyczek poświadczeń wypróbuj interfejs wiersza polecenia dotnet na ścieżce systemowej, jeśli zmienna `DOTNET_HOST_PATH`  środowiskowa nie jest zdefiniowana. - [#7438](https://github.com/NuGet/Home/issues/7438)|
|[goyzhang](https://github.com/goyzhang)|[3370](https://github.com/NuGet/NuGet.Client/pull/3370)|Dodano `latest` opcję `-MSBuildVersion`  -  [dla #8808](https://github.com/NuGet/Home/issues/8808)|

## <a name="summary-whats-new-in-571"></a>Podsumowanie: co nowego w programie 5.7.1

* Rozszerz plik .nupkg.metadata, aby uwzględnić źródło instalacji [— #10354](https://github.com/NuGet/Home/issues/10354)

* Zawartość pakietu dziennikahash podczas rejestrowania przywracania (podczas wyodrębniania) [— #10384](https://github.com/NuGet/Home/issues/10384)

* Podczas przywracania z normalnym poziomem szczegółowości rejestruj źródło, z którego jest przywracany [pakiet](https://github.com/NuGet/Home/issues/10461) — #10461

**[Lista wszystkich problemów rozwiązanych w tej wersji — 5.7.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f5724f84579cc29a79ee)**

**[Lista zatwierdzeń w tej wersji — 5.7.1](https://github.com/NuGet/NuGet.Client/compare/80512866a2c127e52ce3e86fd803fff77e9b9b52...5.7.1.4)**
