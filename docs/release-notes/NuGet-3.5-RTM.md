---
title: Informacje o wersji narzędzia NuGet 3,5 RTM
description: Informacje o wersji programu NuGet 3,5, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 158373fb62f57fe6947fb863a1eef8122399959a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776353"
---
# <a name="nuget-35-release-notes"></a>Informacje o wersji narzędzia NuGet 3,5

Pakiet [NuGet 3,5 — informacje](../release-notes/nuget-3.5-RC.md)  |  o wersji RC [Informacje o wersji narzędzia NuGet 4,0 RC](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Poprawki błędów

* Pakiet nie używa programu MSBuild 14,1 w programie mono- [#3550](https://github.com/NuGet/Home/issues/3550)

* Na karcie aktualizacja nie jest wybrana najnowsza dostępna wersja, która ma zostać zaktualizowana, a zamiast tego wybierana jest bieżąca zainstalowana wersja — [#3498](https://github.com/NuGet/Home/issues/3498)

* Napraw awarię po uwierzytelnieniu prywatnego źródła danych w wersji 2 MyGet i kliknięciu pozycji "Pokaż x więcej wyników" — [#3469](https://github.com/NuGet/Home/issues/3469)

* Komunikaty dziennika pozornie są uporządkowane w kolejności odwrotnej dla interfejsu użytkownika [#3446](https://github.com/NuGet/Home/issues/3446)

* v 3.4.4 — Przywracanie NuGet zgłasza "format danego ścieżki nie jest obsługiwany"- [#3442](https://github.com/NuGet/Home/issues/3442)

* Pakiet NuGet Cmdlines 3,6 beta nie jest zgodny z konfiguracją = Release- [#3432](https://github.com/NuGet/Home/issues/3432)

* Powolna instalacja narzędzia NuGet IKVM na dużym projekcie — [#3428](https://github.com/NuGet/Home/issues/3428)

* nuget.exe Update — umożliwia samodzielną aktualizację [#3395](https://github.com/NuGet/Home/issues/3395)

* 3,5 Zainstaluj/Przywróć z udziału UNC ma regresję wydajności z 3.4.4 — [#3355](https://github.com/NuGet/Home/issues/3355)

* Wystąpił błąd podczas instalowania MOQ z interfejsu użytkownika zarządzania pakietami dla projektu net451 — [#3349](https://github.com/NuGet/Home/issues/3349)

* Karta Instalacja na poziomie rozwiązania nie wyświetla wersji [#3339](https://github.com/NuGet/Home/issues/3339) pakietu

* `project.json`Aktualizacja xproj z zainstalowanej karty traci stan- [#3303](https://github.com/NuGet/Home/issues/3303)

* Pakiet NuGet w przypadku `.csproj` ignorowania pustego elementu Files w `.nuspec` pliku- [#3257](https://github.com/NuGet/Home/issues/3257)

* Projekty witryn sieci Web hostowane w usługach IIS nie powinny spowodować niepowodzenia przywracania [#3235](https://github.com/NuGet/Home/issues/3235)

* Nie pobrano poświadczeń z Nuget.Config po przekierowaniu punktu końcowego v3 do wersji 2- [#3179](https://github.com/NuGet/Home/issues/3179)

* Pakiet NuGet nie może rozpoznać zestawu podczas pobierania metadanych zestawu przenośnego — [#3128](https://github.com/NuGet/Home/issues/3128)

* Pakiet NuGet nie może znaleźć `msbuild.exe` na mono- [#3085](https://github.com/NuGet/Home/issues/3085)

* Pakiet nuget.exe nie zezwala na tag w wersji wstępnej zaczynający się od cyfr- [#1743](https://github.com/NuGet/Home/issues/1743)

* Instalacja pakietu NuGet kończy się niepowodzeniem na VS2015E- [#1298](https://github.com/NuGet/Home/issues/1298)

* Filtr allowedVersions nie działa na poziomie rozwiązania — [#333](https://github.com/NuGet/Home/issues/333)

* Operacja przywracania losowo kończy się niepowodzeniem z elementem z tym samym kluczem, który został już dodany. - [#2646](https://github.com/NuGet/Home/issues/2646)

* Nie można zainstalować NuGet. Common w `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* W przypadku używania interfejsu użytkownika do wyszukiwania źródła w wersji 2 FindPackagesById jest wywoływana dwa razy dla każdego identyfikatora — [#2517](https://github.com/NuGet/Home/issues/2517)

* Pakiety nie mogą zależeć od projektów — [#2490](https://github.com/NuGet/Home/issues/2490)

* Pakiet nuget.exe — wykluczenie jest udokumentowane, ale nie jest obsługiwane — [#2284](https://github.com/NuGet/Home/issues/2284)

* Problemy z komunikatami o błędach, gdy sekcja "contentFiles" `.nuspec` jest nieprawidłowa — [#1686](https://github.com/NuGet/Home/issues/1686)

* Wypychanie zawsze wysyła cały pakiet z uwierzytelnionymi źródłami pakietów — [#1501](https://github.com/NuGet/Home/issues/1501)

* Nie podano informacji podczas wywoływania nuget.exe Update *. csproj, gdy projekt nie ma `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config` instrukcja RESTORE nie ponawia próby dla kodów stanu 5xx ze źródeł v2 — [#1217](https://github.com/NuGet/Home/issues/1217)

* Podwójna kropka w pliku SRC `.nuspec` nie działa — [#2947](https://github.com/NuGet/Home/issues/2947)

* Przywracanie CoreCLR musi ignorować kanały informacyjne z szyfrowaniem [#2942](https://github.com/NuGet/Home/issues/2942)

* nuget.exe obsługi wypychania 403 — nieprawidłowo Monituj o poświadczenia — [#2910](https://github.com/NuGet/Home/issues/2910)

* Aktualizacja NuGet za pomocą Menedżera pakietów usuwa właściwości z `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)

* NuGet. PackageManagement. VisualStudio spróbuj załadować "NuGet. TeamFoundationServer14", ale nazwa biblioteki DLL została zmieniona na "NuGet. TeamFoundationServer"- [#2857](https://github.com/NuGet/Home/issues/2857)

* Interfejs użytkownika Menedżera pakietów nie wyświetla nowo zaktualizowanej wersji — [#2828](https://github.com/NuGet/Home/issues/2828)

* Update-pakiet próbuje użyć PackageID, Version zamiast Package. Version- [#2771](https://github.com/NuGet/Home/issues/2771)

* CSPROJ przywracania NuGet powinien błąd, jeśli projekt nie korzysta z NuGet ( `packages.config` lub `project.json` )- [#2766](https://github.com/NuGet/Home/issues/2766)

* Błąd TFS "[plik] nie został znaleziony w Twoim obszarze roboczym lub nie masz uprawnień dostępu do niego" podczas uaktualniania lub odinstalowywania, gdy rozwiązanie/projekt jest powiązane z kontrolą źródła TFS- [#2739](https://github.com/NuGet/Home/issues/2739)

* pakiet aktualizacji nie pobiera zależności dla pakietów innych niż docelowe — [#2724](https://github.com/NuGet/Home/issues/2724)

* Nie ma możliwości ustawienia poziomu szczegółowości dzienników dla akcji interfejsu użytkownika Menedżera pakietów NuGet — [#2705](https://github.com/NuGet/Home/issues/2705)

* Konfiguracja NuGet jest nieprawidłowa — VS 2015 VSIX (v 3.4.3) — [#2667](https://github.com/NuGet/Home/issues/2667)

* DefaultPushSource w `NuGetDefaults.Config` ( `ProgramData\NuGet` ) nie działa — [#2653](https://github.com/NuGet/Home/issues/2653)

* wydanie NuGet 3.4.3 — pobieranie wartości nie może mieć wartości null w kompilacji pakietu- [#2648](https://github.com/NuGet/Home/issues/2648)

* Przywracanie nie używa przechowywanych poświadczeń z Nuget.Config dla źródeł danych VSTS — [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet restore] — ConfigFile jest względem projektu dir zamiast cmd dir- [#2639](https://github.com/NuGet/Home/issues/2639)

* Nadmierne alokacje w wersji comparsion Code- [#2632](https://github.com/NuGet/Home/issues/2632)

* Wiele wystąpień nuget.exe próbuje zainstalować ten sam pakiet równolegle powoduje podwójny zapis [#2628](https://github.com/NuGet/Home/issues/2628)

* Informacje o zależnościach nie są buforowane dla operacji wieloprojektowych — [#2619](https://github.com/NuGet/Home/issues/2619)

* Zainstaluj i zaktualizuj pakiety pobierania bez sprawdzania folderu Packages First- [#2618](https://github.com/NuGet/Home/issues/2618)

* Jeśli lista źródeł pakietów jest pusta, nie można dodać źródła pakietu za pośrednictwem interfejsu użytkownika (NuGet 3.4. x) — [#2617](https://github.com/NuGet/Home/issues/2617)

* Błąd mylący podczas próby zainstalowania pakietu, który zależy od [#2594](https://github.com/NuGet/Home/issues/2594) fasad czasu projektowania

* Instalowanie pakietu z konsoli pakietu Packagemanager z ustawieniem "All" powoduje tylko próbę pierwszego źródła — [#2557](https://github.com/NuGet/Home/issues/2557)

* Najnowsza wersja beta nie rozpakować ModernHttpClient — [#2518](https://github.com/NuGet/Home/issues/2518)

* PROGRAMU VS2015 awarię przy uruchamianiu przy użyciu wbudowanego narzędzia NuGetobject- [#2419](https://github.com/NuGet/Home/issues/2419)

* Polecenie Update może być nieco bardziej pełne, jeśli poprosił o to...- [#2418](https://github.com/NuGet/Home/issues/2418)

* Program VSIX utworzony lokalnie powinien mieć te same biblioteki DLL i pliki co kompilacja elementu konfiguracji. - [#2401](https://github.com/NuGet/Home/issues/2401)

* Napraw ostrzeżenia o obniżeniu poziomu NuGet w [#2396](https://github.com/NuGet/Home/issues/2396) kompilacji

* Niepowodzenie uwierzytelniania źródła pakietów (3 razy) jest blokowane w nieskończoność — [#2362](https://github.com/NuGet/Home/issues/2362)

* Zawartość pakietu nie jest przywracana poprawnie podczas instalowania pakietu z programu NuGet v 3.3 + ze źródła danych argument-nocache, gdy pakiet zawiera `.nupkg` pliki- [#2354](https://github.com/NuGet/Home/issues/2354)

* Instalacja narzędzia NuGet ze wszystkimi źródłami pakietów, ale brakuje pakietu z 1 źródła, kończy się niepowodzeniem — [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet. PackageManagement. VisualStudio. VSMSBuildNuGetProjectSystem + * lt; &gt; c__DisplayClass_0 i &lt; &lt; addreference &gt; B__ &gt; d. MoveNext- [#2285](https://github.com/NuGet/Home/issues/2285)

* Zainstaluj bloki w przypadku niepowodzenia autoryzacji pojedynczego źródła — [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` zakres wersji powinien przesłonić IncludeReferencedProjects wersji [#1983](https://github.com/NuGet/Home/issues/1983)

* Update-Package bardzo wolno — "próba zebrania informacji o zależnościach" — [#1909](https://github.com/NuGet/Home/issues/1909)

* Pakiet NuGet niewidzialnego obniżenia poziomu przy aktualizacji wsadowej — [#1903](https://github.com/NuGet/Home/issues/1903)

* nuget.exe Update odrzuca silną nazwę i atrybut prywatny zestawu. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Względna ścieżka pliku dla "DefaultPushSource" — [#1746](https://github.com/NuGet/Home/issues/1746)

* Optymalizowanie komunikatów o błędach programu rozpoznawania nazw — [#1373](https://github.com/NuGet/Home/issues/1373)

* pakiet aktualizacji w wersji v3 kończy się niepowodzeniem z pakietami spoza określonego źródła — [#1013](https://github.com/NuGet/Home/issues/1013)

* Używanie ścieżek względnych dla źródeł pakietów jest problematyczne do użycia- [#865](https://github.com/NuGet/Home/issues/865)

* Brakująca zależność w NUPKG — plik wygenerowany z projektu, jeśli zależność pośrednia już istnieje o niższej wersji — [#759](https://github.com/NuGet/Home/issues/759)

* Usunięcie projektu powoduje zamknięcie odpowiedniego okna interfejsu użytkownika, ale zmiana nazwy projektu nie powoduje zmiany nazwy okna interfejsu użytkownika. Należy zauważyć, że PMC nasłuchuje w celu zmiany nazwy projektu i zdarzeń usunięcia projektu — [#670](https://github.com/NuGet/Home/issues/670)

* [Willow obciążenia sieci Web] Tworzenie zawieszeń z aparatu Razor v3 — [#3241](https://github.com/NuGet/Home/issues/3241)

* Instalacja/przywracanie określonego pakietu kończy się niepowodzeniem z "pakiet zawiera wiele plików nuspec". - [#3231](https://github.com/NuGet/Home/issues/3231)

* Małe identyfikatory & `packages.config` scenariusze — [#3209](https://github.com/NuGet/Home/issues/3209)

* [3,5-beta2] Przywracanie pakietu nie może przywrócić "starszych" pakietów — [#3208](https://github.com/NuGet/Home/issues/3208)

* Pakiet NuGet wymusza dodanie plików TT do folderu Content niezależnie od tego, co [#3203](https://github.com/NuGet/Home/issues/3203)

* Funkcja Update-Package programu ASP.NET Web App generuje ostrzeżenie związane z plikiem: Source- [#3194](https://github.com/NuGet/Home/issues/3194)

* Pakiet NuGet csproj (z `project.json` ) ulega awarii, jeśli nie ma packOptions i właściciela w pliku JSON — [#3180](https://github.com/NuGet/Home/issues/3180)

* Pakiet NuGet dla `project.json` ignorowania tagów packOptions, takich jak podsumowanie, autorzy, właściciele itp., [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException za pośrednictwem NuGet. pakowanie. PhysicalPackageFile. GetStream- [#3160](https://github.com/NuGet/Home/issues/3160)

* Pakiet NuGet ignoruje zależności w danych wyjściowych `.nuspec` dla `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Aktualizacja wielu pakietów z wycofywaniem pozostawia projekt w stanie przerwania — [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles w obszarze any nie są dodawane do projektów standardowych, [#3118](https://github.com/NuGet/Home/issues/3118)

* Nie można prawidłowo spakować biblioteki dla platformy .NET standard- [#3108](https://github.com/NuGet/Home/issues/3108)

* Plik > nowy projekt — > Biblioteka klas (przenośna) kończy się niepowodzeniem w programu VS2015 i Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)

* błąd nuGet-1.0.0-* nie jest prawidłowym ciągiem wersji- [#3070](https://github.com/NuGet/Home/issues/3070)

* Nie można wyświetlić Find-Package, ale Install-Package działa [#3068](https://github.com/NuGet/Home/issues/3068)

* Błąd podczas "Install-Package jQuery. Validation" w dev15- [#3061](https://github.com/NuGet/Home/issues/3061)

* Pakiet NuGet xproj ma domyślnie wartość nieprawidłowa ścieżka docelowa — [#3060](https://github.com/NuGet/Home/issues/3060)

* Po zainstalowaniu programu VS 2015 Update 3 w programie VS, który korzysta z 3.5.0 w wersji NuGet, występuje błąd- [#3053](https://github.com/NuGet/Home/issues/3053)

* "Zablokowane przez packages.config" w `project.json` (platformy UWP, a. k. a kompilacja zintegrowana) projekt — [#3046](https://github.com/NuGet/Home/issues/3046)

* Zaktualizuj interfejs wiersza polecenia dotnet instalowany przez skrypt kompilacji do preview2-003121, który jest oficjalną kompilacją preview2. - [#3045](https://github.com/NuGet/Home/issues/3045)

* Interfejs użytkownika Menedżera pakietów: nie wyświetla nowej wersji po zaktualizowaniu pakietu — [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey w wierszu polecenia usuwania nie jest odczytywany/wysyłany w 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* Niepoprawny ciąg: stabilna wersja pakietu nie powinna mieć w zależności od wersji wstępnej. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Pamięć podręczna OptimizedZipPackage pozostawia puste foldery — [#3029](https://github.com/NuGet/Home/issues/3029)

* Tworzenie wyjątku NullRef w projekcie PCL (net46 i Windows 10). - [#3014](https://github.com/NuGet/Home/issues/3014)

* Aktualizacja NuGet powinna podawać komunikat informacyjny, gdy wyższa wersja jest ograniczona przez ograniczenie allowedVersions — [#3013](https://github.com/NuGet/Home/issues/3013)

* Problemy z przywracaniem NuGet v3 — [#2891](https://github.com/NuGet/Home/issues/2891)

* Wtyczka poświadczeń została zakończona z błędem-1/Pobieranie pakietu podczas korzystania z dostawców poświadczeń z wieloma źródłami — [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json` Przywracanie NuGet powoduje ponowną kompilację, gdy nic się nie zmieniło — [#2817](https://github.com/NuGet/Home/issues/2817)

* Pakiety symboli nie powinny być używane w instalacji ani aktualizacji- [#2807](https://github.com/NuGet/Home/issues/2807)

* Program VS nie obsługuje zmiennych środowiskowych w programie repositoryPath (nuget.exe) — [#2763](https://github.com/NuGet/Home/issues/2763)

* Oznacz nieoznaczone elementy UIElement w interfejsie użytkownika Menedżera pakietów na potrzeby ułatwień dostępu [#2745](https://github.com/NuGet/Home/issues/2745)

* Platformy przenośne z zadzielonymi profilami są odrzucane. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Menedżer pakietów NuGet powinien wyczyścić, że lista opcji w szczegółach pakietów nie ma zastosowania do `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* nuget.exe push/Delete nie będzie używać klucza interfejsu API [#2627](https://github.com/NuGet/Home/issues/2627)

* Usuń zablokowaną właściwość z pliku blokady — [#2379](https://github.com/NuGet/Home/issues/2379)

* Aktualizacja NuGet 3.3.0 kończy się niepowodzeniem z "dodatkowym ograniczeniem... zdefiniowane w packages.config uniemożliwia wykonanie tej operacji ". - [#1816](https://github.com/NuGet/Home/issues/1816)

* Instalowanie pakietu z lokalnego źródła, które nie istnieje, zgłasza fałszywe wiadomości [#1674](https://github.com/NuGet/Home/issues/1674)

* Filtr "dostępne uaktualnienie" zawiera uaktualnienia, które naruszają ograniczenie wersji — [#1094](https://github.com/NuGet/Home/issues/1094)

* Nie można zaktualizować pakietów natywnych — [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>Funkcje

* Obsługa ustawienia CopyLocal na wartość false w odwołaniach dodanych przez NuGet- [#329](https://github.com/NuGet/Home/issues/329)

* nuget.exe obsługa programu MSBuild 15 — [#1937](https://github.com/NuGet/Home/issues/1937)

* Obsługa pakietu dla programu.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* Wyłącz akcję użytkownika, gdy są wykonywane akcje użytkownika — [#1440](https://github.com/NuGet/Home/issues/1440)

* Pakiet NuGet powinien dodać obsługę `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* W programie NuGet 2. x brakuje niezgodności struktur, które znajdują się już w 3. x) — [#2720](https://github.com/NuGet/Home/issues/2720)

* Obsługa folderów pakietów powrotu — [#2899](https://github.com/NuGet/Home/issues/2899)

* Projektuj i Implementuj pojęcie typu pakietu do obsługi pakietów narzędzi — [#2476](https://github.com/NuGet/Home/issues/2476)

* Dodaj interfejs API, aby uzyskać ścieżkę do folderu pakietów globalnych — [#2403](https://github.com/NuGet/Home/issues/2403)

* Włączanie SemVer 2.0.0 w pakiecie Pack- [#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>DCR

* nuget.exe parametr limitu czasu wypychania nie działa — [#2785](https://github.com/NuGet/Home/issues/2785)

* Tekst opisu pakietu powinien być wybrany- [#1769](https://github.com/NuGet/Home/issues/1769)

* Włącz nuget.exe do produkcji `.props` i `.targets` plików dla `.nuproj` projektów [#2711](https://github.com/NuGet/Home/issues/2711)

* Dodawanie interfejsu API rozszerzalności do porównywania platform z importami — [#2633](https://github.com/NuGet/Home/issues/2633)

* Ukryj Opcje zależności przy użyciu `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Drukuj nagłówek nuget.exe wersji w szczegółowych danych wyjściowych — [#1887](https://github.com/NuGet/Home/issues/1887)

* Pakiet NuGet musi poinformować użytkowników, że uaktualnianie/Instalowanie w formacie PCL opartym na platformie dotnet TFM może powodować problemy — [#3138](https://github.com/NuGet/Home/issues/3138)

* Ostrzegaj o złej instalacji/uaktualnieniu dla projektu w/TFM = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* Rozwiązywanie problemów z wydajnością za pomocą Przekształć i narzędzia NuGet na potrzeby aktualizacji [#3044](https://github.com/NuGet/Home/issues/3044)

* Dodawanie obsługi netcoreapp11 i netstandard17 — [#2998](https://github.com/NuGet/Home/issues/2998)

* Wykorzystanie atrybutu AssemblyMetadata dla `.nuspec` zamiany tokenów — [#2851](https://github.com/NuGet/Home/issues/2851)
