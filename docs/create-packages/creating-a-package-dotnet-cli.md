---
title: Tworzenie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet
description: Szczegółowy przewodnik dotyczący procesu projektowania i tworzenia pakietu NuGet, w tym najważniejszych punktów decyzyjnych, takich jak pliki i przechowywanie wersji.
author: JonDouglas
ms.author: jodou
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 4771a30ee2ff73e68154d05f1c84efd90b584162
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774481"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a>Tworzenie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet

Niezależnie od tego, co Twój pakiet lub jaki kod zawiera, użyj jednego z narzędzi interfejsu wiersza polecenia `nuget.exe` lub `dotnet.exe` , aby spakować tę funkcję do składnika, który może być współużytkowany i używany przez dowolną liczbę innych deweloperów. W tym artykule opisano sposób tworzenia pakietu przy użyciu interfejsu wiersza polecenia dotnet. Aby zainstalować `dotnet` interfejs wiersza polecenia, zobacz [Instalowanie narzędzi klienckich programu NuGet](../install-nuget-client-tools.md). Począwszy od programu Visual Studio 2017, interfejs wiersza polecenia dotnet jest dołączany do obciążeń .NET Core.

W przypadku projektów .NET Core i .NET Standard, które korzystają z [formatu zestawu SDK](../resources/check-project-format.md)i innych projektów w stylu zestawu SDK, NuGet używa informacji w pliku projektu bezpośrednio do tworzenia pakietu. Aby zapoznać się z samouczkami krok po kroku, zobacz [Tworzenie pakietów .NET standard za pomocą interfejsu wiersza polecenia dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) lub [Tworzenie pakietów .NET standard przy użyciu programu Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).

`msbuild -t:pack` Funkcja jest równoważna z `dotnet pack` . Aby skompilować przy użyciu programu MSBuild, zobacz [Tworzenie pakietu NuGet przy użyciu programu MSBuild](creating-a-package-msbuild.md).

> [!IMPORTANT]
> Ten temat ma zastosowanie do projektów w [stylu zestawu SDK](../resources/check-project-format.md) , zwykle .NET Core i projektów .NET Standard.

## <a name="set-properties"></a>Ustawianie właściwości

Do utworzenia pakietu wymagane są następujące właściwości.

- `PackageId`Identyfikator pakietu, który musi być unikatowy w galerii, w której znajduje się pakiet. Jeśli nie zostanie określony, wartość domyślna to `AssemblyName` .
- `Version`, określony numer wersji w postaci *główna. pomocnicza. poprawka [-sufiks]* , gdzie *-sufiks* określa [wersję wstępną](prerelease-packages.md). Jeśli nie zostanie określony, wartość domyślna to 1.0.0.
- Tytuł pakietu, który powinien pojawić się na hoście (na przykład nuget.org)
- `Authors`Informacje o autorze i właścicielu. Jeśli nie zostanie określony, wartość domyślna to `AssemblyName` .
- `Company`, nazwa firmy. Jeśli nie zostanie określony, wartość domyślna to `AssemblyName` .

W programie Visual Studio można ustawić te wartości we właściwościach projektu (kliknij prawym przyciskiem myszy projekt w Eksplorator rozwiązań, wybierz **Właściwości**, a następnie wybierz kartę **pakiet** ). Możesz również ustawić te właściwości bezpośrednio w plikach projektu ( `.csproj` ).

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> Nadaj pakietowi identyfikator, który jest unikatowy w obrębie nuget.org lub dowolnego źródła pakietów, którego używasz.

Poniższy przykład pokazuje prosty, kompletny plik projektu z tymi właściwościami. (Nowy projekt domyślny można utworzyć przy użyciu `dotnet new classlib` polecenia).

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

Można również ustawić właściwości opcjonalne, takie jak `Title` , `PackageDescription` , i `PackageTags` , zgodnie z opisem w obszarze [targets pakietu MSBuild](../reference/msbuild-targets.md#pack-target), [kontrolować zasoby zależności](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)i [właściwości metadanych NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

> [!NOTE]
> W przypadku pakietów przeznaczonych do użycia publicznego należy zwrócić szczególną uwagę na Właściwość **PackageTags** , ponieważ Tagi ułatwiają innym znalezienie pakietu i zrozumienie jego działania.

Aby uzyskać szczegółowe informacje na temat deklarowania zależności i określania numerów wersji, zobacz [odwołania do pakietów w plikach projektu](../consume-packages/package-references-in-project-files.md) i [przechowywanie wersji pakietu](../concepts/package-versioning.md). Istnieje również możliwość, że zasoby są zależne od zależności bezpośrednio w pakiecie przy użyciu `<IncludeAssets>` `<ExcludeAssets>` atrybutów i. Aby uzyskać więcej informacji, zobacz [kontrolowanie elementów zależnych](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

## <a name="add-an-optional-description-field"></a>Dodaj opcjonalne pole opisu

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>Wybierz unikatowy identyfikator pakietu i ustaw numer wersji

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a>Uruchom pakiet polecenie

Aby skompilować pakiet NuGet ( `.nupkg` plik) z projektu, uruchom `dotnet pack` polecenie, które również automatycznie kompiluje projekt:

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

Dane wyjściowe przedstawiają ścieżkę do `.nupkg` pliku.

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Automatycznie Generuj pakiet podczas kompilacji

Aby automatycznie uruchomić `dotnet pack` `dotnet build` program, Dodaj następujący wiersz do pliku projektu w `<PropertyGroup>` :

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

Po uruchomieniu `dotnet pack` w rozwiązaniu to pakiety wszystkie projekty w rozwiązaniu, które są możliwe do spakowania ( [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) Właściwość jest ustawiona na `true` ).

> [!NOTE]
> Po automatycznym wygenerowaniu pakietu czas do spakowania zwiększa czas kompilacji projektu.

### <a name="test-package-installation"></a>Instalacja pakietu testowego

Przed opublikowaniem pakietu zazwyczaj należy przetestować proces instalacji pakietu w projekcie. Testy upewniają się, że wszystkie niezbędne pliki kończą się w ich prawidłowych miejscach w projekcie.

Instalacje można testować ręcznie w programie Visual Studio lub w wierszu polecenia przy użyciu standardowych [kroków instalacji pakietu](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).

> [!IMPORTANT]
> Pakiety są niezmienne. W przypadku usunięcia problemu należy ponownie zmienić zawartość pakietu i pakietu, po ponownym przetestowaniu nadal będzie używana stara wersja pakietu do momentu [wyczyszczenia folderu pakiety globalne](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) . Jest to szczególnie istotne w przypadku testowania pakietów, które nie używają unikatowej etykiety wersji wstępnej dla każdej kompilacji.

## <a name="next-steps"></a>Następne kroki

Po utworzeniu pakietu, który jest `.nupkg` plikiem, można go opublikować w wybranej galerii, zgodnie z opisem w artykule [Publikowanie pakietu](../nuget-org/publish-a-package.md).

Możesz również chcieć zwiększyć możliwości pakietu lub w inny sposób obsługiwać inne scenariusze zgodnie z opisem w następujących tematach:

- [Przechowywanie wersji pakietów](../concepts/package-versioning.md)
- [Obsługa wielu platform docelowych](../create-packages/multiple-target-frameworks-project-file.md)
- [Dodaj ikonę pakietu](../reference/nuspec.md#icon)
- [Przekształcenia plików źródłowych i konfiguracji](../create-packages/source-and-config-file-transformations.md)
- [Lokalizacja](../create-packages/creating-localized-packages.md)
- [Wersje wstępne](../create-packages/prerelease-packages.md)
- [Ustawianie typu pakietu](../create-packages/set-package-type.md)
- [Tworzenie pakietów z zestawami międzyoperacyjnymi modelu COM](../create-packages/author-packages-with-COM-interop-assemblies.md)

Na koniec należy pamiętać o dodatkowych typach pakietów:

- [Pakiety natywne](../guides/native-packages.md)
- [Pakiety symboli](../create-packages/symbol-packages-snupkg.md)
