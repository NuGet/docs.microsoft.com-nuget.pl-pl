---
title: Informacje o wersji narzędzia NuGet 4,0 RTM
description: Informacje o wersji dla programu NuGet 4,0 RTM, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: anangaur
ms.author: anangaur
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: c3ec5c20e5175edd315de20ca98c7a106c51809e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776277"
---
# <a name="nuget-40-rtm-release-notes"></a>Informacje o wersji narzędzia NuGet 4,0 RTM

[Program Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z pakietem NuGet 4,0, który dodaje obsługę platformy .NET Core, ma wiele poprawek dotyczących jakości i poprawia wydajność. W tej wersji wprowadzono również kilka ulepszeń, takich jak obsługa PackageReference, poleceń NuGet jako obiektów docelowych programu MSBuild, przywrócenie pakietu w tle i nie tylko.

## <a name="known-issues"></a>Znane problemy

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a>Przywracanie pakietów NuGet może się nie powieść, jeśli masz wiele projektów odwołujących się do innego projektu w rozwiązaniu

#### <a name="issue"></a>Problem

Przywracanie pakietów NuGet może nie działać, jeśli w rozwiązaniu istnieją odwołania do projektu do tego samego projektu z inną wielkością liter lub innymi ścieżkami względnymi. [NuGet#4574](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a>Obejście

Napraw wielkość liter lub ścieżki względne w taki sposób, aby były takie same dla wszystkich odwołań do projektu.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Podczas korzystania z konsoli Menedżera pakietów może nie działać klawisz „Enter”

#### <a name="issue"></a>Problem

Czasami klawisz Enter nie działa w konsoli Menedżera pakietów. Jeśli tak się dzieje, sprawdź postęp poprawki i podaj wszystkie przydatne informacje dodatkowe dotyczące kroków odtwarzania. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Obejście

Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania. Alternatywnie spróbuj usunąć `project.lock.json` i przywrócić ponownie.

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a>W projektach .NET Core użytkownik może pozostać w pętli nieskończonej przywracania w przypadku użycia pakietu zawierającego zestaw z nieprawidłowym podpisem

#### <a name="issue"></a>Problem

Czasami, w przypadku użycia pakietu zawierającego zestaw z nieprawidłowym podpisem lub gdy wersja pakietu została ustawiona za pomocą znacznika „DateTime”, automatyczne przywracanie pakietu będzie uruchamiane w pętli nieskończonej. [NuGet#4542](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a>Obejście

Obecnie nie istnieje obejście tego problemu.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Nie można wyświetlać, dodawać ani aktualizować składnika dotnetclitools przy użyciu Menedżera pakietów NuGet

#### <a name="issue"></a>Problem

Menedżer pakietów NuGet nie wyświetla składnika DotNetCLITools ani nie zezwala na jego dodawanie/aktualizowanie. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Obejście

Należy ręcznie edytować składnik DotNetCLIToolReferences w pliku projektu.

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a>Przywracanie NuGet zakończy się niepowodzeniem po ustawieniu właściwości PackageId dla projektów

#### <a name="issue"></a>Problem

Dla projektów .NET Core funkcja przywracania NuGet w programie Visual Studio nie przestrzega właściwości PackageId projektów. [NuGet#4586](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a>Obejście

Uruchom przywracanie przy użyciu wiersza polecenia.

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a>Gdy projekt nie ma folderu „obj”, przywracanie pakietu może zakończyć się niepowodzeniem

#### <a name="issue"></a>Problem

Program Visual Studio nie może przywrócić składnika PackageReferences, jeśli folder „obj” został usunięty. [NuGet#4528](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a>Obejście

Gdy utworzysz folder „obj” ręcznie, funkcja przywracania powinna zadziałać.

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a>Ręczna aktualizacja pakietów przy użyciu pakietu aktualizacji w konsoli może zakończyć się niepowodzeniem

#### <a name="issue"></a>Problem

Ręczne użycie pakietu aktualizacji w konsoli działa tylko jeden raz dla projektów PackageReferences, które zostały właśnie przekonwertowane. [NuGet#4431](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a>Obejście

Obecnie nie istnieje obejście tego problemu.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense

#### <a name="issue"></a>Problem

Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense w programie Visual Studio. Dzieje się tak w przypadku używania składnika PackageReferences jako formatu Menedżera pakietów. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Obejście

Wykonaj przywracanie ręczne.

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a>Działanie polecenia msbuild /t:restore kończy się niepowodzeniem, gdy projekt przeznaczony dla platformy .NET461 odwołuje się do innego projektu przeznaczonego dla platformy .NETStandard

#### <a name="issue"></a>Problem

Działanie polecenia msbuild /t:restore kończy się niepowodzeniem, gdy projekt oparty na składniku PackageReferenece przeznaczony dla platformy .NET461 odwołuje się do innego projektu opartego na składniku PackageReference przeznaczonego dla platformy .NETStandard.  [NuGet#4532](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a>Obejście

Obecnie nie istnieje obejście tego problemu.

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a>Problemy rozwiązane w przedziale czasu NuGet 4,0 RTM

[Informacje o wersji programu nuget 4,0 RC](../release-notes/nuget-4.0-RC.md) — zawiera listę wszystkich problemów rozwiązanych dla programu NuGet 4,0 RC

### <a name="features"></a>Funkcje

- Lokalizowanie ciągów w NuGet. Core. sln- [#2041](https://github.com/NuGet/Home/issues/2041)

- Siły NuGet do ładowania projektów aplikacji sieci Web w trybie SKRÓCONO — [#4258](https://github.com/NuGet/Home/issues/4258)

- Obsługa PackageReference, która blokuje zmiany wersji w interfejsie użytkownika dla pakietów "zainstalowane w zestawie SDK" — [#4044](https://github.com/NuGet/Home/issues/4044)

- Poprawnie komunikuj PackageSpec. Version dla dowolnych zależności projektu (PackageRef) — [#3902](https://github.com/NuGet/Home/issues/3902)

- obsługa usuwania odwołań do `.csproj` z wierszy polecenia — [#4101](https://github.com/NuGet/Home/issues/4101)

- Obsługa przywracania projektów PackageReference (normalne i Xplat) i uproszczonego ładowania rozwiązań — [#4003](https://github.com/NuGet/Home/issues/4003)

- Obsługa dodawania odwołań do `.csproj` z wiersza polecenia — [#3751](https://github.com/NuGet/Home/issues/3751)

- Obsługa przywracania NuGet na potrzeby uproszczonego ładowania rozwiązań dla programu `packages.config` lub `project.json`  -  [#3711](https://github.com/NuGet/Home/issues/3711)

- Obsługa contentFiles w pliku docelowych wygenerowanych przez narzędzie NuGet — [#3683](https://github.com/NuGet/Home/issues/3683)

- Ustanawianie elementu konfiguracji mono dla nuget.exe weryfikacji na komputerze Mac przy użyciu programu MSBuild — [#3646](https://github.com/NuGet/Home/issues/3646)

- Przenoszenie narzędzia NuGet z wersji 2 programu NuGet. zależności podstawowe — [#3645](https://github.com/NuGet/Home/issues/3645)

### <a name="bugs"></a>Usterki

- Przywracanie NuGet w programie Visual Studio nie uwzględnia właściwości PackageId projektów — [#4586](https://github.com/NuGet/Home/issues/4586)

- Błąd narzędzia NuGet ProjectSystemCache podczas dodawania pakietu w pakiecie VSIX — [#4545](https://github.com/NuGet/Home/issues/4545)

- Pakiet zgłasza wyjątek, jeśli IncludeSource jest używany w projekcie z wieloma TFMs- [#4536](https://github.com/NuGet/Home/issues/4536)

- VS 2017 RC3 awarie przy użyciu aktualizacji z zarządzania pakietami w całym rozwiązaniu — [#4474](https://github.com/NuGet/Home/issues/4474)

- Nie można odinstalować nowo zainstalowanego pakietu — [#4435](https://github.com/NuGet/Home/issues/4435)

- W przypadku migrowania do PackageRef rozwiązania hybrydowe mają nietypowe zachowanie przywracania — [#4433](https://github.com/NuGet/Home/issues/4433)

- Kompilowanie wkrótce po uruchomieniu operacji NuGet (Install, Update, Restore), może spowodować zawieszenie [#4420](https://github.com/NuGet/Home/issues/4420)

- Zawieszanie zawieszenia interfejsu użytkownika podczas inicjowania NuGet. SolutionRestoreManager. RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)

- polecenie Dodaj pakiet powinno dodać wersję jako atrybut zamiast elementu [#4325](https://github.com/NuGet/Home/issues/4325)

- dotnet
  - dotnetcore Restore foo. sln--kończy się niepowodzeniem, jeśli konfiguracje w SLN powodują zduplikowane projekty (ale różnice konfiguracji) w programie Restore Graph- [#4316](https://github.com/NuGet/Home/issues/4316)

- Pakiety tylko zawartości — [#3668](https://github.com/NuGet/Home/issues/3668)

- Domyślnie zrezygnuj z opcji selektora formatu pakietu — [#4468](https://github.com/NuGet/Home/issues/4468)

- Wydajność: CreateUAP_CSharp_VS. 01.1. Create Project uległa pogorszeniu Duration_TotalElapsedTime o 3 153,570 MS (149,1%). Linia bazowa 26129,02- [#4452](https://github.com/NuGet/Home/issues/4452)

- Wydajność: ManagedLangs_CS_DDRIT .0300. Rebuild rozwiązanie uległa pogorszeniu Duration_TotalElapsedTime o 1,5 sek. Linia bazowa 26105- [#4441](https://github.com/NuGet/Home/issues/4441)

- Nominacja nie powiedzie się w projektach wieloTFMowych — [#4419](https://github.com/NuGet/Home/issues/4419)

- Wydajność: WebForms_DDRIT .1200. Zamknij rozwiązanie uległa pogorszeniu VM_ImagesInMemory_Total_devenv według liczby 3,000 (0,5%). Linia bazowa 26123,04- [#4408](https://github.com/NuGet/Home/issues/4408)

- vsfeedback — ostrzeżenia dotyczące pakietów podczas określania wartości docelowej netcoreapp [#4397](https://github.com/NuGet/Home/issues/4397) 1.1

- PathTooLongException podczas próby dodania pakietu NuGet do pustej ASP.NET Core aplikacji sieci Web — [#4391](https://github.com/NuGet/Home/issues/4391)

- Pakiet jest uruchamiany zbyt często — dotnet
  - Pakiet dotnetcore kończy się niepowodzeniem, gdy istnieje zależność cykliczna w docelowym grafie zależności obejmująca element docelowy "Pack" — [#4381](https://github.com/NuGet/Home/issues/4381)

- Pakiet jest uruchamiany zbyt często — Generowanie pakietu NuGet nie obejmuje wszystkich konfiguracji — [#4380](https://github.com/NuGet/Home/issues/4380)

- NullReferenceException Dodawanie NuGet z packageref w projekcie C++ — [#4378](https://github.com/NuGet/Home/issues/4378)

- Ułatwienia dostępu: program Narrator nie narratoruje tego pola wyboru, aby wybrać projekty, do których ma zostać zainstalowany pakiet- [#4366](https://github.com/NuGet/Home/issues/4366)

- VS17 NuGet sporadycznie nie może nawiązać połączenia ze źródłami VSO/VSTS — Usterka programu VS 365798 — [#4365](https://github.com/NuGet/Home/issues/4365)

- contentFiles uzyskać dane wyjściowe do nieprawidłowej lokalizacji, jeśli PackagePath określa ścieżkę jako "contentFiles"- [#4348](https://github.com/NuGet/Home/issues/4348)

- Element docelowy Pack dołącza Właściwość PackageVersion z VersionSuffix- [#4324](https://github.com/NuGet/Home/issues/4324)

- Określanie ścieżki pakietu nie działa z pakietem dotnet Pack — [#4321](https://github.com/NuGet/Home/issues/4321)

- Pakiet NuGet wyprowadza wiele ostrzeżeń dotyczących zduplikowanych importów podczas przywracania [#4304](https://github.com/NuGet/Home/issues/4304)

- Wybierz opcję "format Menedżera pakietów NuGet" jest nieprawidłowy w przypadku motywu ciemny — [#4300](https://github.com/NuGet/Home/issues/4300)

- VS Crash podczas przywracania kompilacji — [#4298](https://github.com/NuGet/Home/issues/4298)

- Zakleszczenie programu Visual Studio w przypadku dodania TFM w targetframeworks, Zapisz, a następnie Skompiluj. 10% czasu [#4295](https://github.com/NuGet/Home/issues/4295)

- Pakiet NuGet nie wyprowadza komunikatu o powodzeniu w przypadku pomyślnego pakowania projektu — [#4294](https://github.com/NuGet/Home/issues/4294)

- PackTask nie powiodła się z powodu nieznalezienia metody System. IO. Compression 4,1- [#4290](https://github.com/NuGet/Home/issues/4290)

- Pakiet jest uruchamiany zbyt często — PackTask często kończy się niepowodzeniem z powodu konfliktu dostępu do plików — [#4289](https://github.com/NuGet/Home/issues/4289)

- Pakiet NuGet otwiera okno dane wyjściowe podczas przywracania w tle — [#4274](https://github.com/NuGet/Home/issues/4274)

- Eliminowanie jako wzorca kodowania niebezpiecznego (co może spowodować zawieszenie) — [#4268](https://github.com/NuGet/Home/issues/4268)

- Perf/UIHang — ulepszanie operacji odczytu DownloadTimeoutStream- [#4266](https://github.com/NuGet/Home/issues/4266)

- Zakleszczenie programu Visual Studio w przypadku próby zamknięcia projektu przed zakończeniem przywracania NuGet [#4257](https://github.com/NuGet/Home/issues/4257)

- Problemy z PackTask i pakowanie `.nuspec`  -  [#4250](https://github.com/NuGet/Home/issues/4250)

- [vsfeedback] Nie można rozpoznać pakietów NuGet w nowym projekcie (wymaga ponownego uruchomienia programu Visual Studio) — [#4217](https://github.com/NuGet/Home/issues/4217)

- [vsfeedback] Zostanie wyświetlona lista rozwijana "wersja", która zawiera dostępne wersje pakietów, co może pozostawać w synchronizacji z wybranym pakietem nuGet...- [#4198](https://github.com/NuGet/Home/issues/4198)

- Pakiet NuGet. Klient powinien używać JoinableTaskFactory CPS podczas współpracy z serwerem CPS, aby zapobiec zakleszczeniom — [#4185](https://github.com/NuGet/Home/issues/4185)

- Pakiet NuGet 3.5.0 nie rozpakować `.targets` z pakietu — [#4171](https://github.com/NuGet/Home/issues/4171)

- dotnet
  - Pakiet dotnetcore nie obsługuje tytułu w `.csproj`  -  [#4150](https://github.com/NuGet/Home/issues/4150)

- Install-Package wyniki w oknie dialogowym błędów w program VS2017 RC — [#4127](https://github.com/NuGet/Home/issues/4127)

- Aktualizacja pakietu dla projektu .NET Core prawdopodobnie nie działa, ponieważ interfejs użytkownika nie pobiera aktualizacji CPS z nominacji. - [#4035](https://github.com/NuGet/Home/issues/4035)

- Popraw nierozwiązane ostrzeżenie dotyczące odwołań — [#3955](https://github.com/NuGet/Home/issues/3955)

- dotnet
  - dotnetcore Pack — elementu ProjectReference utraci informacje o wersji — [#3953](https://github.com/NuGet/Home/issues/3953)

- Utwórz aplikację platformy UWP Utwórz projekt & ponownie skompilować łączny czas, który upłynął, [#3873](https://github.com/NuGet/Home/issues/3873)

- Komunikat o powodzeniu przywracania jest wyświetlany nawet po wystąpieniu błędu podczas przywracania. - [#3799](https://github.com/NuGet/Home/issues/3799)

- ponownie Opublikuj pakiet NuGet. CommandLine 3.4.4 do Nuget.org- [#2931](https://github.com/NuGet/Home/issues/2931)

- Po migracji projekty zmieniają się z `project.json` na `.csproj` ---przywracanie nie powiedzie się [#4297](https://github.com/NuGet/Home/issues/4297)

- Przywracanie nie powiodło się w przypadku nowo utworzonego projektu testowego xUnit — [#4296](https://github.com/NuGet/Home/issues/4296)

- Projekty podstawowe mogą zawieszać się, blokować interfejs użytkownika przy otwartym [#4269](https://github.com/NuGet/Home/issues/4269)

- Napraw plik elementów docelowych dla zadań kompilacji — [#4267](https://github.com/NuGet/Home/issues/4267)

- Lista błędów zawiera błąd po rozwiązaniu kompilacji, które zwalnia przywoływany projekt [#4208](https://github.com/NuGet/Home/issues/4208)

- MSB4057: element docelowy "_GenerateRestoreGraphProjectEntry" nie istnieje w projekcie. - [#4194](https://github.com/NuGet/Home/issues/4194)

- vsfeedback: interfejs użytkownika Menedżera NuGet dla awarii rozwiązań po wybraniu opcji wszystkie projekty — [#4191](https://github.com/NuGet/Home/issues/4191)

- nuget.exe msbuildpath kończy się niepowodzeniem, gdy występuje końcowy ukośnik — [#4180](https://github.com/NuGet/Home/issues/4180)

- vsfeedback: Przywracanie NuGet daje kilka ostrzeżeń odwołania projektu dla projektu LinqToTwitter — [#4156](https://github.com/NuGet/Home/issues/4156)

- Pakiet od `.csproj` nie zawiera atrybutu minClientVersion — [#4135](https://github.com/NuGet/Home/issues/4135)

- NuGet.Build.Tasks.Pack.dll wysłane opóźnienie z podpisem program VS2017 (d15rel 26014,00) — [#4122](https://github.com/NuGet/Home/issues/4122)

- VSFeedback: Przywracanie nie powiodło się dla projektu VS 2015 wygenerowanego z CMake 3.7.1- [#4114](https://github.com/NuGet/Home/issues/4114)

- VSFeedback: Błędy przywracania mogą zasłaniać bardziej kompletne komunikaty o błędach, które kompilacja może dać [#4113](https://github.com/NuGet/Home/issues/4113)

- [VSFeedback] Wystąpił błąd podczas przywracania pakietów NuGet dla projektu witryny sieci Web: wartość nie może być równa null. - [#4092](https://github.com/NuGet/Home/issues/4092)

- Migracja zgłasza "wyjątek odwołania do obiektu" w NuGet. PackageManagement. VisualStudio. SolutionRestoreWorker- [#4067](https://github.com/NuGet/Home/issues/4067)

- dotnet
  - Pakiet dotnetcore Pack powinien mieć pakiet narzędzi z wersjami, dla których został skompilowany pakiet — [#4063](https://github.com/NuGet/Home/issues/4063)

- Nowe przywracanie w tle powoduje zapis milisekund na pasku stanu, gdy trwa sekund, aby przywrócić [#4036](https://github.com/NuGet/Home/issues/4036)

- Literówka w przypadku niepowodzenia rozpoznania wszystkich odwołań do projektu — [#4018](https://github.com/NuGet/Home/issues/4018)

- Włącz przepływy pracy PCM w scenariuszach odwołań do pakietów — [#4016](https://github.com/NuGet/Home/issues/4016)

- Nie można znaleźć zainstalowanych pakietów w interfejsie użytkownika Menedżera pakietów — [#4015](https://github.com/NuGet/Home/issues/4015)

- dotnet
  - Pakiet dotnetcore kończy się niepowodzeniem, gdy PackagePath jest pusty- [#3993](https://github.com/NuGet/Home/issues/3993)

- Zadanie przywracania kończy się niepowodzeniem w scenariuszu obejmującym wiele użytkowników — [#3897](https://github.com/NuGet/Home/issues/3897)

- Nie można zmienić typu zawartości podczas pakowania przy użyciu zadania pakietu NuGet — [#3895](https://github.com/NuGet/Home/issues/3895)

- Domyślna kopia ContentFiles jest niepoprawna dla programu MsBuild/t: Pack- [#3894](https://github.com/NuGet/Home/issues/3894)

- Pakiet instalacyjny programu instalacyjnego podwójnego rejestrowania komunikat przywracania pakietów — [#3785](https://github.com/NuGet/Home/issues/3785)

- Usuń Guardrails — przywracanie sekcji "środowiska uruchomieniowe" powinno być stosowane tylko do bieżącego projektu — [#3768](https://github.com/NuGet/Home/issues/3768)

- Pakiet Task umieszcza pliki zawartości w "Content/" i "contentFiles/"- [#3718](https://github.com/NuGet/Home/issues/3718)

- dotnet
  - dotnetcore Pack3 wykonuje dodatkowe dzielenie tagów — [#3701](https://github.com/NuGet/Home/issues/3701)

- dotnet
  - Pakiet dotnetcore: projekty pakowania z odwołaniami do pakietu są wynikiem ostrzeżenia o zduplikowanym imporcie — [#3665](https://github.com/NuGet/Home/issues/3665)

- Przywracanie dzienników w programie VS nie jest zawsze wyświetlane- [#3633](https://github.com/NuGet/Home/issues/3633)

- tekst pomocy dla ustawień regionalnych NuGet nadal omawiany w pamięci podręcznej pakietów — [#3592](https://github.com/NuGet/Home/issues/3592)

- Restore3 Couples składnika packagereferences z TargetFrameworks. - [#3504](https://github.com/NuGet/Home/issues/3504)

- Pakiet NuGet wybiera nieoczekiwaną wersję programu MSBuild w programie VS "15" (wersja zapoznawcza 4). wiersz polecenia — [#3408](https://github.com/NuGet/Home/issues/3408)

- Zapisuj pliki docelowe/elementy props w przypadku niepowodzenia przywracania — [#3399](https://github.com/NuGet/Home/issues/3399)

- Pakiet NuGet podczas przywracania nie uwzględnia tych samych podkładek zgodności jak MSBuild w przypadku uruchamiania w wierszu polecenia programu VS 15 — [#3387](https://github.com/NuGet/Home/issues/3387)

- Ponowne włączanie PackFromProjectWithDevelopmentDependencySet dla VS15- [#3272](https://github.com/NuGet/Home/issues/3272)

- Mieszanie problemów z pakietem NuGet — [#4043](https://github.com/NuGet/Home/issues/4043)

- Integruj 4.0.0.2067 w interfejsie wiersza polecenia i repozytoria zestawu SDK, aby dostarczyć z użyciem RC2- [#4029](https://github.com/NuGet/Home/issues/4029)

- VS zawiesza się podczas tworzenia nowej aplikacji z konsolą podstawową, zamykaj rozwiązanie, otwieraj rozwiązanie i zamykaj rozwiązanie — [#4008](https://github.com/NuGet/Home/issues/4008)

- Wysunięcie otwierające projekt względem d15prerel. 25916.01- [#3982](https://github.com/NuGet/Home/issues/3982)

- Naprawianie dokumentu/pomocy dotyczącej ustawień regionalnych dotnet/nuget.exe — [#3919](https://github.com/NuGet/Home/issues/3919)

- Sprawdź PackTask pod kątem problemów z końcowym lub wiodącym odstępem — [#3906](https://github.com/NuGet/Home/issues/3906)

- dotnet
  - Pakiet dotnetcore Pack jest pakowany z opakowania nie bin- [#3880](https://github.com/NuGet/Home/issues/3880)

- dotnet
  - Pakiet dotnetcore zawsze wygląda na ustawienie wersji elementu ProjectReference na 1.0.0- [#3874](https://github.com/NuGet/Home/issues/3874)

- dotnet
  - Pakiet dotnetcore kończy się niepowodzeniem z odwołaniami projektu i <TargetFramework>  -  [#3865](https://github.com/NuGet/Home/issues/3865)

- LockRecursionException w ProjectSystemCache. TryGetProjectNameByShortName- [#3861](https://github.com/NuGet/Home/issues/3861)

- Przytnij odstępy od właściwości programu MSBuild — [#3819](https://github.com/NuGet/Home/issues/3819)

- Konsoliduj dwa zdarzenia projektu zgłoszone podczas ładowania projektu — [#3759](https://github.com/NuGet/Home/issues/3759)

- Biblioteki P2P w `project.assets.json` pliku mają niepoprawną wersję [#3748](https://github.com/NuGet/Home/issues/3748)

- Przywracanie awarii z powodu braku odpowiedzi i niedostępnego pakietu — [#3672](https://github.com/NuGet/Home/issues/3672)

- nuget.exe może zawiesić się dużą ilość danych wyjściowych błędu MSBuild — [#3572](https://github.com/NuGet/Home/issues/3572)

- Przywracanie po kompilacji dla programu Blend kończy się niepowodzeniem po raz pierwszy [#2121](https://github.com/NuGet/Home/issues/2121) .

### <a name="dcrs"></a>DCR

- Migrowanie VSIX z wersji 2 VSIX do V3 VSIX- [#4196](https://github.com/NuGet/Home/issues/4196)

- Pakiet NuGet powinien mieć mechanizm pobierania ścieżki do pliku blokady w programie MSBuild — [#3351](https://github.com/NuGet/Home/issues/3351)

- Dodaj zasoby kompilacji do TFM kontroli zgodności i plików zasobów — [#3296](https://github.com/NuGet/Home/issues/3296)

- Zdefiniuj nowy ProjectCapability "Pack" w celu włączenia funkcji związanych z pakietem — [#4146](https://github.com/NuGet/Home/issues/4146)

- Uruchom pakiet jako element docelowy po kompilacji dla właściwości "GeneratePackageOnBuild" programu MSBuild — [#4145](https://github.com/NuGet/Home/issues/4145)

- Użyj właściwości NuGet RestoreProjectStyle, aby utworzyć określony projekt NuGet — [#4134](https://github.com/NuGet/Home/issues/4134)

- Dostosuj przywracanie dla przechodnich odwołań do projektu- [#4076](https://github.com/NuGet/Home/issues/4076)

- Dodaj właściwości NuGet w pliku docelowym dla projektów innych niż platformy UWP — [#4030](https://github.com/NuGet/Home/issues/4030)

- Obsługa TargetPlatformVersion platformy UWP — [#3923](https://github.com/NuGet/Home/issues/3923)

- Przekaż metadane odwołania projektu do systemu projektu NuGet — [#3922](https://github.com/NuGet/Home/issues/3922)

- Dodaj interfejs użytkownika dla trybu pakowania — [#3921](https://github.com/NuGet/Home/issues/3921)

- Starsze `.csproj` potrzeby NugetTargetMoniker i RuntimeIdentifiers są ustawiane w elemencie proj/targets- [#3854](https://github.com/NuGet/Home/issues/3854)

- Pakiet instalacyjny może się pokrywać z funkcją automatycznej przywracania [#3836](https://github.com/NuGet/Home/issues/3836)

- QueryStatus menu kontekstowego nie nastąpi, gdy pakietu VSPackage nie jest załadowany- [#3835](https://github.com/NuGet/Home/issues/3835)

- Przywracanie rozwiązań i przywracanie kompilacji nadal wyświetla okna dialogowe — [#3789](https://github.com/NuGet/Home/issues/3789)

- Izolowanie wersji VSSDK w programie NuGet. klienci — kompilacja rozwiązań — [#3890](https://github.com/NuGet/Home/issues/3890)

## <a name="links-to-github-issues-fixed-in-rtm"></a>Linki do problemów z usługą GitHub rozwiązane w wersji RTM
[Lista problemów 1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[Lista problemów 2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[Lista problemów 3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[Lista problemów 4](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[Lista problemów 5](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
