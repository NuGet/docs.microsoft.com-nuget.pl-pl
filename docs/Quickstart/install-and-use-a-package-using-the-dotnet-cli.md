---
title: "Wprowadzenie do przewodnika za pomocą pakietów NuGet przez dotnet interfejsu wiersza polecenia | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Samouczek wskazówki na proces instalowania i używania pakietu NuGet w projekcie platformy .NET Core."
keywords: "instalowania NuGet użycia pakietu NuGet, instalowanie pakietów NuGet, odwołania do pakietu NuGet, za pomocą pakietów NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: accc6d7bb5abff43ffaa083fa55c13cd5b10ce10
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/08/2018
---
# <a name="install-and-use-a-package-using-the-dotnet-cli"></a>Zainstalować i używać pakietu przy użyciu dotnet interfejsu wiersza polecenia

Pakiety NuGet zawiera kod wielokrotnego użytku, który inni deweloperzy udostępnić użytkownikowi do użycia w projektach. Zobacz [co to jest NuGet?](../What-is-NuGet.md) w tle. Pakiety są zainstalowane w projekcie platformy .NET Core za pomocą `dotnet add package` polecenia zgodnie z opisem w tym artykule popularnych [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) pakietu.

Po zakończeniu instalacji można znaleźć pakietu w kodzie z `using <namespace>` gdzie \<przestrzeni nazw\> jest przeznaczony dla pakietu używasz. Po odniesienia, można wywołać pakietu za pośrednictwem jej interfejsu API.

> [!Tip]
> **Rozpoczynać nuget.org**: nuget.org przeglądania jest jak .NET deweloperzy zazwyczaj znaleźć składników może zostać ponownie użyty we własnych aplikacjach. Można wyszukiwać nuget.org bezpośrednio lub znaleźć i zainstalować pakiety w programie Visual Studio, jak pokazano w tym artykule.

## <a name="prerequisites"></a>Wymagania wstępne

- [.NET Core SDK](https://www.microsoft.com/net/download/), która zapewnia `dotnet` narzędzia wiersza polecenia.

## <a name="create-a-project"></a>Tworzenie projektu

Można zainstalować pakietów NuGet w projekcie .NET określonego rodzaju. W ramach tego przewodnika Utwórz prosty projekt konsoli .NET Core w następujący sposób:

1. Utwórz folder dla projektu.

1. Utwórz projekt za pomocą następującego polecenia:

    ```cli
    dotnet new console
    ```

1. Użyj `dotnet run` do przetestowania, czy aplikacja została utworzona poprawnie.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Dodaj pakiet Newtonsoft.Json NuGet

1. Użyj następującego polecenia, aby zainstalować `Newtonsoft.json` pakietu:

    ```cli
    dotnet add package Newtonsoft.Json
    ```

1. Po zakończeniu działania polecenia Otwórz `.csproj` plik, aby wyświetlić odwołania dodane:

    ```xml
  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.3" />
  </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Użyj Newtonsoft.Json interfejsu API w aplikacji

1. Otwórz `Program.cs` pliku i Dodaj następujący wiersz na początku pliku:

    ```cs
    using Newtonsoft.Json;
    ```

1. Dodaj następujący kod przed `class Program` wiersza:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. Zastąp `Main` funkcji z następujących czynności:

    ```cs
    static void Main(string[] args)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@nuget.org",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };

        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        Console.WriteLine(json);
    }
    ```

1. Tworzenie i uruchamianie aplikacji przy użyciu `dotnet run` polecenia. Dane wyjściowe powinny mieć reprezentacja JSON `Account` obiektu w kodzie:

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a>Pokrewne artykuły

- [Omówienie i przepływ pracy zużycia pakietu](../consume-packages/overview-and-workflow.md)
- [Znajdowanie i wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md)
- [Sposoby instalacji pakietu](../consume-packages/ways-to-install-a-package.md)
- [Konfigurowanie zachowania programu NuGet](../consume-packages/configuring-nuget-behavior.md)
