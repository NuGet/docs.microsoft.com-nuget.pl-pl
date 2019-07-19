---
title: Instalowanie pakietów NuGet i zarządzanie nimi przy użyciu interfejsu wiersza polecenia dotnet
description: Instrukcje dotyczące używania interfejsu wiersza polecenia dotnet do pracy z pakietami NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: a796c7a7537c3052259c7cf3f17d60981a495442
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317715"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a>Instalowanie pakietów i zarządzanie nimi przy użyciu interfejsu wiersza polecenia dotnet

Narzędzie interfejsu wiersza polecenia umożliwia łatwe instalowanie, Odinstalowywanie i aktualizowanie pakietów NuGet w projektach i rozwiązaniach. Działa w systemach Windows, Mac OS X i Linux.

Interfejs wiersza polecenia dotnet jest używany w projekcie .NET Core i .NET Standard projektu (typy projektów w stylu zestawu SDK) oraz dla innych projektów w stylu zestawu SDK (na przykład projekt w stylu zestawu SDK, który jest przeznaczony dla .NET Framework). Aby uzyskać więcej informacji, zobacz [atrybut zestawu SDK](/dotnet/core/tools/csproj#additions).

W tym artykule przedstawiono podstawowe użycie kilku typowych poleceń interfejsu wiersza polecenia dotnet. W przypadku większości tych poleceń narzędzie interfejsu wiersza polecenia szuka pliku projektu w bieżącym katalogu, chyba że plik projektu jest określony w poleceniu (plik projektu jest przełącznikiem opcjonalnym). Aby uzyskać pełną listę poleceń i argumentów, których można użyć, zobacz [Narzędzia interfejsu wiersza polecenia (CLI) platformy .NET Core](../reference/dotnet-commands.md).

## <a name="prerequisites"></a>Wymagania wstępne

- [Zestaw .NET Core SDK](https://www.microsoft.com/net/download/), która udostępnia `dotnet` narzędzie wiersza polecenia. Począwszy od programu Visual Studio 2017, interfejs wiersza polecenia dotnet jest automatycznie instalowany z dowolnymi obciążeniami związanymi z platformą .NET Core.

## <a name="install-a-package"></a>Zainstaluj pakiet

polecenie [dotnet Add Package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) dodaje odwołanie do pakietu do pliku projektu, a następnie `dotnet restore` uruchamia polecenie, aby zainstalować pakiet.

1. Otwórz wiersz polecenia i przejdź do katalogu, który zawiera plik projektu.

2. Użyj następującego polecenia, aby zainstalować pakiet NuGet:

    ```cli
    dotnet add package <PACKAGE_NAME>
    ```

    Na przykład aby zainstalować `Newtonsoft.Json` pakiet, użyj następującego polecenia

    ```cli
    dotnet add package Newtonsoft.Json
    ```

3. Po zakończeniu wykonywania polecenia Sprawdź plik projektu, aby upewnić się, że pakiet został zainstalowany.

   Możesz otworzyć `.csproj` plik, aby zobaczyć dodane odwołanie:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a>Zainstaluj określoną wersję pakietu

Jeśli wersja nie zostanie określona, NuGet zainstaluje najnowszą wersję pakietu. Aby zainstalować określoną wersję pakietu NuGet, można również użyć polecenia [dotnet Add Package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) :

```cli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

Na przykład, aby dodać wersję 12.0.1 `Newtonsoft.Json` pakietu, użyj tego polecenia:

```cli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a>Wyświetl listę odwołań do pakietów

Możesz wyświetlić listę odwołań do pakietów dla projektu przy użyciu polecenia [pakietu dotnet list](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) .

```cli
dotnet list package
```

## <a name="remove-a-package"></a>Usuń pakiet

Aby usunąć odwołanie do pakietu z pliku projektu, użyj polecenia [dotnet Remove Package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) .

```cli
dotnet remove package <PACKAGE_NAME>
```

Na przykład aby usunąć `Newtonsoft.Json` pakiet, użyj następującego polecenia

```cli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a>Aktualizowanie pakietu

Pakiet NuGet instaluje najnowszą wersję pakietu przy użyciu `dotnet add package` polecenia, o ile nie zostanie określona wersja pakietu (`-v` przełącznik).

## <a name="restore-packages"></a>Przywróć pakiety

Użyj [dotnet Restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) polecenie, które przywraca pakiety wymienione w pliku projektu (zobacz [PackageReference](../consume-packages/package-references-in-project-files.md)). W przypadku platformy .NET Core 2,0 i nowszych przywracanie jest wykonywane automatycznie `dotnet build` z `dotnet run`i. W przypadku programu NuGet 4,0 ten sam kod jest uruchamiany co `nuget restore`.

Podobnie jak w przypadku `dotnet` innych poleceń interfejsu wiersza polecenia, najpierw Otwórz wiersz poleceń i przejdź do katalogu, który zawiera plik projektu.

Aby przywrócić pakiet przy użyciu `dotnet restore`:

```cli
dotnet restore 
```
