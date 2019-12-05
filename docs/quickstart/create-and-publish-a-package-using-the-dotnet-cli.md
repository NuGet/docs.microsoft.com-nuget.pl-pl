---
title: Tworzenie i publikowanie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet
description: Samouczek instruktażowy dotyczący tworzenia i publikowania pakietu NuGet przy użyciu interfejs wiersza polecenia platformy .NET Core, dotnet.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 55f9c760ae05f060b748e6fbb82d8e9bd77c4e37
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825318"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a>Szybki Start: Tworzenie i publikowanie pakietu (interfejs wiersza polecenia dotnet)

Jest to prosty proces tworzenia pakietu NuGet z biblioteki klas .NET i publikowania go do nuget.org przy użyciu interfejsu wiersza polecenia `dotnet` (CLI).

## <a name="prerequisites"></a>Wymagania wstępne

1. Zainstaluj [zestaw .NET Core SDK](https://www.microsoft.com/net/download/), który zawiera `dotnet` interfejsu wiersza polecenia. Począwszy od programu Visual Studio 2017, interfejs wiersza polecenia dotnet jest automatycznie instalowany z dowolnymi obciążeniami związanymi z platformą .NET Core.

1. [Zarejestruj się, aby korzystać z bezpłatnego konta w usłudze NuGet.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) , jeśli jeszcze go nie masz. Utworzenie nowego konta spowoduje wysłanie wiadomości e-mail z potwierdzeniem. Musisz potwierdzić konto, aby można było przekazać pakiet.

## <a name="create-a-class-library-project"></a>Tworzenie projektu biblioteki klas

Można użyć istniejącego projektu biblioteki klas .NET dla kodu, który ma zostać spakowany, lub utworzyć prosty jeden w następujący sposób:

1. Utwórz folder o nazwie `AppLogger`.

1. Otwórz wiersz polecenia i przejdź do folderu `AppLogger`.

1. Wpisz `dotnet new classlib`, który używa nazwy bieżącego folderu dla projektu.

   Spowoduje to utworzenie nowego projektu.

## <a name="add-package-metadata-to-the-project-file"></a>Dodawanie metadanych pakietu do pliku projektu

Każdy pakiet NuGet wymaga manifestu opisującego zawartość pakietu i jego zależności. W pakiecie końcowym manifest jest plikiem `.nuspec`, który jest generowany na podstawie właściwości metadanych NuGet, które są zawarte w pliku projektu.

1. Otwórz plik projektu (`.csproj`) i Dodaj następujące minimalne właściwości w istniejącym tagu `<PropertyGroup>`, zmieniając wartości zgodnie z potrzebami:

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > Nadaj pakietowi identyfikator, który jest unikatowy w obrębie nuget.org lub dowolnego hosta, którego używasz. W tym instruktażu Zalecamy uwzględnienie "przykładowego" lub "testowego" w nazwie, jak w późniejszym kroku publikowania sprawia, że pakiet jest widoczny publicznie (chociaż prawdopodobnie nikt się nie używa).

1. Dodaj wszystkie opcjonalne właściwości opisane we [właściwościach metadanych NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

    > [!Note]
    > W przypadku pakietów przeznaczonych do użycia publicznego należy zwrócić szczególną uwagę na Właściwość **PackageTags** , ponieważ Tagi ułatwiają innym znalezienie pakietu i zrozumienie jego działania.

## <a name="run-the-pack-command"></a>Uruchom pakiet polecenie

Aby skompilować pakiet NuGet (plik `.nupkg`) z projektu, uruchom polecenie `dotnet pack`, które również automatycznie kompiluje projekt:

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

Dane wyjściowe przedstawiają ścieżkę do pliku `.nupkg`:

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Automatycznie Generuj pakiet podczas kompilacji

Aby automatycznie uruchomić `dotnet pack` podczas uruchamiania `dotnet build`, Dodaj następujący wiersz do pliku projektu w `<PropertyGroup>`:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a>Publikowanie pakietu

Gdy masz plik `.nupkg`, opublikujesz go w usłudze nuget.org przy użyciu polecenia `dotnet nuget push` wraz z kluczem interfejsu API uzyskanym z nuget.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Pozyskiwanie klucza interfejsu API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a>Publikowanie przy użyciu wypychania NuGet programu dotnet

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Błędy publikowania

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Zarządzanie opublikowanym pakietem

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a>Następne kroki

Gratulujemy utworzenia pierwszego pakietu NuGet!

> [!div class="nextstepaction"]
> [Tworzenie pakietu](../create-packages/creating-a-package-dotnet-cli.md)

Aby poznać więcej informacji o tym, że pakiet NuGet jest oferowany, wybierz poniższe linki.

- [Publikowanie pakietu](../nuget-org/publish-a-package.md)
- [Pakiety wersji wstępnej](../create-packages/Prerelease-Packages.md)
- [Obsługa wielu platform docelowych](../create-packages/multiple-target-frameworks-project-file.md)
- [Przechowywanie wersji pakietów](../concepts/package-versioning.md)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
- [Tworzenie pakietów symboli](../create-packages/symbol-packages-snupkg.md)
- [Podpisywanie pakietów](../create-packages/Sign-a-package.md)
