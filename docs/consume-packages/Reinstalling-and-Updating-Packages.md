---
title: Ponowna instalacja i aktualizowanie pakietów NuGet
description: Szczegółowe informacje o tym, kiedy jest to konieczne do ponownej instalacji i aktualizacji pakietów, tak jak w przypadku odwołań do pakietów przerwanych w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: conceptual
ms.openlocfilehash: 101c6d6b9d93da912f60c40b27559e80327154b8
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428703"
---
# <a name="how-to-reinstall-and-update-packages"></a>Jak ponownie zainstalować i zaktualizować pakiety

Istnieje wiele sytuacji, opisane poniżej w obszarze [Kiedy ponownie zainstalować pakiet](#when-to-reinstall-a-package), gdzie odwołania do pakietu może zostać przerwane w ramach projektu programu Visual Studio. W takich przypadkach odinstalowanie, a następnie ponowne zainstalowanie tej samej wersji pakietu spowoduje przywrócenie tych odwołań do stanu używa. Aktualizacja pakietu oznacza po prostu zainstalowanie zaktualizowanej wersji, która często przywraca pakiet do kolejności pracy.

W programie Visual Studio konsola Menedżera pakietów udostępnia wiele elastycznych opcji aktualizowania i ponownej instalacji pakietów.

Aktualizowanie i ponowna instalacja pakietów odbywa się w następujący sposób:

| Metoda | Aktualizacja | Ponowna instalacja |
| --- | --- | --- |
| Konsola Menedżera pakietów (opisana w [aplikacji Using Update-Package)](#using-update-package) | Polecenie `Update-Package` | Polecenie `Update-Package -reinstall` |
| Interfejs użytkownika menedżera pakietów | Na karcie **Aktualizacje** wybierz jeden lub więcej pakietów i wybierz pozycję **Aktualizuj** | Na karcie **Zainstalowany** wybierz pakiet, zapisz jego nazwę, a następnie wybierz pozycję **Odinstaluj**. Przełącz się na kartę **Przeglądaj,** wyszukaj nazwę pakietu, wybierz ją, a następnie wybierz pozycję **Zainstaluj**). |
| Interfejs wiersza polecenia nuget.exe | Polecenie `nuget update` | W przypadku wszystkich pakietów usuń `nuget install`folder pakietu, a następnie uruchom program . W przypadku pojedynczego pakietu usuń `nuget install <id>` folder pakietu i użyj do ponownej instalacji tego samego. |

> [!NOTE]
> W przypadku interfejsu wiersza polecenia dotnet równoważna procedura nie jest wymagana. W podobnym scenariuszu można [przywrócić pakiety za pomocą dotnet CLI](package-restore.md#restore-using-the-dotnet-cli).

W tym artykule:

- [Kiedy ponownie zainstalować pakiet](#when-to-reinstall-a-package)
- [Ograniczanie wersji uaktualnienia](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a>Kiedy ponownie zainstalować pakiet

1. **Przerwane odwołania po przywróceniu pakietu:** Jeśli otworzysz projekt i przywrócisz pakiety NuGet, ale nadal widzisz przerwane odwołania, spróbuj ponownie zainstalować każdy z tych pakietów.
1. **Projekt jest uszkodzony z powodu usuniętych plików:** NuGet nie uniemożliwia usuwania elementów dodanych z pakietów, więc łatwo jest przypadkowo zmodyfikować zawartość zainstalowaną z pakietu i przerwać projekt. Aby przywrócić projekt, zainstaluj ponownie pakiety, których dotyczy problem.
1. **Aktualizacja pakietu przerwała projekt:** Jeśli aktualizacja pakietu przerywa projekt, błąd jest zazwyczaj spowodowany przez pakiet zależności, który również mógł zostać zaktualizowany. Aby przywrócić stan zależności, zainstaluj ponownie ten określony pakiet.
1. **Retargeting lub uaktualnienie projektu:** Może to być przydatne, gdy projekt został ponownie ukierunkowany lub uaktualniony i jeśli pakiet wymaga ponownej instalacji ze względu na zmianę struktury docelowej. NuGet pokazuje błąd kompilacji w takich przypadkach natychmiast po retargeting projektu, a kolejne ostrzeżenia kompilacji poinformować, że pakiet może wymagać ponownej instalacji. W przypadku uaktualnienia projektu nuget pokazuje błąd w dzienniku uaktualnienia projektu.
1. **Ponowne instalowanie pakietu podczas jego tworzenia:** Autorzy pakietu często muszą ponownie zainstalować tę samą wersję pakietu, którą opracowują, aby przetestować zachowanie. Polecenie `Install-Package` nie zapewnia opcji wymuszenia ponownej `Update-Package -reinstall` instalacji, więc zamiast tego należy go użyć.

## <a name="constraining-upgrade-versions"></a>Ograniczanie wersji uaktualnienia

Domyślnie ponowna instalacja lub aktualizowanie pakietu *zawsze* instaluje najnowszą wersję dostępną ze źródła pakietu.

W projektach `packages.config` przy użyciu formatu zarządzania można jednak w szczególności ograniczyć zakres wersji. Na przykład jeśli wiesz, że aplikacja działa tylko w wersji 1.x pakietu, ale nie 2.0 i powyżej, być może ze względu na poważne zmiany w interfejsie API pakietu, następnie chcesz ograniczyć uaktualnienia do wersji 1.x. Zapobiega to przypadkowe aktualizacje, które mogłyby złamać aplikację.

Aby ustawić ograniczenie, `packages.config` otwórz w edytorze tekstu, znajdź daną `allowedVersions` zależność i dodaj atrybut z zakresem wersji. Na przykład, aby ograniczyć aktualizacje do `allowedVersions` `[1,2)`wersji 1.x, ustawiono na:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

We wszystkich przypadkach należy użyć notacji opisanej w [wersji pakietu](../concepts/package-versioning.md#version-ranges).

## <a name="using-update-package"></a>Korzystanie z pakietu aktualizacji

Mając na uwadze [zagadnienia](#considerations) opisane poniżej, można łatwo ponownie zainstalować dowolny pakiet za pomocą [polecenia Update-Package](../reference/ps-reference/ps-ref-update-package.md) w konsoli Programu Visual Studio Package Manager (**Tools** > **NuGet Package Manager** > **Package Manager Console**).

```ps
Update-Package -Id <package_name> –reinstall
```

Za pomocą tego polecenia jest znacznie łatwiejsze niż usunięcie pakietu, a następnie próbuje zlokalizować ten sam pakiet w galerii NuGet z tej samej wersji. Należy pamiętać, że `-Id` przełącznik jest opcjonalny.

To samo `-reinstall` polecenie bez aktualizacji pakietu do nowszej wersji, jeśli ma to zastosowanie. Polecenie podaje błąd, jeśli dany pakiet nie jest jeszcze zainstalowany w projekcie; oznacza to, `Update-Package` że nie instaluje pakietów bezpośrednio.

```ps
Update-Package <package_name>
```

Domyślnie `Update-Package` wpływa na wszystkie projekty w rozwiązaniu. Aby ograniczyć akcję do określonego `-ProjectName` projektu, użyj przełącznika, używając nazwy projektu, która pojawia się w Eksploratorze rozwiązań:

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```

Aby *zaktualizować* wszystkie pakiety w projekcie `-reinstall`(lub `-ProjectName` ponownie zainstalować przy użyciu ), należy użyć bez określania konkretnego pakietu:

```ps
Update-Package -ProjectName MyProject
```

Aby zaktualizować wszystkie pakiety w `Update-Package` rozwiązaniu, po prostu użyj samodzielnie bez innych argumentów lub przełączników. Użyj tego formularza ostrożnie, ponieważ może to zająć dużo czasu, aby wykonać wszystkie aktualizacje:

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

Aktualizowanie pakietów w projekcie lub rozwiązaniu przy użyciu [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) zawsze aktualizuje do najnowszej wersji pakietu (z wyłączeniem pakietów wersji wstępnej). Projekty, `packages.config` które używają można, w razie potrzeby, ograniczyć wersje aktualizacji, jak opisano poniżej w [Ograniczające wersje uaktualnienia](#constraining-upgrade-versions).

Aby uzyskać szczegółowe informacje na temat polecenia, zobacz [update-package](../reference/ps-reference/ps-ref-update-package.md) odwołania.

### <a name="considerations"></a>Zagadnienia do rozważenia

Podczas ponownej instalacji pakietu może mieć wpływ następujące elementy:

1. **Ponowna instalacja pakietów zgodnie z retargetingem struktury docelowej projektu**
    - W prostym przypadku wystarczy ponownie zainstalować `Update-Package –reinstall <package_name>` pakiet przy użyciu działa. Pakiet, który jest zainstalowany w starej platformie docelowej zostanie odinstalowany i ten sam pakiet zostanie zainstalowany w ramach bieżącej struktury docelowej projektu.
    - W niektórych przypadkach może istnieć pakiet, który nie obsługuje nowej struktury docelowej.
        - Jeśli pakiet obsługuje biblioteki klas przenośnych (PCLs), a projekt jest ponownie kierowane do kombinacji platform, które nie są już obsługiwane przez pakiet, odwołania do pakietu będą brakować po ponownej instalacji.
        - To może powierzchni dla pakietów, których używasz bezpośrednio lub dla pakietów zainstalowanych jako zależności. Jest możliwe dla pakietu, którego używasz bezpośrednio do obsługi nowej struktury docelowej, podczas gdy jego zależność nie.
        - Jeśli ponowna instalacja pakietów po retargeting wyników aplikacji w kompilacji lub środowiska uruchomieniowego błędów, może być konieczne przywrócenie struktury docelowej lub wyszukać alternatywne pakiety, które poprawnie obsługują nową platformę docelową.

1. **requireReinstallation atrybut dodany w packages.config po retargeting projektu lub uaktualnienia**
    - Jeśli NuGet wykryje, że pakiety zostały naruszone przez `requireReinstallation="true"` retargeting lub uaktualnienie projektu, dodaje atrybut `packages.config` do wszystkich odwołań do pakietu, którego dotyczy problem. W związku z tym każda kolejna kompilacja w programie Visual Studio wywołuje ostrzeżenia kompilacji dla tych pakietów, dzięki czemu można pamiętać, aby ponownie je zainstalować.

1. **Ponowna instalacja pakietów z zależnościami**
    - `Update-Package –reinstall`ponownie instaluje tę samą wersję oryginalnego pakietu, ale instaluje najnowszą wersję zależności, chyba że są podane ograniczenia określonej wersji. Dzięki temu można zaktualizować tylko zależności wymagane do rozwiązania problemu. Jeśli jednak ta zależność powróci do wcześniejszej wersji, można użyć `Update-Package <dependency_name>` do ponownej instalacji tej jednej zależności bez wpływu na pakiet zależny.
    - `Update-Package –reinstall <packageName> -ignoreDependencies`ponownie instaluje tę samą wersję oryginalnego pakietu, ale nie instaluje ponownie zależności. Użyj tego podczas aktualizowania zależności pakietu może spowodować przerwany stan

1. **Ponowna instalacja pakietów, gdy zaangażowane są wersje zależne**
    - Jak wyjaśniono powyżej, ponowna instalacja pakietu nie powoduje zmiany wersji innych zainstalowanych pakietów, które są od niego zależne. Możliwe jest zatem, że ponowne zainstalowanie zależności może spowodować przerwanie pakietu zależnego.
