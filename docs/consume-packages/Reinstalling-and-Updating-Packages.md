---
title: Ponowne instalowanie i aktualizowanie pakietów NuGet
description: Szczegółowe informacje dotyczące kiedy zachodzi konieczność ponownej instalacji i aktualizowanie pakietów, podobnie jak w przypadku odwołania do pakietu przerwane w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: conceptual
ms.openlocfilehash: 9b2a7b299a0cb944ad9045684e14cc7b83e1cff4
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426667"
---
# <a name="how-to-reinstall-and-update-packages"></a>Jak zainstalować i pakietów aktualizacji

Istnieje wiele sytuacji, w opisany poniżej w sekcji [podczas ponownej instalacji pakietu](#when-to-reinstall-a-package), gdy odwołania do pakietu zawiera uszkodzone w ramach projektu programu Visual Studio. W takich przypadkach odinstalować i ponownie zainstalować tę samą wersję pakietu spowoduje przywrócenie te odwołania do działania. Aktualizowanie pakietu to po prostu zainstalowaniu zaktualizowanej wersji, które często przywraca pakietu sprawne.

Aktualizowanie i ponowne zainstalowanie pakietów odbywa się w następujący sposób:

| Metoda | Aktualizowanie | Zainstaluj ponownie |
| --- | --- | --- |
| Konsola Menedżera pakietów (opisanego w [pakiet aktualizacji przy użyciu](#using-update-package)) | `Update-Package` Polecenie | `Update-Package -reinstall` Polecenie |
| Interfejs użytkownika menedżera pakietów | Na **aktualizacje** karty, wybierz jeden lub więcej pakietów i wybierz **aktualizacji** | Na **zainstalowane** karty, wybierz pakiet, zapisać jego nazwę, a następnie wybierz **Odinstaluj**. Przełącz się do **Przeglądaj** kartę, wyszukaj nazwę pakietu, wybierz ją, a następnie wybierz **zainstalować**). |
| Interfejs wiersza polecenia nuget.exe | `nuget update` Polecenie | Dla wszystkich pakietów, usuń folder pakietu, a następnie uruchom `nuget install`. Jeden pakiet, usuń folder pakietu i użyj `nuget install <id>` ponowna instalacja taki sam. |

> [!NOTE]
> Wiersz polecenia dotnet odpowiedniej procedury nie jest wymagany. W podobny scenariusz można [przywrócenia pakietów z wiersz polecenia dotnet](../consume-packages/install-use-packages-dotnet-cli.md#restore-packages).

W tym artykule:

- [Kiedy należy ponownie zainstalować pakiet](#when-to-reinstall-a-package)
- [Ograniczający uaktualniania wersji](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a>Kiedy należy ponownie zainstalować pakiet

1. **Uszkodzenie odwołań po Przywracanie pakietu**: Jeśli projekt i przywrócony pakiety NuGet jest już otwarte, ale nadal widzą przerwanymi odwołaniami, spróbuj ponownej instalacji każdej z tych pakietów.
1. **Projekt został przerwany ze względu na usunięte pliki**: NuGet nie uniemożliwiają usunięcie elementy dodane z pakietów, dzięki czemu można łatwo przypadkowo modyfikowanie instalowanych z pakietu zawartości i przerwać projektu. Aby przywrócić projektu, należy ponownie zainstalować pakiety, których to dotyczy.
1. **Aktualizacja pakietu Przerwano projektu**: Jeśli aktualizacja pakietu przerywa projektu, błąd jest zazwyczaj spowodowane pakietu zależności, który może być również zostały zaktualizowane. Aby przywrócić stan zależność, ponownej instalacji tego określonego pakietu.
1. **Projekt, przekierowywanie lub Uaktualnij**: Może to być przydatne, gdy projekt został przekierowano element lub uaktualnić, a pakiet wymaga ponownej instalacji z powodu zmiany platformy docelowej. NuGet pokazuje błąd kompilacji w takich przypadkach natychmiast po przekierowanie projektu oraz ostrzeżenia kompilacji kolejnych pozwalają dowiedzieć się, że pakiet może być wymagana ponowna instalacja. W celu uaktualnienia projektu NuGet, pokazuje błąd, w dzienniku uaktualnienia projektu.
1. **Ponowne zainstalowanie pakietu podczas jego tworzenia**: Autorzy pakietów często trzeba ponownie zainstalować tę samą wersję pakietu, które tworzą się testowanie zachowania. `Install-Package` Polecenia nie zapewnia możliwość wymuszenia konieczności ponownej instalacji, a więc `Update-Package -reinstall` zamiast tego.

## <a name="constraining-upgrade-versions"></a>Ograniczający uaktualniania wersji

Domyślnie, ponownego instalowania lub aktualizowania pakietu *zawsze* instaluje najnowszą wersją dostępną ze źródła pakietu.

W projektach przy użyciu `packages.config` format zarządzania, w szczególności ograniczenie zakresu wersji. Na przykład jeśli wiesz, że aplikacja działa tylko z wersji 1.x pakietu ale nie 2.0 i nowszych, prawdopodobnie ze względu na istotne zmiany w pakiecie interfejsu API, a następnie można będzie chciała ograniczenie jest uaktualniane do wersji 1.x. Zapobiega to przypadkowym aktualizacji, które spowoduje przerwanie aplikacji.

Aby ustawić ograniczenie, otwórz `packages.config` w edytorze tekstów, zlokalizuj omawianego zależności, a następnie dodaj `allowedVersions` atrybutu z zakresu wersji. Na przykład, aby ograniczyć aktualizacji do wersji 1.x, ustaw `allowedVersions` do `[1,2)`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

We wszystkich przypadkach Notacja opisanego w [przechowywanie wersji pakietów](../reference/package-versioning.md#version-ranges-and-wildcards).

## <a name="using-update-package"></a>Użycie pakietu aktualizacji

Trwa w trosce o [zagadnienia](#considerations) opisane poniżej, można łatwo ponownie zainstalować wszystkie pakietu przy użyciu [polecenia Update-Package](../Tools/ps-ref-update-package.md) w konsoli Menedżera pakietów Visual Studio (**narzędzia**  >  **Menedżera pakietów NuGet** > **Konsola Menedżera pakietów**):

```ps
Update-Package -Id <package_name> –reinstall
```

Za pomocą tego polecenia jest znacznie prostsze niż usunięcie pakietu, a następnie wykonywanie próby zlokalizowania tego samego pakietu w galerii pakietów NuGet za pomocą tej samej wersji. Należy pamiętać, że `-Id` przełącznik jest opcjonalne.

Tego samego polecenia bez `-reinstall` aktualizuje pakiet do nowszej wersji, jeśli ma to zastosowanie. Polecenie powoduje błąd, jeśli danego pakietu nie jest już zainstalowany w projekcie; oznacza to, że `Update-Package` nie można zainstalować pakiety bezpośrednio.

```ps
Update-Package <package_name>
```

Domyślnie `Update-Package` ma wpływ na wszystkie projekty w rozwiązaniu. Aby ograniczyć liczbę akcji do określonego projektu, należy użyć `-ProjectName` przełączyć, przy użyciu nazwy projektu, która jest wyświetlana w Eksploratorze rozwiązań:

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```

Do *aktualizacji* wszystkich pakietów w projekcie (lub ponownie zainstalować przy użyciu `-reinstall`), użyj `-ProjectName` bez określania żadnych danego pakietu:

```ps
Update-Package -ProjectName MyProject
```

Aby zaktualizować wszystkie pakiety w rozwiązaniu, wystarczy użyć `Update-Package` samodzielnie bez argumentów lub przełączników. Ten formularz ostrożnie, ponieważ może upłynąć pewien czas do wykonywania wszystkich aktualizacji:

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

Trwa aktualizowanie pakietów w projekcie lub rozwiązaniu przy użyciu [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) zawsze aktualizacji do najnowszej wersji pakietu (z wyjątkiem pakiety w wersji wstępnej). Projekty używające `packages.config` Jeśli to konieczne, ograniczyć wersje aktualizacji zgodnie z poniższym opisem w [wersji uaktualnienie Constraining](#constraining-upgrade-versions).

Aby uzyskać szczegółowe informacje o poleceniu, zobacz [pakiet aktualizacji](../Tools/ps-ref-update-package.md) odwołania.

### <a name="considerations"></a>Uwagi

Następujące może mieć wpływ na podczas ponownej instalacji pakietu:

1. **Ponowne instalowanie pakietów według projektu target framework przekierowania**
    - W przypadku prostych, po prostu ponownie zainstalować pakiet przy użyciu `Update-Package –reinstall <package_name>` działa. Pakiet, który jest zainstalowany przed stare platformę docelową pobiera odinstalowane i tego samego pakietu pobiera względem bieżącej struktury docelowej projektu.
    - W niektórych przypadkach może być pakiet, który nie obsługuje nowe platformy docelowej.
        - Jeśli pakiet obsługuje bibliotek klas przenośnych (PCLs), a projekt jest ukierunkowany na kombinacji platform, które nie jest już obsługiwany przez pakiet, odwołania do pakietu będzie brak po ponownej instalacji.
        - To może pojawiać się pakietami, których używasz, bezpośrednio lub pakietów zainstalowanych jako zależności. Istnieje możliwość pakietu, który bezpośrednio do obsługi nowej platformy docelowej, a jego zależność nie jest używany.
        - Ponowne instalowanie pakietów po przekierowania aplikacji w wyniku kompilacji lub środowisko uruchomieniowe błędów, może być konieczne Przywróć swoje wartości docelowej lub Wyszukaj alternatywnych pakiety, które poprawnie obsługuje Twojej nowej platformy docelowej.

1. **Atrybut requireReinstallation dodane w pliku packages.config po przekierowanie projektu lub uaktualnienia**
    - Jeśli NuGet wykryje, że pakiety wpłynęła na retargeting i uaktualniania projektu, dodaje `requireReinstallation="true"` atrybutu w `packages.config` do wszystkich wpływ na odwołania do pakietu. W związku z tym każdej kolejnej kompilacji w programie Visual Studio zgłasza ostrzeżenia kompilacji dla tych pakietów, dlatego należy pamiętać zainstalować je ponownie.

1. **Ponowne instalowanie pakietów z zależnościami**
    - `Update-Package –reinstall` Ponownie instaluje tę samą wersję z oryginalnego pakietu, ale instaluje najnowszą wersję zależności, chyba że znajdują się ograniczeń określonej wersji. Dzięki temu można zaktualizować tylko zależności zgodnie z potrzebami w celu rozwiązania problemu. Jednakże, jeśli to wycofanie zależność do wcześniejszej wersji, można użyć `Update-Package <dependency_name>` do ponownej instalacji tego jedną zależność bez wywierania wpływu na zależnego pakietu.
    - `Update-Package –reinstall <packageName> -ignoreDependencies` Ponownie instaluje tę samą wersję z oryginalnego pakietu, ale nie zainstalować zależności. Użyj tego ustawienia podczas aktualizowania zależności pakietów może spowodować w stanie uszkodzenia

1. **Ponowne instalowanie pakietów, w przypadku wersji zależne**
    - Jak wyjaśniono powyżej, ponowna instalacja pakietu nie zmienia wersji wszystkie zainstalowane pakiety, które zależą od niej. Jest to możliwe, a następnie tej zależności ponowna instalacja może spowodować przerwanie zależnego pakietu.
