---
title: Ponowne instalowanie i aktualizowanie pakietów NuGet
description: Szczegółowe informacje o tym, kiedy należy ponownie zainstalować i zaktualizować pakiety, podobnie jak w przypadku uszkodzonych odwołań do pakietów w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: conceptual
ms.openlocfilehash: c48980bc3f955a62962ca6e9619ce09f4a94a835
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488076"
---
# <a name="how-to-reinstall-and-update-packages"></a>Jak ponownie zainstalować i zaktualizować pakiety

Poniżej znajduje się wiele sytuacji, w których [można było ponownie zainstalować pakiet](#when-to-reinstall-a-package), gdzie odwołania do pakietu mogą zostać uszkodzone w projekcie programu Visual Studio. W takich przypadkach Odinstalowywanie i ponowna instalacja tej samej wersji pakietu spowoduje przywrócenie tych odwołań do kolejności roboczej. Aktualizacja pakietu oznacza po prostu zainstalowanie zaktualizowanej wersji, która często przywraca pakiet do kolejności roboczej.

W programie Visual Studio konsola Menedżera pakietów zawiera wiele elastycznych opcji aktualizowania i instalowania pakietów.

Aktualizowanie i ponowne instalowanie pakietów odbywa się w następujący sposób:

| Metoda | Aktualizowanie | Następnie |
| --- | --- | --- |
| Konsola Menedżera pakietów (opisana w temacie [using Update-Package](#using-update-package)) | `Update-Package`dotyczące | `Update-Package -reinstall`dotyczące |
| Interfejs użytkownika menedżera pakietów | Na karcie **aktualizacje** wybierz co najmniej jeden pakiet i wybierz pozycję **Aktualizuj** . | Na karcie **zainstalowane** wybierz pakiet, Zapisz jego nazwę, a następnie wybierz pozycję **Odinstaluj**. Przejdź do karty **Przeglądaj** , wyszukaj nazwę pakietu, wybierz ją, a następnie wybierz pozycję **Zainstaluj**. |
| Interfejs wiersza polecenia NuGet. exe | `nuget update`dotyczące | W przypadku wszystkich pakietów Usuń folder pakietu, a następnie uruchom `nuget install`polecenie. W przypadku jednego pakietu Usuń folder pakietu i Użyj `nuget install <id>` programu, aby ponownie zainstalować ten sam plik. |

> [!NOTE]
> W przypadku interfejsu wiersza polecenia dotnet odpowiednik procedury nie jest wymagany. W podobnym scenariuszu można [przywrócić pakiety za pomocą interfejsu wiersza polecenia dotnet](package-restore.md#restore-using-the-dotnet-cli).

W tym artykule:

- [Kiedy należy ponownie zainstalować pakiet](#when-to-reinstall-a-package)
- [Ograniczenia dotyczące wersji uaktualnienia](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a>Kiedy należy ponownie zainstalować pakiet

1. **Przerwane odwołania po przywróceniu pakietu**: Jeśli otwarto projekt i przywrócono pakiety NuGet, ale nadal są wyświetlane uszkodzone odwołania, spróbuj zainstalować ponownie każdy z tych pakietów.
1. **Projekt został przerwany z powodu usuniętych plików**: Pakiet NuGet nie uniemożliwia usuwania elementów dodanych z pakietów, dzięki czemu można łatwo przypadkowo zmodyfikować zawartość zainstalowaną z pakietu i przerwać projekt. Aby przywrócić projekt, zainstaluj ponownie odpowiednie pakiety.
1. **Aktualizacja pakietu przerwała projekt**: Jeśli aktualizacja pakietu powoduje przerwanie projektu, błąd jest zwykle spowodowany przez pakiet zależności, który mógł również zostać zaktualizowany. Aby przywrócić stan zależności, zainstaluj ponownie ten określony pakiet.
1. Przekierowanie **lub uaktualnienie projektu**: Może to być przydatne w przypadku przekierowania lub uaktualnienia projektu, a jeśli pakiet wymaga ponownej instalacji z powodu zmiany w strukturze docelowej. Pakiet NuGet pokazuje błąd kompilacji w takich przypadkach natychmiast po przekierowaniu projektu, a kolejne ostrzeżenia kompilacji informują o tym, że może być konieczne ponowne zainstalowanie pakietu. W przypadku uaktualniania projektu pakiet NuGet pokazuje błąd w dzienniku uaktualniania projektu.
1. **Ponowna instalacja pakietu w trakcie jego tworzenia**: Autorzy pakietów często muszą ponownie zainstalować tę samą wersję pakietu, który opracowuje, aby przetestować zachowanie. Polecenie nie udostępnia opcji wymuszenia ponownej instalacji, dlatego należy zamiast `Update-Package -reinstall` tego użyć. `Install-Package`

## <a name="constraining-upgrade-versions"></a>Ograniczenia dotyczące wersji uaktualnienia

Domyślnie ponowna instalacja lub aktualizacja pakietu *zawsze* instaluje najnowszą wersję dostępną ze źródła pakietu.

Jednak w projektach korzystających z `packages.config` formatu zarządzania można ograniczyć zakres wersji. Na przykład, Jeśli wiesz, że aplikacja działa tylko w wersji 1. x pakietu, ale nie 2,0 i wyższych, prawdopodobnie z powodu poważnej zmiany w interfejsie API pakietu, a następnie chcesz ograniczyć uaktualnienia do wersji 1. x. Zapobiega to przypadkowym aktualizacjom, które spowodują uszkodzenie aplikacji.

Aby ustawić ograniczenie, Otwórz `packages.config` w edytorze tekstu, odszukaj zależność i `allowedVersions` Dodaj atrybut do zakresu wersji. Na przykład, aby ograniczyć aktualizacje do wersji 1. x, ustaw `allowedVersions` na `[1,2)`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

We wszystkich przypadkach należy użyć notacji opisanej w artykule [przechowywanie wersji pakietu](../concepts/package-versioning.md#version-ranges-and-wildcards).

## <a name="using-update-package"></a>Korzystanie z pakietu aktualizacji

W trosce o [zagadnienia](#considerations) opisane poniżej można łatwo ponownie zainstalować dowolny pakiet za pomocą [polecenia Update-Package](../reference/ps-reference/ps-ref-update-package.md) w konsoli Menedżera pakietów programu Visual Studio (**Narzędzia** > **Menedżera** pakietówNuGet >  **Konsola Menedżera pakietów**).

```ps
Update-Package -Id <package_name> –reinstall
```

Użycie tego polecenia jest znacznie łatwiejsze niż usunięcie pakietu, a następnie próba zlokalizowania tego samego pakietu w galerii NuGet z tą samą wersją. Należy pamiętać, `-Id` że przełącznik jest opcjonalny.

To samo polecenie bez `-reinstall` aktualizacji pakietu do nowszej wersji, jeśli ma zastosowanie. Polecenie powoduje błąd, jeśli dany pakiet nie jest jeszcze zainstalowany w projekcie; oznacza to, `Update-Package` że program nie instaluje pakietów bezpośrednio.

```ps
Update-Package <package_name>
```

Domyślnie `Update-Package` wpływa na wszystkie projekty w rozwiązaniu. Aby ograniczyć akcję do określonego projektu, użyj `-ProjectName` przełącznika przy użyciu nazwy projektu wyświetlanej w Eksplorator rozwiązań:

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```

Aby *zaktualizować* wszystkie pakiety w projekcie (lub ponownie zainstalować program `-reinstall`przy użyciu programu `-ProjectName` ), użyj polecenia bez określenia określonego pakietu:

```ps
Update-Package -ProjectName MyProject
```

Aby zaktualizować wszystkie pakiety w rozwiązaniu, wystarczy użyć `Update-Package` samego siebie niezależnie od innych argumentów lub przełączników. Użyj tego formularza uważnie, ponieważ wykonanie wszystkich aktualizacji może zająć dużo czasu:

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

Aktualizowanie pakietów w projekcie lub rozwiązaniu przy użyciu programu [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) zawsze aktualizuje najnowszą wersję pakietu (z wyłączeniem pakietów wersji wstępnej). Projekty, które `packages.config` używają programu mogą, w razie potrzeby, ograniczyć wersje aktualizacji zgodnie z poniższym opisem w artykule [ograniczenia dotyczące wersji uaktualnienia](#constraining-upgrade-versions).

Aby uzyskać szczegółowe informacje na temat tego polecenia, zobacz informacje dotyczące [aktualizacji pakietu](../reference/ps-reference/ps-ref-update-package.md) .

### <a name="considerations"></a>Uwagi

W przypadku ponownej instalacji pakietu mogą wystąpić następujące zmiany:

1. **Ponowne instalowanie pakietów zgodnie z przekierowaniem platformy docelowej projektu**
    - W prostym przypadku wystarczy ponownie zainstalować pakiet przy użyciu `Update-Package –reinstall <package_name>` programu Works. Pakiet instalowany względem starej platformy docelowej zostanie odinstalowany, a ten sam pakiet zostanie zainstalowany w porównaniu z bieżącą platformą docelową projektu.
    - W niektórych przypadkach może istnieć pakiet, który nie obsługuje nowej platformy docelowej.
        - Jeśli pakiet obsługuje biblioteki klas przenośnych (PCLs), a projekt zostanie przekierowaniy do kombinacji platform, które nie są już obsługiwane przez pakiet, nie będzie można odwoływać się do pakietu po ponownej instalacji.
        - Może to być obszar dla pakietów, które są używane bezpośrednio lub dla pakietów zainstalowanych jako zależności. Jest możliwe, aby pakiet był używany bezpośrednio do obsługi nowej platformy docelowej, a jej zależność nie jest.
        - Jeśli ponowne instalowanie pakietów po przekierowaniu aplikacji spowoduje błędy kompilacji lub wykonania, może być konieczne przywrócenie platformy docelowej lub wyszukanie alternatywnych pakietów, które prawidłowo obsługują nową platformę docelową.

1. **atrybut requireReinstallation został dodany w pliku Packages. config po przekierowaniu lub uaktualnieniu projektu**
    - Jeśli program NuGet wykryje, że pakiety miały wpływ na przekierowanie lub uaktualnianie projektu, `requireReinstallation="true"` dodaje `packages.config` atrybut do wszystkich odwołań do pakietów, których to dotyczy. Z tego powodu każda kolejna kompilacja w programie Visual Studio zgłasza ostrzeżenia kompilacji dla tych pakietów, aby można było zapamiętać, aby zainstalować je ponownie.

1. **Ponowne instalowanie pakietów z zależnościami**
    - `Update-Package –reinstall`zainstaluje ponownie tę samą wersję oryginalnego pakietu, ale instaluje najnowszą wersję zależności, chyba że zostaną podane określone ograniczenia wersji. Pozwala to zaktualizować tylko zależności wymagane do rozwiązania problemu. Jeśli jednak spowoduje to przywrócenie zależności do wcześniejszej wersji, można użyć `Update-Package <dependency_name>` programu, aby ponownie zainstalować tę zależność bez wpływu na pakiet zależny.
    - `Update-Package –reinstall <packageName> -ignoreDependencies`instaluje ponownie tę samą wersję oryginalnego pakietu, ale nie powoduje ponownej instalacji zależności. Użyj tego elementu, gdy aktualizowanie zależności pakietów może spowodować uszkodzenie stanu

1. **Ponowne instalowanie pakietów, gdy są objęte zależnymi wersjami**
    - Jak wyjaśniono powyżej, ponowna instalacja pakietu nie zmienia wersji żadnych innych zainstalowanych pakietów, które od niego zależą. Jest możliwe, że ponowne zainstalowanie zależności może spowodować przerwanie pakietu zależnego.
