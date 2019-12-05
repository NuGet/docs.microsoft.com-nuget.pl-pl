---
title: Instalowanie i używanie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet
description: Samouczek instruktażowy dotyczący procesu instalowania i używania pakietu NuGet w projekcie .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 9b6eb012b4bc8135b1648fa9f5e84d7d1c9d6b16
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825351"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>Szybki Start: Instalowanie i używanie pakietu przy użyciu interfejsu wiersza polecenia dotnet

Pakiety NuGet zawierają kod wielokrotnego użytku, który inni deweloperzy udostępnili do użycia w projektach. Zobacz, [co to jest NuGet?](../What-is-NuGet.md) w tle. Pakiety są instalowane w projekcie .NET Core za pomocą polecenia `dotnet add package`, zgodnie z opisem w tym artykule dla popularnego pakietu [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) .

Po zainstalowaniu programu zapoznaj się z pakietem w kodzie, `using <namespace>` gdzie \<przestrzeń nazw\> jest specyficzna dla używanego pakietu. Następnie można użyć interfejsu API pakietu.

> [!Tip]
> **Zacznij od NuGet.org**: przeglądanie NuGet.org polega na tym, że deweloperzy platformy .NET zwykle wyszukują składniki, których mogą ponownie używać w swoich aplikacjach. Możesz przeszukiwać nuget.org bezpośrednio lub znajdować i instalować pakiety w programie Visual Studio, jak pokazano w tym artykule.

## <a name="prerequisites"></a>Wymagania wstępne

- [Zestaw .NET Core SDK](https://www.microsoft.com/net/download/), która zapewnia `dotnet` narzędzie wiersza polecenia. Począwszy od programu Visual Studio 2017, interfejs wiersza polecenia dotnet jest automatycznie instalowany z dowolnymi obciążeniami związanymi z platformą .NET Core.

## <a name="create-a-project"></a>Tworzenie projektu

Pakiety NuGet można instalować w projekcie .NET pewnego rodzaju. W tym instruktażu Utwórz prosty projekt konsoli programu .NET Core w następujący sposób:

1. Utwórz folder dla projektu.

1. Otwórz wiersz polecenia i przejdź do nowego folderu.

1. Utwórz projekt przy użyciu następującego polecenia:

    ```dotnetcli
    dotnet new console
    ```

1. Użyj `dotnet run`, aby sprawdzić, czy aplikacja została utworzona poprawnie.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Dodawanie pakietu NuGet Newtonsoft. JSON

1. Aby zainstalować pakiet `Newtonsoft.json`, użyj następującego polecenia:

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. Po zakończeniu wykonywania polecenia Otwórz plik `.csproj`, aby wyświetlić dodane odwołanie:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Korzystanie z interfejsu API Newtonsoft. JSON w aplikacji

1. Otwórz plik `Program.cs` i Dodaj następujący wiersz w górnej części pliku:

    ```cs
    using Newtonsoft.Json;
    ```

1. Dodaj następujący kod przed wierszem `class Program`:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. Zastąp funkcję `Main` następującym:

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

1. Skompiluj i uruchom aplikację za pomocą polecenia `dotnet run`. Dane wyjściowe powinny być reprezentacją JSON obiektu `Account` w kodzie:

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="next-steps"></a>Następne kroki

Gratulacje z myślą o instalowaniu i używaniu pierwszego pakietu NuGet!

> [!div class="nextstepaction"]
> [Instalowanie i używanie pakietów przy użyciu interfejsu wiersza polecenia dotnet](../consume-packages/install-use-packages-dotnet-cli.md)

Aby poznać więcej informacji o tym, że pakiet NuGet jest oferowany, wybierz poniższe linki.

- [Omówienie użycia pakietu i przepływ pracy](../consume-packages/overview-and-workflow.md)
- [Znajdowanie i wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md)
- [Odwołania do pakietu w plikach projektu](../consume-packages/package-references-in-project-files.md)
