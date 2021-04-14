---
title: Zestaw SDK klienta programu NuGet
description: Interfejs API ewoluuje i nie został jeszcze udokumentowany, ale przykłady są dostępne na blogu Dave'a Glicka.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 6417c971dc13cf9ed05dcec4e4156af94c0ea058
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387390"
---
# <a name="nuget-client-sdk"></a>Zestaw SDK klienta programu NuGet

Zestaw *SDK klienta NuGet* odwołuje się do grupy pakietów NuGet:

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) — Służy do interakcji ze źródłami danych NuGet opartymi na plikach i HTTP
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) — Służy do interakcji z pakietami NuGet. `NuGet.Protocol` zależy od tego pakietu

Kod źródłowy tych pakietów można znaleźć w [repozytorium GitHub NuGet/NuGet.Client.](https://github.com/NuGet/NuGet.Client)
Kod źródłowy tych przykładów można znaleźć w [projekcie NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) w witrynie GitHub.

> [!Note]
> Aby uzyskać dokumentację dotyczącą protokołu serwera NuGet, zapoznaj się z interfejsem [API serwera NuGet.](~/api/overview.md)

## <a name="nugetprotocol"></a>NuGet.Protocol

Zainstaluj pakiet, aby wchodzić w interakcje z kanałami informacyjnymi pakietów NuGet opartymi na http `NuGet.Protocol` i folderach:

```ps1
dotnet add package NuGet.Protocol
```

> [!Tip]
> `Repository.Factory` Element jest zdefiniowany w `NuGet.Protocol.Core.Types` przestrzeni nazw , a metoda jest metodą rozszerzenia `GetCoreV3` zdefiniowaną w przestrzeni nazw `NuGet.Protocol` . W związku z tym należy dodać `using` instrukcje dla obu przestrzeni nazw.

### <a name="list-package-versions"></a>Lista wersji pakietów

Znajdź wszystkie wersje pakietu Newtonsoft.Jsprzy użyciu interfejsu API zawartości pakietu [NuGet V3:](../api/package-base-address-resource.md#enumerate-package-versions)

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>Pobieranie pakietu

Pobierz Newtonsoft.Jsw wersji 12.0.1 przy użyciu interfejsu API zawartości pakietu [NuGet V3:](../api/package-base-address-resource.md)

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>Uzyskiwanie metadanych pakietu

Pobierz metadane dla pakietu "Newtonsoft.Json" przy użyciu interfejsu API metadanych pakietu [NuGet v3:](../api/registration-base-url-resource.md)

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>Wyszukiwanie pakietów

Wyszukaj pakiety "json" przy użyciu interfejsu [API wyszukiwania NuGet v3:](../api/search-query-service-resource.md)

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a>Wypychanie pakietu

Wypchnąć pakiet przy użyciu interfejsu API wypychania i usuwania [nuGet w wersji 3:](../api/package-publish-resource.md)

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a>Usuwanie pakietu

Usuń pakiet przy użyciu interfejsu [API wypychania NuGet v3 i usuwania:](../api/package-publish-resource.md)

> [!Note]
> Serwery NuGet mogą interpretować żądanie usunięcia pakietu jako "twarde usuwanie", "usuwanie nie soft" lub "unlist".
> Na przykład nuget.org żądanie usunięcia pakietu jest interpretowane jako "unlist". Aby uzyskać więcej informacji na temat tego rozwiązania, zobacz [zasady Usuwanie](../nuget-org/policies/deleting-packages.md) pakietów.

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a>Praca z uwierzytelnionym kanałami informacyjnymi

Użyj [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) do pracy z uwierzytelnianych kanałów informacyjnych.

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a>NuGet.Packaging

Zainstaluj `NuGet.Packaging` pakiet, aby wchodzić w `.nupkg` interakcje z `.nuspec` plikami i ze strumienia:

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a>Tworzenie pakietu

Utwórz pakiet, ustaw metadane i dodaj zależności przy użyciu elementu [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .

> [!IMPORTANT]
> Zdecydowanie zaleca się, aby pakiety NuGet były tworzone przy użyciu oficjalnych narzędzi NuGet, a **nie** przy użyciu tego interfejsu API niskiego poziomu. W przypadku dobrze utworzonego pakietu istnieją różne charakterystyki, a najnowsza wersja narzędzi ułatwia uwzględnienie tych najlepszych rozwiązań.
> 
> Aby uzyskać więcej informacji na temat tworzenia [](../create-packages/overview-and-workflow.md) pakietów NuGet, zobacz omówienie przepływu pracy tworzenia pakietów i dokumentację dotyczącą oficjalnych narzędzi pakietu (na przykład przy użyciu interfejsu wiersza [polecenia dotnet).](../create-packages/creating-a-package-dotnet-cli.md)

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a>Odczytywanie pakietu

Odczytaj pakiet ze strumienia plików przy [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) użyciu .

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a>Dokumentacja innych firm

Przykłady i dokumentację dla niektórych interfejsów API można znaleźć w następującej serii blogów Autorstwa Dave'a Glicka, opublikowanej w 2016 r.:

- [Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts (Eksplorowanie bibliotek NuGet w wersji 3, część 1: wprowadzenie i pojęcia)](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Exploring the NuGet v3 Libraries, Part 2: Searching for packages (Eksplorowanie bibliotek NuGet w wersji 3, część 2: wyszukiwanie pakietów)](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Eksplorowanie bibliotek NuGet w wersji 3, część 3: instalowanie pakietów](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Te wpisy w blogu zostały napisane wkrótce po wersji **3.4.3** pakietów zestawu SDK klienta NuGet.
> Nowsze wersje pakietów mogą być niezgodne z informacjami we wpisach w blogu.

Martin Björkström opublikował kolejne wpisy w blogu Dave'a Glicka, w którym przedstawia inne podejście do instalowania pakietów NuGet przy użyciu zestawu SDK klienta NuGet:

- [Ponowne poprawianie bibliotek NuGet w wersji 3](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
