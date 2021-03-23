---
title: Instalowanie i używanie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet
description: Samouczek instruktażowy dotyczący procesu instalowania i używania pakietu NuGet w projekcie .NET Core.
author: JonDouglas
ms.author: jodou
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: dbe1d3ee8e50a90803140bc2c5cb5821b485a2fd
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859437"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>Szybki Start: Instalowanie i używanie pakietu przy użyciu interfejsu wiersza polecenia dotnet

Pakiety NuGet zawierają kod wielokrotnego użytku, który inni deweloperzy udostępnili do użycia w projektach. Zobacz, [co to jest NuGet?](../What-is-NuGet.md) w tle. Pakiety są instalowane w projekcie .NET Core za pomocą `dotnet add package` polecenia zgodnie z opisem w tym artykule dla popularnego [Newtonsoft.Jsw](https://www.nuget.org/packages/Newtonsoft.Json/) pakiecie.

Po zainstalowaniu programu zapoznaj się z pakietem w kodzie, `using <namespace>` gdzie \<namespace\> jest specyficzny dla używanego pakietu. Następnie można użyć interfejsu API pakietu.

> [!Tip]
> **Zacznij od NuGet.org**: przeglądanie NuGet.org polega na tym, że deweloperzy platformy .NET zwykle wyszukują składniki, których mogą ponownie używać w swoich aplikacjach. Możesz przeszukiwać nuget.org bezpośrednio lub znajdować i instalować pakiety w programie Visual Studio, jak pokazano w tym artykule.

## <a name="prerequisites"></a>Wymagania wstępne

- [Zestaw .NET Core SDK](https://www.microsoft.com/net/download/), która udostępnia `dotnet` Narzędzie wiersza polecenia. Począwszy od programu Visual Studio 2017, interfejs wiersza polecenia dotnet jest automatycznie instalowany z dowolnymi obciążeniami związanymi z platformą .NET Core.

## <a name="create-a-project"></a>Tworzenie projektu

Pakiety NuGet można instalować w projekcie .NET pewnego rodzaju. W tym instruktażu Utwórz prosty projekt konsoli programu .NET Core w następujący sposób:

1. Utwórz folder dla projektu.

1. Otwórz wiersz polecenia i przejdź do nowego folderu.

1. Utwórz projekt przy użyciu następującego polecenia:

    ```dotnetcli
    dotnet new console
    ```

1. Użyj `dotnet run` , aby sprawdzić, czy aplikacja została utworzona poprawnie.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Dodaj Newtonsoft.Jsw pakiecie NuGet

1. Użyj następującego polecenia, aby zainstalować `Newtonsoft.json` pakiet:

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. Po zakończeniu wykonywania polecenia Otwórz plik, `.csproj` Aby wyświetlić dodane odwołanie:

    ```xml
    <ItemGroup>
      <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
    </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Używanie Newtonsoft.Jsw interfejsie API w aplikacji

1. Otwórz `Program.cs` plik i Dodaj następujący wiersz w górnej części pliku:

    ```cs
    using Newtonsoft.Json;
    ```

1. Dodaj następujący kod przed `class Program` wierszem:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. Zastąp `Main` funkcję następującymi:

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

1. Skompiluj i uruchom aplikację za pomocą `dotnet run` polecenia. Dane wyjściowe powinny być reprezentacją JSON `Account` obiektu w kodzie:

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```
## <a name="related-video"></a>Pokrewne wideo

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-the-NET-CLI-3-of-5/player]

Znajdź więcej filmów wideo NuGet w witrynie [Channel 9](https://channel9.msdn.com/Series/NuGet-101) i [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="next-steps"></a>Następne kroki

Gratulacje z myślą o instalowaniu i używaniu pierwszego pakietu NuGet!

> [!div class="nextstepaction"]
> [Instalowanie i używanie pakietów przy użyciu interfejsu wiersza polecenia dotnet](../consume-packages/install-use-packages-dotnet-cli.md)

Aby poznać więcej informacji o tym, że pakiet NuGet jest oferowany, wybierz poniższe linki.

- [Omówienie użycia pakietu i przepływ pracy](../consume-packages/overview-and-workflow.md)
- [Znajdowanie i wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md)
- [Odwołania do pakietu w plikach projektu](../consume-packages/package-references-in-project-files.md)
