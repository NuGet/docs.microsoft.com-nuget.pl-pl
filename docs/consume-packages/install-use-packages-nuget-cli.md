---
title: Zarządzanie pakietami NuGet przy użyciu interfejsu wiersza polecenia NuGet. exe
description: Instrukcje dotyczące używania interfejsu wiersza polecenia NuGet. exe do pracy z pakietami NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 7039dd27f2dddebc3c84e5ad35d5efec59547792
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428689"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a>Zarządzanie pakietami za pomocą interfejsu wiersza polecenia NuGet. exe

Narzędzie interfejsu wiersza polecenia umożliwia łatwe aktualizowanie i przywracanie pakietów NuGet w projektach i rozwiązaniach. To narzędzie zapewnia wszystkie możliwości programu NuGet w systemie Windows, a także zapewnia większość funkcji na komputerach Mac i Linux, gdy działa w trybie mono.

Interfejs wiersza polecenia `nuget.exe` jest przeznaczony dla projektu .NET Framework i projektów spoza zestawu SDK (na przykład projekt typu innego niż zestaw SDK przeznaczony dla bibliotek .NET Standard). Jeśli używasz projektu typu innego niż zestaw SDK, który został zmigrowany do `PackageReference`, zamiast tego użyj interfejsu wiersza polecenia `dotnet`. Interfejs wiersza polecenia `nuget.exe` wymaga pliku [Packages. config](../reference/packages-config.md) na potrzeby odwołań do pakietu.

> [!NOTE]
> W większości scenariuszy zalecamy [Migrowanie projektów typu non-SDK](../consume-packages/migrate-packages-config-to-package-reference.md) , które używają `packages.config` do PackageReference, a następnie można użyć interfejsu wiersza polecenia `dotnet` zamiast interfejsu wiersza polecenia `nuget.exe`. Migracja nie jest obecnie dostępna dla C++ projektów i ASP.NET.

W tym artykule przedstawiono podstawowe użycie kilku typowych poleceń interfejsu wiersza polecenia `nuget.exe`. W przypadku większości tych poleceń narzędzie interfejsu wiersza polecenia szuka pliku projektu w bieżącym katalogu, chyba że plik projektu jest określony w poleceniu. Aby uzyskać pełną listę poleceń i argumentów, których można użyć, zobacz [Dokumentacja interfejsu wiersza polecenia NuGet. exe](../reference/nuget-exe-cli-reference.md).

## <a name="prerequisites"></a>Wymagania wstępne

- Zainstaluj interfejs wiersza polecenia `nuget.exe`, pobierając go z [NuGet.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), zapisując plik `.exe` do odpowiedniego folderu i dodając go do zmiennej środowiskowej PATH.

## <a name="install-a-package"></a>Zainstaluj pakiet

Polecenie [instalacji](../reference/cli-reference/cli-ref-install.md) pobiera i instaluje pakiet w projekcie, domyślnie do bieżącego folderu przy użyciu określonych źródeł pakietów. Zainstaluj nowe pakiety w folderze *Packages* w katalogu głównym projektu.

> [!IMPORTANT]
> Polecenie `install`nie modyfikuje pliku projektu ani *pakietów. config*; w ten sposób przypomina `restore`, że tylko dodaje pakiety do dysku, ale nie zmienia zależności projektu. Aby dodać zależność, Dodaj pakiet za pomocą interfejsu użytkownika lub konsoli Menedżera pakietów w programie Visual Studio lub zmodyfikuj *plik Packages. config* , a następnie uruchom polecenie `install` lub `restore`.

1. Otwórz wiersz polecenia i przejdź do katalogu, który zawiera plik projektu.

2. Użyj poniższego polecenia, aby zainstalować pakiet NuGet w folderze *Packages* .

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    Aby zainstalować pakiet `Newtonsoft.json` w folderze *Packages* , użyj następującego polecenia:

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

Alternatywnie możesz użyć poniższego polecenia, aby zainstalować pakiet NuGet przy użyciu istniejącego pliku `packages.config` w folderze *Packages* . Nie powoduje to dodania pakietu do zależności projektu, ale instaluje go lokalnie.

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a>Zainstaluj określoną wersję pakietu

Jeśli wersja nie zostanie określona podczas korzystania z polecenia [Install](../reference/cli-reference/cli-ref-install.md) , pakiet NuGet instaluje najnowszą wersję pakietu. Można także zainstalować określoną wersję pakietu NuGet:

```cli
nuget install <packageID | configFilePath> -Version <version>
```

Na przykład, aby dodać wersję 12.0.1 pakietu `Newtonsoft.json`, użyj tego polecenia:

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

Aby uzyskać więcej informacji o ograniczeniach i zachowaniu `install`, zobacz [Instalowanie pakietu](#install-a-package).

## <a name="remove-a-package"></a>Usuń pakiet

Aby usunąć co najmniej jeden pakiet, Usuń pakiety, które chcesz usunąć z folderu *pakiety* .

Jeśli chcesz ponownie zainstalować pakiety, użyj polecenia `restore` lub `install`.

## <a name="list-packages"></a>Wyświetl listę pakietów

Możesz wyświetlić listę pakietów z danego źródła za pomocą polecenia [list](../reference/cli-reference/cli-ref-list.md) . Użyj opcji `-Source`, aby ograniczyć wyszukiwanie.

```cli
nuget list -Source <source>
```

Na przykład Wyświetl listę pakietów w folderze *Packages* .

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

W przypadku korzystania z wyszukiwanego terminu wyszukiwanie obejmuje nazwy pakietów, tagów i opisów pakietów.

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a>Aktualizowanie pojedynczego pakietu

Pakiet NuGet instaluje najnowszą wersję pakietu przy użyciu polecenia `install`, o ile nie zostanie określona wersja pakietu.

## <a name="update-all-packages"></a>Aktualizuj wszystkie pakiety

Użyj polecenia [Aktualizuj](../reference/cli-reference/cli-ref-update.md) , aby zaktualizować wszystkie pakiety. Aktualizuje wszystkie pakiety w projekcie (przy użyciu `packages.config`) do ich najnowszych dostępnych wersji. Przed uruchomieniem `update`zaleca się uruchomienie `restore`.

```cli
nuget update
```

## <a name="restore-packages"></a>Przywróć pakiety

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

## <a name="get-the-cli-version"></a>Pobierz wersję interfejsu wiersza polecenia

Użyj tego polecenia:

```cli
nuget help
```

Pierwszy wiersz w danych wyjściowych pomocy pokazuje wersję. Aby uniknąć przewijania, Użyj zamiast tego `nuget help | more`.