---
title: "Przewodnik konsoli Menedżera pakietów NuGet | Dokumentacja firmy Microsoft"
author: kraigb
hms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
f1_keywords:
- vs.nuget.packagemanager.console
description: "Instrukcje dotyczące używania konsoli Menedżera pakietów NuGet w programie Visual Studio do pracy z pakietami."
keywords: "Konsoli Menedżera pakietów NuGet, programu NuGet powershell zarządzać pakietami NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 60c7edd0497e162cc511424e9acfbbfd6f53fd46
ms.sourcegitcommit: a40a6ce6897b2d9411397b2e29b1be234eb6e50c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/27/2018
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

Instalowanie pakietu wykonuje następujące czynności:

- Wyświetla odpowiednich postanowieniach licencyjnych w oknie konsoli umowę domyślnych. Jeśli nie akceptujesz postanowień, należy odinstalować pakiet natychmiast.
- Dodaje odwołanie do projektu w dowolnie wybrany format odwołania jest w użyciu. Następnie odwołania są wyświetlane w Eksploratorze rozwiązań i plik formatu dotyczy odwołanie. Należy jednak pamiętać, że z PackageReference, należy zapisać projekt, aby wyświetlić zmiany w pliku projektu bezpośrednio.
- Buforuje pakietu:
  - PackageReference: pakiet zostanie zbuforowana w `%USERPROFILE%\.nuget\packages` i blokady pliku, np. `project.assets.json` jest aktualizowany.
  - `packages.config`: tworzy `packages` folder główny rozwiązania i kopie do podfolderu w nim pliki pakietu. `package.config` Plik został zaktualizowany.
- Aktualizacje `app.config` i/lub `web.config` Jeśli pakiet używa [źródła i konfiguracji pliku przekształcenia](../create-packages/source-and-config-file-transformations.md).
- Instaluje wszystkie zależności, jeśli jeszcze nie istnieje w projekcie. To może zaktualizować wersje pakietu w procesie, zgodnie z opisem w [rozpoznawania zależności](../consume-packages/dependency-resolution.md).
- Wyświetla plik readme pakietu, jeśli są dostępne w oknie programu Visual Studio.

> [!Tip]
> Jedną z zalet głównej instalowania pakietów z `Install-Package` polecenie w konsoli jest, który dodaje odwołanie do projektu, podobnie jak w przypadku korzystania z interfejsu użytkownika Menedżera pakietów. Z kolei `nuget install` tylko pliki do pobrania pakietu polecenia interfejsu wiersza polecenia i nie powoduje automatycznego dodania odwołania.

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

- Usuwa odwołania do pakietu z projektu (i jest używany format niezależnie od odwołania). Odwołania nie są widoczne w Eksploratorze rozwiązań. (Konieczne może być ponownie skompilować projekt, aby zobaczyć, usunąć je z **Bin** folderu.)
- Odwraca wszelkie zmiany wprowadzone do `app.config` lub `web.config` Jeśli pakiet został zainstalowany.
- Usuwa wcześniej zainstalowane zależności nie pozostałych pakietów użycie tych zależności.

> [!Tip]
> Podobnie jak `Install-Package`, `Uninstall-Package` polecenie ma zaletą Zarządzanie odwołaniami w projekcie, w odróżnieniu od `nuget uninstall` polecenia interfejsu wiersza polecenia.

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

Ponadto jeśli jest Brak Menedżera pakietów NuGet w programie Visual Studio 2015 i starszych wersji, sprawdź **Narzędzia > rozszerzenia i aktualizacje...**  i wyszukaj rozszerzenie NuGet Package Manager. Jeśli nie możesz użyć Instalatora rozszerzeń programu Visual Studio, możesz pobrać rozszerzenia bezpośrednio z [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).

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
