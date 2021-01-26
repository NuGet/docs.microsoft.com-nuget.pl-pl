---
title: Informacje o wersji narzędzia NuGet 2,5
description: Informacje o wersji programu NuGet 2,5, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: efcfb9767772c9e27372b4616f817656d51efed8
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776853"
---
# <a name="nuget-25-release-notes"></a>Informacje o wersji narzędzia NuGet 2,5

Informacje o wersji pakietu [NuGet 2.2.1](../release-notes/nuget-2.2.1.md)  |  [Informacje o wersji narzędzia NuGet 2,6](../release-notes/nuget-2.6.md)

Pakiet NuGet 2,5 został wydaną 25 kwietnia 2013. Ta wersja była bardzo duża, dlatego warto pominąć wersje 2,3 i 2,4. To jest największa wersja pakietu NuGet z ponad [160 elementami roboczymi](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) w wersji.

## <a name="acknowledgements"></a>Podziękowania

Chcemy podziękowanie następujących zewnętrznych współautorom w celu uzyskania znaczących wkładów do programu NuGet 2,5:

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ( [@dsplaisted](https://twitter.com/dsplaisted) )
    - [#2847](https://nuget.codeplex.com/workitem/2847) — Dodaj do listy znanych identyfikatorów platformy docelowej systemy Android i platformy monomac, a także opcję z nich.
2. [Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ( [@knocte](https://twitter.com/knocte) )
    - [#2865](https://nuget.codeplex.com/workitem/2865) — poprawianie pisowni `NuGet.targets` dla systemu operacyjnego uwzględniającego wielkość liter
3. [David Fowlera](https://www.codeplex.com/site/users/view/dfowler) ( [@davidfowl](https://twitter.com/davidfowl) )
    - Utwórz rozwiązanie na mono.
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ( [@atheken](https://twitter.com/atheken) )
    - Napraw testy jednostkowe zakończone niepowodzeniem na mono.
5. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ( [@OliIsCool](https://twitter.com/oliiscool) )
    - polecenie [#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe Pack nie propaguje właściwości do programu MSBuild
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ( [@bajtos](https://twitter.com/bajtos) )
    - [#1511](https://nuget.codeplex.com/workitem/1511) -zmodyfikowano kod obsługi XML, aby zachować formatowanie.
7. [Adam pracownik2](http://www.codeplex.com/site/users/view/adamralph) ( [@adamralph](https://twitter.com/adamralph) )
    - Dodano rozpoznane wyrazy do słownika niestandardowego, aby zezwolić programowi Build. cmd na pomyślne zakończenie.
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Napraw testy jednostkowe w przypadku uruchamiania w lokalizacji zlokalizowanej i
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - Wyodrębniony interfejs z PackageService
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ( [@brugidou](https://twitter.com/brugidou) )
     - [#936](https://nuget.codeplex.com/workitem/936) — obsługa zależności projektu podczas pakowania
11. [Xavier](https://www.codeplex.com/site/users/view/XavierDecoster) ( [@XavierDecoster](https://twitter.com/xavierdecoster) )
     - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) — obsługa hasła czystego tekstu podczas zapisywania poświadczeń źródła pakietu w plikach NuGet. cofig
12. [Odłogi](http://www.codeplex.com/site/users/view/jmanning) ( [@manningj](https://twitter.com/manningj) )
     - [#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -Fix Get-Package opis pomocy

Doceniamy również następujące osoby do znajdowania usterek z pakietem NuGet 2,5 beta/RC, które zostały zatwierdzone i naprawione przed ostateczną wersją:

1. [Ścianka której należy Tony](https://www.codeplex.com/site/users/view/CodeChief) ( [@CodeChief](https://twitter.com/codechief) )
    - [#3200](https://nuget.codeplex.com/workitem/3200) -MSTest przerwany z ostatnimi kompilacjami NuGet 2,4 i 2,5

## <a name="notable-features-in-the-release"></a>Istotne funkcje w wersji

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Zezwalaj użytkownikom na zastępowanie już istniejących plików zawartości

Jedną z najbardziej pożądanych funkcji całego czasu było możliwość zastępowania plików zawartości, które już istnieją na dysku, gdy są zawarte w pakiecie NuGet. Począwszy od programu NuGet 2,5, te konflikty są identyfikowane i zostanie wyświetlony monit o zastąpienie plików, podczas gdy wcześniej te pliki były zawsze pomijane.

![Zastąp pliki zawartości](./media/NuGet-2.5/overwrite-file.png)

Elementy "nuget.exe Update" i "Install-Package" teraz mają nową opcję "-FileConflictAction", aby ustawić niektóre wartości domyślne dla scenariuszy wiersza polecenia.

Ustaw domyślną akcję, gdy plik z pakietu już istnieje w projekcie docelowym. Ustaw wartość "Zastąp", aby zawsze zastępować pliki. Ustaw na wartość "Ignoruj", aby pominąć pliki. Jeśli nie zostanie określony, zostanie wyświetlony monit o podanie każdego pliku powodującego konflikt.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>Automatyczne Importowanie elementów docelowych programu MSBuild i plików props

Nowy konwencjonalny folder został utworzony na najwyższym poziomie pakietu NuGet.  Jako element równorzędny do `\lib` , `\content` , i `\tools` , możesz teraz dołączyć `\build` folder do pakietu.  W tym folderze można umieścić dwa pliki o stałych nazwach `{packageid}.targets` lub `{packageid}.props` . Te dwa pliki mogą znajdować się bezpośrednio w folderze `build` lub w obszarze folderów specyficznych dla platformy, podobnie jak w przypadku innych folderów. Reguła wybierania najlepszego dopasowanego folderu struktury jest dokładnie taka sama jak w przypadku tych.

Gdy narzędzie NuGet zainstaluje pakiet z plikami \Build, doda element programu MSBuild `<Import>` w pliku projektu wskazujący `.targets` `.props` pliki i. `.props`Plik zostanie dodany u góry, natomiast `.targets` plik zostanie dodany na końcu.

### <a name="specify-different-references-per-platform-using-references-element"></a>Określ różne odwołania na platformę przy użyciu `<References/>` elementu

Przed 2,5, w `.nuspec` pliku, użytkownik może określić tylko pliki referencyjne, które mają być dodane do wszystkich platform. Teraz dzięki tej nowej funkcji w 2,5, użytkownik może utworzyć `<reference/>` element dla każdej z obsługiwanych platform, na przykład:

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

Oto przepływ, dla którego NuGet dodaje odwołania do projektów opartych na `.nuspec` pliku:

1. Znajdź `lib` folder, który jest odpowiedni dla platformy docelowej, i Pobierz listę zestawów z tego folderu
1. Oddzielnie Znajdź grupę odwołania, która jest odpowiednia dla platformy docelowej i Pobierz listę zestawów z tej grupy. Grupa odwołania bez określonej platformy docelowej jest grupą rezerwową.
1. Znajdź część wspólną dwóch list i użyj jej jako odwołań do dodania

Ta nowa funkcja umożliwi autorom pakietów używanie funkcji odwołań do stosowania podzestawów zestawów w różnych strukturach, gdy w przeciwnym razie konieczne będzie przeprowadzenie zduplikowanych zestawów w wielu `lib` folderach.

Uwaga: Aby korzystać z tej funkcji, musisz użyć pakietu nuget.exe Pack; Eksplorator pakietów NuGet jeszcze go nie obsługuje.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Przycisk Aktualizuj wszystko, aby zezwolić na jednoczesną aktualizację wszystkich pakietów

Wiele informacji na temat polecenia cmdlet programu PowerShell "Update-Package" w celu zaktualizowania wszystkich pakietów jest możliwe. Teraz można łatwo wykonać tę czynność za pomocą interfejsu użytkownika.

Aby wypróbować tę funkcję:

1. tworzenie nowej aplikacji platformy ASP.NET MVC
1. Uruchom okno dialogowe Zarządzanie pakietami NuGet
1. Wybierz pozycję "aktualizacje"
1. Kliknij przycisk "Aktualizuj wszystko"

![Przycisk Aktualizuj wszystko w oknie dialogowym](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Ulepszona obsługa odwołań projektu dla pakietu nuget.exe

Teraz nuget.exe pakiety poleceń pakietów, do których odwołują się projekty z następującymi regułami:

1. Jeśli przywoływany projekt ma odpowiedni `.nuspec` plik, na przykład plik o nazwie `proj1.nuspec` w tym samym folderze co `proj1.csproj` , ten projekt jest dodawany jako zależność do pakietu, przy użyciu identyfikatora i wersji Odczytaj z `.nuspec` pliku.
1. W przeciwnym razie pliki projektu, do którego istnieje odwołanie, są powiązane z pakietem. Następnie projekty, do których odwołuje się ten projekt, zostaną przetworzone cyklicznie przy użyciu tych samych reguł.
1. `.pdb`Dodawane są wszystkie pliki dll, i `.exe` .
1. Wszystkie inne pliki zawartości są dodawane.
1. Wszystkie zależności są scalane.

Dzięki temu projekt, do którego istnieje odwołanie, może być traktowany jako zależność, jeśli istnieje `.nuspec` plik, jest częścią pakietu.

Więcej szczegółów znajduje się tutaj: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>Dodaj właściwość "minimalna wersja NuGet" do pakietów

Nowy atrybut metadanych o nazwie "minClientVersion" może teraz wskazywać minimalną wersję klienta NuGet wymaganą do korzystania z pakietu.

Ta funkcja pomaga autorowi pakietu określić, że pakiet będzie działał tylko po określonej wersji programu NuGet. `.nuspec`Po dodaniu nowych funkcji programu nuget 2,5 pakiety będą mogły przejąć minimalną wersję narzędzia NuGet.

```xml
<metadata minClientVersion="2.6">
```

Jeśli użytkownik ma zainstalowaną program NuGet 2,5, a pakiet jest identyfikowany jako wymagający 2,6, podpowiedzi wizualne zostaną przekazane Użytkownikowi wskazującym, że pakiet nie zostanie zainstalowany. Użytkownik będzie następnie mógł zaktualizować swoją wersję programu NuGet.

Poprawi to istniejące środowisko, w którym rozpocznie się instalacja pakietów, ale kończy się niepowodzeniem wskazujących, że zidentyfikowano nierozpoznaną wersję schematu.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>Zależności nie są już niepotrzebne do aktualizacji podczas instalacji pakietu

Przed pakietem NuGet 2,5, podczas instalowania pakietu, który jest zależny od pakietu już zainstalowanego w projekcie, zależność zostanie zaktualizowana w ramach nowej instalacji, nawet jeśli istniejąca wersja spełnia tę zależność.

Począwszy od programu NuGet 2,5, jeśli wersja zależności jest już spełniona, zależność nie zostanie zaktualizowana podczas innych instalacji pakietu.

**Scenariusz:**

1. Repozytorium źródłowe zawiera pakiet B z wersjami 1.0.0 i 1.0.2. Zawiera również pakiet A, który ma zależność od B (>= 1.0.0).
1. Załóżmy, że bieżący projekt ma już zainstalowany pakiet B w wersji 1.0.0. Teraz chcesz zainstalować pakiet A.

**W programie NuGet 2,2 i starszych:**

* Podczas instalowania pakietu A pakiet NuGet aktualizuje aktualizację B do 1.0.2, nawet jeśli istniejąca wersja 1.0.0 już spełnia ograniczenie wersji zależności, czyli >= 1.0.0.

**W programie NuGet 2,5 i nowszych:**

* Pakiet NuGet nie zostanie już zaktualizowany B, ponieważ wykryje, że istniejąca wersja 1.0.0 spełnia ograniczenie wersji zależności.

Aby uzyskać więcej informacji na temat tej zmiany, przeczytaj szczegółowy [element roboczy](http://nuget.codeplex.com/workitem/1681) oraz powiązany [wątek dyskusji](http://nuget.codeplex.com/discussions/436712).

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>nuget.exe wyprowadza żądania HTTP z szczegółowym szczegółowośćem

W przypadku rozwiązywania problemów nuget.exe lub po prostu chcesz wiedzieć, jakie żądania HTTP są wykonywane podczas operacji, przełącznik "-verbose Szczegółowa" spowoduje teraz wyjściu wszystkie żądania HTTP.

![Dane wyjściowe HTTP z nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>nuget.exe push obsługuje teraz źródła UNC i folderów

Przed pakietem NuGet 2,5, Jeśli podjęto próbę uruchomienia "nuget.exe wypychania" do źródła pakietu na podstawie ścieżki UNC lub folderu lokalnego, wypchnięcie nie powiedzie się. W przypadku ostatnio dodanej funkcji konfiguracji hierarchicznej staje się ona wspólna dla nuget.exe musi być ścieżką UNC/folderem źródłowym lub galerią NuGet opartą na protokole HTTP.

Począwszy od programu NuGet 2,5, jeśli nuget.exe identyfikuje źródło UNC/folder, wykona kopię pliku do źródła.

Następujące polecenie będzie teraz działało:

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>nuget.exe obsługuje jawnie określone pliki konfiguracji

nuget.exe polecenia, które uzyskują dostęp do konfiguracji (wszystkie z wyjątkiem "spec" i "Pack"), teraz obsługują nową opcję "-ConfigFile", która wymusza użycie określonego pliku konfiguracji zamiast domyślnego pliku konfiguracyjnego w lokalizacji% AppData% \nuget\Nuget.Config.

Przykład:

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>Obsługa projektów natywnych

W przypadku programu NuGet 2,5 narzędzia NuGet są teraz dostępne dla natywnych projektów w programie Visual Studio. Oczekujemy, że większość natywnych pakietów będzie korzystać z funkcji importów MSBuild powyżej, przy użyciu narzędzia utworzonego przez [projekt CoApp](http://coapp.org). Aby uzyskać więcej informacji, zapoznaj [się ze szczegółowymi informacjami o narzędziu](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) w witrynie coapp.org.

Nazwa platformy docelowej "native" została wprowadzona dla pakietów do dołączania plików w \Build, \Content i \Tools, gdy pakiet jest zainstalowany w projekcie natywnym.  \`Folder lib nie jest używany dla projektów natywnych.
