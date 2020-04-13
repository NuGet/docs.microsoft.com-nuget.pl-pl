---
title: Zarządzanie pakietami NuGet przy użyciu interfejsu wiersza polecenia nuget.exe
description: Instrukcje dotyczące korzystania z nuget.exe CLI do pracy z pakietami NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 7039dd27f2dddebc3c84e5ad35d5efec59547792
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428689"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a>Zarządzanie pakietami przy użyciu interfejsu wiersza polecenia nuget.exe

Narzędzie CLI umożliwia łatwą aktualizację i przywracanie pakietów NuGet w projektach i rozwiązaniach. To narzędzie zapewnia wszystkie funkcje NuGet w systemie Windows, a także zapewnia większość funkcji na komputerach Mac i Linux podczas uruchamiania w obszarze Mono.

Cli `nuget.exe` jest dla projektu .NET Framework i projektów w stylu innych niż SDK (na przykład projekt stylu innych niż SDK, który jest przeznaczony dla bibliotek .NET Standard). Jeśli używasz projektu w stylu nieskładu SDK, który został zmigrowany do `PackageReference`, użyj `dotnet` interfejsu wiersza polecenia. Cli `nuget.exe` wymaga pliku [packages.config](../reference/packages-config.md) dla odwołań do pakietu.

> [!NOTE]
> W większości scenariuszy zaleca się [migrację projektów w stylu innych niż SDK,](../consume-packages/migrate-packages-config-to-package-reference.md) które używają `packages.config` do PackageReference, a następnie można użyć `dotnet` interfejsu wiersza polecenia zamiast interfejsu wiersza `nuget.exe` polecenia. Migracja nie jest obecnie dostępna dla projektów języka C++ i ASP.NET.

W tym artykule przedstawiono podstawowe użycie `nuget.exe` kilku najczęściej spotykanych poleceń interfejsu wiersza polecenia. W przypadku większości z tych poleceń narzędzie interfejsu wiersza polecenia wyszukuje plik projektu w bieżącym katalogu, chyba że w poleceniu określono plik projektu. Aby uzyskać pełną listę poleceń i argumenty, których można użyć, zobacz [odwołanie do interfejsu wiersza polecenia nuget.exe](../reference/nuget-exe-cli-reference.md).

## <a name="prerequisites"></a>Wymagania wstępne

- Zainstaluj `nuget.exe` interfejsu wiersza polecenia, pobierając go `.exe` z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), zapisując ten plik do odpowiedniego folderu i dodając ten folder do zmiennej środowiskowej PATH.

## <a name="install-a-package"></a>Instalowanie pakietu

Polecenie [install](../reference/cli-reference/cli-ref-install.md) pobiera i instaluje pakiet w projekcie, domyślnie w bieżącym folderze, przy użyciu określonych źródeł pakietu. Zainstaluj nowe pakiety w folderze *pakietów* w katalogu głównym projektu.

> [!IMPORTANT]
> Polecenie `install`nie modyfikuje pliku projektu ani *pliku packages.config*; w ten sposób jest `restore` podobny do tego, że tylko dodaje pakiety do dysku, ale nie zmienia zależności projektu. Aby dodać zależność, dodaj pakiet za pośrednictwem interfejsu użytkownika menedżera pakietów lub konsoli w programie Visual `install` `restore`Studio lub zmodyfikuj *plik packages.config,* a następnie uruchom albo .

1. Otwórz wiersz polecenia i przełącz się do katalogu zawierającego plik projektu.

2. Użyj następującego polecenia, aby zainstalować pakiet NuGet w folderze *pakietów.*

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    Aby zainstalować `Newtonsoft.json` pakiet w folderze *pakietów,* użyj następującego polecenia:

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

Alternatywnie można użyć następującego polecenia, aby zainstalować pakiet `packages.config` NuGet przy użyciu istniejącego pliku do folderu *pakietów.* Nie powoduje to dodania pakietu do zależności projektu, ale instaluje go lokalnie.

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a>Instalowanie określonej wersji pakietu

Jeśli wersja nie jest określona podczas korzystania z polecenia [install,](../reference/cli-reference/cli-ref-install.md) NuGet instaluje najnowszą wersję pakietu. Można również zainstalować określoną wersję pakietu Nuget:

```cli
nuget install <packageID | configFilePath> -Version <version>
```

Na przykład, aby dodać wersję 12.0.1 `Newtonsoft.json` pakietu, użyj tego polecenia:

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

Aby uzyskać więcej informacji na `install`temat ograniczeń i zachowania programu , zobacz [Instalowanie pakietu](#install-a-package).

## <a name="remove-a-package"></a>Usuwanie pakietu

Aby usunąć jeden lub więcej pakietów, usuń pakiety, które chcesz usunąć z folderu *pakietów.*

Jeśli chcesz ponownie zainstalować pakiety, `restore` `install` użyj polecenia lub polecenia.

## <a name="list-packages"></a>Lista pakietów

Za pomocą polecenia [list](../reference/cli-reference/cli-ref-list.md) można wyświetlić listę pakietów z danego źródła. Użyj `-Source` tej opcji, aby ograniczyć wyszukiwanie.

```cli
nuget list -Source <source>
```

Na przykład lista pakietów w folderze *pakietów.*

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

Jeśli używasz wyszukiwanego terminu, wyszukiwanie zawiera nazwy pakietów, tagów i opisów pakietów.

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a>Aktualizowanie pojedynczego pakietu

NuGet instaluje najnowszą wersję pakietu `install` podczas korzystania z polecenia, chyba że określisz wersję pakietu.

## <a name="update-all-packages"></a>Aktualizuj wszystkie pakiety

Użyj polecenia [update,](../reference/cli-reference/cli-ref-update.md) aby zaktualizować wszystkie pakiety. Aktualizuje wszystkie pakiety `packages.config`w projekcie (za pomocą) do ich najnowszych dostępnych wersji. Zaleca się uruchomienie `restore` przed `update`uruchomieniem .

```cli
nuget update
```

## <a name="restore-packages"></a>Przywracanie pakietów

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

## <a name="get-the-cli-version"></a>Pobierz wersję interfejsu wiersza polecenia

Użyj tego polecenia:

```cli
nuget help
```

Pierwszy wiersz w danych wyjściowych pomocy pokazuje wersję. Aby uniknąć przewijania `nuget help | more` w górę, użyj zamiast tego.