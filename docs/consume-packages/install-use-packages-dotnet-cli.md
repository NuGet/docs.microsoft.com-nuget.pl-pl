---
title: Instalowanie pakietów NuGet i zarządzanie nimi przy użyciu interfejsu wiersza polecenia dotnet
description: Instrukcje dotyczące używania interfejsu wiersza polecenia dotnet do pracy z pakietami NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 62c05aad388c25120d5b9f5143017a2f4f3b276b
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323612"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a>Instalowanie pakietów i zarządzanie nimi przy użyciu interfejsu wiersza polecenia dotnet

Narzędzie interfejsu wiersza polecenia umożliwia łatwe instalowanie, odinstalowywanie i aktualizowanie pakietów NuGet w projektach i rozwiązaniach. Działa w systemach Windows, Mac OS X i Linux.

Interfejs wiersza polecenia dotnet jest przeznaczony do użycia w projekcie .NET Core i .NET Standard (typy projektów w stylu zestawu SDK) oraz w innych projektach w stylu zestawu SDK (na przykład w projekcie w stylu zestawu SDK przeznaczonym dla .NET Framework). Aby uzyskać więcej informacji, zobacz [Atrybut zestawu SDK](/dotnet/core/tools/csproj#additions).

W tym artykule przedstawiono podstawowe użycie kilku najpopularniejszych poleceń interfejsu wiersza polecenia dotnet. W przypadku większości tych poleceń narzędzie interfejsu wiersza polecenia szuka pliku projektu w bieżącym katalogu, chyba że w poleceniu określono plik projektu (plik projektu jest opcjonalnym przełącznikiem). Aby uzyskać pełną listę poleceń i argumentów, których można użyć, zobacz narzędzia interfejsu wiersza polecenia [(CLI) programu .NET Core.](../reference/dotnet-commands.md)

## <a name="prerequisites"></a>Wymagania wstępne

- Narzędzie [zestaw .NET Core SDK](https://www.microsoft.com/net/download/), które udostępnia `dotnet` narzędzie wiersza polecenia. Począwszy od Visual Studio 2017 r., interfejs wiersza polecenia dotnet jest automatycznie instalowany z dowolnymi obciążeniami powiązanymi z programem .NET Core.

## <a name="install-a-package"></a>Instalowanie pakietu

[Dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) dodaje odwołanie do pakietu do pliku projektu, a następnie uruchamia program `dotnet restore` w celu zainstalowania pakietu.

1. Otwórz wiersz polecenia i przejdź do katalogu zawierającego plik projektu.

2. Użyj następującego polecenia, aby zainstalować pakiet NuGet:

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    Aby na przykład zainstalować `Newtonsoft.Json` pakiet, użyj następującego polecenia

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. Po zakończeniu polecenia sprawdź plik projektu, aby upewnić się, że pakiet został zainstalowany.

   Możesz otworzyć `.csproj` plik, aby zobaczyć dodane odwołanie:

    ```xml
    <ItemGroup>
      <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
    </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a>Instalowanie określonej wersji pakietu

Jeśli wersja nie zostanie określona, program NuGet zainstaluje najnowszą wersję pakietu. Możesz również użyć polecenia [dotnet add package,](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) aby zainstalować określoną wersję pakietu NuGet:

```dotnetcli
dotnet add package <PACKAGE_NAME> --version <VERSION>
```

Aby na przykład dodać wersję 12.0.1 `Newtonsoft.Json` pakietu, użyj tego polecenia:

```dotnetcli
dotnet add package Newtonsoft.Json --version 12.0.1
```

## <a name="list-package-references"></a>Lista odwołań do pakietów

Odwołania do pakietu dla projektu można wyświetlić za pomocą polecenia [dotnet list package.](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x)

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a>Usuwanie pakietu

Użyj polecenia [dotnet remove package,](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) aby usunąć odwołanie do pakietu z pliku projektu.

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

Aby na przykład usunąć `Newtonsoft.Json` pakiet, użyj następującego polecenia

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a>Aktualizowanie pakietu

NuGet instaluje najnowszą wersję pakietu podczas korzystania z polecenia , chyba że określisz wersję `dotnet add package` pakietu `-v` (przełącznik).

## <a name="restore-packages"></a>Przywracanie pakietów

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
