---
title: Tworzenie i publikowanie pakietu NuGet dotnet interfejsu wiersza polecenia
description: Samouczek wskazówki na temat tworzenia i publikowania za pomocą .NET Core CLI, platformy dotnet pakietu NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/24/2018
ms.topic: quickstart
ms.openlocfilehash: c50c92f966cd68477cd3f29ab99857911299b7ea
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818454"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a>Szybki Start: Tworzenie i publikowanie pakietu (dotnet CLI)

Jest to prosty proces tworzenia pakietów NuGet z biblioteki klas .NET i opublikować go za pomocą nuget.org `dotnet` interfejsu wiersza polecenia (CLI).

## <a name="prerequisites"></a>Wymagania wstępne

1. Zainstaluj [.NET Core SDK](https://www.microsoft.com/net/download/), która obejmuje `dotnet` interfejsu wiersza polecenia.

1. [Zarejestruj bezpłatne konto na nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Jeśli nie masz już. Tworzenie nowego konta wysyła wiadomość e-mail z potwierdzeniem. Aby przekazać pakiet, musisz potwierdzić konto.

## <a name="create-a-class-library-project"></a>Tworzenie projektu biblioteki klas

Można użyć istniejącego projektu biblioteki klas .NET dla kodu, który ma być pakietu lub Utwórz proste w następujący sposób:

1. Utwórz folder o nazwie `AppLogger` i zmiany do niego.

1. Utwórz projekt za pomocą `dotnet new classlib`, która używa nazwy folderu bieżącego projektu.

## <a name="add-package-metadata-to-the-project-file"></a>Dodaj metadane pakietów do pliku projektu

Każdy pakiet NuGet musi manifestu, który opisuje zawartość pakietu i zależności. W ostatnim pakiecie plik manifestu to `.nuspec` pliku, który jest generowany na podstawie właściwości metadanych NuGet, które obejmują w pliku projektu.

1. Otwórz plik projektu (`.csproj`) i dodaj następujące minimalne właściwości wewnątrz Kończenie `<PropertyGroup>` tag, zmiana wartości zależnie od potrzeb:

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > Nadaj pakietu używany unikatowy identyfikator w nuget.org lub niezależnie od hosta można. W ramach tego przewodnika, zaleca się tym "Sample" lub "Test" w nazwie, ponieważ kolejnych kroków publikowania pakietu widocznego publicznie (chociaż jest mało prawdopodobne, każda osoba, która zostanie rzeczywiście używane).

1. Dodać opcjonalne właściwości opisu w [właściwości metadanych NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

    > [!Note]
    > W przypadku pakietów skompilowany dla publicznych zużycia zwrócić szczególną uwagę na **PackageTags** właściwości, jak tagi ułatwiała innym pakietu odnaleźć i zrozumieć, jakie operacje.

## <a name="run-the-pack-command"></a>Uruchom polecenie pakietu

Aby utworzyć pakiet NuGet ( `.nupkg` pliku) w projekcie, uruchom `dotnet pack` polecenia, które również automatycznie tworzy projekt:

```cli
# Uses the project file in the current folder by default
dotnet pack
```

Dane wyjściowe zawierają ścieżki do `.nupkg` pliku:

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Automatyczne generowanie pakietu podczas kompilacji

Aby automatycznie uruchomić `dotnet pack` po uruchomieniu `dotnet build`, Dodaj następujący wiersz w pliku projektu w `<PropertyGroup>`:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a>Publikowanie pakietu

Po utworzeniu `.nupkg` pliku opublikowaniu go przy użyciu nuget.org `dotnet nuget push` polecenia wraz z kluczem interfejsu API z nuget.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Uzyskanie klucza interfejsu API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a>Publikowanie za pomocą wypychania nuget dotnet

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Publikowanie błędów

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Zarządzanie opublikowanego pakietu

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>Tematy pokrewne

- [Tworzenie pakietu](../create-packages/creating-a-package.md)
- [Publikowanie pakietu](../create-packages/publish-a-package.md)
- [Pakiety wersji wstępnej](../create-packages/Prerelease-Packages.md)
- [Obsługuje wiele platform docelowych](../create-packages/supporting-multiple-target-frameworks.md)
- [Przechowywanie wersji pakietów](../reference/package-versioning.md)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
- [Podpisywanie pakietów](../create-packages/Sign-a-package.md)
