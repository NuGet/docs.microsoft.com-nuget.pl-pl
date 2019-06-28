---
title: Instalowanie i Zarządzaj pakietami NuGet za pomocą interfejsu wiersza polecenia platformy dotnet
description: Instrukcje dotyczące używania interfejsu wiersza polecenia platformy dotnet do pracy z pakietów NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: a8fd525f2446f9468664f1d80ef8808127a24be7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427642"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a>Instalowanie i zarządzanie pakietami za pomocą interfejsu wiersza polecenia platformy dotnet

Narzędzie interfejsu wiersza polecenia umożliwia łatwe instalowanie, odinstalowywanie oraz aktualizowanie pakietów NuGet w projektach i rozwiązaniach. Działa w Windows, Mac OS X i Linux.

Wiersz polecenia dotnet jest do użytku w projekcie platformy .NET Core i .NET Standard (typy projektów zestawu SDK stylu) oraz wszelkich innych zestawu SDK stylu projektów (na przykład, zestawu SDK stylu projektu, który jest przeznaczony dla .NET Framework). Aby uzyskać więcej informacji, zobacz [atrybutu zestawu SDK](/dotnet/core/tools/csproj#additions).

W tym artykule przedstawiono podstawowe użycia kilka najbardziej typowe polecenia interfejsu wiersza polecenia platformy dotnet. Dla większości z tych poleceń narzędzie interfejsu wiersza polecenia szuka pliku projektu w bieżącym katalogu, o ile nie określono pliku projektu w poleceniu (plik projektu jest opcjonalnym przełącznikiem). Aby uzyskać pełną listę poleceń i argumentów, można użyć, zobacz [narzędzi interfejsu wiersza polecenia (CLI) platformy .NET Core](../tools/dotnet-commands.md).

## <a name="prerequisites"></a>Wymagania wstępne

- [Zestawu .NET Core SDK](https://www.microsoft.com/net/download/), która zapewnia `dotnet` narzędzie wiersza polecenia. Począwszy od programu Visual Studio 2017, dotnet, których interfejs wiersza polecenia jest automatycznie instalowany z dowolnej platformy .NET Core powiązanych obciążeń.

## <a name="install-a-package"></a>Zainstaluj pakiet

[polecenia DotNet Dodaj pakiet](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) dodaje odwołania do pakietu do pliku projektu, a następnie uruchamia `dotnet restore` do zainstalowania pakietu.

1. Otwórz wiersz polecenia i przejdź do katalogu zawierającego plik projektu.

2. Aby zainstalować pakiet Nuget, użyj następującego polecenia:

    ```cli
    dotnet add package <PACKAGE_NAME>
    ```

    Na przykład, aby zainstalować `Newtonsoft.Json` pakietów, użyj następującego polecenia

    ```cli
    dotnet add package Newtonsoft.Json
    ```

3. Po wykonaniu polecenia, sprawdź plik projektu, aby upewnić się, że pakiet został zainstalowany.

   Możesz otworzyć `.csproj` plik, aby zobaczyć odwołania dodane:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a>Instalowanie określonej wersji pakietu

Jeśli nie określono wersji, NuGet instaluje najnowszą wersję pakietu. Można również użyć [dotnet Dodaj pakiet](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) polecenie, aby zainstalować określoną wersję pakietu Nuget:

```cli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

Na przykład, aby dodać wersję 12.0.1 `Newtonsoft.Json` pakietów, użyj tego polecenia:

```cli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a>Odwołania do pakietu z listy

Możesz wyświetlić listę odwołań do pakietów dla projektów przy użyciu [dotnet wyświetlenia listy pakietów](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) polecenia.

```cli
dotnet list package
```

## <a name="remove-a-package"></a>Usuń pakiet

Użyj [dotnet Usuń pakiet](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) polecenie, aby usunąć odwołanie do pakietu z pliku projektu.

```cli
dotnet remove package <PACKAGE_NAME>
```

Na przykład, aby usunąć `Newtonsoft.Json` pakietów, użyj następującego polecenia

```cli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a>Aktualizacja pakietu

NuGet instaluje najnowszą wersję pakietu, gdy używasz `dotnet add package` polecenia, chyba że określisz wersja pakietu (`-v` przełącznika).

## <a name="restore-packages"></a>Przywracanie pakietów

Użyj [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) polecenia, które pakiety wymienione w pliku projektu (zobacz [PackageReference](../consume-packages/package-references-in-project-files.md)). Za pomocą platformy .NET Core 2.0 i nowszych przywracania odbywa się automatycznie przy użyciu `dotnet build` i `dotnet run`. Począwszy od NuGet 4.0, spowoduje to uruchomienie tego samego kodu jako `nuget restore`.

Aby przywrócić dane przy użyciu pakietu `dotnet restore`:

```cli
dotnet restore 
```
