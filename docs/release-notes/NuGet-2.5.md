---
title: Informacje o wersji narzędzia NuGet 2,5
description: Informacje o wersji programu NuGet 2,5, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940582d5173f5a53dcd04cf1258fc02a2439af4e
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825283"
---
# <a name="nuget-25-release-notes"></a>Informacje o wersji narzędzia NuGet 2,5

[Informacje o wersji pakietu NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [Informacje o wersji narzędzia NuGet 2,6](../release-notes/nuget-2.6.md)

Pakiet NuGet 2,5 został wydaną 25 kwietnia 2013. Ta wersja była bardzo duża, dlatego warto pominąć wersje 2,3 i 2,4. To jest największa wersja pakietu NuGet z ponad [160 elementami roboczymi](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) w wersji.

## <a name="acknowledgements"></a>Podziękowania

Chcemy podziękowanie następujących zewnętrznych współautorom w celu uzyskania znaczących wkładów do programu NuGet 2,5:

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) — Dodaj do listy znanych identyfikatorów platformy docelowej systemy Android i platformy monomac, a także opcję z nich.
2. [Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) — poprawianie pisowni `NuGet.targets` dla systemu operacyjnego uwzględniającego wielkość liter
3. [David Fowlera](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Utwórz rozwiązanie na mono.
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Napraw testy jednostkowe zakończone niepowodzeniem na mono.
5. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) — polecenie pakietu NuGet. exe nie propaguje właściwości do programu MSBuild
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#1511](https://nuget.codeplex.com/workitem/1511) -zmodyfikowano kod obsługi XML, aby zachować formatowanie.
7. [Adam](http://www.codeplex.com/site/users/view/adamralph) : ([@adamralph](https://twitter.com/adamralph))
    - Dodano rozpoznane wyrazy do słownika niestandardowego, aby zezwolić programowi Build. cmd na pomyślne zakończenie.
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Napraw testy jednostkowe w przypadku uruchamiania w lokalizacji zlokalizowanej i
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - Wyodrębniony interfejs z PackageService
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
     - [#936](https://nuget.codeplex.com/workitem/936) — obsługa zależności projektu podczas pakowania
11. [Xavier](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
     - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) — obsługa hasła czystego tekstu podczas zapisywania poświadczeń źródła pakietu w plikach NuGet. cofig
12. [Odłogi](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
     - [#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) — opis pomocy Get-Package

Doceniamy również następujące osoby do znajdowania usterek z pakietem NuGet 2,5 beta/RC, które zostały zatwierdzone i naprawione przed ostateczną wersją:

1. [Której należy Tony](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) -MSTest przerwany z ostatnimi kompilacjami NuGet 2,4 i 2,5

## <a name="notable-features-in-the-release"></a>Istotne funkcje w wersji

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Zezwalaj użytkownikom na zastępowanie już istniejących plików zawartości

Jedną z najbardziej pożądanych funkcji całego czasu było możliwość zastępowania plików zawartości, które już istnieją na dysku, gdy są zawarte w pakiecie NuGet. Począwszy od programu NuGet 2,5, te konflikty są identyfikowane i zostanie wyświetlony monit o zastąpienie plików, podczas gdy wcześniej te pliki były zawsze pomijane.

![Zastąp pliki zawartości](./media/NuGet-2.5/overwrite-file.png)

plik "NuGet. exe Update" i "Install-Package" teraz mają nową opcję "-FileConflictAction", aby ustawić niektóre domyślne dla scenariuszy wiersza polecenia.

Ustaw domyślną akcję, gdy plik z pakietu już istnieje w projekcie docelowym. Ustaw wartość "Zastąp", aby zawsze zastępować pliki. Ustaw na wartość "Ignoruj", aby pominąć pliki. Jeśli nie zostanie określony, zostanie wyświetlony monit o podanie każdego pliku powodującego konflikt.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>Automatyczne Importowanie elementów docelowych programu MSBuild i plików props

Nowy konwencjonalny folder został utworzony na najwyższym poziomie pakietu NuGet.  Jako element równorzędny do `\lib`, `\content`i `\tools`możesz teraz dołączyć folder `\build` do pakietu.  W tym folderze można umieścić dwa pliki o stałych nazwach, `{packageid}.targets` lub `{packageid}.props`. Te dwa pliki mogą znajdować się bezpośrednio w obszarze `build` lub w folderach specyficznych dla platformy, podobnie jak w przypadku innych folderów. Reguła wybierania najlepszego dopasowanego folderu struktury jest dokładnie taka sama jak w przypadku tych.

Gdy narzędzie NuGet zainstaluje pakiet z plikami \Build, spowoduje dodanie elementu `<Import>` MSBuild w pliku projektu wskazującego pliki `.targets` i `.props`. Plik `.props` zostanie dodany u góry, natomiast plik `.targets` zostanie dodany na końcu.

### <a name="specify-different-references-per-platform-using-references-element"></a>Określ różne odwołania na platformę przy użyciu elementu `<References/>`

Przed 2,5, w pliku `.nuspec`, użytkownik może określić tylko pliki referencyjne, które mają być dodane do wszystkich platform. Teraz dzięki tej nowej funkcji w 2,5 można utworzyć element `<reference/>` dla każdej z obsługiwanych platform, na przykład:

```xml
<references>
    <group targetFramework="net45">
        <reference file="a.dll" />
    </group>
    <group targetFramework="netcore45">
        <reference file="b.dll" />
    </group>
    <group>
        <reference file="c.dll" />
    </group>
</references>
```

Oto przepływ, dla którego NuGet dodaje odwołania do projektów opartych na pliku `.nuspec`:

1. Znajdź folder `lib`, który jest odpowiedni dla platformy docelowej, i Pobierz listę zestawów z tego folderu
1. Oddzielnie Znajdź grupę odwołania, która jest odpowiednia dla platformy docelowej i Pobierz listę zestawów z tej grupy. Grupa odwołania bez określonej platformy docelowej jest grupą rezerwową.
1. Znajdź część wspólną dwóch list i użyj jej jako odwołań do dodania

Ta nowa funkcja umożliwi autorom pakietów używanie funkcji odwołań do stosowania podzestawów zestawów w różnych strukturach, gdy w przeciwnym razie konieczne będzie przeprowadzenie zduplikowanych zestawów w wielu `lib` folderach.

Uwaga: Aby korzystać z tej funkcji, musisz używać pakietu NuGet. exe Pack; Eksplorator pakietów NuGet jeszcze go nie obsługuje.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Przycisk Aktualizuj wszystko, aby zezwolić na jednoczesną aktualizację wszystkich pakietów

Wiele informacji na temat polecenia cmdlet programu PowerShell "Update-Package" w celu zaktualizowania wszystkich pakietów jest możliwe. Teraz można łatwo wykonać tę czynność za pomocą interfejsu użytkownika.

Aby wypróbować tę funkcję:

1. Tworzenie nowej aplikacji platformy ASP.NET MVC
1. Uruchom okno dialogowe Zarządzanie pakietami NuGet
1. Wybierz pozycję "aktualizacje"
1. Kliknij przycisk "Aktualizuj wszystko"

![Przycisk Aktualizuj wszystko w oknie dialogowym](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Ulepszona obsługa odwołań do projektu dla pakietu NuGet. exe

Teraz pakiet poleceń NuGet. exe Pack przetwarza odwołania do projektów z następującymi regułami:

1. Jeśli przywoływany projekt ma odpowiedni plik `.nuspec`, na przykład plik o nazwie `proj1.nuspec` w tym samym folderze co `proj1.csproj`, ten projekt zostanie dodany jako zależność do pakietu, przy użyciu identyfikatora i wersji odczytanego z pliku `.nuspec`.
1. W przeciwnym razie pliki projektu, do którego istnieje odwołanie, są powiązane z pakietem. Następnie projekty, do których odwołuje się ten projekt, zostaną przetworzone cyklicznie przy użyciu tych samych reguł.
1. Dodawane są wszystkie pliki DLL, `.pdb`i `.exe`.
1. Wszystkie inne pliki zawartości są dodawane.
1. Wszystkie zależności są scalane.

Dzięki temu projekt, do którego istnieje odwołanie, może być traktowany jako zależność, jeśli istnieje plik `.nuspec`, w przeciwnym razie stał się częścią pakietu.

Więcej szczegółów znajduje się tutaj: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>Dodaj właściwość "minimalna wersja NuGet" do pakietów

Nowy atrybut metadanych o nazwie "minClientVersion" może teraz wskazywać minimalną wersję klienta NuGet wymaganą do korzystania z pakietu.

Ta funkcja pomaga autorowi pakietu określić, że pakiet będzie działał tylko po określonej wersji programu NuGet. Po dodaniu nowych funkcji `.nuspec` po wystąpieniu programu NuGet 2,5 pakiety będą mogły przejąć minimalną wersję narzędzia NuGet.

```xml
<metadata minClientVersion="2.6">
```

Jeśli użytkownik ma zainstalowaną program NuGet 2,5, a pakiet jest identyfikowany jako wymagający 2,6, podpowiedzi wizualne zostaną przekazane Użytkownikowi wskazującym, że pakiet nie zostanie zainstalowany. Użytkownik będzie następnie mógł zaktualizować swoją wersję programu NuGet.

Poprawi to istniejące środowisko, w którym rozpocznie się instalacja pakietów, ale kończy się niepowodzeniem wskazujących, że zidentyfikowano nierozpoznaną wersję schematu.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>Zależności nie są już niepotrzebne do aktualizacji podczas instalacji pakietu

Przed pakietem NuGet 2,5, podczas instalowania pakietu, który jest zależny od pakietu już zainstalowanego w projekcie, zależność zostanie zaktualizowana w ramach nowej instalacji, nawet jeśli istniejąca wersja spełnia tę zależność.

Począwszy od programu NuGet 2,5, jeśli wersja zależności jest już spełniona, zależność nie zostanie zaktualizowana podczas innych instalacji pakietu.

**Scenariusz:**

1. Repozytorium źródłowe zawiera pakiet B z wersjami 1.0.0 i 1.0.2. Zawiera również pakiet A, który ma zależność od B (> = 1.0.0).
1. Załóżmy, że bieżący projekt ma już zainstalowany pakiet B w wersji 1.0.0. Teraz chcesz zainstalować pakiet A.

**W programie NuGet 2,2 i starszych:**

* Podczas instalowania pakietu A pakiet NuGet aktualizuje aktualizację B do 1.0.2, nawet jeśli istniejąca wersja 1.0.0 już spełnia ograniczenie wersji zależności, czyli > = 1.0.0.

**W programie NuGet 2,5 i nowszych:**

* Pakiet NuGet nie zostanie już zaktualizowany B, ponieważ wykryje, że istniejąca wersja 1.0.0 spełnia ograniczenie wersji zależności.

Aby uzyskać więcej informacji na temat tej zmiany, przeczytaj szczegółowy [element roboczy](http://nuget.codeplex.com/workitem/1681) oraz powiązany [wątek dyskusji](http://nuget.codeplex.com/discussions/436712).

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>NuGet. exe wyprowadza żądania HTTP z szczegółowym szczegółowośćem

W przypadku rozwiązywania problemów z pakietem NuGet. exe lub po prostu chcesz wiedzieć, jakie żądania HTTP są wykonywane podczas operacji, przełącznik "-verbose Szczegółowa" spowoduje teraz wyjściu wszystkie żądania HTTP.

![Dane wyjściowe HTTP z NuGet. exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>Pakiet NuGet. exe push obsługuje teraz źródła UNC i folderów

Przed pakietem NuGet 2,5, Jeśli podjęto próbę uruchomienia polecenia "NuGet. exe push" jako źródła pakietu na podstawie ścieżki UNC lub folderu lokalnego, wypchnięcie zakończy się niepowodzeniem. W przypadku ostatnio dodanej funkcji konfiguracji hierarchicznej stał się ona wspólna dla programu NuGet. exe, aby mogła ona być docelowa dla źródła UNC/folderu lub Galerii pakietów NuGet opartych na protokole HTTP.

Począwszy od programu NuGet 2,5, jeśli plik NuGet. exe identyfikuje źródło UNC/folder, wykona kopię pliku do źródła.

Następujące polecenie będzie teraz działało:

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>NuGet. exe obsługuje jawnie określone pliki konfiguracji

polecenia NuGet. exe, które mają dostęp do konfiguracji (wszystkie z wyjątkiem "spec" i "Pack"), obsługują teraz nową opcję "-ConfigFile", która wymusza użycie określonego pliku konfiguracji zamiast domyślnego pliku konfiguracji w lokalizacji%AppData%\nuget\Nuget.Config.

Przykład:

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>Obsługa projektów natywnych

W przypadku programu NuGet 2,5 narzędzia NuGet są teraz dostępne dla natywnych projektów w programie Visual Studio. Oczekujemy, że większość natywnych pakietów będzie korzystać z funkcji importów MSBuild powyżej, przy użyciu narzędzia utworzonego przez [projekt CoApp](http://coapp.org). Aby uzyskać więcej informacji, zapoznaj [się ze szczegółowymi informacjami o narzędziu](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) w witrynie coapp.org.

Nazwa platformy docelowej "native" została wprowadzona dla pakietów do dołączania plików w \Build, \Content i \Tools, gdy pakiet jest zainstalowany w projekcie natywnym.  Folder \`lib nie jest używany dla projektów natywnych.
