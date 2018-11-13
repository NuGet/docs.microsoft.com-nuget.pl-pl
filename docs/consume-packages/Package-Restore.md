---
title: Przywracanie pakietu NuGet
description: Omówienie, jak NuGet przywraca pakietów, od których zależy od projektu, w tym sposób wyłączania przywracania i ograniczenia wersji.
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: da69181aebe3bebcea6acd6e15fde6b77dd33452
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580301"
---
# <a name="package-restore"></a>Przywracanie pakietu

Aby promować bardziej przejrzyste środowisko deweloperskie i zmniejszyć rozmiar repozytorium, NuGet **Przywracanie pakietów** instaluje zależności projektu wszystkie wymienione w jednym pliku projektu lub `packages.config`. Program Visual Studio można przywrócić pakietów automatycznie, podczas kompilowania projektu. `dotnet build` i `dotnet run` przeprowadzić automatycznego przywracania poleceń (.NET Core 2.0 +). W dowolnym momencie za pomocą programu Visual Studio, można przywrócić pakietów `nuget restore`, `dotnet restore`i xbuild na platformy Mono.

Przywracanie pakietu gwarantuje, że projektu wszystkie zależności są dostępne bez przechowywania tych pakietów w kontroli źródła. Zobacz [pakiety i kontrola źródła](../consume-packages/packages-and-source-control.md) dotyczące sposobu konfigurowania repozytorium, aby wykluczyć pliki binarne pakietu.

## <a name="package-restore-overview"></a>Omówienie przywracania pakietu

Trwa przywracanie pakietów najpierw instaluje bezpośredniej zależności projektu, zgodnie z potrzebami, a następnie instaluje wszystkie zależności tych pakietów w całym wykres zależności całego.

Jeśli pakiet nie jest już zainstalowany, NuGet najpierw próbuje pobrać go z [pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md). Jeśli pakiet nie jest w pamięci podręcznej, NuGet następnie próbuje pobrać pakiet ze wszystkich źródeł włączonych (zobacz [zachowania programu NuGet Konfigurowanie](Configuring-NuGet-Behavior.md); źródła są również wyświetlane w **Narzędzia > Opcje > Menedżer pakietów NuGet > Źródła pakietów** listy w programie Visual Studio). Podczas przywracania NuGet ignoruje kolejność źródeł pakietów przy użyciu pakietów z dowolnego źródła najpierw do odpowiadania na żądania.

> [!Note]
> NuGet nie wskazuje nieudanej próbie przywrócenia pakietów, dopóki wszystkie źródła zostały zaewidencjonowane. W tym czasie NuGet zgłasza błąd tylko ostatni źródła na liście. Ten błąd oznacza, że pakiet nie był dostępny na *wszelkie* innych źródeł, mimo że błędów nie są wyświetlane dla każdego z tych źródeł indywidualnie.

Przywracanie pakietu jest wyzwalany w następujący sposób:

- **Wiersz polecenia DotNet**: Użyj [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) polecenia, które pakiety wymienione w pliku projektu (zobacz [PackageReference](../consume-packages/package-references-in-project-files.md)). Za pomocą platformy .NET Core 2.0 i nowszych przywracania odbywa się automatycznie przy użyciu `dotnet build` i `dotnet run`.

- **Interfejs użytkownika Menedżera pakietów (Visual Studio Windows)**: pakiety zostaną przywrócone automatycznie podczas tworzenia projektu z szablonu, a podczas kompilowania projektu (podlegają opcji można znaleźć w [Włączanie i wyłączanie pakietu przywrócić](#enabling-and-disabling-package-restore)). W pakiecie NuGet 4.0 + Przywracanie również odbywa się automatycznie podczas zmiany zostały wprowadzone do projektu na podstawie zestawu .NET Core SDK.

    Aby przywrócić ręcznie, kliknij prawym przyciskiem myszy rozwiązanie w Eksploratorze rozwiązań i wybierz **Przywróć pakiety NuGet**. Jeśli co najmniej jeden z indywidualnych pakietów są nadal nie jest poprawnie zainstalowany (co oznacza, że Eksplorator rozwiązań pokazuje ikona błędu), a następnie użyj interfejsu użytkownika Menedżera pakietów, aby odinstalować i ponownie zainstalować pakiety, których to dotyczy. Zobacz [ponowne zainstalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md)

    Jeśli zostanie wyświetlony błąd "ten projekt odwołuje się do pakietów NuGet, których brakuje na tym komputerze" lub "co najmniej jednego pakietu NuGet muszą zostać przywrócone, ale nie może być, ponieważ nie udzielono zgody", włączyć automatycznego przywracania, postępując zgodnie z instrukcjami zawartymi w sekcji [Włączanie i wyłączanie Przywracanie pakietu](#enabling-and-disabling-package-restore). Zobacz też [Rozwiązywanie problemów z przywracania pakietu](Package-restore-troubleshooting.md).

- **Interfejs wiersza polecenia NuGet**: Użyj [Przywracanie pakietów nuget](../tools/cli-ref-restore.md) polecenia, które pakiety wymienione w pliku projektu lub w `packages.config`. Można również określić plik rozwiązania.

- **Program MSBuild**: Użyj [msbuild /t:restore](../reference/msbuild-targets.md#restore-target) polecenia, które przywraca pakietów pakiety wymienione w pliku projektu (tylko PackageReference). Dostępne tylko w NuGet 4.x+ i MSBuild 15.1 +, które są dołączone do programu Visual Studio 2017. `nuget restore` i `dotnet restore` dla projektów dotyczy zarówno Użyj tego polecenia.

- **Visual Studio Team Services**: podczas tworzenia definicji kompilacji w usłudze Team Services, obejmują [Przywracanie pakietów NuGet](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) lub [przywracania programu .NET Core](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) zadania w definicji przed dowolnego zadania kompilacji. To zadanie jest domyślnie włączone w wiele szablonów kompilacji.

- **Team Foundation Server**: TFS 2013 lub nowszym automatycznie przywraca pakietów podczas kompilacji, pod warunkiem, że używasz zespołu tworzenie szablonu dla TFS 2013 lub nowszym. Dla wcześniejszych wersji programu TFS można dołączyć kroku kompilacji do wywoływania jednej z powyższych opcji wiersza polecenia restore. Opcjonalnie można migrować szablonu kompilacji do programu TFS 2013. Aby uzyskać więcej informacji, zobacz [wskazówki dotyczące przywracania pakietów w programie Team Foundation Build](../consume-packages/team-foundation-build.md).

## <a name="enabling-and-disabling-package-restore"></a>Włączanie i wyłączanie Przywracanie pakietu

Przywracanie pakietu przede wszystkim jest włączana za pomocą **Narzędzia > Opcje > Menedżer pakietów NuGet** w programie Visual Studio:

![Kontrolowanie zachowania przywracania pakietów za pomocą opcji Menedżer pakietów NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Zezwalaj na rozszerzenie NuGet, aby pobrać brakujące pakiety**: kontroluje wszystkie formularze Przywracanie pakietu, zmieniając `packageRestore/enabled` w `NuGet.Config` pliku, jak pokazano poniżej (`%AppData%\NuGet\NuGet.Config` na Windows, `~/.nuget/NuGet/NuGet.Config` w systemie Mac/Linux). W programie Visual Studio, to ustawienie umożliwia **Przywróć pakiety NuGet** polecenia w menu kontekstowym rozwiązania do pracy.

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```

> [!Note]
>  `packageRestore/enabled` Ustawienie można przesłonić globalny, ustawiając zmienną środowiskową o nazwie **EnableNuGetPackageRestore** o wartości TRUE lub FALSE przed uruchomieniem programu Visual Studio lub uruchamianie kompilacji.

- **Automatyczne sprawdzenie dostępności dla brakujących pakietów podczas kompilacji w programie Visual Studio**: Określa automatycznego przywracania, zmieniając `packageRestore/automatic` w `NuGet.Config` pliku, jak pokazano poniżej (`%AppData%\NuGet\NuGet.Config` na Windows, `~/.nuget/NuGet/NuGet.Config` w systemie Mac/Linux). Gdy ta opcja jest ustawiona, uruchamianie kompilacji w programie Visual Studio automatycznie przywraca wszystkie brakujące pakiety. Opcja nie wpływa na kompilacje uruchamiane z wiersza polecenia, korzystając z programu MSBuild.

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

Aby informacje, zobacz [NuGet pliku config - sekcji packageRestore](../reference/nuget-config-file.md#packagerestore-section).

W niektórych przypadkach włączyć lub wyłączyć przywracania pakietu dla wszystkich użytkowników na komputerze może być dewelopera lub firmy. Aby to zrobić, Dodaj te same ustawienia powyżej do globalnych znajduje się w pliku konfiguracji w NuGet `%ProgramData%\NuGet\Config` (Windows potencjalnie w ramach określonego `\{IDE}\{Version}\{SKU}\` folderu dla programu Visual Studio) lub `~/.local/share` (Mac/Linux). Poszczególnych użytkowników można selektywnie włączysz przywracania na poziomie projektu. Zobacz [zachowania programu NuGet Konfigurowanie](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) dokładnie szczegółowe informacje na temat sposobu NuGet umożliwia określenie wielu plików konfiguracji.

> [!Important]
> Jeśli edytujesz `packageRestore` ustawienia bezpośrednio w `nuget.config`, uruchom ponownie program Visual Studio, okno dialogowe Opcje Pokazuje bieżące wartości.

## <a name="constraining-package-versions-with-restore"></a>Ograniczający wersji pakietu, dzięki funkcji przywracania

Podczas przywracania pakietów przy użyciu dowolnej metody, NuGet honoruje wszelkie ograniczenia określone w `packages.config` lub pliku projektu:

- `packages.config`: Określ zakres wersji w `allowedVersion` właściwość zależności. Zobacz [ponowne zainstalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Na przykład:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- Plik projektu (PackageReference): Określ zakres wersji bezpośrednio z numerem wersji zależności. Na przykład:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

We wszystkich przypadkach Notacja opisanego w [przechowywanie wersji pakietów](../reference/package-versioning.md).

## <a name="forcing-restore-from-package-sources"></a>Wymuszanie przywracanie ze źródła pakietu

Domyślnie operacje przywracania NuGet używania pakietów *globalnymi pakietami* i *pamięci podręcznej http* foldery, które są opisane na [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](managing-the-global-packages-and-cache-folders.md).

Aby uniknąć używania *globalnymi pakietami* folder, wykonaj jedną z następujących czynności:

- Wyczyść folderze przy użyciu `nuget locals global-packages -clear` lub `dotnet nuget locals global-packages --clear`
- Tymczasowo zmienić lokalizację *globalnymi pakietami* folder przed rozpoczęciem operacji przywracania przy użyciu jednej z następujących metod:
  - Ustaw zmienną środowiskową NUGET_PACKAGES do innego folderu.
  - Tworzenie `NuGet.Config` pliku, który ustawia `globalPackagesFolder` (w przypadku korzystania z funkcji PackageReference) lub `repositoryPath` (Jeśli za pomocą `packages.config`) do innego folderu (zobacz [ustawień konfiguracji](../reference/nuget-config-file.md#config-section)
  - Tylko MSBuild: określić inny folder z `RestorePackagesPath` właściwości.

Aby uniknąć, za pomocą pamięci podręcznej dla źródła HTTP, wykonaj jedną z następujących czynności:

- Użyj `-NoCache` z opcją `nuget restore` lub `--no-cache` z opcją `dotnet restore`. Te opcje nie wpływają na operacje przywracania za pomocą programu Visual Studio interfejs użytkownika Menedżera pakietów lub konsoli.
- Wyczyść pamięć podręczną za pomocą `nuget locals http-cache -clear` lub `dotnet nuget locals http-cache --clear`.
- Tymczasowe ustawienie zmiennej środowiskowej NUGET_HTTP_CACHE_PATH do innego folderu.

## <a name="troubleshooting"></a>Rozwiązywanie problemów

Zobacz [Rozwiązywanie problemów z Przywracanie pakietu](package-restore-troubleshooting.md).
