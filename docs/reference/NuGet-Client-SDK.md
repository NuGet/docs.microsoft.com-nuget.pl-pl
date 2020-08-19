---
title: Zestaw SDK klienta programu NuGet
description: Interfejs API jest rozwijany i nie został jeszcze udokumentowany, ale przykłady są dostępne w blogu Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 39a4de4071eec70c88a2add158f2a3a734f7d7b7
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622931"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="a6b0e-103">Zestaw SDK klienta programu NuGet</span><span class="sxs-lookup"><span data-stu-id="a6b0e-103">NuGet Client SDK</span></span>

<span data-ttu-id="a6b0e-104">*Zestaw SDK klienta NuGet* odwołuje się do grupy pakietów NuGet:</span><span class="sxs-lookup"><span data-stu-id="a6b0e-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="a6b0e-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) — Służy do współpracy z użyciem protokołu HTTP i opartych na plikach źródeł narzędzia NuGet</span><span class="sxs-lookup"><span data-stu-id="a6b0e-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="a6b0e-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) — Służy do współpracy z pakietami NuGet.</span><span class="sxs-lookup"><span data-stu-id="a6b0e-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="a6b0e-107">`NuGet.Protocol` zależy od tego pakietu</span><span class="sxs-lookup"><span data-stu-id="a6b0e-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="a6b0e-108">Kod źródłowy tych pakietów można znaleźć w repozytorium programu [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="a6b0e-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>

> [!Note]
> <span data-ttu-id="a6b0e-109">Aby uzyskać dokumentację dotyczącą protokołu serwera NuGet, zapoznaj się z [interfejsem API serwera NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="a6b0e-109">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="a6b0e-110">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="a6b0e-110">Getting started</span></span>

### <a name="install-the-packages"></a><span data-ttu-id="a6b0e-111">Zainstaluj pakiety</span><span class="sxs-lookup"><span data-stu-id="a6b0e-111">Install the packages</span></span>

```ps1
dotnet add package NuGet.Protocol  # interact with HTTP and folder-based NuGet package feeds, includes NuGet.Packaging

dotnet add package NuGet.Packaging # interact with .nupkg and .nuspec files from a stream
```

## <a name="examples"></a><span data-ttu-id="a6b0e-112">Przykłady</span><span class="sxs-lookup"><span data-stu-id="a6b0e-112">Examples</span></span>

<span data-ttu-id="a6b0e-113">Te przykłady można znaleźć w projekcie [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="a6b0e-113">You can find these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="a6b0e-114">Wyświetl wersje pakietów</span><span class="sxs-lookup"><span data-stu-id="a6b0e-114">List package versions</span></span>

<span data-ttu-id="a6b0e-115">Znajdź wszystkie wersje Newtonsoft.Jsna korzystanie z [interfejsu API zawartości pakietu NuGet v3](../api/package-base-address-resource.md#enumerate-package-versions):</span><span class="sxs-lookup"><span data-stu-id="a6b0e-115">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="a6b0e-116">Pobierz pakiet</span><span class="sxs-lookup"><span data-stu-id="a6b0e-116">Download a package</span></span>

<span data-ttu-id="a6b0e-117">Pobierz Newtonsoft.Jsw usłudze v 12.0.1 przy użyciu [interfejsu API zawartości pakietu NuGet v3](../api/package-base-address-resource.md):</span><span class="sxs-lookup"><span data-stu-id="a6b0e-117">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="a6b0e-118">Pobierz metadane pakietu</span><span class="sxs-lookup"><span data-stu-id="a6b0e-118">Get package metadata</span></span>

<span data-ttu-id="a6b0e-119">Pobierz metadane pakietu "Newtonsoft.Json" przy użyciu [interfejsu API metadanych pakietu NuGet v3](../api/registration-base-url-resource.md):</span><span class="sxs-lookup"><span data-stu-id="a6b0e-119">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="a6b0e-120">Wyszukaj pakiety</span><span class="sxs-lookup"><span data-stu-id="a6b0e-120">Search packages</span></span>

<span data-ttu-id="a6b0e-121">Wyszukaj pakiety "JSON" przy użyciu [interfejsu API wyszukiwania programu NuGet v3](../api/search-query-service-resource.md):</span><span class="sxs-lookup"><span data-stu-id="a6b0e-121">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="create-a-package"></a><span data-ttu-id="a6b0e-122">Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="a6b0e-122">Create a package</span></span>

<span data-ttu-id="a6b0e-123">Tworzenie pakietu, Ustawianie metadanych i Dodawanie zależności przy użyciu [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="a6b0e-123">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a6b0e-124">Zdecydowanie zaleca się, aby pakiety NuGet zostały utworzone przy użyciu oficjalnych narzędzi NuGet, a **nie** za pomocą tego interfejsu API niskiego poziomu.</span><span class="sxs-lookup"><span data-stu-id="a6b0e-124">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="a6b0e-125">Istnieją różne cechy istotne dla dobrze uformowanego pakietu, a Najnowsza wersja narzędzi ułatwia uwzględnienie tych najlepszych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="a6b0e-125">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="a6b0e-126">Aby uzyskać więcej informacji na temat tworzenia pakietów NuGet, zobacz Omówienie [przepływu pracy tworzenia pakietów](../create-packages/overview-and-workflow.md) i dokumentacji oficjalnych narzędzi pakietu (na przykład [za pomocą interfejsu wiersza polecenia dotnet](../create-packages/creating-a-package-dotnet-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="a6b0e-126">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="a6b0e-127">Odczytaj pakiet</span><span class="sxs-lookup"><span data-stu-id="a6b0e-127">Read a package</span></span>

<span data-ttu-id="a6b0e-128">Odczytaj pakiet ze strumienia plików przy użyciu polecenia [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="a6b0e-128">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="a6b0e-129">Dokumentacja dotycząca innych firm</span><span class="sxs-lookup"><span data-stu-id="a6b0e-129">Third-party documentation</span></span>

<span data-ttu-id="a6b0e-130">Przykłady i Dokumentacja dla niektórych interfejsów API można znaleźć w następujących seriach blogów: Dave Glick, opublikowano 2016.</span><span class="sxs-lookup"><span data-stu-id="a6b0e-130">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="a6b0e-131">Eksplorowanie bibliotek programu NuGet v3, część 1: wprowadzenie i pojęcia</span><span class="sxs-lookup"><span data-stu-id="a6b0e-131">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="a6b0e-132">Eksplorowanie bibliotek programu NuGet v3, część 2: wyszukiwanie pakietów</span><span class="sxs-lookup"><span data-stu-id="a6b0e-132">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="a6b0e-133">Eksplorowanie bibliotek programu NuGet v3, część 3: Instalowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="a6b0e-133">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="a6b0e-134">Te wpisy w blogu zostały ogłoszone wkrótce po wydaniu wersji **3.4.3** pakietów SDK klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="a6b0e-134">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="a6b0e-135">Nowsze wersje pakietów mogą być niezgodne z informacjami w wpisach w blogu.</span><span class="sxs-lookup"><span data-stu-id="a6b0e-135">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="a6b0e-136">Martin Björkström zakończył wpis w blogu do serii blogów Dave Glick, gdzie wprowadzono inne podejście do instalowania pakietów NuGet przy użyciu zestawu SDK klienta NuGet:</span><span class="sxs-lookup"><span data-stu-id="a6b0e-136">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="a6b0e-137">Ponowne odwiedzanie bibliotek NuGet v3</span><span class="sxs-lookup"><span data-stu-id="a6b0e-137">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
