---
title: Przywracanie pakietu NuGet
description: Przegląd sposobu NuGet przywraca pakietów, od których jest zależna projektu, w tym jak wyłączyć przywracania i ograniczyć wersji.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 6a8a2f1c5ced956f18b623f112756cdd2fab22f5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="package-restore"></a>Przywracanie pakietu

Aby promować czyszczący Środowisko deweloperskie i zmniejszyć rozmiar repozytorium NuGet **przywracania pakietów** instaluje zależności projektu wszystkie wymienione w jednym pliku projektu lub `packages.config`. Visual Studio można przywrócić pakietów automatycznie, podczas tworzenia projektu. `dotnet build` i `dotnet run` przywracania automatycznie przeprowadzić poleceń (.NET Core 2.0 +). Można także przywrócić pakiety w dowolnej chwili za pomocą programu Visual Studio, `nuget restore`, `dotnet restore`i xbuild na Mono.

Przywracanie pakietu upewnia się, że projektu wszystkie zależności są dostępne bez przechowywania tych pakietów w kontroli źródła. Zobacz [pakietów i kontroli źródła](../consume-packages/packages-and-source-control.md) na temat konfigurowania repozytorium, aby wykluczyć pliki binarne pakietu.

## <a name="package-restore-overview"></a>Omówienie przywracania pakietu

Trwa przywracanie pakietów najpierw instaluje bezpośrednich zależności projektu, w razie potrzeby, a następnie instaluje wszystkie zależności tych pakietów w całym na wykresie zależności całego.

Jeśli pakiet nie jest już zainstalowany, NuGet najpierw próbuje pobrać go z [pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md). Jeśli pakiet nie jest w pamięci podręcznej, NuGet następnie próbuje pobrać pakiet ze wszystkich źródeł włączone (zobacz [NuGet Konfigurowanie zachowania](Configuring-NuGet-Behavior.md); źródła są również wyświetlane w **Narzędzia > Opcje > Menedżera pakietów NuGet > Źródła pakietów** listy w programie Visual Studio). Podczas przywracania NuGet ignoruje kolejność źródeł pakietów przy użyciu pakietu z dowolną wskazaną źródło jest najpierw odpowiadać na żądania.

> [!Note]
> NuGet nie wskazuje niepowodzenie przywracania pakietu, dopóki wszystkie źródła zostały sprawdzone. W tym czasie program NuGet zgłasza błąd tylko ostatni źródła na liście. Ten błąd oznacza, że pakiet nie był dostępny na *żadnych* z innych źródeł, mimo że błędy nie są wyświetlane dla każdego z tych źródeł pojedynczo.

Przywracanie pakietu zostanie wywołany w następujący sposób:

- **DotNet CLI**: Użyj [przywracania dotnet](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) polecenia, które przywraca pakiety wymienione w pliku projektu (zobacz [PackageReference](../consume-packages/package-references-in-project-files.md)). .NET Core 2.0 lub nowszy, przywracania odbywają się automatycznie z `dotnet build` i `dotnet run`.

- **Interfejs użytkownika Menedżera pakietów (Visual Studio w systemie Windows)**: pakiety zostaną przywrócone automatycznie podczas tworzenia projektu z szablonu i podczas kompilowania projektu (może ulec opcja opisana w [Włączanie i wyłączanie pakietu przywrócić](#enabling-and-disabling-package-restore)). W NuGet 4.0 + przywracania również odbywa się automatycznie po wprowadzeniu zmian projekt na podstawie zestawu SDK programu .NET Core.

    Aby przywrócić ręcznie, kliknij prawym przyciskiem myszy rozwiązanie w Eksploratorze rozwiązań i wybierz **przywracania pakietów NuGet**. Jeśli co najmniej jeden indywidualne pakiety są nadal nie jest poprawnie zainstalowany (co oznacza, że Eksplorator rozwiązań zawiera ikony błędu), a następnie użyj interfejsu użytkownika Menedżera pakietu na odinstalowanie i ponowne zainstalowanie odpowiednich pakietów. Zobacz [ponowne zainstalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md)

    Jeśli zostanie wyświetlony błąd "ten projekt zawiera odwołania do pakietów NuGet, na tym komputerze brakuje" lub "co najmniej jednego pakietu NuGet konieczne jest przywrócenie, ale nie może być, ponieważ nie udzielono zgody", należy włączyć automatyczne przywracanie zgodnie z instrukcjami w obszarze [Włączanie i wyłączanie Przywracanie pakietu](#enabling-and-disabling-package-restore). Zobacz też [Rozwiązywanie problemów z przywracania pakietu](Package-restore-troubleshooting.md).

- **Interfejs wiersza polecenia NuGet**: Użyj [Przywracanie nuget](../tools/cli-ref-restore.md) polecenia, które przywraca pakiety wymienione w pliku projektu lub w `packages.config`. Można również określić plik rozwiązania.

- **MSBuild**: Użyj [msbuild /t:restore](../reference/msbuild-targets.md#restore-target) poleceń, które przywraca pakietów pakiety wymienione w pliku projektu (tylko PackageReference). Dostępne tylko w NuGet 4.x+ i MSBuild 15.1 +, które są dołączone do programu Visual Studio 2017 r. `nuget restore` i `dotnet restore` dla projektów dotyczy zarówno Użyj tego polecenia.

- **Visual Studio Team Services**: podczas tworzenia definicji kompilacji na Team Services, obejmują [Przywracanie NuGet](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) lub [.NET Core przywrócić](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) zadania w definicji przed żadnego zadania kompilacji. To zadanie jest domyślnie włączone w szablony kompilacji.

- **Team Foundation Server**: TFS 2013 lub nowszym automatycznie przywraca pakietów podczas kompilacji, pod warunkiem, że używasz kompilacji szablonu Team TFS 2013 lub nowszym. Dla wcześniejszych wersji programu TFS mogą obejmować kroku kompilacji, aby wywołać za pomocą jednego z powyższych opcji wiersza polecenia przywracania. Opcjonalnie można przenieść szablonu kompilacji TFS 2013. Aby uzyskać więcej informacji, zobacz [wskazówki dotyczące przywracania pakietu z Team Foundation Build](../consume-packages/team-foundation-build.md).

## <a name="enabling-and-disabling-package-restore"></a>Włączanie i wyłączanie przywracania pakietu

Przywracanie pakietu głównie jest włączany za pomocą **Narzędzia > Opcje > Menedżera pakietów NuGet** w programie Visual Studio:

![Kontrolowanie zachowania przywracania pakietu za pomocą opcji Menedżera pakietów NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Zezwalaj narzędziu NuGet na pobieranie brakujących pakietów**: Określa wszystkich formularzy Przywracanie pakietu, zmieniając `packageRestore/enabled` w `NuGet.Config` plików, jak pokazano poniżej (`%AppData%\NuGet\NuGet.Config` w systemie Windows, `~/.nuget/NuGet/NuGet.Config` na system Mac/Linux). W programie Visual Studio, to ustawienie umożliwia **przywracania pakietów NuGet** polecenia w menu kontekstowym rozwiązania do pracy.

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  `packageRestore/enabled` Ustawienie można zastąpić globalny, ustawiając zmienną środowiskową o nazwie **EnableNuGetPackageRestore** o wartości TRUE lub FALSE przed uruchomieniem programu Visual Studio lub uruchamianie kompilacji.

- **Automatyczne sprawdzenie dostępności dla brakujących pakietów podczas kompilacji w programie Visual Studio**: Określa przywracania automatycznie, zmieniając `packageRestore/automatic` w `NuGet.Config` plików, jak pokazano poniżej (`%AppData%\NuGet\NuGet.Config` w systemie Windows, `~/.nuget/NuGet/NuGet.Config` na system Mac/Linux). Gdy ta opcja jest ustawiona, uruchamianie kompilacji w programie Visual Studio automatycznie przywraca wszystkie brakujące pakiety. Opcja nie ma wpływu na kompilacje uruchomić z wiersza polecenia przy użyciu programu MSBuild.

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

Aby informacje, zobacz [NuGet pliku konfiguracji - sekcji packageRestore](../reference/nuget-config-file.md#packagerestore-section).

W niektórych przypadkach włączyć lub wyłączyć Przywracanie pakietów dla wszystkich użytkowników na komputerze może być deweloperem lub firmy. Aby to zrobić, należy dodać tych samych ustawień powyżej do globalnych znajduje się w pliku konfiguracji w NuGet `%ProgramData%\NuGet\Config` (Windows potencjalnie w obszarze określonej `\{IDE}\{Version}\{SKU}\` folderu dla programu Visual Studio) lub `~/.local/share` (system Mac/Linux). Poszczególnym użytkownikom można selektywnie włączysz przywracania na poziomie projektu. Zobacz [NuGet Konfigurowanie zachowania](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) dokładne szczegółowe informacje na temat sposobu NuGet priorytetem wiele plików konfiguracji.

> [!Important]
> Po zmodyfikowaniu `packageRestore` ustawienia bezpośrednio w `nuget.config`, uruchom ponownie program Visual Studio, opcje — Okno dialogowe zawiera bieżące wartości.

## <a name="constraining-package-versions-with-restore"></a>Ograniczający wersje pakietu z przywracania

Podczas przywracania pakietów przy użyciu dowolnej metody, NuGet honoruje żadnych ograniczeń określone w `packages.config` lub pliku projektu:

- `packages.config`: Określ zakres wersji w `allowedVersion` właściwości zależności. Zobacz [ponowne zainstalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Na przykład:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- Plik projektu (PackageReference): Określ zakres wersji bezpośrednio z numerem wersji tych zależności. Na przykład:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

We wszystkich przypadkach Notacja opisanego w [wersji pakietu](../reference/package-versioning.md).

## <a name="forcing-restore-from-package-sources"></a>Wymuszanie przywracania ze źródeł pakietów

Domyślnie operacje przywracania NuGet korzystają z pakietu z *globalne pakietów* i *http pamięci podręcznej* foldery, które są opisane na [Zarządzanie globalne pakietów i pamięci podręcznej folderów](managing-the-global-packages-and-cache-folders.md).

Aby uniknąć używania *globalne pakiety* folder, wykonaj jedną z następujących czynności:

- Wyczyść folderu przy użyciu `nuget locals global-packages -clear` lub `dotnet nuget locals global-packages --clear`
- Tymczasowo zmienić lokalizację *globalne pakiety* folderu przed wykonaniem operacji przywracania przy użyciu jednej z następujących metod:
  - Ustaw zmienną środowiskową NUGET_PACKAGES do innego folderu.
  - Utwórz `NuGet.Config` pliku, który ustawia `globalPackagesFolder` (jeśli jest używana PackageReference) lub `repositoryPath` (Jeśli za pomocą `packages.config`) do innego folderu (zobacz [ustawienia konfiguracji](../reference/nuget-config-file.md#config-section)
  - Tylko MSBuild: Określ inny folder o `RestorePackagesPath` właściwości.

Aby uniknąć przy użyciu pamięci podręcznej dla źródeł protokołu HTTP, wykonaj jedną z następujących czynności:

- Użyj `-NoCache` opcję z `nuget restore` lub `--no-cache` opcję z `dotnet restore`. Te opcje nie wpływają na operacje przywracania za pomocą programu Visual Studio interfejs użytkownika Menedżera pakietów lub konsoli.
- Usuń zaznaczenie przy użyciu pamięci podręcznej `nuget locals http-cache -clear` lub `dotnet nuget locals http-cache --clear`.
- Tymczasowo ustawić zmiennej środowiskowej NUGET_HTTP_CACHE_PATH do innego folderu.

## <a name="troubleshooting"></a>Rozwiązywanie problemów

Zobacz [Rozwiązywanie problemów z Przywracanie pakietu](package-restore-troubleshooting.md).