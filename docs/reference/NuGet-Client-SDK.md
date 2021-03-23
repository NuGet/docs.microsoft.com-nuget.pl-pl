---
title: Zestaw SDK klienta programu NuGet
description: Interfejs API jest rozwijany i nie został jeszcze udokumentowany, ale przykłady są dostępne w blogu Dave Glick.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: f9e08d37b30dfea83fd9b61f168c1e20f530ff9f
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859411"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="0397d-103">Zestaw SDK klienta programu NuGet</span><span class="sxs-lookup"><span data-stu-id="0397d-103">NuGet Client SDK</span></span>

<span data-ttu-id="0397d-104">*Zestaw SDK klienta NuGet* odwołuje się do grupy pakietów NuGet:</span><span class="sxs-lookup"><span data-stu-id="0397d-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="0397d-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) — Służy do współpracy z użyciem protokołu HTTP i opartych na plikach źródeł narzędzia NuGet</span><span class="sxs-lookup"><span data-stu-id="0397d-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="0397d-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) — Służy do współpracy z pakietami NuGet.</span><span class="sxs-lookup"><span data-stu-id="0397d-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="0397d-107">`NuGet.Protocol` zależy od tego pakietu</span><span class="sxs-lookup"><span data-stu-id="0397d-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="0397d-108">Kod źródłowy tych pakietów można znaleźć w repozytorium programu [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="0397d-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>
<span data-ttu-id="0397d-109">Kod źródłowy dla tych przykładów można znaleźć w projekcie [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="0397d-109">You can find the source code for these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) project on GitHub.</span></span>

> [!Note]
> <span data-ttu-id="0397d-110">Aby uzyskać dokumentację dotyczącą protokołu serwera NuGet, zapoznaj się z [interfejsem API serwera NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="0397d-110">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="nugetprotocol"></a><span data-ttu-id="0397d-111">NuGet. Protocol</span><span class="sxs-lookup"><span data-stu-id="0397d-111">NuGet.Protocol</span></span>

<span data-ttu-id="0397d-112">Zainstaluj `NuGet.Protocol` pakiet, aby korzystać z kanałów informacyjnych pakietów NuGet opartych na protokole HTTP i folderze:</span><span class="sxs-lookup"><span data-stu-id="0397d-112">Install the `NuGet.Protocol` package to interact with HTTP and folder-based NuGet package feeds:</span></span>

```ps1
dotnet add package NuGet.Protocol
```

### <a name="list-package-versions"></a><span data-ttu-id="0397d-113">Wyświetl wersje pakietów</span><span class="sxs-lookup"><span data-stu-id="0397d-113">List package versions</span></span>

<span data-ttu-id="0397d-114">Znajdź wszystkie wersje Newtonsoft.Jsna korzystanie z [interfejsu API zawartości pakietu NuGet v3](../api/package-base-address-resource.md#enumerate-package-versions):</span><span class="sxs-lookup"><span data-stu-id="0397d-114">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="0397d-115">Pobierz pakiet</span><span class="sxs-lookup"><span data-stu-id="0397d-115">Download a package</span></span>

<span data-ttu-id="0397d-116">Pobierz Newtonsoft.Jsw usłudze v 12.0.1 przy użyciu [interfejsu API zawartości pakietu NuGet v3](../api/package-base-address-resource.md):</span><span class="sxs-lookup"><span data-stu-id="0397d-116">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="0397d-117">Pobierz metadane pakietu</span><span class="sxs-lookup"><span data-stu-id="0397d-117">Get package metadata</span></span>

<span data-ttu-id="0397d-118">Pobierz metadane pakietu "Newtonsoft.Json" przy użyciu [interfejsu API metadanych pakietu NuGet v3](../api/registration-base-url-resource.md):</span><span class="sxs-lookup"><span data-stu-id="0397d-118">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="0397d-119">Wyszukaj pakiety</span><span class="sxs-lookup"><span data-stu-id="0397d-119">Search packages</span></span>

<span data-ttu-id="0397d-120">Wyszukaj pakiety "JSON" przy użyciu [interfejsu API wyszukiwania programu NuGet v3](../api/search-query-service-resource.md):</span><span class="sxs-lookup"><span data-stu-id="0397d-120">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a><span data-ttu-id="0397d-121">Wypchnij pakiet</span><span class="sxs-lookup"><span data-stu-id="0397d-121">Push a package</span></span>

<span data-ttu-id="0397d-122">Wypchnij pakiet za pomocą [interfejsu API wypychania i usuwania NuGet v3](../api/package-publish-resource.md):</span><span class="sxs-lookup"><span data-stu-id="0397d-122">Push a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a><span data-ttu-id="0397d-123">Usuwanie pakietu</span><span class="sxs-lookup"><span data-stu-id="0397d-123">Delete a package</span></span>

<span data-ttu-id="0397d-124">Usuń pakiet za pomocą [interfejsu API wypychania i usuwania NuGet v3](../api/package-publish-resource.md):</span><span class="sxs-lookup"><span data-stu-id="0397d-124">Delete a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

> [!Note]
> <span data-ttu-id="0397d-125">Serwery NuGet są bezpłatne, aby interpretować żądanie usunięcia pakietu jako "trwałe usuwanie", "Usuwanie miękkie" lub "unlisting".</span><span class="sxs-lookup"><span data-stu-id="0397d-125">NuGet servers are free to interpret a package delete request as a "hard delete", "soft delete", or "unlist".</span></span>
> <span data-ttu-id="0397d-126">Na przykład nuget.org interpretuje żądanie usunięcia pakietu jako "unlisting".</span><span class="sxs-lookup"><span data-stu-id="0397d-126">For example, nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="0397d-127">Aby uzyskać więcej informacji na temat tego rozwiązania, zobacz [usuwanie zasad pakietów](../nuget-org/policies/deleting-packages.md) .</span><span class="sxs-lookup"><span data-stu-id="0397d-127">For more information about this practice, see the [Deleting Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span>

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a><span data-ttu-id="0397d-128">Pracuj z uwierzytelnionymi źródłami danych</span><span class="sxs-lookup"><span data-stu-id="0397d-128">Work with authenticated feeds</span></span>

<span data-ttu-id="0397d-129">Służy [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) do pracy z uwierzytelnionymi źródłami danych.</span><span class="sxs-lookup"><span data-stu-id="0397d-129">Use [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) to work with authenticated feeds.</span></span>

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a><span data-ttu-id="0397d-130">NuGet. pakowanie</span><span class="sxs-lookup"><span data-stu-id="0397d-130">NuGet.Packaging</span></span>

<span data-ttu-id="0397d-131">Zainstaluj `NuGet.Packaging` pakiet, aby korzystać z usługi `.nupkg` i `.nuspec` plików ze strumienia:</span><span class="sxs-lookup"><span data-stu-id="0397d-131">Install the `NuGet.Packaging` package to interact with `.nupkg` and `.nuspec` files from a stream:</span></span>

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a><span data-ttu-id="0397d-132">Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="0397d-132">Create a package</span></span>

<span data-ttu-id="0397d-133">Tworzenie pakietu, Ustawianie metadanych i Dodawanie zależności przy użyciu [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="0397d-133">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0397d-134">Zdecydowanie zaleca się, aby pakiety NuGet zostały utworzone przy użyciu oficjalnych narzędzi NuGet, a **nie** za pomocą tego interfejsu API niskiego poziomu.</span><span class="sxs-lookup"><span data-stu-id="0397d-134">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="0397d-135">Istnieją różne cechy istotne dla dobrze uformowanego pakietu, a Najnowsza wersja narzędzi ułatwia uwzględnienie tych najlepszych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="0397d-135">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="0397d-136">Aby uzyskać więcej informacji na temat tworzenia pakietów NuGet, zobacz Omówienie [przepływu pracy tworzenia pakietów](../create-packages/overview-and-workflow.md) i dokumentacji oficjalnych narzędzi pakietu (na przykład [za pomocą interfejsu wiersza polecenia dotnet](../create-packages/creating-a-package-dotnet-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="0397d-136">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="0397d-137">Odczytaj pakiet</span><span class="sxs-lookup"><span data-stu-id="0397d-137">Read a package</span></span>

<span data-ttu-id="0397d-138">Odczytaj pakiet ze strumienia plików przy użyciu polecenia [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="0397d-138">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="0397d-139">Dokumentacja dotycząca innych firm</span><span class="sxs-lookup"><span data-stu-id="0397d-139">Third-party documentation</span></span>

<span data-ttu-id="0397d-140">Przykłady i Dokumentacja dla niektórych interfejsów API można znaleźć w następujących seriach blogów: Dave Glick, opublikowano 2016.</span><span class="sxs-lookup"><span data-stu-id="0397d-140">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="0397d-141">Eksplorowanie bibliotek programu NuGet v3, część 1: wprowadzenie i pojęcia</span><span class="sxs-lookup"><span data-stu-id="0397d-141">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="0397d-142">Eksplorowanie bibliotek programu NuGet v3, część 2: wyszukiwanie pakietów</span><span class="sxs-lookup"><span data-stu-id="0397d-142">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="0397d-143">Eksplorowanie bibliotek programu NuGet v3, część 3: Instalowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="0397d-143">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="0397d-144">Te wpisy w blogu zostały ogłoszone wkrótce po wydaniu wersji **3.4.3** pakietów SDK klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="0397d-144">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="0397d-145">Nowsze wersje pakietów mogą być niezgodne z informacjami w wpisach w blogu.</span><span class="sxs-lookup"><span data-stu-id="0397d-145">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="0397d-146">Martin Björkström zakończył wpis w blogu do serii blogów Dave Glick, gdzie wprowadzono inne podejście do instalowania pakietów NuGet przy użyciu zestawu SDK klienta NuGet:</span><span class="sxs-lookup"><span data-stu-id="0397d-146">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="0397d-147">Ponowne odwiedzanie bibliotek NuGet v3</span><span class="sxs-lookup"><span data-stu-id="0397d-147">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
