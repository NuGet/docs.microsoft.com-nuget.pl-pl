---
title: Informacje o wersji narzędzia NuGet 5,3
description: Informacje o wersji programu NuGet 5,3, w tym nowe funkcje, poprawki błędów i DCR.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: e77219d355f73f3bf01f68283ffb2759813af563
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611327"
---
# <a name="nuget-53-release-notes"></a>Informacje o wersji narzędzia NuGet 5,3

Pojazdy dystrybucji NuGet:

| Wersja programu NuGet | Dostępne w wersji programu Visual Studio| Dostępne w zestawach SDK platformy .NET|
|:---|:---|:---|
| [**5.3.0**](https://nuget.org/downloads) | [Visual Studio 2019 w wersji 16,3](https://visualstudio.microsoft.com/downloads/) | [3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup> |
| [**5.3.1**](https://nuget.org/downloads) | [Visual Studio 2019 w wersji 16.3.6](https://visualstudio.microsoft.com/downloads/) | [Przyszła wersja: 3.0.101](https://dotnet.microsoft.com/download/dotnet-core/3.0) |

<sup>1</sup> Zainstalowane z programem Visual Studio 2019 przy użyciu obciążenia .NET Core

## <a name="summary-whats-new-in-53"></a>Podsumowanie: co nowego w 5,3

* [Ikonę pakietu można osadzić w pakiecie](../reference/msbuild-targets.md#packing-an-icon-image-file), zamiast korzystać z zewnętrznego adresu URL. - [#352](https://github.com/NuGet/Home/issues/352)

* Ulepszone zabezpieczenia dzięki śledzeniu i wymuszaniu algorytmu SHA dla pakietów Packages. config — [#7281](https://github.com/NuGet/Home/issues/7281)

* Włącz wycofanie przestarzałych/starszych pakietów NuGet [#2867](https://github.com/NuGet/Home/issues/2867) | [wpis w blogu](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [docs](https://docs.microsoft.com/nuget/nuget-org/deprecate-packages)

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

**Usterek**

* Pakiety NuGet utworzone za pomocą zestawu SDK 3.0.100-preview9 nie mogą być używane przez użytkowników SDK 2,2... w zależności od [#8603](https://github.com/NuGet/Home/issues/8603) strefy czasowej

* "Znaki cudzysłowu" w ścieżce powodują awarię "niedozwolone znaki w ścieżce" w `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)

* VS: zestawy są w pełni NGen-Ed nie częściowo NGen-Ed- [#8513](https://github.com/NuGet/Home/issues/8513)

* Zmniejsz użycie pamięci (anulowanie subskrypcji zdarzeń) — [#8471](https://github.com/NuGet/Home/issues/8471)

* Komunikat "Error_UnableToFindProjectInfo" nie jest poprawny gramatycznie — [#8441](https://github.com/NuGet/Home/issues/8441)

* Udoskonalenia NU1403 — sprawdzaj poprawność wszystkich pakietów, Uwzględnij oczekiwane/rzeczywiste wartości SHA- [#8424](https://github.com/NuGet/Home/issues/8424)

* Wielokrotne Wyliczenie w `NuGetPackageManager.PreviewUpdatePackagesAsync` - [#8401](https://github.com/NuGet/Home/issues/8401)

* Przywróć zmianę "Public-> Internal" w PluginProcess — [#8390](https://github.com/NuGet/Home/issues/8390)

* IVsPackageSourceProvider. getsources (...) ma źle zdefiniowane zachowanie wyjątków — [#8383](https://github.com/NuGet/Home/issues/8383)

* Utwórz ponownie Konstruktor wtyczki — [#8379](https://github.com/NuGet/Home/issues/8379)

* Metryki do śledzenia częstotliwości odświeżania interfejsu użytkownika PM — [#8369](https://github.com/NuGet/Home/issues/8369)

* Zmniejsz liczbę odświeżanych interfejsów użytkownika podczas instalacji za pomocą interfejsu użytkownika Menedżera pakietów — [#8358](https://github.com/NuGet/Home/issues/8358)

* Telemetrię: wartości DateTime używają formatów specyficznych dla kultury — [#8351](https://github.com/NuGet/Home/issues/8351)

* Zmniejsz liczbę odświeżanych interfejsów użytkownika na karcie Przeglądaj w interfejsie użytkownika Menedżera pakietów #6570 — [#8339](https://github.com/NuGet/Home/issues/8339)

* [Niepowodzenie testu] "Nie można przeanalizować pliku konfiguracji" zostanie wyświetlony monit dwa razy — [#8320](https://github.com/NuGet/Home/issues/8320)

* Zgłoś błąd NU5037 z dobrą stroną dokumentu, która objaśnia poprawki klientów (w pakiecie brakuje wymaganego pliku nuspec) — [#8291](https://github.com/NuGet/Home/issues/8291)

* Przywracanie w trybie zablokowanym kończy się niepowodzeniem, gdy RuntimeIdentifier projektu zostanie zmieniony — [#8260](https://github.com/NuGet/Home/issues/8260)

* Ustaw odczytywanie ustawień w programie VS z opóźnieniem [#8156](https://github.com/NuGet/Home/issues/8156)

* Regresja w `Nuget sources add` powoduje, że "znak": ", wartość szesnastkowa 0x3A, nie może zostać uwzględniony w nazwie" Błędy — [#7948](https://github.com/NuGet/Home/issues/7948)

* Dostawcy poświadczeń wtyczki NuGet — ukrywanie okna procesu — [#7511](https://github.com/NuGet/Home/issues/7511)

* Wymuś PackagePathResolver jest ścieżką bezwzględną- [#7349](https://github.com/NuGet/Home/issues/7349)

* Zmniejsz odświeżanie interfejsu użytkownika na kartach Instalowanie i aktualizowanie interfejsu użytkownika Menedżera pakietów — [#6570](https://github.com/NuGet/Home/issues/6570)

**DCR**

* Aktualizowanie platform platformy Xamarin do mapowania na Standard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368)

* Włącz kopiowanie zawartości Menedżera pakietów "okno podglądu" dla instalacji/aktualizacji- [#8324](https://github.com/NuGet/Home/issues/8324)

* Włącz przywracanie na plikach. proj — [#8212](https://github.com/NuGet/Home/issues/8212)

* Wprowadź `NUGET_NETFX_PLUGIN_PATHS` i `NUGET_NETCORE_PLUGIN_PATHS` do obsługi konfiguracji obu jednocześnie [#8151](https://github.com/NuGet/Home/issues/8151)

* Włącz wiele wersji dla PackageDownload za pomocą atrybutu Version- [#8074](https://github.com/NuGet/Home/issues/8074)

* Opcje Add-SolutionDirectory i-PackageDirectory do programu NuGet. exe Pack- [#7163](https://github.com/NuGet/Home/issues/7163)

**[Lista wszystkich problemów rozwiązanych w tej wersji — 5,3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**

## <a name="summary-whats-new-in-531"></a>Podsumowanie: co nowego w programie 5.3.1

* Wtyczka: zadanie zostało anulowane — nie Zezwalaj na anulowanie dla tworzenia wystąpienia wtyczki — [#8648](https://github.com/NuGet/Home/issues/8648)

* Nie można bezpiecznie uruchomić zadania przywracania dwa razy w jednym procesie (gdy są używane dostawcy poświadczeń) — [#8688](https://github.com/NuGet/Home/issues/8688)
