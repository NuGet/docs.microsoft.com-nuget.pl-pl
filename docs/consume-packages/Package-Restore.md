---
title: Przywracanie pakietów NuGet
description: Omówienie sposobu przywracania pakietów NuGet przez projekt, w tym sposobu wyłączania przywracania i ograniczania wersji.
author: JonDouglas
ms.author: jodou
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: 6cdc826c85f233c7108a53ad244aa8c47df0be67
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901840"
---
# <a name="restore-packages-using-package-restore"></a>Przywracanie pakietów przy użyciu funkcji przywracania pakietów

Aby promować czyste środowisko projektowe i zmniejszyć rozmiar repozytorium, przywracanie pakietów **NuGet** instaluje wszystkie zależności projektu wymienione w pliku projektu lub `packages.config` . Polecenia .NET Core 2.0+ `dotnet build` i `dotnet run` wykonają automatyczne przywracanie pakietów. Visual Studio automatycznie przywracać pakiety podczas kompilowania projektu, a pakiety można przywrócić w dowolnym momencie za pomocą programu Visual Studio, , i xbuild w `nuget restore` `dotnet restore` programie Mono.

Przywracanie pakietów zapewnia, że wszystkie zależności projektu są dostępne bez konieczności przechowywania ich w kontroli źródła. Aby skonfigurować repozytorium kontroli źródła w celu wykluczenia plików binarnych pakietu, zobacz [Pakiety i kontrola źródła](../consume-packages/packages-and-source-control.md). 

## <a name="package-restore-overview"></a>Omówienie przywracania pakietów

Przywracanie pakietów najpierw instaluje bezpośrednie zależności projektu zgodnie z potrzebami, a następnie instaluje wszelkie zależności tych pakietów w całym grafie zależności.

Jeśli pakiet nie został jeszcze zainstalowany, pakiet NuGet najpierw próbuje pobrać go z pamięci [podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md). Jeśli pakiet nie znajduje się w pamięci podręcznej, narzędzie NuGet spróbuje pobrać pakiet ze wszystkich włączonych źródeł na liście w menu Narzędzia Opcje NuGet Menedżer pakietów źródeł pakietów w  >    >    >   programie Visual Studio. Podczas przywracania program NuGet ignoruje kolejność źródeł pakietów i używa pakietu z tego, które źródło odpowiada najpierw na żądania. Aby uzyskać więcej informacji na temat zachowania rozwiązania NuGet, zobacz [Typowe konfiguracje NuGet](Configuring-NuGet-Behavior.md). 

> [!Note]
> NuGet nie wskazuje błędu przywracania pakietu, dopóki wszystkie źródła nie zostaną sprawdzone. W tym czasie program NuGet zgłasza błąd tylko dla ostatniego źródła na liście. Ten błąd oznacza, że pakiet  nie był obecny w żadnym z innych źródeł, mimo że błędy nie są wyświetlane osobno dla każdego z tych źródeł.

## <a name="restore-packages"></a>Przywracanie pakietów

Przywracanie pakietu próbuje zainstalować wszystkie zależności pakietu do prawidłowego stanu zgodnego z odwołaniami do pakietu w pliku projektu *(csproj)* lub w *packages.config* pliku. (W Visual Studio odwołania są wyświetlane w Eksplorator rozwiązań w obszarze **Zależności \ NuGet** lub w **węźle Odwołania).**

1. Jeśli odwołania do pakietu w pliku projektu są poprawne, użyj preferowanego narzędzia do przywracania pakietów.

   - [Visual Studio](#restore-using-visual-studio) [(przywracanie automatyczne lub](#restore-packages-automatically-using-visual-studio) przywracanie [ręczne)](#restore-packages-manually-using-visual-studio)
   - [Interfejs wiersza polecenia dotnet](#restore-using-the-dotnet-cli)
   - [Interfejs wiersza polecenia nuget.exe](#restore-using-the-nugetexe-cli)
   - [MSBuild](#restore-using-msbuild)
   - [Azure Pipelines](#restore-using-azure-pipelines)
   - [Azure DevOps Server](#restore-using-azure-devops-server)

   Jeśli odwołania do pakietu w pliku projektu *(csproj)* lub w plikupackages.configsą nieprawidłowe (nie są zgodne z żądanym stanem po przywróceniu pakietu), zamiast *tego* należy zainstalować lub zaktualizować pakiety.

   W przypadku projektów korzystających z packageReference po pomyślnym przywróceniu pakiet powinien być obecny w folderze *global-packages,* a `obj/project.assets.json` plik zostanie ponownie utworzony. W przypadku `packages.config` projektów korzystających z programu pakiet powinien pojawić się w `packages` folderze projektu. Projekt powinien teraz zostać pomyślnie skompilowany. 

2. Po uruchomieniu przywracania pakietu, jeśli nadal występują brakujące pakiety lub błędy związane z pakietem (takie jak ikony błędów w programie Eksplorator rozwiązań w programie Visual Studio), może być konieczne postępuj zgodnie z instrukcjami opisanymi w części [Rozwiązywanie](package-restore-troubleshooting.md) problemów z błędami przywracania pakietów lub, alternatywnie, ponowne instalowanie i [aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md).

   W Visual Studio konsoli Menedżer pakietów udostępnia kilka elastycznych opcji ponownego instalowania pakietów. Zobacz [Using Package-Update (Korzystanie z aktualizacji pakietu).](reinstalling-and-updating-packages.md#using-update-package)

## <a name="restore-using-visual-studio"></a>Przywracanie przy użyciu Visual Studio

W Visual Studio w systemie Windows:

- Automatyczne przywracanie pakietów lub

- Ręczne przywracanie pakietów

### <a name="restore-packages-automatically-using-visual-studio"></a>Automatyczne przywracanie pakietów przy użyciu Visual Studio

Przywracanie pakietu odbywa się automatycznie podczas tworzenia projektu na podstawie szablonu lub kompilowania projektu, z zastrzeżeniem opcji dostępnych w temacie Włączanie i [wyłączanie przywracania pakietu.](#enable-and-disable-package-restore-in-visual-studio) W programie NuGet 4.0+ przywracanie odbywa się również automatycznie w przypadku zmiany projektu w stylu zestawu SDK (zazwyczaj jest to projekt platformy .NET Core .NET Standard).

1. Włącz automatyczne przywracanie pakietów, wybierając pozycję Opcje narzędzi NuGet Menedżer pakietów , a następnie wybierając pozycję Automatycznie sprawdzaj brakujące pakiety podczas kompilacji w  >    >   **programie Visual Studio** **obszarze Przywracanie pakietów.**

   W przypadku projektów innych niż w stylu zestawu SDK należy najpierw wybrać pozycję Zezwalaj pakietowi **NuGet na** pobieranie brakujących pakietów, aby włączyć opcję automatycznego przywracania.

1. Skompiluj projekt.

   Jeśli co najmniej jeden indywidualny pakiet nadal nie został poprawnie **zainstalowany,** Eksplorator rozwiązań ikona błędu. Kliknij prawym przyciskiem myszy i wybierz  polecenie **Zarządzaj pakietami NuGet,** a następnie użyj Menedżer pakietów, aby odinstalować i ponownie zainstalować odpowiednie pakiety. Aby uzyskać więcej informacji, zobacz [Ponowne instalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md)

   Jeśli zostanie wyświetlony błąd "Ten projekt odwołuje się do pakietów NuGet, których brakuje na tym komputerze", lub "Co najmniej jeden pakiet NuGet musi zostać przywrócony, ale nie można tego zrobić, ponieważ nie udzielono [zgody",](#enable-and-disable-package-restore-in-visual-studio)włącz automatyczne przywracanie . W przypadku starszych projektów zobacz również [Migrowanie do automatycznego przywracania pakietów.](#migrate-to-automatic-package-restore-visual-studio) Zobacz też rozwiązywanie [problemów z przywracaniem pakietów.](Package-restore-troubleshooting.md)

### <a name="restore-packages-manually-using-visual-studio"></a>Przywróć pakiety ręcznie przy użyciu Visual Studio

1. Włącz przywracanie pakietów, wybierając **opcje**  >  **narzędzi**  >  **NuGet Menedżer pakietów**. W **obszarze Opcje przywracania** pakietów wybierz pozycję **Zezwalaj programowi NuGet na pobieranie brakujących pakietów.**

1. W **Eksplorator rozwiązań** kliknij rozwiązanie prawym przyciskiem myszy i wybierz polecenie **Przywróć pakiety NuGet.**

   Jeśli co najmniej jeden indywidualny pakiet nadal nie został poprawnie **zainstalowany,** Eksplorator rozwiązań ikona błędu. Kliknij prawym przyciskiem myszy i wybierz polecenie  Zarządzaj **pakietami NuGet,** a następnie użyj Menedżer pakietów, aby odinstalować i ponownie zainstalować odpowiednie pakiety. Aby uzyskać więcej informacji, zobacz [Ponowne instalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md)

   Jeśli zostanie wyświetlony błąd "Ten projekt odwołuje się do pakietów NuGet, których brakuje na tym komputerze", lub "Co najmniej jeden pakiet NuGet musi zostać przywrócony, ale nie można tego zrobić, ponieważ nie udzielono [zgody",](#enable-and-disable-package-restore-in-visual-studio)włącz automatyczne przywracanie . W przypadku starszych projektów zobacz również [Migrowanie do automatycznego przywracania pakietów.](#migrate-to-automatic-package-restore-visual-studio) Zobacz też rozwiązywanie [problemów z przywracaniem pakietów.](Package-restore-troubleshooting.md)

### <a name="enable-and-disable-package-restore-in-visual-studio"></a>Włączanie i wyłączanie przywracania pakietów w Visual Studio

W Visual Studio można kontrolować przywracanie pakietów przede wszystkim za pomocą **opcji**  >  **narzędzi**  >  **NuGet Menedżer pakietów**:

![Kontrolowanie przywracania pakietów za pomocą Menedżer pakietów NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Ustawienie Zezwalaj** programowi NuGet na pobieranie brakujących pakietów steruje wszystkimi formami przywracania pakietów przez zmianę ustawienia w sekcji packageRestore pliku w systemie Windows lub w systemie `packageRestore/enabled` [](../reference/nuget-config-file.md#packagerestore-section) `NuGet.Config` `%AppData%\NuGet\` `~/.nuget/NuGet/` Mac/Linux. To ustawienie włącza również **polecenie Przywróć** pakiety NuGet w menu kontekstowym rozwiązania w Visual Studio, .

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    
  > [!Note]
  > Aby globalnie zastąpić to ustawienie, ustaw zmienną środowiskową `packageRestore/enabled` **EnableNuGetPackageRestore** na wartość True lub False przed uruchomieniem Visual Studio lub uruchomieniem kompilacji.

- **Automatycznie sprawdzaj brakujące pakiety podczas** kompilacji w programie Visual Studio automatycznie przywracać, zmieniając ustawienie w sekcji `packageRestore/automatic` [packageRestore](../reference/nuget-config-file.md#packagerestore-section) `NuGet.Config` pliku. Jeśli ta opcja jest ustawiona na wartość True, uruchomienie kompilacji z Visual Studio automatycznie przywraca wszystkie brakujące pakiety. To ustawienie nie ma wpływu na kompilacje uruchamiane z wiersza polecenia programu MSBuild.

    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

Aby włączyć lub wyłączyć przywracanie pakietów dla wszystkich użytkowników na komputerze, deweloper lub firma może dodać ustawienia konfiguracji do pliku `nuget.config` globalnego. Globalna jest w systemie Windows w systemie , czasami w określonym Visual Studio folderze lub w `nuget.config` `%ProgramData%\NuGet\Config` systemie `\{IDE}\{Version}\{SKU}\` Mac/Linux w folderze `~/.local/share` . Poszczegórni użytkownicy mogą następnie selektywnie włączyć przywracanie zgodnie z potrzebami na poziomie projektu. Aby uzyskać więcej informacji na temat sposobu, w jaki nuGet określa priorytety dla wielu plików konfiguracji, zobacz [Typowe konfiguracje NuGet.](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)

> [!Important]
> Jeśli edytujesz ustawienia bezpośrednio w programie , uruchom Visual Studio, aby w oknie dialogowym Opcje `packageRestore` `nuget.config` wyświetlane są bieżące wartości. 

### <a name="choose-default-package-management-format"></a>Wybieranie domyślnego formatu zarządzania pakietami

![Kontrolowanie domyślnego formatu zarządzania pakietami za pomocą opcji Menedżer pakietów NuGet](media/Restore-02-PackageFormatOptions.png)

NuGet ma dwa formaty, w których projekt może używać pakietów: [`PackageReference`](package-references-in-project-files.md) i [`packages.config`](../reference/packages-config.md) . Domyślny format można wybrać z listy rozwijanej w obszarze **Zarządzanie pakietami** nagłówka. Dostępna jest również opcja monitowania o pierwszy pakiet zainstalowany w projekcie.

> [!Note]
> Jeśli projekt nie obsługuje obu formatów zarządzania pakietami, używany format zarządzania pakietami będzie formatem zgodnym z projektem i w związku z tym może nie być domyślnym ustawieniem w opcjach. Ponadto program NuGet nie będzie monitować o wybór podczas pierwszej instalacji pakietu, nawet jeśli opcja jest zaznaczona w oknie opcji.
>
> Jeśli Menedżer pakietów do zainstalowania pierwszego pakietu w projekcie, program NuGet nie będzie monitować o wybór formatu, nawet jeśli opcja zostanie wybrana w oknie opcji.

## <a name="restore-using-the-dotnet-cli"></a>Przywracanie przy użyciu interfejsu wiersza polecenia dotnet

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]

> [!IMPORTANT]
> Aby dodać brakujące odwołanie do pakietu do pliku projektu, użyj [polecenia dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x), które również uruchamia polecenie `restore` .

## <a name="restore-using-the-nugetexe-cli"></a>Przywracanie przy użyciu interfejsu wiersza nuget.exe interfejsu wiersza polecenia

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

> [!IMPORTANT]
> Polecenie `restore` nie modyfikuje pliku projektu ani pliku *packages.config*. Aby dodać zależność, dodaj pakiet za pośrednictwem interfejsu użytkownika Menedżer pakietów lub  konsoli w programie Visual Studio lub zmodyfikujpackages.config, a następnie uruchom `install` lub `restore` .

## <a name="restore-using-msbuild"></a>Przywracanie przy użyciu programu MSBuild

Użyj polecenia [msbuild -t:restore,](../reference/msbuild-targets.md#restore-target) aby przywrócić pakiety wymienione w pliku projektu (zobacz [PackageReference](package-references-in-project-files.md)) i począwszy od projektów MSBuild 16.5+. `packages.config`

 To polecenie jest dostępne tylko w programach NuGet 4.x+ i MSBuild 15.1+, które są dostępne w wersji Visual Studio 2017 i wyższych.
Począwszy od programu MSBuild 16.5+, to polecenie może również przywracać oparte na `packages.config` projektach po uruchomieniu polecenia z poleceniem `-p:RestorePackagesConfig=true` .

1. Otwórz wiersz polecenia dewelopera (w **polu Wyszukaj** wpisz wiersz **polecenia dewelopera**).

   Zazwyczaj chcesz uruchomić aplikację dla programu wiersz polecenia dla deweloperów Visual Studio menu **Start,** ponieważ zostanie ona skonfigurowana ze wszystkimi niezbędnymi ścieżkami dla programu MSBuild.

2. Przejdź do folderu zawierającego plik projektu i wpisz następujące polecenie.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

3. Wpisz następujące polecenie, aby ponownie skompilować projekt.

   ```cmd
   msbuild
   ```

   Upewnij się, że dane wyjściowe programu MSBuild wskazują, że kompilacja została ukończona pomyślnie.
   
> [!Note]
> Program msbuild ma `-restore` przełącznik, który uruchamia `Restore` , ponownie ładuje projekt, a następnie tworzy kompilację. Zobacz [Przywracanie i budowania za pomocą jednego polecenia MSBuild.](../reference/msbuild-targets.md#restoring-and-building-with-one-msbuild-command)

```cmd
# Will restore the project, then build, since build is the default target.
msbuild -restore
```

## <a name="restore-using-azure-pipelines"></a>Przywracanie przy użyciu Azure Pipelines

Podczas tworzenia definicji kompilacji w programie Azure Pipelines zadania przywracania [NuGet](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) lub przywracania .NET [Core](/azure/devops/pipelines/tasks/build/dotnet-core-cli) w definicji przed dowolnymi zadaniami kompilacji. Niektóre szablony kompilacji domyślnie zawierają zadanie przywracania.

## <a name="restore-using-azure-devops-server"></a>Przywracanie przy użyciu Azure DevOps Server

Azure DevOps Server i TFS 2013 lub nowszy automatycznie przywracają pakiety podczas kompilacji, jeśli używasz szablonu TFS 2013 lub nowszej kompilacji zespołowej. W przypadku wcześniejszych wersji serwera TFS można dołączyć krok kompilacji w celu uruchomienia opcji przywracania wiersza polecenia lub opcjonalnie przeprowadzić migrację szablonu kompilacji do nowszej wersji. Aby uzyskać więcej informacji, zobacz [Konfigurowanie przywracania pakietów za pomocą kompilacji Team Foundation Build](../consume-packages/team-foundation-build.md).

## <a name="constrain-package-versions-with-restore"></a>Ograniczanie wersji pakietów za pomocą przywracania

Gdy program NuGet przywraca pakiety za pomocą dowolnej metody, honoruje wszelkie ograniczenia określone w pliku `packages.config` projektu lub :

- W `packages.config` pliku można określić zakres wersji we właściwości `allowedVersion` zależności. Aby [uzyskać więcej informacji,](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) zobacz Ograniczanie wersji uaktualnienia. Na przykład:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- W pliku projektu można użyć funkcji PackageReference, aby bezpośrednio określić zakres zależności. Na przykład:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

We wszystkich przypadkach należy użyć notacji opisanej w [te tematze Package versioning (Wersjonarowanie pakietów).](../concepts/package-versioning.md)

## <a name="force-restore-from-package-sources"></a>Wymuszanie przywracania ze źródeł pakietów

Domyślnie operacje przywracania NuGet używają pakietów z *folderów global-packages* i *http-cache,* które opisano w tece Zarządzanie globalnymi pakietami [i folderami pamięci podręcznej](managing-the-global-packages-and-cache-folders.md).

Aby uniknąć używania *folderu global-packages,* wykonaj jedną z następujących czynności:

- Wyczyść folder przy użyciu `nuget locals global-packages -clear` lub `dotnet nuget locals global-packages --clear` .
- Tymczasowo zmień lokalizację folderu *global-packages* przed operacją przywracania, korzystając z jednej z następujących metod:
  - Ustaw zmienną NUGET_PACKAGES środowiskowej na inny folder.
  - Utwórz `NuGet.Config` plik, który ustawia `globalPackagesFolder` (jeśli używasz PackageReference) lub (jeśli używasz `repositoryPath` ) do innego `packages.config` folderu. Aby uzyskać więcej informacji, zobacz [ustawienia konfiguracji](../reference/nuget-config-file.md#config-section).
  - Tylko program MSBuild: określ inny folder za pomocą `RestorePackagesPath` właściwości .

Aby uniknąć używania pamięci podręcznej dla źródeł HTTP, wykonaj jedną z następujących czynności:

- Użyj opcji z opcją lub z `-NoCache` `nuget restore` `--no-cache` opcją `dotnet restore` . Te opcje nie mają wpływu na operacje przywracania za pośrednictwem Visual Studio Menedżer pakietów lub konsoli.
- Wyczyść pamięć podręczną przy użyciu `nuget locals http-cache -clear` lub `dotnet nuget locals http-cache --clear` .
- Tymczasowo ustaw zmienną NUGET_HTTP_CACHE_PATH na inny folder.

## <a name="migrate-to-automatic-package-restore-visual-studio"></a>Migrowanie do automatycznego przywracania pakietów (Visual Studio)

W przypadku programu NuGet 2.6 i starszych wersji przywracanie pakietów zintegrowanych z programem MSBuild było wcześniej obsługiwane, ale nie jest to już prawdziwe. (Zazwyczaj było to włączane przez kliknięcie prawym przyciskiem myszy rozwiązania w Visual Studio i wybranie pozycji Włącz przywracanie **pakietów NuGet).** Jeśli projekt używa przestarzałego przywracania pakietów zintegrowanych z programem MSBuild, przemigruj do automatycznego przywracania pakietów.

Projekty, które używają MSBuild-Integrated przywracania pakietu, zwykle zawierają folder *.nuget* z *trzema* plikami:NuGet.config, *nuget.exe* i *NuGet.targets.* Obecność pliku *NuGet.targets* określa, czy program NuGet będzie nadal używać podejścia zintegrowanego z programem MSBuild, więc ten plik musi zostać usunięty podczas migracji.

Aby przeprowadzić migrację do automatycznego przywracania pakietów:

1. Zamknij program Visual Studio.
2. Usuń *pliki .nuget/nuget.exe* *i .nuget/NuGet.targets.*
3. Dla każdego pliku projektu usuń `<RestorePackages>` element i usuń wszelkie odwołania do pliku *NuGet.targets.*

Aby przetestować automatyczne przywracanie pakietów:

1. Usuń folder *packages* z rozwiązania.
2. Otwórz rozwiązanie w Visual Studio i rozpocznij kompilację.

   Automatyczne przywracanie pakietów powinno pobierać i instalować każdy pakiet zależności bez dodawania ich do kontroli źródła.

## <a name="troubleshooting"></a>Rozwiązywanie problemów

Zobacz [Rozwiązywanie problemów z przywracaniem pakietu.](Package-restore-troubleshooting.md)
