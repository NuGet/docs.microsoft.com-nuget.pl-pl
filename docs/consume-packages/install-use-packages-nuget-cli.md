---
title: Zarządzaj pakietami NuGet za pomocą interfejsu wiersza polecenia nuget.exe
description: Instrukcje dotyczące używania nuget.exe interfejsu wiersza polecenia do pracy z pakietami NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: a7177b956930835693921163e634321548c22462
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842370"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a>Zarządzanie pakietami za pomocą interfejsu wiersza polecenia nuget.exe

Narzędzie interfejsu wiersza polecenia pozwala łatwo zaktualizować i przywracanie pakietów NuGet w projektach i rozwiązaniach. To narzędzie oferuje wszystkie możliwości NuGet w Windows, a także większości funkcji na komputerach Mac i Linux w przypadku uruchomienia w Mono.

Nuget.exe interfejsu wiersza polecenia jest projekt programu .NET Framework i projektów innych stylu zestawu SDK (na przykład-SDK stylu projektu, który jest przeznaczony dla biblioteki .NET Standard). Jeśli używasz projektu bez stylu zestawu SDK, który zostały przeniesione do `PackageReference`, zamiast tego użyj wiersz polecenia dotnet. Interfejs wiersza polecenia NuGet wymaga [packages.config](../reference/packages-config.md) odwołania do pakietu w pliku.

> [!NOTE]
> W większości przypadków zaleca się [migrowania projektów bez SDK-style](../reference/migrate-packages-config-to-package-reference.md) używające `packages.config` do odwołania PackageReference, a następnie przy użyciu interfejsu wiersza polecenia platformy dotnet zamiast `nuget.exe` interfejsu wiersza polecenia. Migracja nie jest obecnie dostępna dla projektów C++ i programu ASP.NET.

W tym artykule przedstawiono podstawowe użycie niektóre z najczęściej używanych poleceń interfejsu wiersza polecenia nuget.exe. Dla większości z tych poleceń narzędzie interfejsu wiersza polecenia szuka pliku projektu w bieżącym katalogu, o ile nie określono pliku projektu w poleceniu. Aby uzyskać pełną listę poleceń i argumentów, można użyć, zobacz [dokumentacja interfejsu wiersza polecenia nuget.exe](../tools/nuget-exe-cli-reference.md).

## <a name="prerequisites"></a>Wymagania wstępne

- Zainstaluj `nuget.exe` interfejsu wiersza polecenia, pobierając go z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), zapisywania, który `.exe` pliku do odpowiedniego folderu i dodawanie folderu do zmiennej środowiskowej PATH.

## <a name="install-a-package"></a>Zainstaluj pakiet

[Zainstalować](../tools/cli-ref-install.md) polecenie pobiera i instaluje pakiet do projektu, domyślnie używany do bieżącego folderu, za pomocą źródeł określonego pakietu. Instalowanie nowych pakietów do *pakietów* folder w katalogu głównym projektu.

> [!IMPORTANT]
> `install`Polecenie nie modyfikuje plik projektu lub *packages.config*; dzięki temu jest on podobny do `restore` , ponieważ jej tylko dodaje pakiety do dysku, ale nie zmienia zależności projektu. Aby dodać zależność, Dodaj pakiet za pomocą interfejs użytkownika Menedżera pakietów lub konsoli w programie Visual Studio lub zmodyfikować *packages.config* , a następnie uruchom opcję `install` lub `restore`.

1. Otwórz wiersz polecenia i przejdź do katalogu zawierającego plik projektu.

2. Użyj następującego polecenia, aby zainstalować pakiet NuGet, aby *pakietów* folderu.

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    Aby zainstalować `Newtonsoft.json` pakietu *pakietów* folderu, użyj następującego polecenia:

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

Alternatywnie można użyć następującego polecenia można zainstalować pakietu NuGet, za pomocą istniejącego `packages.config` plik *pakietów* folderu. Nie powoduje dodania pakietu do zależności projektu, ale instaluje ją lokalnie.

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a>Instalowanie określonej wersji pakietu

Jeśli nie określono wersji, gdy używasz [zainstalować](../tools/cli-ref-install.md) polecenia NuGet instaluje najnowszą wersję pakietu. Można także zainstalować określoną wersję pakietu Nuget:

```cli
nuget install <packageID | configFilePath> -Version <version>
```

Na przykład, aby dodać wersję 12.0.1 `Newtonsoft.json` pakietów, użyj tego polecenia:

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

Aby uzyskać więcej informacji na temat ograniczeń i zachowanie `install`, zobacz [zainstalować pakiet](#install-a-package).

## <a name="remove-a-package"></a>Usuń pakiet

Aby usunąć co najmniej jeden pakiet, Usuń pakiety, aby usunąć z *pakietów* folderu.

Jeśli chcesz ponownie zainstalować pakiety, użyj `restore` lub `install` polecenia.

## <a name="list-packages"></a>Lista pakietów

Możesz wyświetlić listę pakietów z danego źródła przy użyciu [listy](../tools/cli-ref-list.md) polecenia. Użyj `-Source` opcję, aby ograniczyć wyszukiwanie.

```cli
nuget list -Source <source>
```

Na przykład listy pakietów *pakietów* folderu.

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

Jeśli używasz wyszukiwany termin, wyszukiwanie obejmuje nazwy pakietów, tagi i opisy pakietu.

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a>Aktualizowanie poszczególnych pakietów

NuGet instaluje najnowszą wersję pakietu, gdy używasz `install` polecenia, chyba że określisz wersja pakietu.

## <a name="update-all-packages"></a>Aktualizuj wszystkie pakiety

Użyj [aktualizacji](../tools/cli-ref-update.md) polecenie, aby zaktualizować wszystkich pakietów. Aktualizuje wszystkie pakiety w projekcie (przy użyciu `packages.config`) do jego najnowszej dostępnej wersji. Zaleca się uruchomienie `restore` przed uruchomieniem `update`.

```cli
nuget update
```

## <a name="restore-packages"></a>Przywracanie pakietów

Użyj [przywrócić](../tools/cli-ref-restore.md) polecenia, które pobiera i instaluje wszystkie pakiety brakuje *pakietów* folderu.

`restore` tylko dodaje pakiety do dysku, ale nie zmienia zależności projektu. Aby przywrócić zależności projektu, należy zmodyfikować `packages.config`, następnie za pomocą `restore` polecenia.

Podobnie jak w przypadku innych `dotnet` poleceń interfejsu wiersza polecenia, najpierw otwórz wiersz polecenia i przejdź do katalogu zawierającego plik projektu.

Aby przywrócić dane przy użyciu pakietu `restore`:

```cli
nuget restore MySolution.sln
```