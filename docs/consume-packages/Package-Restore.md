---
title: Przywracanie pakietu NuGet
description: Omówienie sposobu przywracania pakietów NuGet zależy od projektu, w tym jak wyłączyć przywracanie i ograniczać wersje.
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: c1f1957c58839ac763238938b476eb0882c56a59
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428745"
---
# <a name="restore-packages-using-package-restore"></a>Przywracanie pakietów przy użyciu przywracania pakietu

Aby promować czystsze środowisko programistyczne i zmniejszyć rozmiar repozytorium, narzędzie NuGet **Package Restore** instaluje `packages.config`wszystkie zależności projektu wymienione w pliku projektu lub pliku . .NET Core `dotnet build` 2.0+ `dotnet run` i polecenia zrobić automatyczne przywracanie pakietu. Visual Studio można przywrócić pakiety automatycznie podczas tworzenia projektu i można przywrócić pakiety `dotnet restore`w dowolnym momencie za pośrednictwem programu Visual Studio , `nuget restore`i xbuild na mono.

Przywracanie pakietu upewnia się, że wszystkie zależności projektu są dostępne, bez konieczności przechowywania ich w kontroli źródła. Aby skonfigurować repozytorium kontroli źródła w celu wykluczenia plików binarnych [pakietów, zobacz Pakiety i formant źródła](../consume-packages/packages-and-source-control.md). 

## <a name="package-restore-overview"></a>Omówienie przywracania pakietu

Przywracanie pakietu najpierw instaluje bezpośrednie zależności projektu w razie potrzeby, a następnie instaluje wszelkie zależności tych pakietów na całym wykresie zależności.

Jeśli pakiet nie jest jeszcze zainstalowany, NuGet najpierw próbuje pobrać go z [pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md). Jeśli pakiet nie znajduje się w pamięci podręcznej, NuGet próbuje pobrać pakiet ze wszystkich włączonych źródeł na liście w **narzędzia** > **opcje** > **NuGet Package Manager** > **źródła pakietów** w programie Visual Studio. Podczas przywracania NuGet ignoruje kolejność źródeł pakietów i używa pakietu z dowolnego źródła, które jest pierwsze, aby odpowiedzieć na żądania. Aby uzyskać więcej informacji na temat zachowania nuget, zobacz [typowe konfiguracje NuGet](Configuring-NuGet-Behavior.md). 

> [!Note]
> NuGet nie wskazuje na niepowodzenie przywracania pakietu, dopóki nie zostały sprawdzone wszystkie źródła. W tym czasie NuGet zgłasza błąd tylko dla ostatniego źródła na liście. Błąd oznacza, że pakiet nie był obecny w *żadnym* z innych źródeł, mimo że błędy nie są wyświetlane dla każdego z tych źródeł indywidualnie.

## <a name="restore-packages"></a>Przywracanie pakietów

Narzędzie Package Restore próbuje zainstalować wszystkie zależności pakietów do prawidłowego stanu odpowiadającego odwołaniom do pakietu w pliku projektu (*.csproj*) lub pliku *packages.config.* (W programie Visual Studio odwołania są wyświetlane w Eksploratorze rozwiązań w obszarze **zależności \ NuGet** lub węźle **Odwołania).**

1. Jeśli odwołania do pakietu w pliku projektu są poprawne, użyj preferowanego narzędzia do przywracania pakietów.

   - [Visual Studio](#restore-using-visual-studio) [(automatyczne przywracanie](#restore-packages-automatically-using-visual-studio) lub [ręczne przywracanie)](#restore-packages-manually-using-visual-studio)
   - [Interfejs wiersza polecenia dotnet](#restore-using-the-dotnet-cli)
   - [Interfejs wiersza polecenia nuget.exe](#restore-using-the-nugetexe-cli)
   - [MSBuild](#restore-using-msbuild)
   - [Azure Pipelines](#restore-using-azure-pipelines)
   - [Azure DevOps Server](#restore-using-azure-devops-server)

   Jeśli odwołania do pakietu w pliku projektu (*.csproj*) lub plik *packages.config* są niepoprawne (nie pasują do żądanego stanu po przywracaniu pakietu), należy zainstalować lub zaktualizować pakiety zamiast tego.

   W przypadku projektów korzystających z PackageReference, po pomyślnym przywróceniu `obj/project.assets.json` pakiet powinien znajdować się w folderze *pakietów globalnych,* a plik jest odtworzony. W przypadku `packages.config`projektów korzystających z pakietu `packages` powinien pojawić się w folderze projektu. Projekt powinien teraz pomyślnie zbudować. 

2. Po uruchomieniu narzędzia Przywracanie pakietu, jeśli nadal występują brakujące pakiety lub błędy związane z pakietem (takie jak ikony błędów w Eksploratorze rozwiązań w programie Visual Studio), może być konieczne przestrzeganie instrukcji opisanych w [przypadku błędów przywracania pakietu](package-restore-troubleshooting.md) lub, alternatywnie, [ponowne instalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md).

   W programie Visual Studio konsola Menedżera pakietów udostępnia kilka elastycznych opcji ponownej instalacji pakietów. Zobacz [Korzystanie z aktualizacji pakietu](reinstalling-and-updating-packages.md#using-update-package).

## <a name="restore-using-visual-studio"></a>Przywracanie przy użyciu programu Visual Studio

W programie Visual Studio w systemie Windows:

- Automatyczne przywracanie pakietów lub

- Ręczne przywracanie pakietów

### <a name="restore-packages-automatically-using-visual-studio"></a>Automatyczne przywracanie pakietów przy użyciu programu Visual Studio

Przywracanie pakietu odbywa się automatycznie podczas tworzenia projektu z szablonu lub tworzenia projektu, z zastrzeżeniem opcji w [Włącz i wyłącz przywracanie pakietu](#enable-and-disable-package-restore-in-visual-studio). W NuGet 4.0+ przywracanie odbywa się również automatycznie po wprowadzeniu zmian w projekcie w stylu SDK (zazwyczaj w projekcie .NET Core lub .NET Standard).

1. Włącz automatyczne przywracanie pakietu, wybierając pozycję**Opcje** >  **narzędzi** > **NuGet Package Manager**, a następnie wybierając opcję Automatycznie **sprawdzaj brakujące pakiety podczas kompilacji w programie Visual Studio w** obszarze **Przywracanie pakietów**.

   W przypadku projektów w stylu innych niż SDK należy najpierw wybrać **opcję Zezwalaj nugetowi na pobieranie brakujących pakietów,** aby włączyć opcję automatycznego przywracania.

1. Skompiluj projekt.

   Jeśli jeden lub więcej pojedynczych pakietów nadal nie jest poprawnie zainstalowanych, **Eksplorator rozwiązań** wyświetla ikonę błędu. Kliknij prawym przyciskiem myszy i wybierz pozycję **Zarządzaj pakietami NuGet**i użyj **Menedżera pakietów,** aby odinstalować i ponownie zainstalować pakiety, których dotyczy problem. Aby uzyskać więcej informacji, zobacz [Ponowne instalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md)

   Jeśli zostanie wyświetlony błąd "Ten projekt odwołuje się do pakietów NuGet, których brakuje na tym komputerze" lub "Jeden lub więcej pakietów NuGet musi zostać przywrócony, ale nie może być, ponieważ nie udzielono zgody", [włącz automatyczne przywracanie](#enable-and-disable-package-restore-in-visual-studio). W przypadku starszych projektów zobacz [Migracja do automatycznego przywracania pakietów](#migrate-to-automatic-package-restore-visual-studio). Zobacz też [Rozwiązywanie problemów z przywracaniem pakietów](Package-restore-troubleshooting.md).

### <a name="restore-packages-manually-using-visual-studio"></a>Ręczne przywracanie pakietów przy użyciu programu Visual Studio

1. Włącz przywracanie pakietu, wybierając **opcję Opcje** > **Options** > narzędzi**NuGet Package Manager**. W obszarze Opcje **przywracania pakietu** wybierz pozycję **Zezwalaj nugetowi na pobieranie brakujących pakietów**.

1. W **Eksploratorze rozwiązań**kliknij prawym przyciskiem myszy rozwiązanie i wybierz polecenie **Przywróć pakiety NuGet**.

   Jeśli jeden lub więcej pojedynczych pakietów nadal nie jest poprawnie zainstalowanych, **Eksplorator rozwiązań** wyświetla ikonę błędu. Kliknij prawym przyciskiem myszy i wybierz polecenie **Zarządzaj pakietami NuGet**, a następnie użyj **Menedżera pakietów,** aby odinstalować i ponownie zainstalować pakiety, których dotyczy problem. Aby uzyskać więcej informacji, zobacz [Ponowne instalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md)

   Jeśli zostanie wyświetlony błąd "Ten projekt odwołuje się do pakietów NuGet, których brakuje na tym komputerze" lub "Jeden lub więcej pakietów NuGet musi zostać przywrócony, ale nie może być, ponieważ nie udzielono zgody", [włącz automatyczne przywracanie](#enable-and-disable-package-restore-in-visual-studio). W przypadku starszych projektów zobacz [Migracja do automatycznego przywracania pakietów](#migrate-to-automatic-package-restore-visual-studio). Zobacz też [Rozwiązywanie problemów z przywracaniem pakietów](Package-restore-troubleshooting.md).

### <a name="enable-and-disable-package-restore-in-visual-studio"></a>Włączanie i wyłączanie przywracania pakietów w programie Visual Studio

W programie Visual Studio można kontrolować przywracanie pakietów głównie za pomocą**opcji** >  **narzędzi** > **NuGet Package Manager:**

![Opcje przywracania pakietu sterowania za pomocą menedżera pakietów NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Zezwalaj NuGet na pobieranie brakujących pakietów** `packageRestore/enabled` kontroluje wszystkie formy przywracania `NuGet.Config` pakietu, `%AppData%\NuGet\` zmieniając ustawienie `~/.nuget/NuGet/` w [sekcji packageRestore](../reference/nuget-config-file.md#packagerestore-section) pliku, w systemie Windows lub na komputerze Mac/Linux. To ustawienie włącza również polecenie **Przywróć pakiety NuGet** w menu kontekstowym rozwiązania w programie Visual Studio.

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
  > Aby globalnie zastąpić `packageRestore/enabled` ustawienie, ustaw zmienną środowiskową **EnableNuGetPackageRestore** z wartością True lub False przed uruchomieniem programu Visual Studio lub uruchomieniem kompilacji.

- **Automatyczne sprawdzanie brakujących pakietów podczas kompilacji w** `packageRestore/automatic` programie Visual Studio kontroluje automatyczne przywracanie, zmieniając ustawienie w [sekcji packageRestore](../reference/nuget-config-file.md#packagerestore-section) `NuGet.Config` pliku. Gdy ta opcja jest ustawiona na True, uruchomienie kompilacji z programu Visual Studio automatycznie przywraca brakujące pakiety. To ustawienie nie wpływa na kompilacje uruchamiane z wiersza polecenia MSBuild.

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

Aby włączyć lub wyłączyć przywracanie pakietu dla wszystkich użytkowników na komputerze, deweloper `nuget.config` lub firma może dodać ustawienia konfiguracji do pliku globalnego. Globalny `nuget.config` jest w `%ProgramData%\NuGet\Config`systemie Windows w `\{IDE}\{Version}\{SKU}\` , czasami w określonym folderze Visual Studio, lub w Mac / Linux w `~/.local/share`. Poszczególni użytkownicy mogą następnie selektywnie włączyć przywracanie zgodnie z potrzebami na poziomie projektu. Aby uzyskać więcej informacji na temat ustalania priorytetów przez nuget wielu plików konfiguracyjnych, zobacz [Typowe konfiguracje NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

> [!Important]
> Jeśli `packageRestore` ustawienia są edytowane `nuget.config`bezpośrednio w programie Visual Studio, aby okno dialogowe **Opcje** było wyświetlane w bieżącym oknie dialogowym.

### <a name="choose-default-package-management-format"></a>Wybieranie domyślnego formatu zarządzania pakietami

![Kontroluj domyślny format zarządzania pakietami za opcjami NuGet Package Manager](media/Restore-02-PackageFormatOptions.png)

NuGet ma dwa formaty, w których [`PackageReference`](package-references-in-project-files.md) [`packages.config`](../reference/packages-config.md)projekt może używać pakietów: i . Domyślny format można wybrać z listy rozwijanej w nagłówku **Zarządzanie pakietami.** Dostępna jest również opcja monitowana po zainstalowaniu pierwszego pakietu w projekcie.

> [!Note]
> Jeśli projekt nie obsługuje obu formatów zarządzania pakietami, używany format zarządzania pakietami będzie zgodny z projektem i dlatego może nie być domyślnym zestawem w opcjach. Ponadto NuGet nie wyświetli monitu o wybór w pierwszej instalacji pakietu, nawet jeśli opcja jest zaznaczona w oknie opcji.
>
> Jeśli Konsola Menedżera pakietów jest używana do zainstalowania pierwszego pakietu w projekcie, NuGet nie wyświetli monitu o wybór formatu, nawet jeśli opcja jest zaznaczona w oknie opcji.

## <a name="restore-using-the-dotnet-cli"></a>Przywracanie przy użyciu interfejsu wiersza polecenia dotnet

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]

> [!IMPORTANT]
> Aby dodać brakujące odwołanie do pakietu do pliku projektu, użyj `restore` [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x), który również uruchamia polecenie.

## <a name="restore-using-the-nugetexe-cli"></a>Przywracanie przy użyciu interfejsu wiersza polecenia nuget.exe

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

> [!IMPORTANT]
> Polecenie `restore`nie modyfikuje pliku projektu ani pliku *packages.config*. Aby dodać zależność, dodaj pakiet za pośrednictwem interfejsu użytkownika menedżera pakietów lub konsoli w programie Visual `install` `restore`Studio lub zmodyfikuj *plik packages.config,* a następnie uruchom albo .

## <a name="restore-using-msbuild"></a>Przywracanie przy użyciu usługi MSBuild

Aby przywrócić pakiety wymienione w pliku projektu za pomocą packagereference, użyj polecenia [msbuild -t:restore.](../reference/msbuild-targets.md#restore-target) To polecenie jest dostępne tylko w nuget 4.x+ i MSBuild 15.1+, które są dołączone do programu Visual Studio 2017 i nowszych wersji. Oba `nuget restore` `dotnet restore` i użyj tego polecenia dla odpowiednich projektów.

1. Otwórz wiersz polecenia Deweloper (w polu **Wyszukiwania** wpisz **wiersz polecenia Deweloper**).

   Zazwyczaj chcesz uruchomić wiersz polecenia dewelopera dla programu Visual Studio z menu **Start,** ponieważ zostanie on skonfigurowany ze wszystkimi niezbędnymi ścieżkami dla usługi MSBuild.

2. Przełącz się do folderu zawierającego plik projektu i wpisz następujące polecenie.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

3. Wpisz następujące polecenie, aby odbudować projekt.

   ```cmd
   msbuild
   ```

   Upewnij się, że dane wyjściowe MSBuild wskazuje, że kompilacja została pomyślnie ukończona.

## <a name="restore-using-azure-pipelines"></a>Przywracanie przy użyciu potoków platformy Azure

Podczas tworzenia definicji kompilacji w potokach platformy Azure, należy [uwzględnić](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) NuGet restore lub .NET Core [restore](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) task w definicji przed wszelkimi zadaniami kompilacji. Niektóre szablony kompilacji zawierają zadanie przywracania domyślnie.

## <a name="restore-using-azure-devops-server"></a>Przywracanie przy użyciu serwera DevOps platformy Azure

Usługi Azure DevOps Server i TFS 2013 i nowsze automatycznie przywracają pakiety podczas kompilacji, jeśli używasz szablonu kompilacji zespołu TFS 2013 lub nowszego. W przypadku wcześniejszych wersji TFS można dołączyć krok kompilacji w celu uruchomienia opcji przywracania wiersza polecenia lub opcjonalnie przeprowadzić migrację szablonu kompilacji do nowszej wersji. Aby uzyskać więcej informacji, zobacz [Konfigurowanie przywracania pakietu za pomocą team foundation build](../consume-packages/team-foundation-build.md).

## <a name="constrain-package-versions-with-restore"></a>Ograniczanie wersji pakietów za pomocą przywracania

Gdy NuGet przywraca pakiety za pomocą dowolnej metody, `packages.config` honoruje wszelkie ograniczenia określone w pliku projektu lub:

- W `packages.config`obszarze , można określić `allowedVersion` zakres wersji we właściwości zależności. Aby uzyskać więcej informacji, zobacz [Ograniczanie wersji uaktualniania.](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) Przykład:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- W pliku projektu można użyć PackageReference, aby określić zakres zależności bezpośrednio. Przykład:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

We wszystkich przypadkach należy użyć notacji opisanej w [wersji pakietu](../concepts/package-versioning.md).

## <a name="force-restore-from-package-sources"></a>Wymuszanie przywracania ze źródeł pakietów

Domyślnie operacje przywracania NuGet używają pakietów z *pakietów globalnych* i folderów *http-cache,* które są opisane w [obszarze Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](managing-the-global-packages-and-cache-folders.md).

Aby uniknąć używania folderu *pakietów globalnych,* wykonaj jedną z następujących czynności:

- Wyczyść `nuget locals global-packages -clear` `dotnet nuget locals global-packages --clear`folder za pomocą lub .
- Tymczasowo zmień lokalizację folderu *pakietów globalnych* przed operacją przywracania, korzystając z jednej z następujących metod:
  - Ustaw zmienną środowiskową NUGET_PACKAGES na inny folder.
  - Utwórz `NuGet.Config` plik, `globalPackagesFolder` który ustawia (jeśli `repositoryPath` używa packagereference) lub (jeśli używam `packages.config`) do innego folderu. Aby uzyskać więcej informacji, zobacz [ustawienia konfiguracji](../reference/nuget-config-file.md#config-section).
  - TYLKO MSBuild: Określ inny `RestorePackagesPath` folder z właściwością.

Aby uniknąć używania pamięci podręcznej dla źródeł HTTP, wykonaj jedną z następujących czynności:

- Użyj `-NoCache` opcji `nuget restore`z , `--no-cache` lub `dotnet restore`opcji z . Te opcje nie mają wpływu na operacje przywracania za pośrednictwem Menedżera pakietów programu Visual Studio lub konsoli.
- Wyczyść `nuget locals http-cache -clear` `dotnet nuget locals http-cache --clear`pamięć podręczną za pomocą lub .
- Tymczasowo ustaw zmienną środowiskową NUGET_HTTP_CACHE_PATH na inny folder.

## <a name="migrate-to-automatic-package-restore-visual-studio"></a>Migracja do automatycznego przywracania pakietów (Visual Studio)

Dla NuGet 2.6 i wcześniej, msbuild zintegrowane przywracanie pakietu był wcześniej obsługiwany, ale to już nie jest true. (Zazwyczaj włączono je, klikając prawym przyciskiem myszy rozwiązanie w programie Visual Studio i wybierając **pozycję Włącz przywracanie pakietu NuGet).** Jeśli projekt używa przestarzałego przywracania pakietu zintegrowanego z MSBuild, przemiń do automatycznego przywracania pakietu.

Projekty korzystające z przywracania pakietu MSBuild-Integrated zazwyczaj zawierają folder *.nuget* z trzema plikami: *NuGet.config*, *nuget.exe*i *NuGet.targets*. Obecność pliku *NuGet.targets* określa, czy NuGet będzie nadal używać msbuild-untegrated podejście, więc ten plik musi zostać usunięty podczas migracji.

Aby przeprowadzić migrację do automatycznego przywracania pakietu:

1. Zamknij program Visual Studio.
2. Usuń *pliki .nuget/nuget.exe* i *.nuget/NuGet.targets*.
3. Dla każdego pliku projektu `<RestorePackages>` usuń element i usuń wszelkie odwołania do *pliku NuGet.targets*.

Aby przetestować automatyczne przywracanie pakietu:

1. Usuń folder *pakietów* z rozwiązania.
2. Otwórz rozwiązanie w programie Visual Studio i uruchom kompilację.

   Automatyczne przywracanie pakietu należy pobrać i zainstalować każdy pakiet zależności, bez dodawania ich do kontroli źródła.

## <a name="troubleshooting"></a>Rozwiązywanie problemów

Zobacz [Rozwiązywanie problemów z przywracaniem pakietu](package-restore-troubleshooting.md).
