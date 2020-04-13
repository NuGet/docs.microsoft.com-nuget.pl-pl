---
title: Tworzenie i publikowanie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet
description: Samouczek instruktażowy dotyczący tworzenia i publikowania pakietu NuGet przy użyciu interfejsu wiersza polecenia .NET Core, dotnet.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 8c09d6d5662ed6ff0deffa5d45b823ad0992f399
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231308"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a>Szybki start: tworzenie i publikowanie pakietu (dotnet CLI)

Jest to prosty proces, aby utworzyć pakiet NuGet z biblioteki klas .NET `dotnet` i opublikować go do nuget.org przy użyciu interfejsu wiersza polecenia (CLI).

## <a name="prerequisites"></a>Wymagania wstępne

1. Zainstaluj zestaw [SDK .NET](https://www.microsoft.com/net/download/)Core `dotnet` , który zawiera zestaw wiersza polecenia. Począwszy od programu Visual Studio 2017, dotnet interfejsu wiersza polecenia jest automatycznie instalowany z dowolnego .NET Core obciążeń związanych.

1. [Zarejestruj się na darmowe konto w nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) jeśli jeszcze go nie masz. Utworzenie nowego konta wysyła wiadomość e-mail z potwierdzeniem. Musisz potwierdzić konto, zanim będzie można przesłać pakiet.

## <a name="create-a-class-library-project"></a>Tworzenie projektu biblioteki klas

Można użyć istniejącego projektu biblioteki klas platformy .NET dla kodu, który chcesz spakować, lub utworzyć prosty w następujący sposób:

1. Tworzenie folderu `AppLogger`o nazwie .

1. Otwórz wiersz polecenia i `AppLogger` przełącz się do folderu.

1. Typ `dotnet new classlib`, który używa nazwy bieżącego folderu dla projektu.

   Spowoduje to utworzenie nowego projektu.

## <a name="add-package-metadata-to-the-project-file"></a>Dodawanie metadanych pakietu do pliku projektu

Każdy pakiet NuGet potrzebuje manifestu, który opisuje zawartość i zależności pakietu. W pakiecie końcowym manifest jest `.nuspec` plikiem, który jest generowany z właściwości metadanych NuGet, które można uwzględnić w pliku projektu.

1. Otwórz plik projektu`.csproj`( ) i dodaj następujące `<PropertyGroup>` minimalne właściwości wewnątrz istniejącego tagu, zmieniając odpowiednie wartości:

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > Nadaj pakietowi identyfikator, który jest unikatowy w nuget.org lub dowolnym hostie, którego używasz. W tym instruktażu zalecamy dołączenie "Przykład" lub "Test" w nazwie, ponieważ późniejszy krok publikowania powoduje, że pakiet jest publicznie widoczny (choć jest mało prawdopodobne, aby ktoś go faktycznie używał).

1. Dodaj wszystkie opcjonalne właściwości opisane we [właściwościach metadanych NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

    > [!Note]
    > W przypadku pakietów przeznaczonych do użytku publicznego należy zwrócić szczególną uwagę na **PackageTags** właściwości, jak tagi pomóc innym znaleźć pakiet i zrozumieć, co robi.

## <a name="run-the-pack-command"></a>Uruchamianie polecenia pack

Aby utworzyć pakiet NuGet `.nupkg` (plik) z projektu, uruchom `dotnet pack` polecenie, które również automatycznie tworzy projekt:

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

Dane wyjściowe pokazują `.nupkg` ścieżkę do pliku:

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Automatyczne generowanie pakietu na kompilacji

Aby uruchomić `dotnet pack` je automatycznie `dotnet build`po uruchomieniu, dodaj następujący `<PropertyGroup>`wiersz do pliku projektu w obrębie:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a>Publikowanie pakietu

Po opublikowaniu `.nupkg` pliku, aby opublikować go do `dotnet nuget push` nuget.org przy użyciu polecenia wraz z kluczem interfejsu API nabyte z nuget.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Uzyskaj klucz interfejsu API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a>Publikuj z dotnet nuget push

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Błędy publikowania

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Zarządzanie opublikowanym pakietem

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-video"></a>Podobne wideo

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-the-NET-CLI-5-of-5/player]

Znajdź więcej filmów NuGet na [Channel 9](https://channel9.msdn.com/Series/NuGet-101) i [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="next-steps"></a>Następne kroki

Gratulujemy stworzenia pierwszego pakietu NuGet!

> [!div class="nextstepaction"]
> [Tworzenie pakietu](../create-packages/creating-a-package-dotnet-cli.md)

Aby dowiedzieć się więcej, że NuGet ma do zaoferowania, wybierz poniższe łącza.

- [Publikowanie pakietu](../nuget-org/publish-a-package.md)
- [Pakiety w wersji wstępnej](../create-packages/Prerelease-Packages.md)
- [Obsługa wielu platform docelowych](../create-packages/multiple-target-frameworks-project-file.md)
- [Przechowywanie wersji pakietów](../concepts/package-versioning.md)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
- [Tworzenie pakietów symboli](../create-packages/symbol-packages-snupkg.md)
- [Podpisywanie pakietów](../create-packages/Sign-a-package.md)
