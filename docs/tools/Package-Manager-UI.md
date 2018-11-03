---
title: Informacje o interfejsie użytkownika Menedżera pakietów NuGet
description: Instrukcje dotyczące używania interfejsu użytkownika Menedżera pakietów NuGet w programie Visual Studio do pracy z pakietami NuGet.
author: karann-msft
ms.author: karann
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 1de6ddeca6295c621a90409807af198bc3c7a068
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981187"
---
# <a name="nuget-package-manager-ui"></a>Interfejs użytkownika Menedżera pakietów NuGet

Interfejs użytkownika Menedżera pakietów NuGet w programie Visual Studio na Windows pozwala na łatwe instalowanie, odinstalowywanie oraz aktualizowanie pakietów NuGet w projektach i rozwiązaniach. Aby w programie Visual Studio dla komputerów Mac, zobacz [pakietu w tym NuGet w projekcie](/visualstudio/mac/nuget-walkthrough). Interfejs użytkownika Menedżera pakietów nie jest uwzględniona w programie Visual Studio Code.

W tym temacie:

- [Znajdowanie i instalowanie pakietu (Karta Przeglądaj)](#finding-and-installing-a-package)
- [Odinstalowywanie pakietu (karta zainstalowane)](#uninstalling-a-package)
- [Aktualizowanie pakietu (karty aktualizacji i zainstalowane)](#updating-a-package) (obejmuje ["Niejawnie odwołuje zestawu SDK" lub "AutoReferenced" wiadomości](#implicit_reference))
- [Zarządzanie pakietami dla rozwiązania](#managing-packages-for-the-solution) (Praca z wieloma projektami w tym samym czasie).
- [Źródła pakietów](#package-sources)
- [Kontrolowanie opcji Menedżera pakietów](#package-manager-options-control)

> [!Note]
> Jeśli masz Brak Menedżera pakietów NuGet w programie Visual Studio 2015, sprawdź **Narzędzia > rozszerzenia i aktualizacje...**  i wyszukaj *Menedżera pakietów NuGet* rozszerzenia. Jeśli nie możesz używać Instalator rozszerzenia programu Visual Studio, należy pobrać rozszerzenia bezpośrednio z [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).
>
> W programie Visual Studio 2017 Menedżer pakietów NuGet i NuGet są instalowane automatycznie z żadną. Obciążenia związane z sieci. Zainstalować osobno, wybierając **poszczególne składniki > Kod Narzędzia > Menedżer pakietów NuGet** opcji w Instalatorze programu Visual Studio 2017.

## <a name="finding-and-installing-a-package"></a>Znajdowanie i instalowanie pakietu

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy opcję **odwołania** lub projektu i wybierz **Zarządzaj pakietami NuGet...** .

    ![Zarządzanie pakietami NuGet w menu](media/ManagePackagesUICommand.png)

1. **Przeglądaj** karcie są wyświetlane według popularności z aktualnie wybranego źródła pakietów (zobacz [pakietu źródeł](#package-sources)). Wyszukiwanie określonego pakietu, korzystając z pola wyszukiwania w lewym górnym rogu. Wybierz pakiet z listy, aby wyświetlić jego informacje, które umożliwia także **zainstalować** przycisk wraz z menu rozwijane wybór wersji.

    ![Zarządzanie karty Przeglądaj, okno dialogowe pakiety NuGet](media/Search.png)

1. Wybierz żądaną wersję z listy rozwijanej i wybierz **zainstalować**. Program Visual Studio instaluje pakiet i jego zależności do projektu. Może zostać wyświetlona prośba o zaakceptowanie postanowień licencyjnych. Po zakończeniu instalacji dodano pakiety są widoczne na **zainstalowane** kartę. Pakiety są również wyszczególnione w **odwołania** węzła Eksploratora rozwiązań, wskazujący, że możesz zapoznać się z nimi w projekcie z `using` instrukcji.

    ![Odwołania w Eksploratorze rozwiązań](media/References.png)

> [!Tip]
> Obejmuje wersje wstępne w wyszukiwaniu i udostępnianie wersji wstępnych w wersji listy rozwijanej, wybierz **Uwzględnij wersję wstępną** opcji.

## <a name="uninstalling-a-package"></a>Odinstalowywanie pakietu

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy opcję **odwołania** lub żądanego projektu i wybierz **Zarządzaj pakietami NuGet...** .
1. Wybierz **zainstalowane** kartę.
1. Wybierz pakiet, aby odinstalować (przy użyciu wyszukiwania, aby filtrować listę, jeśli to konieczne), a następnie wybierz **Odinstaluj**.

    ![Odinstalowywanie pakietu](media/UninstallPackage.png)

1. Należy pamiętać, że **Uwzględnij wersję wstępną** i **źródła pakietu** formanty nie mają zastosowania podczas odinstalowywanie pakietów.

## <a name="updating-a-package"></a>Aktualizowanie pakietu

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy opcję **odwołania** lub żądanego projektu i wybierz **Zarządzaj pakietami NuGet...** . (W projektach witryny sieci web, kliknij prawym przyciskiem myszy **Bin** folderu.)
1. Wybierz **aktualizacje** kartę, aby zobaczyć pakiety, które są dostępne aktualizacje ze źródeł wybranego pakietu. Wybierz **Uwzględnij wersję wstępną** obejmujący pakietów wydań wstępnych, na liście aktualizacji.
1. Wybierz pakiet do aktualizacji, wybierz żądaną wersję z listy rozwijanej po prawej stronie, a następnie wybierz **aktualizacji**.

    ![Aktualizowanie pakietu](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>W przypadku niektórych pakietów **aktualizacji** przycisk jest niedostępny i zostanie wyświetlony komunikat informujący o tym, że odwołuje się do"niejawnie zestawu SDK" (lub "AutoReferenced"). Ten komunikat oznacza, że pakiet jest częścią większej struktury lub zestawu SDK i nie powinny być aktualizowane niezależnie. (Wewnętrznie są oznaczone takie pakiety `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Na przykład `Microsoft.NETCore.App` jest częścią zestawu .NET Core SDK i wersję pakietu nie jest taka sama jak wersja framework środowiska uruchomieniowego używane przez aplikację. Musisz [aktualizacji instalacji platformy .NET Core](https://aka.ms/dotnet-download) można pobrać nowe wersje środowiska uruchomieniowego platformy ASP.NET Core i .NET Core. [Zobacz ten dokument, aby uzyskać więcej informacji na metapakiety platformy .NET Core i przechowywanie wersji](/dotnet/core/packages). Dotyczy to często używane następujące pakiety:
    * Pakiet
    * Microsoft.AspNetCore.App
    * Pakietów Microsoft.NETCore.App
    * NETStandard.Library

    ![Przykład pakietu oznaczenie niejawnie odwołania lub AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. Aby zaktualizować wielu pakietów do ich najnowszych wersji, zaznacz je na liście i wybierz **aktualizacji** przycisk nad listą.
1. Możesz także zaktualizować poszczególnych pakietów, od **zainstalowane** kartę. W tym przypadku szczegóły pakietu obejmują selektor wersji (podlegają **Uwzględnij wersję wstępną** opcja) i **aktualizacji** przycisku.

## <a name="managing-packages-for-the-solution"></a>Zarządzanie pakietami dla rozwiązania

Zarządzanie pakietami dla rozwiązania jest wygodny sposób pracy z wieloma projektami równocześnie.

1. Wybierz **Narzędzia > Menedżer pakietów NuGet > Zarządzaj pakietami NuGet dla rozwiązania...**  menu poleceń, lub kliknij prawym przyciskiem myszy rozwiązanie i wybierz pozycję **Zarządzaj pakietami NuGet...** :

    ![Zarządzaj pakietami NuGet dla rozwiązania](media/ManagePackagesSolutionUICommand.png)

1. Podczas zarządzania pakietami dla rozwiązania, interfejs użytkownika umożliwia Wybierz projekty, których dotyczy operacji:

    ![Selektor projektu podczas zarządzania pakietami dla rozwiązania](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Konsolidacja kartę

Deweloperzy zazwyczaj należy wziąć pod uwagę jej złym zwyczajem korzystają z różnych wersji pakietu NuGet między różnymi projektami w tym samym rozwiązaniu. W przypadku zarządzania pakietami dla rozwiązania udostępnia interfejs użytkownika Menedżera pakietów **Konsolidacja** karty, na którym można łatwo zobaczyć gdzie pakiety z numerami wersji distinct są używane przez różne projekty w rozwiązaniu:

![Karta Konsolidacja interfejsu użytkownika Menedżera pakietów](media/ConsolidateTab.png)

W tym przykładzie projekt ClassLibrary1 jest za pomocą platformy EntityFramework 6.2.0, natomiast ConsoleApp1 jest za pomocą platformy EntityFramework 6.1.0. Aby skonsolidować wersje pakietów, wykonaj następujące czynności:

- Wybierz projekty, które można zaktualizować w liście projektu.
- Wybierz wersję do użycia w tych projektach w **wersji** kontrolki, takiej jak 6.2.0 platformy EntityFramework.
- Wybierz **zainstalować** przycisku.

Menedżer pakietów powoduje zainstalowanie wersji wybranego pakietu do wszystkich wybranych projektów, po upływie których pakiet nie jest już wyświetlany na **Konsolidacja** kartę.

## <a name="package-sources"></a>Źródła pakietów

Aby zmienić źródło, z którego program Visual Studio pobiera pakiety, wybierz jeden z selektora źródła:

![Selektor źródła pakietów w interfejs użytkownika Menedżera pakietów](media/PackageSourceDropDown.png)

Aby zarządzać źródeł pakietów:

1. Wybierz **ustawienia** ikony w Interfejsie użytkownika Menedżera pakietów opisane poniżej, lub użyj **Narzędzia > Opcje** polecenia, a następnie przewiń listę do **Menedżera pakietów NuGet**:

    ![Ikona ustawienia interfejsu użytkownika Menedżera pakietów](media/PackageSourceSettings.png)

1. Wybierz **źródeł pakietów** węzła:

    ![Opcje źródła pakietów](media/options.png)

1. Aby dodać źródła, wybierz **+**, umożliwia edytowanie nazwy, wprowadź adres URL lub ścieżkę w **źródła** sterowania, a następnie wybierz **aktualizacji**. Źródło jest teraz wyświetlany w selektorze listy rozwijanej.
1. Aby zmienić źródło pakietu, należy ją zaznaczyć, dokonaj edycji w **nazwa** i **źródła** pola, a następnie wybierz **aktualizacji**.
1. Aby wyłączyć źródło pakietu, wyczyść pole po lewej stronie nazwy na liście.
1. Aby usunąć źródło pakietu, wybierz ją, a następnie wybierz pozycję **X** przycisku.
1. W górę i w dół przycisków strzałek, aby zmienić kolejność priorytetów źródeł pakietów. Podczas przywracania pakietów w projekcie programu Visual Studio wyszukiwania do tych źródeł w kolejności priorytetu. Aby uzyskać więcej informacji, zobacz [Przywracanie pakietu](../consume-packages/package-restore.md).

> [!Tip]
> Jeśli źródło pakietu pojawi się ponownie po jej usunięciu, mogą być wymienione w poziomie komputera lub użytkownika na poziomie `NuGet.Config` plików. Zobacz [zachowania programu NuGet Konfigurowanie](../consume-packages/configuring-nuget-behavior.md) dla lokalizacji tych plików, następnie usuń źródła przez edycję plików ręcznie lub za pomocą [nuget źródeł polecenia](../tools/nuget-exe-CLI-reference.md).

## <a name="package-manager-options-control"></a>Kontrolowanie opcji Menedżera pakietów

Po wybraniu pakietu interfejsu użytkownika Menedżera pakietów wyświetla mały rozwijania **opcje** kontroli poniżej selektor wersji (tutaj pokazane zarówno zwinięte i rozwinięte). Należy zauważyć, że dla niektórych projektów tylko typy **Pokaż okno podglądu** znajduje się opcja.

![Opcje Menedżera pakietów](media/PackageManagerUIOptions.png)

W poniższych sekcjach opisano te opcje.

### <a name="show-preview-window"></a>Pokaż okno (wersja zapoznawcza)

Po wybraniu modalny Wyświetla które zależności wybranego pakietu przed zainstalowaniem pakietu:

![Przykładowe okno dialogowe z wersji zapoznawczej](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Instalowanie i aktualizowanie opcje

(Niedostępne dla wszystkich typów projektów).

**Zachowanie zależności** konfiguruje się, jak NuGet decyduje, które wersje zależne pakiety do zainstalowania:

- *Ignoruj zależności* pomija instalowanie jakieś zależności, która dzieli zazwyczaj jest zainstalowany pakiet.
- *Najniższy* [domyślnie] instaluje zależność o numerze minimalnej wersji, który spełnia wymagania wybranego pakiet główny.
- *Poprawka najwyższy* powoduje zainstalowanie wersji z takie same numery wersji głównych i pomocniczych, ale najwyższy numer poprawki. Na przykład jeśli określono wersję 1.2.2 następnie najwyższa wersja, która rozpoczyna się od 1.2 zostanie zainstalowany
- *Najwyższy drobnych* powoduje zainstalowanie wersji ten sam główny numer wersji, ale najwyższy numer podrzędny i numer poprawki. Jeśli wersja 1.2.2 jest określona, następnie najwyższa wersja, która rozpoczyna się od 1 zostanie zainstalowany
- *Najwyższy* instaluje najwyższej dostępnej wersji pakietu.

**Plik akcji konflikt** określa sposób obsługi NuGet pakiety, które już istnieją w projekcie lub komputer lokalny:

- *Monituj* powoduje, że rozszerzenie NuGet, aby zadać, czy zachować, czy zastąpić istniejące pakiety.
- *Ignoruj wszystkie* powoduje, że rozszerzenie NuGet, aby pominąć, zastępując istniejące pakiety.
- *Zastąpienie wszystkich* powoduje, że rozszerzenie NuGet, aby zastąpić istniejące pakiety.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Odinstaluj opcje

(Niedostępne dla wszystkich typów projektów).

**Usuń zależności**: po wybraniu usuwa wszelkie zależne pakiety, jeśli są one nie odwoływać się gdzie indziej w projekcie.

**Wymuszaj odinstalowanie nawet, jeśli istnieją zależności na nim**: po wybraniu odinstalowuje pakiet nawet wtedy, gdy nadal jest on przywoływany w projekcie. To jest zwykle używany w połączeniu z **usuwanie zależności** do usunięcia pakietu i niezależnie od zależności ona zainstalowana. Użycie tej opcji może jednak prowadzić do przerwanymi odwołaniami w projekcie. W takich przypadkach może być konieczne [ponownie zainstalować te pakiety innych](../consume-packages/reinstalling-and-updating-packages.md).
