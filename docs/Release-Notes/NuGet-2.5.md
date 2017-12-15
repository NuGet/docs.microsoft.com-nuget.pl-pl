---
title: Informacje o wersji NuGet 2.5 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: c193f1e3-d114-427f-9425-9930cc8e4db3
description: "Informacje o wersji 2.5 NuGet tym znanych problemów, poprawki, dodatkowe funkcje i dcr."
keywords: NuGet 2.5 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8d3bebbbe550645fcffad078538134427103cf98
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-25-release-notes"></a>Informacje o wersji 2,5 NuGet

[Informacje o wersji NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 informacje o wersji](../release-notes/nuget-2.6.md)

NuGet 2.5 został wydany 25 kwietnia 2013. Ta wersja została tak duży, możemy mieli świadomość zmuszony do pomijania w wersji 2.3 i 2.4! Data, to największy zlecenia, które zostały było programu NuGet, z za pośrednictwem [elementy robocze 160](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) w wersji.

## <a name="acknowledgements"></a>Potwierdzeń

Chcielibyśmy Dziękujemy następujące współautorzy zewnętrznych dla ich znaczących wkładów do NuGet 2.5:

1. [Danielowi Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) — Dodaj MonoAndroid, MonoTouch i MonoMac do listy znanych docelowej framework identyfikatorów.
1. [Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) -Popraw pisownię wyrazu `NuGet.targets` dla z uwzględnieniem wielkości liter systemu operacyjnego
1. [Dominik Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Należy kompilacji w jedno rozwiązanie.
1. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Napraw na Mono testów jednostkowych.
1. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) — polecenie Pakiet nuget.exe nie propaguje właściwości dla programu MSBuild
1. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#1511](https://nuget.codeplex.com/workitem/1511) — zmodyfikować XML kod obsługi Aby zachować formatowanie.
1. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - Rozpoznany wyrazy zostały dodane do słownika niestandardowego, aby umożliwić build.cmd powiodło się.
1. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Napraw testów jednostkowych w zlokalizowanej wersji programu VS.
1. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - Interfejs wyodrębnione z PackageService
1. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
    - [#936](https://nuget.codeplex.com/workitem/936) -obsługi zależności projektu podczas pakowania
1. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
    - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) — Obsługa Wyczyść hasła tekstu podczas zapisywania poświadczeń dostępu do źródła pakietu w plikach nuget.cofig
1. [Kuba Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
    - [#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -Get-Package Usuń opis pomocy

Dziękujemy następującym osobom również do znajdowania usterki z NuGet 2.5 Beta lub RC zatwierdzone i rozwiązać przed ostateczną wersją:

1. [Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) — MSTest przerwanie najnowsza NuGet 2.4 i tworzy 2,5

# <a name="notable-features-in-the-release"></a>Ważne funkcje w wersji

## <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Zezwalaj użytkownikom na zastąpienie plików zawartości, które już istnieją

Jedną z najbardziej pożądanych funkcji cały czas została możliwość zastąpienia plików zawartości, które już istnieją na dysku, gdy uwzględnione w pakiecie NuGet. Począwszy od NuGet 2.5 te konflikty zostaną rozpoznane i pojawi się monit o zastąpienie plików, należy wcześniej zawsze pliki te zostały pominięte.

![Zastąp pliki zawartości](./media/NuGet-2.5/overwrite-file.png)

"nuget.exe aktualizacji" i "Install-Package" teraz mają nową opcję "-FileConflictAction" można ustawić pewne domyślne dla scenariuszy wiersza polecenia.

Domyślna akcja należy ustawić, gdy plik z pakietu już istnieje w projekcie docelowym. Wartość "Zastąp" zawsze zastąpienie plików. Wartość "Ignore" Pomiń pliki. Jeśli nie zostanie określony, pojawi się monit o poszczególnych plików powodujących konflikt.

## <a name="automatic-import-of-msbuild-targets-and-props-files"></a>Automatyczne importowanie MSBuild cele i pliki właściwości

Nowy folder konwencjonalnej został utworzony na najwyższym poziomie pakietu NuGet.  Jako elementu równorzędnego do `\lib`, `\content`, i `\tools`, obecnie można uwzględnić `\build` folderu do pakietu.  W tym folderze, możesz umieścić dwoma plikami o stałej nazwie `{packageid}.targets` lub `{packageid}.props`. Te dwa pliki mogą być bezpośrednio w obszarze `build` lub w obszarze określonej struktury folderów, podobnie jak w innych folderach. Reguła dla folderu framework najlepiej dopasowane do pobrania jest dokładnie takie same jak te.

Podczas instalowania NuGet pakietu z plikami \build doda MSBuild `<Import>` elementu w pliku projektu wskazujący `.targets` i `.props` plików. `.props` Plik zostanie dodany u góry, podczas gdy `.targets` plik zostanie dodany do dołu.

## <a name="specify-different-references-per-platform-using-references-element"></a>Określ różne odwołania na platformie za pomocą `<References/>` — element

Przed 2.5 w `.nuspec` pliku użytkownika można określić tylko pliki odwołania, ma zostać dodana dla wszystkich framework. Teraz dzięki tej nowej funkcji 2.5 użytkownika można tworzyć `<reference/>` elementu dla każdej z obsługiwanych platform, na przykład:

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

Poniżej przedstawiono przepływ dla jak NuGet dodaje odwołań do projektów opartych na `.nuspec` pliku:

1. Znajdź `lib` folderu, który jest odpowiedni dla platformy docelowej i Pobierz listę zestawów z tego folderu
1. Oddzielnie znaleźć odwołuje się do grupy, który jest odpowiedni dla platformy docelowej i listę zestawów z tej grupy. Grupy odwołania bez określonej platformy docelowej jest grupa rezerwowego.
1. Znajdź część wspólną dwóch list i używać go jako odwołania do dodania

Ta nowa funkcja umożliwia autorów pakiet do użycia funkcji odwołań do zastosowania podzbiór zestawów do różnych platform, gdy byłby normalnie potrzebny do przenoszenia zestawy zduplikowany w wielu `lib` folderów.

Uwaga: należy obecnie używasz pakietu nuget.exe Aby użyć tej funkcji; Eksplorator pakietu NuGet nie obsługuje jeszcze go.

## <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Zaktualizuj wszystkie przycisk umożliwia jednocześnie aktualizowania wszystkich pakietów

Wiele osób wiedzieć o polecenia cmdlet programu PowerShell "Pakiet aktualizacji" można zaktualizować wszystkich pakietów; teraz jest prosty sposób, w tym także interfejsu użytkownika.

Aby wypróbować tę funkcję:

1. Tworzenie nowej aplikacji ASP.NET MVC
1. Uruchom okno dialogowe "Manage NuGet Packages"
1. Wybierz opcję "Aktualizacji"
1. Kliknij przycisk "Aktualizuj wszystkie"

![Zaktualizuj wszystkie przycisk w oknie dialogowym](./media/NuGet-2.5/update-all.png)

## <a name="improved-project-reference-support-for-nugetexe-pack"></a>Odwołanie projektu ulepszone obsługę nuget.exe pakietu

Teraz nuget.exe pakiet polecenia procesów przywoływane projekty z następującymi regułami:

1. Jeśli ma przywoływanego projektu odpowiadającego `.nuspec` pliku, np. istnieje plik o nazwie `proj1.nuspec` w tym samym folderze co `proj1.csproj`, następnie ten projekt zostanie dodany jako zależność do pakietu przy użyciu identyfikatora i odczytać wersji z `.nuspec` pliku.
1. W przeciwnym razie pliki przywoływanego projektu są połączone w pakiecie. Następnie projektów odwołuje się ten projekt zostanie przetworzona za pomocą sames rekursywnie reguły.
1. Wszystkie biblioteki DLL, `.pdb`, i `.exe` pliki zostaną dodane.
1. Wszystkie pliki zawartości są dodawane.
1. Wszystkie zależności są łączone.

Dzięki temu przywoływanego projektu powinien być traktowany jako zależność, jeśli istnieje `.nuspec` pliku, w przeciwnym razie staje się częścią pakietu.

Więcej informacji w tym miejscu: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

## <a name="add-a-minimum-nuget-version-property-to-packages"></a>Dodaj właściwość "Minimalna wersja narzędzia NuGet" do pakietów

Nowy atrybut metadanych o nazwie "minClientVersion" można teraz wskazać minimalnej wersji klienta NuGet musieli korzystać z pakietem.

Funkcja ta ułatwia autora pakietu, aby określić, że pakiet będą działać dopiero po określonej wersji programu NuGet. Jak nowe `.nuspec` funkcje zostaną dodane po NuGet 2.5 pakiety będą mogli oświadczeń minimalna wersja narzędzia NuGet.

```xml
<metadata minClientVersion="2.6">
```

Jeśli użytkownik ma zainstalowane 2.5 NuGet, pakiet zostanie zidentyfikowana jako wymagające 2.6 wizualnych otrzyma użytkownikowi wskazujący, że pakiet nie będzie możliwe do zainstalowania. Użytkownik zostanie następnie z przewodnikiem, aby zaktualizować ich wersja programu NuGet.

Poprawia to na istniejące środowisko, gdzie rozpocząć pakietów do zainstalowania, a następnie się nie powieść wskazujący, że wersja schematu nierozpoznany została zidentyfikowana.

## <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>Zależności już niepotrzebnie są aktualizowane podczas instalacji pakietu aktualizacji

Przed 2.5 NuGet gdy pakiet został zainstalowany, która była uzależniona od pakietu już zainstalowany w projekcie, zależności byłby aktualizowany w ramach nowej instalacji nawet wtedy, gdy istniejąca wersja spełnione zależności.

Począwszy NuGet 2.5, jeśli wersja zależności już jest spełniony, zależność nie zostanie zaktualizowany podczas inne instalacje pakietu.

**Scenariusz:**

1. Repozytorium źródłowe zawiera pakiet B w wersji 1.0.0 i w wersji 1.0.2. Zawiera także pakietu A zależy B (> = 1.0.0).
1. Załóżmy, że bieżący projekt ma już wersję pakietu B 1.0.0 zainstalowane. Teraz ma zostać zainstalowany pakiet A.

**W NuGet 2,2 i starszych:**

* Podczas instalowania pakietu, A, NuGet automatycznie zaktualizuje B 1.0.2, nawet jeśli istniejąca wersja 1.0.0 spełnia już ograniczenie wersji zależności, która jest > = 1.0.0.

**W NuGet 2.5 lub nowszej:**

* NuGet już zaktualizuje B, ponieważ wykrywa, że istniejąca wersja 1.0.0 spełnia ograniczenia wersji zależności.

W tle więcej na temat tej zmiany, przeczytaj szczegółowe [elementu roboczego](http://nuget.codeplex.com/workitem/1681) oraz powiązanych [wątek dyskusji](http://nuget.codeplex.com/discussions/436712).

## <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>nuget.exe danych wyjściowych żądań http o poziomie szczegółowości szczegółowe

Jeśli występuje problem nuget.exe lub po prostu zastanawiasz się, jakie żądania HTTP są wprowadzane podczas operacji, '-szczegółowości szczegółowe "przełącznika teraz dane wyjściowe obejmują wszystkie żądania HTTP.

![Dane wyjściowe nuget.exe HTTP](./media/NuGet-2.5/verbosity.png)

## <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>wypychania nuget.exe obsługuje teraz źródeł UNC i folderów

Przed NuGet 2.5 podczas próby uruchomienia "nuget.exe push" do źródła pakietu na podstawie ścieżki UNC lub folderu lokalnego powiadomienia wypychanego nie powiedzie się. Z funkcją ostatnio dodane konfiguracji hierarchiczna stało się często nuget.exe trzeba objęcie źródła UNC lub folder lub galerii NuGet oparte na protokole HTTP.

Zaczynając NuGet 2.5, jeśli nuget.exe identyfikuje źródła UNC lub folder, zostanie przeprowadzone kopiowania plików do źródła.

Teraz działa następujące polecenie:

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

## <a name="nugetexe-supports-explicitly-specified-config-files"></a>nuget.exe obsługuje jawnie określić pliki konfiguracji

polecenia nuget.exe, które uzyskują dostęp do konfiguracji (wszystkie z wyjątkiem "spec" oraz "pakiet"), teraz obsługują nowy "-ConfigFile" opcja, która wymusza konfiguracji określonego pliku do użycia zamiast domyślnego pliku konfiguracji % AppData%\nuget\Nuget.Config.

Przykład:

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

## <a name="support-for-native-projects"></a>Pomoc techniczna dla projektów natywnych

Z NuGet 2.5 narzędzia NuGet jest teraz dostępna dla projektów natywnych w programie Visual Studio. Oczekujemy najbardziej natywnego pakietów korzystanie z funkcji importów MSBuild powyżej, przy użyciu narzędzia utworzone przez [projektu CoApp](http://coapp.org). Aby uzyskać więcej informacji, przeczytaj [szczegółowe informacje o narzędziu](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) na coapp.org witryny sieci Web.

Nazwa docelowej framework "native" wprowadzono pakietów podczas dołączania plików \build, \content i \tools po zainstalowaniu pakietu do natywnego projektu.  \`Lib "folder nie jest używany dla projektów natywnych.
