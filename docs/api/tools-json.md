---
title: tools.jsna potrzeby odnajdywania nuget.exe wersji
description: Punkt końcowy dla
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: eb28ccbc4460663b0f149d2d08e9b47dd69847c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773813"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="fd78d-103">tools.jsna potrzeby odnajdywania nuget.exe wersji</span><span class="sxs-lookup"><span data-stu-id="fd78d-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="fd78d-104">Obecnie istnieje kilka sposobów uzyskania najnowszej wersji nuget.exe na komputerze w sposób skryptowy.</span><span class="sxs-lookup"><span data-stu-id="fd78d-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="fd78d-105">Na przykład możesz pobrać i wyodrębnić [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) pakiet z NuGet.org. Jest to pewna złożoność, ponieważ wymaga już nuget.exe (dla `nuget.exe install` ) lub trzeba rozpakować plik. nupkg przy użyciu podstawowego narzędzia rozpakować i znaleźć dane binarne wewnątrz.</span><span class="sxs-lookup"><span data-stu-id="fd78d-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="fd78d-106">Jeśli masz już nuget.exe, możesz również użyć programu `nuget.exe update -self` , ale wymaga to również istniejącej kopii nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="fd78d-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="fd78d-107">To podejście powoduje także aktualizację do najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="fd78d-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="fd78d-108">Nie zezwala na korzystanie z określonej wersji.</span><span class="sxs-lookup"><span data-stu-id="fd78d-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="fd78d-109">`tools.json`Punkt końcowy jest dostępny zarówno w celu rozwiązywania problemów z uruchamianiem programu, jak i zapewnienia kontroli wersji pobieranych nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="fd78d-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="fd78d-110">Ta usługa może być używana w środowiskach ciągłej integracji/ciągłego wdrażania lub w skryptach niestandardowych w celu odnajdywania i pobierania dowolnej wydanej wersji nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="fd78d-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="fd78d-111">`tools.json`Punkt końcowy można pobrać przy użyciu nieuwierzytelnionego żądania HTTP (np. `Invoke-WebRequest` w programie PowerShell lub `wget` ).</span><span class="sxs-lookup"><span data-stu-id="fd78d-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="fd78d-112">Można ją analizować przy użyciu deserializacji JSON, a kolejne adresy URL pobierania nuget.exe można także pobrać przy użyciu nieuwierzytelnionych żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="fd78d-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="fd78d-113">Punkt końcowy można pobrać przy użyciu `GET` metody:</span><span class="sxs-lookup"><span data-stu-id="fd78d-113">The endpoint can be fetched using the `GET` method:</span></span>

```
GET https://dist.nuget.org/tools.json
```

<span data-ttu-id="fd78d-114">[Schemat JSON](https://json-schema.org/) dla punktu końcowego jest dostępny tutaj:</span><span class="sxs-lookup"><span data-stu-id="fd78d-114">The [JSON schema](https://json-schema.org/) for the endpoint is available here:</span></span>

```
GET https://dist.nuget.org/tools.schema.json
```

## <a name="response"></a><span data-ttu-id="fd78d-115">Reakcja</span><span class="sxs-lookup"><span data-stu-id="fd78d-115">Response</span></span>

<span data-ttu-id="fd78d-116">Odpowiedź to dokument JSON zawierający wszystkie dostępne wersje nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="fd78d-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="fd78d-117">Główny obiekt JSON ma następującą właściwość:</span><span class="sxs-lookup"><span data-stu-id="fd78d-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="fd78d-118">Nazwa</span><span class="sxs-lookup"><span data-stu-id="fd78d-118">Name</span></span>      | <span data-ttu-id="fd78d-119">Typ</span><span class="sxs-lookup"><span data-stu-id="fd78d-119">Type</span></span>             | <span data-ttu-id="fd78d-120">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fd78d-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="fd78d-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="fd78d-121">nuget.exe</span></span> | <span data-ttu-id="fd78d-122">Tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="fd78d-122">array of objects</span></span> | <span data-ttu-id="fd78d-123">tak</span><span class="sxs-lookup"><span data-stu-id="fd78d-123">yes</span></span>

<span data-ttu-id="fd78d-124">Każdy obiekt w `nuget.exe` tablicy ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="fd78d-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="fd78d-125">Nazwa</span><span class="sxs-lookup"><span data-stu-id="fd78d-125">Name</span></span>     | <span data-ttu-id="fd78d-126">Typ</span><span class="sxs-lookup"><span data-stu-id="fd78d-126">Type</span></span>   | <span data-ttu-id="fd78d-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fd78d-127">Required</span></span> | <span data-ttu-id="fd78d-128">Uwagi</span><span class="sxs-lookup"><span data-stu-id="fd78d-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="fd78d-129">Wersja</span><span class="sxs-lookup"><span data-stu-id="fd78d-129">version</span></span>  | <span data-ttu-id="fd78d-130">ciąg</span><span class="sxs-lookup"><span data-stu-id="fd78d-130">string</span></span> | <span data-ttu-id="fd78d-131">tak</span><span class="sxs-lookup"><span data-stu-id="fd78d-131">yes</span></span>      | <span data-ttu-id="fd78d-132">Ciąg 2.0.0 SemVer</span><span class="sxs-lookup"><span data-stu-id="fd78d-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="fd78d-133">url</span><span class="sxs-lookup"><span data-stu-id="fd78d-133">url</span></span>      | <span data-ttu-id="fd78d-134">ciąg</span><span class="sxs-lookup"><span data-stu-id="fd78d-134">string</span></span> | <span data-ttu-id="fd78d-135">tak</span><span class="sxs-lookup"><span data-stu-id="fd78d-135">yes</span></span>      | <span data-ttu-id="fd78d-136">Bezwzględny adres URL pobierania tej wersji nuget.exe</span><span class="sxs-lookup"><span data-stu-id="fd78d-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="fd78d-137">etap</span><span class="sxs-lookup"><span data-stu-id="fd78d-137">stage</span></span>    | <span data-ttu-id="fd78d-138">ciąg</span><span class="sxs-lookup"><span data-stu-id="fd78d-138">string</span></span> | <span data-ttu-id="fd78d-139">tak</span><span class="sxs-lookup"><span data-stu-id="fd78d-139">yes</span></span>      | <span data-ttu-id="fd78d-140">Ciąg wyliczeniowy</span><span class="sxs-lookup"><span data-stu-id="fd78d-140">An enum string</span></span>
<span data-ttu-id="fd78d-141">wysyłane</span><span class="sxs-lookup"><span data-stu-id="fd78d-141">uploaded</span></span> | <span data-ttu-id="fd78d-142">ciąg</span><span class="sxs-lookup"><span data-stu-id="fd78d-142">string</span></span> | <span data-ttu-id="fd78d-143">tak</span><span class="sxs-lookup"><span data-stu-id="fd78d-143">yes</span></span>      | <span data-ttu-id="fd78d-144">Przybliżona sygnatura czasowa ISO 8601, gdy wersja została udostępniona</span><span class="sxs-lookup"><span data-stu-id="fd78d-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="fd78d-145">Elementy w tablicy zostaną posortowane w kolejności malejącej, SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="fd78d-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="fd78d-146">Gwarantuje to zmniejszenie obciążenia klienta, który ma największy numer wersji.</span><span class="sxs-lookup"><span data-stu-id="fd78d-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="fd78d-147">Oznacza to jednak, że lista nie jest posortowana w kolejności chronologicznej.</span><span class="sxs-lookup"><span data-stu-id="fd78d-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="fd78d-148">Na przykład jeśli niższa wersja główna jest obsługiwana w dacie późniejszej niż wyższa wersja główna, ta wersja serwisowa nie będzie widoczna w górnej części listy.</span><span class="sxs-lookup"><span data-stu-id="fd78d-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="fd78d-149">Jeśli chcesz, aby Najnowsza wersja została wydana przez *sygnaturę czasową*, po prostu posortuj tablicę według `uploaded` ciągu.</span><span class="sxs-lookup"><span data-stu-id="fd78d-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="fd78d-150">Dzieje się tak, ponieważ `uploaded` sygnatura czasowa znajduje się w formacie [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) , który można sortować chronologicznie przy użyciu sortowania lexicographical (tj. proste sortowanie ciągu).</span><span class="sxs-lookup"><span data-stu-id="fd78d-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="fd78d-151">`stage`Właściwość wskazuje, jak zbadane ta wersja narzędzia.</span><span class="sxs-lookup"><span data-stu-id="fd78d-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="fd78d-152">Etap</span><span class="sxs-lookup"><span data-stu-id="fd78d-152">Stage</span></span>              | <span data-ttu-id="fd78d-153">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="fd78d-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="fd78d-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="fd78d-154">EarlyAccessPreview</span></span> | <span data-ttu-id="fd78d-155">Nie jest jeszcze widoczne na [stronie pobierania](https://www.nuget.org/downloads) i powinny być sprawdzone przez partnerów</span><span class="sxs-lookup"><span data-stu-id="fd78d-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="fd78d-156">Wydano</span><span class="sxs-lookup"><span data-stu-id="fd78d-156">Released</span></span>           | <span data-ttu-id="fd78d-157">Dostępne w witrynie pobierania, ale nie jest jeszcze zalecane do użycia w szerokim zakresie.</span><span class="sxs-lookup"><span data-stu-id="fd78d-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="fd78d-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="fd78d-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="fd78d-159">Dostępne w witrynie pobierania i zalecane do użycia</span><span class="sxs-lookup"><span data-stu-id="fd78d-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="fd78d-160">Jednym z prostych podejścia do uzyskania najnowszej, zalecanej wersji jest wykonanie pierwszej wersji na liście, która ma `stage` wartość `ReleasedAndBlessed` .</span><span class="sxs-lookup"><span data-stu-id="fd78d-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="fd78d-161">To działa, ponieważ wersje są sortowane w kolejności SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="fd78d-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="fd78d-162">`NuGet.CommandLine`Pakiet w programie NuGet.org jest zazwyczaj aktualizowany tylko przy użyciu `ReleasedAndBlessed` wersji.</span><span class="sxs-lookup"><span data-stu-id="fd78d-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="fd78d-163">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="fd78d-163">Sample request</span></span>

```
GET https://dist.nuget.org/tools.json
```

### <a name="sample-response"></a><span data-ttu-id="fd78d-164">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="fd78d-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
