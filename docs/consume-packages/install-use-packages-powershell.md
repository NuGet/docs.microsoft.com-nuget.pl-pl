---
title: Instalowanie pakietów NuGet i zarządzanie nimi przy użyciu konsoli programu Visual Studio
description: Instrukcje dotyczące korzystania z konsoli Menedżera pakietów NuGet w programie Visual Studio do pracy z pakietami.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 42031f7b5fe4d3c1b4dbe5e1bfbf9197014e0e88
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428955"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a>Instalowanie pakietów i zarządzanie nimi za pomocą konsoli Menedżera pakietów w programie Visual Studio (PowerShell)

Konsola Menedżera pakietów NuGet umożliwia używanie [poleceń programu PowerShell NuGet](../reference/powershell-reference.md) do znajdowania, instalowania, odinstalowywania i aktualizowania pakietów NuGet. Korzystanie z konsoli programu jest niezbędne w przypadkach, gdy interfejs użytkownika Menedżera pakietów nie zapewnia sposobu wykonywania operacji. Aby użyć poleceń interfejsu wiersza polecenia `nuget.exe` w konsoli programu, zobacz [using the NuGet. exe CLI w konsoli programu](#use-the-nugetexe-cli-in-the-console).

Konsola programu jest wbudowana w program Visual Studio w systemie Windows. Nie jest on dołączony do Visual Studio dla komputerów Mac ani Visual Studio Code.

## <a name="find-and-install-a-package"></a>Znajdowanie i instalowanie pakietu

Na przykład wyszukiwanie i instalowanie pakietu odbywa się z trzema prostymi krokami:

1. Otwórz projekt/rozwiązanie w programie Visual Studio i Otwórz konsolę przy użyciu **narzędzi > Menedżer pakietów NuGet > polecenie konsoli Menedżera pakietów** .

1. Znajdź pakiet, który chcesz zainstalować. Jeśli już wiesz, przejdź do kroku 3.

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
> Wszystkie operacje, które są dostępne w konsoli programu, można również wykonać przy użyciu [interfejsu wiersza polecenia NuGet](../reference/nuget-exe-cli-reference.md). Jednak polecenia konsoli działają w kontekście programu Visual Studio i zapisanego projektu/rozwiązania i często wykonują więcej niż odpowiadające im polecenia interfejsu CLI. Na przykład zainstalowanie pakietu za pomocą konsoli programu dodaje odwołanie do projektu, podczas gdy polecenie interfejsu wiersza polecenia nie jest. Z tego powodu deweloperzy pracujący w programie Visual Studio zwykle preferują korzystanie z konsoli programu z interfejsem wiersza polecenia.

> [!Tip]
> Wiele operacji konsoli jest zależne od tego, czy rozwiązanie zostało otwarte w programie Visual Studio o znanej nazwie ścieżki. Jeśli masz niezapisane rozwiązanie lub nie masz rozwiązania, zobaczysz błąd, "rozwiązanie nie jest otwarte lub nie zostało zapisane. Upewnij się, że masz otwarte i zapisane rozwiązanie ". Oznacza to, że konsola nie może określić folderu rozwiązania. Podczas zapisywania niezapisanego rozwiązania lub tworzenia i zapisywania rozwiązania, jeśli nie masz otwartego, należy usunąć ten błąd.

## <a name="opening-the-console-and-console-controls"></a>Otwieranie konsoli programu i kontrolek konsoli

1. Otwórz konsolę programu Visual Studio przy użyciu **narzędzi > Menedżer pakietów NuGet > polecenie konsoli Menedżera pakietów** . Konsola programu jest oknem programu Visual Studio, które można odpowiednio rozmieścić i umieścić (zobacz [Dostosowywanie układów okien w programie Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. Domyślnie polecenia konsoli działają względem określonego źródła pakietu i projektu ustawionego w kontrolce w górnej części okna:

    ![Formanty konsoli Menedżera pakietów dla źródła i projektu pakietu](media/PackageManagerConsoleControls1.png)

1. Wybranie innego źródła pakietu i/lub projektu powoduje zmianę ustawień domyślnych dla kolejnych poleceń. Aby overrride te ustawienia bez zmiany wartości domyślnych, większość poleceń obsługuje opcje `-Source` i `-ProjectName`.

1. Aby zarządzać źródłami pakietów, wybierz ikonę koła zębatego. Jest to skrót do **narzędzi > opcje > Menedżer pakietów NuGet > źródłami pakietów** , zgodnie z opisem na stronie [interfejsu użytkownika Menedżera pakietów](install-use-packages-visual-studio.md#package-sources) . Ponadto kontrolka z prawej strony selektora projektu czyści zawartość konsoli:

    ![Ustawienia konsoli Menedżera pakietów i wyczyść kontrolki](media/PackageManagerConsoleControls2.png)

1. Prawy przycisk przerywa wykonywanie długotrwałych poleceń. Na przykład uruchomienie `Get-Package -ListAvailable -PageSize 500` zawiera listę najważniejszych pakietów 500 dla domyślnego źródła (na przykład nuget.org), co może potrwać kilka minut.

    ![Sterowanie zatrzymaniem konsoli Menedżera pakietów](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a>Zainstaluj pakiet

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Zobacz [install-package](../reference/ps-reference/ps-ref-install-package.md).

Zainstalowanie pakietu w konsoli programu wykonuje te same czynności, co opisane w temacie [co się stanie w przypadku zainstalowania pakietu](../concepts/package-installation-process.md), z następującymi dodatkami:

- W oknie konsoli zostaną wyświetlone odpowiednie postanowienia licencyjne. Jeśli nie akceptujesz warunków, należy odinstalować pakiet natychmiast.
- Odwołanie do pakietu jest również dodawane do pliku projektu i pojawia się w **Eksplorator rozwiązań** w węźle **odwołania** , należy zapisać projekt, aby wyświetlić zmiany w pliku projektu bezpośrednio.

## <a name="uninstall-a-package"></a>Odinstalowywanie pakietu

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

Zobacz [odinstalowywanie pakietu](../reference/ps-reference/ps-ref-uninstall-package.md). Użyj [Get-Package](../reference/ps-reference/ps-ref-get-package.md) , aby zobaczyć wszystkie pakiety aktualnie zainstalowane w domyślnym projekcie, jeśli trzeba znaleźć identyfikator.

Odinstalowywanie pakietu wykonuje następujące czynności:

- Usuwa odwołania do pakietu z projektu (wraz z dowolnym formatem zarządzania jest używany). Odwołania nie są już wyświetlane w **Eksplorator rozwiązań**. (Może być konieczne ponowne skompilowanie projektu, aby zobaczyć, że został usunięty z folderu **bin** ).
- Odwraca wszelkie zmiany wprowadzone do `app.config` lub `web.config` podczas instalowania pakietu.
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

Zobacz sekcję [Znajdź pakiet](../reference/ps-reference/ps-ref-find-package.md). W Visual Studio 2013 i starszych, zamiast tego użyj polecenia [Get-Package](../reference/ps-reference/ps-ref-get-package.md) .

## <a name="availability-of-the-console"></a>Dostępność konsoli programu

Począwszy od programu Visual Studio 2017, NuGet i Menedżer pakietów NuGet są instalowane automatycznie po wybraniu dowolnego z nich. Obciążenia związane z usługą SIECIową; można ją także zainstalować oddzielnie, sprawdzając **poszczególne składniki > narzędzia kodu > opcji Menedżera pakietów NuGet** w Instalatorze programu Visual Studio.

Ponadto w przypadku braku Menedżera pakietów NuGet w programie Visual Studio 2015 i jego wcześniejszych wersjach zapoznaj się z **narzędziami > rozszerzenia i aktualizacje...** , a następnie wyszukaj rozszerzenie Menedżera pakietów NuGet. Jeśli nie możesz użyć Instalatora rozszerzeń w programie Visual Studio, możesz pobrać rozszerzenie bezpośrednio z [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).

Konsola Menedżera pakietów nie jest obecnie dostępna z Visual Studio dla komputerów Mac. Równoważne polecenia są jednak dostępne za pomocą [interfejsu wiersza polecenia NuGet](../reference/nuget-exe-CLI-reference.md). Visual Studio dla komputerów Mac ma interfejs użytkownika do zarządzania pakietami NuGet. Zobacz [dołączanie pakietu NuGet do projektu](/visualstudio/mac/nuget-walkthrough).

Konsola Menedżera pakietów nie jest dołączona do Visual Studio Code.

## <a name="extend-the-package-manager-console"></a>Rozwiń konsolę Menedżera pakietów

Niektóre pakiety instalują nowe polecenia dla konsoli programu. Na przykład `MvcScaffolding` tworzy polecenia, takie jak `Scaffold` pokazano poniżej, generujące kontrolery i widoki ASP.NET MVC:

![Instalowanie i używanie MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a>Konfigurowanie profilu programu PowerShell NuGet

Profil programu PowerShell umożliwia wykonywanie typowych poleceń dostępnych wszędzie tam, gdzie używasz programu PowerShell. Pakiet NuGet obsługuje profil specyficzny dla programu NuGet, który zwykle znajduje się w następującej lokalizacji:

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Aby znaleźć profil, wpisz `$profile` w konsoli programu:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Aby uzyskać więcej informacji, zobacz [Profile programu Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).

## <a name="use-the-nugetexe-cli-in-the-console"></a>Korzystanie z interfejsu wiersza polecenia NuGet. exe w konsoli programu

Aby udostępnić [interfejs wiersza polecenia`nuget.exe`](../reference/nuget-exe-cli-reference.md) w konsoli Menedżera pakietów, zainstaluj pakiet [NuGet. CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) z konsoli programu:

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
