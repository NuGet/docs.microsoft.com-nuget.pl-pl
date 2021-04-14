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
# <a name="nuget-client-sdk"></a><span data-ttu-id="27bb5-103">Zestaw SDK klienta programu NuGet</span><span class="sxs-lookup"><span data-stu-id="27bb5-103">NuGet Client SDK</span></span>

<span data-ttu-id="27bb5-104">Zestaw *SDK klienta NuGet* odwołuje się do grupy pakietów NuGet:</span><span class="sxs-lookup"><span data-stu-id="27bb5-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="27bb5-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) — Służy do interakcji ze źródłami danych NuGet opartymi na plikach i HTTP</span><span class="sxs-lookup"><span data-stu-id="27bb5-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="27bb5-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) — Służy do interakcji z pakietami NuGet.</span><span class="sxs-lookup"><span data-stu-id="27bb5-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="27bb5-107">`NuGet.Protocol` zależy od tego pakietu</span><span class="sxs-lookup"><span data-stu-id="27bb5-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="27bb5-108">Kod źródłowy tych pakietów można znaleźć w [repozytorium GitHub NuGet/NuGet.Client.](https://github.com/NuGet/NuGet.Client)</span><span class="sxs-lookup"><span data-stu-id="27bb5-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>
<span data-ttu-id="27bb5-109">Kod źródłowy tych przykładów można znaleźć w [projekcie NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="27bb5-109">You can find the source code for these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) project on GitHub.</span></span>

> [!Note]
> <span data-ttu-id="27bb5-110">Aby uzyskać dokumentację dotyczącą protokołu serwera NuGet, zapoznaj się z interfejsem [API serwera NuGet.](~/api/overview.md)</span><span class="sxs-lookup"><span data-stu-id="27bb5-110">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="nugetprotocol"></a><span data-ttu-id="27bb5-111">NuGet.Protocol</span><span class="sxs-lookup"><span data-stu-id="27bb5-111">NuGet.Protocol</span></span>

<span data-ttu-id="27bb5-112">Zainstaluj pakiet, aby wchodzić w interakcje z kanałami informacyjnymi pakietów NuGet opartymi na http `NuGet.Protocol` i folderach:</span><span class="sxs-lookup"><span data-stu-id="27bb5-112">Install the `NuGet.Protocol` package to interact with HTTP and folder-based NuGet package feeds:</span></span>

```ps1
dotnet add package NuGet.Protocol
```

> [!Tip]
> <span data-ttu-id="27bb5-113">`Repository.Factory` Element jest zdefiniowany w `NuGet.Protocol.Core.Types` przestrzeni nazw , a metoda jest metodą rozszerzenia `GetCoreV3` zdefiniowaną w przestrzeni nazw `NuGet.Protocol` .</span><span class="sxs-lookup"><span data-stu-id="27bb5-113">`Repository.Factory` is defined in the `NuGet.Protocol.Core.Types` namespace, and the `GetCoreV3` method is an extension method defined in the `NuGet.Protocol` namespace.</span></span> <span data-ttu-id="27bb5-114">W związku z tym należy dodać `using` instrukcje dla obu przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="27bb5-114">Therefore, you will need to add `using` statements for both namespaces.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="27bb5-115">Lista wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="27bb5-115">List package versions</span></span>

<span data-ttu-id="27bb5-116">Znajdź wszystkie wersje pakietu Newtonsoft.Jsprzy użyciu interfejsu API zawartości pakietu [NuGet V3:](../api/package-base-address-resource.md#enumerate-package-versions)</span><span class="sxs-lookup"><span data-stu-id="27bb5-116">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="27bb5-117">Pobieranie pakietu</span><span class="sxs-lookup"><span data-stu-id="27bb5-117">Download a package</span></span>

<span data-ttu-id="27bb5-118">Pobierz Newtonsoft.Jsw wersji 12.0.1 przy użyciu interfejsu API zawartości pakietu [NuGet V3:](../api/package-base-address-resource.md)</span><span class="sxs-lookup"><span data-stu-id="27bb5-118">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="27bb5-119">Uzyskiwanie metadanych pakietu</span><span class="sxs-lookup"><span data-stu-id="27bb5-119">Get package metadata</span></span>

<span data-ttu-id="27bb5-120">Pobierz metadane dla pakietu "Newtonsoft.Json" przy użyciu interfejsu API metadanych pakietu [NuGet v3:](../api/registration-base-url-resource.md)</span><span class="sxs-lookup"><span data-stu-id="27bb5-120">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="27bb5-121">Wyszukiwanie pakietów</span><span class="sxs-lookup"><span data-stu-id="27bb5-121">Search packages</span></span>

<span data-ttu-id="27bb5-122">Wyszukaj pakiety "json" przy użyciu interfejsu [API wyszukiwania NuGet v3:](../api/search-query-service-resource.md)</span><span class="sxs-lookup"><span data-stu-id="27bb5-122">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a><span data-ttu-id="27bb5-123">Wypychanie pakietu</span><span class="sxs-lookup"><span data-stu-id="27bb5-123">Push a package</span></span>

<span data-ttu-id="27bb5-124">Wypchnąć pakiet przy użyciu interfejsu API wypychania i usuwania [nuGet w wersji 3:](../api/package-publish-resource.md)</span><span class="sxs-lookup"><span data-stu-id="27bb5-124">Push a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a><span data-ttu-id="27bb5-125">Usuwanie pakietu</span><span class="sxs-lookup"><span data-stu-id="27bb5-125">Delete a package</span></span>

<span data-ttu-id="27bb5-126">Usuń pakiet przy użyciu interfejsu [API wypychania NuGet v3 i usuwania:](../api/package-publish-resource.md)</span><span class="sxs-lookup"><span data-stu-id="27bb5-126">Delete a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

> [!Note]
> <span data-ttu-id="27bb5-127">Serwery NuGet mogą interpretować żądanie usunięcia pakietu jako "twarde usuwanie", "usuwanie nie soft" lub "unlist".</span><span class="sxs-lookup"><span data-stu-id="27bb5-127">NuGet servers are free to interpret a package delete request as a "hard delete", "soft delete", or "unlist".</span></span>
> <span data-ttu-id="27bb5-128">Na przykład nuget.org żądanie usunięcia pakietu jest interpretowane jako "unlist".</span><span class="sxs-lookup"><span data-stu-id="27bb5-128">For example, nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="27bb5-129">Aby uzyskać więcej informacji na temat tego rozwiązania, zobacz [zasady Usuwanie](../nuget-org/policies/deleting-packages.md) pakietów.</span><span class="sxs-lookup"><span data-stu-id="27bb5-129">For more information about this practice, see the [Deleting Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span>

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a><span data-ttu-id="27bb5-130">Praca z uwierzytelnionym kanałami informacyjnymi</span><span class="sxs-lookup"><span data-stu-id="27bb5-130">Work with authenticated feeds</span></span>

<span data-ttu-id="27bb5-131">Użyj [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) do pracy z uwierzytelnianych kanałów informacyjnych.</span><span class="sxs-lookup"><span data-stu-id="27bb5-131">Use [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) to work with authenticated feeds.</span></span>

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a><span data-ttu-id="27bb5-132">NuGet.Packaging</span><span class="sxs-lookup"><span data-stu-id="27bb5-132">NuGet.Packaging</span></span>

<span data-ttu-id="27bb5-133">Zainstaluj `NuGet.Packaging` pakiet, aby wchodzić w `.nupkg` interakcje z `.nuspec` plikami i ze strumienia:</span><span class="sxs-lookup"><span data-stu-id="27bb5-133">Install the `NuGet.Packaging` package to interact with `.nupkg` and `.nuspec` files from a stream:</span></span>

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a><span data-ttu-id="27bb5-134">Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="27bb5-134">Create a package</span></span>

<span data-ttu-id="27bb5-135">Utwórz pakiet, ustaw metadane i dodaj zależności przy użyciu elementu [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="27bb5-135">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="27bb5-136">Zdecydowanie zaleca się, aby pakiety NuGet były tworzone przy użyciu oficjalnych narzędzi NuGet, a **nie** przy użyciu tego interfejsu API niskiego poziomu.</span><span class="sxs-lookup"><span data-stu-id="27bb5-136">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="27bb5-137">W przypadku dobrze utworzonego pakietu istnieją różne charakterystyki, a najnowsza wersja narzędzi ułatwia uwzględnienie tych najlepszych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="27bb5-137">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="27bb5-138">Aby uzyskać więcej informacji na temat tworzenia [](../create-packages/overview-and-workflow.md) pakietów NuGet, zobacz omówienie przepływu pracy tworzenia pakietów i dokumentację dotyczącą oficjalnych narzędzi pakietu (na przykład przy użyciu interfejsu wiersza [polecenia dotnet).](../create-packages/creating-a-package-dotnet-cli.md)</span><span class="sxs-lookup"><span data-stu-id="27bb5-138">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="27bb5-139">Odczytywanie pakietu</span><span class="sxs-lookup"><span data-stu-id="27bb5-139">Read a package</span></span>

<span data-ttu-id="27bb5-140">Odczytaj pakiet ze strumienia plików przy [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) użyciu .</span><span class="sxs-lookup"><span data-stu-id="27bb5-140">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="27bb5-141">Dokumentacja innych firm</span><span class="sxs-lookup"><span data-stu-id="27bb5-141">Third-party documentation</span></span>

<span data-ttu-id="27bb5-142">Przykłady i dokumentację dla niektórych interfejsów API można znaleźć w następującej serii blogów Autorstwa Dave'a Glicka, opublikowanej w 2016 r.:</span><span class="sxs-lookup"><span data-stu-id="27bb5-142">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="27bb5-143">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts (Eksplorowanie bibliotek NuGet w wersji 3, część 1: wprowadzenie i pojęcia)</span><span class="sxs-lookup"><span data-stu-id="27bb5-143">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="27bb5-144">Exploring the NuGet v3 Libraries, Part 2: Searching for packages (Eksplorowanie bibliotek NuGet w wersji 3, część 2: wyszukiwanie pakietów)</span><span class="sxs-lookup"><span data-stu-id="27bb5-144">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="27bb5-145">Eksplorowanie bibliotek NuGet w wersji 3, część 3: instalowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="27bb5-145">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="27bb5-146">Te wpisy w blogu zostały napisane wkrótce po wersji **3.4.3** pakietów zestawu SDK klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="27bb5-146">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="27bb5-147">Nowsze wersje pakietów mogą być niezgodne z informacjami we wpisach w blogu.</span><span class="sxs-lookup"><span data-stu-id="27bb5-147">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="27bb5-148">Martin Björkström opublikował kolejne wpisy w blogu Dave'a Glicka, w którym przedstawia inne podejście do instalowania pakietów NuGet przy użyciu zestawu SDK klienta NuGet:</span><span class="sxs-lookup"><span data-stu-id="27bb5-148">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="27bb5-149">Ponowne poprawianie bibliotek NuGet w wersji 3</span><span class="sxs-lookup"><span data-stu-id="27bb5-149">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
