---
title: "Przewodnik wprowadzający do tworzenia i publikowania pakietu NuGet dotnet interfejsu wiersza polecenia | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/24/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Samouczek wskazówki na temat tworzenia i publikowania za pomocą .NET Core CLI, platformy dotnet pakietu NuGet."
keywords: Pakiet NuGet tworzenie, publikowanie pakietu NuGet, samouczek NuGet pakietu NuGet publikowania dotnet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c9f46cafafcdc238e43979d6f05521e19bf3d7f6
ms.sourcegitcommit: eabd401616a98dda2ae6293612acb3b81b584967
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/09/2018
---
# <a name="create-and-publish-a-package"></a>Tworzenie i publikowanie pakietu

Jest to prosty proces tworzenia pakietów NuGet z biblioteki klas .NET i opublikować go za pomocą nuget.org `dotnet` interfejsu wiersza polecenia (CLI).

## <a name="pre-requisites"></a>Wymagania wstępne

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

Aby utworzyć pakiet NuGet ( `.nupkg` pliku) w projekcie, uruchom `dotnet pack` polecenia:

```cli
# Uses the project file in the current folder by default
dotnet pack
```

Dane wyjściowe będą pokazywały ścieżkę do `.nupkg` pliku:

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

## <a name="publish-the-package"></a>Publikowanie pakietu

Po utworzeniu `.nupkg` pliku opublikowaniu go przy użyciu nuget.org `dotnet nuget push` polecenia wraz z kluczem interfejsu API z nuget.org.

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Uzyskanie klucza interfejsu API

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a>Publikowanie za pomocą wypychania nuget dotnet

[!INCLUDE[publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Publikowanie błędów

[!INCLUDE[publish-errors](includes/publish-errors.md)]


### <a name="manage-the-published-package"></a>Zarządzanie opublikowanego pakietu

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>Tematy pokrewne

- [Tworzenie pakietu](../create-packages/creating-a-package.md)
- [Publikowanie pakietu](../create-packages/publish-a-package.md)
- [Obsługuje wiele platform docelowych](../create-packages/supporting-multiple-target-frameworks.md)
- [Przechowywanie wersji pakietów](../reference/package-versioning.md)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
