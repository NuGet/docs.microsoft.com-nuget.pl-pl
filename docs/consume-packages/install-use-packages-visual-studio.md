---
title: Instalowanie pakietów NuGet i zarządzanie nimi w programie Visual Studio
description: Instrukcje dotyczące korzystania z interfejsu użytkownika Menedżera pakietów NuGet w programie Visual Studio do pracy z pakietami NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 3adceac8c725d9ea1610aea090753c9c1d8bc818
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428696"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a>Instalowanie pakietów w programie Visual Studio i zarządzanie nimi przy użyciu Menedżera pakietów NuGet

Interfejs użytkownika Menedżera pakietów NuGet w programie Visual Studio w systemie Windows umożliwia łatwe instalowanie, odinstalowywanie i aktualizowanie pakietów NuGet w projektach i rozwiązaniach. Aby uzyskać środowisko w programie Visual Studio dla komputerów Mac, zobacz [Dołączanie pakietu NuGet w projekcie.](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json) Interfejs użytkownika Menedżera pakietów nie jest dołączony do kodu programu Visual Studio.

> [!NOTE]
> Jeśli brakuje Menedżera pakietów NuGet w programie Visual Studio 2015, sprawdź **narzędzia > rozszerzenia i aktualizacje...** i wyszukaj rozszerzenie Menedżera *pakietów NuGet.* Jeśli nie możesz użyć instalatora rozszerzeń w programie Visual [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)Studio, pobierz je bezpośrednio z programu .
>
> Począwszy od programu Visual Studio 2017, NuGet i Menedżer pakietów NuGet są automatycznie instalowane z dowolnym . Obciążenia związane z siecią. Zainstaluj go indywidualnie, wybierając poszczególne składniki > narzędzia Kodu > menedżera **pakietów NuGet** w instalatorze programu Visual Studio.

## <a name="find-and-install-a-package"></a>Znajdowanie i instalowanie pakietu

1. W **Eksploratorze rozwiązań**kliknij prawym przyciskiem myszy **odwołania** lub projekt i wybierz pozycję **Zarządzaj pakietami NuGet...**.

    ![Opcja menu Zarządzanie pakietami NuGet](media/ManagePackagesUICommand.png)

1. Karta **Przeglądaj** wyświetla pakiety według popularności z aktualnie wybranego źródła (patrz [źródła pakietów).](#package-sources) Wyszukaj określony pakiet za pomocą pola wyszukiwania w lewym górnym rogu. Wybierz pakiet z listy, aby wyświetlić jego informacje, co również włącza przycisk **Zainstaluj** wraz z listą rozwijaną wyboru wersji.

    ![Karta Przeglądanie okna dialogowego Zarządzanie pakietami NuGet](media/Search.png)

1. Wybierz żądaną wersję z listy rozwijanej i wybierz **pozycję Zainstaluj**. Visual Studio instaluje pakiet i jego zależności w projekcie. Użytkownik może zostać poproszony o zaakceptowanie postanowień licencyjnych. Po zakończeniu instalacji dodane pakiety są wyświetlane na karcie **References** `using` **Zainstalowane.**

    ![Odwołania w Eksploratorze rozwiązań](media/References.png)

> [!Tip]
> Aby uwzględnić wersje wersji wstępnej w wyszukiwaniu i udostępnić wersje wstępnej w wersji rozwijanej, wybierz opcję **Dołącz wersję wstępną.**

> [!Note]
> NuGet ma dwa formaty, w których [`PackageReference`](package-references-in-project-files.md) [`packages.config`](../reference/packages-config.md)projekt może używać pakietów: i . [Wartość domyślną można ustawić w oknie opcji programu Visual Studio](Package-Restore.md#choose-default-package-management-format).

## <a name="uninstall-a-package"></a>Odinstalowywanie pakietu

1. W **Eksploratorze rozwiązań**kliknij prawym przyciskiem myszy **odwołania** lub żądany projekt, a następnie wybierz pozycję **Zarządzaj pakietami NuGet...**.
1. Wybierz kartę **Zainstalowano**.
1. Wybierz pakiet do odinstalowania (w razie potrzeby za pomocą wyszukiwania odfiltrować listę) i wybierz pozycję **Odinstaluj**.

    ![Odinstalowywanie pakietu](media/UninstallPackage.png)

1. Należy zauważyć, że **uwzględnij prerelease** i **Package source** formantów nie mają wpływu podczas odinstalowywania pakietów.

## <a name="update-a-package"></a>Aktualizowanie pakietu

1. W **Eksploratorze rozwiązań**kliknij prawym przyciskiem myszy **odwołania** lub żądany projekt, a następnie wybierz pozycję **Zarządzaj pakietami NuGet...**. (W projektach witryn sieci Web kliknij prawym przyciskiem myszy folder **Bin).**
1. Wybierz kartę **Aktualizacje,** aby wyświetlić pakiety, które mają dostępne aktualizacje z wybranych źródeł pakietów. Wybierz **dołącz wstępnąrelea,** aby uwzględnić pakiety wersji wstępnej na liście aktualizacji.
1. Wybierz pakiet do aktualizacji, wybierz żądaną wersję z listy rozwijanej po prawej stronie i wybierz pozycję **Aktualizuj**.

    ![Aktualizowanie pakietu](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>W przypadku niektórych pakietów przycisk **Aktualizuj** jest wyłączony i pojawia się komunikat informujący, że jest "niejawnie odwołuje się SDK" (lub "AutoReferenced"). Ten komunikat wskazuje, że pakiet jest częścią większej struktury lub zestawu SDK i nie powinien być aktualizowany niezależnie. (Takie pakiety są `<IsImplicitlyDefined>True</IsImplicitlyDefined>`wewnętrznie oznaczone .) Na przykład `Microsoft.NETCore.App` jest częścią zestawu .NET Core SDK, a wersja pakietu nie jest taka sama jak wersja struktury środowiska wykonawczego używane przez aplikację. Musisz [zaktualizować instalację .NET Core,](https://aka.ms/dotnet-download) aby uzyskać nowe wersje środowiska wykonawczego ASP.NET Core i .NET Core. [Więcej informacji na temat metapakietów rdzeni .NET i przechowywania wersji można znaleźć w tym dokumencie.](/dotnet/core/packages) Dotyczy to następujących powszechnie używanych pakietów:
    * Microsoft.AspNetCore.All
    * Aplikacja Microsoft.AspNetCore.App
    * Aplikacja Microsoft.NETCore.App
    * NETStandard.Library

    ![Przykładowy pakiet oznaczony jako niejawnie odwołania lub AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. Aby zaktualizować wiele pakietów do ich najnowszych wersji, zaznacz je na liście i wybierz przycisk **Aktualizuj** nad listą.
1. Można również zaktualizować pojedynczy pakiet na karcie **Zainstalowane.** W takim przypadku szczegóły pakietu obejmują selektor wersji (z zastrzeżeniem opcji **Dołącz wersję wstępną)** i przycisk **Update.**

## <a name="manage-packages-for-the-solution"></a>Zarządzanie pakietami dla rozwiązania

Zarządzanie pakietami dla rozwiązania jest wygodnym sposobem pracy z wieloma projektami jednocześnie.

1. Wybierz polecenie **menu Narzędzia > Menedżera pakietów NuGet > zarządzanie pakietami NuGet dla rozwiązania...** lub kliknij prawym przyciskiem myszy rozwiązanie i wybierz polecenie **Zarządzaj pakietami NuGet...**

    ![Zarządzanie pakietami NuGet dla rozwiązania](media/ManagePackagesSolutionUICommand.png)

1. Podczas zarządzania pakietami dla rozwiązania interfejsu użytkownika pozwala wybrać projekty, których dotyczą operacje:

    ![Selektor projektu podczas zarządzania pakietami dla rozwiązania](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Karta Konsolidacja

Deweloperzy zazwyczaj uważają, że złe praktyki do korzystania z różnych wersji tego samego pakietu NuGet w różnych projektach w tym samym rozwiązaniu. Po wybraniu do zarządzania pakietami dla rozwiązania, Interfejs menedżera pakietów udostępnia **konsolidować** kartę, na której można łatwo zobaczyć, gdzie pakiety z różnymi numerami wersji są używane przez różne projekty w rozwiązaniu:

![Karta Konsolidacja interfejsu użytkownika menedżera pakietów](media/ConsolidateTab.png)

W tym przykładzie classlibrary1 projektu używa EntityFramework 6.2.0, podczas gdy ConsoleApp1 używa EntityFramework 6.1.0. Aby skonsolidować wersje pakietów, wykonaj następujące czynności:

- Wybierz projekty, które mają być aktualizowane na liście projektów.
- Wybierz wersję, która ma być używana we wszystkich tych projektach w **formancie Wersja,** takich jak EntityFramework 6.2.0.
- Wybierz przycisk **Zainstaluj.**

Menedżer pakietów instaluje wybraną wersję pakietu we wszystkich wybranych projektach, po czym pakiet nie jest już wyświetlany na karcie **Konsolidacja.**

## <a name="package-sources"></a>Źródła pakietów

Aby zmienić źródło, z którego program Visual Studio uzyskuje pakiety, wybierz jeden z selektora źródłowego:

![Selektor źródła pakietów w interfejsie użytkownika menedżera pakietów](media/PackageSourceDropDown.png)

Aby zarządzać źródłami pakietów:

1. Wybierz ikonę **Ustawienia** w interfejsie użytkownika Menedżera pakietów opisanego poniżej lub użyj polecenia **Narzędzia > Opcje** i przewiń do Menedżera **pakietów NuGet:**

    ![Ikona ustawień interfejsu użytkownika menedżera pakietów](media/PackageSourceSettings.png)

1. Wybierz węzeł **Źródła pakietów:**

    ![Opcje źródeł pakietów](media/options.png)

1. Aby dodać źródło, **+** wybierz , edytuj nazwę, wprowadź adres URL lub ścieżkę w formancie **Źródło** i wybierz pozycję **Aktualizuj**. Źródło pojawi się teraz w z listy rozwijanej selektora.
1. Aby zmienić źródło pakietu, zaznacz je, wykonuj zmiany w polach **Nazwa** i **Źródło, a** następnie wybierz pozycję **Aktualizuj**.
1. Aby wyłączyć źródło pakietu, wyczyść pole po lewej stronie nazwy na liście.
1. Aby usunąć źródło pakietu, zaznacz go, a następnie wybierz przycisk **X.**
1. Za pomocą przycisków strzałki w górę i w dół nie zmienia kolejność priorytetów źródeł pakietu. Visual Studio ignoruje kolejność źródeł pakietów, przy użyciu pakietu, z któregokolwiek źródła jest pierwszy odpowiedzieć na żądania. Aby uzyskać więcej informacji, zobacz [Przywracanie pakietu](../consume-packages/package-restore.md).

> [!Tip]
> Jeśli źródło pakietu pojawi się ponownie po usunięciu go, może być wymieniony w `NuGet.Config` plikach na poziomie komputera lub na poziomie użytkownika. Zobacz [typowe konfiguracje NuGet](../consume-packages/configuring-nuget-behavior.md) dla lokalizacji tych plików, a następnie usunąć źródło, edytując pliki ręcznie lub za pomocą [polecenia nuget sources](../reference/nuget-exe-CLI-reference.md).

## <a name="package-manager-options-control"></a>Kontrola opcji menedżera pakietów

Po wybraniu pakietu interfejs użytkownika Menedżera pakietów wyświetla mały, rozwijany **formant Opcji** poniżej selektora wersji (pokazane tutaj zarówno zwinięte, jak i rozwinięte). Należy zauważyć, że w przypadku niektórych typów projektów dostępna jest tylko opcja **Pokaż okno podglądu.**

![Opcje menedżera pakietów](media/PackageManagerUIOptions.png)

W poniższych sekcjach wyjaśniono te opcje.

### <a name="show-preview-window"></a>Pokaż okno podglądu

Po wybraniu tej opcji w oknie modalnym zostaną wyświetlone zależności wybranego pakietu przed zainstalowaniem pakietu:

![Przykładowe okno dialogowe podglądu](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Opcje instalacji i aktualizacji

(Niedostępne dla wszystkich typów projektów).

**Zachowanie zależności** konfiguruje sposób, w jaki NuGet decyduje, które wersje pakietów zależnych należy zainstalować:

- *Ignoruj zależności* pomija instalowanie żadnych zależności, które zazwyczaj przerywa pakiet jest instalowany.
- *Najniższa* [Domyślna] instaluje zależność z minimalnym numerem wersji, który spełnia wymagania wybranego pakietu podstawowego.
- *Najwyższa poprawka* instaluje wersję z tymi samymi głównymi i pomocniczymi numerami wersji, ale z najwyższą liczbą poprawek. Na przykład, jeśli określono wersję 1.2.2, zostanie zainstalowana najwyższa wersja, która zaczyna się od wersji 1.2
- *Najwyższy Minor* instaluje wersję z tym samym głównym numerem wersji, ale z najwyższą liczbą pomocniczą i numerem poprawki. Jeśli zostanie określona wersja 1.2.2, zostanie zainstalowana najwyższa wersja, która zaczyna się od 1
- *Najwyższa* instaluje najwyższą dostępną wersję pakietu.

**Akcja konfliktu plików** określa, jak NuGet powinien obsługiwać pakiety, które już istnieją w projekcie lub na komputerze lokalnym:

- *Prompt* nakazuje NuGet zapytać, czy zachować lub zastąpić istniejące pakiety.
- *Ignoruj wszystko* nakazuje NuGet pominąć zastępowanie istniejących pakietów.
- *Zastąpienie wszystkie* nakazuje NuGet zastąpić wszystkie istniejące pakiety.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Opcje odinstalowywania

(Niedostępne dla wszystkich typów projektów).

**Usuń zależności:** gdy ta opcja jest zaznaczona, usuwa wszystkie pakiety zależne, jeśli nie są one dostępne w innym miejscu w projekcie.

**Wymuś odinstalowanie, nawet jeśli istnieją zależności od niego:** po wybraniu, odinstalowuje pakiet, nawet jeśli jest nadal odwołuje się w projekcie. Jest to zwykle używane w połączeniu z **Usuń zależności,** aby usunąć pakiet i niezależnie od zależności, które zainstalowano. Użycie tej opcji może jednak prowadzić do przerwanych odwołań w projekcie. W takich przypadkach może być konieczne [ponowne zainstalowanie tych innych pakietów](../consume-packages/reinstalling-and-updating-packages.md).
