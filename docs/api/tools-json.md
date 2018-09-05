---
title: Tools.JSON nuget.exe wersji odnajdywania
description: Punkt końcowy
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 6184fe8e987e0637cb912999f2e3fa3a3dc9b4ba
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546938"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="42094-103">Tools.JSON nuget.exe wersji odnajdywania</span><span class="sxs-lookup"><span data-stu-id="42094-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="42094-104">Już dziś istnieje kilka sposobów, aby uzyskać najnowszą wersję programu nuget.exe na swojej maszynie w sposób za pomocą skryptów.</span><span class="sxs-lookup"><span data-stu-id="42094-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="42094-105">Na przykład, Pobierz i Wyodrębnij [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) pakietów z witryny nuget.org. Ma złożoność, ponieważ wymaga ona albo, że masz już nuget.exe (dla `nuget.exe install`) lub masz rozpakowywanie .nupkg przy użyciu narzędzia unzip podstawowe i znaleźć wewnątrz binarnego.</span><span class="sxs-lookup"><span data-stu-id="42094-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="42094-106">Jeśli masz już nuget.exe, można również użyć `nuget.exe update -self`, jednak wymaga to również, masz istniejącą kopię nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="42094-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="42094-107">Takie podejście również aktualizacji do najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="42094-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="42094-108">Nie zezwalaj na użycie określonej wersji.</span><span class="sxs-lookup"><span data-stu-id="42094-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="42094-109">`tools.json` Punkt końcowy jest dostępny dla obu problemu bootstrapping i zapewnić kontrolę wersji nuget.exe pobrany.</span><span class="sxs-lookup"><span data-stu-id="42094-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="42094-110">To może służyć w środowiskach ciągłej integracji/ciągłego Dostarczania i niestandardowych skryptów do odnajdywania i Pobierz wszelkie wydanej wersji nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="42094-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="42094-111">`tools.json` Punktu końcowego można pobrać za pomocą nieuwierzytelnione żądania HTTP (np. `Invoke-WebRequest` w programie PowerShell lub `wget`).</span><span class="sxs-lookup"><span data-stu-id="42094-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="42094-112">Można analizować, przy użyciu deserializacji JSON i pobierania nuget.exe kolejne adresy URL można również pobrać za pomocą nieuwierzytelnione żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="42094-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="42094-113">Punkt końcowy można pobrać przy użyciu `GET` metody:</span><span class="sxs-lookup"><span data-stu-id="42094-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="42094-114">[Schematu JSON](http://json-schema.org/) punkt końcowy jest dostępny tutaj:</span><span class="sxs-lookup"><span data-stu-id="42094-114">The [JSON schema](http://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="42094-115">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="42094-115">Response</span></span>

<span data-ttu-id="42094-116">Odpowiedź jest dokumentem JSON, zawierającą wszystkie dostępne wersje nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="42094-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="42094-117">Główny obiekt JSON ma następującą właściwość:</span><span class="sxs-lookup"><span data-stu-id="42094-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="42094-118">Nazwa</span><span class="sxs-lookup"><span data-stu-id="42094-118">Name</span></span>      | <span data-ttu-id="42094-119">Typ</span><span class="sxs-lookup"><span data-stu-id="42094-119">Type</span></span>             | <span data-ttu-id="42094-120">Wymagane</span><span class="sxs-lookup"><span data-stu-id="42094-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="42094-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="42094-121">nuget.exe</span></span> | <span data-ttu-id="42094-122">Tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="42094-122">array of objects</span></span> | <span data-ttu-id="42094-123">Tak</span><span class="sxs-lookup"><span data-stu-id="42094-123">yes</span></span>

<span data-ttu-id="42094-124">Każdy obiekt w `nuget.exe` tablica ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="42094-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="42094-125">Nazwa</span><span class="sxs-lookup"><span data-stu-id="42094-125">Name</span></span>     | <span data-ttu-id="42094-126">Typ</span><span class="sxs-lookup"><span data-stu-id="42094-126">Type</span></span>   | <span data-ttu-id="42094-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="42094-127">Required</span></span> | <span data-ttu-id="42094-128">Uwagi</span><span class="sxs-lookup"><span data-stu-id="42094-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="42094-129">version</span><span class="sxs-lookup"><span data-stu-id="42094-129">version</span></span>  | <span data-ttu-id="42094-130">string</span><span class="sxs-lookup"><span data-stu-id="42094-130">string</span></span> | <span data-ttu-id="42094-131">Tak</span><span class="sxs-lookup"><span data-stu-id="42094-131">yes</span></span>      | <span data-ttu-id="42094-132">Ciąg SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="42094-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="42094-133">adres URL</span><span class="sxs-lookup"><span data-stu-id="42094-133">url</span></span>      | <span data-ttu-id="42094-134">string</span><span class="sxs-lookup"><span data-stu-id="42094-134">string</span></span> | <span data-ttu-id="42094-135">Tak</span><span class="sxs-lookup"><span data-stu-id="42094-135">yes</span></span>      | <span data-ttu-id="42094-136">Bezwzględny adres URL pobierania tej wersji programu nuget.exe</span><span class="sxs-lookup"><span data-stu-id="42094-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="42094-137">etap</span><span class="sxs-lookup"><span data-stu-id="42094-137">stage</span></span>    | <span data-ttu-id="42094-138">string</span><span class="sxs-lookup"><span data-stu-id="42094-138">string</span></span> | <span data-ttu-id="42094-139">Tak</span><span class="sxs-lookup"><span data-stu-id="42094-139">yes</span></span>      | <span data-ttu-id="42094-140">Ciąg typu wyliczeniowego</span><span class="sxs-lookup"><span data-stu-id="42094-140">An enum string</span></span>
<span data-ttu-id="42094-141">Przekazany</span><span class="sxs-lookup"><span data-stu-id="42094-141">uploaded</span></span> | <span data-ttu-id="42094-142">string</span><span class="sxs-lookup"><span data-stu-id="42094-142">string</span></span> | <span data-ttu-id="42094-143">Tak</span><span class="sxs-lookup"><span data-stu-id="42094-143">yes</span></span>      | <span data-ttu-id="42094-144">Przybliżony sygnaturę czasową gdy wersja została udostępniona</span><span class="sxs-lookup"><span data-stu-id="42094-144">An approximate timestamp of when the version was made available</span></span>

<span data-ttu-id="42094-145">Elementy w tablicy zostaną posortowane, malejąco według współczynnika SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="42094-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="42094-146">Gwarancja ta jest przeznaczona do odciążenia wyszukiwania dla najnowszej wersji klienta.</span><span class="sxs-lookup"><span data-stu-id="42094-146">This guarantee is meant to ease the burden on a client looking for the latest version.</span></span> 

<span data-ttu-id="42094-147">`stage` Właściwość wskazuje, jak vettect to narzędzie jest wersja.</span><span class="sxs-lookup"><span data-stu-id="42094-147">The `stage` property indicates how vettect this version of the tool is.</span></span> 

<span data-ttu-id="42094-148">etap</span><span class="sxs-lookup"><span data-stu-id="42094-148">Stage</span></span>              | <span data-ttu-id="42094-149">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="42094-149">Meaning</span></span>
------------------ | ------
<span data-ttu-id="42094-150">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="42094-150">EarlyAccessPreview</span></span> | <span data-ttu-id="42094-151">Jeszcze nie są widoczne na [pobierania strony sieci web](https://www.nuget.org/downloads) i powinny być weryfikowane przez partnerów</span><span class="sxs-lookup"><span data-stu-id="42094-151">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="42094-152">Wydana</span><span class="sxs-lookup"><span data-stu-id="42094-152">Released</span></span>           | <span data-ttu-id="42094-153">Dostępne w witrynie pobierania, ale nie jest jeszcze zalecane w przypadku użycia rozprzestrzeniania się całej</span><span class="sxs-lookup"><span data-stu-id="42094-153">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="42094-154">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="42094-154">ReleasedAndBlessed</span></span> | <span data-ttu-id="42094-155">Dostępne w witrynie pobierania i jest zalecane w przypadku użycia</span><span class="sxs-lookup"><span data-stu-id="42094-155">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="42094-156">Jeden proste podejście do posiadanie najnowszy, zalecana wersja ma mieć pierwszej wersji na liście, który ma `stage` wartość `ReleasedAndBlessed`.</span><span class="sxs-lookup"><span data-stu-id="42094-156">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span>

<span data-ttu-id="42094-157">`NuGet.CommandLine` Pakietu w witrynie nuget.org są zazwyczaj aktualizowane tylko przy użyciu `ReleasedAndBlessed` wersji.</span><span class="sxs-lookup"><span data-stu-id="42094-157">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="42094-158">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="42094-158">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="42094-159">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="42094-159">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
