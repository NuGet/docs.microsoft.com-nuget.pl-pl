---
title: Ponowne instalowanie i aktualizowanie pakietów NuGet
description: Szczegółowe informacje na gdy jest konieczne ponowne zainstalowanie i aktualizację pakietów, tak jak w przypadku odwołania do pakietu przerwane w programie Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: conceptual
ms.openlocfilehash: 86765b56c994c96635feb8e706ff794001a1c1dc
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818298"
---
# <a name="how-to-reinstall-and-update-packages"></a>Jak zainstalować i pakietów aktualizacji

Istnieje wiele sytuacji opisanego poniżej w sekcji [kiedy należy ponownie zainstalować pakiet](#when-to-reinstall-a-package), gdzie odwołania do pakietu zostać przerwane w ramach projektu programu Visual Studio. W takich przypadkach odinstalowanie i ponowne zainstalowanie tej samej wersji pakietu spowoduje przywrócenie tych odwołań do działania. Aktualizowanie pakietu to po prostu zainstalowaniu zaktualizowanej wersji, które często przywraca pakietu sprawne.

Aktualizowanie i ponowne zainstalowanie pakietów odbywa się w następujący sposób:

| Metoda | Aktualizacja | Zainstaluj ponownie |
| --- | --- | --- |
| Konsola Menedżera pakietów (opisany w [pakiet aktualizacji przy użyciu](#using-update-package)) | `Update-Package` polecenie | `Update-Package -reinstall` polecenie |
| Interfejs użytkownika Menedżera pakietów | Na **aktualizacje** , wybierz jeden lub więcej pakietów i zaznacz **aktualizacji** | Na **zainstalowana** , wybierz pakiet, zapisz jego nazwę, a następnie wybierz **Odinstaluj**. Przełącz się do **Przeglądaj** , wyszukaj nazwę pakietu, wybierz go, a następnie wybierz **zainstalować**). |
| nuget.exe interfejsu wiersza polecenia | `nuget update` polecenie | Dla wszystkich pakietów, usuń folder pakietu, a następnie uruchom `nuget install`. Jeden pakiet, usuń folder pakietu i używać `nuget install <id>` ponownie zainstalować ten sam. |

W tym artykule:

- [Kiedy należy ponownie zainstalować pakiet](#when-to-reinstall-a-package)
- [Ograniczający uaktualniania wersji](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a>Kiedy należy ponownie zainstalować pakiet

1. **Uszkodzenie odwołań po przywróceniu pakietu**: Jeśli już otwarty projekt i przywrócić pakietów NuGet, ale nadal odwołania Zobacz uszkodzony, spróbuj ponownie zainstalować każdego z tych pakietów.
1. **Projekt jest uszkodzony z powodu usuniętych plików**: NuGet nie uniemożliwiają usunięcie elementów dodanych z pakietów, więc łatwo przypadkowo modyfikowanie zawartości zainstalowane z pakietu i przerwać projektu. Aby przywrócić projekt, zainstaluj ponownie odpowiednich pakietów.
1. **Aktualizacja pakietu spowodowało przerwanie projektu**: Jeśli aktualizacja pakietu dzieli projektu, awarii jest zazwyczaj spowodowane pakietu zależności, które mogą również zostały zaktualizowane. Aby przywrócić stan zależności, ponownej instalacji tego określonego pakietu.
1. **Projekt przekierowania lub Uaktualnij**: może to być przydatne, gdy projekt został przekierować lub uaktualnić, a pakiet wymaga ponownej instalacji z powodu zmiany w platformie docelowej. NuGet przedstawia błąd kompilacji w takich przypadkach natychmiast po przekierowania projektu oraz ostrzeżenia kompilacji kolejnych informacją o tym, że pakiet może być konieczne ponowne zainstalowanie. Do uaktualnienia projektu NuGet pokazuje błąd w dzienniku uaktualnić projekt.
1. **Ponowna instalacja pakietu podczas jego tworzenia**: autorów pakietu często konieczne ponowne zainstalowanie tej samej wersji pakietu, tworzony jest do testowania zachowanie. `Install-Package` Polecenia nie zapewnia opcję, aby wymusić konieczności ponownej instalacji, należy więc `Update-Package -reinstall` zamiast tego.

## <a name="constraining-upgrade-versions"></a>Ograniczający uaktualniania wersji

Domyślnie, ponownej instalacji lub aktualizacji pakietu *zawsze* instaluje najnowszą wersję dostępne w źródle pakietów.

W projektach przy użyciu `packages.config` format zarządzania, w szczególności ograniczyć zakres wersji. Na przykład jeśli wiadomo, że aplikacja działa tylko z wersją 1.x pakietu ale nie 2.0 i nowszych, prawdopodobnie z powodu istotne zmiany w pakiecie interfejsu API, możesz warto, aby ograniczyć uaktualnienia do wersji 1.x. Pozwala to zapobiec przypadkowemu aktualizacje, które spowoduje przerwanie aplikacji.

Aby ustawić ograniczenie, otwórz `packages.config` w edytorze tekstów, zlokalizuj w zależności, a następnie dodaj `allowedVersions` atrybut z zakres wersji. Na przykład, aby ograniczyć aktualizacji do wersji 1.x, ustaw `allowedVersions` do `[1,2)`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

We wszystkich przypadkach Notacja opisanego w [wersji pakietu](../reference/package-versioning.md#version-ranges-and-wildcards).

## <a name="using-update-package"></a>Przy użyciu pakietu aktualizacji

Trwa mając na uwadze [zagadnienia](#considerations) opisane poniżej, można łatwo ponownie zainstalować wszystkie pakietu przy użyciu [polecenia pakiet aktualizacji](../Tools/ps-ref-update-package.md) w konsoli Menedżera pakietów programu Visual Studio (**narzędzia**  >  **Menedżera pakietów NuGet** > **Konsola Menedżera pakietów**):

```ps
Update-Package -Id <package_name> –reinstall
```

To polecenie jest znacznie prostsze niż usunięcie pakietu, a następnie próbuje zlokalizować tego samego pakietu w galerii NuGet z tej samej wersji. Należy pamiętać, że `-Id` przełącznik jest opcjonalne.

Takie same polecenie bez `-reinstall` aktualizuje pakiet do nowszej wersji, jeśli ma to zastosowanie. Polecenie zwraca błąd, jeśli danego pakietu nie jest już zainstalowany w projekcie; oznacza to, że `Update-Package` nie można zainstalować pakietów bezpośrednio.

```ps
Update-Package <package_name>
```

Domyślnie `Update-Package` ma wpływ na wszystkie projekty w rozwiązaniu. Aby ograniczyć akcji do określonego projektu, użyj `-ProjectName` przełącznika, przy użyciu nazwy projektu, pojawiającą się w Eksploratorze rozwiązań:

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```

Do *aktualizacji* wszystkie pakiety w projekcie (lub ponownej instalacji przy użyciu `-reinstall`), użyj `-ProjectName` bez określania dowolnego określonego pakietu:

```ps
Update-Package -ProjectName MyProject
```

Aby zaktualizować wszystkich pakietów w rozwiązaniu, wystarczy użyć `Update-Package` samodzielnie bez argumentów lub przełączników. Ostrożne korzystanie z tego formularza, ponieważ jego może zająć wiele czasu, aby wykonać wszystkie aktualizacje:

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

Aktualizowanie pakietów w projekt lub rozwiązanie przy użyciu [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) zawsze aktualizacji do najnowszej wersji pakietu (z wyjątkiem pakiety wersji wstępnej). Projekty używające `packages.config` w razie potrzeby można ograniczyć wersje aktualizacji zgodnie z poniższym opisem w [wersji uaktualnienie Constraining](#constraining-upgrade-versions).

Aby uzyskać szczegółowe informacje o poleceniu, zobacz [pakiet aktualizacji](../Tools/ps-ref-update-package.md) odwołania.

### <a name="considerations"></a>Uwagi

Następujące może mieć wpływ na podczas ponownej instalacji pakietu:

1. **Ponowna instalacja pakiety zgodnie z projektu docelowego framework przekierowania**
    - W przypadku prostego, po prostu ponowna instalacja pakietu przy użyciu `Update-Package –reinstall <package_name>` działa. Pakiet, który jest zainstalowany na starym platformy docelowej pobiera odinstalowane i tego samego pakietu pobiera przed Bieżąca platforma docelowa projektu.
    - W niektórych przypadkach może być pakietu, który nie obsługuje nowe platformy docelowej.
        - Jeśli pakiet obsługuje bibliotek klas przenośnych (PCLs) i projektu jest przekierować kombinację platform nie jest już obsługiwany przez pakiet, odwołania do pakietu będą niedostępne po ponownej instalacji.
        - To powierzchni dla pakietów, którego używasz, bezpośrednio lub pakiety zainstalowane jako zależności. Istnieje możliwość pakietu używanego bezpośrednio do obsługi nowej struktury docelowej, podczas gdy nie ma zależności.
        - Ponowne instalowanie pakietów po przekierowania aplikacji powoduje kompilacji lub środowisko uruchomieniowe błędów, może być konieczne przywrócenie z platformy docelowej lub Wyszukaj alternatywne pakiety, które poprawnie obsługiwać Twoje nowe platformy docelowej.

1. **Atrybut requireReinstallation po przekierowania projektu lub aktualizacja dodaje w pliku packages.config**
    - Jeśli NuGet wykryje, że pakiety wpłynęła przekierowania lub uaktualniania projektu, dodaje `requireReinstallation="true"` atrybutu w `packages.config` do wszystkich wpływ odwołania do pakietu. W związku z tym każda kolejne kompilacji w programie Visual Studio zgłasza ostrzeżeń kompilacji dla tych pakietów, należy pamiętać zainstalować je ponownie.

1. **Ponowne instalowanie pakietów z zależnościami**
    - `Update-Package –reinstall` Ponownie instaluje tej samej wersji oryginalnego pakietu, ale instaluje najnowszą wersję zależności, ile ograniczenia określonej wersji. Dzięki temu można aktualizować tylko zależności wymagane w celu rozwiązania problemu. Jednak jeśli zależności zbiorcze powrót do wcześniejszej wersji, można użyć `Update-Package <dependency_name>` ponownie zainstalować ten jedną zależność bez wpływu na zależnego pakietu.
    - `Update-Package –reinstall <packageName> -ignoreDependencies` Ponownie instaluje tej samej wersji oryginalnego pakietu, ale nie zainstalować zależności. Użyj go, jeśli zależności pakietów aktualizacji może spowodować uszkodzenie stanu

1. **Ponowne instalowanie pakietów w przypadku wersji zależne**
    - Zgodnie z powyższymi wskazówkami, ponowna instalacja pakietu nie zmienia wersji wszystkie zainstalowane pakiety, które od niego zależne. Jest to możliwe, a następnie tej zależności ponowna instalacja może spowodować przerwanie zależnego pakietu.
