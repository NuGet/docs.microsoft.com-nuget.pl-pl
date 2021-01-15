---
title: Zestaw SDK klienta programu NuGet
description: Interfejs API jest rozwijany i nie został jeszcze udokumentowany, ale przykłady są dostępne w blogu Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 0eca8478b4d6509dbc1407560d2c86069c7575dd
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235740"
---
# <a name="nuget-client-sdk"></a>Zestaw SDK klienta programu NuGet

*Zestaw SDK klienta NuGet* odwołuje się do grupy pakietów NuGet:

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) — Służy do współpracy z użyciem protokołu HTTP i opartych na plikach źródeł narzędzia NuGet
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) — Służy do współpracy z pakietami NuGet. `NuGet.Protocol` zależy od tego pakietu

Kod źródłowy tych pakietów można znaleźć w repozytorium programu [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) w serwisie GitHub.
Kod źródłowy dla tych przykładów można znaleźć w projekcie [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) w witrynie GitHub.

> [!Note]
> Aby uzyskać dokumentację dotyczącą protokołu serwera NuGet, zapoznaj się z [interfejsem API serwera NuGet](~/api/overview.md).

## <a name="nugetprotocol"></a>NuGet. Protocol

Zainstaluj `NuGet.Protocol` pakiet, aby korzystać z kanałów informacyjnych pakietów NuGet opartych na protokole HTTP i folderze:

```ps1
dotnet add package NuGet.Protocol
```

### <a name="list-package-versions"></a>Wyświetl wersje pakietów

Znajdź wszystkie wersje Newtonsoft.Jsna korzystanie z [interfejsu API zawartości pakietu NuGet v3](../api/package-base-address-resource.md#enumerate-package-versions):

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>Pobierz pakiet

Pobierz Newtonsoft.Jsw usłudze v 12.0.1 przy użyciu [interfejsu API zawartości pakietu NuGet v3](../api/package-base-address-resource.md):

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>Pobierz metadane pakietu

Pobierz metadane pakietu "Newtonsoft.Json" przy użyciu [interfejsu API metadanych pakietu NuGet v3](../api/registration-base-url-resource.md):

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>Wyszukaj pakiety

Wyszukaj pakiety "JSON" przy użyciu [interfejsu API wyszukiwania programu NuGet v3](../api/search-query-service-resource.md):

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a>Wypchnij pakiet

Wypchnij pakiet za pomocą [interfejsu API wypychania i usuwania NuGet v3](../api/package-publish-resource.md):

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a>Usuwanie pakietu

Usuń pakiet za pomocą [interfejsu API wypychania i usuwania NuGet v3](../api/package-publish-resource.md):

> [!Note]
> Serwery NuGet są bezpłatne, aby interpretować żądanie usunięcia pakietu jako "trwałe usuwanie", "Usuwanie miękkie" lub "unlisting".
> Na przykład nuget.org interpretuje żądanie usunięcia pakietu jako "unlisting". Aby uzyskać więcej informacji na temat tego rozwiązania, zobacz [usuwanie zasad pakietów](../nuget-org/policies/deleting-packages.md) .

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a>Pracuj z uwierzytelnionymi źródłami danych

Służy [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) do pracy z uwierzytelnionymi źródłami danych.

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a>NuGet. pakowanie

Zainstaluj `NuGet.Packaging` pakiet, aby korzystać z usługi `.nupkg` i `.nuspec` plików ze strumienia:

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a>Tworzenie pakietu

Tworzenie pakietu, Ustawianie metadanych i Dodawanie zależności przy użyciu [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .

> [!IMPORTANT]
> Zdecydowanie zaleca się, aby pakiety NuGet zostały utworzone przy użyciu oficjalnych narzędzi NuGet, a **nie** za pomocą tego interfejsu API niskiego poziomu. Istnieją różne cechy istotne dla dobrze uformowanego pakietu, a Najnowsza wersja narzędzi ułatwia uwzględnienie tych najlepszych rozwiązań.
> 
> Aby uzyskać więcej informacji na temat tworzenia pakietów NuGet, zobacz Omówienie [przepływu pracy tworzenia pakietów](../create-packages/overview-and-workflow.md) i dokumentacji oficjalnych narzędzi pakietu (na przykład [za pomocą interfejsu wiersza polecenia dotnet](../create-packages/creating-a-package-dotnet-cli.md)).

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a>Odczytaj pakiet

Odczytaj pakiet ze strumienia plików przy użyciu polecenia [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a>Dokumentacja dotycząca innych firm

Przykłady i Dokumentacja dla niektórych interfejsów API można znaleźć w następujących seriach blogów: Dave Glick, opublikowano 2016.

- [Eksplorowanie bibliotek programu NuGet v3, część 1: wprowadzenie i pojęcia](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Eksplorowanie bibliotek programu NuGet v3, część 2: wyszukiwanie pakietów](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Eksplorowanie bibliotek programu NuGet v3, część 3: Instalowanie pakietów](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Te wpisy w blogu zostały ogłoszone wkrótce po wydaniu wersji **3.4.3** pakietów SDK klienta NuGet.
> Nowsze wersje pakietów mogą być niezgodne z informacjami w wpisach w blogu.

Martin Björkström zakończył wpis w blogu do serii blogów Dave Glick, gdzie wprowadzono inne podejście do instalowania pakietów NuGet przy użyciu zestawu SDK klienta NuGet:

- [Ponowne odwiedzanie bibliotek NuGet v3](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
