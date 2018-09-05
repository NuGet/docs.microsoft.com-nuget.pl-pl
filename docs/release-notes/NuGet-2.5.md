---
title: Informacje o wersji 2,5 NuGet
description: Informacje o wersji programu NuGet 2.5, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 29d0b33714a574281680e110b967269699afbaf1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550486"
---
# <a name="nuget-25-release-notes"></a>Informacje o wersji 2,5 NuGet

[Informacje o wersji NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [informacjach o wersji NuGet 2.6](../release-notes/nuget-2.6.md)

25 kwietnia 2013 został wydany NuGet 2.5. Ta wersja została tak dużych, będziemy mieli świadomość zmuszony do pominięcia w wersji 2.3 i 2.4! Do tej pory, to najprawdopodobniej największe wydanie, już od dłuższego NuGet, za pomocą za pośrednictwem [elementów roboczych 160](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) w wersji.

## <a name="acknowledgements"></a>Potwierdzanie

Chcielibyśmy podziękować następujące współautorów zewnętrznych dla ich znaczny wkład do NuGet 2.5:

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) — Dodaj MonoAndroid MonoTouch i platformy MonoMac do listy znanych target framework identyfikatorów.
2. [Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) -napraw pisownię `NuGet.targets` dla liter systemu operacyjnego
3. [David Fowlera](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Należy to rozwiązanie kompilacji na platformy Mono.
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Usuń testy jednostkowe, które kończy się niepowodzeniem w Mono.
5. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) — polecenie Pakiet nuget.exe nie propaguje właściwości programu MSBuild
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#1511](https://nuget.codeplex.com/workitem/1511) — zmodyfikowane pliki XML kodu obsługującego Zachowaj formatowanie.
7. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - Dodano rozpoznane słowa do słownika niestandardowego, aby umożliwić build.cmd zakończyło się sukcesem.
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Usuń testy jednostkowe, podczas uruchamiania w programie VS zlokalizowane.
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - Interfejs wyodrębnione z PackageService
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
     - [#936](https://nuget.codeplex.com/workitem/936) — Obsługa zależności projektu podczas pakowania
11. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
     - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) — Obsługa wyczyść tekst hasła, kiedy przechowywanie poświadczeń źródła pakietu w plikach nuget.cofig
12. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
     - [#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -napraw Get-help Opis pakietu

Doceniamy również następujące osoby do wyszukiwania usterek za pomocą NuGet 2.5 wersji Beta lub RC, które zostały zatwierdzone i rozwiązane przed ostatecznym wydaniem:

1. [Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) — MSTest uszkodzenie Najpóźniejsza NuGet 2.4 i 2,5 kompilacji

## <a name="notable-features-in-the-release"></a>Ważne funkcje w wersji

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Zezwalaj użytkownikom na zastąpienie plików zawartości, które już istnieją

Jedną z najbardziej pożądanych funkcji cały czas został możliwości zastępowania plików zawartości, które już istnieją na dysku, gdy włączone do pakietu NuGet. Począwszy od wersji 2.5 NuGet są identyfikowane te konflikty i zostanie wyświetlony monit o zastąpienie plików, należy wcześniej te pliki były zawsze pominięte.

![Zastąp pliki zawartości](./media/NuGet-2.5/overwrite-file.png)

"Aktualizacja nuget.exe" i "Install-Package" teraz zarówno istnieje nowa opcja "-FileConflictAction" można ustawić niektórych wartość domyślna dla scenariuszy z wiersza polecenia.

Domyślna akcja należy ustawić, gdy plik z pakietu już istnieje w projekcie docelowego. Ustawienie "Zastąp" zawsze mają pierwszeństwo przed plików. Ustawienie "Ignore" Pomiń pliki. Jeśli nie zostanie określony, pojawi się monit o każdego pliku powodującego konflikt.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>Automatyczne importowanie MSBuild cele i pliki właściwości

Nowy folder konwencjonalne został utworzony na najwyższym poziomie pakietu NuGet.  Jako element równorzędny do `\lib`, `\content`, i `\tools`, obecnie możesz uwzględniać `\build` folder w pakiecie.  W tym folderze można umieścić dwa pliki z nazwami stały `{packageid}.targets` lub `{packageid}.props`. Te dwa pliki mogą być bezpośrednio w obszarze `build` lub równy podanemu właściwa dla struktury folderów, podobnie jak inne foldery. Reguły dla folder struktury najlepiej dopasowany do pobrania jest dokładnie taka sama, jak te.

Podczas instalowania pakietu z plikami \build NuGet doda MSBuild `<Import>` elementu w pliku projektu, wskazując `.targets` i `.props` plików. `.props` Plik zostanie dodany u góry strony, natomiast `.targets` plik zostanie dodany do dołu.

### <a name="specify-different-references-per-platform-using-references-element"></a>Określ różne odwołania na platformie za pomocą `<References/>` — element

Przed 2.5 w `.nuspec` pliku użytkownika można określić tylko plików źródłowych, ma zostać dodana dla wszystkich framework. Teraz dzięki tej nowej funkcji w wersji 2.5 użytkownika można tworzyć `<reference/>` elementu dla każdego z obsługiwanych platform, na przykład:

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

Poniżej przedstawiono przepływ dla jak NuGet dodaje odwołania do projektów na podstawie `.nuspec` pliku:

1. Znajdź `lib` folder, który jest odpowiedni dla platformy docelowej i Uzyskaj listę zestawów z tego folderu
1. Oddzielnie znaleźć grupy odwołania, który jest odpowiedni dla platformy docelowej i Uzyskaj listę zestawów z tej grupy. Grupa odwołań bez określona lokalizacja docelowa jest to grupa rezerwowego.
1. Znajdź część wspólną dwóch list i używać go jako odwołania do dodania

Ta nowa funkcja umożliwi autorom pakietów korzystać z funkcji odwołania do zastosowania podzbiór zestawów do różnych platform, gdy byłby normalnie potrzebny do przenoszenia zduplikowane zestawów w wielu `lib` folderów.

Uwaga: należy obecnie używasz nuget.exe pakietu można korzystać z tej funkcji; Eksplorator pakietów NuGet nie obsługuje jeszcze je.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Aktualizuj wszystkie przycisk umożliwia aktualizowanie jednocześnie wszystkie pakiety

Wiele osób wiedzieć o polecenia cmdlet programu PowerShell "Pakiet aktualizacji" można zaktualizować wszystkich pakietów; teraz jest prosty sposób, aby to zrobić przy użyciu interfejsu użytkownika w także.

Aby wypróbować tę funkcję:

1. Tworzenie nowej aplikacji platformy ASP.NET MVC
1. Uruchom okno dialogowe "Zarządzaj pakietami NuGet"
1. Wybierz opcję "Aktualizacje"
1. Kliknij przycisk "Aktualizuj wszystkie"

![Aktualizuj wszystkie przycisk w oknie dialogowym](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Ulepszony projekt odwołania obsługę nuget.exe pakietu

Teraz procesy polecenia programu nuget.exe pakiet przywoływane projekty z następującymi regułami:

1. Jeśli przywoływany projekt ma odpowiadające `.nuspec` pliku, np. istnieje plik o nazwie `proj1.nuspec` w tym samym folderze co `proj1.csproj`, następnie ten projekt zostanie dodany jako zależność do pakietu przy użyciu identyfikatora i odczytywać wersji `.nuspec` pliku.
1. W przeciwnym razie pliki przywoływanego projektu są powiązane w pakiecie. Następnie projekty przywoływane przez ten projekt zostanie przetworzone przy użyciu sames rekursywnie reguły.
1. Wszystkie biblioteki DLL, `.pdb`, i `.exe` pliki zostaną dodane.
1. Wszystkie pliki zawartości są dodawane.
1. Wszystkie zależności są scalane.

Dzięki temu przywoływanego projektu powinien być traktowany jako zależność, jeśli istnieje `.nuspec` pliku, w przeciwnym razie staje się częścią pakietu.

Szczegółowe informacje w tym miejscu: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>Dodawanie właściwości Minimum NuGet wersji do pakietów

Nowy atrybut metadanych o nazwie "atrybut minClientVersion" teraz może wskazywać minimalna wersja klienta NuGet wymagana do korzystania z pakietu.

Ta funkcja pomaga autorem pakietu, aby określić, że pakiet będą działać dopiero po określonej wersji pakietu NuGet. Jako nowe `.nuspec` funkcje są dodawane po NuGet 2.5, pakietów będą mogli oświadczenia minimalnej wersji NuGet.

```xml
<metadata minClientVersion="2.6">
```

Jeśli użytkownik ma 2.5 NuGet zainstalowany pakiet jest identyfikowany jako wymagające 2.6, otrzymają podpowiedzi wizualne dla użytkownika, wskazujący, że pakiet nie będzie możliwe do zainstalowania. Użytkownika zostaną następnie przekierowani do zaktualizowania ich wersji pakietu nuget.

Pozwoli to udoskonalić od istniejącego środowiska, gdzie rozpocząć pakiety do instalacji, ale następnie nie, wskazujący, że została zidentyfikowana Nierozpoznana wersja schematu.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>Zależności nie są już niepotrzebnie są aktualizowane podczas instalacji pakietu aktualizacji

Przed NuGet 2.5 podczas instalowania pakietu, zależne od pakietu już zainstalowany w projekcie, zależność będzie można zaktualizować w ramach nowej instalacji, nawet jeśli istniejąca wersja spełniła zależność.

Zaczynając od NuGet 2.5, jeśli wersja zależności już jest spełniony, zależność nie zostanie zaktualizowany w inne instalacje pakietu.

**Scenariusz:**

1. Repozytorium źródłowe zawiera pakiet B w wersji 1.0.0 i 1.0.2. Zawiera ona także pakiet element, który ma zależność od B (> = 1.0.0).
1. Załóżmy, że bieżący projekt ma już pakiet B w wersji 1.0.0 zainstalowane. Teraz chcesz zainstalować pakiet A.

**W pakiecie NuGet 2,2 i starszych:**

* Podczas instalowania pakietu A, NuGet automatycznie zaktualizuje B 1.0.2, nawet jeśli istniejąca wersja 1.0.0 spełnia już ograniczenie wersji zależności, który jest > = 1.0.0.

**W pakiecie NuGet 2.5 lub nowszej:**

* NuGet nie są już zaktualizuje B, ponieważ wykrywa, że istniejąca wersja 1.0.0 spełnia ograniczenie wersji zależności.

Aby uzyskać więcej ogólnych informacji na temat tej zmiany, przeczytaj szczegółowe [elementu roboczego](http://nuget.codeplex.com/workitem/1681) oraz powiązane [wątek dyskusji](http://nuget.codeplex.com/discussions/436712).

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>nuget.exe wysyła żądania http z szczegółowy poziom szczegółowości

Jeśli rozwiązujesz nuget.exe lub po prostu zastanawiasz się, jakie żądania HTTP są wykonywane podczas wykonywania operacji "— szczegółowy poziom szczegółowości" przełącznika teraz zwróci wszystkie żądania HTTP.

![Dane wyjściowe HTTP nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>wypychane nuget.exe obsługuje teraz źródeł UNC i folderów

Przed NuGet 2.5 Jeśli próbujesz uruchomić "nuget.exe push" do źródła pakietu na podstawie ścieżki UNC lub lokalny folder wypychania może zakończyć się niepowodzeniem. Dzięki funkcji ostatnio dodane hierarchiczne konfiguracji stało się typowe narzędzia nuget.exe muszą źródła UNC/folderu lub galerii pakietów NuGet oparty na protokole HTTP.

Zaczynając od NuGet 2.5, jeśli nuget.exe identyfikuje źródła UNC lub folder, zostanie przeprowadzone kopiowania plików do źródła.

Następujące polecenie będzie teraz działać:

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>nuget.exe obsługuje jawnie określone pliki konfiguracji

polecenia nuget.exe, uzyskujących dostęp do konfiguracji (wszystkie z wyjątkiem "Specyfikacja" i "pack"), teraz obsługują nową "-ConfigFile" opcja, która wymusza pliku określonej konfiguracji, ma być używany zamiast domyślnego pliku konfiguracji % AppData%\nuget\Nuget.Config.

Przykład:

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>Obsługa natywnych projektów

Za pomocą NuGet 2.5 narzędzia NuGet jest teraz dostępna w przypadku natywnych projektów w programie Visual Studio. Oczekujemy, że najbardziej pakiety natywne korzystanie z funkcji Importy MSBuild powyżej, za pomocą narzędzia utworzone przez [projektu CoApp](http://coapp.org). Aby uzyskać więcej informacji, przeczytaj [szczegółowe informacje o narzędziu](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) w witrynie sieci Web coapp.org.

Nazwa docelowego framework "native" został wprowadzony dla pakietów, które mają zostać objęte pliki \build \content i \tools po zainstalowaniu pakietu do natywnego projektu.  \`Lib "folder nie jest używany do natywnych projektów.
