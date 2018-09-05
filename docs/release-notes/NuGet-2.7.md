---
title: Informacje o wersji 2.7 NuGet
description: Informacje o wersji programu NuGet 2.7, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 97d3e5f0238fd6947a54e5eb3229b89b6746f18c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550968"
---
# <a name="nuget-27-release-notes"></a>Informacje o wersji 2.7 NuGet

[NuGet 2.6.1 dla programu WebMatrix wersji](../release-notes/nuget-2.6.1-for-webmatrix.md) | [informacjach o wersji NuGet 2.7.1](../release-notes/nuget-2.7.1.md)

22 sierpnia 2013 został wydany NuGet w wersji 2.7.

## <a name="acknowledgements"></a>Potwierdzanie

Chcielibyśmy podziękować następujące współautorów zewnętrznych dla znaczny wkład w 2.7 NuGet:

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - Pokaż adres url licencji, podczas wyświetlania listy pakietów i poziom szczegółowości została szczegółowo opisana.
2. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -Dodaj atrybut developmentDependency, aby `packages.config` i używać go w poleceniu pakiet obejmujący tylko pakiety środowiska uruchomieniowego
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Należy unikać zduplikowany klucz właściwości w poleceniu pakiet nuget.exe.
4. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) — Zwiększ rozmiar pamięci podręcznej maszyny do 200.
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -NuGet naprawić Wyświetla okno dialogowe aktualizacji w niewłaściwej karty
    - Poprawka Project.TargetFramework może być pusta w Menedżer_projektu
    - [#3248](http://nuget.codeplex.com/workitem/3248) -packageId nieistniejącej naprawić SharedPackageRepository FindPackage/FindPackagesById zakończy się niepowodzeniem
6. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -Włącz obsługę Nomad projektu
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) — poprawki wypychania polecenie kończy się niepowodzeniem z zakończenia kod 0, jeśli plik nie istnieje.
8. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -naprawić błąd, za pomocą polecenia Add-BindingRedirect, gdy projekt odwołuje się do projektu bazy danych.
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -naprawić błąd nuget.pack niepoprawnie analizowania symbolu wieloznacznego w atrybucie "Wyklucz".
10. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
     - [#3307](http://nuget.codeplex.com/workitem/3307) -naprawić błąd `NuGet.targets` nie przekazuje $(Platform) do nuget.exe podczas przywracania pakietów.
11. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) -poprawkę usterki w poleceniu pakietu nuget.exe, który umożliwi dodawanie plików o takiej samej nazwie, ale inną wielkością liter, może sprawić, że wyjątek "Już istnieje element".
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
     - [#2990](http://nuget.codeplex.com/workitem/2990) — Dodawanie wersji właściwości do klasy NetPortableProfile.
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) -Naprawiano błąd obiektu NullReferenceException Jeśli requireApiKey = true, ale nagłówek X-NUGET-APIKEY nie jest obecny
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
     - [#3278](https://nuget.codeplex.com/workitem/3278) — plik poprawki NuGet.Build celów, tak, że działa on prawidłowo w narzędziu MonoDevelop
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
     - Poprawianie wydajności polecenia Restore, zwiększając przetwarzania równoległego

## <a name="notable-features-in-the-release"></a>Ważne funkcje w wersji

### <a name="package-restore-by-default-with-implicit-consent"></a>Przywracanie pakietu domyślnie (za zgodą niejawne)

NuGet w wersji 2.7 wprowadza nowe podejście do pakietu przywracania, a także pozwala pokonać głównych próg wykluczający: zgody przywracania pakietu jest teraz domyślnie! Kombinacja nowe podejście i niejawne zgody znacząco upraszcza scenariuszy przywracania pakietu.

#### <a name="implicit-consent"></a>Niejawne zgody

W przypadku wersji NuGet w wersji 2.0, 2.1, 2.2, 2.5 i 2.6 użytkowników, niezbędnych w celu jawnego zezwalania pakietu NuGet, aby pobrać brakujące pakiety podczas kompilacji. Gdyby ta zgody nie została jawnie podana, rozwiązania, które ma włączone Przywracanie pakietu może się nie powieść, tworzyć, dopóki użytkownik miał uzyska zatwierdzenie.

Począwszy od NuGet w wersji 2.7 zgody przywracania pakietów jest włączone domyślnie równocześnie umożliwiając użytkownikom jawnie *zrezygnować* przywracania pakietu, jeśli to konieczne, za pomocą pola wyboru w ustawieniach NuGet w programie Visual Studio. Ta zmiana niejawne zgody wpływa na NuGet w następujących środowiskach:

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* Narzędzie wiersza polecenia nuget.exe

#### <a name="automatic-package-restore-in-visual-studio"></a>Przywracanie pakietu automatyczne w programie Visual Studio

Począwszy od NuGet w wersji 2.7 NuGet będzie automatycznie pobierał brakujących pakietów podczas kompilacji w programie Visual Studio, nawet jeśli Przywracanie pakietu nie zostało jawnie włączone dla rozwiązania. To automatyczne przywracanie pakietu odbywa się w programie Visual Studio, gdy tworzysz projekt lub rozwiązanie, ale przed wywołaniem programu MSBuild. Daje to kilka istotne korzyści:

1. Żadne dodatkowe muszą używać gest "Włącz Przywracanie pakietów NuGet" w rozwiązaniu
1. Nie trzeba modyfikować projekty i NuGet nie wprowadzić zmiany do projektu, aby upewnić się, że włączono Przywracanie pakietu
1. Wszystkie pakiety NuGet, w tym te, które uwzględnione MSBuild importuje pliki właściwości/elementów docelowych zostaną przywrócone *przed* MSBuild, zostanie wywołana, zapewniając te właściwości/obiekty docelowe są prawidłowo rozpoznawane podczas kompilacji

Aby można było używać automatycznego przywracania pakietów w programie Visual Studio, wystarczy wykonać jedną (akcję cale):

1. Nie można zaewidencjonować swoje `packages` folderu

Istnieje kilka sposobów, aby pominąć swoje `packages` folderu z kontroli źródła. Aby uzyskać więcej informacji, zobacz [pakiety i kontrola źródła](../consume-packages/packages-and-source-control.md) tematu.

Podczas gdy wszyscy użytkownicy są niejawnie przeniesione do automatycznego przywracania pakietów zgody, możesz łatwo zrezygnować z za pomocą ustawień Menedżera pakietów w programie Visual Studio.

![Ustawienia Menedżera pakietów](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Przywracanie pakietu uproszczone z wiersza polecenia

NuGet w wersji 2.7 wprowadzono nową funkcję nuget.exe: `nuget.exe restore`

To nowe polecenie Restore umożliwia łatwo przywrócić wszystkie pakiety dla rozwiązania za pomocą jednego polecenia, akceptując plik rozwiązania lub folder jako argument. Ponadto ten argument jest implikowane, gdy istnieje tylko jedno rozwiązanie w bieżącym folderze. Oznacza to, że wszystkie następujące pracować z folderu, który zawiera plik jednego rozwiązania (MySolution.sln):

1. nuget.exe restore MySolution.sln
1. Przywracanie nuget.exe.
1. Przywracanie nuget.exe

Polecenie Restore będzie Otwórz plik rozwiązania i Znajdź wszystkie projekty w rozwiązaniu. W efekcie zostanie odnaleziony `packages.config` pliki dla wszystkich projektów i Przywróć wszystkie pakiety znaleziono. Przywraca także pakietów poziomie rozwiązania w `.nuget\packages.config` pliku. Więcej informacji na temat nowego polecenia przywracania znajdują się w [odwołanie do wiersza polecenia](../tools/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>Nowy przepływ pracy przywracania pakietu

Cieszymy się o tych zmianach, aby przywrócić pakietu, ponieważ wprowadza nowy przepływ pracy. Jeśli chcesz pominąć pakietów z kontroli źródła po prostu nie zdecydujesz się `packages` folderu. Visual Studio użytkownicy otworzyć i skompilować rozwiązanie zobaczą automatycznie przywrócono pakiety. Dla kompilacji z wiersza polecenia, po prostu wywołać `nuget.exe restore` przed wywołaniem `msbuild`. Nie są już potrzebne do zapamiętania na korzystanie z rozwiązania gest "Włącz Przywracanie pakietów NuGet", a firma Microsoft będzie nie jest już konieczne zmodyfikowanie projektów, aby zmienić kompilacji. A także zapewni znacznie udoskonalony interfejs użytkownika dla pakietów, które zawierają Importy MSBuild, szczególnie w przypadku importów dodane za pomocą funkcji ostatnie NuGet dla [automatycznie zaimportować właściwości/elementów docelowych pliki](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) z folderu \build.

Oprócz pracy, które firma Microsoft wykonane osoby pracujemy także niektóre ważne partnerom zaokrąglić to nowe podejście w. Nie mamy jeszcze konkretnych osie czasu dla każdego z nich, ale każdego partnera jest tak jak My temat nowego podejścia.

* Team Foundation Service - pracują zintegrować wywołanie `nuget.exe restore` do domyślnej kompilacji scenariuszy.
* Windows Azure Web Sites — pracują umożliwia przyspieszenie realizacji projektu na platformie Azure i mają `nuget.exe restore` wywoływana przed wykonaniem powstała witryny sieci web.
* TeamCity - aktualizują ich wtyczki Instalatora NuGet dla TeamCity 8.x
* AppHarbor - pracują aby możliwe było wypchnąć repozytorium do AppHarbor i mieć `nuget.exe restore` wywoływana zanim rozwiązanie będzie kompilacji.

Z każdą z powyższych partnerów będzie korzystać z własnej kopii nuget.exe i nie trzeba wykonać nuget.exe w rozwiązaniu.

#### <a name="known-issues"></a>Znane problemy

Wystąpiły dwa znane problemy dotyczące przywracania nuget.exe początkowa wersja 2.7, ale zostaną naprawione 9/6/2013 z aktualizacją [pakietu NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/).  Ta aktualizacja jest dostępna również na [strony pobierania NuGet w wersji 2.7](https://nuget.codeplex.com/releases/view/107605) w witrynie CodePlex.  Uruchamianie `nuget.exe update -self` zostanie zaktualizowany do najnowszej wersji.

Wprowadzono stałe:

1. [Nowe Przywracanie pakietu nie działa w przypadku platformy Mono, korzystając z pliku SLN](https://nuget.codeplex.com/workitem/3596)
1. [Nowe Przywracanie pakietu nie działa z projektami Wix](https://nuget.codeplex.com/workitem/3598)

Jest również znany problem z nowy przepływ pracy przywracania pakietów zgodnie z którą [automatyczne przywracanie pakietu nie działa w przypadku projektów w folderze rozwiązania](https://nuget.codeplex.com/workitem/3625). Ten problem został rozwiązany w pakiecie NuGet 2.7.1.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Przekierowanie i uaktualnieniu błędy/ostrzeżenia kompilacji projektu

Wiele prób po retargeting i uaktualniania projektu, możesz znaleźć niektóre pakiety NuGet nie działa prawidłowo. Niestety nie ma żadnego wskazania i to nie ma żadnej wskazówki na temat rozwiązać problem. Za pomocą NuGet w wersji 2.7 używamy teraz niektóre zdarzenia programu Visual Studio do rozpoznawania już przekierowano element lub uaktualniony projekt, w sposób, który ma wpływ na zainstalowanych pakietów NuGet.

Wykryliśmy, że dowolne pakiety wpłynęła na retargeting i uaktualniania, firma Microsoft wygenerowanie błędy kompilacji natychmiastowego informacją o tym. Oprócz błąd kompilacji natychmiastowego również utrzymujemy `requireReinstallation="true"` znacznik w swojej `packages.config` pliku dla wszystkich pakietów, które zostały objęte przez przekierowywanie i każdego kolejnego kompilacji w programie Visual Studio zgłosi ostrzeżenia kompilacji dla tych pakietów.

Mimo że NuGet nie może automatycznie podjąć odpowiednie działania do ponownej instalacji pakietów których to dotyczy, mamy nadzieję, że to oznaczenie i ostrzeżenie przeprowadzi pomocy można wykryć, kiedy trzeba będzie ponownie zainstalować pakiety. Pracujemy również nad [dokumentacja ze wskazówkami dotyczącymi jego ponowna instalacja pakietu](../consume-packages/reinstalling-and-updating-packages.md) czy te komunikaty o błędach przekierowany.

### <a name="nuget-configuration-defaults"></a>Domyślne wartości NuGet

Wiele firm używa się NuGet wewnętrznie, lecz mieli czas twardych przeprowadzi ich deweloperom używanie źródeł wewnętrznych pakietów zamiast nuget.org. NuGet w wersji 2.7 wprowadza funkcja domyślne ustawienia konfiguracji, która umożliwia domyślne ustawienia dla komputera, może być określona dla:

1. Źródła pakietów włączone
1. Źródła pakietów zarejestrowane, ale wyłączone
1. Domyślne źródło wypychania nuget.exe

Każdy z nich można teraz skonfigurować w pliku znajdującym się w `%ProgramData%\NuGet\NuGetDefaults.Config`. Jeśli ten plik konfiguracji określa źródeł pakietów, a następnie domyślne źródło pakietów nuget.org nie zostanie automatycznie zarejestrowany i podane w `NuGetDefaults.Config` zostanie zarejestrowana, zamiast tego.

Chociaż nie jest wymagane do użycia tej funkcji, oczekujemy, że firmom na wdrażanie `NuGetDefaults.Config` plików za pomocą zasad grupy.

*Należy pamiętać, że ta funkcja nigdy nie spowoduje źródło pakietu, który ma zostać usunięty z ustawień NuGet dla deweloperów. Oznacza to, że jeśli deweloper, który już użył NuGet i dlatego ma źródło pakietów nuget.org zarejestrowany, go nie zostaną usunięte po utworzeniu `NuGetDefaults.Config` pliku.*

Zobacz [domyślne konfiguracji NuGet](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) Aby uzyskać więcej informacji na temat tej funkcji.

### <a name="renaming-the-default-package-source"></a>Zmienianie nazwy domyślnego źródła pakietu

NuGet zawsze zarejestrował domyślne źródło pakietu o nazwie "NuGet oficjalne źródło pakietu" wskazującego na stronie nuget.org. Ta nazwa została pełne i go również nie określił gdzie zostało faktycznie wskazuje. Aby rozwiązać te dwa problemy, firma Microsoft po zmianie nazwy tego źródła pakietów, można po prostu "nuget.org" w interfejsie użytkownika. Również zmieniono adres URL źródła pakietu do uwzględnienia "www". prefiks. Po zakończeniu korzystania z NuGet w wersji 2.7 swoje istniejące "NuGet oficjalne źródła pakietu" zostaną automatycznie zaktualizowane do "nuget.org" jako nazwy i "<https://www.nuget.org/api/v2/>" jako jej adresu URL.

### <a name="performance-improvements"></a>Usprawnienia wydajności

Wprowadziliśmy pewne poprawę wydajności w wersji 2.7, która umożliwia uzyskanie mniejsze zużycie pamięci, mniejsze użycie dysku oraz szybszą instalację pakietu. Wprowadziliśmy także inteligentniejszych zapytań OData na podstawie źródeł danych, co zmniejsza ogólną ładunku.

### <a name="new-extensibility-apis"></a>Nowe interfejsy API rozszerzalności

Dodaliśmy kilka nowych interfejsów API do naszych usług rozszerzalności, aby wypełnić przerwa brakujące funkcje w poprzednich wersjach.

#### <a name="ivspackageinstallerservices"></a>IVsPackageInstallerServices

    ```cs
    // Checks if a NuGet package with the specified Id and version is installed in the specified project.
    bool IsPackageInstalledEx(Project project, string id, string versionString);

    // Get the list of NuGet packages installed in the specified project.
    IEnumerable<IVsPackageMetadata> GetInstalledPackages(Project project);
    ```

#### <a name="ivspackageinstaller"></a>IVsPackageInstaller

    ```cs
    // Installs one or more packages that exist on disk in a folder defined in the registry.
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    // Installs one or more packages that are embedded in a Visual Studio Extension Package.
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);
    ```

### <a name="development-only-dependencies"></a>Tylko do tworzenia zależności

Ta funkcja została pochodzącego z danego [Adam Ralph](https://twitter.com/adamralph) i umożliwia autorom pakietów do deklarowania zależności, które były używane tylko w rozwoju czasu i nie wymagają zależności pakietów. Dodając `developmentDependency="true"` atrybutu do pakietu w `packages.config`, `nuget.exe pack` nie będą już uwzględniać pakiet jako zależność.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Usunięto obsługę dla programu Visual Studio 2010 Express dla Windows Phone

Nowy model przywracania pakietów w wersji 2.7 jest implementowany przez nowego pakietu VSPackage, który jest inny niż główny pakietu NuGet VSPackage. Z powodu problemu technicznego tego nowego pakietu VSPackage nie działa poprawnie w programie *Visual Studio 2010 Express dla Windows Phone* jednostka SKU udostępniamy tej samej bazy kodu z innymi obsługiwana Visual Studio SKU. W związku z tym, począwszy od NuGet w wersji 2.7, firma Microsoft odrzucają obsługę *Visual Studio 2010 Express dla Windows Phone* z opublikowanych rozszerzeń. Obsługa *Visual Studio 2010 Express for Web* nadal znajduje się w rozszerzeniu podstawowe publikowane w galerii rozszerzenia programu Visual Studio.

Ponieważ firma Microsoft pewności, jak wielu deweloperów są nadal za pomocą narzędzia NuGet w tej wersji/wydania programu Visual Studio, jesteśmy publikowanie rozszerzenia programu Visual Studio w oddzielnych, specjalnie dla tych użytkowników i publikując je na portalu CodePlex (a nie w galerii rozszerzenia programu Visual Studio) . Firma Microsoft nie planujesz kontynuować pracy do obsługi tego rozszerzenia, ale jeśli ma to wpływ na możesz Daj nam znać, rejestrując problem w witrynie CodePlex.

Aby pobrać Menedżera pakietów NuGet (dla programu Visual Studio 2010 Express dla Windows Phone), odwiedź stronę [NuGet w wersji 2.7 pliki do pobrania](https://nuget.codeplex.com/releases/view/107605) strony.

### <a name="bug-fixes"></a>Poprawki błędów

Poza tymi funkcjami ta wersja pakietu nuget zawiera również wiele innych poprawek. Wystąpiły 97 Suma problemów, które zostały rozwiązane w wydaniu. Aby uzyskać pełną listę prac elementy rozwiązane w NuGet w wersji 2.7. widok [NuGet narzędzie do śledzenia problemów w tej wersji](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
