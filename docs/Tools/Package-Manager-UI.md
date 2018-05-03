---
title: Informacje o interfejsie użytkownika Menedżera pakietów NuGet
description: Instrukcje dotyczące używania interfejsu użytkownika Menedżera pakietów NuGet w programie Visual Studio do pracy z pakietami NuGet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 99bd51798460a56cb8515d46791a9e75d9e630cc
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-package-manager-ui"></a>Interfejs użytkownika Menedżera pakietów NuGet

Interfejs użytkownika Menedżera pakietów NuGet w programie Visual Studio w systemie Windows umożliwia łatwe instalowanie, odinstalowywanie oraz aktualizację pakietów NuGet w projekty i rozwiązania. Środowisko w programie Visual Studio dla komputerów Mac, zobacz [pakietu w tym NuGet w projekcie](/visualstudio/mac/nuget-walkthrough). Interfejs użytkownika Menedżera pakietów nie jest uwzględniona w programie Visual Studio Code.

W tym temacie:

- [Znajdowanie i instalowanie pakietu (Przeglądaj karta)](#finding-and-installing-a-package)
- [Odinstalowywanie pakietu (karta zainstalowana)](#uninstalling-a-package)
- [Aktualizowanie pakietu (instalacji i aktualizacji karty)](#updating-a-package) (obejmuje ["Niejawnie odwołuje się zestaw SDK" lub "AutoReferenced" wiadomości](#implicit_reference))
- [Zarządzanie pakietami dla rozwiązania](#managing-packages-for-the-solution) (Praca z wieloma projektami w tym samym czasie).
- [Źródła pakietów](#package-sources)
- [Kontrolki opcji Menedżera pakietów](#package-manager-options-control)

> [!Note]
> Sprawdź, czy jest Brak Menedżera pakietów NuGet w programie Visual Studio 2015, **Narzędzia > rozszerzenia i aktualizacje...**  i wyszukaj *Menedżera pakietów NuGet* rozszerzenia. Jeśli nie można użyć Instalatora rozszerzeń programu Visual Studio, pobierz rozszerzenie bezpośrednio z [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).
>
> W programie Visual Studio 2017 r. NuGet i Menedżer pakietów NuGet są automatycznie instalowane ze wszystkimi. Obciążenia związane z sieci. Zainstalować oddzielnie, wybierając **pojedynczych składników > narzędzia Code > Menedżera pakietów NuGet** opcji w Instalatorze programu Visual Studio 2017 r.

## <a name="finding-and-installing-a-package"></a>Znajdowanie i instalowanie pakietu

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy albo **odwołania** lub projektu i wybierz **Zarządzaj pakietami NuGet...** .

    ![Zarządzanie pakietami NuGet opcji menu](media/ManagePackagesUICommand.png)

1. **Przeglądaj** karcie są wyświetlane pakiety przez popularne z aktualnie wybranego źródła (zobacz [pakietu źródeł](#package-sources)). Wyszukiwanie określonego pakietu przy użyciu pola wyszukiwania w lewym górnym rogu. Wybierz pakiet z listy, aby wyświetlić jego informacje, które umożliwia również **zainstalować** przycisk wraz z menu rozwijane wyboru wersji.

    ![Zarządzaj kartą Przeglądaj okna dialogowego pakietów NuGet](media/Search.png)

1. Wybierz żądaną wersję z listy rozwijanej i wybierz **zainstalować**. Visual Studio instaluje pakiet i jego zależności w projekcie. Może być monit zaakceptować warunki umowy licencyjnej. Po zakończeniu instalacji dodano pakiety są wyświetlane na **zainstalowana** kartę. Pakiety są również wyświetlane w **odwołania** węzła Eksploratorze rozwiązań i wskazujący, że można odwołać się do nich w projekcie z `using` instrukcje.

    ![Odwołania w Eksploratorze rozwiązań](media/References.png)

> [!Tip]
> Aby w wyszukiwaniu uwzględnić wersje wstępne i udostępnić wersje wstępne w wersji listy rozwijanej, wybierz **Uwzględnij wersję wstępną** opcji.

## <a name="uninstalling-a-package"></a>Odinstalowywanie pakietu

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy albo **odwołania** lub żądanego projektu i wybierz **Zarządzaj pakietami NuGet...** .
1. Wybierz **zainstalowana** kartę.
1. Wybierz pakietu do odinstalowania (za pomocą wyszukiwania, aby filtrować listę, jeśli to konieczne), a następnie wybierz **Odinstaluj**.

    ![Odinstalowywanie pakietu](media/UninstallPackage.png)

1. Należy pamiętać, że **Uwzględnij wersję wstępną** i **źródła pakietu** formanty nie mają żadnego skutku odinstalowanie pakietów.

## <a name="updating-a-package"></a>Aktualizowanie pakietu

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy albo **odwołania** lub żądanego projektu i wybierz **Zarządzaj pakietami NuGet...** . (W projektach witryny sieci web, kliknij prawym przyciskiem myszy **Bin** folderu.)
1. Wybierz **aktualizacje** kartę, aby wyświetlić pakiety, które są dostępne aktualizacje ze źródeł wybranego pakietu. Wybierz **Uwzględnij wersję wstępną** do dołączenia do listy aktualizacji pakiety wersji wstępnej.
1. Wybierz pakiet aktualizacji, wybierz odpowiednią wersję z listy rozwijanej po prawej stronie, a następnie wybierz **aktualizacji**.

    ![Aktualizowanie pakietu](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>W przypadku niektórych pakietów **aktualizacji** przycisku jest wyłączona i zostanie wyświetlony komunikat informujący o tym, że "niejawnie odwołuje się zestaw SDK" (lub "AutoReferenced"). Komunikat wskazuje, że pakiet, takie jak Microsoft.NETCore.App lub Microsoft.NETStandard.Library, jest częścią większej struktury lub zestawu SDK i nie powinny być aktualizowane niezależnie. (Takie pakiety wewnętrznie są oznaczone ikoną z `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Do zaktualizowania pakietu, należy zaktualizować zestawu SDK, do którego on należy.

    ![Przykład pakietu oznaczenie niejawnie odwołania lub AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. Aby zaktualizować wielu pakietów do swoich najnowszej wersji, wybierz je na liście i wybierz **aktualizacji** przycisk powyżej listy.
1. Można także zaktualizować poszczególnych pakietu z **zainstalowana** kartę. W takim przypadku informacje dla pakietu zawierają selektora wersji (podlega **Uwzględnij wersję wstępną** opcji) i **aktualizacji** przycisku.

## <a name="managing-packages-for-the-solution"></a>Zarządzanie pakietami dla rozwiązania

Zarządzanie pakietami dla rozwiązania to wygodny sposób pracować z wieloma projektami równocześnie.

1. Wybierz **Narzędzia > Menedżera pakietów NuGet > Zarządzaj pakietami NuGet dla rozwiązania...**  menu poleceń, lub kliknij rozwiązanie prawym przyciskiem myszy i wybierz polecenie **Zarządzaj pakietami NuGet...** :

    ![Zarządzaj pakietami NuGet dla rozwiązania](media/ManagePackagesSolutionUICommand.png)

1. Podczas zarządzania pakietami dla rozwiązania, interfejs użytkownika umożliwia Wybierz projekty, do których zastosowano operacje:

    ![Selektor projektu podczas zarządzania pakietami dla rozwiązania](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Konsolidacja kartę

Deweloperzy zazwyczaj uważają, że zły praktyką jest używanie różnych wersji tego samego pakietu NuGet wielu różnych projektów, w tym samym rozwiązaniu. W przypadku zarządzania pakietami dla rozwiązania interfejsu użytkownika Menedżera pakietów zawiera **Konsoliduj** kartę, na którym można łatwo widzisz gdzie pakiety z różnych wersji numery są używane przez różne projekty w rozwiązaniu:

![Karta skonsolidować interfejsu użytkownika Menedżera pakietów](media/ConsolidateTab.png)

W tym przykładzie projektu ClassLibrary1 jest za pomocą platformy EntityFramework 6.2.0, podczas gdy ConsoleApp1 jest za pomocą platformy EntityFramework 6.1.0. Aby skonsolidować wersji pakietu, wykonaj następujące czynności:

- Wybierz projekty, aby zaktualizować w liście projektu.
- Wybierz wersję do użycia w tych projektach w **wersji** kontroli, takich jak EntityFramework 6.2.0.
- Wybierz **zainstalować** przycisku.

Menedżer pakietów instaluje wersję wybranego pakietu do wszystkich wybranych projektów, po których pakiet nie jest już widoczna na **Konsoliduj** kartę.

## <a name="package-sources"></a>Źródła pakietów

Aby zmienić źródło, z którego program Visual Studio pobiera pakiety, wybierz jedną z selektora źródła:

![Selektor źródła pakietu w interfejs użytkownika Menedżera pakietów](media/PackageSourceDropDown.png)

Aby zarządzać źródła pakietów:

1. Wybierz **ustawienia** ikonę w Interfejsie użytkownika Menedżera pakietów przedstawione poniżej lub użyj **Narzędzia > Opcje** polecenia, a następnie przewiń do **Menedżera pakietów NuGet**:

    ![Ikona ustawienia interfejsu użytkownika Menedżera pakietów](media/PackageSourceSettings.png)

1. Wybierz **źródła pakietów** węzła:

    ![Opcje źródła pakietów](media/options.png)

1. Aby dodać źródła, wybierz **+**, umożliwia edytowanie nazwy, wprowadź adres URL lub ścieżkę w **źródła** kontroli i wybierz **aktualizacji**. Źródło jest teraz wyświetlany w selektorze listy rozwijanej.
1. Aby zmienić źródło pakietu, wybierz ją, wprowadź zmiany w **nazwa** i **źródła** pola, a następnie wybierz **aktualizacji**.
1. Aby wyłączyć źródła pakietu, usuń zaznaczenie pola nazwy na liście z lewej strony.
1. Aby usunąć źródło pakietu, wybierz go, a następnie wybierz **X** przycisku.
1. W górę i w dół przycisków strzałek, aby zmienić kolejność priorytetów źródła pakietu. Visual Studio wyszukuje tych źródeł w kolejności priorytetu, gdy trwa przywracanie pakietów dla projektu. Aby uzyskać więcej informacji, zobacz [Przywracanie pakietu](../consume-packages/package-restore.md).

> [!Tip]
> Jeśli źródła pakietu zostanie wyświetlony ponownie po jej usunięciu, mogą być wymienione w poziomie komputera lub użytkownika na poziomie `NuGet.Config` plików. Zobacz [NuGet Konfigurowanie zachowania](../consume-packages/configuring-nuget-behavior.md) na lokalizację tych plików, następnie usunąć źródło przez edycję plików ręcznie lub za pomocą [nuget źródeł polecenia](../tools/nuget-exe-CLI-reference.md).

## <a name="package-manager-options-control"></a>Kontrolki opcji Menedżera pakietów

Po wybraniu pakietu interfejsu użytkownika Menedżera pakietów wyświetla mały rozwijania **opcje** kontroli poniżej selektora wersji (przedstawione zarówno zwinięte i rozwinięte). Należy pamiętać, że dla projektu niektórych typów tylko **Pokaż okno podglądu** podano opcję.

![Opcje Menedżera pakietów](media/PackageManagerUIOptions.png)

W poniższych sekcjach opisano te opcje.

### <a name="show-preview-window"></a>Pokaż okno podglądu

Po wybraniu modalny Wyświetla którego zależności wybranego pakietu przed zainstalowaniem pakietu:

![Przykład okna dialogowego podglądu](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Opcje instalacji i aktualizacji

(Niedostępne dla wszystkie typy projektów).

**Zachowanie zależności** konfiguruje sposób NuGet decyduje o tym, które wersje pakietów zależnych, aby zainstalować:

- *Ignoruj zależności* pomija instalowanie zależności, co zwykle przerwie instalowanego pakietu.
- *Najniższa* [domyślnie] instaluje zależności z numerem wersji minimalnego, który spełnia wymagania wybranego pakietu podstawowego.
- *Poprawka najwyższy* powoduje zainstalowanie wersji o tej samej liczby wersji głównej i pomocniczej, ale najwyższy numer poprawki. Na przykład jeśli określono wersję 1.2.2 następnie najwyższej wersji, która rozpoczyna się od 1.2 zostanie zainstalowana
- *Pomocnicze najwyższy* powoduje zainstalowanie wersji tego samego numeru wersji głównej, ale najwyższym numerem i numer poprawki. Jeśli określono wersję 1.2.2, następnie najwyższej wersji, która rozpoczyna się od 1 zostanie zainstalowana
- *Najwyższy* instaluje najwyższy dostępna wersja pakietu.

**Plik akcję konfliktów** określa sposób obsługi NuGet pakiety, które już istnieją w projekcie lub komputer lokalny:

- *Monituj* nakazuje NuGet zapytać, czy zachować, czy zastąpić istniejące pakiety.
- *Ignoruj wszystkie* program NuGet, aby pominąć zastępowanie wszelkie istniejące pakiety.
- *Zastąpienie wszystkich* program NuGet, aby zastąpić wszystkie istniejące pakiety.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Opcji odinstalowywania

(Niedostępne dla wszystkie typy projektów).

**Usuwanie zależności**: po wybraniu usuwa wszystkie zależne pakiety, jeśli ich nie jest wywoływany w innym miejscu w projekcie.

**Życie odinstalować, nawet jeśli istnieją zależności na nim**: po wybraniu odinstalowuje pakiet nawet wtedy, gdy nadal jest ono przywoływane w projekcie. To jest zwykle używana w połączeniu z **usuwanie zależności** do usunięcia pakietu i niezależnie od zależności ona zainstalowana. Przy użyciu tej opcji, może prowadzić do uszkodzenie odwołań w projekcie. W takich przypadkach może być konieczne [ponownie zainstalować inne pakiety](../consume-packages/reinstalling-and-updating-packages.md).
