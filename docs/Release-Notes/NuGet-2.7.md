---
title: Informacje o wersji NuGet 2.7 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Informacje o wersji 2.7 NuGet tym znanych problemów, poprawki, dodatkowe funkcje i dcr.
keywords: NuGet 2.7 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 71ced70af127c8219001069739a6cec59d7d1684
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-27-release-notes"></a>Informacje o wersji 2.7 NuGet

[2.6.1 NuGet, aby uzyskać informacje o wersji programu WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md) | [NuGet 2.7.1 informacje o wersji](../release-notes/nuget-2.7.1.md)

NuGet 2.7 wydanej w dniu 22 sierpnia 2013.

## <a name="acknowledgements"></a>Potwierdzeń

Chcielibyśmy Dziękujemy następujące współautorzy zewnętrznych dla ich znaczących wkładów 2.7 NuGet:

1. [Jan Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - Pokaż adres url licencji podczas szczegółowe listę pakietów i szczegółowości.
1. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -Dodaj atrybut developmentDependency do `packages.config` i używać go w poleceniu pakietu tylko pakiety mają być środowiska wykonawczego
1. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Unikaj zduplikowany klucz właściwości w poleceniu pakiet nuget.exe.
1. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) -Zwiększ rozmiar pamięci podręcznej maszyny do 200.
1. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) — okno dialogowe Napraw NuGet przedstawiający aktualizacje na karcie niewłaściwy
    - Poprawka Project.TargetFramework może mieć wartości null w Menedżer_projektu
    - [#3248](http://nuget.codeplex.com/workitem/3248) -Usuń SharedPackageRepository FindPackage/FindPackagesById zakończy się niepowodzeniem na nieistniejącą packageId
1. [Jan Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) — Włączanie obsługi Nomad projektu
1. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -poprawka wypychania polecenie kończy się niepowodzeniem z zakończenia kod 0, jeśli plik nie istnieje.
1. [Pole Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -Poprawka usterki za pomocą polecenia Dodaj BindingRedirect, gdy projekt odwołuje się do projektu bazy danych.
1. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -Poprawka usterki z nuget.pack niepoprawnie analizowania symbolu wieloznacznego w atrybucie "exclude".
1. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
    - [#3307](http://nuget.codeplex.com/workitem/3307) -Poprawka usterki `NuGet.targets` nie przekazuje $(Platform) do nuget.exe podczas przywracania pakietów.
1. [Brianowi Federici](http://www.codeplex.com/site/users/view/benerdin)
    - [#3294](http://nuget.codeplex.com/workitem/3294) -Poprawka usterki w poleceniu pakietu nuget.exe, który umożliwi dodawanie plików z tej samej nazwy, ale innej wielkości znaków, powodując wyjątek "Istnieje już element".
1. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
    - [#2990](http://nuget.codeplex.com/workitem/2990) -wersji Dodaj właściwość do klasy NetPortableProfile.
1. [Simner Dominik](https://www.codeplex.com/site/users/view/DavidSimner)
    - [#3460](https://nuget.codeplex.com/workitem/3460) — w razie Usuń usterki NullReferenceException requireApiKey = true, ale nagłówek X-NUGET-APIKEY nie jest obecny
1. [Jan Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
    - [#3278](https://nuget.codeplex.com/workitem/3278) — poprawki NuGet.Build cele pliku, która działa poprawnie na MonoDevelop
1. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
    - Poprawianie wydajności polecenia Restore, zwiększając paralelizacja

## <a name="notable-features-in-the-release"></a>Ważne funkcje w wersji

### <a name="package-restore-by-default-with-implicit-consent"></a>Przywracanie pakietu domyślnie (za zgodą niejawne)

NuGet 2.7 wprowadza nowe podejście do Przywracanie pakietów, a także pozwala pokonać głównych próg wykluczający: zgody przywracania pakietów jest teraz domyślnie! Kombinacja nowe podejście i niejawne zgody co znacznie uprości scenariuszy przywracania pakietu.

#### <a name="implicit-consent"></a>Niejawne zgody

Z NuGet w wersji 2.0, 2.1, 2.2, 2.5 i 2.6 użytkowników, konieczne jest jawnie Zezwalaj narzędziu NuGet na pobieranie brakujących pakietów podczas kompilacji. Gdyby ta zgody nie został jawnie podany, rozwiązania, które były włączone Przywracanie pakietu nie powiedzie się do kompilacji, dopóki użytkownik udzieliła zgody.

Począwszy od NuGet 2.7 zgody przywracania pakietu jest włączone domyślnie równocześnie umożliwiając użytkownikom jawnie *zrezygnować* przywracania pakietu w razie potrzeby można za pomocą pola wyboru w ustawieniach NuGet w programie Visual Studio. Ta zmiana niejawne zgodę wpływa NuGet w następujących środowiskach:

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* Narzędzie wiersza polecenia nuget.exe

#### <a name="automatic-package-restore-in-visual-studio"></a>Przywracanie pakietu automatyczne w programie Visual Studio

Począwszy od NuGet 2.7 NuGet zostanie automatycznie pobieranie brakujących pakietów podczas kompilacji w programie Visual Studio, nawet jeśli nie została jawnie włączona Przywracanie pakietów dla rozwiązania. Przywracanie automatyczne pakietu odbywa się w programie Visual Studio, podczas tworzenia projektu lub rozwiązania, ale przed MSBuild jest wywoływany. Daje to kilka znaczących korzyści:

1. Żadne dodatkowe muszą używać gestu "Włącz Przywracanie pakietu NuGet" w rozwiązaniu
1. Projekty nie muszą zostać zmodyfikowane i NuGet nie wprowadzić zmiany do projektu w taki sposób, aby upewnić się, że włączono Przywracanie pakietu
1. Wszystkie pakiety NuGet, w tym te, które uwzględnione Importy MSBuild dla właściwości/elementów docelowych pliki, zostaną przywrócone *przed* MSBuild zostanie wywołany, zapewniając właściwości/cele są prawidłowo rozpoznawane podczas kompilacji

Aby można było używać automatyczne przywracanie pakietów w programie Visual Studio, wystarczy wykonać jedną (akcję w):

1. Nie wyszukuj Twojej `packages` folderu

Istnieje kilka sposobów, aby pominąć Twojej `packages` folder z kontrolą źródła. Aby uzyskać więcej informacji, zobacz [pakietów i kontroli źródła](../consume-packages/packages-and-source-control.md) tematu.

Gdy wszyscy użytkownicy są domyślnie wyłączony na automatyczne przywracanie pakietów zgody, można łatwo zrezygnować z ustawieniach Menedżera pakietów w programie Visual Studio.

![Ustawienia Menedżera pakietów](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Przywracanie pakietu uproszczony z wiersza polecenia

NuGet 2.7 wprowadzono nową funkcję dla nuget.exe: `nuget.exe restore`

To nowe polecenie Restore umożliwia łatwo przywrócić wszystkich pakietów dla rozwiązania za pomocą jednego polecenia, zatwierdzając rozwiązania plik lub folder jako argument. Ponadto ten argument jest niejawnego, jeśli istnieje tylko jedno rozwiązanie w bieżącym folderze. Oznacza to, że wszystkie następujące działania z folderu, który zawiera plik pojedyncze rozwiązanie (MySolution.sln):

1. nuget.exe restore MySolution.sln
1. nuget.exe przywracania.
1. Przywracanie nuget.exe

Polecenie Restore będzie Otwórz plik rozwiązania i Znajdź wszystkie projekty w rozwiązaniu. Z tego miejsca, zostaną znalezione `packages.config` plików dla poszczególnych projektów i Przywróć wszystkie pakiety znalezione. Również przywraca rozwiązanie na poziomie znaleziono pakietów w `.nuget\packages.config` pliku. Więcej informacji na temat nowego polecenia Restore znajduje się w [dotyczące wiersza polecenia](../tools/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>Nowy przepływ pracy przywracania pakietu

Możemy radością dotyczące tych zmian, aby przywrócić pakietu, ponieważ wprowadza ona nowy przepływ pracy. Jeśli chcesz pominąć pakiety z kontroli źródła po prostu nie zatwierdzeniu `packages` folderu. Visual Studio użytkownicy otworzyć i Skompiluj rozwiązanie zobaczą automatycznie przywrócenia pakietów. Dla kompilacji z wiersza polecenia, po prostu Wywołaj `nuget.exe restore` przed wywołaniem `msbuild`. Nie trzeba Pamiętaj, aby użyć gestu "Włącz Przywracanie pakietu NuGet" w rozwiązaniu i już nie musisz zmodyfikować alter kompilacji projektów. A także daje to znacznie lepszą obsługę pakietów zawierających importów MSBuild, szczególnie w przypadku importów dodane za pomocą funkcji ostatnie NuGet dla [automatycznego importowania właściwości/elementów docelowych pliki](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) z folderu \build.

Oprócz pracy, które firma Microsoft wykonane nad również pracujemy niektóre ważne partnerom zaokrąglona to nowe podejście. Konkretnych osiach czasu nie są jeszcze dla każdego z tych wszystkich partnerów, jest jednak jako radością, ponieważ nie jesteśmy o nowe podejście.

* Team Foundation Service - działają wywołaniu integrację `nuget.exe restore` w domyślnej kompilacji scenariuszy.
* Windows Azure Web Sites - działają pozwala push projektu na platformie Azure i mają `nuget.exe restore` wywoływana przed wykonaniem działania witryny sieci web jest wbudowana.
* TeamCity - aktualizują ich wtyczki Instalatora NuGet dla TeamCity 8.x
* AppHarbor - działają umożliwia wypychanie Twojego repozytorium do AppHarbor i mieć `nuget.exe restore` wywołać budowania rozwiązania.

Z każdą z powyższych partnerów użyje ich własnych kopię nuget.exe i nie będzie potrzebny do przenoszenia nuget.exe w rozwiązaniu.

#### <a name="known-issues"></a>Znane problemy

Wystąpiły dwa znane problemy dotyczące przywracania nuget.exe w wersji 2.7 początkowej, ale zostały one ustalone na 9/6/2013 z aktualizacją do [pakietu NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/).  Ta aktualizacja jest dostępna również na [stronę pobierania NuGet 2.7](https://nuget.codeplex.com/releases/view/107605) w witrynie CodePlex.  Uruchomiona `nuget.exe update -self` aktualizację do najnowszej wersji.

Zostały usunięte:

1. [Nowe przywracanie pakietów nie działa w Mono przy użyciu pliku SLN](https://nuget.codeplex.com/workitem/3596)
1. [Nowe przywracanie pakietów nie działa z projektami Wix](https://nuget.codeplex.com/workitem/3598)

Istnieje również znany problem dotyczący nowego przepływu pracy przywracania pakietu zgodnie z którymi [automatyczne przywracanie pakietów nie działa dla projektów w folderze rozwiązania](https://nuget.codeplex.com/workitem/3625). Ten problem został rozwiązany w NuGet 2.7.1.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Przekierowania projektu i uaktualniania kompilacji błędy lub ostrzeżenia

Wiele razy po przekierowania lub uaktualniania projektu, można znaleźć niektórych pakietów NuGet nie działa prawidłowo. Niestety nie są oznaki pojawia się i to nie ma żadnej wskazówki dotyczące jego rozwiązania. Z NuGet 2.7 używamy teraz niektóre zdarzenia programu Visual Studio to rozpoznanie zostały przekierować lub uaktualnić projekt w taki sposób, który ma wpływ na zainstalowanych pakietów NuGet.

Firma Microsoft wykrywać wszelkie pakiety zostały zainfekowane przez przekierowania lub uaktualnienie, możemy wygenerowanie błędy kompilacji natychmiastowego z powiadomieniem. Oprócz błąd kompilacji natychmiastowego możemy także zachowanie `requireReinstallation="true"` oflagowane w Twojej `packages.config` pliku dla wszystkich pakietów, które były dotkniętych przekierowania i każdego kolejnego kompilacji w programie Visual Studio zostanie podniesiony ostrzeżeń kompilacji dla tych pakietów.

Mimo że NuGet nie może automatycznie podjąć odpowiednie działania, aby ponownie zainstalować odpowiednich pakietów, mamy nadzieję, że to wskazanie i ostrzeżenie przeprowadzi pomocy odkrywasz, kiedy trzeba ponownie zainstaluj pakiety. Również pracujemy nad [dokumentacji wskazówki dotyczące jego ponowna instalacja pakietu](../consume-packages/reinstalling-and-updating-packages.md) te komunikaty o błędach bezpośrednie do.

### <a name="nuget-configuration-defaults"></a>Ustawienia domyślne konfiguracji NuGet

Wiele firm korzysta wewnętrznie NuGet, ale miały twardych czasu, przeprowadzi deweloperom korzystać źródła pakietów w wewnętrznej zamiast nuget.org. NuGet 2.7 wprowadzono funkcja domyślne ustawienia konfiguracji, która umożliwia domyślne komputera może być określony dla:

1. Włączonych źródeł pakietów
1. Źródła pakietów w zarejestrowany, ale wyłączone
1. Źródło wypychania nuget.exe domyślne

Każdy z tych teraz można skonfigurować w pliku w lokalizacji `%ProgramData%\NuGet\NuGetDefaults.Config`. Jeśli ten plik konfiguracji określa źródła pakietów, a następnie źródło pakietu nuget.org domyślne nie zostanie automatycznie zarejestrowany i te w `NuGetDefaults.Config` zostanie zarejestrowana, zamiast tego.

Gdy nie trzeba używać tej funkcji, oczekujemy firmom wdrażanie `NuGetDefaults.Config` pliki za pomocą zasad grupy.

*Należy pamiętać, że ta funkcja nigdy nie spowoduje, że źródło pakietu, który ma zostać usunięty z ustawień NuGet dewelopera. Oznacza to, że jeśli projektanta został już użyty NuGet i w związku z tym ma w źródle pakietów nuget.org zarejestrowany, jego nie zostaną usunięte po utworzeniu `NuGetDefaults.Config` pliku.*

Zobacz [domyślnie przyjmowana jest Konfiguracja NuGet](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) Aby uzyskać więcej informacji dotyczących tej funkcji.

### <a name="renaming-the-default-package-source"></a>Zmiana nazwy domyślnego źródła pakietu

NuGet zawsze został zarejestrowany o nazwie "NuGet oficjalnego źródła pakietu" wskazujący nuget.org źródło pakietu domyślne. Ta nazwa została pełne i go również nie określono gdzie została faktycznie wskazujące. W celu rozwiązania tych dwóch problemów, firma Microsoft już zmienić nazwy tego źródła pakietu w celu po prostu "nuget.org" w interfejsie użytkownika. Adres URL źródła pakietu również została zmieniona na obejmują "www". prefiks. Po użyciu NuGet 2.7, istniejące "NuGet pakietu oficjalnego źródła", zostaną automatycznie zaktualizowane do "nuget.org", jak jego nazwa i "https://www.nuget.org/api/v2/" jako adresu URL.

### <a name="performance-improvements"></a>Usprawnienia wydajności

Wprowadziliśmy niektórych zwiększenie wydajności w 2.7, która umożliwia uzyskanie mniejsze zużycie pamięci, mniej użycia dysku i szybsze instalacji pakietu aktualizacji. Wprowadziliśmy również inteligentny zapytań OData na podstawie źródeł, co zmniejsza ogólną ładunku.

### <a name="new-extensibility-apis"></a>Nowe interfejsy API rozszerzalności

Niektóre z nowych interfejsów API dodane do naszych usług rozszerzalności, aby wypełnić przerwa brakujące funkcje w poprzednich wersjach.

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

### <a name="development-only-dependencies"></a>Tylko do rozwoju zależności

Ta funkcja została przekazanych przez [Adam Ralph](https://twitter.com/adamralph) i umożliwia autorom pakietu zadeklarować zależności, które były używane tylko w rozwoju czasu i nie wymagają zależności pakietów. Dodając `developmentDependency="true"` atrybutu do pakietu w `packages.config`, `nuget.exe pack` nie zawiera tego pakietu jako zależność.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Usunięta obsługa programu Visual Studio 2010 Express dla Windows Phone

Nowy model przywracania pakietu w 2.7 jest implementowany przez nowy pakiet VSPackage, który jest inny niż główny pakiet NuGet VSPackage. Z powodu problemu technicznego, to nowy pakiet VSPackage nie działa prawidłowo w *programu Visual Studio 2010 Express dla Windows Phone* SKU udostępniamy tej samej bazy kodu z innych obsługiwanych Visual Studio SKU. W związku z tym, począwszy od NuGet 2.7, możemy usuwanych obsługę *programu Visual Studio 2010 Express dla Windows Phone* z opublikowanego rozszerzenia. Obsługa *programu Visual Studio 2010 Express for Web* nadal znajduje się w rozszerzeniu podstawowe opublikowany w galerii rozszerzeń programu Visual Studio.

Ponieważ firma Microsoft nie wiesz, jak wielu deweloperów są nadal przy użyciu narzędzia NuGet w tej wersji/wydania programu Visual Studio, jesteśmy publikowanie osobnych rozszerzenie programu Visual Studio dla tych użytkowników i opublikować go w witrynie CodePlex (zamiast galerii rozszerzeń programu Visual Studio) . Firma Microsoft nie planuje Zachowaj tego rozszerzenia, ale jeśli ma to wpływ na możesz prosimy o kontakt przez składanie problemu w witrynie CodePlex.

Aby pobrać Menedżera pakietów NuGet (dla programu Visual Studio 2010 Express dla Windows Phone), odwiedź stronę [pobiera 2.7 NuGet](https://nuget.codeplex.com/releases/view/107605) strony.

### <a name="bug-fixes"></a>Poprawki błędów

Oprócz tych funkcji ta wersja programu NuGet zawiera również inne poprawki błędów. Znaleziono 97 całkowita problemy rozwiązane w wersji. Pełną listę prac elementów usunięto w wersji NuGet 2.7, sprawdź widok [NuGet Tracker problem w tej wersji](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
