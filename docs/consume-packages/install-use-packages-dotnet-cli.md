---
title: Instalowanie pakietów NuGet i zarządzanie nimi przy użyciu interfejsu wiersza polecenia dotnet
description: Instrukcje dotyczące korzystania z dotnet CLI do pracy z pakietami NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 67cca81c48970c7f2e2cf0a64ee5ba57704a31e2
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825162"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a>Instalowanie pakietów i zarządzanie nimi przy użyciu interfejsu wiersza polecenia dotnet

Narzędzie CLI umożliwia łatwe instalowanie, odinstalowywanie i aktualizowanie pakietów NuGet w projektach i rozwiązaniach. Działa w systemach Windows, Mac OS X i Linux.

Dotnet CLI jest do użytku w projekcie .NET Core i .NET Standard (typy projektów w stylu SDK) oraz dla wszystkich innych projektów w stylu SDK (na przykład projektu w stylu SDK, który jest przeznaczony dla platformy .NET Framework). Aby uzyskać więcej informacji, zobacz [atrybut SDK](/dotnet/core/tools/csproj#additions).

W tym artykule przedstawiono podstawowe użycie kilku najczęściej spotykanych poleceń dotnet CLI. W przypadku większości z tych poleceń narzędzie interfejsu wiersza polecenia wyszukuje plik projektu w bieżącym katalogu, chyba że plik projektu jest określony w poleceniu (plik projektu jest przełącznikiem opcjonalnym). Aby uzyskać pełną listę poleceń i argumenty, których można użyć, zobacz [narzędzia interfejsu wiersza polecenia .NET Core .](../reference/dotnet-commands.md)

## <a name="prerequisites"></a>Wymagania wstępne

- Zestaw [SDK .NET Core](https://www.microsoft.com/net/download/) `dotnet` , który udostępnia narzędzie wiersza polecenia. Począwszy od programu Visual Studio 2017, dotnet interfejsu wiersza polecenia jest automatycznie instalowany z dowolnego .NET Core obciążeń związanych.

## <a name="install-a-package"></a>Instalowanie pakietu

[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) dodaje odwołanie do pakietu `dotnet restore` do pliku projektu, a następnie uruchamia się, aby zainstalować pakiet.

1. Otwórz wiersz polecenia i przełącz się do katalogu zawierającego plik projektu.

2. Aby zainstalować pakiet Nuget, użyj następującego polecenia:

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    Na przykład, aby `Newtonsoft.Json` zainstalować pakiet, użyj następującego polecenia

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. Po zakończeniu polecenia, spójrz na plik projektu, aby upewnić się, że pakiet został zainstalowany.

   Możesz otworzyć `.csproj` plik, aby wyświetlić dodane odwołanie:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a>Instalowanie określonej wersji pakietu

Jeśli wersja nie jest określona, NuGet instaluje najnowszą wersję pakietu. Można również użyć polecenia [dotnet add package,](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) aby zainstalować określoną wersję pakietu Nuget:

```dotnetcli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

Na przykład, aby dodać wersję 12.0.1 `Newtonsoft.Json` pakietu, użyj tego polecenia:

```dotnetcli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a>Numery pakietów list

Odwołania do pakietu dla projektu można wyświetlić za pomocą polecenia [pakietu listy dotnet.](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x)

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a>Usuwanie pakietu

Użyj polecenia [dotnet remove package,](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) aby usunąć odwołanie do pakietu z pliku projektu.

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

Na przykład, aby `Newtonsoft.Json` usunąć pakiet, użyj następującego polecenia

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a>Aktualizowanie pakietu

NuGet instaluje najnowszą wersję pakietu `dotnet add package` podczas korzystania z polecenia,`-v` chyba że określisz wersję pakietu ( przełącznik).

## <a name="restore-packages"></a>Przywracanie pakietów

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
