---
title: Instalowanie pakietów NuGet przy użyciu konsoli przy użyciu konsoli i zarządzanie nimi
description: Instrukcje dotyczące korzystania z konsoli Menedżera pakietów NuGet w programie Visual Studio do pracy z pakietami.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 42031f7b5fe4d3c1b4dbe5e1bfbf9197014e0e88
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428955"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a>Instalowanie pakietów i zarządzanie nimi za pomocą konsoli Menedżera pakietów w programie Visual Studio (PowerShell)

Konsola Menedżera pakietów NuGet umożliwia znajdowanie, instalowanie, odinstalowywanie i aktualizowanie pakietów NuGet za pomocą [poleceń NuGet PowerShell.](../reference/powershell-reference.md) Korzystanie z konsoli jest konieczne w przypadkach, gdy interfejs użytkownika Menedżera pakietów nie zapewnia sposobu wykonania operacji. Aby `nuget.exe` użyć poleceń interfejsu wiersza polecenia w konsoli, zobacz [Korzystanie z interfejsu wiersza polecenia nuget.exe w konsoli](#use-the-nugetexe-cli-in-the-console).

Konsola jest wbudowana w program Visual Studio w systemie Windows. Nie jest dołączony do programu Visual Studio dla komputerów Mac lub Visual Studio Code.

## <a name="find-and-install-a-package"></a>Znajdowanie i instalowanie pakietu

Na przykład znalezienie i zainstalowanie pakietu odbywa się za pomocą trzech prostych kroków:

1. Otwórz projekt/rozwiązanie w programie Visual Studio i otwórz konsolę za pomocą polecenia **Narzędzia > Menedżera pakietów NuGet > konsoli Menedżera pakietów.**

1. Znajdź pakiet, który chcesz zainstalować. Jeśli już to wiesz, przejdź do kroku 3.

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
> Wszystkie operacje, które są dostępne w konsoli można również wykonać za pomocą [NuGet CLI](../reference/nuget-exe-cli-reference.md). Jednak polecenia konsoli działają w kontekście programu Visual Studio i zapisanego projektu/rozwiązania i często osiągają więcej niż ich równoważne polecenia interfejsu wiersza polecenia. Na przykład zainstalowanie pakietu za pośrednictwem konsoli dodaje odwołanie do projektu, podczas gdy polecenie CLI nie. Z tego powodu deweloperzy pracujący w programie Visual Studio zazwyczaj wolą używać konsoli do interfejsu wiersza polecenia.

> [!Tip]
> Wiele operacji konsoli zależy od konieczności rozwiązania otwartego w programie Visual Studio o znanej nazwie ścieżki. Jeśli masz niezapisane rozwiązanie lub nie ma rozwiązania, możesz zobaczyć błąd " Rozwiązanie nie jest otwarte lub nie zapisane. Upewnij się, że masz otwarte i zapisane rozwiązanie." Oznacza to, że konsola nie może określić folderu rozwiązania. Zapisanie niezapisanego rozwiązania lub utworzenie i zapisanie rozwiązania, jeśli nie masz otwartego rozwiązania, powinno poprawić błąd.

## <a name="opening-the-console-and-console-controls"></a>Otwieranie elementów sterujących konsoli i konsoli

1. Otwórz konsolę w programie Visual Studio za pomocą polecenia **Narzędzia > Menedżer pakietów NuGet > konsoli Menedżera pakietów.** Konsola jest oknem programu Visual Studio, które można rozmieszczać i pozycjonować w jak sposób (zobacz [Dostosowywanie układów okien w programie Visual Studio).](/visualstudio/ide/customizing-window-layouts-in-visual-studio)

1. Domyślnie polecenia konsoli działają względem określonego źródła pakietu i projektu zgodnie z ustawieniem w formancie w górnej części okna:

    ![Formanty konsoli Menedżera pakietów dla źródła i projektu pakietu](media/PackageManagerConsoleControls1.png)

1. Wybranie innego źródła pakietu i/lub projektu powoduje zmianę tych wartości domyślnych dla kolejnych poleceń. Aby przecenić te ustawienia bez zmiany ustawień `-Source` `-ProjectName` domyślnych, większość poleceń obsługuje i opcje.

1. Aby zarządzać źródłami pakietów, wybierz ikonę koła zębatego. Jest to skrót do **narzędzia > opcje > NuGet Package Manager > źródła pakietów,** jak opisano na stronie interfejsu użytkownika Menedżera [pakietów.](install-use-packages-visual-studio.md#package-sources) Ponadto kontrolka po prawej stronie selektora projektu czyści zawartość konsoli:

    ![Ustawienia konsoli Menedżera pakietów i wyczyść kontrolki](media/PackageManagerConsoleControls2.png)

1. Przycisk po prawej stronie przerywa długotrwałe polecenie. Na przykład `Get-Package -ListAvailable -PageSize 500` uruchomione wyświetla listę 500 najlepszych pakietów w źródle domyślnym (na przykład nuget.org), co może potrwać kilka minut.

    ![Kontrola zatrzymania konsoli menedżera pakietów](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a>Instalowanie pakietu

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Zobacz [Install-Package](../reference/ps-reference/ps-ref-install-package.md).

Instalowanie pakietu w konsoli wykonuje te same kroki, co opisano w [sprawie Co się dzieje, gdy pakiet jest zainstalowany,](../concepts/package-installation-process.md)z następującymi dodatkami:

- Konsola wyświetla odpowiednie postanowienia licencyjne w swoim oknie z dorozumianą umową. Jeśli nie zgadzasz się na warunki, powinieneś natychmiast odinstalować pakiet.
- Również odwołanie do pakietu jest dodawany do pliku projektu i pojawia się w **Eksploratorze rozwiązań** w **węźle Odwołania,** należy zapisać projekt, aby zobaczyć zmiany w pliku projektu bezpośrednio.

## <a name="uninstall-a-package"></a>Odinstalowywanie pakietu

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

Zobacz [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md). Użyj [Get-Package,](../reference/ps-reference/ps-ref-get-package.md) aby wyświetlić wszystkie pakiety aktualnie zainstalowane w projekcie domyślnym, jeśli trzeba znaleźć identyfikator.

Odinstalowanie pakietu wykonuje następujące czynności:

- Usuwa odwołania do pakietu z projektu (i niezależnie od formatu zarządzania jest w użyciu). Odwołania nie są już wyświetlane w **Eksploratorze rozwiązań**. (Może być konieczne odbudowycie projektu, aby został usunięty z folderu **Bin).**
- Odwraca wszelkie zmiany `app.config` wprowadzone `web.config` do lub gdy pakiet został zainstalowany.
- Usuwa wcześniej zainstalowane zależności, jeśli żadne pozostałe pakiety nie używają tych zależności.

## <a name="update-a-package"></a>Aktualizowanie pakietu

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

Zobacz [Get-Package](../reference/ps-reference/ps-ref-get-package.md) i [Update-Package](../reference/ps-reference/ps-ref-update-package.md)

## <a name="find-a-package"></a>Znajdź pakiet

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

Zobacz [Znajdź pakiet](../reference/ps-reference/ps-ref-find-package.md). W programie Visual Studio 2013 i wcześniejszych należy użyć [get-package](../reference/ps-reference/ps-ref-get-package.md) zamiast tego.

## <a name="availability-of-the-console"></a>Dostępność konsoli

Począwszy od programu Visual Studio 2017, NuGet i Menedżer pakietów NuGet są instalowane automatycznie po wybraniu dowolnego . Obciążenia związane z siecią net; można również zainstalować go indywidualnie, sprawdzając poszczególne składniki > Narzędzia kodu > menedżer **pakietów NuGet** w instalatorze programu Visual Studio.

Ponadto jeśli brakuje Menedżera pakietów NuGet w programie Visual Studio 2015 i wcześniejszych, sprawdź **Narzędzia > rozszerzenia i aktualizacje...** i wyszukaj rozszerzenie Menedżera pakietów NuGet. Jeśli nie możesz użyć instalatora rozszerzeń w programie Visual Studio, [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)możesz pobrać je bezpośrednio z programu .

Konsola Menedżera pakietów nie jest obecnie dostępna w programie Visual Studio dla komputerów Mac. Równoważne polecenia są jednak dostępne za pośrednictwem [interfejsu wiersza polecenia NuGet.](../reference/nuget-exe-CLI-reference.md) Visual Studio dla komputerów Mac ma interfejs użytkownika do zarządzania pakietami NuGet. Zobacz [Dołączanie pakietu NuGet w projekcie](/visualstudio/mac/nuget-walkthrough).

Konsola Menedżera pakietów nie jest dołączona do programu Visual Studio Code.

## <a name="extend-the-package-manager-console"></a>Rozszerzanie konsoli Menedżera pakietów

Niektóre pakiety instalują nowe polecenia dla konsoli. Na przykład `MvcScaffolding` tworzy polecenia, takie jak `Scaffold` pokazano poniżej, który generuje ASP.NET kontrolerów MVC i widoków:

![Instalacja i używanie rusztowania MvcS](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a>Konfigurowanie profilu programu NuGet PowerShell

Profil programu PowerShell umożliwia udostępnianie często używanych poleceń wszędzie tam, gdzie jest używany program PowerShell. NuGet obsługuje profil specyficzne dla NuGet zazwyczaj znajduje się w następującej lokalizacji:

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Aby znaleźć profil, `$profile` wpisz w konsoli:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Aby uzyskać więcej informacji, zobacz [Profile programu Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).

## <a name="use-the-nugetexe-cli-in-the-console"></a>Użyj interfejsu wiersza polecenia nuget.exe w konsoli

Aby udostępnić [ `nuget.exe` wiersz polecenia](../reference/nuget-exe-cli-reference.md) w konsoli Menedżera pakietów, zainstaluj pakiet [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) z konsoli:

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
