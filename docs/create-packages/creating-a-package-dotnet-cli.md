---
title: Tworzenie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet
description: Szczegółowy przewodnik po procesie projektowania i tworzenia pakietu NuGet, w tym kluczowych punktów decyzyjnych, takich jak pliki i przechowywanie wersji.
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 712e4c7159aa9719052330d8e45f63e18e390325
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230590"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a>Tworzenie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet

Bez względu na to, co pakiet robi lub jaki kod zawiera, należy użyć jednego z narzędzi interfejsu wiersza polecenia, albo `nuget.exe` lub `dotnet.exe`, aby spakować tę funkcjonalność do składnika, który może być współużytkowany i używany przez dowolną liczbę innych deweloperów. W tym artykule opisano sposób tworzenia pakietu przy użyciu interfejsu wiersza polecenia dotnet. Aby zainstalować `dotnet` wiersz polecenia, zobacz [Instalowanie narzędzi klienckich NuGet](../install-nuget-client-tools.md). Począwszy od programu Visual Studio 2017, dotnet interfejsu wiersza polecenia jest dołączony do obciążeń .NET Core.

W przypadku projektów .NET Core i .NET Standard, które używają [formatu w stylu zestawu SDK,](../resources/check-project-format.md)oraz innych projektów w stylu zestawu SDK, NuGet używa informacji w pliku projektu bezpośrednio do utworzenia pakietu. Aby uzyskać samouczki krok po kroku, zobacz [Tworzenie pakietów standardowych platformy .NET za pomocą interfejsu wiersza polecenia dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) lub [Tworzenie pakietów standardowych platformy .NET za pomocą programu Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).

`msbuild -t:pack`jest funkcją `dotnet pack`równoważną . Aby tworzyć za pomocą msbuild, zobacz [Tworzenie pakietu NuGet przy użyciu msbuild](creating-a-package-msbuild.md).

> [!IMPORTANT]
> W tym temacie stosuje się do projektów [w stylu SDK,](../resources/check-project-format.md) zazwyczaj .NET Core i .NET Standard projektów.

## <a name="set-properties"></a>Ustawianie właściwości

Następujące właściwości są wymagane do utworzenia pakietu.

- `PackageId`, identyfikator pakietu, który musi być unikatowy w galerii, która obsługuje pakiet. Jeśli nie zostanie określona, wartością domyślną jest `AssemblyName`.
- `Version`, określony numer wersji w postaci *Major.Minor.Patch[-Suffix],* gdzie *-Suffix* identyfikuje [wersje przedpremierowe](prerelease-packages.md). Jeśli nie zostanie określona, wartość domyślna to 1.0.0.
- Tytuł pakietu, który powinien pojawić się na hoście (np. nuget.org)
- `Authors`, informacje o autorze i właścicielu. Jeśli nie zostanie określona, wartością domyślną jest `AssemblyName`.
- `Company`, nazwę firmy. Jeśli nie zostanie określona, wartością domyślną jest `AssemblyName`.

W programie Visual Studio można ustawić te wartości we właściwościach projektu (kliknij prawym przyciskiem myszy projekt w Eksploratorze **rozwiązań,** wybierz polecenie Właściwości i wybierz kartę **Pakiet).** Można również ustawić te właściwości bezpośrednio w`.csproj`plikach projektu ( ).

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> Nadaj pakietowi identyfikator, który jest unikatowy w nuget.org lub niezależnie od źródła pakietu, którego używasz.

W poniższym przykładzie przedstawiono prosty, kompletny plik projektu z tymi właściwościami. (Za pomocą `dotnet new classlib` polecenia można utworzyć nowy projekt domyślny).

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

Można również ustawić właściwości opcjonalne, `Title` `PackageDescription`takie `PackageTags`jak , i , zgodnie z opisem w [msbuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).

> [!NOTE]
> W przypadku pakietów przeznaczonych do użytku publicznego należy zwrócić szczególną uwagę na **PackageTags** właściwości, jak tagi pomóc innym znaleźć pakiet i zrozumieć, co robi.

Aby uzyskać szczegółowe informacje na temat deklarowania zależności i określania numerów wersji, zobacz [Odwołania do pakietów w plikach projektu](../consume-packages/package-references-in-project-files.md) i przechowywanie wersji [pakietu](../concepts/package-versioning.md). Jest również możliwe do powierzchni zasobów z zależności bezpośrednio w `<IncludeAssets>` `<ExcludeAssets>` pakiecie przy użyciu i atrybuty. Aby uzyskać więcej informacji, zobacz [Kontrolowanie zasobów zależności](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

## <a name="add-an-optional-description-field"></a>Dodawanie opcjonalnego pola opisu

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>Wybierz unikatowy identyfikator pakietu i ustaw numer wersji

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a>Uruchamianie polecenia pack

Aby utworzyć pakiet NuGet `.nupkg` (plik) z projektu, uruchom `dotnet pack` polecenie, które również automatycznie tworzy projekt:

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

Dane wyjściowe pokazuje `.nupkg` ścieżkę do pliku.

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

Po uruchomieniu `dotnet pack` rozwiązania, to pakuje wszystkie projekty w rozwiązaniu,[<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) które są `true`spakowane (właściwość jest ustawiona na ).

> [!NOTE]
> Po automatycznym wygenerowaniu pakietu czas do spakowania zwiększa czas kompilacji dla projektu.

### <a name="test-package-installation"></a>Instalacja pakietu testowego

Przed opublikowaniem pakietu zazwyczaj chcesz przetestować proces instalowania pakietu w projekcie. Testy upewnij się, że wszystkie pliki koniecznie kończy się w ich odpowiednich miejscach w projekcie.

Instalacje można testować ręcznie w programie Visual Studio lub w wierszu polecenia, wykonując [normalne kroki instalacji pakietu](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).

> [!IMPORTANT]
> Pakiety są niezmienne. Jeśli rozwiążesz problem, zmień zawartość pakietu i zapakuj ponownie, podczas ponownego testowania nadal będziesz używać starej wersji pakietu, dopóki nie [wyczyścisz folderu pakietów globalnych.](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) Jest to szczególnie istotne podczas testowania pakietów, które nie używają unikatowej etykiety wstępnej wersji w każdej kompilacji.

## <a name="next-steps"></a>Następne kroki

Po utworzeniu pakietu, który jest `.nupkg` plikiem, można go opublikować w wybranej galerii, zgodnie z opisem w [polu Publikowanie pakietu.](../nuget-org/publish-a-package.md)

Można również rozszerzyć możliwości pakietu lub w inny sposób obsługiwać inne scenariusze, jak opisano w następujących tematach:

- [Przechowywanie wersji pakietów](../concepts/package-versioning.md)
- [Obsługa wielu platform docelowych](../create-packages/multiple-target-frameworks-project-file.md)
- [Dodawanie ikony pakietu](../reference/nuspec.md#icon)
- [Przekształcenia plików źródłowych i konfiguracyjnych](../create-packages/source-and-config-file-transformations.md)
- [Lokalizacja](../create-packages/creating-localized-packages.md)
- [Wersje w wersji wstępnej](../create-packages/prerelease-packages.md)
- [Ustawianie typu pakietu](../create-packages/set-package-type.md)
- [Tworzenie pakietów z zestawami współdziałań COM](../create-packages/author-packages-with-COM-interop-assemblies.md)

Na koniec istnieją dodatkowe typy pakietów, o których należy pamiętać:

- [Pakiety natywne](../guides/native-packages.md)
- [Pakiety symboli](../create-packages/symbol-packages-snupkg.md)
