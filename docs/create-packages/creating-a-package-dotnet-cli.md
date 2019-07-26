---
title: Tworzenie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet
description: Szczegółowy przewodnik dotyczący procesu projektowania i tworzenia pakietu NuGet, w tym najważniejszych punktów decyzyjnych, takich jak pliki i przechowywanie wersji.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: da5dbc8b1659cef66e8439b9a3c3bb2c9205cbe6
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/24/2019
ms.locfileid: "68462454"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a>Tworzenie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet

Niezależnie od tego, co Twój pakiet lub jaki kod zawiera, użyj jednego z narzędzi `nuget.exe` interfejsu wiersza polecenia lub `dotnet.exe`, aby spakować tę funkcję do składnika, który może być współużytkowany i używany przez dowolną liczbę innych deweloperów. W tym artykule opisano sposób tworzenia pakietu przy użyciu interfejsu wiersza polecenia dotnet. Aby zainstalować `dotnet` interfejs wiersza polecenia, zobacz [Instalowanie narzędzi klienckich programu NuGet](../install-nuget-client-tools.md). Począwszy od programu Visual Studio 2017, interfejs wiersza polecenia dotnet jest dołączany do obciążeń .NET Core.

W przypadku projektów .NET Core i .NET Standard, które korzystają z [formatu zestawu SDK](../resources/check-project-format.md)i innych projektów w stylu zestawu SDK, NuGet używa informacji w pliku projektu bezpośrednio do tworzenia pakietu. Aby zapoznać się z samouczkami krok po kroku, zobacz [Tworzenie pakietów .NET standard za pomocą interfejsu wiersza polecenia dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md), [Tworzenie pakietów .NET standard za pomocą programu Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).

`msbuild -t:pack`Funkcja jest równoważna `dotnet pack`z. W celu kompilowania przy użyciu programu MSBuild koncepcje są takie same jak opisane w tym artykule, ale polecenia wiersza polecenia są nieco inne. Podobnie, w przypadku projektu typu innego niż zestaw SDK i `<PackageReference>`, można użyć. `msbuild /t:pack` W tych scenariuszach należy dodać pakiet NuGet. Build. Tasks. Pack do ich zależności. Zapoznaj się [z pakietem NuGet i Przywróć jako elementy docelowe programu MSBuild](../reference/msbuild-targets.md).

> [!IMPORTANT]
> Ten temat ma zastosowanie do projektów w [stylu zestawu SDK](../resources/check-project-format.md) , zwykle .NET Core i projektów .NET Standard.

## <a name="set-properties"></a>Ustaw właściwości

Do utworzenia pakietu wymagane są następujące właściwości.

- `PackageId`Identyfikator pakietu, który musi być unikatowy w galerii, w której znajduje się pakiet. Jeśli nie zostanie określony, wartość domyślna to `AssemblyName`.
- `Version`, określony numer wersji w postaci *główna. pomocnicza. poprawka [-sufiks]* , gdzie *-sufiks* określa [wersję wstępną](prerelease-packages.md). Jeśli nie zostanie określony, wartość domyślna to 1.0.0.
- Tytuł pakietu, który powinien pojawić się na hoście (na przykład nuget.org)
- `Authors`Informacje o autorze i właścicielu. Jeśli nie zostanie określony, wartość domyślna to `AssemblyName`.
- `Company`, nazwa firmy. Jeśli nie zostanie określony, wartość domyślna to `AssemblyName`.

W programie Visual Studio można ustawić te wartości we właściwościach projektu (kliknij prawym przyciskiem myszy projekt w Eksplorator rozwiązań, wybierz **Właściwości**, a następnie wybierz kartę **pakiet** ). Możesz również ustawić te właściwości bezpośrednio w plikach projektu (`.csproj`).

    ```xml
    <PropertyGroup>
      ...
      <PackageId>AppLogger</PackageId>
      <Version>1.0.0</Version>
      <Authors>your_name</Authors>
      <Company>your_company</Company>
    </PropertyGroup>
    ```

> [!Important]
> Nadaj pakietowi identyfikator, który jest unikatowy w obrębie nuget.org lub dowolnego źródła pakietów, którego używasz.

Można `Title`również ustawić właściwości opcjonalne, takie jak, `PackageTags` `PackageDescription`, i, zgodnie z opisem w obszarze [targets pakietu MSBuild](../reference/msbuild-targets.md#pack-target), [kontrolować zasoby zależności](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)i [właściwości metadanych NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

> [!NOTE]
> W przypadku pakietów przeznaczonych do użycia publicznego należy zwrócić szczególną uwagę na Właściwość **PackageTags** , ponieważ Tagi ułatwiają innym znalezienie pakietu i zrozumienie jego działania.

Aby uzyskać szczegółowe informacje na temat deklarowania zależności i określania numerów wersji, zobacz [wersja pakietu](../reference/package-versioning.md). Istnieje również możliwość, że zasoby są zależne od zależności bezpośrednio w pakiecie przy użyciu `<IncludeAssets>` atrybutów `<ExcludeAssets>` i. Aby uzyskać więcej informacji, seee [kontrolowania elementów zależnych](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>Wybierz unikatowy identyfikator pakietu i ustaw numer wersji

Identyfikator pakietu i numer wersji to dwie najważniejsze wartości w projekcie, ponieważ jednoznacznie identyfikują dokładny kod zawarty w pakiecie.

**Najlepsze rozwiązania dotyczące identyfikatora pakietu:**

- **Unikatowość**: Identyfikator musi być unikatowy w obrębie nuget.org lub dowolnej galerii, w której znajduje się pakiet. Przed podjęciem decyzji o identyfikatorze Przeszukaj stosowną galerię, aby sprawdzić, czy nazwa jest już używana. Aby uniknąć konfliktów, dobrym wzorcem jest użycie nazwy firmy jako pierwszej części identyfikatora, na przykład `Contoso.`.
- **Nazwy podobne do nazw**: Postępuj zgodnie ze wzorcem podobnym do przestrzeni nazw w programie .NET przy użyciu notacji kropkowej zamiast łączników. Na przykład użyj `Contoso.Utility.UsefulStuff` `Contoso-Utility-UsefulStuff` zamiast lub `Contoso_Utility_UsefulStuff`. Konsumenci są również pomocne, gdy identyfikator pakietu jest zgodny z przestrzeniami nazw używanymi w kodzie.
- **Przykładowe pakiety**: Jeśli utworzysz pakiet przykładowego kodu, który pokazuje, jak używać innego pakietu, Dołącz `.Sample` jako sufiks do identyfikatora, jak w. `Contoso.Utility.UsefulStuff.Sample` (Przykładowy pakiet jest oczywiście zależny od innego pakietu). Podczas tworzenia przykładowego pakietu Użyj `contentFiles` wartości w. `<IncludeAssets>` W folderze Rozmieść przykładowy kod w folderze o nazwie `\Samples\<identifier>` w `\Samples\Contoso.Utility.UsefulStuff.Sample`. `content`

**Najlepsze rozwiązania dotyczące wersji pakietu:**

- Ogólnie rzecz biorąc Ustaw wersję pakietu na zgodną z projektem (lub zestawem), ale nie jest to ściśle wymagane. Jest to prosta kwestia w przypadku ograniczenia pakietu do jednego zestawu. Ogólnie, pamiętaj, że sam pakiet NuGet zajmuje się wersjami pakietu podczas rozpoznawania zależności, a nie wersji zestawu.
- W przypadku korzystania ze schematu wersji niestandardowej należy wziąć pod uwagę reguły obsługi wersji NuGet zgodnie z opisem w temacie [wersja pakietu](../reference/package-versioning.md). Pakiet NuGet jest w większości [semver 2 zgodny](../reference/package-versioning.md#semantic-versioning-200).

> Aby uzyskać informacje dotyczące rozpoznawania zależności, zobacz [rozpoznawanie zależności z PackageReference](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference). Aby poznać starsze informacje, które mogą być przydatne do lepszego zrozumienia wersji, zobacz tę serię wpisów w blogu.
>
> - [Część 1. Pobieranie na Hell DLL](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Część 2. Podstawowy algorytm](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Część 3: Ujednolicenie za pomocą przekierowań powiązań](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="run-the-pack-command"></a>Uruchom pakiet polecenie

Aby skompilować pakiet NuGet ( `.nupkg` plik) z projektu, `dotnet pack` Uruchom polecenie, które również automatycznie kompiluje projekt:

```cli
# Uses the project file in the current folder by default
dotnet pack
```

Dane wyjściowe przedstawiają ścieżkę do `.nupkg` pliku:

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Automatycznie Generuj pakiet podczas kompilacji

Aby automatycznie uruchomić `dotnet pack` `dotnet build`program, Dodaj następujący wiersz do pliku projektu w `<PropertyGroup>`:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

Po uruchomieniu `dotnet pack` w rozwiązaniu to pakiety wszystkie projekty w rozwiązaniu, które są możliwe do spakowania ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) właściwość jest ustawiona na `true`.

> [!NOTE]
> Po automatycznym wygenerowaniu pakietu czas do spakowania zwiększa czas kompilacji projektu.

### <a name="test-package-installation"></a>Instalacja pakietu testowego

Przed opublikowaniem pakietu zazwyczaj należy przetestować proces instalacji pakietu w projekcie. Testy upewniają się, że wszystkie pliki, które się na bieżąco, kończą się w ich prawidłowym miejscu w projekcie.

Instalacje można testować ręcznie w programie Visual Studio lub w wierszu polecenia przy użyciu standardowych [kroków instalacji pakietu](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).

> [!IMPORTANT]
> Pakiety są niezmienne. W przypadku usunięcia problemu należy ponownie zmienić zawartość pakietu i pakietu, po ponownym przetestowaniu nadal będzie używana stara wersja pakietu do momentu wyczyszczenia folderu [pakiety globalne](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) . Jest to szczególnie istotne w przypadku testowania pakietów, które nie używają unikatowej etykiety wersji wstępnej dla każdej kompilacji.

## <a name="next-steps"></a>Następne kroki

Po utworzeniu pakietu, który jest `.nupkg` plikiem, można go opublikować w wybranej galerii, zgodnie z opisem w artykule [Publikowanie pakietu](../nuget-org/publish-a-package.md).

Możesz również chcieć zwiększyć możliwości pakietu lub w inny sposób obsługiwać inne scenariusze zgodnie z opisem w następujących tematach:

- [Przechowywanie wersji pakietów](../reference/package-versioning.md)
- [Obsługa wielu platform docelowych](../create-packages/multiple-target-frameworks-project-file.md)
- [Przekształcenia plików źródłowych i konfiguracji](../create-packages/source-and-config-file-transformations.md)
- [Lokalizacja](../create-packages/creating-localized-packages.md)
- [Wersje wstępne](../create-packages/prerelease-packages.md)
- [Ustawianie typu pakietu](../create-packages/set-package-type.md)
- [Tworzenie pakietów z zestawami międzyoperacyjnymi modelu COM](../create-packages/author-packages-with-COM-interop-assemblies.md)

Na koniec należy pamiętać o dodatkowych typach pakietów:

- [Pakiety natywne](../create-packages/native-packages.md)
- [Pakiety symboli](../create-packages/symbol-packages.md)
