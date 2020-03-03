---
title: Zestaw SDK klienta NuGet
description: Interfejs API jest rozwijany i nie został jeszcze udokumentowany, ale przykłady są dostępne w blogu Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: a5c542379318f24ee35ccf25651d0e8de91253ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231243"
---
# <a name="nuget-client-sdk"></a>Zestaw SDK klienta NuGet

*Zestaw SDK klienta NuGet* odwołuje się do grupy pakietów NuGet:

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) — używane do współpracy z użyciem protokołu HTTP i źródeł danych NuGet opartych na plikach
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) — używane do współpracy z pakietami NuGet. `NuGet.Protocol` zależy od tego pakietu

Kod źródłowy tych pakietów można znaleźć w repozytorium programu [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) w serwisie GitHub.

> [!Note]
> Aby uzyskać dokumentację dotyczącą protokołu serwera NuGet, zapoznaj się z [interfejsem API serwera NuGet](~/api/overview.md).

## <a name="getting-started"></a>Wprowadzenie

### <a name="install-the-package"></a>Zainstaluj pakiet

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a>Przykłady

Te przykłady można znaleźć w projekcie [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) w witrynie GitHub.

### <a name="list-package-versions"></a>Wyświetl wersje pakietów

Znajdź wszystkie wersje pliku Newtonsoft. JSON przy użyciu [interfejsu API zawartości pakietu NuGet v3](../api/package-base-address-resource.md#enumerate-package-versions):

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>Pobierz pakiet

Pobierz pakiet Newtonsoft. JSON v 12.0.1 przy użyciu [interfejsu API zawartości pakietu NuGet v3](../api/package-base-address-resource.md):

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>Pobierz metadane pakietu

Pobierz metadane pakietu "Newtonsoft. JSON" przy użyciu [interfejsu API metadanych pakietu NuGet v3](../api/registration-base-url-resource.md):

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>Wyszukaj pakiety

Wyszukaj pakiety "JSON" przy użyciu [interfejsu API wyszukiwania programu NuGet v3](../api/search-query-service-resource.md):

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

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
