---
title: Instalowanie pakietów NuGet i zarządzanie nimi w programie Visual Studio
description: Instrukcje dotyczące używania interfejsu użytkownika Menedżera pakietów NuGet w programie Visual Studio do pracy z pakietami NuGet.
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
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231010"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a>Instalowanie pakietów i zarządzanie nimi w programie Visual Studio przy użyciu Menedżera pakietów NuGet

Interfejs użytkownika Menedżera pakietów NuGet w programie Visual Studio w systemie Windows umożliwia łatwe instalowanie, Odinstalowywanie i aktualizowanie pakietów NuGet w projektach i rozwiązaniach. Aby zapoznać się z doświadczeniem w Visual Studio dla komputerów Mac, zobacz [dołączanie pakietu NuGet do projektu](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json). Interfejs użytkownika Menedżera pakietów nie jest dołączony do Visual Studio Code.

> [!NOTE]
> Jeśli brakuje Menedżera pakietów NuGet w programie Visual Studio 2015, sprawdź **narzędzia > rozszerzenia i aktualizacje...** , a następnie wyszukaj rozszerzenie *Menedżera pakietów NuGet* . Jeśli nie możesz użyć Instalatora rozszerzeń w programie Visual Studio, Pobierz rozszerzenie bezpośrednio z [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).
>
> Począwszy od programu Visual Studio 2017, NuGet i Menedżer pakietów NuGet są automatycznie instalowane z dowolnymi. Obciążenia związane z usługą SIECIową. Zainstaluj ją oddzielnie, wybierając opcję **> narzędzia kodu > opcji Menedżera pakietów NuGet** w Instalatorze programu Visual Studio.

## <a name="find-and-install-a-package"></a>Znajdowanie i instalowanie pakietu

1. W **Eksplorator rozwiązań**kliknij prawym przyciskiem myszy opcję **odwołania** lub projekt i wybierz polecenie **Zarządzaj pakietami NuGet.**...

    ![Opcja menu Zarządzaj pakietami NuGet](media/ManagePackagesUICommand.png)

1. Na karcie **przeglądanie** są wyświetlane pakiety według popularności z aktualnie wybranego źródła (zobacz [źródła pakietu](#package-sources)). Wyszukaj konkretny pakiet przy użyciu pola wyszukiwania w lewym górnym rogu. Wybierz pakiet z listy, aby wyświetlić jego informacje, które również włącza przycisk **Instaluj** wraz z listą rozwijaną wyboru wersji.

    ![Karta przeglądania okna dialogowego Zarządzanie pakietami NuGet](media/Search.png)

1. Wybierz żądaną wersję z listy rozwijanej i wybierz pozycję **Zainstaluj**. Program Visual Studio instaluje pakiet i jego zależności w projekcie. Może zostać wyświetlony monit o zaakceptowanie postanowień licencyjnych. Po zakończeniu instalacji dodane pakiety pojawiają się na **zainstalowanej** karcie. pakiety są również wymienione w węźle **odwołania** Eksplorator rozwiązań, co oznacza, że można odwołać się do nich w projekcie za pomocą instrukcji `using`.

    ![Odwołania w Eksplorator rozwiązań](media/References.png)

> [!Tip]
> Aby uwzględnić wersje wstępne w wyszukiwaniu i udostępnić wersje wstępne dostępne na liście rozwijanej wersja, wybierz opcję **Uwzględnij wersję wstępną** .

> [!Note]
> Pakiet NuGet ma dwa formaty, w których projekt może używać pakietów: [`PackageReference`](package-references-in-project-files.md) i [`packages.config`](../reference/packages-config.md). Wartość [domyślną można ustawić w oknie Opcje programu Visual Studio](Package-Restore.md#choose-default-package-management-format).

## <a name="uninstall-a-package"></a>Odinstalowywanie pakietu

1. W **Eksplorator rozwiązań**kliknij prawym przyciskiem myszy pozycję **odwołania** lub żądany projekt, a następnie wybierz polecenie **Zarządzaj pakietami NuGet.**...
1. Wybierz kartę **Zainstalowano**.
1. Wybierz pakiet, który ma zostać odinstalowany (za pomocą wyszukiwania, w razie potrzeby odfiltruj listę), a następnie wybierz pozycję **Odinstaluj**.

    ![Odinstalowywanie pakietu](media/UninstallPackage.png)

1. Należy zauważyć, że kontrolki **Uwzględnij wersję wstępną** i **Źródło pakietu** nie mają wpływu na Odinstalowywanie pakietów.

## <a name="update-a-package"></a>Aktualizowanie pakietu

1. W **Eksplorator rozwiązań**kliknij prawym przyciskiem myszy pozycję **odwołania** lub żądany projekt, a następnie wybierz polecenie **Zarządzaj pakietami NuGet.**... (W obszarze projekty witryny sieci Web kliknij prawym przyciskiem myszy folder **bin** ).
1. Wybierz kartę **aktualizacje** , aby zobaczyć pakiety z dostępnymi aktualizacjami z wybranych źródeł pakietów. Wybierz pozycję **Uwzględnij wersję wstępną** , aby uwzględnić pakiety wersji wstępnej na liście aktualizacji.
1. Wybierz pakiet do zaktualizowania, wybierz żądaną wersję z listy rozwijanej po prawej stronie, a następnie wybierz pozycję **Aktualizuj**.

    ![Aktualizowanie pakietu](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>W przypadku niektórych pakietów przycisk **Aktualizuj** jest wyłączony i pojawia się komunikat informujący o tym, że jest to "niejawnie przywoływane przez zestaw SDK" (lub "autoreferencja"). Ten komunikat oznacza, że pakiet jest częścią większej struktury lub zestawu SDK i nie należy go aktualizować niezależnie. (Takie pakiety są wewnętrznie oznaczone `<IsImplicitlyDefined>True</IsImplicitlyDefined>`m). Na przykład `Microsoft.NETCore.App` jest częścią zestaw .NET Core SDK, a wersja pakietu nie jest taka sama jak wersja środowiska uruchomieniowego używanego przez aplikację. Musisz [zaktualizować instalację programu .NET Core](https://aka.ms/dotnet-download) , aby uzyskać nowe wersje ASP.NET Core i środowiska uruchomieniowego platformy .NET Core. [Zapoznaj się z tym dokumentem, aby uzyskać szczegółowe informacje o pakietach i wersjach platformy .NET Core](/dotnet/core/packages). Dotyczy to następujących najczęściej używanych pakietów:
    * Microsoft.AspNetCore.All
    * Microsoft.AspNetCore.App
    * Microsoft.NETCore.App
    * Biblioteka standardowa. Library

    ![Przykładowy pakiet oznaczony jako niejawnie przywoływany lub autoreferencja](media/PackageManagerUIAutoReferenced.png)

1. Aby zaktualizować wiele pakietów do ich najnowszych wersji, zaznacz je na liście i wybierz przycisk **Aktualizuj** nad listą.
1. Możesz również zaktualizować pojedynczy pakiet z karty **zainstalowane** . W takim przypadku szczegóły pakietu obejmują selektor wersji (z opcją **Uwzględnij wersję wstępną** ) i przycisk **Aktualizuj** .

## <a name="manage-packages-for-the-solution"></a>Zarządzaj pakietami dla rozwiązania

Zarządzanie pakietami dla rozwiązania jest wygodnym sposobem pracy z wieloma projektami jednocześnie.

1. Wybierz **narzędzia > Menedżer pakietów nuget > zarządzanie pakietami NuGet dla rozwiązania...** menu, lub kliknij rozwiązanie prawym przyciskiem myszy i wybierz pozycję **Zarządzaj pakietami NuGet...**:

    ![Zarządzaj pakietami NuGet dla rozwiązania](media/ManagePackagesSolutionUICommand.png)

1. Podczas zarządzania pakietami dla rozwiązania interfejs użytkownika umożliwia wybranie projektów, na które mają wpływ operacje:

    ![Selektor projektu podczas zarządzania pakietami dla rozwiązania](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Karta konsolidowanie

Deweloperzy zazwyczaj uważają, że niewłaściwe rozwiązanie do korzystania z różnych wersji tego samego pakietu NuGet w różnych projektach w tym samym rozwiązaniu. W przypadku wybrania opcji zarządzania pakietami dla rozwiązania interfejs użytkownika Menedżera pakietów zawiera kartę **Konsolidacja** , w której można łatwo zobaczyć, gdzie pakiety o różnych numerach wersji są używane przez różne projekty w rozwiązaniu:

![Karta konsolidacja interfejsu użytkownika Menedżera pakietów](media/ConsolidateTab.png)

W tym przykładzie projekt ClassLibrary1 korzysta z EntityFramework 6.2.0, a ConsoleApp1 używa EntityFramework 6.1.0. Aby skonsolidować wersje pakietów, wykonaj następujące czynności:

- Wybierz projekty do zaktualizowania na liście projektów.
- Wybierz wersję, która ma być używana we wszystkich projektach w kontroli **wersji** , np. EntityFramework 6.2.0.
- Wybierz przycisk **Instaluj** .

Menedżer pakietów instaluje wybraną wersję pakietu we wszystkich wybranych projektach, po upływie których pakiet nie jest już wyświetlany na karcie **konsolidowanie** .

## <a name="package-sources"></a>Źródła pakietów

Aby zmienić źródło, z którego program Visual Studio uzyskuje pakiety, wybierz jeden z selektora źródła:

![Selektor źródła pakietu w interfejsie użytkownika Menedżera pakietów](media/PackageSourceDropDown.png)

Aby zarządzać źródłami pakietów:

1. Wybierz ikonę **ustawień** w interfejsie użytkownika Menedżera pakietów przedstawionym poniżej lub użyj **narzędzi > Opcje** i przewiń do **Menedżera pakietów NuGet**:

    ![Ikona ustawień interfejsu użytkownika Menedżera pakietów](media/PackageSourceSettings.png)

1. Wybierz węzeł **źródła pakietów** :

    ![Opcje źródeł pakietów](media/options.png)

1. Aby dodać źródło, wybierz **+**, Edytuj nazwę, wprowadź adres URL lub ścieżkę w kontroli **źródła** , a następnie wybierz pozycję **Aktualizuj**. Źródło zostanie wyświetlone na liście rozwijanej selektora.
1. Aby zmienić źródło pakietu, zaznacz je, wprowadź zmiany w polach **Nazwa** i **Źródło** , a następnie wybierz pozycję **Aktualizuj**.
1. Aby wyłączyć źródło pakietu, wyczyść pole z lewej strony nazwy na liście.
1. Aby usunąć źródło pakietu, zaznacz je, a następnie wybierz przycisk **X** .
1. Używanie przycisków strzałek w górę i w dół nie zmienia kolejności priorytetów źródeł pakietów. Program Visual Studio ignoruje kolejność źródeł pakietów przy użyciu pakietu z dowolnego źródła jest najpierw odpowiedzi na żądania. Aby uzyskać więcej informacji, zobacz [przywracanie pakietu](../consume-packages/package-restore.md).

> [!Tip]
> Jeśli źródło pakietu zostanie ponownie wyświetlone po jego usunięciu, może ono znajdować się na liście plików `NuGet.Config` na poziomie komputera lub użytkownika. Zapoznaj się z [typowymi konfiguracjami NuGet](../consume-packages/configuring-nuget-behavior.md) dla lokalizacji tych plików, a następnie Usuń źródło, edytując pliki ręcznie lub używając [polecenia źródła NuGet](../reference/nuget-exe-CLI-reference.md).

## <a name="package-manager-options-control"></a>Kontrola opcji Menedżera pakietów

Po wybraniu pakietu interfejs użytkownika Menedżera pakietów wyświetla małą, rozwijalną kontrolkę **opcji** poniżej selektora wersji (pokazanej w tym miejscu: zwinięte i rozwinięte). Należy pamiętać, że w przypadku niektórych typów projektów dostępna jest tylko opcja **Pokaż podgląd okna** .

![Opcje Menedżera pakietów](media/PackageManagerUIOptions.png)

W poniższych sekcjach opisano te opcje.

### <a name="show-preview-window"></a>Pokaż okno podglądu

Po wybraniu okno modalne wyświetla zależności wybranego pakietu przed zainstalowaniem pakietu:

![Przykładowe okno dialogowe podglądu](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Opcje instalacji i aktualizacji

(Niedostępne dla wszystkich typów projektów).

**Zachowanie zależności** konfiguruje sposób, w jaki pakiet NuGet decyduje, które wersje pakietów zależnych zainstalować:

- *Ignorowanie zależności* powoduje pominięcie instalacji wszelkich zależności, które zwykle przerywa instalację pakietu.
- *Najniższy* [domyślnie] instaluje zależność z minimalnym numerem wersji, który spełnia wymagania głównego wybranego pakietu.
- *Najwyższa poprawka* instaluje wersję z tymi samymi głównymi i pomocniczymi numerami wersji, ale najwyższa numer poprawki. Na przykład jeśli zostanie określona wersja 1.2.2, zostanie zainstalowana najwyższa wersja, która rozpoczyna się od 1,2
- *Największa drobna* instaluje wersję z tym samym głównym numerem wersji, ale z najwyższym numerem i numerem poprawki. Jeśli zostanie określona wersja 1.2.2, zostanie zainstalowana najwyższa wersja, która rozpoczyna się od 1
- *Najwyższa* instalacja jest najwyższa dostępna wersja pakietu.

**Akcja konfliktu plików** określa, jak NuGet powinien obsługiwać pakiety, które już istnieją w projekcie lub na komputerze lokalnym:

- *Monit* instruuje pakiet NuGet, aby poprosił o zachowanie lub zastąpienie istniejących pakietów.
- *Zignoruj wszystkie* instruuje pakiet NuGet, aby pominąć zastępowanie wszystkich istniejących pakietów.
- Polecenie *overwrite All* instruuje pakiet NuGet, aby zastąpić wszystkie istniejące pakiety.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Opcje dezinstalacji

(Niedostępne dla wszystkich typów projektów).

**Usuń zależności**: po zaznaczeniu usuwa wszystkie zależne pakiety, jeśli nie są one przywoływane w innym miejscu w projekcie.

**Wymuś dezinstalację, nawet jeśli istnieją zależności**: w przypadku wybrania tej funkcji program Odinstalowuje pakiet nawet wtedy, gdy jest on nadal przywoływany w projekcie. Jest to zwykle używane w połączeniu z **usuwaniem zależności** w celu usunięcia pakietu i wszelkich zależnych od niego zależności. Użycie tej opcji może jednak prowadzić do przerwania odwołań w projekcie. W takich przypadkach może być konieczne [ponowne zainstalowanie tych innych pakietów](../consume-packages/reinstalling-and-updating-packages.md).
