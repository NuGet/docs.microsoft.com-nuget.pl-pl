---
title: Informacje o wersji narzędzia NuGet 5,7
description: Informacje o wersji programu NuGet 5,7, w tym nowe funkcje, poprawki błędów i DCR.
author: chgill-msft
ms.author: chgill
ms.date: 8/14/2020
ms.topic: conceptual
ms.openlocfilehash: 6c821091983ab0b5d59b759e1ee9930cf449fd9d
ms.sourcegitcommit: 6cda91f135e58cf57a2471b0c7c4a2f748f40024
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/02/2020
ms.locfileid: "89364169"
---
# <a name="nuget-57-release-notes"></a>Informacje o wersji narzędzia NuGet 5,7

Pojazdy dystrybucji NuGet:

| Wersja programu NuGet | Dostępne w wersji programu Visual Studio | Dostępne w zestawach SDK platformy .NET |
|:---|:---|:---|
| [**5.7.0**](https://nuget.org/downloads) | [Visual Studio 2019 w wersji 16,7](https://visualstudio.microsoft.com/downloads/) | [3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> zainstalowano z programem Visual Studio 2019 przy użyciu obciążenia .NET Core

## <a name="summary-whats-new-in-57"></a>Podsumowanie: co nowego w 5,7

### <a name="features-added-in-this-release"></a>Funkcje dodane w tej wersji

* Dodano obsługę aliasów zewnętrznych dla odwołań do pakietów NuGet — [#4989](https://github.com/NuGet/Home/issues/4989)

* Przełączenie między zainstalowanym i aktualizowaniem kart jest szybsze, umożliwiając im udostępnianie źródła danych i zmniejszenie resfreshing [#8294](https://github.com/NuGet/Home/issues/8294)

* Zwiększ szybkość przywracania przyspieszanie, wywołując statyczne interfejsy API programu MSBuild (dotnet.exe) — [#9644](https://github.com/NuGet/Home/issues/9644)

* Dodano częściowe przywracanie programu Visual Studio dla projektów PackageReference (No-op + +) — [#9513](https://github.com/NuGet/Home/issues/9513)

* Interfejs użytkownika Menedżera pakietów programu Visual Studio będzie rzadziej ulegać awarii podczas wyszukiwania źródeł pakietów błędna, które zwracają więcej niż żądaną liczbę wyników na żądanie HTTP. - [#8478](https://github.com/NuGet/Home/issues/8478)

* Dodano integrację PackageVersion informacji dla projektów typu non-SDK w programie VS Restore- [#9236](https://github.com/NuGet/Home/issues/9236)

* Dodano obsługę nuget.exe aktualizacji `-self -Source` https://feed  -  [#1783](https://github.com/NuGet/Home/issues/1783)

* Dodano obsługę wielu plików konfiguracji w katalogu%APPDATA%\NuGet — [#9394](https://github.com/NuGet/Home/issues/9394)

* DeterministicSourcePaths teraz pobiera pakiety źródłowe NuGet do konta [#9431](https://github.com/NuGet/Home/issues/9431)

* Dodano interfejs API rozszerzalności INuGetProjectService. GetInstalledPackagesAsync — [#9702](https://github.com/NuGet/Home/issues/9702)

* Dodano interfejs API międzyoperacyjności do wyliczania folderów rezerwowych bez konieczności [#9395](https://github.com/NuGet/Home/issues/9395) rozwiązania/projektu

* Dodano `latest` opcję dla `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

**Błędy:**

* W przypadku przywracania interfejsu wiersza polecenia dotnet podczas uruchamiania wtyczek poświadczeń wypróbuj interfejs wiersza polecenia dotnet na ścieżce systemowej, jeśli `DOTNET_HOST_PATH`  zmienna środowiskowa nie jest zdefiniowana. - [#7438](https://github.com/NuGet/Home/issues/7438)

* Specyfikacja nuget.exea generuje tag Copyright z zakodowanym tekstem Copyright rrrr zamiast `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)

* NuGet.exe zgłasza wyjątek "autorów wymaganych" w trakcie pakowania csproj ignorowanie symboli zastępczych i atrybutów AssemblyInfo, jeśli nazwa zestawu zostanie zmieniona — [#4234](https://github.com/NuGet/Home/issues/4234)

* HttpRequestMessage wielokrotnie wykorzystano wielokrotnie, co nie jest obsługiwane w przypadku SocketHttpHandler- [#8661](https://github.com/NuGet/Home/issues/8661)

* NuGet. Indexing 5.6.0 wersja zapoznawcza 3 i nowsze używają innego tokenu klucza publicznego — [#9481](https://github.com/NuGet/Home/issues/9481)

* Honor TreatWarningsAsErrors podczas tworzenia pakietu NuGet — [#7404](https://github.com/NuGet/Home/issues/7404)

* [CPVM] Fałszywe obniżenie pakietów dla wielu projektów P2P — [#9549](https://github.com/NuGet/Home/issues/9549)

* Karta "Przeglądaj" nie jest wyrównana do lewej strony pola wyszukiwania — [#9559](https://github.com/NuGet/Home/issues/9559)

* Zainstalowana wersja jest niespójna z osadzoną ikoną w interfejsie użytkownika PM poziomu rozwiązania dla jednego identyfikatora pakietu z zainstalowanymi wieloma wersjami — [#9321](https://github.com/NuGet/Home/issues/9321)

* Przeciek: obiektu partcreationpolicy (CreationPolicy. inshared) NuGet. SolutionRestoreManager. RestoreOperationLogger- [#9595](https://github.com/NuGet/Home/issues/9595)

* Unikanie odczytywania pliku zasobów w ramach przywracania No-op — [#9693](https://github.com/NuGet/Home/issues/9693)

* Pakiet NuGet. Protocol nie obsługuje pobierania liczby pobieranych wersji z wyszukiwania [#9086](https://github.com/NuGet/Home/issues/9086)

* Zwiększenie wydajności pamięci PackageMetadataResourceV3 przez zredukowanie zależności JObject — [#9719](https://github.com/NuGet/Home/issues/9719)

**Żądania zmiany projektu:**

* Pominięto `<owners>` element, gdy jest nadmiarowy — [#5134](https://github.com/NuGet/Home/issues/5134)

* Rejestruj IntervalTrackers jako zdarzenia ETW — [#9593](https://github.com/NuGet/Home/issues/9593)

* Dodano komunikat informacyjny dotyczący przywracania w celu informowania użytkowników CPVM o tym, że ta funkcja jest w wersji zapoznawczej — [#9340](https://github.com/NuGet/Home/issues/9340)

* Wypełnij Eksplorator rozwiązań zależności między pakietami i projektami z pliku zasobów — [#9580](https://github.com/NuGet/Home/issues/9580)

* Na karcie zainstalowane pakiety nie należy podzielić na strony listy pakietów — [#6995](https://github.com/NuGet/Home/issues/6995)

**[Lista wszystkich problemów rozwiązanych w tej wersji — 5,7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**

### <a name="community-contributions"></a>Materiały przekazywane przez społeczność

Dziękujemy, że wszyscy Współautorzy, którzy pomogą Ci w udostępnieniu tej wersji NuGet!

|Którzy|Żądań ściągnięcia|Problemy|
|----|----|----|
|[campersau](https://github.com/campersau)|[3433](https://github.com/NuGet/NuGet.Client/pull/3433), [3120](https://github.com/NuGet/NuGet.Client/pull/3120)|Pakiet NuGet. Protocol nie obsługuje pobierania liczby pobieranych wersji z wyszukiwania [#9086](https://github.com/NuGet/Home/issues/9086) </br>HttpRequestMessage wielokrotnie wykorzystano wielokrotnie, co nie jest obsługiwane w przypadku SocketHttpHandler- [#8661](https://github.com/NuGet/Home/issues/8661)|
|[Joseph Musser (jnm2)](https://github.com/jnm2)|[3241](https://github.com/NuGet/NuGet.Client/pull/3241)|Pominięto `<owners>` element, gdy jest nadmiarowy — [#5134](https://github.com/NuGet/Home/issues/5134)|
|[Volodymyr Shkolka (BlackGad)](https://github.com/BlackGad)|[3273](https://github.com/NuGet/NuGet.Client/pull/3273)|Pakiet NuGet nie może zostać przywrócony ze źródeł HTTPS, które wymagają certyfikatów klienta — [#5773](https://github.com/NuGet/Home/issues/5773)|
|[Mariusa Ungureanu (Therzok)](https://github.com/Therzok)|[3357](https://github.com/NuGet/NuGet.Client/pull/3357)|HttpSourceAuthenticationHandler SemaphoreSlim w przyszłości — [#9463](https://github.com/NuGet/Home/issues/9463)|
|[Sunner (SuNNjek)](https://github.com/SuNNjek)|[3088](https://github.com/NuGet/NuGet.Client/pull/3088)|Specyfikacja nuget.exea generuje tag Copyright z zakodowanym tekstem Copyright rrrr zamiast `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)|
|[Olivier Spinelli (olivier-spinelli)](https://github.com/olivier-spinelli)|[3335](https://github.com/NuGet/NuGet.Client/pull/3335)|W przypadku przywracania interfejsu wiersza polecenia dotnet podczas uruchamiania wtyczek poświadczeń wypróbuj interfejs wiersza polecenia dotnet na ścieżce systemowej, jeśli `DOTNET_HOST_PATH`  zmienna środowiskowa nie jest zdefiniowana. - [#7438](https://github.com/NuGet/Home/issues/7438)|
|[goyzhang](https://github.com/goyzhang)|[3370](https://github.com/NuGet/NuGet.Client/pull/3370)|Dodano `latest` opcję dla `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)|
