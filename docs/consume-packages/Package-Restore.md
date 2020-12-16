---
title: Przywracanie pakietu NuGet
description: Omówienie sposobu przywracania pakietów przez pakiet NuGet, od których zależy projekt, w tym sposobu wyłączania wersji przywracania i ograniczania.
author: JonDouglas
ms.author: jodou
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: bac4d88c29539f9fbe7b33b44ce11d350920d365
ms.sourcegitcommit: 650c08f8bc3d48dfd206a111e5e2aaca3001f569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97523529"
---
# <a name="restore-packages-using-package-restore"></a>Przywróć pakiety przy użyciu przywracania pakietów

Aby podwyższyć poziom czystego środowiska programistycznego i zmniejszyć rozmiar repozytorium, **przywracanie pakietu** NuGet instaluje wszystkie zależności projektu wymienione w pliku projektu lub `packages.config` . Polecenia programu .NET Core 2.0 + `dotnet build` i `dotnet run` wykonują automatyczne przywracanie pakietów. Program Visual Studio może automatycznie przywracać pakiety podczas kompilacji projektu, a pakiety można przywracać w dowolnym momencie za pomocą programu Visual Studio, `nuget restore` , `dotnet restore` i Xbuild na mono.

Przywracanie pakietu gwarantuje, że wszystkie zależności projektu są dostępne bez konieczności przechowywania ich w kontroli źródła. Aby skonfigurować repozytorium kontroli źródła w celu wykluczenia plików binarnych pakietu, zobacz [pakiety i kontrola źródła](../consume-packages/packages-and-source-control.md). 

## <a name="package-restore-overview"></a>Przegląd przywracania pakietu

Funkcja przywracania pakietu najpierw instaluje bezpośrednie zależności projektu w razie konieczności, a następnie instaluje wszystkie zależności tych pakietów w całym grafie zależności.

Jeśli pakiet nie jest już zainstalowany, program NuGet najpierw podejmie próbę pobrania go z [pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md). Jeśli pakiet nie znajduje się w pamięci podręcznej, program NuGet próbuje pobrać pakiet ze wszystkich włączonych źródeł znajdujących się na liście **narzędzi**  >  **Opcje** narzędzia  >  **Menedżer pakietów NuGet**  >   w programie Visual Studio. Podczas przywracania program NuGet ignoruje kolejność źródeł pakietów i używa pakietu z tego samego źródła, aby odpowiedzieć na żądania. Aby uzyskać więcej informacji o zachowaniu NuGet, zobacz [typowe konfiguracje NuGet](Configuring-NuGet-Behavior.md). 

> [!Note]
> Pakiet NuGet nie wskazuje błędu przywrócenia pakietu, dopóki nie zostaną sprawdzone wszystkie źródła. W tym czasie NuGet zgłosi błąd tylko dla ostatniego źródła na liście. Ten błąd oznacza, że pakiet nie był obecny w *żadnym* z innych źródeł, mimo że błędy nie są wyświetlane dla każdego z tych źródeł osobno.

## <a name="restore-packages"></a>Przywracanie pakietów

Przywracanie pakietu próbuje zainstalować wszystkie zależności pakietów do poprawnego stanu pasującego do odwołania do pakietu w pliku projektu (*. csproj*) lub pliku *packages.config* . (W programie Visual Studio odwołania pojawiają się w Eksplorator rozwiązań w obszarze **zależności \ NuGet** lub węzeł **odwołania** ).

1. Jeśli odwołania do pakietu w pliku projektu są poprawne, użyj preferowanego narzędzia, aby przywrócić pakiety.

   - [Visual Studio](#restore-using-visual-studio) ([automatyczne przywracanie](#restore-packages-automatically-using-visual-studio) lub [przywracanie ręczne](#restore-packages-manually-using-visual-studio))
   - [Interfejs wiersza polecenia dotnet](#restore-using-the-dotnet-cli)
   - [Interfejs wiersza polecenia nuget.exe](#restore-using-the-nugetexe-cli)
   - [MSBuild](#restore-using-msbuild)
   - [Azure Pipelines](#restore-using-azure-pipelines)
   - [Azure DevOps Server](#restore-using-azure-devops-server)

   Jeśli pakiet odwołuje się do pliku projektu (*. csproj*) lub pliku *packages.config* są niepoprawne (nie są one zgodne z żądanym stanem po przywróceniu pakietu), należy zamiast tego zainstalować lub zaktualizować pakiety.

   W przypadku projektów korzystających z PackageReference po pomyślnym przywróceniu pakiet powinien znajdować się w folderze *Global-Packages* , a `obj/project.assets.json` plik zostanie utworzony ponownie. W przypadku projektów używających `packages.config` pakiet powinien pojawić się w `packages` folderze projektu. Projekt powinien teraz zostać pomyślnie skompilowany. 

2. Po uruchomieniu przywracania pakietów, jeśli nadal występują brakujące pakiety lub błędy związane z pakietami (takie jak ikony błędów w Eksplorator rozwiązań w programie Visual Studio), może być konieczne wykonanie instrukcji opisanych w [temacie Rozwiązywanie problemów z błędami przywracania pakietów](package-restore-troubleshooting.md) lub, Alternatywnie, [ponowne instalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md).

   W programie Visual Studio konsola Menedżera pakietów udostępnia kilka elastycznych opcji ponownego instalowania pakietów. Zobacz [using Package-Update](reinstalling-and-updating-packages.md#using-update-package).

## <a name="restore-using-visual-studio"></a>Przywróć przy użyciu programu Visual Studio

W programie Visual Studio w systemie Windows:

- Przywróć pakiety automatycznie lub

- Ręcznie Przywróć pakiety

### <a name="restore-packages-automatically-using-visual-studio"></a>Przywróć pakiety automatycznie przy użyciu programu Visual Studio

Przywracanie pakietu odbywa się automatycznie podczas tworzenia projektu na podstawie szablonu lub kompilowania projektu, z zastosowaniem opcji w [Włączanie i wyłączanie przywracania pakietów](#enable-and-disable-package-restore-in-visual-studio). W programie NuGet 4.0 + przywracanie odbywa się również automatycznie po wprowadzeniu zmian w projekcie w stylu zestawu SDK (zazwyczaj jest to projekt .NET Core lub .NET Standard).

1. Włącz automatyczne przywracanie pakietów, wybierając pozycję **Narzędzia**  >    >  **Menedżer pakietów NuGet**, a następnie wybierając opcję **automatycznie sprawdzaj brakujące pakiety podczas kompilacji w programie Visual Studio** w obszarze **przywracanie pakietu**.

   W przypadku projektów typu non-SDK należy najpierw wybrać opcję Zezwól narzędziu **NuGet na pobieranie brakujących pakietów** , aby włączyć opcję automatycznego przywracania.

1. Skompiluj projekt.

   Jeśli co najmniej jeden z pojedynczych pakietów nadal nie jest prawidłowo zainstalowany, **Eksplorator rozwiązań** pokazuje ikonę błędu. Kliknij prawym przyciskiem myszy i wybierz pozycję **Zarządzaj pakietami NuGet**, a następnie użyj **Menedżera pakietów** do odinstalowania i ponownego zainstalowania odpowiednich pakietów. Aby uzyskać więcej informacji, zobacz [Instalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md)

   Jeśli zostanie wyświetlony komunikat o błędzie "ten projekt odwołuje się do pakietów NuGet, których brakuje na tym komputerze" lub "co najmniej jeden pakiet NuGet musi zostać przywrócony, ale nie można go przydzielić," [Włącz automatyczne przywracanie](#enable-and-disable-package-restore-in-visual-studio). W przypadku starszych projektów Zobacz również [Migrowanie do automatycznego przywracania pakietów](#migrate-to-automatic-package-restore-visual-studio). Zobacz również [Rozwiązywanie problemów z przywracaniem pakietów](Package-restore-troubleshooting.md).

### <a name="restore-packages-manually-using-visual-studio"></a>Przywróć pakiety ręcznie przy użyciu programu Visual Studio

1. Włącz przywracanie pakietów, wybierając   >  **Opcje** narzędzia  >  **Menedżer pakietów NuGet**. W obszarze Opcje **przywracania pakietu** wybierz opcję Zezwól narzędziu **NuGet na pobieranie brakujących pakietów**.

1. W **Eksplorator rozwiązań** kliknij prawym przyciskiem myszy rozwiązanie i wybierz polecenie **Przywróć pakiety NuGet**.

   Jeśli co najmniej jeden z pojedynczych pakietów nadal nie jest prawidłowo zainstalowany, **Eksplorator rozwiązań** pokazuje ikonę błędu. Kliknij prawym przyciskiem myszy i wybierz pozycję **Zarządzaj pakietami NuGet**, a następnie użyj **Menedżera pakietów** do odinstalowania i ponownego zainstalowania odpowiednich pakietów. Aby uzyskać więcej informacji, zobacz [Instalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md)

   Jeśli zostanie wyświetlony komunikat o błędzie "ten projekt odwołuje się do pakietów NuGet, których brakuje na tym komputerze" lub "co najmniej jeden pakiet NuGet musi zostać przywrócony, ale nie można go przydzielić," [Włącz automatyczne przywracanie](#enable-and-disable-package-restore-in-visual-studio). W przypadku starszych projektów Zobacz również [Migrowanie do automatycznego przywracania pakietów](#migrate-to-automatic-package-restore-visual-studio). Zobacz również [Rozwiązywanie problemów z przywracaniem pakietów](Package-restore-troubleshooting.md).

### <a name="enable-and-disable-package-restore-in-visual-studio"></a>Włączanie i wyłączanie przywracania pakietów w programie Visual Studio

W programie Visual Studio można sterować przywracaniem pakietów głównie za poorednictwem opcji **Narzędzia**  >    >  **Menedżer pakietów NuGet**:

![Sterowanie przywracaniem pakietu za poorednictwem opcji Menedżera pakietów NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Zezwól narzędziu NuGet na pobieranie brakujących pakietów** kontroluje wszystkie formy przywracania pakietu, zmieniając `packageRestore/enabled` ustawienie w [sekcji PackageRestore](../reference/nuget-config-file.md#packagerestore-section) `NuGet.Config` pliku, w `%AppData%\NuGet\` systemie Windows lub `~/.nuget/NuGet/` na komputerze Mac/Linux. To ustawienie włącza również polecenie **Przywróć pakiety NuGet** w menu kontekstowym rozwiązania w programie Visual Studio.

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
  > Aby globalnie zastąpić to `packageRestore/enabled` ustawienie, należy ustawić zmienną środowiskową **EnableNuGetPackageRestore** z wartością true lub false przed uruchomieniem programu Visual Studio lub rozpoczęciem kompilacji.

- **Automatycznie sprawdzaj brakujące pakiety podczas kompilacji w programie Visual Studio** kontroluje automatyczne przywracanie, zmieniając `packageRestore/automatic` ustawienie w [sekcji packageRestore](../reference/nuget-config-file.md#packagerestore-section) `NuGet.Config` pliku. Gdy ta opcja jest ustawiona na wartość true, uruchomienie kompilacji z programu Visual Studio automatycznie przywraca wszystkie brakujące pakiety. To ustawienie nie ma wpływu na kompilacje wykonywane z wiersza polecenia programu MSBuild.

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

Aby włączyć lub wyłączyć Przywracanie pakietów dla wszystkich użytkowników na komputerze, deweloper lub firma może dodać ustawienia konfiguracji do `nuget.config` pliku globalnego. Globalnie `nuget.config` znajduje się w systemie Windows `%ProgramData%\NuGet\Config` , czasami w ramach określonego `\{IDE}\{Version}\{SKU}\` folderu programu Visual Studio lub na komputerze Mac/Linux pod adresem `~/.local/share` . Indywidualni użytkownicy mogą następnie wybiórczo włączać przywracanie zgodnie z potrzebami na poziomie projektu. Aby uzyskać więcej informacji o tym, jak program NuGet ustala priorytety wielu plików konfiguracji, zobacz [popularne konfiguracje NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

> [!Important]
> Jeśli edytujesz `packageRestore` Ustawienia bezpośrednio w programie `nuget.config` , uruchom ponownie program Visual Studio, aby okno dialogowe **Opcje** pokazywało bieżące wartości.

### <a name="choose-default-package-management-format"></a>Wybierz domyślny format zarządzania pakietami

![Kontrolowanie domyślnego formatu zarządzania pakietami, gdy opcje Menedżera pakietów NuGet](media/Restore-02-PackageFormatOptions.png)

Pakiet NuGet ma dwa formaty, w których projekt może używać pakietów: [`PackageReference`](package-references-in-project-files.md) i [`packages.config`](../reference/packages-config.md) . Domyślny format można wybrać z listy rozwijanej pod nagłówkiem **Zarządzanie pakietami** . Opcja wyświetlania monitu, gdy pierwszy pakiet zostanie zainstalowany w projekcie jest również dostępny.

> [!Note]
> Jeśli projekt nie obsługuje obu formatów zarządzania pakietami, używany format zarządzania pakietami będzie zgodny z projektem i w związku z tym nie może być domyślnym zestawem opcji. Ponadto pakiet NuGet nie monituje o wybór przy pierwszej instalacji pakietu, nawet jeśli opcja została wybrana w oknie Opcje.
>
> Jeśli konsola Menedżera pakietów jest używana do instalowania pierwszego pakietu w projekcie, pakiet NuGet nie wyświetli monitu o wybranie formatu, nawet jeśli opcja jest zaznaczona w oknie Opcje.

## <a name="restore-using-the-dotnet-cli"></a>Przywracanie przy użyciu interfejsu wiersza polecenia dotnet

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]

> [!IMPORTANT]
> Aby dodać brakujące odwołanie do pakietu do pliku projektu, należy użyć polecenia [dotnet Add Package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x), które również uruchamia `restore` polecenie.

## <a name="restore-using-the-nugetexe-cli"></a>Przywracanie przy użyciu interfejsu wiersza polecenia nuget.exe

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

> [!IMPORTANT]
> `restore`Polecenie nie modyfikuje pliku projektu ani *packages.config*. Aby dodać zależność, Dodaj pakiet za pomocą interfejsu użytkownika lub konsoli Menedżera pakietów w programie Visual Studio lub zmodyfikuj *packages.config* a następnie uruchom albo `install` `restore` .

## <a name="restore-using-msbuild"></a>Przywróć przy użyciu programu MSBuild

Użyj polecenia [MSBuild-t:Restore](../reference/msbuild-targets.md#restore-target) , aby przywrócić pakiety wymienione w pliku projektu (zobacz [PackageReference](package-references-in-project-files.md)) i Zaczynając od programu MSBuild 16.5 +, `packages.config` Projects.

 To polecenie jest dostępne tylko w pakiecie NuGet 4. x + i MSBuild 15.1 +, które są dołączone do programu Visual Studio 2017 i nowszych wersji.
Począwszy od programu MSBuild 16.5 +, to polecenie umożliwia również przywracanie `packages.config` projektów opartych na programie przy użyciu programu `-p:RestorePackagesConfig=true` .

1. Otwórz wiersz polecenia dewelopera (w polu **wyszukiwania** wpisz **wiersz polecenia programisty**).

   Zazwyczaj chcesz uruchomić wiersz polecenia dla deweloperów dla programu Visual Studio z menu **Start** , ponieważ zostanie on skonfigurowany ze wszystkimi niezbędnymi ścieżkami dla programu MSBuild.

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
> Program MSBuild ma `-restore` przełącznik, który zostanie uruchomiony `Restore` , załaduje projekt, a następnie skompiluje. Zobacz [przywracanie i kompilowanie za pomocą jednego polecenia MSBuild](../reference/msbuild-targets.md#restoring-and-building-with-one-msbuild-command).

```cmd
# Will restore the project, then build, since build is the default target.
msbuild -restore
```

## <a name="restore-using-azure-pipelines"></a>Przywróć przy użyciu Azure Pipelines

Podczas tworzenia definicji kompilacji w Azure Pipelines należy uwzględnić w definicji zadanie [przywracania](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) NuGet lub [przywracanie](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) oprogramowania .NET Core przed zadaniami kompilacji. Niektóre szablony kompilacji domyślnie zawierają zadanie przywracania.

## <a name="restore-using-azure-devops-server"></a>Przywróć przy użyciu Azure DevOps Server

Azure DevOps Server i TFS 2013 i nowsze automatycznie przywracają pakiety podczas kompilacji, jeśli używasz szablonu kompilacji TFS 2013 lub nowszego. W przypadku wcześniejszych wersji programu TFS można uwzględnić krok kompilacji, aby uruchomić opcję przywracania wiersza polecenia lub opcjonalnie przeprowadzić migrację szablonu kompilacji do nowszej wersji. Aby uzyskać więcej informacji, zobacz [Konfigurowanie przywracania pakietu przy użyciu Team Foundation Build](../consume-packages/team-foundation-build.md).

## <a name="constrain-package-versions-with-restore"></a>Ogranicz wersje pakietów przy użyciu funkcji przywracania

Gdy pakiet NuGet przywraca pakiety za pomocą dowolnej metody, przestrzega ograniczeń określonych w `packages.config` lub pliku projektu:

- W programie `packages.config` można określić zakres wersji we `allowedVersion` właściwości zależności. Aby uzyskać więcej informacji, zobacz [ograniczanie wersji uaktualnienia](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) . Na przykład:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- W pliku projektu można użyć PackageReference, aby określić zakres zależności bezpośrednio. Na przykład:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

We wszystkich przypadkach należy użyć notacji opisanej w artykule [przechowywanie wersji pakietu](../concepts/package-versioning.md).

## <a name="force-restore-from-package-sources"></a>Wymuś przywracanie ze źródeł pakietów

Domyślnie operacje przywracania NuGet używają pakietów z folderów globalne i *pakiety* *pamięci podręcznej http* , które są opisane w temacie [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](managing-the-global-packages-and-cache-folders.md).

Aby uniknąć używania folderu *Global-Packages* , wykonaj jedną z następujących czynności:

- Wyczyść folder przy użyciu `nuget locals global-packages -clear` lub `dotnet nuget locals global-packages --clear` .
- Tymczasowo Zmień lokalizację folderu *Global-Packages* przed operacją przywracania, używając jednej z następujących metod:
  - Ustaw zmienną środowiskową NUGET_PACKAGES na inny folder.
  - Utwórz `NuGet.Config` plik, który ustawia `globalPackagesFolder` (jeśli jest używany PackageReference) lub `repositoryPath` (jeśli jest używany `packages.config` ) do innego folderu. Aby uzyskać więcej informacji, zobacz [Ustawienia konfiguracji](../reference/nuget-config-file.md#config-section).
  - Tylko MSBuild: Określ inny folder z `RestorePackagesPath` właściwością.

Aby uniknąć używania pamięci podręcznej dla źródeł HTTP, wykonaj jedną z następujących czynności:

- Użyj `-NoCache` opcji with `nuget restore` lub `--no-cache` opcji z opcją `dotnet restore` . Te opcje nie wpływają na operacje przywracania za pomocą Menedżera pakietów lub konsoli programu Visual Studio.
- Wyczyść pamięć podręczną przy użyciu `nuget locals http-cache -clear` lub `dotnet nuget locals http-cache --clear` .
- Tymczasowo Ustaw zmienną środowiskową NUGET_HTTP_CACHE_PATH na inny folder.

## <a name="migrate-to-automatic-package-restore-visual-studio"></a>Migrowanie do automatycznego przywracania pakietów (Visual Studio)

W przypadku programu NuGet 2,6 i wcześniejszego przywracanie pakietu programu MSBuild zostało wcześniej obsługiwane, ale nie jest już prawdziwe. (Zwykle jest to możliwe po kliknięciu prawym przyciskiem myszy rozwiązania w programie Visual Studio i wybraniu opcji **Włącz przywracanie pakietu NuGet**). Jeśli projekt używa przestarzałego przywracania pakietu MSBuild, należy przeprowadzić migrację do automatycznego przywracania pakietów.

Projekty używające przywracania pakietów MSBuild-Integrated zwykle zawierają folder *. NuGet* z trzema plikami: *NuGet.config*, *nuget.exe* i *NuGet. targets*. Obecność pliku *NuGet. targets* określa, czy pakiet NuGet będzie nadal używać metody zintegrowanej z użyciem programu MSBuild, więc ten plik musi zostać usunięty podczas migracji.

Aby przeprowadzić migrację do automatycznego przywracania pakietów:

1. Zamknij program Visual Studio.
2. Usuń *. NuGet/nuget.exe* i *. NuGet/NuGet. targets*.
3. Dla każdego pliku projektu, Usuń `<RestorePackages>` element i Usuń odwołania do *NuGet. targets*.

Aby przetestować automatyczne przywracanie pakietów:

1. Usuń folder *Packages* z rozwiązania.
2. Otwórz rozwiązanie w programie Visual Studio i Rozpocznij kompilację.

   Automatyczne przywracanie pakietów powinno pobierać i instalować każdy pakiet zależności bez dodawania ich do kontroli źródła.

## <a name="troubleshooting"></a>Rozwiązywanie problemów

Zobacz [Rozwiązywanie problemów z przywracaniem pakietu](package-restore-troubleshooting.md).
