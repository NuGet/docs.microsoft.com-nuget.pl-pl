---
title: Zestaw SDK klienta programu NuGet
description: Interfejs API jest rozwijającą się i nie jest jeszcze udokumentowane, ale przykłady są dostępne na blogu Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 8f96bf289e8121fd25262fb95c2f36dfc89045c5
ms.sourcegitcommit: 9f94e00428d83aef4a7a87db679129eff7720c59
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/03/2019
ms.locfileid: "58911039"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="1f1dd-103">Zestaw SDK klienta programu NuGet</span><span class="sxs-lookup"><span data-stu-id="1f1dd-103">NuGet Client SDK</span></span>

> [!Note]
> <span data-ttu-id="1f1dd-104">Nie należy mylić z [NuGet *Web* interfejsu API](https://docs.microsoft.com/en-us/nuget/api/overview)</span><span class="sxs-lookup"><span data-stu-id="1f1dd-104">Not to be confused with the [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span></span>

<span data-ttu-id="1f1dd-105">*Zestawu SDK klienta usługi NuGet* odnosi się do grupy bibliotek .NET, a ich tematyka wokół [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), i [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span><span class="sxs-lookup"><span data-stu-id="1f1dd-105">The *NuGet Client SDK* refers to a group of .NET libraries centered around [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="1f1dd-106">Te pakiety Zastąp wcześniej [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) biblioteki.</span><span class="sxs-lookup"><span data-stu-id="1f1dd-106">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

<span data-ttu-id="1f1dd-107">Pracujemy nad o stabilne powierzchni, firma Microsoft wkrótce dokumentu.</span><span class="sxs-lookup"><span data-stu-id="1f1dd-107">We are working on having a stable surface area that we can document soon.</span></span>

## <a name="source-code"></a><span data-ttu-id="1f1dd-108">Kod źródłowy</span><span class="sxs-lookup"><span data-stu-id="1f1dd-108">Source code</span></span>

<span data-ttu-id="1f1dd-109">Kod źródłowy jest opublikowany w usłudze GitHub w projekcie [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span><span class="sxs-lookup"><span data-stu-id="1f1dd-109">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="1f1dd-110">Dokumentacja usługi innych firm</span><span class="sxs-lookup"><span data-stu-id="1f1dd-110">Third-party documentation</span></span>

<span data-ttu-id="1f1dd-111">Przykłady i dokumentację dla niektórych interfejsu API można znaleźć w następującego cyklu blogów przez Dave Glick, opublikowane 2016:</span><span class="sxs-lookup"><span data-stu-id="1f1dd-111">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="1f1dd-112">Eksplorowanie NuGet w wersji 3 biblioteki, część 1: Wprowadzenie i pojęcia</span><span class="sxs-lookup"><span data-stu-id="1f1dd-112">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="1f1dd-113">Eksplorowanie NuGet w wersji 3 biblioteki, część 2: Wyszukiwanie pakietów</span><span class="sxs-lookup"><span data-stu-id="1f1dd-113">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="1f1dd-114">Eksplorowanie NuGet w wersji 3 biblioteki, część 3: Instalowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="1f1dd-114">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="1f1dd-115">Wpisy na blogu zostały napisane wkrótce po **3.4.3** wersji pakietu NuGet zostały wydane pakiety zestawu SDK klienta.</span><span class="sxs-lookup"><span data-stu-id="1f1dd-115">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="1f1dd-116">Nowsze wersje pakietów mogą być niezgodne z informacjami w wpisów w blogu.</span><span class="sxs-lookup"><span data-stu-id="1f1dd-116">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="1f1dd-117">Martin Björkström czy wpis w blogu monitowania na serię wpisów w blogu Dave Glick, gdzie przedstawia różne podejście na temat używania zestawu SDK klienta NuGet na instalowanie pakietów NuGet:</span><span class="sxs-lookup"><span data-stu-id="1f1dd-117">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK for installing NuGet packages:</span></span>

- [<span data-ttu-id="1f1dd-118">Ponowne spojrzenie na NuGet biblioteki v3</span><span class="sxs-lookup"><span data-stu-id="1f1dd-118">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
