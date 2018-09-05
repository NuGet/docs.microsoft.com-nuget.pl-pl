---
title: Informacje o wersji 2.8 NuGet
description: Informacje o wersji programu NuGet 2.8 tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547462"
---
# <a name="nuget-28-release-notes"></a>Informacje o wersji 2.8 NuGet

[Informacje o wersji NuGet 2.7.2](../release-notes/nuget-2.7.2.md) | [informacjach o wersji NuGet 2.8.1](../release-notes/nuget-2.8.1.md)

NuGet 2.8 został wydany 29 stycznia 2014 roku.

## <a name="acknowledgements"></a>Potwierdzanie

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) — w przypadku pakowania pakietów, weryfikowanie identyfikator zależności pakietów.
2. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) -usuń sufiks $metadata, gdy persistening podawania poświadczeń.
3. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) — Określanie pliku projektu dla polecenia update nuget.exe pomocy technicznej.
4. [Juan Gonzales](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) — tokeny zastępowania nie zostały przekazane z - IncludeReferencedProjects.
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -napraw nuget.push zgłaszanie OutOfMemoryException podczas wypychania duży pakiet.
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) — ścieżka nieprawidłowym elementem docelowym poprawki, jeśli projekt odwołuje się do innego projektu interfejsu wiersza polecenia/C++.
7. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) — Zezwalaj na pakiety do zainstalowania jako zależności rozwoju domyślnie
8. [David Fowlera](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -Usuń niejawne uaktualnienia do najnowszej wersji poprawki
9. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Niektóre poprawki błędów i ulepszenia NuGet.Server, polecenie dublowanie nuget.exe i inne.
    - Tę pracę zostało wykonane w ciągu kilku miesięcy, przy użyciu Gregory współpracę nad chronometrażu prawo do integracji z wzorcem 2.8.

## <a name="patch-resolution-for-dependencies"></a>Rozpoznawanie poprawki dla zależności

Podczas rozpoznawania zależności pakietów, NuGet w przeszłości została zaimplementowana strategii wybierania Najniższa wersja pakietu głównych i pomocniczych, spełniające zależności w pakiecie. W przeciwieństwie do wersji głównych i pomocniczych, wersja poprawki zabezpieczeń był zawsze rozpoznać najwyższa wersja. Chociaż zachowanie było intencjami, utworzyć braku determinizm dla instalowanie pakietów z zależnościami. Rozważmy następujący przykład:

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

W tym przykładzie, nawet jeśli Developer1 i Developer2 zainstalowane PackageA@1.0.0, każdy zakończone się w innej wersji PackageB. NuGet 2.8 zmienia to zachowanie domyślne w taki sposób, że sposób rozpoznawania zależności dla wersji poprawki jest zgodne z zachowaniem dla wersji głównych i pomocniczych. W powyższym przykładzie, a następnie PackageB@1.0.0 zostanie zainstalowany w wyniku instalacji PackageA@1.0.0, niezależnie od tego, nowsza wersja poprawki.

## <a name="-dependencyversion-switch"></a>DependencyVersion — przełącznik

Chociaż zmienia NuGet 2.8 _domyślne_ zachowanie dla rozpoznawania zależności, dodaje także bardziej precyzyjną kontrolę nad procesem rozpoznawania zależności za pośrednictwem przełącznika - DependencyVersion w konsoli Menedżera pakietów. Przełącznik umożliwia rozpoznawania zależności, aby Najniższa wersja możliwe (zachowanie domyślne), najnowsza wersja to możliwe, lub najwyższy drobnych lub wersja poprawki zabezpieczeń.  Ta opcja działa tylko dla install-package polecenia programu powershell.

![Przełącznik DependencyVersion](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>Atrybut DependencyVersion

Oprócz przełącznika - DependencyVersion szczegóły przedstawiono powyżej, NuGet ma również dozwolone dla możliwości można ustawić nowy atrybut w pliku Nuget.Config Definiowanie co to jest wartość domyślna, jeśli nie określono przełącznika - DependencyVersion w wywołania Install-package. Ta wartość obowiązują również w oknie dialogowym Menedżer pakietów NuGet dla wszystkich operacji pakietu instalacji. Aby ustawić tę wartość, należy dodać atrybut poniżej do pliku Nuget.Config:

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>-Whatif operacje NuGet w wersji zapoznawczej

Niektóre pakiety NuGet może mieć wykresy zależności szczegółowe i jako takie on być przydatne podczas instalacji, odinstalowywania i zaktualizować operację, aby najpierw sprawdzić, co się stanie. NuGet 2.8 dodaje standardowego przełącznika - whatif PowerShell install-package, odinstaluj pakiet i polecenia pakietu aktualizacji, aby włączyć, wizualizowanie całego zamknięcia pakietów, do których zostanie zastosowana polecenia. Aby na przykład uruchomić `install-package Microsoft.AspNet.WebApi -whatif` w puste ASP.NET sieci Web aplikacji daje następujące czynności.

    PM> install-package Microsoft.AspNet.WebApi -whatif
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.WebHost (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Core (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Client (≥ 5.0.0)'.
    Attempting to resolve dependency 'Newtonsoft.Json (≥ 4.5.11)'.
    Install Newtonsoft.Json 4.5.11
    Install Microsoft.AspNet.WebApi.Client 5.0.0
    Install Microsoft.AspNet.WebApi.Core 5.0.0
    Install Microsoft.AspNet.WebApi.WebHost 5.0.0
    Install Microsoft.AspNet.WebApi 5.0.0

## <a name="downgrade-package"></a>Obniżanie wersji pakietu

Nie jest niczym niezwykłym, aby zainstalować wstępną wersję pakietu w celu zbadania nowe funkcje i zdecydować wycofać do ostatniego stabilnej wersji. Przed NuGet 2.8 to wieloetapowy proces odinstalowywania wstępną wersję pakietu oraz jego zależności, a następnie zainstaluj starszą wersję. Za pomocą NuGet 2.8, pakiet aktualizacji będzie teraz wycofać zamknięcia cały pakiet (np. drzewo zależności pakietu) do poprzedniej wersji.

## <a name="development-dependencies"></a>Tworzenie zależności

Wiele różnych typów funkcji mogą być dostarczane jako pakietów NuGet — w tym narzędzia, które są używane do optymalizacji procesu rozwoju. Te składniki mogą być zarejestrowana w tworzeniu nowego pakietu, nie należy rozważyć zależność nowego pakietu po opublikowaniu go później. NuGet 2.8 umożliwia pakietu do identyfikacji w `.nuspec` pliku jako developmentDependency. Po zainstalowaniu tych metadanych także zostaną dodane do `packages.config` pliku projektu, do którego pakiet został zainstalowany. Gdy, `packages.config` zależności NuGet podczas dalszej analizy pliku `nuget.exe pack`, spowoduje wykluczenie, te zależności, oznaczone jako zależności rozwoju.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Pliki poszczególnych packages.config na różnych platformach

Podczas opracowywania aplikacji dla wielu platform docelowych jest często mają różne pliki projektów dla poszczególnych środowisk odpowiednich kompilacji. Jest również typowe korzystanie z różnych pakietach NuGet w plikach inny projekt, pakiety są dostępne dla różnych poziomów pomocy technicznej dla różnych platform. NuGet 2.8 zapewnia ulepszoną obsługę tego scenariusza, tworząc różne `packages.config` plików dla plików do innego projektu specyficznego dla platformy.

![Wiele plików package.config plików](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Powrót do lokalnej pamięci podręcznej

Chociaż pakiety NuGet są zwykle używane z galerii zdalnego takich jak [galerii pakietów NuGet](http://www.nuget.org/) połączenia z siecią, istnieje wiele scenariuszy, w których klient nie jest połączony. Bez połączenia sieciowego klienta programu NuGet nie mógł pomyślnie zainstalować pakiety — nawet wtedy, gdy te pakiety zostały już na komputerze klienckim, w lokalnej pamięci podręcznej narzędzia NuGet. NuGet 2.8 dodaje automatyczne rezerwowego pamięci podręcznej do konsoli Menedżera pakietów. Na przykład podczas odłączenie karty sieciowej i instalowanie jQuery, w konsoli wyświetlone zostaną następujące:

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

Funkcja rezerwowego pamięci podręcznej nie wymaga żadnych argumentów. Ponadto pamięć podręczna rezerwowego obecnie działa tylko w konsoli Menedżera pakietów — zachowanie aktualnie nie działa w oknie dialogowym Menedżer pakietów.

## <a name="webmatrix-nuget-client-updates"></a>Aktualizacje klienta programu NuGet programu WebMatrix

Wraz z NuGet 2.8 rozszerzenie NuGet dla programu WebMatrix został także zaktualizowany obejmujący wiele główne funkcje oferowane przez [NuGet 2.5](../release-notes/nuget-2.5.md). Nowe możliwości obejmują te, takich jak "Update All", "Minimalna NuGet w wersji" i pozwalając na zastąpienie plików zawartości.

Aby zaktualizować rozszerzenia Menedżera pakietów NuGet w programie WebMatrix 3:

1. Otwórz program WebMatrix 3
1. Kliknij ikonę rozszerzenia na Wstążce
1. Wybierz kartę Aktualizacje
1. Kliknij, aby zaktualizować Menedżera pakietów NuGet do 2.5.0
1. Zamknij i ponownie uruchom program WebMatrix 3

Jest to zespół NuGet pierwsza wersja rozszerzenia Menedżera pakietów NuGet dla programu WebMatrix.  Kod został niedawno zamieszczone przez firmę Microsoft do projektu NuGet typu open source. Wcześniej integracji NuGet został utworzony w programie WebMatrix i nie może zostać zaktualizowana poza pasmem z programu WebMatrix.  Teraz mamy możliwość dalszego zaktualizować go razem z pozostałymi narzędziami klienckimi NuGet.

## <a name="bug-fixes"></a>Poprawki błędów

Jedną z głównych poprawki wprowadzone był poprawę wydajności w pakiecie aktualizacji-Zainstaluj ponownie polecenie.

Oprócz te funkcje i poprawki wymienione wyżej wydajności ta wersja programu NuGet obejmuje wiele poprawek błędów. Wystąpiły 181 Suma problemów, które zostały rozwiązane w wydaniu. Aby uzyskać pełną listę prac elementy rozwiązane w NuGet 2.8, widok [NuGet narzędzie do śledzenia problemów w tej wersji](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
