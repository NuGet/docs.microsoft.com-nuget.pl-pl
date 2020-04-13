---
title: Informacje o wersji nuGet 4.0 RC
description: Informacje o wersji dla NuGet 4.0 RTM, w tym znane problemy, poprawki błędów, dodane funkcje i dcrs.
author: anangaur
ms.author: anangaur
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: c27d0aa2e5c9af9cb15d2f487b93e93aca666214
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496607"
---
# <a name="nuget-40-rtm-release-notes"></a>Informacje o wydaniu programu NuGet 4.0 RTM

[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest wyposażony w NuGet 4.0, który dodaje obsługę .NET Core, ma kilka poprawek jakości i zwiększa wydajność. Ta wersja zawiera również kilka ulepszeń, takich jak obsługa PackageReference, Polecenia NuGet jako obiekty docelowe MSBuild, przywraca pakiet w tle i inne.

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

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Nie można wyświetlać, dodawać ani aktualizować dotNetCLITools przy użyciu Menedżera pakietów Nuget

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

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a>Naprawiono problemy w ramach czasowych NuGet 4.0 RTM

[NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md) - Wyświetla listę wszystkich problemów rozwiązanych dla NuGet 4.0 RC

### <a name="features"></a>Funkcje

- Lokalizuj ciągi w pliku NuGet.Core.sln — [#2041](https://github.com/NuGet/Home/issues/2041)

- Nuget wymusza ładowanie projektów aplikacji internetowych w trybie LSL - [#4258](https://github.com/NuGet/Home/issues/4258)

- Obsługa funkcji AutoReferenced PackageReference w celu zablokowania zmian wersji w interfejsie użytkownika dla pakietów "zainstalowany sdk" — [#4044](https://github.com/NuGet/Home/issues/4044)

- Poprawnie komunikować PackageSpec.Version dla wszystkich zależności projektu (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)

- obsługa usuwania odwołań `.csproj` z wierszy poleceń - [#4101](https://github.com/NuGet/Home/issues/4101)

- Obsługa przywracania dla projektów PackageReference (normalny i xplat) i lekkie obciążenie rozwiązania - [#4003](https://github.com/NuGet/Home/issues/4003)

- obsługa dodawania odwołań do `.csproj` wierszy poleceń — [#3751](https://github.com/NuGet/Home/issues/3751)

- Obsługa przywracania NuGet dla `packages.config` `project.json`  - lekkiego ładowania rozwiązania dla lub [#3711](https://github.com/NuGet/Home/issues/3711)

- contentFiles wsparcie w pliku docelowym generowanym przez nuget - [#3683](https://github.com/NuGet/Home/issues/3683)

- Ustanawianie mono ci dla sprawdzania poprawności nuget.exe na komputerze Mac przy użyciu MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)

- Przenieś NuGet off z v2 NuGet.Core zależności - [#3645](https://github.com/NuGet/Home/issues/3645)

### <a name="bugs"></a>Usterki

- NuGet restore w programie Visual Studio nie respektuje właściwości PackageId projektów — [#4586](https://github.com/NuGet/Home/issues/4586)

- Błąd NuGet ProjectSystemCache podczas dodawania pakietu w pakiecie vsix - [#4545](https://github.com/NuGet/Home/issues/4545)

- Pack zgłasza wyjątek, jeśli IncludeSource jest używany w projekcie z wieloma TFM - [#4536](https://github.com/NuGet/Home/issues/4536)

- Vs 2017 RC3 zawiesza się przy użyciu aktualizacji z zarządzania pakietami w całej rozwiązania - [#4474](https://github.com/NuGet/Home/issues/4474)

- Nie można odinstalować nowo zainstalowanego pakietu - [#4435](https://github.com/NuGet/Home/issues/4435)

- Podczas migracji do PackageRef rozwiązania hybrydowe mają dziwne zachowanie przywracania — [#4433](https://github.com/NuGet/Home/issues/4433)

- Tworzenie wkrótce po uruchomieniu operacji NuGet (instalacja, aktualizacja, przywracanie), może spowodować VS hang - [#4420](https://github.com/NuGet/Home/issues/4420)

- Zawieszanie interfejsu użytkownika — zakleszczenie inicjowania nuget.solutionrestoremanager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)

- polecenie dodaj pakiet należy dodać wersję jako atrybut zamiast elementu - [#4325](https://github.com/NuGet/Home/issues/4325)

- dotnet
  - dotnetcore Restore foo.sln -- kończy się niepowodzeniem, gdy konfiguracje w SLN powodują duplikaty (ale diff config) projekty na wykresie przywracania - [#4316](https://github.com/NuGet/Home/issues/4316)

- Pakiety tylko do zawartości - [#3668](https://github.com/NuGet/Home/issues/3668)

- Domyślnie opcja wyboru formatu pakietu - [#4468](https://github.com/NuGet/Home/issues/4468)

- Perf: CreateUAP_CSharp_VS.01.1.Tworzenie projektu regressed Duration_TotalElapsedTime o 3.153.570 ms (149.1%). Wartość bazowa 26129,02 - [#4452](https://github.com/NuGet/Home/issues/4452)

- Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Rozwiązanie cofło Duration_TotalElapsedTime o 1,5 s. Wartość bazowa 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)

- Nominacja nie powiedzie się w wielu projektach TFM - [#4419](https://github.com/NuGet/Home/issues/4419)

- Perf: WebForms_DDRIT.1200.Close Rozwiązanie cofło VM_ImagesInMemory_Total_devenv o 3.000 Count (0.5%). Wartość bazowa 26123,04 - [#4408](https://github.com/NuGet/Home/issues/4408)

- vsfeedback - Ostrzeżenia o pakowaniu podczas kierowania netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)

- PathTooLongException podczas próby dodania pakietu NuGet do pustej aplikacji sieci web ASP.NET Core — [#4391](https://github.com/NuGet/Home/issues/4391)

- Pakiet działa zbyt często - dotnet
  - pakiet dotnetcore kończy się niepowodzeniem z istnieje cykliczna zależność na wykresie zależności docelowej obejmującej docelowy "Pack" — [#4381](https://github.com/NuGet/Home/issues/4381)

- Pakiet działa zbyt często — generowanie pakietu NuGet nie zawiera wszystkich konfiguracji — [#4380](https://github.com/NuGet/Home/issues/4380)

- NullReferenceException dodawanie nuget z packageref w projekcie C++ - [#4378](https://github.com/NuGet/Home/issues/4378)

- Dostępność : Narrator nie opowiada pola wyboru, aby wybrać projekty, aby zainstalować pakiet do - [#4366](https://github.com/NuGet/Home/issues/4366)

- NuGet VS17 sporadycznie nie łączy się z kanałami informacyjnymi VSO/VSTS — błąd 365798 — [#4365](https://github.com/NuGet/Home/issues/4365)

- contentFiles uzyskać dane wyjściowe do niewłaściwej lokalizacji, jeśli PackagePath określa ścieżkę jako "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)

- Pack target dołącza packageversion właściwości z VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)

- Określanie ścieżki pakietu nie działa z pakietem dotnet - [#4321](https://github.com/NuGet/Home/issues/4321)

- NuGet wyprowadza kilka ostrzeżeń o zduplikowanych importach podczas przywracania — [#4304](https://github.com/NuGet/Home/issues/4304)

- Wybierz okno dialogowe "NuGet Package Manager Format" wygląda źle pod ciemnym motywem - [#4300](https://github.com/NuGet/Home/issues/4300)

- Awaria vs na przywracanie kompilacji - [#4298](https://github.com/NuGet/Home/issues/4298)

- Zakleszczenia programu Visual Studio, jeśli dodasz TFM w targetframeworks, zapisz, a następnie skompilować. 10% czasu - [#4295](https://github.com/NuGet/Home/issues/4295)

- nuget pack nie wyprowadza komunikatu o sukcesie podczas pomyślnego pakowania projektu - [#4294](https://github.com/NuGet/Home/issues/4294)

- PackTask nie powiedzie się z powodu nieuleczeniu systemu.IO.Compression 4.1 - [#4290](https://github.com/NuGet/Home/issues/4290)

- Pack działa zbyt często — PackTask często kończy się niepowodzeniem z konfliktem dostępu do plików - [#4289](https://github.com/NuGet/Home/issues/4289)

- NuGet otwiera okno wyjściowe podczas przywracania tła - [#4274](https://github.com/NuGet/Home/issues/4274)

- Wyeliminuj ServiceProvider jako niebezpieczny wzorzec kodowania (który może powodować zawiesza się) - [#4268](https://github.com/NuGet/Home/issues/4268)

- Perf/UIHang - Poprawa odczytów DownloadTimeoutStream - [#4266](https://github.com/NuGet/Home/issues/4266)

- Zakleszczenia programu Visual Studio, jeśli spróbujesz zamknąć projekt przed zakończeniem przywracania NuGet - [#4257](https://github.com/NuGet/Home/issues/4257)

- Problemy z PackTask `.nuspec`  - i pakowania [#4250](https://github.com/NuGet/Home/issues/4250)

- [vsfeedback] Nie można rozwiązać pakietów nuget w nowym projekcie (musi ponownie uruchomić visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)

- [vsfeedback] Rozwijana "Wersja", która pokazuje dostępne wersje pakietów, stara się pozostać w synchronizacji z wybranym pakietem nuGet... - [#4198](https://github.com/NuGet/Home/issues/4198)

- Nuget.Client powinien używać CPS JoinableTaskFactory podczas interakcji z CPS, aby zapobiec zakleszczenia - [#4185](https://github.com/NuGet/Home/issues/4185)

- NuGet 3.5.0 nie `.targets` rozpakowywanie z opakowania - [#4171](https://github.com/NuGet/Home/issues/4171)

- dotnet
  - dotnetcore pack nie obsługuje `.csproj`  - tytułu w [#4150](https://github.com/NuGet/Home/issues/4150)

- Install-Package powoduje błąd w vs2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)

- Aktualizowanie pakietu dla projektu .net core wydaje się nie działać, ponieważ interfejs użytkownika nie pobiera aktualizacji CPS z nominuj. - [#4035](https://github.com/NuGet/Home/issues/4035)

- Poprawa ostrzeżenia o nierozwiązanym odwołaniu - [#3955](https://github.com/NuGet/Home/issues/3955)

- dotnet
  - dotnetcore pack - ProjectReference traci informacje o wersji - [#3953](https://github.com/NuGet/Home/issues/3953)

- Tworzenie aplikacji platformy uniwersalnej systemu ZWP tworzenie projektu & odbudowy całkowitych regresji czasu, które upłynął - [#3873](https://github.com/NuGet/Home/issues/3873)

- Komunikat pomyślnego przywracania jest wyświetlany nawet po błędzie podczas przywracania. - [#3799](https://github.com/NuGet/Home/issues/3799)

- ponownie opublikować Nuget.CommandLine 3.4.4 do Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)

- Podczas migracji projekty zmieniają `project.json` `.csproj` się z --- przywracania --- nie powiedzie się — [#4297](https://github.com/NuGet/Home/issues/4297)

- Przywracanie w przypadku niepowodzenia nowo utworzonego projektu testu xunit — [#4296](https://github.com/NuGet/Home/issues/4296)

- Podstawowe projekty mogą zawieszać się, blokować interfejs użytkownika na otwartym - [#4269](https://github.com/NuGet/Home/issues/4269)

- naprawić plik docelowy dla zadań kompilacji - [#4267](https://github.com/NuGet/Home/issues/4267)

- Lista błędów zawiera błąd po rozwiązaniu kompilacji, które zwalnia projekt, do którego istnieje odwołanie - [#4208](https://github.com/NuGet/Home/issues/4208)

- MSB4057: Docelowy "_GenerateRestoreGraphProjectEntry" nie istnieje w projekcie. - [#4194](https://github.com/NuGet/Home/issues/4194)

- vsfeedback: nuget manager ui dla rozwiązania ulega awarii po wybraniu wszystkich projektów - [#4191](https://github.com/NuGet/Home/issues/4191)

- nuget.exe msbuildpath nie powiedzie się, gdy istnieje cięcie końcowe - [#4180](https://github.com/NuGet/Home/issues/4180)

- vsfeedback: Przywracanie NuGet daje kilka ostrzeżeń odwołania do projektu LinqToTwitter — [#4156](https://github.com/NuGet/Home/issues/4156)

- Pakiet `.csproj` z nie zawiera atrybutu minClientVersion - [#4135](https://github.com/NuGet/Home/issues/4135)

- NuGet.Build.Tasks.Pack.dll wysłane opóźnienie podpisane w programie VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)

- VSFeedback: Przywracanie kończy się niepowodzeniem dla projektu VS 2015 wygenerowanego za pomocą CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)

- VSFeedback: Przywracanie błędów może przesłaniać bardziej kompletne komunikaty o błędach, które kompilacji może dać - [#4113](https://github.com/NuGet/Home/issues/4113)

- [VSFeedback] Wystąpił błąd podczas przywracania pakietów NuGet dla projektu witryny: Wartość nie może być null. - [#4092](https://github.com/NuGet/Home/issues/4092)

- Migracja zgłasza "Wyjątek odwołania do obiektu" w NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)

- dotnet
  - dotnetcore pack powinien pakować narzędzia z wersjami, przeciwko których pakiet został zbudowany - [#4063](https://github.com/NuGet/Home/issues/4063)

- Nowe przywracanie tła zapisuje milisekundy na pasku stanu, gdy trwa kilka sekund, aby przywrócić - [#4036](https://github.com/NuGet/Home/issues/4036)

- Literówka na nie może rozwiązać wszystkich odwołań do projektu - [#4018](https://github.com/NuGet/Home/issues/4018)

- Włączanie przepływów pracy PCM w scenariuszach referencyjnych pakietów — [#4016](https://github.com/NuGet/Home/issues/4016)

- Nie można znaleźć zainstalowanych pakietów w interfejsie menedżera pakietów - [#4015](https://github.com/NuGet/Home/issues/4015)

- dotnet
  - pakiet dotnetcore kończy się niepowodzeniem, gdy PackagePath jest pusty - [#3993](https://github.com/NuGet/Home/issues/3993)

- Przywracanie zadania kończy się niepowodzeniem w scenariuszu dla wielu użytkowników — [#3897](https://github.com/NuGet/Home/issues/3897)

- Nie można zmienić typu zawartości podczas pakowania przy użyciu zadania Pakietu NuGet Pack — [#3895](https://github.com/NuGet/Home/issues/3895)

- Domyślna kopia contentfiles są niepoprawne dla MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)

- Zainstaluj pakiet przywracanie dwukrotnie rejestruje komunikat przywracania pakietów - [#3785](https://github.com/NuGet/Home/issues/3785)

- Usuń barierki — przywracanie sekcji "środowiska wykonawcze" powinno dotyczyć tylko bieżącego projektu — [#3768](https://github.com/NuGet/Home/issues/3768)

- Zadanie pack umieszcza pliki zawartości zarówno w "zawartość / " i "contentFiles/" - [#3718](https://github.com/NuGet/Home/issues/3718)

- dotnet
  - dotnetcore pack3 robi dodatkowe dzielenie tagów - [#3701](https://github.com/NuGet/Home/issues/3701)

- dotnet
  - dotnetcore pack: projekty pakowania z odniesieniami do pakietów skutkują zduplikowanym ostrzeżeniem importu - [#3665](https://github.com/NuGet/Home/issues/3665)

- Przywróć rejestrowanie w vs nie zawsze pokazuje - [#3633](https://github.com/NuGet/Home/issues/3633)

- nuget mieszkańcy pomagają tekst nadal wymienione pakiety cache - [#3592](https://github.com/NuGet/Home/issues/3592)

- Restore3 pary PackageReferences z TargetFrameworks. - [#3504](https://github.com/NuGet/Home/issues/3504)

- Nuget wybiera nieoczekiwaną wersję MSBuild w vs "15" Preview 4 dev. wiersz polecenia - [#3408](https://github.com/NuGet/Home/issues/3408)

- Zapisz pliki obiektów docelowych/rekwizytów podczas nie powiodło się przywracanie - [#3399](https://github.com/NuGet/Home/issues/3399)

- NuGet podczas przywracania nie respektuje tych samych podkładek compat co MSBuild podczas uruchamiania w wierszu polecenia programu VS 15 — [#3387](https://github.com/NuGet/Home/issues/3387)

- Ponownie włącz PackFromProjectWithDevelopmentDependencySet for VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)

- Problemy z mieszaniem z NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)

- Integracja 4.0.0.2067 z repo CLI i SDK do wysyłki z RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)

- VS zawiesza się podczas tworzenia nowej aplikacji Core Console, zamknij rozwiązanie, otwarte rozwiązanie i zamknij rozwiązanie - [#4008](https://github.com/NuGet/Home/issues/4008)

- Uderzenie w projekt otwarcia zawieszenia przeciwko d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)

- Napraw komunikat dotnet/nuget.exe locals doc/help - [#3919](https://github.com/NuGet/Home/issues/3919)

- Sprawdź PackTask pod kątem problemów z spływu lub wiodących odstępów - [#3906](https://github.com/NuGet/Home/issues/3906)

- dotnet
  - dotnetcore pack jest pakowanie z obj nie bin - [#3880](https://github.com/NuGet/Home/issues/3880)

- dotnet
  - dotnetcore pack zawsze wydaje się ustawić wersję ProjectReference na 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)

- dotnet
  - pakiet dotnetcore kończy się <TargetFramework>  - niepowodzeniem z odwołaniami do projektu i [#3865](https://github.com/NuGet/Home/issues/3865)

- LockRecursionException w programie ProjectSystemCache.TryGetProjectNameByShortName — [#3861](https://github.com/NuGet/Home/issues/3861)

- Przycinanie odstępu z właściwości MSBuild - [#3819](https://github.com/NuGet/Home/issues/3819)

- Konsolidacja dwóch zdarzeń projektu podniesionych przy obciążeniu projektu - [#3759](https://github.com/NuGet/Home/issues/3759)

- Biblioteki P2P `project.assets.json` w pliku mają niepoprawną wersję - [#3748](https://github.com/NuGet/Home/issues/3748)

- Przywracanie awarii z powodu braku odpowiedzi i niedostępnego pakietu - [#3672](https://github.com/NuGet/Home/issues/3672)

- nuget.exe może zawiesić się na dużej ilości danych wyjściowych błędu MSBuild - [#3572](https://github.com/NuGet/Home/issues/3572)

- Przywracanie na kompilacji dla blendu kończy się niepowodzeniem po raz pierwszy, kończy się po raz drugi (poprawiony scenariusz VS) — [#2121](https://github.com/NuGet/Home/issues/2121)

### <a name="dcrs"></a>DDR

- migrować vsix z v2 vsix do v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)

- NuGet powinien mieć mechanizm uzyskiwania ścieżki do pliku blokady w MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)

- Dodawanie zasobów kompilacji do pliku sprawdzania zgodności tfm i zasobów — [#3296](https://github.com/NuGet/Home/issues/3296)

- Zdefiniuj nowy pakiet "Pack" w pakiecie docelowym umożliwiający włączenie możliwości związanych z pakietem — [#4146](https://github.com/NuGet/Home/issues/4146)

- Uruchom pakiet jako miejsce docelowe kompilacji postu uwarunkowane właściwością MSBuild "GeneratePackageOnBuild" — [#4145](https://github.com/NuGet/Home/issues/4145)

- Użyj Właściwości NuGet RestoreProjectStyle do utworzenia określonego projektu NuGet - [#4134](https://github.com/NuGet/Home/issues/4134)

- Adaptuj przywracanie dla przechodnich odwołań do projektu — [#4076](https://github.com/NuGet/Home/issues/4076)

- Dodaj właściwości NuGet w pliku docelowym dla projektów innych niż platformy uniwersalne — [#4030](https://github.com/NuGet/Home/issues/4030)

- Obsługa platformy docelowej platformy uniwersalnej platformy uniwersalnej — [#3923](https://github.com/NuGet/Home/issues/3923)

- Komunikuj metadane odwołania do projektu do systemu projektu NuGet — [#3922](https://github.com/NuGet/Home/issues/3922)

- Dodaj interfejs użytkownika dla trybu pakowania - [#3921](https://github.com/NuGet/Home/issues/3921)

- Starsze `.csproj` potrzeby NugetTargetMoniker i RuntimeIdentifiers określone w proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)

- Pakiet instalacyjny może pokrywać się z automatycznym przywracaniem - [#3836](https://github.com/NuGet/Home/issues/3836)

- Menu kontekstowe QueryStatus nie dzieje się, gdy VSPackage nie jest załadowany - [#3835](https://github.com/NuGet/Home/issues/3835)

- Przywracanie i przywracanie kompilacji rozwiązania nadal wyświetla okna dialogowe - [#3789](https://github.com/NuGet/Home/issues/3789)

- Izoluj wersję VSSDK w kompilacji rozwiązania NuGet.Clients - [#3890](https://github.com/NuGet/Home/issues/3890)

## <a name="links-to-github-issues-fixed-in-rtm"></a>Naprawiono łącza do githubu
[Lista problemów 1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[Lista problemów 2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[Lista problemów 3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[Lista problemów 4](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[Lista problemów 5](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
