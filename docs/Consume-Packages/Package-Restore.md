---
title: Przywracanie pakietu NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Opis sposobu NuGet przywraca pakietów, od których jest zależna projektu, w tym jak wyłączyć przywracania i ograniczyć wersji."
keywords: "Przywracanie pakietu NuGet, instalacja pakietu NuGet, instalowanie pakietu Przywracanie pakietów, wersje zależności, wyłączenie automatycznego przywracania ograniczający wersji pakietu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c2567f45b6bb36cdd94c4ce6f1418cb1c7ceac5e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="package-restore"></a>Przywracanie pakietu

Aby promować czyszczący Środowisko deweloperskie i zmniejszyć rozmiar repozytorium NuGet **przywracania pakietów** instaluje pakiety wszystkich przywoływanych przed projektu jest wbudowana. Ta funkcja powszechnie używane gwarantuje, że wszystkie zależności są dostępne w projekcie bez konieczności pakiety mają być przechowywane w kontroli źródła (zobacz [pakietów i kontroli źródła](../consume-packages/packages-and-source-control.md) na temat konfigurowania repozytorium, aby wykluczyć pliki binarne pakietu).

W tym temacie:
- [Przywróć krótki przewodnik do pakietu](#quick-guide-to-package-restore)
- [Omówienie przywracania pakietu](#package-restore-overview)
- [Włączanie i wyłączanie przywracania pakietu](#enabling-and-disabling-package-restore)
- [Ograniczający wersje pakietu z przywracania](#constraining-package-versions-with-restore)
- [Przywracanie wiersza polecenia](#command-line-restore), wszystkie wersje programu NuGet
- [Automatyczne przywracania w programie Visual Studio](#automatic-restore-in-visual-studio)dla NuGet 2.7 i później.
- [Zintegrowane MSBuild przywracania w programie Visual Studio](#msbuild-integrated-restore)dla NuGet 2.6 i starszych.
- [Przywracanie pakietu z Team Foundation Build](#package-restore-with-team-foundation-build)

Przywróć zachowanie zależy od wersji; Aby sprawdzić wersję programu NuGet, wystarczy uruchomić `nuget.exe` na wiersz polecenia i znajduje się w pierwszym wierszu danych wyjściowych.

Aby uzyskać dodatkowe szczegóły dotyczące przywracania pakietu na serwerach kompilacji, zobacz [Przywracanie pakietu z TFBuild](../consume-packages/team-foundation-build.md).

> [!Note]
> Projekty skonfigurowane dla pakietu przywrócić również współpracują z xbuild na Mono.

## <a name="quick-guide-to-package-restore"></a>Przywróć krótki przewodnik do pakietu

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> Jeśli zostanie wyświetlony błąd "ten projekt zawiera odwołania do pakietów NuGet, na tym komputerze brakuje" lub "co najmniej jednego pakietu NuGet konieczne jest przywrócenie, ale nie może być, ponieważ nie udzielono zgody", należy włączyć automatyczne przywracanie zgodnie z instrukcjami w obszarze [Włączanie i wyłączanie Przywracanie pakietu](#enabling-and-disabling-package-restore).

## <a name="package-restore-overview"></a>Omówienie przywracania pakietu

Po pierwsze odwołania do pakietu są obsługiwane w jednym z następujących formatów zarządzania pakiet, w zależności od typu projektu i wersja narzędzia NuGet. (Uwaga NuGet 4 i MSBuild 15.1 są instalowane z programu Visual Studio 2017 r.)

| Metoda | Wersja narzędzia NuGet | Opis | 
| --- | --- | --- |
| `packages.config` | 2.x + | Wyświetla listę pełny zestaw głębokie zależności. Dodane do pakietów `packages.config` również musi zostać dodany do pliku projektu i cele i właściwości, również muszą zostać dodane do pliku projektu. Jest to metoda linii bazowej dla wszystkich wersji programu NuGet, ale działa wolniej w porównaniu z innymi opcjami. (Zobacz [schematu pliku packages.config](../schema/packages-config.md).) | 
| `project.json` | 3.x + | Używany domyślnie tylko z projektami platformy uniwersalnej systemu Windows, ale można przekonwertować projektów z `packages.config`. `project.json`zawiera tylko zależności najwyższego poziomu. Odwołania do obiektów docelowych i właściwości są dodawane dynamicznie do projektu podczas kompilacji, co zapewnia lepszą wydajność w porównaniu z `packages.config`. (Zobacz [schematu project.json](../schema/project-json.md).)|
| PackageReference | 4.x + | Zawiera listę zależności bezpośrednio w pliku projektu w `<PackageReference>` węzła, alongside `<Reference>` i `<ProjectReference>`. Działa podobnie do `project.json`; zobacz [pakietu odwołań w plikach projektu](../Consume-Packages/Package-References-in-Project-Files.md). |

Po drugie rozpoczęciem przywracania przy użyciu listy odwołania na różne sposoby:

W wierszu polecenia lub [Konsola Menedżera pakietów](../tools/Package-Manager-Console.md):

| Polecenie | Scenariusze zastosowania |
| --- | --- | 
| `nuget restore` | Wszystkie wersje programu NuGet i wszystkie typy referencyjne. Zobacz [wiersza polecenia przywracania](#command-line-restore) poniżej. | 
| `dotnet restore` | Taki sam jak `nuget restore` dla projektów .NET Core. Zobacz [przywracania dotnet](https://docs.microsoft.com/dotnet/articles/core/tools/dotnet-restore). |
| `msbuild /t:restore` | Nuget 4.x+ i MSBuild 15.1 + z [pakietu odwołań w plikach projektu](../Consume-Packages/Package-References-in-Project-Files.md) tylko. `nuget restore`i `dotnet restore` dla projektów dotyczy zarówno Użyj tego polecenia. Zobacz [pakiet NuGet i przywracania jako MSBuild elementy docelowe przywracaniem docelowej](../schema/msbuild-targets.md#restore-target).|

Visual Studio, sama przywraca również pakiety w różnym czasie:

| Typ | Podczas przywracania sytuacji |
| --- | --- |
| Przywracanie szablonu | Podczas tworzenia nowego projektu jako niektóre szablony są zależne od pakietów zewnętrznych. |
| Tworzenie przywracania | W pierwszym kroku kompilacji. |
| Przywrócenie rozwiązania | Gdy użytkownik kliknie prawym przyciskiem myszy rozwiązanie i wybiera **przywracania pakietów NuGet**. |
| Przywracanie w przypadku zmiany projektu | *(NuGet tylko 4.x)*  Projektu podczas .NET Core SDK jest używany, łącznie z projektu zmiany stanu. |

## <a name="enabling-and-disabling-package-restore"></a>Włączanie i wyłączanie przywracania pakietu

Przywracanie pakietu głównie jest włączany za pomocą **Narzędzia > Opcje > Menedżera pakietów NuGet** w programie Visual Studio:

![Kontrolowanie zachowania przywracania pakietu za pomocą opcji Menedżera pakietów NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Zezwalaj narzędziu NuGet na pobieranie brakujących pakietów**: Określa wszystkich formularzy Przywracanie pakietu, zmieniając `packageRestore/enabled` w `%AppData%\NuGet\NuGet.Config` plików, jak pokazano poniżej.

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
    

- **Automatyczne sprawdzenie dostępności dla brakujących pakietów podczas kompilacji w programie Visual Studio**: Określa przywracania automatycznie NuGet 2.7 i później, zmieniając `packageRestore/automatic` w `%AppData%\NuGet\NuGet.Config` plików, jak pokazano poniżej.
            
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

Aby informacje, zobacz [NuGet pliku konfiguracji - sekcji packageRestore](../Schema/nuget-config-file.md#packagerestore-section).

W niektórych przypadkach włączyć lub wyłączyć Przywracanie pakietu na komputerze, domyślnie dla wszystkich użytkowników może być deweloperem lub firmy. Można to zrobić przez dodanie tych samych ustawień powyżej do globalnych znajduje się w pliku konfiguracji w NuGet `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`. Poszczególnym użytkownikom można selektywnie włączysz przywracania na poziomie projektu. Zobacz [Konfigurowanie zachowania NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) dokładne szczegółowe informacje na temat sposobu NuGet priorytetem wiele plików konfiguracji.

## <a name="constraining-package-versions-with-restore"></a>Ograniczający wersje pakietu z przywracania

Gdy NuGet przywraca pakietów przy użyciu dowolnej metody, podlegają wszystkie ograniczenia określone w `packages.config`, `project.json`, lub plik projektu:

- `packages.config`: Określ zakres wersji w `allowedVersion` właściwości zależności. Zobacz [ponowne instalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Na przykład:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- `project.json`: Określ zakres wersji bezpośrednio z numerem wersji tych zależności. Na przykład:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- Pakiet odwołań w plikach projektu: Określ zakres wersji bezpośrednio z numerem wersji tych zależności. Na przykład:
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

We wszystkich przypadkach Notacja opisanego w [wersji pakietu](../reference/package-versioning.md).

## <a name="command-line-restore"></a>Przywracanie wiersza polecenia

NuGet 2.7 i nowszych, użyj [przywrócić](../tools/cli-ref-restore.md) polecenia, aby przywrócić wszystkie pakiety w rozwiązaniu (czy używa `packages.config`, `project.json`, lub pakietu odwołań w plikach projektu). W przypadku folderu danego projektu, takie jak `c:\proj\app`, typowe przykłady poniżej każdego przywrócenia pakietów:

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

NuGet 4.0 + i MSBuild 15.1 + umożliwia także `MSBuild /t:restore` zgodnie z opisem na [NuGet pakietu i ich przywracania docelowych elementów MSBuild](../schema/msbuild-targets.md).

## <a name="build-time-restore-in-visual-studio"></a>Przywracanie czas kompilacji w programie Visual Studio

Visual Studio automatycznie przywraca brakujących pakietów domyślnie na początku kompilacji. To zachowanie można zmienić po usunięciu zaznaczenia **Narzędzia > Opcje > Menedżera pakietów NuGet > Ogólne > automatyczne sprawdzenie dostępności dla brakujących pakietów podczas kompilacji w programie Visual Studio**.

Po włączeniu automatycznej przywracania działa w następujący sposób:

1. Po rozpoczęciu kompilacji programu Visual Studio nakazuje NuGet pod kątem przywracania pakietów.
1. NuGet rekursywnie wyszukuje wszystkie `packages.config` wyszukuje pliki w rozwiązaniu, `project.json`, lub jest wyszukiwany w pliku projektu.
1. Dla każdego pakietów na liście plików źródłowych, NuGet kontroli Jeśli już istnieje w rozwiązaniu ( `packages` folderu, `project.lock.json`, lub `project.assets.json` w zależności od tego, czy projekt jest przy użyciu `packages.config`, `project.json`, lub pakietu odwołań w pliki projektu).
1. Jeśli pakiet nie zostanie znaleziony, NuGet podejmuje próbę pobrania pakietu z pamięci podręcznej najpierw (zobacz [Zarządzanie pamięci podręcznej NuGet](../consume-packages/managing-the-nuget-cache.md). Jeśli pakiet nie jest w pamięci podręcznej, NuGet podejmuje próbę pobrania pakietu z włączonych źródeł wymienionych w **Narzędzia > Opcje > Menedżera pakietów NuGet > źródła pakietów w**, w kolejności źródeł. W takim przypadku NuGet nie wskazuje niepowodzenie, można znaleźć pakietu, dopóki wszystkie źródła zostały sprawdzone, po tym czasie zgłasza błąd tylko dla ostatniego źródła na liście. Co za tym idzie takiego błędu oznacza także, że pakiet nie był dostępny na żadnym z innych źródeł albo, nawet jeśli błędy zostały nie wyświetlane dla tych źródeł pojedynczo.
1. Jeśli pobieranie się pomyślnie, NuGet buforuje pakietu i instaluje je do rozwiązania (ponownie, albo do `packages` folderu, `project.lock.json`, lub `project.assets.json`); w przeciwnym razie NuGet kończy się niepowodzeniem i kompilacja zakończy się niepowodzeniem.

W trakcie tego procesu zostanie wyświetlony postęp okno dialogowe z opcji, aby anulować przywracanie pakietu.

## <a name="package-restore-with-team-foundation-build"></a>Przywracanie pakietu z programu Team Foundation Build

Przywracanie pakietu jest często stosowany podczas tworzenia projektów na serwerach kompilacji, tak jak w przypadku Team Foundation Server (TFS) i Visual Studio Team Services (a także innych systemów kompilacji, które nie zostały omówione w tym miejscu).

### <a name="visual-studio-team-services"></a>Visual Studio Team Services

Podczas tworzenia definicji kompilacji na Team Services, wystarczy dołączyć zadań przywracania pakietów NuGet w definicji przed dowolnego zadania kompilacji. To zadanie jest domyślnie włączone w szablony kompilacji.

![Zadanie przywracania pakietów NuGet w definicji kompilacji programu Visual Studio Team Service](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a>Team Foundation Server

Z programem TFS 2013 i nowsze są automatycznie przywrócić pakiety domyślnie podczas kompilacji, pod warunkiem, że używasz zespołu tworzenie szablonu dla Team Foundation Server 2013 lub nowszym.

Jeśli używasz poprzednią wersję szablonów kompilacji (takich jak klastry projektu, które zostały poddane migracji z wcześniejszych wersji programu TFS), musisz również migrację kompilacji tych szablonów do TFS 2013. Oznacza to, zasadniczo odtworzenie części niestandardowe szablony kompilacji dla kontroli źródła (TFVC lub Git) przy użyciu odpowiedniego szablonu.

Dla wcześniejszych wersji programu TFS, należy po prostu zawierają kroku kompilacji do wywołania [wiersza polecenia przywracania](#command-line-restore) zgodnie z wcześniejszym opisem.

Aby uzyskać więcej informacji, zobacz następnie [wskazówki z przywracania pakietów z Team Foundation Build](../consume-packages/team-foundation-build.md).    
