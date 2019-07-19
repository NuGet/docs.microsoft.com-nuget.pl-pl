---
title: Zarządzanie pakietami NuGet przy użyciu interfejsu wiersza polecenia NuGet. exe
description: Instrukcje dotyczące używania interfejsu wiersza polecenia NuGet. exe do pracy z pakietami NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 9eefed6f2c1a362f27c4a5d33d07645d743379fa
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317746"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a>Zarządzanie pakietami za pomocą interfejsu wiersza polecenia NuGet. exe

Narzędzie interfejsu wiersza polecenia umożliwia łatwe aktualizowanie i przywracanie pakietów NuGet w projektach i rozwiązaniach. To narzędzie zapewnia wszystkie możliwości programu NuGet w systemie Windows, a także zapewnia większość funkcji na komputerach Mac i Linux, gdy działa w trybie mono.

`nuget.exe` Interfejs wiersza polecenia jest przeznaczony dla projektu .NET Framework i projektów nie należących do zestawu SDK (na przykład projektu w stylu innym niż zestaw SDK, który jest celem bibliotek .NET standard). Jeśli używasz projektu typu innego niż zestaw SDK, który został zmigrowany do `PackageReference`, `dotnet` Użyj interfejsu wiersza polecenia. Interfejs wiersza polecenia wymaga pliku [Packages. config](../reference/packages-config.md) na potrzeby odwołań do pakietu. `nuget.exe`

> [!NOTE]
> W większości scenariuszy zalecamy Migrowanie [projektów typu non-SDK](../reference/migrate-packages-config-to-package-reference.md) , które są używane `packages.config` do PackageReference, a następnie można użyć `dotnet` interfejsu wiersza polecenia zamiast `nuget.exe` interfejsu wiersza polecenia. Migracja nie jest obecnie dostępna dla C++ projektów i ASP.NET.

W tym artykule przedstawiono podstawowe użycie kilku najpopularniejszych `nuget.exe` poleceń interfejsu wiersza polecenia. W przypadku większości tych poleceń narzędzie interfejsu wiersza polecenia szuka pliku projektu w bieżącym katalogu, chyba że plik projektu jest określony w poleceniu. Aby uzyskać pełną listę poleceń i argumentów, których można użyć, zobacz [Dokumentacja interfejsu wiersza polecenia NuGet. exe](../reference/nuget-exe-cli-reference.md).

## <a name="prerequisites"></a>Wymagania wstępne

- Zainstaluj interfejs wiersza polecenia, pobierając go z [NuGet.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), zapisując `.exe` ten plik w odpowiednim folderze i dodając go do zmiennej środowiskowej PATH. `nuget.exe`

## <a name="install-a-package"></a>Zainstaluj pakiet

Polecenie [instalacji](../reference/cli-reference/cli-ref-install.md) pobiera i instaluje pakiet w projekcie, domyślnie do bieżącego folderu przy użyciu określonych źródeł pakietów. Zainstaluj nowe pakiety w folderze *Packages* w katalogu głównym projektu.

> [!IMPORTANT]
> Polecenie nie modyfikuje pliku projektu lub Packages *. config*; w ten sposób jest to podobne do `restore` w przypadku, gdy tylko dodaje pakiety do dysku, ale nie zmienia zależności projektu. `install` Aby dodać zależność, Dodaj pakiet za pomocą interfejsu użytkownika lub konsoli Menedżera pakietów w programie Visual Studio lub zmodyfikuj *plik Packages. config* , a następnie uruchom `install` polecenie `restore`lub.

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

Aby uzyskać więcej informacji o ograniczeniach i zachowaniu programu `install`, zobacz [Instalowanie pakietu](#install-a-package).

## <a name="remove-a-package"></a>Usuń pakiet

Aby usunąć co najmniej jeden pakiet, Usuń pakiety, które chcesz usunąć z folderu *pakiety* .

Jeśli chcesz ponownie zainstalować pakiety, użyj `restore` polecenia lub. `install`

## <a name="list-packages"></a>Wyświetl listę pakietów

Możesz wyświetlić listę pakietów z danego źródła za pomocą polecenia [list](../reference/cli-reference/cli-ref-list.md) . `-Source` Użyj opcji, aby ograniczyć wyszukiwanie.

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

Użyj polecenia [Aktualizuj](../reference/cli-reference/cli-ref-update.md) , aby zaktualizować wszystkie pakiety. Aktualizuje wszystkie pakiety w projekcie (przy użyciu `packages.config`programu) do ich najnowszych dostępnych wersji. Zaleca się uruchomienie `restore` przed uruchomieniem `update`programu.

```cli
nuget update
```

## <a name="restore-packages"></a>Przywróć pakiety

Użyj polecenia [Restore](../reference/cli-reference/cli-ref-restore.md) , które pobiera i instaluje wszystkie brakujące pakiety w folderze *Packages* .

`restore`dodaje pakiety tylko do dysku, ale nie zmienia zależności projektu. Aby przywrócić zależności projektu, należy `packages.config`zmodyfikować, a następnie `restore` użyć polecenia.

Podobnie jak w przypadku `nuget.exe` innych poleceń interfejsu wiersza polecenia, najpierw Otwórz wiersz poleceń i przejdź do katalogu, który zawiera plik projektu.

Aby przywrócić pakiet przy użyciu `restore`:

```cli
nuget restore MySolution.sln
```