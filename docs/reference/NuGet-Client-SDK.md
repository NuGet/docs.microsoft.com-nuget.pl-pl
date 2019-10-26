---
title: Zestaw SDK klienta NuGet
description: Interfejs API jest rozwijany i nie został jeszcze udokumentowany, ale przykłady są dostępne w blogu Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 873bde467a39653b818b49173d53bc983e99d1b9
ms.sourcegitcommit: f9645fc5f49c18978e12a292a3f832e162e069d5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/25/2019
ms.locfileid: "72924603"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="72cd0-103">Zestaw SDK klienta NuGet</span><span class="sxs-lookup"><span data-stu-id="72cd0-103">NuGet Client SDK</span></span>

<span data-ttu-id="72cd0-104">*Zestaw SDK klienta NuGet* odwołuje się do grupy pakietów NuGet wyśrodkowanych wokół [NuGet. polecenia](https://www.nuget.org/packages/NuGet.Commands), [NuGet. pakowanie](https://www.nuget.org/packages/NuGet.Packaging)i [NuGet. Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span><span class="sxs-lookup"><span data-stu-id="72cd0-104">The *NuGet Client SDK* refers to a group of NuGet packages centered around [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [NuGet.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="72cd0-105">Te pakiety zastępują wcześniejszą bibliotekę [NuGet. Core](https://www.nuget.org/packages/NuGet.Core/) .</span><span class="sxs-lookup"><span data-stu-id="72cd0-105">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

> [!Note]
>  <span data-ttu-id="72cd0-106">Aby uzyskać dokumentację dotyczącą protokołu serwera NuGet, zapoznaj się z [interfejsem API serwera NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="72cd0-106">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="source-code"></a><span data-ttu-id="72cd0-107">Kod źródłowy</span><span class="sxs-lookup"><span data-stu-id="72cd0-107">Source code</span></span>

<span data-ttu-id="72cd0-108">Kod źródłowy jest publikowany w witrynie GitHub w projekcie [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client).</span><span class="sxs-lookup"><span data-stu-id="72cd0-108">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="72cd0-109">Dokumentacja dotycząca innych firm</span><span class="sxs-lookup"><span data-stu-id="72cd0-109">Third-party documentation</span></span>

<span data-ttu-id="72cd0-110">Przykłady i Dokumentacja dla niektórych interfejsów API można znaleźć w następujących seriach blogów: Dave Glick, opublikowano 2016.</span><span class="sxs-lookup"><span data-stu-id="72cd0-110">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="72cd0-111">Eksplorowanie bibliotek programu NuGet v3, część 1: wprowadzenie i pojęcia</span><span class="sxs-lookup"><span data-stu-id="72cd0-111">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="72cd0-112">Eksplorowanie bibliotek programu NuGet v3, część 2: wyszukiwanie pakietów</span><span class="sxs-lookup"><span data-stu-id="72cd0-112">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="72cd0-113">Eksplorowanie bibliotek programu NuGet v3, część 3: Instalowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="72cd0-113">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="72cd0-114">Te wpisy w blogu zostały ogłoszone wkrótce po wydaniu wersji **3.4.3** pakietów SDK klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="72cd0-114">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="72cd0-115">Nowsze wersje pakietów mogą być niezgodne z informacjami w wpisach w blogu.</span><span class="sxs-lookup"><span data-stu-id="72cd0-115">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="72cd0-116">Martin Björkström zakończył wpis w blogu do serii blogów Dave Glick, gdzie wprowadzono inne podejście do korzystania z zestawu SDK klienta NuGet do instalowania pakietów NuGet:</span><span class="sxs-lookup"><span data-stu-id="72cd0-116">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK for installing NuGet packages:</span></span>

- [<span data-ttu-id="72cd0-117">Ponowne odwiedzanie bibliotek NuGet v3</span><span class="sxs-lookup"><span data-stu-id="72cd0-117">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
