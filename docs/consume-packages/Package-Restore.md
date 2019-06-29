---
title: Przywracanie pakietu NuGet
description: Omówienie sposobu przywracania NuGet pakietów projektu zależy od, np. Wyłącz przywracania i ograniczenia wersji.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 3b64c035886818496339fe1bdd8f9abce060278a
ms.sourcegitcommit: b9a134a6e10d7d8502613f389f7d5f9b9e206ec8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467795"
---
# <a name="package-restore"></a>Przywracanie pakietu

Aby promować bardziej przejrzyste środowisko deweloperskie i zmniejszyć rozmiar repozytorium, NuGet **Przywracanie pakietów** instaluje wszystkie zależności projektu, wymienione w pliku projektu lub `packages.config`. .NET Core 2.0 + `dotnet build` i `dotnet run` poleceń wykonaj Przywracanie pakietu automatyczne. Program Visual Studio można przywrócić pakietów automatycznie podczas tworzenia projektu i w dowolnym momencie za pomocą programu Visual Studio, można przywrócić pakietów `nuget restore`, `dotnet restore`i xbuild na platformy Mono.

Przywracanie pakietu gwarantuje, że projektu wszystkie zależności są dostępne, bez konieczności przechowywania ich w kontroli źródła. Aby skonfigurować repozytorium kontroli źródła, aby wykluczyć pliki binarne pakietu, zobacz [pakiety i kontrola źródła](../consume-packages/packages-and-source-control.md). 

## <a name="package-restore-overview"></a>Omówienie przywracania pakietu

Przywracanie pakietu najpierw instaluje bezpośrednich zależności projektu, zgodnie z potrzebami, a następnie instaluje wszystkie zależności tych pakietów w całym wykres zależności całego.

Jeśli pakiet nie jest już zainstalowany, NuGet najpierw próbuje pobrać go z [pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md). Jeśli pakiet jest w pamięci podręcznej, NuGet próbuje pobrać pakiet ze wszystkich źródeł włączonych na liście u **narzędzia** > **opcje** > **Menedżera pakietów NuGet**   >  **Pakietu źródeł** w programie Visual Studio. Podczas przywracania NuGet ignoruje kolejność źródeł pakietów i używa pakietów z dowolnego źródła najpierw do odpowiadania na żądania. Aby uzyskać więcej informacji na temat zachowania NuGet, zobacz [NuGet typowe konfiguracje](Configuring-NuGet-Behavior.md). 

> [!Note]
> NuGet nie oznacza nieudanej próbie przywrócenia pakietów, dopóki wszystkie źródła zostały zaewidencjonowane. W tym czasie NuGet zgłasza błąd tylko ostatni źródła na liście. Ten błąd oznacza, że pakiet nie był dostępny na *wszelkie* innych źródeł, mimo że błędów nie są wyświetlane dla każdego z tych źródeł indywidualnie.

Przywracanie pakietów można wyzwalać w dowolnym z następujących sposobów:

- **Wiersz polecenia DotNet**: Użyj [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) polecenie, aby przywrócić pakiety wymienione w pliku projektu za pomocą [PackageReference](../consume-packages/package-references-in-project-files.md). Za pomocą platformy .NET Core 2.0 i nowszych przywracania odbywa się automatycznie przy użyciu `dotnet build` i `dotnet run` poleceń.  

- **Menedżer pakietów**: W programie Visual Studio, Windows, przywracanie pakietów odbywa się automatycznie po Tworzenie projektu z szablonu lub kompilowania projektu, z zastrzeżeniem opcje w [włączać i wyłączać przywracanie pakietu](#enable-and-disable-package-restore). W pakiecie NuGet 4.0 + Przywracanie również odbywa się automatycznie po wprowadzeniu zmian do projektu na podstawie zestawu .NET Core SDK.

    Do ręcznego przywrócenia pakietów, kliknij prawym przyciskiem myszy rozwiązanie w **Eksploratora rozwiązań** i wybierz **Przywróć pakiety NuGet**. Jeśli co najmniej jeden z indywidualnych pakietów nadal nie są zainstalowane prawidłowo, **Eksploratora rozwiązań** znajduje się ikona błąd. Kliknij prawym przyciskiem myszy i wybierz **Zarządzaj pakietami NuGet**i użyj **Menedżera pakietów** odinstalować i ponownie zainstalować pakiety, których to dotyczy. Aby uzyskać więcej informacji, zobacz [pakiety ponownej instalacji i aktualizacji](../consume-packages/reinstalling-and-updating-packages.md)

    Jeśli zostanie wyświetlony błąd "ten projekt odwołuje się do pakietów NuGet, których brakuje na tym komputerze" lub "co najmniej jednego pakietu NuGet muszą zostać przywrócone, ale nie może być, ponieważ nie udzielono zgody," [włączyć automatycznego przywracania](#enable-and-disable-package-restore). Zobacz też [Przywracanie pakietów Rozwiązywanie problemów z](Package-restore-troubleshooting.md).

- **Interfejs wiersza polecenia nuget.exe**: Użyj [Przywracanie pakietów nuget](../tools/cli-ref-restore.md) polecenie, aby przywrócić pakiety wymienione w pliku projektu lub rozwiązania lub w `packages.config`. 

- **Program MSBuild**: Użyj [msbuild - t: Przywracanie](../reference/msbuild-targets.md#restore-target) polecenie, aby przywrócić pakiety wymienione w pliku projektu za pomocą funkcji PackageReference. To polecenie jest dostępne tylko w NuGet 4.x+ i MSBuild 15.1 +, które są dołączone do programu Visual Studio 2017 i nowsze wersje. Zarówno `nuget restore` i `dotnet restore` to polecenie dotyczy projektów.

- **Potoki usługi Azure**: Podczas tworzenia definicji kompilacji w potokach platformy Azure, obejmują NuGet [przywrócić](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) lub .NET Core [przywrócić](/azure/devops/pipelines/tasks/build/dotnet-core#restore-nuget-packages) zadania w definicji przed dowolnego zadania kompilacji. Domyślnie kilka szablonów kompilacji zawierają zadania przywracania.

- **Azure DevOps Server**: Azure DevOps Server i TFS 2013 lub nowszym automatycznie przywrócić, pakietów podczas kompilacji, jeśli używasz programu TFS 2013 lub nowszej kompilacji zespołowej szablonu. W przypadku starszych wersji programu TFS obejmuje kroku kompilacji do uruchamiania z opcją wiersza polecenia restore lub opcjonalnie migracji szablonu kompilacji do nowszej wersji. Aby uzyskać więcej informacji, zobacz [Konfigurowanie przywracania pakietów w programie Team Foundation Build](../consume-packages/team-foundation-build.md).

## <a name="enable-and-disable-package-restore"></a>Włączanie i wyłączanie Przywracanie pakietu

W programie Visual Studio, możesz kontrolować, głównie za pomocą Przywracanie pakietów **narzędzia** > **opcje** > **Menedżera pakietów NuGet**:

![Przywracanie pakietów sterowania za pomocą opcji Menedżer pakietów NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Zezwalaj na rozszerzenie NuGet, aby pobrać brakujące pakiety** kontroluje wszystkie formularze Przywracanie pakietu, zmieniając `packageRestore/enabled` w [sekcji packageRestore](../reference/nuget-config-file.md#packagerestore-section) z `NuGet.Config` pliku na `%AppData%\NuGet\` na Windows, lub `~/.nuget/NuGet/` w systemie Mac/Linux. To ustawienie umożliwia również **Przywróć pakiety NuGet** polecenia w menu kontekstowym rozwiązania w programie Visual Studio.

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
  > Aby zastąpić globalnie `packageRestore/enabled` ustawienie, ustaw zmienną środowiskową **EnableNuGetPackageRestore** o wartości True lub False przed uruchomieniem programu Visual Studio lub uruchamianie kompilacji.

- **Automatyczne sprawdzenie dostępności dla brakujących pakietów podczas kompilacji w programie Visual Studio** kontroluje automatycznego przywracania, zmieniając `packageRestore/automatic` w [sekcji packageRestore](../reference/nuget-config-file.md#packagerestore-section) z `NuGet.Config` pliku. Gdy ta opcja jest ustawiona na wartość True, uruchamianie kompilacji w programie Visual Studio automatycznie przywraca wszystkie brakujące pakiety. To ustawienie nie wpływa na kompilacje uruchamiane z wiersza polecenia programu MSBuild.

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

Aby włączyć lub wyłączyć Przywracanie pakietów dla wszystkich użytkowników na komputerze, deweloperów i firmy można dodać ustawień konfiguracji do globalnego `nuget.config` pliku. Globalna `nuget.config` znajduje się w Windows na `%ProgramData%\NuGet\Config`, czasami w ramach określonego `\{IDE}\{Version}\{SKU}\` folder programu Visual Studio lub Mac/Linux w `~/.local/share`. Poszczególnych użytkowników można selektywnie włączysz przywracania na poziomie projektu. Aby uzyskać szczegółowe informacje na temat sposobu NuGet umożliwia określenie wielu plików konfiguracji, zobacz [NuGet typowe konfiguracje](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

> [!Important]
> Jeśli edytujesz `packageRestore` ustawienia bezpośrednio w `nuget.config`, uruchom ponownie program Visual Studio, tak, aby **opcje** bieżące wartości wyświetlane okno dialogowe.

## <a name="constrain-package-versions-with-restore"></a>Ograniczenie wersji pakietu, dzięki funkcji przywracania

Gdy NuGet przywraca pakietów przy użyciu dowolnej metody, będzie używana wszelkie ograniczenia określone w `packages.config` lub pliku projektu:

- W `packages.config`, można określić zakres wersji w `allowedVersion` właściwość zależności. Zobacz [wersji uaktualnienie Zachowaj](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) Aby uzyskać więcej informacji. Na przykład:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- W pliku projektu można użyć PackageReference do określania zakresu zależności bezpośrednio. Na przykład:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

We wszystkich przypadkach Notacja opisanego w [przechowywanie wersji pakietów](../reference/package-versioning.md).

## <a name="force-restore-from-package-sources"></a>Wymusić przywracanie ze źródła pakietu

Domyślnie operacje przywracania NuGet używania pakietów *globalnymi pakietami* i *pamięci podręcznej http* foldery, które są opisane w [Zarządzanie globalnymi pakietami i folderamiwpamięcipodręcznej](managing-the-global-packages-and-cache-folders.md).

Aby uniknąć używania *globalnymi pakietami* folder, wykonaj jedną z następujących czynności:

- Wyczyść folderze przy użyciu `nuget locals global-packages -clear` lub `dotnet nuget locals global-packages --clear`.
- Tymczasowo zmienić lokalizację *globalnymi pakietami* folder przed rozpoczęciem operacji przywracania, przy użyciu jednej z następujących metod:
  - Ustaw zmienną środowiskową NUGET_PACKAGES do innego folderu.
  - Tworzenie `NuGet.Config` pliku, który ustawia `globalPackagesFolder` (w przypadku korzystania z funkcji PackageReference) lub `repositoryPath` (Jeśli za pomocą `packages.config`) do innego folderu. Aby uzyskać więcej informacji, zobacz [ustawienia konfiguracji](../reference/nuget-config-file.md#config-section).
  - Program MSBuild tylko: Określ inny folder z `RestorePackagesPath` właściwości.

Aby uniknąć, za pomocą pamięci podręcznej dla źródła HTTP, wykonaj jedną z następujących czynności:

- Użyj `-NoCache` z opcją `nuget restore`, lub `--no-cache` z opcją `dotnet restore`. Te opcje nie wpływa na operacje przywracania Menedżera pakietów za pomocą Visual Studio lub konsoli.
- Wyczyść pamięć podręczną za pomocą `nuget locals http-cache -clear` lub `dotnet nuget locals http-cache --clear`.
- Tymczasowo ustawić zmienną środowiskową NUGET_HTTP_CACHE_PATH do innego folderu.

## <a name="troubleshooting"></a>Rozwiązywanie problemów

Zobacz [Rozwiązywanie problemów z Przywracanie pakietu](package-restore-troubleshooting.md).
