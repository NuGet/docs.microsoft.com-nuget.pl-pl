---
title: Zarządzanie pakietami NuGet przy użyciu interfejsu wiersza polecenia nuget.exe
description: Instrukcje dotyczące używania interfejsu wiersza polecenia nuget.exe do pracy z pakietami NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 7039dd27f2dddebc3c84e5ad35d5efec59547792
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237390"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a>Zarządzanie pakietami za pomocą interfejsu wiersza polecenia nuget.exe

Narzędzie interfejsu wiersza polecenia umożliwia łatwe aktualizowanie i przywracanie pakietów NuGet w projektach i rozwiązaniach. To narzędzie zapewnia wszystkie możliwości programu NuGet w systemie Windows, a także zapewnia większość funkcji na komputerach Mac i Linux, gdy działa w trybie mono.

`nuget.exe`Interfejs wiersza polecenia jest przeznaczony dla projektu .NET Framework i projektów nie należących do zestawu SDK (na przykład projektu w stylu innym niż zestaw SDK, który jest celem bibliotek .NET standard). Jeśli używasz projektu typu innego niż zestaw SDK, który został zmigrowany do `PackageReference` , użyj `dotnet` interfejsu wiersza polecenia. `nuget.exe`Interfejs wiersza polecenia wymaga pliku [packages.config](../reference/packages-config.md) do odwołania do pakietu.

> [!NOTE]
> W większości scenariuszy zalecamy [Migrowanie projektów typu non-SDK](../consume-packages/migrate-packages-config-to-package-reference.md) , które są używane `packages.config` do PackageReference, a następnie można użyć `dotnet` interfejsu wiersza polecenia zamiast `nuget.exe` interfejsu wiersza polecenia. Migracja nie jest obecnie dostępna dla projektów C++ i ASP.NET.

W tym artykule przedstawiono podstawowe użycie kilku najpopularniejszych `nuget.exe` poleceń interfejsu wiersza polecenia. W przypadku większości tych poleceń narzędzie interfejsu wiersza polecenia szuka pliku projektu w bieżącym katalogu, chyba że plik projektu jest określony w poleceniu. Aby uzyskać pełną listę poleceń i argumentów, których można użyć, zobacz [ informacje dotyczące interfejsu wiersza polecenianuget.exe](../reference/nuget-exe-cli-reference.md).

## <a name="prerequisites"></a>Wymagania wstępne

- Zainstaluj `nuget.exe` interfejs wiersza polecenia, pobierając go z [NuGet.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), zapisując ten `.exe` plik w odpowiednim folderze i dodając go do zmiennej środowiskowej PATH.

## <a name="install-a-package"></a>Instalowanie pakietu

Polecenie [instalacji](../reference/cli-reference/cli-ref-install.md) pobiera i instaluje pakiet w projekcie, domyślnie do bieżącego folderu przy użyciu określonych źródeł pakietów. Zainstaluj nowe pakiety w folderze *Packages* w katalogu głównym projektu.

> [!IMPORTANT]
> `install`Polecenie nie modyfikuje pliku projektu ani *packages.config* . w ten sposób jest to podobne do `restore` tego, że dodaje pakiety tylko do dysku, ale nie zmienia zależności projektu. Aby dodać zależność, Dodaj pakiet za pomocą interfejsu użytkownika lub konsoli Menedżera pakietów w programie Visual Studio lub zmodyfikuj *packages.config* a następnie uruchom albo `install` `restore` .

1. Otwórz wiersz polecenia i przejdź do katalogu, który zawiera plik projektu.

2. Użyj poniższego polecenia, aby zainstalować pakiet NuGet w folderze *Packages* .

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    Aby zainstalować `Newtonsoft.json` pakiet w folderze *Packages* , użyj następującego polecenia:

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

Alternatywnie możesz użyć poniższego polecenia, aby zainstalować pakiet NuGet przy użyciu istniejącego `packages.config` pliku w folderze *Packages* . Nie powoduje to dodania pakietu do zależności projektu, ale instaluje go lokalnie.

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a>Zainstaluj określoną wersję pakietu

Jeśli wersja nie zostanie określona podczas korzystania z polecenia [Install](../reference/cli-reference/cli-ref-install.md) , pakiet NuGet instaluje najnowszą wersję pakietu. Można także zainstalować określoną wersję pakietu NuGet:

```cli
nuget install <packageID | configFilePath> -Version <version>
```

Na przykład, aby dodać wersję 12.0.1 `Newtonsoft.json` pakietu, użyj tego polecenia:

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

Aby uzyskać więcej informacji o ograniczeniach i zachowaniu programu `install` , zobacz [Instalowanie pakietu](#install-a-package).

## <a name="remove-a-package"></a>Usuń pakiet

Aby usunąć co najmniej jeden pakiet, Usuń pakiety, które chcesz usunąć z folderu *pakiety* .

Jeśli chcesz ponownie zainstalować pakiety, użyj `restore` `install` polecenia lub.

## <a name="list-packages"></a>Wyświetl listę pakietów

Możesz wyświetlić listę pakietów z danego źródła za pomocą polecenia [list](../reference/cli-reference/cli-ref-list.md) . Użyj `-Source` opcji, aby ograniczyć wyszukiwanie.

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

Pakiet NuGet instaluje najnowszą wersję pakietu przy użyciu `install` polecenia, o ile nie zostanie określona wersja pakietu.

## <a name="update-all-packages"></a>Aktualizuj wszystkie pakiety

Użyj polecenia [Aktualizuj](../reference/cli-reference/cli-ref-update.md) , aby zaktualizować wszystkie pakiety. Aktualizuje wszystkie pakiety w projekcie (przy użyciu programu `packages.config` ) do ich najnowszych dostępnych wersji. Zaleca się uruchomienie `restore` przed uruchomieniem programu `update` .

```cli
nuget update
```

## <a name="restore-packages"></a>Przywracanie pakietów

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

## <a name="get-the-cli-version"></a>Pobierz wersję interfejsu wiersza polecenia

Użyj następującego polecenia:

```cli
nuget help
```

Pierwszy wiersz w danych wyjściowych pomocy pokazuje wersję. Aby uniknąć przewijania, użyj `nuget help | more` zamiast tego.