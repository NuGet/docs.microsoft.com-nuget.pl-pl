---
title: Instalowanie i używanie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet
description: Samouczek instruktażowy na temat procesu instalowania i używania pakietu NuGet w projekcie .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 006fff8360ac62393e4b88c1a253514591d22f4c
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231281"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>Szybki start: instalowanie i używanie pakietu przy użyciu interfejsu wiersza polecenia dotnet

Pakiety NuGet zawierają kod wielokrotnego użytku, który inni deweloperzy udostępniają do użycia w projektach. Zobacz [Co to jest NuGet?](../What-is-NuGet.md) w tle. Pakiety są instalowane w `dotnet add package` projekcie .NET Core przy użyciu polecenia opisanego w tym artykule dla popularnego pakietu [Newtonsoft.Json.](https://www.nuget.org/packages/Newtonsoft.Json/)

Po zainstalowaniu należy zapoznać `using <namespace>` się \<z\> pakietem w kodzie, w którym obszar nazw jest specyficzny dla używanego pakietu. Następnie można użyć interfejsu API pakietu.

> [!Tip]
> **Zacznij od nuget.org:** Przeglądanie nuget.org to sposób, w jaki deweloperzy platformy .NET zazwyczaj znajdują składniki, których mogą ponownie wykorzystać we własnych aplikacjach. Można wyszukiwać nuget.org bezpośrednio lub znaleźć i zainstalować pakiety w programie Visual Studio, jak pokazano w tym artykule.

## <a name="prerequisites"></a>Wymagania wstępne

- Zestaw [SDK .NET Core](https://www.microsoft.com/net/download/) `dotnet` , który udostępnia narzędzie wiersza polecenia. Począwszy od programu Visual Studio 2017, dotnet interfejsu wiersza polecenia jest automatycznie instalowany z dowolnego .NET Core obciążeń związanych.

## <a name="create-a-project"></a>Tworzenie projektu

Pakiety NuGet mogą być instalowane w projekcie .NET pewnego rodzaju. W tym instruktażu utwórz prosty projekt konsoli .NET Core w następujący sposób:

1. Utwórz folder dla projektu.

1. Otwórz wiersz polecenia i przełącz się do nowego folderu.

1. Utwórz projekt za pomocą następującego polecenia:

    ```dotnetcli
    dotnet new console
    ```

1. Służy `dotnet run` do testowania, czy aplikacja została utworzona poprawnie.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Dodaj pakiet Newtonsoft.Json NuGet

1. Aby zainstalować pakiet, `Newtonsoft.json` użyj następującego polecenia:

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. Po zakończeniu polecenia otwórz `.csproj` plik, aby wyświetlić dodane odwołanie:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Korzystanie z interfejsu API Newtonsoft.Json w aplikacji

1. Otwórz `Program.cs` plik i dodaj następujący wiersz u góry pliku:

    ```cs
    using Newtonsoft.Json;
    ```

1. Dodaj następujący kod `class Program` przed wierszem:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. Zastąp `Main` funkcję na następujące:

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

1. Tworzenie i uruchamianie aplikacji `dotnet run` za pomocą polecenia. Dane wyjściowe powinny być reprezentacją JSON `Account` obiektu w kodzie:

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```
## <a name="related-video"></a>Podobne wideo

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-the-NET-CLI-3-of-5/player]

Znajdź więcej filmów NuGet na [Channel 9](https://channel9.msdn.com/Series/NuGet-101) i [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="next-steps"></a>Następne kroki

Gratulujemy instalacji i korzystania z pierwszego pakietu NuGet!

> [!div class="nextstepaction"]
> [Instalowanie i używanie pakietów przy użyciu interfejsu wiersza polecenia dotnet](../consume-packages/install-use-packages-dotnet-cli.md)

Aby dowiedzieć się więcej, że NuGet ma do zaoferowania, wybierz poniższe łącza.

- [Omówienie i przepływ pracy zużycia pakietów](../consume-packages/overview-and-workflow.md)
- [Znajdowanie i wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md)
- [Odwołania do pakietu w plikach projektu](../consume-packages/package-references-in-project-files.md)
