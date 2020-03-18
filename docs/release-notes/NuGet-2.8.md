---
title: Informacje o wersji narzędzia NuGet 2,8
description: Informacje o wersji programu NuGet 2,8, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/16/2020
ms.locfileid: "79429053"
---
# <a name="nuget-28-release-notes"></a>Informacje o wersji narzędzia NuGet 2,8

[Informacje o wersji narzędzia NuGet 2.7.2](../release-notes/nuget-2.7.2.md) | [Informacje o wersji narzędzia NuGet 2.8.1](../release-notes/nuget-2.8.1.md)

Pakiet NuGet 2,8 został wydaną 29 stycznia 2014.

## <a name="acknowledgements"></a>Podziękowania

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) — gdy pakiety są zapakowane, weryfikowanie identyfikatora pakietów zależności.
2. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) — usuń sufiks $Metadata, gdy poświadczenia źródła danych persistening.
3. [Filip de Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) — obsługa określania pliku projektu dla polecenia programu NuGet. exe Update.
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - tokeny zastępcze [#3536](http://nuget.codeplex.com/workitem/3536) nie zostały przesłane z-IncludeReferencedProjects.
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -Fix NuGet. wypychanie generowanie OutOfMemoryException podczas wypychania dużego pakietu.
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) — Popraw niepoprawną ścieżkę docelową, gdyC++ projekt odwołuje się do innego interfejsu wiersza polecenia/projektu
7. [Adam](http://www.codeplex.com/site/users/view/adamralph) : ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) — Zezwalaj na instalowanie pakietów jako zależności programistyczne
8. [David Fowlera](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -Usuń niejawne uaktualnienia do najnowszej wersji poprawki
9. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Kilka poprawek błędów i ulepszeń dla NuGet. Server, polecenia dublowania NuGet. exe i innych.
    - Ta praca została wykonana przez kilka miesięcy, a firma Gregory współpracuje z nami po prawej stronie, aby zintegrować ją z serwerem głównym dla 2,8.

## <a name="patch-resolution-for-dependencies"></a>Rozpoznawanie poprawek dla zależności

W przypadku rozpoznawania zależności pakietów pakiet NuGet ma historyczną strategię wybierania najmniejszej wersji głównej i pomocniczej pakietu, która spełnia zależności pakietu. W przeciwieństwie do wersji głównej i pomocniczej, wersja poprawki była zawsze rozwiązywana do najwyższej wersji. Mimo że zachowanie zostało prawidłowo zamierzone, utworzono brakujące ustalenia dotyczące instalowania pakietów z zależnościami. Rozważmy następujący przykład:

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

W tym przykładzie, mimo że Developer1 i Developer2 zainstalowane PackageA@1.0.0, każdy z nich zakończył działanie z inną wersją PackageB. Program NuGet 2,8 zmienia to zachowanie domyślne, tak że zachowanie rozpoznawania zależności dla wersji poprawek jest spójne z zachowaniem wersji głównych i pomocniczych. W powyższym przykładzie, PackageB@1.0.0 zostanie zainstalowany w wyniku zainstalowania PackageA@1.0.0, niezależnie od nowszej wersji poprawki.

## <a name="-dependencyversion-switch"></a>-DependencyVersion przełącznik

Chociaż w pakiecie NuGet 2,8 zmiany _domyślne_ zachowanie rozpoznawania zależności, program dodaje również dokładniejszą kontrolę nad procesem rozpoznawania zależności za pośrednictwem przełącznika-DependencyVersion w konsoli Menedżera pakietów. Przełącznik włącza rozpoznawanie zależności do najmniejszej możliwej wersji (domyślnego zachowania), najwyższej możliwej wersji lub najwyższej wersji pomocniczej lub poprawki.  Ten przełącznik działa tylko w przypadku instalacji pakietu w poleceniu programu PowerShell.

![Przełącznik DependencyVersion](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>DependencyVersion — atrybut

Oprócz przełącznika-DependencyVersion powyższego powyżej, NuGet również może ustawić nowy atrybut w pliku NuGet. config definiujący, co to jest wartość domyślna, jeśli przełącznik-DependencyVersion nie jest określony w wywołaniu Zainstaluj pakiet. Ta wartość będzie również przestrzegana przez okno dialogowe Menedżera pakietów NuGet dla wszystkich operacji instalacji pakietu. Aby ustawić tę wartość, Dodaj poniższy atrybut do pliku NuGet. config:

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>Podgląd operacji NuGet przy użyciu-whatIf

Niektóre pakiety NuGet mogą mieć szczegółowe wykresy zależności i w ten sposób mogą być przydatne podczas operacji instalowania, odinstalowywania lub aktualizacji, aby najpierw zobaczyć, co się stanie. Program NuGet 2,8 dodaje standardowy przełącznik programu PowerShell-whatIf do poleceń install-package, Uninstall-Package i Update-Package, aby umożliwić wizualizowanie całego zamknięcia pakietów, do których zostanie zastosowane polecenie. Na przykład uruchomienie `install-package Microsoft.AspNet.WebApi -whatif` w pustej aplikacji sieci Web ASP.NET daje następujące działania.

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

## <a name="downgrade-package"></a>Pakiet obniżenia poziomu

Zainstalowanie wersji wstępnej pakietu nie jest nietypowo, aby można było zbadać nowe funkcje, a następnie podjąć decyzję o wycofaniu do ostatniej stabilnej wersji. Przed pakietem NuGet 2,8 jest to proces wieloetapowy odinstalowywania pakietu wstępnego wraz z jego zależnościami, a następnie instalowania wcześniejszej wersji. W przypadku programu NuGet 2,8 pakiet aktualizacji spowoduje teraz wycofanie całego zamknięcia pakietu (np. drzewa zależności pakietu) do poprzedniej wersji.

## <a name="development-dependencies"></a>Zależności programistyczne

Wiele różnych typów możliwości można dostarczyć jako pakiety NuGet — w tym narzędzia służące do optymalizowania procesu tworzenia oprogramowania. Te składniki, chociaż mogą być instrumentalem podczas tworzenia nowego pakietu, nie powinny być traktowane jako zależność nowego pakietu, gdy jest on później publikowany. Program NuGet 2,8 umożliwia pakietowi identyfikację w pliku `.nuspec` jako developmentDependency. Po zainstalowaniu te metadane również zostaną dodane do pliku `packages.config` projektu, w którym został zainstalowany pakiet. Gdy ten `packages.config` plik zostanie później przeanalizowany pod kątem zależności NuGet podczas `nuget.exe pack`, spowoduje to wykluczenie tych zależności jako zależności deweloperskie.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Poszczególne pliki Packages. config dla różnych platform

Podczas tworzenia aplikacji dla wielu platform docelowych często istnieją różne pliki projektu dla każdego z odpowiednich środowisk kompilacji. Często używa się również różnych pakietów NuGet w różnych plikach projektu, ponieważ pakiety mają różne poziomy obsługi dla różnych platform. Pakiet NuGet 2,8 zapewnia ulepszoną obsługę tego scenariusza przez tworzenie różnych `packages.config` plików dla różnych plików projektu specyficznych dla platformy.

![Wiele plików Package. config](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Powrót do lokalnej pamięci podręcznej

Chociaż pakiety NuGet są zwykle używane z galerii zdalnej, takiej jak [Galeria NuGet](http://www.nuget.org/) przy użyciu połączenia sieciowego, istnieje wiele scenariuszy, w których klient nie jest połączony. Bez połączenia sieciowego klient NuGet nie mógł pomyślnie zainstalować pakietów — nawet wtedy, gdy te pakiety znajdowały się już na komputerze klienta w lokalnej pamięci podręcznej NuGet. Pakiet NuGet 2,8 dodaje automatyczną rezerwę pamięci podręcznej do konsoli Menedżera pakietów. Na przykład podczas odłączania karty sieciowej i instalowania platformy jQuery konsola programu wyświetla następujące elementy:

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

Funkcja rezerwy pamięci podręcznej nie wymaga żadnych argumentów polecenia. Ponadto rezerwa pamięci podręcznej obecnie działa tylko w konsoli Menedżera pakietów — zachowanie aktualnie nie działa w oknie dialogowym Menedżera pakietów.

## <a name="webmatrix-nuget-client-updates"></a>Aktualizacje klienta NuGet w programie WebMatrix

Wraz z pakietem NuGet 2,8 rozszerzenie NuGet dla programu WebMatrix zostało także zaktualizowane w taki sposób, aby zawierało wiele głównych funkcji dostarczanych z pakietem [nuget 2,5](../release-notes/nuget-2.5.md). Nowe możliwości obejmują takie elementy, jak "Update All", "minimalna wersja NuGet" i Zezwalanie na zastępowanie plików zawartości.

Aby zaktualizować rozszerzenie Menedżera pakietów NuGet w programie WebMatrix 3:

1. Otwórz WebMatrix 3
1. Kliknij ikonę rozszerzenia na Wstążce
1. Wybierz kartę aktualizacje
1. Kliknij, aby zaktualizować Menedżera pakietów NuGet do 2.5.0
1. Zamknij i uruchom ponownie aplikację WebMatrix 3

Jest to pierwsza wersja rozszerzenia Menedżera pakietów NuGet w programie WebMatrix.  Kod został ostatnio wniesiony przez firmę Microsoft do projektu NuGet Open Source. Wcześniej integracja NuGet została wbudowana w Program WebMatrix i nie można jej zaktualizować poza pasmem z programu WebMatrix.  Teraz możemy zaktualizować go wraz z pozostałą częścią narzędzi klienckich narzędzia NuGet.

## <a name="bug-fixes"></a>Poprawki błędów

Jeden z najważniejszych poprawek błędów został ulepszony w poleceniu Update-Package-install.

Oprócz tych funkcji i wyżej wymienionej poprawki wydajności ta wersja programu NuGet zawiera również wiele innych poprawek błędów. W wydaniu wystąpiło 181 całkowite problemy rozwiązane. Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 2,8, zobacz [Śledzenie problemów NuGet dla tej wersji](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
