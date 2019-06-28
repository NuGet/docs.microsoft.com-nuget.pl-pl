---
title: Tworzenie i publikowanie pakietu NuGet za pomocą interfejsu wiersza polecenia platformy dotnet
description: Samouczek wskazówki na temat tworzenia i publikowania pakietu NuGet za pomocą platformy .NET Core interfejsu wiersza polecenia dotnet.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 051fcc355fb78c0ab208125c2295b6316236fd46
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426361"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a>Szybki start: Tworzenie i publikowanie pakietu (wiersz polecenia dotnet wim)

Jest to prosty proces, aby utworzyć pakiet NuGet z biblioteki klas .NET i opublikuj go w witrynie nuget.org przy użyciu `dotnet` interfejsu wiersza polecenia (CLI).

## <a name="prerequisites"></a>Wymagania wstępne

1. Zainstaluj [zestawu .NET Core SDK](https://www.microsoft.com/net/download/), która obejmuje `dotnet` interfejsu wiersza polecenia.

1. [Zarejestruj, aby utworzyć bezpłatne konto w witrynie nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Jeśli nie masz jeszcze takiego. Tworzenie nowego konta wysyła wiadomość e-mail z potwierdzeniem. Aby można było przekazać pakiet, należy potwierdzić konto.

## <a name="create-a-class-library-project"></a>Utwórz projekt biblioteki klas

Można użyć istniejącego projektu biblioteki klas platformy .NET dla kodu, który ma być pakietu lub Utwórz proste w następujący sposób:

1. Utwórz folder o nazwie `AppLogger` i zmienić tę sytuację.

1. Utwórz projekt za pomocą `dotnet new classlib`, który używa nazwy bieżącego folderu projektu.

## <a name="add-package-metadata-to-the-project-file"></a>Dodaj metadane pakietu do pliku projektu

Każdy pakiet NuGet musi manifestu, który opisuje zawartość pakietu i jego zależności. W ostatnim pakiecie manifestu to `.nuspec` pliku, który jest generowany na podstawie właściwości metadanych NuGet, które zawierają w pliku projektu.

1. Otwórz plik projektu (`.csproj`) i dodaj następujące minimalne właściwości wewnątrz istniejącego `<PropertyGroup>` tagu, zmieniając wartości zgodnie z potrzebami:

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > Przekazać pakiet identyfikator, który jest unikatowa w obrębie nuget.org, lub niezależnie od rodzaju hoście jest używany. W ramach tego przewodnika firma Microsoft zaleca, tym "Próbny" lub "Test" w nazwie późniejszym etapie publikowania uwidocznić pakietu publicznie (choć jest mało prawdopodobne, każda osoba będzie faktycznie używać).

1. Dodaj wszelkie opcjonalne właściwości opisanych na [właściwości metadanych NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

    > [!Note]
    > Pakiety utworzone do użytku publicznego, należy zwrócić szczególną uwagę na **PackageTags** właściwości, jak tagi pomóc innym odnaleźć pakietu i zrozumieć, co robi.

## <a name="run-the-pack-command"></a>Uruchom polecenie pakietu

Tworzenie pakietu NuGet ( `.nupkg` plik) z projektu, uruchom `dotnet pack` polecenia, które sprzyja wytwarzaniu się odpowiednich projektu automatycznie:

```cli
# Uses the project file in the current folder by default
dotnet pack
```

Dane wyjściowe zawierają ścieżkę do `.nupkg` pliku:

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Automatyczne generowanie pakietu w kompilacji

Aby automatycznie uruchomić `dotnet pack` po uruchomieniu `dotnet build`, Dodaj następujący wiersz do pliku projektu w ramach `<PropertyGroup>`:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a>Publikowanie pakietu

Po utworzeniu `.nupkg` pliku opublikujesz go w witrynie nuget.org przy użyciu `dotnet nuget push` polecenia wraz z kluczem API uzyskanych z repozytorium nuget.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Uzyskiwanie klucza interfejsu API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a>Publikowanie za pomocą polecenia dotnet nuget wypychania

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Publikowanie błędy

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Zarządzanie opublikowany pakiet

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>Tematy pokrewne

- [Utwórz pakiet](../create-packages/creating-a-package.md)
- [Publikowanie pakietu](../nuget-org/publish-a-package.md)
- [Pakiety w wersji wstępnej](../create-packages/Prerelease-Packages.md)
- [Obsługa wielu platform docelowych](../create-packages/supporting-multiple-target-frameworks.md)
- [Przechowywanie wersji pakietów](../reference/package-versioning.md)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
- [Tworzenie pakietów symboli](../create-packages/symbol-packages-snupkg.md)
- [Podpisywanie pakietów](../create-packages/Sign-a-package.md)
