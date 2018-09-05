---
title: Informacje o wersji programu NuGet 4.0 RC
description: Informacje o wersji NuGet 4.0 RTM, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: anangaur
ms.author: anangaur
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: c27d0aa2e5c9af9cb15d2f487b93e93aca666214
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547764"
---
# <a name="nuget-40-rtm-release-notes"></a>Informacje o wersji NuGet 4.0 RTM

[Program Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z NuGet 4.0, który dodaje obsługę platformy .NET Core i ma wiele poprawek jakości oraz zwiększa wydajność. Ta wersja oferuje również kilka udoskonaleń, takich jak obsługa PackageReference, polecenia NuGet MSBuild elementów docelowych, Przywracanie pakietu tło i inne.

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

Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania. Alternatywnie, spróbuj usunąć `project.lock.json` i przywrócić go ponownie.

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a>W projektach .NET Core użytkownik może pozostać w pętli nieskończonej przywracania w przypadku użycia pakietu zawierającego zestaw z nieprawidłowym podpisem

#### <a name="issue"></a>Problem

Czasami, w przypadku użycia pakietu zawierającego zestaw z nieprawidłowym podpisem lub gdy wersja pakietu została ustawiona za pomocą znacznika „DateTime”, automatyczne przywracanie pakietu będzie uruchamiane w pętli nieskończonej. [NuGet#4542](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a>Obejście

Obecnie nie istnieje obejście tego problemu.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Nie można wyświetlić, dodać ani zaktualizować składnika DotNetCLITools przy użyciu Menedżera pakietów Nuget

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

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a>Problemy rozwiązane w wersji RTM 4.0 NuGet przedziale czasu

[Informacje o wersji NuGet 4.0 RC](../release-notes/nuget-4.0-RC.md) — Wyświetla listę wszystkich problemów naprawione w wersji NuGet 4.0 RC

### <a name="features"></a>Funkcje

- Localize — ciągi w NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)

- Nuget wymusza załadować projektów aplikacji sieci web w trybie LSL - [#4258](https://github.com/NuGet/Home/issues/4258)

- Obsługę AutoReferenced PackageReference wersja bloku zmiany w interfejsie użytkownika dla pakietów "zainstalowany zestaw sdk" - [#4044](https://github.com/NuGet/Home/issues/4044)

- Skomunikował się PackageSpec.Version dla wszelkich zależności projektu (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)

- Obsługa Usuwanie odwołań do `.csproj` z commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)

- Obsługa przywracania projektów PackageReference (normalne i interfejs xplat) i uproszczonego ładowania rozwiązań — [#4003](https://github.com/NuGet/Home/issues/4003)

- Obsługa dodawania odwołań do `.csproj` z commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)

- Obsługa przywracania NuGet dla uproszczonego ładowania rozwiązań dla `packages.config` lub `project.json`  -  [#3711](https://github.com/NuGet/Home/issues/3711)

- Pliki obsługi w pliku cele nuget generowane — [#3683](https://github.com/NuGet/Home/issues/3683)

- Ustanowić ciągła Integracja platformy Mono Walidacja nuget.exe na komputerze Mac przy użyciu platformy MSBuild — [#3646](https://github.com/NuGet/Home/issues/3646)

- Przenieś NuGet poza zależności NuGet.Core v2 - [#3645](https://github.com/NuGet/Home/issues/3645)

### <a name="bugs"></a>Usterki

- Przywracanie pakietów NuGet w programie Visual Studio nie przestrzega właściwości PackageId projektów — [#4586](https://github.com/NuGet/Home/issues/4586)

- Błąd NuGet ProjectSystemCache podczas dodawania pakietu w pakiecie vsix — [#4545](https://github.com/NuGet/Home/issues/4545)

- Pakiet zgłasza wyjątek, jeśli IncludeSource jest używany w projekcie z wielu krótkich nazw platform — [#4536](https://github.com/NuGet/Home/issues/4536)

- Program VS 2017 RC3 awarie na temat korzystania z aktualizacji z całego rozwiązania pakietów zarządzania — [#4474](https://github.com/NuGet/Home/issues/4474)

- Nie można odinstalować nowo zainstalowany pakiet — [#4435](https://github.com/NuGet/Home/issues/4435)

- Podczas migracji do PackageRef, rozwiązania hybrydowego mają przywracania dziwne zachowania - [#4433](https://github.com/NuGet/Home/issues/4433)

- Tworzenie wkrótce po uruchamianie NuGet działanie (instalacja, aktualizacja, przywracanie), może spowodować VS do zawieszenia - [#4420](https://github.com/NuGet/Home/issues/4420)

- Zawieszanie interfejsu użytkownika — inicjowanie NuGet.SolutionRestoreManager.RestoreManagerPackage zakleszczenia [#4371](https://github.com/NuGet/Home/issues/4371)

- Dodaj polecenie pakietu należy dodać wersję jako atrybut zamiast elementu - [#4325](https://github.com/NuGet/Home/issues/4325)

- polecenia DotNet
  - foo.sln przywracania dotnetcore — kończy się niepowodzeniem, podczas konfiguracji w SLN spowodować przywracania graph — projekty zduplikowane (ale config różnic) [#4316](https://github.com/NuGet/Home/issues/4316)

- Zawartość tylko pakiety - [#3668](https://github.com/NuGet/Home/issues/3668)

- Domyślnie zrezygnować z pakietu format selektor, opcja - [#4468](https://github.com/NuGet/Home/issues/4468)

- Danych o wydajności: Projekt CreateUAP_CSharp_VS.01.1.Create uwzględniona Duration_TotalElapsedTime przez 3,153.570 ms (149.1%). Plan bazowy 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)

- Danych o wydajności: Rozwiązanie ManagedLangs_CS_DDRIT.0300.Rebuild uwzględniona Duration_TotalElapsedTime przez 1,5 s. Plan bazowy 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)

- Nominacji zakończy się niepowodzeniem w projektach multi TFM - [#4419](https://github.com/NuGet/Home/issues/4419)

- Danych o wydajności: Rozwiązanie WebForms_DDRIT.1200.Close uwzględniona VM_ImagesInMemory_Total_devenv według liczby 3.000 (0,5%). Plan bazowy 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)

- vsfeedback - pakietu ostrzeżenia podczas określania wartości netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)

- Pathtoolongexception — podczas próby dodania pakiet NuGet do aplikacji sieci web platformy ASP.NET Core puste - [#4391](https://github.com/NuGet/Home/issues/4391)

- Pakiet jest uruchamiany zbyt często — dotnet
  - dotnetcore pakietu zakończy się niepowodzeniem z miejsca to zależność cykliczną w zależności programu graph obejmujące docelowe "Pakiet" - [#4381](https://github.com/NuGet/Home/issues/4381)

- Pakiet jest uruchamiany zbyt często — pakiet NuGet Generowanie nie obejmuje wszystkie konfiguracje — [#4380](https://github.com/NuGet/Home/issues/4380)

- Nuget Dodawanie obiektu NullReferenceException z packageref w projekcie C++ - [#4378](https://github.com/NuGet/Home/issues/4378)

- Ułatwienia dostępu: Narrator nie narracji pole wyboru, aby wybrać projekty, aby zainstalować pakiet: [#4366](https://github.com/NuGet/Home/issues/4366)

- NuGet VS17 sporadycznie nie powiedzie się nawiązywania połączenia z kanałów informacyjnych VSO/VSTS - 365798 usterki programu VS - [#4365](https://github.com/NuGet/Home/issues/4365)

- Pliki pobierać dane wyjściowe do niewłaściwej lokalizacji, jeśli PackagePath Określa ścieżkę jako "pliki" - [#4348](https://github.com/NuGet/Home/issues/4348)

- Pakiet docelowy dołącza właściwość VersionSuffix - PackageVersion [#4324](https://github.com/NuGet/Home/issues/4324)

- Określanie ścieżki pakietu nie działa w przypadku pakietu dotnet - [#4321](https://github.com/NuGet/Home/issues/4321)

- NuGet generuje wiele ostrzeżeń o zduplikowane Importy, podczas przywracania - [#4304](https://github.com/NuGet/Home/issues/4304)

- Wybierz okno dialogowe "Menedżer pakietów NuGet Format" wygląda niewłaściwie w obszarze motyw ciemny - [#4300](https://github.com/NuGet/Home/issues/4300)

- VS awarii po Przywracanie kompilacji — [#4298](https://github.com/NuGet/Home/issues/4298)

- Visual Studio zakleszczenie w przypadku dodania elementu TFM w targetframeworks, Zapisz, a następnie kompilacji. 10% czasu - [#4295](https://github.com/NuGet/Home/issues/4295)

- Pakiet nuget nie wyświetla komunikat informujący o pomyślnym - pakowania projektu [#4294](https://github.com/NuGet/Home/issues/4294)

- PackTask zakończy się niepowodzeniem z powodu 4.1 System.IO.Compression nie można odnaleźć - [#4290](https://github.com/NuGet/Home/issues/4290)

- Pakiet jest uruchamiany zbyt często — PackTask często zakończy się niepowodzeniem z konfliktem dostępu do pliku - [#4289](https://github.com/NuGet/Home/issues/4289)

- NuGet spowoduje otwarcie okna dane wyjściowe podczas przywracania tła - [#4274](https://github.com/NuGet/Home/issues/4274)

- Wyeliminuj element ServiceProvider jako niebezpieczne wzorzec pisania kodu, (które mogą powodować zawiesza się) — [#4268](https://github.com/NuGet/Home/issues/4268)

- Perf/UIHang - poprawić odczyty DownloadTimeoutStream - [#4266](https://github.com/NuGet/Home/issues/4266)

- Zakleszczenia programu Visual Studio, jeśli użytkownik podejmie próbę zamykanie projektu, zanim zakończy przywracanie pakietów NuGet — [#4257](https://github.com/NuGet/Home/issues/4257)

- Problemy związane z PackTask i pakowanie `.nuspec`  -  [#4250](https://github.com/NuGet/Home/issues/4250)

- [vsfeedback] Nie można rozpoznać pakietów nuget dla nowego projektu (wymaga ponownego uruchomienia programu visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)

- [vsfeedback] "Wersja" Lista rozwijana, które pokazuje wersje pakiet niezbyt dobrze radzi sobie, aby pozostać w synchronizacji z pakietu nuGet wybrane... — [#4198](https://github.com/NuGet/Home/issues/4198)

- Nuget.Client skorzystaj z CPS JoinableTaskFactory podczas interakcji z CPS zapobiegające zakleszczenia - [#4185](https://github.com/NuGet/Home/issues/4185)

- NuGet 3.5.0 nie rozpakowywania `.targets` z pakietu - [#4171](https://github.com/NuGet/Home/issues/4171)

- polecenia DotNet
  - dotnetcore nie obsługuje tytuł w `.csproj`  -  [#4150](https://github.com/NuGet/Home/issues/4150)

- Install-Package skutkuje okna dialogowego błędu w programie VS2017 RC — [#4127](https://github.com/NuGet/Home/issues/4127)

- Aktualizowanie pakietu dla projektu programu .net core nie działa prawidłowo, zgodnie z interfejsu użytkownika nie pobranie aktualizacji CPS z nominate. - [#4035](https://github.com/NuGet/Home/issues/4035)

- Poprawa ostrzeżenie nierozpoznane odwołanie - [#3955](https://github.com/NuGet/Home/issues/3955)

- polecenia DotNet
  - Pakiet dotnetcore — elementu ProjectReference utraci informacje o wersji — [#3953](https://github.com/NuGet/Home/issues/3953)

- Tworzenie aplikacji platformy uniwersalnej systemu Windows tworzenie projektu i Odbuduj regresji całkowity upływ czasu — [#3873](https://github.com/NuGet/Home/issues/3873)

- Nawet po błędzie jest wyświetlany komunikat pomyślnie przeprowadzić przywrócenie podczas przywracania. - [#3799](https://github.com/NuGet/Home/issues/3799)

- Ponowne publikowanie Nuget.CommandLine 3.4.4 na stronie Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)

- Na migracji, projekty zmienić z `project.json` do `.csproj` ---Przywracanie nie powiodło się — [#4297](https://github.com/NuGet/Home/issues/4297)

- Niepowodzenie przywracania na projekt testu xunit nowo utworzony - [#4296](https://github.com/NuGet/Home/issues/4296)

- Projekty Core zawieszanie znajduje się w zablokowanie interfejsu użytkownika podczas otwierania - [#4269](https://github.com/NuGet/Home/issues/4269)

- Napraw plik elementów docelowych dla zadania kompilacji - [#4267](https://github.com/NuGet/Home/issues/4267)

- Lista błędów zawiera błąd, po rozwiązania kompilacji, które zwolnić odwołania projekt - [#4208](https://github.com/NuGet/Home/issues/4208)

- MSB4057: Element docelowy "_GenerateRestoreGraphProjectEntry" nie istnieje w projekcie. - [#4194](https://github.com/NuGet/Home/issues/4194)

- vsfeedback: interfejsu użytkownika Menedżera nuget dla rozwiązania ulega awarii podczas wybierz wszystkie projekty - [#4191](https://github.com/NuGet/Home/issues/4191)

- nuget.exe msbuildpath nie powiedzie się po znaku ukośnika na końcu - [#4180](https://github.com/NuGet/Home/issues/4180)

- vsfeedback: Przywracanie pakietów NuGet zapewniają kilka ostrzeżeń odwołania projektu dla projektu LinqToTwitter - [#4156](https://github.com/NuGet/Home/issues/4156)

- Pakietu z `.csproj` nie zawiera atrybutu atrybutu minClientVersion - [#4135](https://github.com/NuGet/Home/issues/4135)

- NuGet.Build.Tasks.Pack.dll dostarczane podpisany w programie VS2017 z opóźnieniem (d15rel 26014.00)- [#4122](https://github.com/NuGet/Home/issues/4122)

- VSFeedback: Restore kończy się niepowodzeniem dla projektu programu VS 2015, wygenerowane za pomocą narzędzia CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)

- VSFeedback: Błędy odtwarzania może zasłaniać pełniejsze komunikaty o błędach kompilacji może przyznać - [#4113](https://github.com/NuGet/Home/issues/4113)

- [VSFeedback] Wystąpił błąd podczas przywracania pakietów NuGet dla projektu witryny sieci Web: wartość nie może mieć wartości null. - [#4092](https://github.com/NuGet/Home/issues/4092)

- Migracja zgłasza "Odwołanie do obiektu wyjątku" w NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)

- polecenia DotNet
  - Pakiet dotnetcore powinien pakietu narzędzi z wersjami, które pakietu została skompilowana - [#4063](https://github.com/NuGet/Home/issues/4063)

- Nowe tle przywracania zapisuje milisekund pasek po zajmuje sekund, aby przywrócić - stanu [#4036](https://github.com/NuGet/Home/issues/4036)

- Błąd pisowni w udało się rozpoznać wszystkie projektu odwołania — [#4018](https://github.com/NuGet/Home/issues/4018)

- Włącz PCM przepływy pracy, w scenariuszach odwołanie do pakietu - [#4016](https://github.com/NuGet/Home/issues/4016)

- Nie można odnaleźć zainstalowanych pakietów w pakiecie Menedżer interfejsu użytkownika — [#4015](https://github.com/NuGet/Home/issues/4015)

- polecenia DotNet
  - Pakiet dotnetcore zakończy się niepowodzeniem, gdy PackagePath jest pusta — [#3993](https://github.com/NuGet/Home/issues/3993)

- Przywracanie nie powiodło się zadań, w scenariuszu użytkownik multi - [#3897](https://github.com/NuGet/Home/issues/3897)

- Nie można zmienić typu zawartości, gdy pakowanie przy użyciu zadania pakietu NuGet — [#3895](https://github.com/NuGet/Home/issues/3895)

- Domyślna kopia pliki są nieprawidłowe dla MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)

- Przywracanie pakietu instalacji double rejestruje przywracania pakietów komunikat - [#3785](https://github.com/NuGet/Home/issues/3785)

- Usuń Guardrails - przywracania w sekcji "runtimes" stosuje się tylko do bieżącego projektu - [#3768](https://github.com/NuGet/Home/issues/3768)

- Zadanie pakietów umieszcza pliki zawartości w obu "zawartość /" i "pliki /"- [#3718](https://github.com/NuGet/Home/issues/3718)

- polecenia DotNet
  - dotnetcore dodatkiem Service Pack 3 dodatkowych tagu podziału - [#3701](https://github.com/NuGet/Home/issues/3701)

- polecenia DotNet
  - Pakiet dotnetcore: pakowanie projektów za pomocą pakietu odwołuje się do powoduje zduplikowanie ostrzeżenia dotyczącego importowania - [#3665](https://github.com/NuGet/Home/issues/3665)

- Przywróć rejestrowania w programie VS nie zawsze pokazuj - [#3633](https://github.com/NuGet/Home/issues/3633)

- tekst pomocy dla zmiennych lokalnych nuget nadal wymienionych pakietów pamięci podręcznej — [#3592](https://github.com/NuGet/Home/issues/3592)

- Pozamałżeńskie Restore3 PackageReferences z TargetFrameworks. - [#3504](https://github.com/NuGet/Home/issues/3504)

- Nuget wybiera nieoczekiwaną wersją programu MSBuild w programie VS "15" dev. 4 (wersja zapoznawcza) Wiersz polecenia — [#3408](https://github.com/NuGet/Home/issues/3408)

- Zapisać pliki celów/arkuszy właściwości na przywracanie nie powiodło się — [#3399](https://github.com/NuGet/Home/issues/3399)

- NuGet podczas przywracania nie jest zgodny ten sam podkładki compat jako MSBuild uruchamianego w wierszu polecenia programu VS 15 - [#3387](https://github.com/NuGet/Home/issues/3387)

- Ponownie włącz PackFromProjectWithDevelopmentDependencySet dla VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)

- Problemy z NuGet — Blend [#4043](https://github.com/NuGet/Home/issues/4043)

- Integrowanie 4.0.0.2067 repozytoriów interfejsu wiersza polecenia i zestawu SDK do wysłania z RC2 — [#4029](https://github.com/NuGet/Home/issues/4029)

- Zawiesza się programu VS, podczas tworzenia nowej aplikacji Konsolowej Core, Zamknij rozwiązanie, otwórz rozwiązanie i Zamknij rozwiązanie - [#4008](https://github.com/NuGet/Home/issues/4008)

- Osiągnięcia zawieszenie otwierania projektu przed d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)

- Usuń lokalne dotnet/nuget.exe komunikatu pomocy doc — [#3919](https://github.com/NuGet/Home/issues/3919)

- Sprawdzanie PackTask problemów za pomocą spacji końcowych lub początkowych — [#3906](https://github.com/NuGet/Home/issues/3906)

- polecenia DotNet
  - Pakiet dotnetcore jest pakowanie z obj nie bin - [#3880](https://github.com/NuGet/Home/issues/3880)

- polecenia DotNet
  - Pakiet dotnetcore zawsze wydaje się równa elementu ProjectReference w wersji 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)

- polecenia DotNet
  - Pakiet dotnetcore kończy się niepowodzeniem z odwołaniami do projektów i <TargetFramework>  -  [#3865](https://github.com/NuGet/Home/issues/3865)

- LockRecursionException w ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)

- Przycina odstępu z właściwości programu MSBuild - [#3819](https://github.com/NuGet/Home/issues/3819)

- Konsoliduj zdarzenia projektu dwóch wywoływane po załadowaniu projektu - [#3759](https://github.com/NuGet/Home/issues/3759)

- Biblioteki p2p w `project.assets.json` plik ma nieprawidłową wersję - [#3748](https://github.com/NuGet/Home/issues/3748)

- Przywróć awarii ze względu na źródło danych nie odpowiada i pakiet niedostępny — [#3672](https://github.com/NuGet/Home/issues/3672)

- nuget.exe mogą powodować zawieszanie na dużą ilość danych wyjściowych błąd MSBuild - [#3572](https://github.com/NuGet/Home/issues/3572)

- Przywracanie w kompilacji dla programu Blend nie powiedzie się po raz pierwszy, zakończy się pomyślnie po raz drugi (VS scenariusz rozwiązany) - [#2121](https://github.com/NuGet/Home/issues/2121)

### <a name="dcrs"></a>DCRs

- Przeprowadź migrację vsix z v2 vsix do v3 vsix — [#4196](https://github.com/NuGet/Home/issues/4196)

- NuGet powinny mieć mechanizm do pobierania ścieżki do pliku blokady w programie MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)

- Dodaj zasoby kompilacji do elementu TFM zgodności wyboru i zasoby pliku - [#3296](https://github.com/NuGet/Home/issues/3296)

- Definiowanie nowych ProjectCapability "Pakiet" w pakiecie cele dotyczące włączania pakietu powiązane możliwości — [#4146](https://github.com/NuGet/Home/issues/4146)

- Uruchom pakiet jako wpis kompilacji można korzystać we właściwości programu MSBuild "GeneratePackageOnBuild" - target [#4145](https://github.com/NuGet/Home/issues/4145)

- Użyj właściwości NuGet RestoreProjectStyle do utworzenia określonego projektu NuGet — [#4134](https://github.com/NuGet/Home/issues/4134)

- Dostosowania przywracania dla zmienić przechodnie odwołania do projektu - [#4076](https://github.com/NuGet/Home/issues/4076)

- Dodaj właściwości NuGet w pliku docelowym dla projektów UWP nie - [#4030](https://github.com/NuGet/Home/issues/4030)

- Pomoc techniczna dla platformy uniwersalnej systemu Windows TargetPlatformVersion — [#3923](https://github.com/NuGet/Home/issues/3923)

- Metadane odwołania projektu do systemu projektu NuGet — komunikacji [#3922](https://github.com/NuGet/Home/issues/3922)

- Dodawanie interfejsu użytkownika dla trybu pakowania - [#3921](https://github.com/NuGet/Home/issues/3921)

- Starsza wersja `.csproj` potrzebuje NugetTargetMoniker i RuntimeIdentifiers w proj/cele — [#3854](https://github.com/NuGet/Home/issues/3854)

- Pakiet instalacyjny nakładają się przy użyciu automatycznego przywracania - [#3836](https://github.com/NuGet/Home/issues/3836)

- Menu kontekstowe QueryStatus nie się zdarzyć, gdy nie został załadowany pakietu VSPackage - [#3835](https://github.com/NuGet/Home/issues/3835)

- Przywracanie rozwiązań i kompilacji przywracania w dalszym ciągu wyświetlać okien dialogowych - [#3789](https://github.com/NuGet/Home/issues/3789)

- Izoluj wersji VSSDK NuGet.Clients kompilacji rozwiązań — [#3890](https://github.com/NuGet/Home/issues/3890)

## <a name="links-to-github-issues-fixed-in-rtm"></a>Linki do serwisu GitHub problemy rozwiązane w wersji RTM
[Lista problemów 1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[Lista problemów 2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[Lista problemów 3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[Lista problemów z 4](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[Lista problemów z 5](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
