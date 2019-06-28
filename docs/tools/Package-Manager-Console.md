---
title: Instalowanie i Zarządzaj pakietami NuGet w programie Visual Studio przy użyciu programu PowerShell
description: Instrukcje dotyczące korzystania z konsoli Menedżera pakietów NuGet w programie Visual Studio do pracy z pakietami.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 11ec25598d3110ba84dec5044642e205e13346af
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426219"
---
# <a name="install-and-manage-packages-using-powershell-in-visual-studio"></a>Instalowanie i zarządzania pakietami przy użyciu programu PowerShell w programie Visual Studio

Konsola Menedżera pakietów NuGet umożliwia korzystanie z [poleceń programu NuGet PowerShell](../tools/powershell-reference.md) można znaleźć, instalowanie, odinstalowywanie oraz aktualizowanie pakietów NuGet. Za pomocą konsoli jest konieczne w przypadku, gdy interfejs użytkownika Menedżera pakietów nie zapewnia sposób wykonania operacji. Aby użyć `nuget.exe` poleceń interfejsu wiersza polecenia w konsoli, zobacz [przy użyciu nuget.exe interfejsu wiersza polecenia w konsoli](#using-the-nugetexe-cli-in-the-console).

Konsoli jest wbudowana w programie Visual Studio na Windows. Nie jest uwzględniona w programie Visual Studio for Mac lub Visual Studio Code.

## <a name="find-and-install-a-package"></a>Znajdowanie i instalowanie pakietu

Na przykład Znajdowanie i instalowanie pakietu jest przeprowadzane za pomocą trzech prostych krokach:

1. Otwórz projekt/rozwiązanie w programie Visual Studio i Otwórz za pomocą konsoli **Narzędzia > Menedżer pakietów NuGet > Konsola Menedżera pakietów** polecenia.

1. Znajdź pakiet, który chcesz zainstalować. Jeśli znasz już to, przejdź do kroku 3.

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. Uruchom polecenia instalacji:

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> Można również wykonać wszystkie operacje, które są dostępne w konsoli za pomocą [interfejs wiersza polecenia NuGet](../tools/nuget-exe-cli-reference.md). Jednak polecenia konsoli działają w kontekście programu Visual Studio i zapisany projekt/rozwiązanie i często osiągnąć bardziej niż ich równoważne poleceń interfejsu wiersza polecenia. Na przykład instalowanie pakietu za pomocą konsoli dodaje odwołanie do projektu, natomiast nie obsługuje polecenia interfejsu wiersza polecenia. Z tego powodu deweloperzy pracujący w programie Visual Studio zazwyczaj preferują przy użyciu konsoli dla interfejsu wiersza polecenia.

> [!Tip]
> Wiele operacji konsoli zależą od tego, rozwiązanie otwarte w programie Visual Studio o nazwie znanej ścieżce. Jeśli masz niezapisane rozwiązanie lub żadne rozwiązanie nie zostanie wyświetlony błąd, "rozwiązania nie otwarcie lub nie zostały zapisane. Upewnij się, że masz rozwiązanie otwarty i zapisany." Oznacza to, że konsoli nie można ustalić folderu rozwiązania. Zapisywanie niezapisane rozwiązanie lub tworzenie i zapisywanie rozwiązania, jeśli nie masz otwarte, należy rozwiązać problem.

## <a name="opening-the-console-and-console-controls"></a>Otwieranie konsoli i formanty konsoli

1. Otwórz konsolę programu Visual Studio przy użyciu **Narzędzia > Menedżer pakietów NuGet > Konsola Menedżera pakietów** polecenia. Konsola jest okno programu Visual Studio, które mogą być ułożone umieszczony w dowolny sposób (zobacz [dostosowywanie układów okien w programie Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. Domyślnie polecenia konsoli działają względem źródła określonego pakietu i projektu jako zestawu w formancie w górnej części okna:

    ![Formanty Konsola Menedżera pakietów dla projektów i źródła pakietu](media/PackageManagerConsoleControls1.png)

1. Wybór źródła pakietu inny projekt i/lub zmienia te ustawienia domyślne używane przy kolejnych poleceniach. Aby overrride tych ustawień bez zmiany ustawień domyślnych, większość używanych poleceń obsługiwać `-Source` i `-ProjectName` opcje.

1. Aby zarządzać źródła pakietu, wybierz ikonę koła zębatego. Jest to skrót do **Narzędzia > Opcje > Menedżer pakietów NuGet > źródeł pakietów** okno dialogowe, zgodnie z opisem na [interfejs użytkownika Menedżera pakietów](package-manager-ui.md#package-sources) strony. Ponadto kontrolka selektora projektów po prawej stronie Czyści zawartość konsoli programu:

    ![Ustawienia konsoli Menedżera pakietów i wyczyść formantów](media/PackageManagerConsoleControls2.png)

1. Po prawej stronie przycisku przerywa działanie polecenia długoterminowych. Aby na przykład uruchomić `Get-Package -ListAvailable -PageSize 500` zawiera listę pakietów pierwszych 500 na domyślnego źródła (np. nuget.org), który może potrwać kilka minut.

    ![Kontrolka stop Konsola Menedżera pakietów](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>Instalowanie pakietu

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Zobacz [Install-Package](../tools/ps-ref-install-package.md).

Instalowanie pakietu w konsoli wykonuje te same czynności, zgodnie z opisem na [co się dzieje po zainstalowaniu pakietu](../concepts/package-installation-process.md), z następującymi dodatkami:

- Konsoli są wyświetlane w odpowiednich postanowieniach licencyjnych w jego oknie dorozumianych umowy. Jeśli nie akceptujesz postanowień, należy odinstalować pakiet natychmiast.
- Również odwołanie do pakietu są dodawane do pliku projektu i pojawia się w **Eksploratora rozwiązań** w obszarze **odwołania** węzła, musisz zapisać projekt, aby zobaczyć zmiany w pliku projektu bezpośrednio.

## <a name="uninstalling-a-package"></a>Odinstalowywanie pakietu

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

Zobacz [Odinstaluj pakiet](../tools/ps-ref-uninstall-package.md). Użyj [Get-Package](../tools/ps-ref-get-package.md) aby zobaczyć wszystkie pakiety, które obecnie zainstalowana na projekt domyślny, jeśli chcesz znaleźć identyfikatora.

Odinstalowywanie pakietu wykonuje następujące czynności:

- Usuwa odwołania do pakietu z projektu (i jest używany format niezależnie od zarządzania). Odwołania nie są wyświetlane w **Eksploratora rozwiązań**. (Może być konieczne ponownie skompiluj projekt, aby zobaczyć, że usuwane z **Bin** folderu.)
- Odwraca wszelkie zmiany wprowadzone do `app.config` lub `web.config` gdy pakiet został zainstalowany.
- Zależności usuwa wcześniej zainstalowane nie pozostałe pakiety użycia tych zależności.

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

Zobacz [Get-Package](../tools/ps-ref-get-package.md) i [pakiet aktualizacji](../tools/ps-ref-update-package.md)

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

Zobacz [Znajdź pakiet](../tools/ps-ref-find-package.md). W programie Visual Studio 2013 i starszych, użyj [Get-Package](../tools/ps-ref-get-package.md) zamiast tego.

## <a name="availability-of-the-console"></a>Dostępność w konsoli programu

Począwszy od programu Visual Studio 2017, Menedżer pakietów NuGet i NuGet są automatycznie instalowane po zaznaczeniu innego. Obciążenia związane z NET; można także zainstalować je oddzielnie, sprawdzając **poszczególne składniki > Kod Narzędzia > Menedżer pakietów NuGet** opcji w Instalatorze programu Visual Studio.

Ponadto jeśli masz Brak Menedżera pakietów NuGet w programie Visual Studio 2015 i starszych, sprawdź **Narzędzia > rozszerzenia i aktualizacje...**  i wyszukaj rozszerzenia Menedżera pakietów NuGet. Jeśli nie możesz używać Instalator rozszerzenia programu Visual Studio, możesz pobrać rozszerzenia bezpośrednio z [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).

Konsola Menedżera pakietów nie jest obecnie dostępne w programie Visual Studio dla komputerów Mac. Równoważne polecenia są jednak dostępne za pośrednictwem [interfejs wiersza polecenia NuGet](nuget-exe-CLI-reference.md). Program Visual Studio for Mac ma interfejs użytkownika zarządzania pakietami NuGet. Zobacz [pakietu w tym NuGet w projekcie](/visualstudio/mac/nuget-walkthrough).

Konsola Menedżera pakietów nie jest uwzględniona w programie Visual Studio Code.

## <a name="extending-the-package-manager-console"></a>Rozszerzanie Konsola Menedżera pakietów

Niektóre pakiety instalują nowe polecenia do konsoli. Na przykład `MvcScaffolding` tworzy poleceń, takich jak `Scaffold` pokazano poniżej, które mają widoków i kontrolerów platformy ASP.NET MVC:

![Zainstalowanie i używanie MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>Konfigurowanie profilu NuGet programu PowerShell

Profil programu PowerShell umożliwia udostępnianie często używanych poleceń w dowolnym miejscu przy użyciu programu PowerShell. NuGet obsługuje profilu specyficzne dla NuGet, zwykle znajdują się w następującej lokalizacji:

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Aby znaleźć profilu, wpisz `$profile` w konsoli:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Aby uzyskać więcej informacji, zapoznaj się [programu Windows PowerShell profile](https://technet.microsoft.com/library/bb613488.aspx).

## <a name="using-the-nugetexe-cli-in-the-console"></a>Za pomocą nuget.exe interfejsu wiersza polecenia w konsoli programu

Zapewnienie [ `nuget.exe` interfejsu wiersza polecenia](nuget-exe-cli-reference.md) dostępne w konsoli Menedżera pakietów Zainstaluj [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) pakietu z poziomu konsoli:

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
