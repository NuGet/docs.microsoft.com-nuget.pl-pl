---
title: Informacje o wersji RC NuGet 4.0 | Dokumentacja firmy Microsoft
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 03/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informacje o tym znanych problemów, poprawki, dodatkowe funkcje i dcr RTM 4.0 NuGet."
keywords: NuGet 4.0 RTM informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d1ab89f0decb64a64d04dc293e5273b577e8398b
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/20/2018
---
# <a name="nuget-40-rtm-release-notes"></a>Informacje o wersji 4.0 RTM NuGet

[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z 4.0 NuGet, który dodaje obsługę platformy .NET Core, licznych poprawki jakości i zwiększa wydajność. Tej wersji wprowadzono również kilka ulepszeń, takich jak obsługa PackageReference polecenia NuGet jako MSBuild elementy docelowe, przywraca pakietu tła i inne.

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

Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania. Alternatywnie, spróbuj usunąć `project.lock.json` i przywracanie ponownie.

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a>W projektach .NET Core użytkownik może pozostać w pętli nieskończonej przywracania w przypadku użycia pakietu zawierającego zestaw z nieprawidłowym podpisem

#### <a name="issue"></a>Problem

Czasami, w przypadku użycia pakietu zawierającego zestaw z nieprawidłowym podpisem lub gdy wersja pakietu została ustawiona za pomocą znacznika „DateTime”, automatyczne przywracanie pakietu będzie uruchamiane w pętli nieskończonej. [NuGet#4542](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a>Obejście

Obecnie nie istnieje obejście tego problemu.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Nie można wyświetlić, dodać lub zaktualizować DotNetCLITools, za pomocą Menedżera pakietów Nuget

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

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a>Problemy, które usunięto w wersji RTM programu NuGet 4.0 przedziale czasu

[Informacje o wersji RC 4.0 NuGet](../release-notes/nuget-4.0-RC.md) -Wyświetla wszystkie problemy u NuGet 4.0 RC

### <a name="features"></a>Funkcje

- Localize — ciągi w NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)

- Nuget wymusza załadować projekty aplikacji sieci web w trybie LSL - [#4258](https://github.com/NuGet/Home/issues/4258)

- Wsparcie AutoReferenced PackageReference wersja bloku zmiany w interfejsie użytkownika dla pakietów "zainstalowany zestaw sdk" - [#4044](https://github.com/NuGet/Home/issues/4044)

- Poprawnie komunikacji PackageSpec.Version wszelkie zależności projektu (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)

- obsługuje usuwania odwołań w `.csproj` z commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)

- Obsługuje przywracania dla projektów PackageReference (normalny i xplat) i ładowania rozwiązania Lightweight - [#4003](https://github.com/NuGet/Home/issues/4003)

- obsługę dodawania odwołania do `.csproj` z commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)

- Obsługa Przywracanie NuGet Lightweight ładowania rozwiązania dla `packages.config` lub `project.json`  -  [#3711](https://github.com/NuGet/Home/issues/3711)

- Pliki obsługi w nuget wygenerowany plik elementów docelowych - [#3683](https://github.com/NuGet/Home/issues/3683)

- Ustanowić CI Mono do weryfikacji nuget.exe dla komputerów Mac przy użyciu programu MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)

- Przenieś NuGet wylogowuje zależności NuGet.Core v2 - [#3645](https://github.com/NuGet/Home/issues/3645)

### <a name="bugs"></a>Usterki

- Przywracanie NuGet w programie Visual Studio nie przestrzega właściwości PackageId projektów - [#4586](https://github.com/NuGet/Home/issues/4586)

- Błąd NuGet ProjectSystemCache podczas dodawania pakietu w pakiecie vsix - [#4545](https://github.com/NuGet/Home/issues/4545)

- Pakiet zgłasza wyjątek, jeśli IncludeSource jest używany w projekcie z wielu TFMs - [#4536](https://github.com/NuGet/Home/issues/4536)

- Awarie 2017 RC3 VS przy użyciu aktualizacji całym rozwiązaniu pakietów zarządzania — [#4474](https://github.com/NuGet/Home/issues/4474)

- Nie można odinstalować nowo zainstalowanego pakietu - [#4435](https://github.com/NuGet/Home/issues/4435)

- Podczas migracji do PackageRef, hybrydowych rozwiązań zachowują się dziwne przywracania - [#4433](https://github.com/NuGet/Home/issues/4433)

- Tworzenie wkrótce po uruchamianie NuGet działanie (instalację aktualizacji, przywracania), może spowodować VS do zawieszenia - [#4420](https://github.com/NuGet/Home/issues/4420)

- Zawieszenie interfejsu użytkownika — Zakleszczenie podczas inicjowania NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)

- Dodaj polecenie pakietu należy dodać wersji jako atrybut zamiast elementu - [#4325](https://github.com/NuGet/Home/issues/4325)

- Przywróć DotNet foo.sln — kończy się niepowodzeniem, podczas konfiguracji w SLN spowodować wykresu przywracania — projekty zduplikowaną (ale różnicowego config) [#4316](https://github.com/NuGet/Home/issues/4316)

- Zawartości tylko pakiety - [#3668](https://github.com/NuGet/Home/issues/3668)

- Domyślnie opcja rezygnacji z pakietu format selektor, opcja - [#4468](https://github.com/NuGet/Home/issues/4468)

- Danych o wydajności: Projekt CreateUAP_CSharp_VS.01.1.Create uwzględniona Duration_TotalElapsedTime przez 3,153.570 ms (149.1%). Plan bazowy 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)

- Danych o wydajności: Rozwiązanie ManagedLangs_CS_DDRIT.0300.Rebuild uwzględniona Duration_TotalElapsedTime przez 1,5 s. Plan bazowy 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)

- Wyznaczenie zakończy się niepowodzeniem w projektach multi TFM - [#4419](https://github.com/NuGet/Home/issues/4419)

- Danych o wydajności: Rozwiązanie WebForms_DDRIT.1200.Close uwzględniona VM_ImagesInMemory_Total_devenv według liczby 3.000 (0,5%). Plan bazowy 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)

- vsfeedback — pakiet ostrzeżenia, gdy netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)

- Pathtoolongexception — podczas próby dodania pakiet NuGet do pustych aplikacji sieci web platformy ASP.NET Core - [#4391](https://github.com/NuGet/Home/issues/4391)

- Pakiet jest uruchamiany zbyt często — dotnet pakietu zakończy się niepowodzeniem z nim to zależność cykliczną w docelowym zależności wykres obejmujące docelowej "Pakiet" - [#4381](https://github.com/NuGet/Home/issues/4381)

- Pakiet jest uruchamiany zbyt często — pakiet NuGet Generowanie nie zawiera wszystkie konfiguracje - [#4380](https://github.com/NuGet/Home/issues/4380)

- Dodawanie nuget NullReferenceException z packageref w projektach C++ - [#4378](https://github.com/NuGet/Home/issues/4378)

- Ułatwienia dostępu: Narrator nie komentować pole wyboru, aby Wybierz projekty, do zainstalowania pakietu do - [#4366](https://github.com/NuGet/Home/issues/4366)

- NuGet VS17 sporadycznie niepowodzenia nawiązywania połączenia źródła danych usługi VSO/VSTS — 365798 usterki VS - [#4365](https://github.com/NuGet/Home/issues/4365)

- Pliki pobierać dane wyjściowe do niewłaściwej lokalizacji, jeżeli PackagePath Określa ścieżkę jako "pliki" - [#4348](https://github.com/NuGet/Home/issues/4348)

- Docelowy pakiet dołącza właściwość PackageVersion o VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)

- Określanie ścieżki pakietu nie działa z dodatkiem Service pack dotnet — [#4321](https://github.com/NuGet/Home/issues/4321)

- NuGet dane wyjściowe licznych ostrzeżenia o zduplikowane Importy podczas przywracania - [#4304](https://github.com/NuGet/Home/issues/4304)

- Wybierz wygląd okna dialogowego "Menedżer pakietów NuGet Format" w obszarze ciemny motyw — [#4300](https://github.com/NuGet/Home/issues/4300)

- VS awarii przy przywracaniu kompilacji - [#4298](https://github.com/NuGet/Home/issues/4298)

- Visual Studio zakleszczenie po dodaniu TFM w targetframeworks, Zapisz, a następnie kompilacji. 10% czasu - [#4295](https://github.com/NuGet/Home/issues/4295)

- Pakiet nuget nie wyprowadza komunikat z potwierdzeniem na pakowania projektu- [#4294](https://github.com/NuGet/Home/issues/4294)

- PackTask zakończy się niepowodzeniem z powodu 4.1 System.IO.Compression nie można odnaleźć - [#4290](https://github.com/NuGet/Home/issues/4290)

- Pakiet jest uruchamiany zbyt często — PackTask często kończy się niepowodzeniem z konflikt dostępu do pliku - [#4289](https://github.com/NuGet/Home/issues/4289)

- NuGet zostanie otwarte okno danych wyjściowych podczas przywracania tła - [#4274](https://github.com/NuGet/Home/issues/4274)

- Wyeliminować element ServiceProvider jako niebezpieczne wzorzec kodowania, (co może spowodować zawieszeń) - [#4268](https://github.com/NuGet/Home/issues/4268)

- Wydajności/UIHang - poprawy odczyty DownloadTimeoutStream - [#4266](https://github.com/NuGet/Home/issues/4266)

- Zakleszczenie programu Visual Studio przy próbie Zamknij projekt zanim zakończy przywracanie NuGet - [#4257](https://github.com/NuGet/Home/issues/4257)

- Problemy z PackTask i pakowania `.nuspec`  -  [#4250](https://github.com/NuGet/Home/issues/4250)

- [vsfeedback] Nie można rozpoznać pakietów nuget dla nowego projektu (wymaga ponownego uruchomienia programu visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)

- [vsfeedback] "Wersja" listy rozwijanej, które zawiera wersje dostępnych pakietów, zmagania pozostanie zsynchronizowana z pakietu nuGet wybranego... - [#4198](https://github.com/NuGet/Home/issues/4198)

- Nuget.Client powinna być używana klasa JoinableTaskFactory CPS podczas interakcji z CPS do zapobiec zakleszczenie - [#4185](https://github.com/NuGet/Home/issues/4185)

- NuGet 3.5.0 nie rozpakowywania `.targets` z pakietu - [#4171](https://github.com/NuGet/Home/issues/4171)

- Pakiet DotNet nie obsługuje tytuł w `.csproj`  -  [#4150](https://github.com/NuGet/Home/issues/4150)

- Pakiet instalacyjny powoduje okna dialogowego błędu w wersji VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)

- Aktualizowanie pakietu dla platformy .net core projektu wydaje się nie działać zgodnie z interfejsu użytkownika nie Pobierz aktualizację CPS z nominate. - [#4035](https://github.com/NuGet/Home/issues/4035)

- Poprawa ostrzeżenie nierozpoznane odwołanie - [#3955](https://github.com/NuGet/Home/issues/3955)

- Pakiet DotNet — informacje o wersji — utraci ProjectReference [#3953](https://github.com/NuGet/Home/issues/3953)

- Tworzenie aplikacji platformy uniwersalnej systemu Windows tworzenia projektu i Odbuduj regresji całkowity czas — [#3873](https://github.com/NuGet/Home/issues/3873)

- Nawet po błędzie podczas przywracania zostanie wyświetlony komunikat przywrócone. - [#3799](https://github.com/NuGet/Home/issues/3799)

- ponownie opublikować Nuget.CommandLine 3.4.4 do Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)

- Na migracji, projekty zmienić z `project.json` do `.csproj` ---przywracania kończy się niepowodzeniem - [#4297](https://github.com/NuGet/Home/issues/4297)

- Niepowodzenie przywracania na xunit nowo utworzonego projektu testowego - [#4296](https://github.com/NuGet/Home/issues/4296)

- Projekty Core mogą wykraczać, blokowanie interfejsu użytkownika na open - [#4269](https://github.com/NuGet/Home/issues/4269)

- Napraw plik elementów docelowych dla zadania kompilacji — [#4267](https://github.com/NuGet/Home/issues/4267)

- Lista błędów zawiera błąd po kompilacji rozwiązania, które zwolnić przywoływanego projektu - [#4208](https://github.com/NuGet/Home/issues/4208)

- MSB4057: Element docelowy "_GenerateRestoreGraphProjectEntry" nie istnieje w projekcie. - [#4194](https://github.com/NuGet/Home/issues/4194)

- vsfeedback: interfejsu użytkownika Menedżera nuget dla rozwiązania ulegnie awarii po wybraniu wszystkich projektów - [#4191](https://github.com/NuGet/Home/issues/4191)

- nuget.exe msbuildpath zakończy się niepowodzeniem, jeśli znajduje się znakiem ukośnika — [#4180](https://github.com/NuGet/Home/issues/4180)

- vsfeedback: Przywracanie NuGet podać kilka ostrzeżeń odwołania projektu dla projektu LinqToTwitter - [#4156](https://github.com/NuGet/Home/issues/4156)

- Pakiet z `.csproj` nie ma atrybutu minClientVersion - [#4135](https://github.com/NuGet/Home/issues/4135)

- NuGet.Build.Tasks.Pack.dll dostarczanego delay zalogowany VS2017 (d15rel 26014.00)- [#4122](https://github.com/NuGet/Home/issues/4122)

- VSFeedback: Przywracanie nie powiodło się dla projektu programu VS 2015 wygenerowane z CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)

- VSFeedback: Błędy odtwarzania mogą przesłaniać bardziej szczegółowy komunikaty o błędach, które zapewniają można kompilacji — [#4113](https://github.com/NuGet/Home/issues/4113)

- [VSFeedback] Wystąpił błąd podczas przywracania pakietów NuGet dla projektu witryny sieci Web: wartość nie może mieć wartości null. - [#4092](https://github.com/NuGet/Home/issues/4092)

- Migracja zgłasza "Obiektu odwołania wyjątek" w NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)

- Pakiet DotNet powinien pakietu narzędzi z wersjami, które pakiet został utworzony przed - [#4063](https://github.com/NuGet/Home/issues/4063)

- Nowe przywracania tła zapisuje milisekund pasek gdy trwa sekund, aby przywrócić - stanu [#4036](https://github.com/NuGet/Home/issues/4036)

- Literówka w nie udało się rozwiązać, wszystkie projektu odwołań - [#4018](https://github.com/NuGet/Home/issues/4018)

- Włącz przepływy pracy PCM w scenariuszach odwołanie do pakietu - [#4016](https://github.com/NuGet/Home/issues/4016)

- Nie można odnaleźć zainstalowanych pakietów w pakiecie menedżera interfejsu użytkownika — [#4015](https://github.com/NuGet/Home/issues/4015)

- DotNet pakietu nie powiedzie się, gdy PackagePath jest pusty — [#3993](https://github.com/NuGet/Home/issues/3993)

- Przywróć zadań kończy się niepowodzeniem w scenariuszu użytkownik multi - [#3897](https://github.com/NuGet/Home/issues/3897)

- Nie można zmienić typu zawartości, podczas pakowania, za pomocą zadania pakiet NuGet- [#3895](https://github.com/NuGet/Home/issues/3895)

- Kopiuj pliki domyślne są nieprawidłowe dla MsBuild /t:pack — [#3894](https://github.com/NuGet/Home/issues/3894)

- Przywracanie pakietu instalacji podwójne rejestruje przywracania komunikat pakiety - [#3785](https://github.com/NuGet/Home/issues/3785)

- Usuń Guardrails - przywracania sekcji "środowisk uruchomieniowych" stosuje się tylko do bieżącego projektu - [#3768](https://github.com/NuGet/Home/issues/3768)

- Zadanie pakietów umieszcza pliki zawartości zarówno w "zawartości /" i "pliki /"- [#3718](https://github.com/NuGet/Home/issues/3718)

- DotNet dodatkiem Service Pack 3 bardzo tagu dzielenia - [#3701](https://github.com/NuGet/Home/issues/3701)

- Pakiet DotNet: pakowania projektów z pakietem odwołuje się do wyników w ostrzeżenie zduplikowane import - [#3665](https://github.com/NuGet/Home/issues/3665)

- Przywróć rejestrowania w programie VS nie zawsze pokazuj - [#3633](https://github.com/NuGet/Home/issues/3633)

- tekst pomocy zmiennych lokalnych nuget wymienionych nadal pamięci podręcznej pakiety - [#3592](https://github.com/NuGet/Home/issues/3592)

- Pozamałżeńskie Restore3 PackageReferences z TargetFrameworks. - [#3504](https://github.com/NuGet/Home/issues/3504)

- Nuget wybiera nieoczekiwany wersji programu MSBuild w programie VS "15" Preview 4 odchyleń Wiersz polecenia - [#3408](https://github.com/NuGet/Home/issues/3408)

- Zapis plików celów/arkuszy właściwości podczas przywracania nie powiodło się - [#3399](https://github.com/NuGet/Home/issues/3399)

- NuGet podczas przywracania nie jest zgodny tego samego podkładek compat jako MSBuild podczas uruchamiania w wierszu polecenia VS 15 - [#3387](https://github.com/NuGet/Home/issues/3387)

- Ponownie włącz PackFromProjectWithDevelopmentDependencySet dla VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)

- Blend problemów z programem NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)

- Integrowanie 4.0.0.2067 interfejsu wiersza polecenia i zestawu SDK repozytoriów dostarczany z RC2 — [#4029](https://github.com/NuGet/Home/issues/4029)

- VS zawieszeń podczas tworzenia nowej aplikacji konsoli Core, Zamknij rozwiązanie, otwórz rozwiązanie i Zamknij rozwiązanie - [#4008](https://github.com/NuGet/Home/issues/4008)

- Naciśnięcie zawieszenie otwierania projektu przed d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)

- Usuń elementy lokalne dotnet/nuget.exe komunikat pomocy doc — [#3919](https://github.com/NuGet/Home/issues/3919)

- Sprawdzenia pod kątem problemów z spacji końcowych lub początkowych - PackTask [#3906](https://github.com/NuGet/Home/issues/3906)

- Pakiet DotNet jest pakowania z obj nie bin - [#3880](https://github.com/NuGet/Home/issues/3880)

- Pakiet DotNet zawsze wydaje się, że wartość elementu ProjectReference w wersji 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)

- Pakiet DotNet kończy się niepowodzeniem z odwołań do projektu i <TargetFramework>  -  [#3865](https://github.com/NuGet/Home/issues/3865)

- LockRecursionException w ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)

- TRIM z wartości właściwości programu MSBuild - [#3819](https://github.com/NuGet/Home/issues/3819)

- Konsoliduj zdarzenia dwóch projektu zgłoszony podczas ładowania projektu — [#3759](https://github.com/NuGet/Home/issues/3759)

- Bibliotek p2p `project.assets.json` plik ma nieprawidłową wersję - [#3748](https://github.com/NuGet/Home/issues/3748)

- Przywróć awarii z powodu źródło danych nie odpowiada, a pakiet niedostępny — [#3672](https://github.com/NuGet/Home/issues/3672)

- nuget.exe mogą powodować zawieszanie na dużą ilość danych wyjściowych błąd MSBuild - [#3572](https://github.com/NuGet/Home/issues/3572)

- Przywracanie w kompilacji dla programu Blend nie powiedzie się po raz pierwszy, powiedzie się po raz drugi (VS scenariusz rozwiązany) — [#2121](https://github.com/NuGet/Home/issues/2121)

### <a name="dcrs"></a>Dcr

- migracji vsix z Instalatora vsix w wersji 2 do vsix w wersji 3 - [#4196](https://github.com/NuGet/Home/issues/4196)

- NuGet powinien mieć mechanizmu uzyskiwania ścieżki do pliku blokady w programie MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)

- Dodaj zasoby kompilacji do TFM zgodności wyboru i zasoby pliku - [#3296](https://github.com/NuGet/Home/issues/3296)

- Zdefiniuj nowy ProjectCapability "Pakiet" w pakiecie cele dotyczące włączania pakietu dotyczące możliwości — [#4146](https://github.com/NuGet/Home/issues/4146)

- Uruchom pakiet jako post kompilacji docelowy przygotować we właściwości "GeneratePackageOnBuild" MSBuild - [#4145](https://github.com/NuGet/Home/issues/4145)

- Użyj właściwości NuGet RestoreProjectStyle do utworzenia danego projektu NuGet - [#4134](https://github.com/NuGet/Home/issues/4134)

- Dostosowania przywracania przechodnie odwołania do projektu zmian - [#4076](https://github.com/NuGet/Home/issues/4076)

- Dodaj właściwości NuGet w pliku docelowym dla projektów aplikacje platformy UWP - [#4030](https://github.com/NuGet/Home/issues/4030)

- Obsługa platformy uniwersalnej systemu Windows TargetPlatformVersion - [#3923](https://github.com/NuGet/Home/issues/3923)

- Komunikacji metadanych odwołania projektu do systemu projektu NuGet - [#3922](https://github.com/NuGet/Home/issues/3922)

- Dodawanie interfejsu użytkownika dla trybu tworzenia pakietów - [#3921](https://github.com/NuGet/Home/issues/3921)

- Starsza wersja `.csproj` potrzebuje NugetTargetMoniker i RuntimeIdentifiers w proj/cele — [#3854](https://github.com/NuGet/Home/issues/3854)

- Pakiet instalacyjny nakładają się z przywracaniem auto - [#3836](https://github.com/NuGet/Home/issues/3836)

- Menu kontekstowe QueryStatus nie jest realizowane podczas VSPackage nie został załadowany - [#3835](https://github.com/NuGet/Home/issues/3835)

- Przywróć rozwiązania i przywrócić kompilacji w dalszym ciągu wyświetlać okien dialogowych - [#3789](https://github.com/NuGet/Home/issues/3789)

- Odizolowanego wersji VSSDK w kompilacji rozwiązania NuGet.Clients - [#3890](https://github.com/NuGet/Home/issues/3890)

## <a name="links-to-github-issues-fixed-in-rtm"></a>Łącza do GitHub problemy rozwiązane w wersji RTM
[Lista problemów 1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RTM")  
[Lista problemów 2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC4")  
[Lista problemów 3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC3")  
[Lista problemów 4](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC2")  
[Lista problemów 5](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC")
