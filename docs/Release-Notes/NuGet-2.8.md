---
title: Informacje o wersji NuGet 2.8 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informacje o wersji dla tym znanych problemów, poprawki, dodatkowe funkcje i dcr 2.8 NuGet."
keywords: NuGet 2.8 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 39b885adc9e23eb815f65639875c4a4c27d61a4c
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-28-release-notes"></a>Informacje o wersji 2,8 NuGet

[Informacje o wersji NuGet 2.7.2](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 informacje o wersji](../release-notes/nuget-2.8.1.md)

NuGet 2.8 został wydany 29 stycznia 2014 roku.

## <a name="acknowledgements"></a>Potwierdzeń

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) — podczas pakowania pakietów, weryfikowanie identyfikator zależności pakietów.
1. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) -usuń sufiks $metadata, gdy persistening podawania poświadczeń.
1. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) — obsługa określania pliku projektu dla polecenia update nuget.exe.
1. [Juan Gonzales](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) -tokeny zamiany nie zostały przekazane z - IncludeReferencedProjects.
1. [Dominik Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -Usuń nuget.push zgłaszanie OutOfMemoryException, gdy wypychanie duży pakiet.
1. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -ścieżki docelowej niepoprawny poprawka gdy projekt odwołuje się do innego projektu interfejsu wiersza polecenia/C++.
1. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) — Zezwalaj na pakiety instalowanego jako zależności programowanie domyślnie
1. [Dominik Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -Usuń niejawne uaktualnienia do najnowszej wersji poprawki
1. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Kilka usterek poprawki i poprawki dotyczące NuGet.Server, polecenie dublowanie nuget.exe i inne.
    - Praca ta została wykonana przez kilka miesięcy, z Gregory współpracę nad chronometrażu prawo do integracji główny 2.8.

## <a name="patch-resolution-for-dependencies"></a>Poprawka rozpoznawania zależności

Podczas rozpoznawania zależności pakietów, NuGet w przeszłości zaimplementowała strategię wybranie Najniższa wersja pakietu główne i pomocnicze, spełniającego zależności w pakiecie. W odróżnieniu od wersji głównej i pomocniczej jednak wersji poprawki zawsze rozpoznano do najwyższej wersji. Chociaż zachowanie był dobrze tych, utworzyć braku determinizm podczas instalowania pakietów z zależności. Rozważmy następujący przykład:

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

W tym przykładzie, nawet jeśli Developer1 i Developer2 zainstalowane PackageA@1.0.0, każdy zakończone się za pomocą innej wersji PackageB. NuGet 2.8 zmienia to zachowanie domyślne, tak, aby był zgodny z zachowanie wersję główną i pomocniczą sposób rozpoznawania zależności dla wersji poprawki. W powyższym przykładzie, a następnie PackageB@1.0.0 zostaną zainstalowane w wyniku instalacji PackageA@1.0.0, niezależnie od nowsza wersja poprawki.

## <a name="-dependencyversion-switch"></a>Przełącznika - DependencyVersion

Chociaż zmienia NuGet 2.8 _domyślne_ zachowanie dla rozpoznawania zależności, dodane również dokładniejszej kontroli nad procesem rozpoznawania zależności za pomocą przełącznika - DependencyVersion w konsoli Menedżera pakietów. Przełącznik umożliwia rozpoznawania zależności Najniższa wersja możliwe (domyślnie), jest najwyższa możliwa wersja najwyższy pomocnicze lub wersji poprawki.  Ta opcja działa tylko dla pakiet instalacyjny polecenia programu powershell.

![Przełącznik DependencyVersion](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>Atrybut DependencyVersion

Oprócz przełącznika - DependencyVersion wymienione powyżej, mogą również NuGet możliwości można ustawić nowy atrybut w pliku Nuget.Config. Definiowanie co to jest wartość domyślna, gdy w wywołaniu nie został określony przełącznik - DependencyVersion pakiet instalacyjny. Ta wartość zostanie również przestrzegane za pomocą okna dialogowego Menedżer pakietów NuGet dla wszystkich operacji pakietu instalacji. Aby ustawić tę wartość, do pliku Nuget.Config. Dodaj atrybut poniżej:

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>-Whatif operacji NuGet w wersji zapoznawczej

Niektóre pakiety NuGet może mieć wykresy zależności bezpośrednich i tak, on być pomocne podczas instalacji, odinstalować ani zaktualizować operacji do najpierw Zobacz, co się stanie. NuGet 2.8 dodaje standardowego przełącznika - whatif programu PowerShell install-package, odinstaluj pakiet i polecenia powodujące włączenie wizualizacja całego zamknięcia pakietów, do których zostaną zastosowane polecenie pakiet aktualizacji. Na przykład uruchomiona `install-package Microsoft.AspNet.WebApi -whatif` w pustym sieci Web ASP.NET aplikacji daje następujące.

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

## <a name="downgrade-package"></a>Zmień wersję pakietu

Nie jest rzadko do zainstalowania wstępnej wersji pakietu w celu zbadania nowe funkcje i zdecydować przywrócić ostatnią stabilną wersję. Przed NuGet 2.8 to proces wieloetapowych odinstalowaniu wersji wstępnej pakiet i jego zależności, a następnie zainstalować starszą wersję. Z 2.8 NuGet jednak pakiet aktualizacji teraz cofnie zamknięcia całego pakietu (np. drzewo zależności pakietu) do poprzedniej wersji.

## <a name="development-dependencies"></a>Programowanie zależności

Wiele różnych typów możliwości mogą być dostarczane jako pakiety NuGet — w tym narzędzia, które są używane do optymalizacji procesu tworzenia. Te składniki mogą być instrumentalnego w tworzeniu nowego pakietu, nie należy traktować jako zależność nowy pakiet publikowanych później. NuGet 2.8 umożliwia pakietu w celu identyfikacji w `.nuspec` pliku jako developmentDependency. Po zainstalowaniu tych metadanych również zostaną dodane do `packages.config` pliku projektu, w którym został zainstalowany pakiet. Gdy który `packages.config` zależności NuGet podczas dalszej analizy pliku `nuget.exe pack`, spowoduje wykluczenie tych zależności oznaczona jako programowanie zależności.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Packages.config poszczególnych plików na różnych platformach

Opracowywanie aplikacji dla wielu platform docelowych, jest często mają różne pliki projektów dla poszczególnych środowisk odpowiednich kompilacji. Również jest często użycie różnych pakietów NuGet w plikach projektu różnych pakietów mają różne poziomy wsparcia dla różnych platform. NuGet 2.8 zapewnia ulepszoną obsługę tego scenariusza, tworząc różnych `packages.config` plików dla plików inny projekt specyficzne dla platformy.

![Wiele plików package.config](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Powrót do lokalnej pamięci podręcznej

Chociaż pakiety NuGet są zazwyczaj używane z galerii zdalnego takich jak [galerii NuGet](http://www.nuget.org/) połączenia z siecią, istnieje wiele scenariuszy, w których klient nie jest połączony. Bez połączenia sieciowego klienta NuGet nie może pomyślnie zainstalować pakiety — nawet wtedy, gdy pakiety zostały już na komputerze klienckim w lokalnej pamięci podręcznej NuGet. NuGet 2.8 dodaje automatyczne pamięci podręcznej powrotu do konsoli Menedżera pakietów. Na przykład gdy odłączenie karty sieciowej oraz jest instalowany jQuery, konsoli znajdują się:

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

Funkcja rezerwowej pamięci podręcznej nie wymaga żadnych argumentów danego polecenia. Ponadto rezerwowej pamięci podręcznej jest obecnie obsługiwane tylko w konsoli Menedżera pakietów — zachowanie aktualnie nie działa w oknie dialogowym Menedżer pakietów.

## <a name="webmatrix-nuget-client-updates"></a>Aktualizacje klienta NuGet programu WebMatrix

Wraz z NuGet 2.8 rozszerzenie NuGet dla programu WebMatrix Zaktualizowano również uwzględnienie wielu najważniejszych funkcji, które są oferowane przez [NuGet 2.5](../release-notes/nuget-2.5.md). Zawiera nowe funkcje takie jak "Aktualizuj wszystkie", "Minimalna wersja narzędzia NuGet" i zezwala na zastępowanie plików zawartości.

Aby zaktualizować rozszerzenia Menedżera pakietów NuGet w programie WebMatrix 3:

1. Otwórz program WebMatrix 3
1. Kliknij ikonę rozszerzeń na Wstążce
1. Wybierz kartę aktualizacji
1. Kliknij, aby zaktualizować Menedżera pakietów NuGet do 2.5.0
1. Zamknij i uruchom ponownie program WebMatrix 3

Jest to zespołu NuGet pierwszej wersji rozszerzenia Menedżera pakietów NuGet dla programu WebMatrix.  Ten kod został ostatnio zamieszczone przez firmę Microsoft do projektu NuGet open source. Poprzednio integracji z programem NuGet został utworzony w programie WebMatrix i nie może zostać zaktualizowana poza pasmem z programu WebMatrix.  Mamy teraz możliwość dalszego aktualizacji wraz z resztą narzędzia klienta NuGet.

## <a name="bug-fixes"></a>Poprawki błędów

Jeden z głównych poprawki wprowadzone jest zwiększenie wydajności w pakiecie aktualizacji-Zainstaluj ponownie polecenie.

Oprócz tych funkcji i popraw wyżej wymienione wydajności ta wersja programu NuGet zawiera również inne poprawki błędów. Znaleziono 181 całkowita problemy rozwiązane w wersji. Pełną listę prac elementów ustalone w NuGet 2.8, sprawdź widok [NuGet Tracker problem w tej wersji](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
