---
title: Przewodnik konsoli Menedżera pakietów NuGet
description: Instrukcje dotyczące używania konsoli Menedżera pakietów NuGet w programie Visual Studio do pracy z pakietami.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/23/2018
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 06c525cab2dac61c92c4596533173f1d93493d9a
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817661"
---
# <a name="package-manager-console"></a>Konsola Menedżera pakietów

Konsola Menedżera pakietów NuGet jest wbudowany w program Visual Studio w systemie Windows w wersji 2012 i nowszych. (Nie jest dołączony do programu Visual Studio for Mac lub Visual Studio Code.)

Konsolę pozwala używać [poleceń programu NuGet PowerShell](../tools/powershell-reference.md) można znaleźć, instalowanie, odinstalowywanie oraz aktualizowanie pakietów NuGet. Za pomocą konsoli jest niezbędne w przypadku, gdy interfejsu użytkownika Menedżera pakietów nie umożliwiają wykonać operację. Aby użyć `nuget.exe` poleceń w konsoli, zobacz [przy użyciu nuget.exe interfejsu wiersza polecenia w konsoli](#using-the-nugetexe-cli-in-the-console).

Na przykład Znajdowanie i instalowanie pakietu wykonuje się za pomocą trzy łatwe kroki:

1. Otwórz projekt/rozwiązanie w programie Visual Studio, a następnie otwórz za pomocą konsoli **Narzędzia > Menedżera pakietów NuGet > konsoli Menedżera pakietów** polecenia.

1. Znajdź pakiet, który chcesz zainstalować. Jeśli znasz już to, przejdź do kroku 3.

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. Uruchom polecenie instalacji:

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> Można również wykonać wszystkie operacje, które są dostępne w konsoli za pomocą [interfejsu wiersza polecenia NuGet](../tools/nuget-exe-cli-reference.md). Jednak polecenia konsoli działają w kontekście programu Visual Studio i zapisane projektu/rozwiązania i często osiągnąć więcej niż ich równoważnych poleceń interfejsu wiersza polecenia. Na przykład instalowania pakietu w konsoli dodaje odwołanie do projektu, natomiast polecenia interfejsu wiersza polecenia nie. Z tego powodu deweloperów pracujących w programie Visual Studio zwykle preferowane przy użyciu konsoli do interfejsu wiersza polecenia.

> [!Tip]
> Wiele operacji konsoli zależą od tego, o rozwiązania otwarte w programie Visual Studio o nazwie znanej ścieżce. Jeśli masz niezapisane rozwiązanie lub żadne rozwiązanie, zostanie wyświetlony błąd, "nie jest otwarty lub nie zapisano rozwiązania. Upewnij się, że masz otwarte i zapisane rozwiązanie." Oznacza to, że konsola nie może określić folder rozwiązania. Zapisywanie niezapisane rozwiązanie lub tworzenie i zapisywanie rozwiązanie, jeśli nie masz open, należy rozwiązać problem.

## <a name="opening-the-console-and-console-controls"></a>Otwieranie konsoli i formanty konsoli

1. Otwórz program Visual Studio przy użyciu **Narzędzia > Menedżera pakietów NuGet > konsoli Menedżera pakietów** polecenia. Konsoli jest oknem programu Visual Studio, które mogą być rozmieszczane i znajduje się jednak chcesz (zobacz [dostosowywanie układów okien w programie Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. Domyślnie polecenia konsoli działają z określonego pakietu źródłowego i projektu jako zestaw w formancie w górnej części okna:

    ![Formanty Konsola Menedżera pakietów dla projektów i źródła pakietu](media/PackageManagerConsoleControls1.png)

1. Wybieranie źródła różnych pakietów i/lub projektu zmiany tych wartości domyślnych dla kolejnych poleceń. Aby overrride tych ustawień bez zmiany ustawień domyślnych, większość używanych poleceń obsługiwać `-Source` i `-ProjectName` opcje.

1. Aby zarządzać źródła pakietów, wybierz ikonę Koło zębate. Jest to skrót do **Narzędzia > Opcje > Menedżera pakietów NuGet > źródła pakietów** okno dialogowe zgodnie z opisem na [interfejsu użytkownika Menedżera pakietów](package-manager-ui.md#package-sources) strony. Ponadto kontrolka selektora projektu z prawej strony Czyści zawartość konsoli programu:

    ![Ustawienia konsoli Menedżera pakietów i usuń zaznaczenie formantów](media/PackageManagerConsoleControls2.png)

1. Po prawej stronie przycisku przerwań polecenia długotrwałe. Na przykład uruchomiona `Get-Package -ListAvailable -PageSize 500` listy pierwszych 500 pakietów na domyślne źródło (na przykład nuget.org), co może zająć kilka minut do uruchomienia.

    ![Formant stop Konsola Menedżera pakietów](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>Instalowanie pakietu

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Zobacz [Install-Package](../tools/ps-ref-install-package.md).

Instalowanie pakietu w konsoli wykonuje te same kroki, zgodnie z opisem na [co się stanie po zainstalowaniu pakietu](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), z następującymi dodatkami:

- W konsoli są wyświetlani odpowiednich postanowieniach licencyjnych w jego oknie umowę domyślnych. Jeśli nie akceptujesz postanowień, należy odinstalować pakiet natychmiast.
- Również odwołanie do pakietu są dodawane do pliku projektu i pojawia się w **Eksploratora rozwiązań** w obszarze **odwołania** węzła, musisz zapisać projekt, aby wyświetlić zmiany w pliku projektu bezpośrednio.

## <a name="uninstalling-a-package"></a>Odinstalowywanie pakietu

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

Zobacz [Odinstaluj pakiet](../tools/ps-ref-uninstall-package.md). Użyj [Get-Package](../tools/ps-ref-get-package.md) aby zobaczyć wszystkie pakiety zainstalowane w projekcie domyślnym, aby znaleźć identyfikator.

Odinstalowywanie pakietu wykonuje następujące czynności:

- Usuwa odwołania do pakietu z projektu (i jest używany format niezależnie od zarządzania). Odwołania nie są widoczne w **Eksploratora rozwiązań**. (Konieczne może być ponownie skompilować projekt, aby zobaczyć, usunąć je z **Bin** folderu.)
- Odwraca wszelkie zmiany wprowadzone do `app.config` lub `web.config` Jeśli pakiet został zainstalowany.
- Usuwa wcześniej zainstalowane zależności nie pozostałych pakietów użycie tych zależności.

## <a name="updating-a-package"></a>Aktualizowanie pakietu

```ps
# Checks if there are newer versions available for any installed packages
Get-Package -updates

# Updates a specific package using its identifier, in this case jQuery
Update-Package jQuery

# Update all packages in the project named MyProject (as it appears in Solution Explorer)
Update-Package -ProjectName MyProject

# Update all packages in the solution
Update-Package
```

Zobacz [Get-Package](../tools/ps-ref-get-package.md) i [pakietu aktualizacji](../tools/ps-ref-update-package.md)

## <a name="finding-a-package"></a>Znajdowanie pakietu

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```

Zobacz [Znajdź pakiet](../tools/ps-ref-find-package.md). W programie Visual Studio 2013 lub starszej użyj [Get-Package](../tools/ps-ref-get-package.md) zamiast tego.

## <a name="availability-of-the-console"></a>Dostępność konsoli

W programie Visual Studio 2017 r. NuGet i Menedżer pakietów NuGet są instalowane automatycznie po wybraniu dowolnego. Obciążeń związanych z NET; można także zainstalować go indywidualnie sprawdzając **pojedynczych składników > Code Narzędzia > Menedżera pakietów NuGet** opcji w Instalatorze programu Visual Studio 2017 r.

Ponadto jeśli jest Brak Menedżera pakietów NuGet w programie Visual Studio 2015 i starszych wersji, sprawdź **Narzędzia > rozszerzenia i aktualizacje...**  i wyszukaj rozszerzenie NuGet Package Manager. Jeśli nie możesz użyć Instalatora rozszerzeń programu Visual Studio, możesz pobrać rozszerzenia bezpośrednio z [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).

Konsola Menedżera pakietów nie jest obecnie dostępna w programie Visual Studio dla komputerów Mac. Jednak równoważnych poleceń są dostępne za pośrednictwem [interfejsu wiersza polecenia NuGet](nuget-exe-CLI-reference.md). Visual Studio dla komputerów Mac mają interfejsu użytkownika do zarządzania pakietami NuGet. Zobacz [pakietu w tym NuGet w projekcie](/visualstudio/mac/nuget-walkthrough).

Konsola Menedżera pakietów nie jest uwzględniona w programie Visual Studio Code.

## <a name="extending-the-package-manager-console"></a>Rozszerzanie konsoli Menedżera pakietów

Niektóre pakiety Zainstaluj nowe polecenia konsoli. Na przykład `MvcScaffolding` tworzy poleceń, takich jak `Scaffold` pokazano poniżej, generująca, widoków i kontrolerów ASP.NET MVC:

![Zainstalowanie i używanie MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>Konfigurowanie profilu programu NuGet PowerShell

Profil programu PowerShell pozwala udostępnić najczęściej używanych poleceń tam, gdzie należy użyć programu PowerShell. NuGet obsługuje profil specyficzne dla NuGet zwykle znajdują się w następującej lokalizacji:

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Aby znaleźć profil, wpisz `$profile` w konsoli:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Aby uzyskać więcej informacji, zapoznaj się [Windows PowerShell profile](https://technet.microsoft.com/library/bb613488.aspx).

## <a name="using-the-nugetexe-cli-in-the-console"></a>Przy użyciu nuget.exe interfejsu wiersza polecenia w konsoli programu

Aby [ `nuget.exe` CLI](nuget-exe-cli-reference.md) dostępne w konsoli Menedżera pakietów Zainstaluj [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) pakietu w konsoli:

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
