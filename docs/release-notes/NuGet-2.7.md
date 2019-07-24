---
title: Informacje o wersji narzędzia NuGet 2,7
description: Informacje o wersji programu NuGet 2,7, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f26ac80046ec321ce5bdbf2bac23c0e1939cd69a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317081"
---
# <a name="nuget-27-release-notes"></a>Informacje o wersji narzędzia NuGet 2,7

[Pakiet NuGet dost dla programu WebMatrix informacje](../release-notes/nuget-2.6.1-for-webmatrix.md) | o wersji[NuGet 2.7.1 — informacje o wersji](../release-notes/nuget-2.7.1.md)

Pakiet NuGet 2,7 został opublikowany od 22 sierpnia 2013.

## <a name="acknowledgements"></a>Potwierdzanie

Chcemy podziękowanie następujących zewnętrznych współautorom w celu uzyskania znaczących wkładów do programu NuGet 2,7:

1. [Jan Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - Pokaż adres URL licencji podczas szczegółowego tworzenia listy pakietów i szczegółowości.
2. [Adam](http://www.codeplex.com/site/users/view/adamralph) : ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -Dodaj atrybut developmentDependency do `packages.config` i użyj go w pakiecie Command w celu uwzględnienia tylko pakietów środowiska uruchomieniowego
3. [Rafael NICOLETTI](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Unikaj duplikowania klucza właściwości w pakiecie NuGet. exe Pack.
4. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) — zwiększenie rozmiaru pamięci podręcznej maszyny do 200.
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) — poprawka okna dialogowego programu NuGet pokazująca aktualizacje na niewłaociwej karcie
    - Poprawka Project. TargetFramework może mieć wartość null w elemencie projectmanager
    - [#3248](http://nuget.codeplex.com/workitem/3248) -poprawka SharedPackageRepository FindPackage/FindPackagesById zakończy się niepowodzeniem w przypadku nieistniejącej packageId
6. [Jan Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) — Włączanie obsługi projektu Nomad
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -Naprawa polecenia push kończy się niepowodzeniem z kodem zakończenia 0, gdy plik nie istnieje.
8. [Veselý Martin](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) — Usuń usterkę za pomocą polecenia Add-bindingRedirect, gdy projekt odwołuje się do projektu bazy danych.
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) — Usuń usterkę programu NuGet. Wyznaczanie symbolu wieloznacznego w atrybucie "exclude".
10. [Justin](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
     - [#3307](http://nuget.codeplex.com/workitem/3307) — usunięcie usterki `NuGet.targets` nie powoduje przekazania pliku $ (platform) do pliku NuGet. exe podczas przywracania pakietów.
11. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) — Usuń usterkę w poleceniu pakietu NuGet. exe, która zezwala na dodawanie plików o tej samej nazwie, ale o innej wielkości liter, ostatecznie powodując wyjątek "element już istnieje".
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
     - [#2990](http://nuget.codeplex.com/workitem/2990) — Dodaj właściwość wersji do klasy NetPortableProfile.
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) — Usuń usterkę NullReferenceException, jeśli requireApiKey = true, ale nagłówek X-NuGet-APIKEY nie istnieje
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
     - [#3278](https://nuget.codeplex.com/workitem/3278) — naprawia plik targets NuGet. Build, aby działał poprawnie na potrzeby narzędzia MonoDevelop
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
     - Poprawianie wydajności poleceń przywracania przez zwiększenie przetwarzanie równoległe

## <a name="notable-features-in-the-release"></a>Istotne funkcje w wersji

### <a name="package-restore-by-default-with-implicit-consent"></a>Przywracanie pakietów domyślnie (z niejawną zgodą)

W pakiecie NuGet 2,7 wprowadzono nowe podejście do przywracania pakietów, a także nastąpi główne progi: Zgoda na przywracanie pakietu jest teraz włączona domyślnie. Połączenie nowego podejścia i niejawnej zgody znacznie upraszcza scenariusze przywracania pakietów.

#### <a name="implicit-consent"></a>Niejawna zgoda

W przypadku pakietów NuGet w wersji 2,0, 2,1, 2,2, 2,5 i 2,6 użytkownicy musieli jawnie zezwolić narzędziu NuGet na pobieranie brakujących pakietów podczas kompilacji. Jeśli ta zgoda nie została jawnie określona, rozwiązania, dla których włączono przywracanie pakietów, nie zostaną skompilowane, dopóki użytkownik nie uzyska zgody.

Począwszy od programu NuGet 2,7, zgoda na przywracanie pakietu jest domyślnie włączona, a użytkownicy  mogą jawnie zrezygnować z przywracania pakietów, jeśli jest to konieczne, przy użyciu pola wyboru w ustawieniach NuGet w programie Visual Studio. Ta zmiana dla niejawnej zgody wpływa na pakiet NuGet w następujących środowiskach:

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* Narzędzie wiersza polecenia NuGet. exe

#### <a name="automatic-package-restore-in-visual-studio"></a>Automatyczne przywracanie pakietów w programie Visual Studio

Począwszy od programu NuGet 2,7, pakiet NuGet automatycznie pobierze brakujące pakiety podczas kompilacji w programie Visual Studio, nawet jeśli przywracanie pakietu nie zostało jawnie włączone dla rozwiązania. To automatyczne przywracanie pakietów odbywa się w programie Visual Studio podczas kompilowania projektu lub rozwiązania, ale przed wywołaniem MSBuild. Daje to kilka znaczących korzyści:

1. Nie trzeba już używać gestu "Włącz przywracanie pakietów NuGet" w rozwiązaniu
1. Projekty nie muszą być modyfikowane, a pakiet NuGet nie wprowadza zmian w projekcie, aby upewnić się, że przywracanie pakietu jest włączone
1. Wszystkie pakiety NuGet, w tym te, które obejmują Importy MSBuild dla plików props/targets, zostaną przywrócone *przed* wywołaniem programu MSBuild, co zapewnia prawidłowe rozpoznanie tych właściwości/obiektów docelowych podczas kompilacji

Aby można było używać automatycznego przywracania pakietów w programie Visual Studio, wystarczy wykonać jedną akcję (w):

1. Nie sprawdzaj w `packages` folderze

Istnieje kilka sposobów pominięcia `packages` folderu z kontroli źródła. Aby uzyskać więcej informacji, zobacz temat [pakiety i kontrola źródła](../consume-packages/packages-and-source-control.md) .

Mimo że wszyscy użytkownicy są niejawnie wybierani jako zgoda na automatyczne przywracanie pakietów, można łatwo zrezygnować z ustawień Menedżera pakietów w programie Visual Studio.

![Ustawienia Menedżera pakietów](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Uproszczone przywracanie pakietu z wiersza polecenia

W programie NuGet 2,7 wprowadzono nową funkcję NuGet. exe:`nuget.exe restore`

To nowe polecenie Restore pozwala łatwo przywrócić wszystkie pakiety dla rozwiązania za pomocą jednego polecenia, akceptując plik rozwiązania lub folder jako argument. Ponadto ten argument jest implikowany, gdy w bieżącym folderze istnieje tylko jedno rozwiązanie. Oznacza to, że poniższe wszystkie zadania pochodzą z folderu zawierającego pojedynczy plik rozwiązania (. sln):

1. nuget.exe restore MySolution.sln
1. Przywracanie pliku NuGet. exe.
1. Przywracanie pliku NuGet. exe

Polecenie Restore spowoduje otwarcie pliku rozwiązania i znalezienie wszystkich projektów w ramach rozwiązania. W tym miejscu znajdą `packages.config` się pliki dla każdego z projektów i zostaną przywrócone wszystkie znalezione pakiety. Powoduje również przywrócenie pakietów na poziomie rozwiązania znalezionych w `.nuget\packages.config` pliku. Więcej informacji na temat nowego polecenia Restore można znaleźć w [dokumentacji wiersza polecenia](../reference/cli-reference/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>Przepływ pracy przywracania nowego pakietu

Przyjemnością o te zmiany w przywracaniu pakietów, ponieważ wprowadza nowy przepływ pracy. Jeśli chcesz pominąć pakiety z kontroli źródła, po prostu nie zatwierdzisz `packages` folderu. Użytkownicy programu Visual Studio, którzy otwierają i tworzą rozwiązanie, zobaczą automatycznie przywrócone pakiety. W przypadku kompilacji wiersza polecenia po prostu wywołaj `nuget.exe restore` przed wywołaniem. `msbuild` Nie trzeba już pamiętać, aby użyć gestu "Włącz przywracanie pakietów NuGet" w rozwiązaniu. nie trzeba już modyfikować projektów, aby zmienić kompilację. Zapewnia również znacznie ulepszone środowisko dla pakietów, które obejmują Importy MSBuild, szczególnie w przypadku importów dodanych za pośrednictwem najnowszej funkcji NuGet do [automatycznego importowania plików props/targets](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) z folderu \Build.

Oprócz pracy, która została zastosowana, pracujemy również z innymi ważnymi partnerami, aby zaokrąglić to nowe podejście. Nie mamy jeszcze konkretnych osi czasu dla żadnego z nich, ale każdy partner jest tak przyjemnością jak w przypadku nowego podejścia.

* Team Foundation Service — pracują nad integracją wywołania z `nuget.exe restore` domyślnymi scenariuszami kompilacji.
* Witryny sieci Web systemu Windows Azure — pracują tak, aby umożliwić wypychanie projektu do platformy Azure `nuget.exe restore` i wywoływanie przed skompilowaniem witryny sieci Web.
* TeamCity — aktualizuje wtyczkę Instalatora NuGet dla TeamCity 8. x
* AppHarbor — działają tak, aby umożliwić wypychanie repozytorium do AppHarbor i `nuget.exe restore` wywołane przed kompilacją rozwiązania.

Każdy partner powyżej mógłby korzystać z własnej kopii NuGet. exe i nie trzeba będzie przenosić pliku NuGet. exe do rozwiązania.

#### <a name="known-issues"></a>Znane problemy

Wystąpiły dwa znane problemy z programem NuGet. exe Restore z początkową wersją 2,7, ale zostały one naprawione na 9/6/2013 z aktualizacją [pakietu NuGet. CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/).  Ta aktualizacja jest również dostępna na [stronie pobierania programu NuGet 2,7](https://nuget.codeplex.com/releases/view/107605) w witrynie CodePlex.  Uruchomiono `nuget.exe update -self` aktualizację do najnowszej wersji.

Naprawiono:

1. [Przywracanie nowego pakietu nie działa na mono podczas korzystania z pliku SLN](https://nuget.codeplex.com/workitem/3596)
1. [Przywracanie nowego pakietu nie działa z projektami WIX](https://nuget.codeplex.com/workitem/3598)

Istnieje również znany problem z nowym przepływem pracy przywracania pakietu, z którego [automatyczne przywracanie pakietów nie działa w przypadku projektów w folderze rozwiązania](https://nuget.codeplex.com/workitem/3625). Ten problem został rozwiązany w narzędziu NuGet 2.7.1.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Przekierowanie projektu i błędy kompilacji/ostrzeżenia

Wiele razy po przekierowaniu lub uaktualnieniu projektu okaże się, że niektóre pakiety NuGet nie działają prawidłowo. Niestety, nie ma informacji o tym, a następnie nie ma wskazówek dotyczących sposobu ich rozwiązywania. W pakiecie NuGet 2,7 są teraz używane pewne zdarzenia programu Visual Studio do rozpoznawania po przekierowaniu lub uaktualnieniu projektu w taki sposób, który ma wpływ na zainstalowane pakiety NuGet.

W przypadku wykrycia, że przekierowanie lub uaktualnienie ma wpływ na dowolne pakiety, firma Microsoft będzie generować natychmiastowe błędy kompilacji, aby poinformować Cię o tym. Oprócz natychmiastowego błędu kompilacji poprowadzimy również `requireReinstallation="true"` flagę `packages.config` w pliku dla wszystkich pakietów, na które miało wpływ przekierowanie, a każda kolejna kompilacja w programie Visual Studio spowoduje wygenerowanie ostrzeżeń kompilacji dla tych pakietów.

Mimo że NuGet nie może wykonać automatycznej akcji w celu ponownego zainstalowania pakietów, których to dotyczy, mamy nadzieję, że to oznaczenie i ostrzeżenie pomogą Ci pomóc w ustaleniu, kiedy trzeba ponownie zainstalować pakiety. Pracujemy również nad dokumentacją dotyczącą [instrukcji ponownej instalacji pakietu](../consume-packages/reinstalling-and-updating-packages.md) , którą kierują te komunikaty o błędach.

### <a name="nuget-configuration-defaults"></a>Domyślne ustawienia konfiguracji narzędzia NuGet

W wielu firmach jest używany wewnętrznie pakiet NuGet, ale miało miejsce na twardym czas, w którym deweloperzy mogą korzystać z wewnętrznych źródeł pakietów zamiast nuget.org. W programie NuGet 2,7 wprowadzono funkcję ustawień domyślnych konfiguracji, która umożliwia określenie wartości domyślnych dla całego komputera dla:

1. Włączone źródła pakietów
1. Zarejestrowane, ale wyłączono źródła pakietów
1. Domyślne źródło wypychania NuGet. exe

Każdy z tych elementów można teraz skonfigurować w pliku znajdującym się `%ProgramData%\NuGet\NuGetDefaults.Config`w lokalizacji. Jeśli ten plik konfiguracji określa źródła pakietów, domyślne źródło pakietów NuGet.org nie zostanie zarejestrowane automatycznie, a zamiast nich `NuGetDefaults.Config` zostanie zarejestrowane.

Chociaż nie jest to wymagane do korzystania z tej funkcji, oczekujemy `NuGetDefaults.Config` , że firma wdraża pliki przy użyciu zasady grupy.

*Należy pamiętać, że ta funkcja nigdy nie spowoduje usunięcia źródła pakietu z ustawień NuGet dewelopera. Oznacza to, że deweloper już użył NuGet i w związku z tym ma zarejestrowane źródło pakietów NuGet.org, nie zostanie usunięte po utworzeniu `NuGetDefaults.Config` pliku.*

Aby uzyskać więcej informacji na temat tej funkcji, zobacz [Ustawienia domyślne konfiguracji programu NuGet](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) .

### <a name="renaming-the-default-package-source"></a>Zmiana nazwy domyślnego źródła pakietu

Pakiet NuGet zawsze zarejestrował domyślne źródło pakietu o nazwie "oficjalne źródło pakietu NuGet", które wskazuje na nuget.org. Ta nazwa była pełna, a także nie została określona, gdzie faktycznie wskazywała. Aby rozwiązać te dwa problemy, zmieniono nazwę tego źródła pakietu na "nuget.org" w interfejsie użytkownika. Adres URL źródła pakietu został również zmieniony w taki sposób, aby zawierał "www". prefiks. Po użyciu programu NuGet 2,7 istniejący "oficjalne źródło pakietu NuGet" zostanie automatycznie zaktualizowany do "NuGet.org" jako nazwę i "<https://www.nuget.org/api/v2/>" jako adres URL.

### <a name="performance-improvements"></a>Usprawnienia wydajności

Wprowadziliśmy pewne zwiększenie wydajności w 2,7, co spowoduje zmniejszenie ilości pamięci, mniejsze użycie dysku i szybszą instalację pakietu. Prowadzimy również inteligentniejsze zapytania do kanałów informacyjnych opartych na protokole OData, które zmniejszają ogólny ładunek.

### <a name="new-extensibility-apis"></a>Nowe interfejsy API rozszerzalności

Dodaliśmy nowe interfejsy API do naszych usług rozszerzalności, aby wypełnić przerwy braku funkcjonalności w poprzednich wersjach.

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

### <a name="development-only-dependencies"></a>Zależności tylko do programowania

Ta funkcja została zaprojektowana przez program [Adam pracownik2](https://twitter.com/adamralph) i umożliwia autorom pakietów deklarowanie zależności, które były używane tylko w czasie projektowania i nie wymagają zależności pakietów. Dodanie `developmentDependency="true"` atrybutu do `packages.config` pakietu`nuget.exe pack` w programie nie spowoduje już dołączenia tego pakietu jako zależności.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Usunięto obsługę programu Visual Studio 2010 Express for Windows Phone

Nowy model przywracania pakietów w 2,7 jest implementowany przez nowy pakietu VSPackage, który różni się od głównego pakietu VSPackage NuGet. Ze względu na problem techniczny ten nowy pakietu VSPackage nie działa prawidłowo w programie *Visual Studio 2010 Express for Windows Phone* , ponieważ udostępniamy tę samą bazę kodu z innymi obsługiwanymi jednostkami SKU programu Visual Studio. W związku z tym, począwszy od programu NuGet 2,7, firma Microsoft porzuca obsługę programu *Visual Studio 2010 Express dla Windows Phone* z opublikowanego rozszerzenia. Obsługa programu *Visual studio 2010 Express for Web* jest nadal uwzględniona w podstawowym rozszerzeniu opublikowanym w galerii rozszerzeń programu Visual Studio.

Ze względu na to, ilu deweloperów nadal używa narzędzia NuGet w tej wersji/wydaniu programu Visual Studio, firma Microsoft publikuje osobne rozszerzenie programu Visual Studio przeznaczone dla tych użytkowników i publikuje je w witrynie CodePlex (a nie w galerii rozszerzeń programu Visual Studio). . Nie planujemy dalszego utrzymania tego rozszerzenia, ale jeśli to wpłynie, skontaktuj się z nami, podając problem z CodePlex.

Aby pobrać Menedżera pakietów NuGet (dla programu Visual Studio 2010 Express for Windows Phone), odwiedź stronę [pliki do pobrania dla programu nuget 2,7](https://nuget.codeplex.com/releases/view/107605) .

### <a name="bug-fixes"></a>Poprawki błędów

Oprócz tych funkcji Ta wersja programu NuGet zawiera również wiele innych poprawek błędów. W wydaniu wystąpiło 97 całkowite problemy rozwiązane. Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 2,7, zobacz [Śledzenie problemów NuGet dla tej wersji](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
