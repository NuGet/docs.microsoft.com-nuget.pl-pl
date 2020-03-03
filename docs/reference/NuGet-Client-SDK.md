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
# <a name="nuget-client-sdk"></a><span data-ttu-id="8dba4-103">Zestaw SDK klienta NuGet</span><span class="sxs-lookup"><span data-stu-id="8dba4-103">NuGet Client SDK</span></span>

<span data-ttu-id="8dba4-104">*Zestaw SDK klienta NuGet* odwołuje się do grupy pakietów NuGet:</span><span class="sxs-lookup"><span data-stu-id="8dba4-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="8dba4-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) — używane do współpracy z użyciem protokołu HTTP i źródeł danych NuGet opartych na plikach</span><span class="sxs-lookup"><span data-stu-id="8dba4-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="8dba4-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) — używane do współpracy z pakietami NuGet.</span><span class="sxs-lookup"><span data-stu-id="8dba4-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="8dba4-107">`NuGet.Protocol` zależy od tego pakietu</span><span class="sxs-lookup"><span data-stu-id="8dba4-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="8dba4-108">Kod źródłowy tych pakietów można znaleźć w repozytorium programu [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="8dba4-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>

> [!Note]
> <span data-ttu-id="8dba4-109">Aby uzyskać dokumentację dotyczącą protokołu serwera NuGet, zapoznaj się z [interfejsem API serwera NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="8dba4-109">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="8dba4-110">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="8dba4-110">Getting started</span></span>

### <a name="install-the-package"></a><span data-ttu-id="8dba4-111">Zainstaluj pakiet</span><span class="sxs-lookup"><span data-stu-id="8dba4-111">Install the package</span></span>

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a><span data-ttu-id="8dba4-112">Przykłady</span><span class="sxs-lookup"><span data-stu-id="8dba4-112">Examples</span></span>

<span data-ttu-id="8dba4-113">Te przykłady można znaleźć w projekcie [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="8dba4-113">You can find these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="8dba4-114">Wyświetl wersje pakietów</span><span class="sxs-lookup"><span data-stu-id="8dba4-114">List package versions</span></span>

<span data-ttu-id="8dba4-115">Znajdź wszystkie wersje pliku Newtonsoft. JSON przy użyciu [interfejsu API zawartości pakietu NuGet v3](../api/package-base-address-resource.md#enumerate-package-versions):</span><span class="sxs-lookup"><span data-stu-id="8dba4-115">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="8dba4-116">Pobierz pakiet</span><span class="sxs-lookup"><span data-stu-id="8dba4-116">Download a package</span></span>

<span data-ttu-id="8dba4-117">Pobierz pakiet Newtonsoft. JSON v 12.0.1 przy użyciu [interfejsu API zawartości pakietu NuGet v3](../api/package-base-address-resource.md):</span><span class="sxs-lookup"><span data-stu-id="8dba4-117">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="8dba4-118">Pobierz metadane pakietu</span><span class="sxs-lookup"><span data-stu-id="8dba4-118">Get package metadata</span></span>

<span data-ttu-id="8dba4-119">Pobierz metadane pakietu "Newtonsoft. JSON" przy użyciu [interfejsu API metadanych pakietu NuGet v3](../api/registration-base-url-resource.md):</span><span class="sxs-lookup"><span data-stu-id="8dba4-119">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="8dba4-120">Wyszukaj pakiety</span><span class="sxs-lookup"><span data-stu-id="8dba4-120">Search packages</span></span>

<span data-ttu-id="8dba4-121">Wyszukaj pakiety "JSON" przy użyciu [interfejsu API wyszukiwania programu NuGet v3](../api/search-query-service-resource.md):</span><span class="sxs-lookup"><span data-stu-id="8dba4-121">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

## <a name="third-party-documentation"></a><span data-ttu-id="8dba4-122">Dokumentacja dotycząca innych firm</span><span class="sxs-lookup"><span data-stu-id="8dba4-122">Third-party documentation</span></span>

<span data-ttu-id="8dba4-123">Przykłady i Dokumentacja dla niektórych interfejsów API można znaleźć w następujących seriach blogów: Dave Glick, opublikowano 2016.</span><span class="sxs-lookup"><span data-stu-id="8dba4-123">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="8dba4-124">Eksplorowanie bibliotek programu NuGet v3, część 1: wprowadzenie i pojęcia</span><span class="sxs-lookup"><span data-stu-id="8dba4-124">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="8dba4-125">Eksplorowanie bibliotek programu NuGet v3, część 2: wyszukiwanie pakietów</span><span class="sxs-lookup"><span data-stu-id="8dba4-125">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="8dba4-126">Eksplorowanie bibliotek programu NuGet v3, część 3: Instalowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="8dba4-126">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="8dba4-127">Te wpisy w blogu zostały ogłoszone wkrótce po wydaniu wersji **3.4.3** pakietów SDK klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="8dba4-127">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="8dba4-128">Nowsze wersje pakietów mogą być niezgodne z informacjami w wpisach w blogu.</span><span class="sxs-lookup"><span data-stu-id="8dba4-128">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="8dba4-129">Martin Björkström zakończył wpis w blogu do serii blogów Dave Glick, gdzie wprowadzono inne podejście do instalowania pakietów NuGet przy użyciu zestawu SDK klienta NuGet:</span><span class="sxs-lookup"><span data-stu-id="8dba4-129">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="8dba4-130">Ponowne odwiedzanie bibliotek NuGet v3</span><span class="sxs-lookup"><span data-stu-id="8dba4-130">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
