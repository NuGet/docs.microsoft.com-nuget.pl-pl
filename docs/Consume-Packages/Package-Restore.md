---
title: Przywracanie pakietu NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Przegląd sposobu NuGet przywraca pakietów, od których jest zależna projektu, w tym jak wyłączyć przywracania i ograniczyć wersji."
keywords: "Przywracanie pakietu NuGet, instalacja pakietu NuGet, instalowanie pakietu Przywracanie pakietów, wersje zależności, wyłączenie automatycznego przywracania ograniczający wersji pakietu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 761ef86a70e0a681449dc9fe86d6a52ac2b19bb1
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/15/2018
---
# <a name="package-restore"></a>Przywracanie pakietu

Aby promować czyszczący Środowisko deweloperskie i zmniejszyć rozmiar repozytorium NuGet **przywracania pakietów** instaluje pakiety wszystkich przywoływanych przed projektu jest wbudowana. Ta funkcja powszechnie używane&mdash;dostępne w Visual Studio .NET Core 2.0 + i xbuild na Mono&mdash;zapewnia, że wszystkie zależności są dostępne w projekcie bez konieczności pakiety mają być przechowywane w kontroli źródła (zobacz [ Pakiety i kontroli źródła](../consume-packages/packages-and-source-control.md) na temat konfigurowania repozytorium, aby wykluczyć pliki binarne pakietu). Można też ręcznie przywrócić pakiety w dowolnym momencie.

Aby uzyskać dodatkowe szczegóły dotyczące przywracania pakietu na serwerach kompilacji, zobacz [Przywracanie pakietu z TFBuild](../consume-packages/team-foundation-build.md).

## <a name="package-restore-overview"></a>Omówienie przywracania pakietu

Najpierw Przywracanie pakietów instaluje bezpośrednich zależności projektu, zgodnie z potrzebami, następnie zainstalować wszelkie zależności tych pakietów w całym na wykresie zależności całego.

Jeśli pakiet nie jest już zainstalowany, NuGet najpierw próbuje pobrać go z [pamięci podręcznej](../consume-packages/managing-the-nuget-cache.md). Jeśli pakiet nie jest w pamięci podręcznej, NuGet podejmuje próbę pobrania (i pamięci podręcznej) pakiet ze wszystkich włączonych źródeł (zobacz [NuGet Konfigurowanie zachowania](Configuring-NuGet-Behavior.md)); źródła są również wyświetlane w **Narzędzia > Opcje > Pakiet NuGet Menedżer > źródła pakietów** listy w programie Visual Studio). NuGet ignoruje kolejność źródeł pakietów przy użyciu pakietu z dowolną wskazaną źródło jest najpierw odpowiadać na żądania.

> [!Note]
> NuGet nie wskazuje niepowodzenie przywracania pakietu, dopóki wszystkie źródła zostały sprawdzone. W tym czasie NuGet zgłasza błąd na liście tylko ostatni źródła. Ten błąd oznacza, że pakiet nie był dostępny na *żadnych* z innych źródeł, mimo że błędy nie są wyświetlane dla każdego z tych źródeł pojedynczo.

Przywracanie pakietu zostanie wywołany w następujący sposób:

- **DotNet CLI**: Użyj [przywracania dotnet](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) polecenia, które przywraca pakiety wymienione w pliku projektu (zobacz [PackageReference](../consume-packages/package-references-in-project-files.md)). .NET Core 2.0 lub nowszy, przywracania odbywają się automatycznie z `dotnet build` i `dotnet run`.

- **Interfejs użytkownika Menedżera pakietów (Visual Studio w systemie Windows)**: pakiety zostaną przywrócone automatycznie podczas tworzenia projektu z szablonu i podczas kompilowania projektu (może ulec opcja opisana w [Włączanie i wyłączanie pakietu przywrócić](#enabling-and-disabling-package-restore)). W NuGet 4.0 + przywracania również odbywa się automatycznie po wprowadzeniu zmian projekt na podstawie zestawu SDK programu .NET Core.

    Aby przywrócić ręcznie, kliknij prawym przyciskiem myszy rozwiązanie w Eksploratorze rozwiązań i wybierz **przywracania pakietów NuGet**. Jeśli co najmniej jeden indywidualne pakiety są nadal nie jest poprawnie zainstalowany (co oznacza, że Eksplorator rozwiązań zawiera ikony błędu), a następnie użyj interfejsu użytkownika Menedżera pakietu na odinstalowanie i ponowne zainstalowanie odpowiednich pakietów. Zobacz [ponowne zainstalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md)

    Jeśli zostanie wyświetlony błąd "ten projekt zawiera odwołania do pakietów NuGet, na tym komputerze brakuje" lub "co najmniej jednego pakietu NuGet konieczne jest przywrócenie, ale nie może być, ponieważ nie udzielono zgody", należy włączyć automatyczne przywracanie zgodnie z instrukcjami w obszarze [Włączanie i wyłączanie Przywracanie pakietu](#enabling-and-disabling-package-restore).

- **Interfejs wiersza polecenia NuGet**: Użyj [Przywracanie nuget](../tools/cli-ref-restore.md) polecenia, które przywraca pakiety wymienione w pliku projektu (zobacz [PackageReference](../consume-packages/package-references-in-project-files.md)) lub w [packages.config](../reference/packages-config.md) plik. Można również określić plik rozwiązania.

- **MSBuild**: Użyj [msbuild /t:restore](../reference/msbuild-targets.md#restore-target) poleceń, które przywraca pakietów pakiety wymienione w pliku projektu (zobacz [PackageReference](../consume-packages/package-references-in-project-files.md)). Dostępne tylko w NuGet 4.x+ i MSBuild 15.1 +, które są dołączone do programu Visual Studio 2017 r. `nuget restore` i `dotnet restore` dla projektów dotyczy zarówno Użyj tego polecenia.

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

W niektórych przypadkach włączyć lub wyłączyć Przywracanie pakietów dla wszystkich użytkowników na komputerze może być deweloperem lub firmy. Jest to realizowane przez dodanie tych samych ustawień powyżej do globalnych znajduje się w pliku konfiguracji w NuGet `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`. Poszczególnym użytkownikom można selektywnie włączysz przywracania na poziomie projektu. Zobacz [NuGet Konfigurowanie zachowania](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) dokładne szczegółowe informacje na temat sposobu NuGet priorytetem wiele plików konfiguracji.

## <a name="constraining-package-versions-with-restore"></a>Ograniczający wersje pakietu z przywracania

Podczas przywracania pakietów przy użyciu dowolnej metody, NuGet honoruje żadnych ograniczeń określone w `packages.config` lub pliku projektu:

- `packages.config`: Określ zakres wersji w `allowedVersion` właściwości zależności. Zobacz [ponowne zainstalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Na przykład:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- PackageReference: Określ zakres wersji bezpośrednio z numerem wersji tych zależności. Na przykład:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

We wszystkich przypadkach Notacja opisanego w [wersji pakietu](../reference/package-versioning.md).

## <a name="troubleshooting"></a>Rozwiązywanie problemów

Zobacz [Rozwiązywanie problemów z Przywracanie pakietu](package-restore-troubleshooting.md).