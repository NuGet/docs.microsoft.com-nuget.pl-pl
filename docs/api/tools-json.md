---
title: Tools. JSON do odnajdywania wersji NuGet. exe
description: Punkt końcowy dla
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: a186db9727bdfd1b55bf73a1f29283352555dede
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611019"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="a42c7-103">Tools. JSON do odnajdywania wersji NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="a42c7-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="a42c7-104">Obecnie istnieje kilka sposobów uzyskania najnowszej wersji pliku NuGet. exe na komputerze w sposób skryptowy.</span><span class="sxs-lookup"><span data-stu-id="a42c7-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="a42c7-105">Na przykład możesz pobrać i wyodrębnić pakiet [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) z NuGet.org. Jest to pewna złożoność, ponieważ wymaga już posiadania pliku NuGet. exe (na potrzeby `nuget.exe install`) lub trzeba rozpakować NUPKG.</span><span class="sxs-lookup"><span data-stu-id="a42c7-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="a42c7-106">Jeśli masz już program NuGet. exe, możesz również użyć `nuget.exe update -self`, ale wymaga to również posiadania istniejącej kopii NuGet. exe.</span><span class="sxs-lookup"><span data-stu-id="a42c7-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="a42c7-107">To podejście powoduje także aktualizację do najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="a42c7-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="a42c7-108">Nie zezwala na korzystanie z określonej wersji.</span><span class="sxs-lookup"><span data-stu-id="a42c7-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="a42c7-109">Punkt końcowy `tools.json` jest dostępny zarówno w celu rozwiązania problemu z uruchamianiem, jak i zapewnienia kontroli wersji programu NuGet. exe pobranej.</span><span class="sxs-lookup"><span data-stu-id="a42c7-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="a42c7-110">Ta usługa może być używana w środowiskach ciągłej integracji/ciągłego wdrażania lub w skryptach niestandardowych w celu odnajdywania i pobierania dowolnej wydanej wersji programu NuGet. exe.</span><span class="sxs-lookup"><span data-stu-id="a42c7-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="a42c7-111">Punkt końcowy `tools.json` można pobrać przy użyciu nieuwierzytelnionego żądania HTTP (np. `Invoke-WebRequest` w programie PowerShell lub `wget`).</span><span class="sxs-lookup"><span data-stu-id="a42c7-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="a42c7-112">Można go przeanalizować przy użyciu deserializacji JSON, a kolejne adresy URL pobierania NuGet. exe mogą być również pobierane przy użyciu nieuwierzytelnionych żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="a42c7-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="a42c7-113">Punkt końcowy można pobrać przy użyciu metody `GET`:</span><span class="sxs-lookup"><span data-stu-id="a42c7-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="a42c7-114">[Schemat JSON](https://json-schema.org/) dla punktu końcowego jest dostępny tutaj:</span><span class="sxs-lookup"><span data-stu-id="a42c7-114">The [JSON schema](https://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="a42c7-115">Reakcji</span><span class="sxs-lookup"><span data-stu-id="a42c7-115">Response</span></span>

<span data-ttu-id="a42c7-116">Odpowiedź to dokument JSON zawierający wszystkie dostępne wersje programu NuGet. exe.</span><span class="sxs-lookup"><span data-stu-id="a42c7-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="a42c7-117">Główny obiekt JSON ma następującą właściwość:</span><span class="sxs-lookup"><span data-stu-id="a42c7-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="a42c7-118">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a42c7-118">Name</span></span>      | <span data-ttu-id="a42c7-119">Typ</span><span class="sxs-lookup"><span data-stu-id="a42c7-119">Type</span></span>             | <span data-ttu-id="a42c7-120">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a42c7-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="a42c7-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="a42c7-121">nuget.exe</span></span> | <span data-ttu-id="a42c7-122">Tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="a42c7-122">array of objects</span></span> | <span data-ttu-id="a42c7-123">opcję</span><span class="sxs-lookup"><span data-stu-id="a42c7-123">yes</span></span>

<span data-ttu-id="a42c7-124">Każdy obiekt w tablicy `nuget.exe` ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="a42c7-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="a42c7-125">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a42c7-125">Name</span></span>     | <span data-ttu-id="a42c7-126">Typ</span><span class="sxs-lookup"><span data-stu-id="a42c7-126">Type</span></span>   | <span data-ttu-id="a42c7-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a42c7-127">Required</span></span> | <span data-ttu-id="a42c7-128">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a42c7-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="a42c7-129">version</span><span class="sxs-lookup"><span data-stu-id="a42c7-129">version</span></span>  | <span data-ttu-id="a42c7-130">string</span><span class="sxs-lookup"><span data-stu-id="a42c7-130">string</span></span> | <span data-ttu-id="a42c7-131">opcję</span><span class="sxs-lookup"><span data-stu-id="a42c7-131">yes</span></span>      | <span data-ttu-id="a42c7-132">Ciąg 2.0.0 SemVer</span><span class="sxs-lookup"><span data-stu-id="a42c7-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="a42c7-133">adres URL</span><span class="sxs-lookup"><span data-stu-id="a42c7-133">url</span></span>      | <span data-ttu-id="a42c7-134">string</span><span class="sxs-lookup"><span data-stu-id="a42c7-134">string</span></span> | <span data-ttu-id="a42c7-135">opcję</span><span class="sxs-lookup"><span data-stu-id="a42c7-135">yes</span></span>      | <span data-ttu-id="a42c7-136">Bezwzględny adres URL do pobierania tej wersji pliku NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="a42c7-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="a42c7-137">Przygotowane</span><span class="sxs-lookup"><span data-stu-id="a42c7-137">stage</span></span>    | <span data-ttu-id="a42c7-138">string</span><span class="sxs-lookup"><span data-stu-id="a42c7-138">string</span></span> | <span data-ttu-id="a42c7-139">opcję</span><span class="sxs-lookup"><span data-stu-id="a42c7-139">yes</span></span>      | <span data-ttu-id="a42c7-140">Ciąg wyliczeniowy</span><span class="sxs-lookup"><span data-stu-id="a42c7-140">An enum string</span></span>
<span data-ttu-id="a42c7-141">wysyłane</span><span class="sxs-lookup"><span data-stu-id="a42c7-141">uploaded</span></span> | <span data-ttu-id="a42c7-142">string</span><span class="sxs-lookup"><span data-stu-id="a42c7-142">string</span></span> | <span data-ttu-id="a42c7-143">opcję</span><span class="sxs-lookup"><span data-stu-id="a42c7-143">yes</span></span>      | <span data-ttu-id="a42c7-144">Przybliżona sygnatura czasowa ISO 8601, gdy wersja została udostępniona</span><span class="sxs-lookup"><span data-stu-id="a42c7-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="a42c7-145">Elementy w tablicy zostaną posortowane w kolejności malejącej, SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="a42c7-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="a42c7-146">Gwarantuje to zmniejszenie obciążenia klienta, który ma największy numer wersji.</span><span class="sxs-lookup"><span data-stu-id="a42c7-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="a42c7-147">Oznacza to jednak, że lista nie jest posortowana w kolejności chronologicznej.</span><span class="sxs-lookup"><span data-stu-id="a42c7-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="a42c7-148">Na przykład jeśli niższa wersja główna jest obsługiwana w dacie późniejszej niż wyższa wersja główna, ta wersja serwisowa nie będzie widoczna w górnej części listy.</span><span class="sxs-lookup"><span data-stu-id="a42c7-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="a42c7-149">Jeśli chcesz, aby Najnowsza wersja została wydana przez *sygnaturę czasową*, po prostu posortuj tablicę według ciągu `uploaded`.</span><span class="sxs-lookup"><span data-stu-id="a42c7-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="a42c7-150">Dzieje się tak, ponieważ sygnatura czasowa `uploaded` jest w formacie [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) , który można sortować chronologicznie przy użyciu sortowania lexicographical (tj. proste sortowanie ciągu).</span><span class="sxs-lookup"><span data-stu-id="a42c7-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="a42c7-151">Właściwość `stage` wskazuje, jak zbadane ta wersja narzędzia.</span><span class="sxs-lookup"><span data-stu-id="a42c7-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="a42c7-152">Przygotowane</span><span class="sxs-lookup"><span data-stu-id="a42c7-152">Stage</span></span>              | <span data-ttu-id="a42c7-153">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="a42c7-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="a42c7-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="a42c7-154">EarlyAccessPreview</span></span> | <span data-ttu-id="a42c7-155">Nie jest jeszcze widoczne na [stronie pobierania](https://www.nuget.org/downloads) i powinny być sprawdzone przez partnerów</span><span class="sxs-lookup"><span data-stu-id="a42c7-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="a42c7-156">Wydano</span><span class="sxs-lookup"><span data-stu-id="a42c7-156">Released</span></span>           | <span data-ttu-id="a42c7-157">Dostępne w witrynie pobierania, ale nie jest jeszcze zalecane do użycia w szerokim zakresie.</span><span class="sxs-lookup"><span data-stu-id="a42c7-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="a42c7-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="a42c7-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="a42c7-159">Dostępne w witrynie pobierania i zalecane do użycia</span><span class="sxs-lookup"><span data-stu-id="a42c7-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="a42c7-160">Jednym z prostych podejścia do uzyskania najnowszej, zalecanej wersji jest wykonanie pierwszej wersji na liście, która ma `stage` wartość `ReleasedAndBlessed`.</span><span class="sxs-lookup"><span data-stu-id="a42c7-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="a42c7-161">To działa, ponieważ wersje są sortowane w kolejności SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="a42c7-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="a42c7-162">Pakiet `NuGet.CommandLine` na nuget.org jest zazwyczaj aktualizowany tylko z wersjami `ReleasedAndBlessed`.</span><span class="sxs-lookup"><span data-stu-id="a42c7-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="a42c7-163">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="a42c7-163">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="a42c7-164">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="a42c7-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
