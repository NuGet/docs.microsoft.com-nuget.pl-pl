---
title: Tools.JSON nuget.exe wersji odnajdywania
description: Punkt końcowy
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 003139abac7808dbdaef4aa66119e09772db2b4f
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852536"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="2c722-103">Tools.JSON nuget.exe wersji odnajdywania</span><span class="sxs-lookup"><span data-stu-id="2c722-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="2c722-104">Już dziś istnieje kilka sposobów, aby uzyskać najnowszą wersję programu nuget.exe na swojej maszynie w sposób za pomocą skryptów.</span><span class="sxs-lookup"><span data-stu-id="2c722-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="2c722-105">Na przykład, Pobierz i Wyodrębnij [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) pakietów z witryny nuget.org. Ma złożoność, ponieważ wymaga ona albo, że masz już nuget.exe (dla `nuget.exe install`) lub masz rozpakowywanie .nupkg przy użyciu narzędzia unzip podstawowe i znaleźć wewnątrz binarnego.</span><span class="sxs-lookup"><span data-stu-id="2c722-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="2c722-106">Jeśli masz już nuget.exe, można również użyć `nuget.exe update -self`, jednak wymaga to również, masz istniejącą kopię nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="2c722-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="2c722-107">Takie podejście również aktualizacji do najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="2c722-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="2c722-108">Nie zezwalaj na użycie określonej wersji.</span><span class="sxs-lookup"><span data-stu-id="2c722-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="2c722-109">`tools.json` Punkt końcowy jest dostępny dla obu problemu bootstrapping i zapewnić kontrolę wersji nuget.exe pobrany.</span><span class="sxs-lookup"><span data-stu-id="2c722-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="2c722-110">To może służyć w środowiskach ciągłej integracji/ciągłego Dostarczania i niestandardowych skryptów do odnajdywania i Pobierz wszelkie wydanej wersji nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="2c722-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="2c722-111">`tools.json` Punktu końcowego można pobrać za pomocą nieuwierzytelnione żądania HTTP (np. `Invoke-WebRequest` w programie PowerShell lub `wget`).</span><span class="sxs-lookup"><span data-stu-id="2c722-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="2c722-112">Można analizować, przy użyciu deserializacji JSON i pobierania nuget.exe kolejne adresy URL można również pobrać za pomocą nieuwierzytelnione żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="2c722-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="2c722-113">Punkt końcowy można pobrać przy użyciu `GET` metody:</span><span class="sxs-lookup"><span data-stu-id="2c722-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="2c722-114">[Schematu JSON](http://json-schema.org/) punkt końcowy jest dostępny tutaj:</span><span class="sxs-lookup"><span data-stu-id="2c722-114">The [JSON schema](http://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="2c722-115">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="2c722-115">Response</span></span>

<span data-ttu-id="2c722-116">Odpowiedź jest dokumentem JSON, zawierającą wszystkie dostępne wersje nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="2c722-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="2c722-117">Główny obiekt JSON ma następującą właściwość:</span><span class="sxs-lookup"><span data-stu-id="2c722-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="2c722-118">Nazwa</span><span class="sxs-lookup"><span data-stu-id="2c722-118">Name</span></span>      | <span data-ttu-id="2c722-119">Typ</span><span class="sxs-lookup"><span data-stu-id="2c722-119">Type</span></span>             | <span data-ttu-id="2c722-120">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2c722-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="2c722-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="2c722-121">nuget.exe</span></span> | <span data-ttu-id="2c722-122">Tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="2c722-122">array of objects</span></span> | <span data-ttu-id="2c722-123">tak</span><span class="sxs-lookup"><span data-stu-id="2c722-123">yes</span></span>

<span data-ttu-id="2c722-124">Każdy obiekt w `nuget.exe` tablica ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="2c722-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="2c722-125">Nazwa</span><span class="sxs-lookup"><span data-stu-id="2c722-125">Name</span></span>     | <span data-ttu-id="2c722-126">Typ</span><span class="sxs-lookup"><span data-stu-id="2c722-126">Type</span></span>   | <span data-ttu-id="2c722-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2c722-127">Required</span></span> | <span data-ttu-id="2c722-128">Uwagi</span><span class="sxs-lookup"><span data-stu-id="2c722-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="2c722-129">version</span><span class="sxs-lookup"><span data-stu-id="2c722-129">version</span></span>  | <span data-ttu-id="2c722-130">string</span><span class="sxs-lookup"><span data-stu-id="2c722-130">string</span></span> | <span data-ttu-id="2c722-131">tak</span><span class="sxs-lookup"><span data-stu-id="2c722-131">yes</span></span>      | <span data-ttu-id="2c722-132">Ciąg SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="2c722-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="2c722-133">url</span><span class="sxs-lookup"><span data-stu-id="2c722-133">url</span></span>      | <span data-ttu-id="2c722-134">string</span><span class="sxs-lookup"><span data-stu-id="2c722-134">string</span></span> | <span data-ttu-id="2c722-135">tak</span><span class="sxs-lookup"><span data-stu-id="2c722-135">yes</span></span>      | <span data-ttu-id="2c722-136">Bezwzględny adres URL pobierania tej wersji programu nuget.exe</span><span class="sxs-lookup"><span data-stu-id="2c722-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="2c722-137">etap</span><span class="sxs-lookup"><span data-stu-id="2c722-137">stage</span></span>    | <span data-ttu-id="2c722-138">string</span><span class="sxs-lookup"><span data-stu-id="2c722-138">string</span></span> | <span data-ttu-id="2c722-139">tak</span><span class="sxs-lookup"><span data-stu-id="2c722-139">yes</span></span>      | <span data-ttu-id="2c722-140">Ciąg typu wyliczeniowego</span><span class="sxs-lookup"><span data-stu-id="2c722-140">An enum string</span></span>
<span data-ttu-id="2c722-141">Przekazany</span><span class="sxs-lookup"><span data-stu-id="2c722-141">uploaded</span></span> | <span data-ttu-id="2c722-142">string</span><span class="sxs-lookup"><span data-stu-id="2c722-142">string</span></span> | <span data-ttu-id="2c722-143">tak</span><span class="sxs-lookup"><span data-stu-id="2c722-143">yes</span></span>      | <span data-ttu-id="2c722-144">Przybliżony ISO 8601 sygnaturę czasową gdy wersja została udostępniona</span><span class="sxs-lookup"><span data-stu-id="2c722-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="2c722-145">Elementy w tablicy zostaną posortowane, malejąco według współczynnika SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="2c722-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="2c722-146">Gwarancja jest przeznaczone do zmniejszenia obciążenia klienta, który jest zainteresowany najwyższy numer wersji.</span><span class="sxs-lookup"><span data-stu-id="2c722-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="2c722-147">Jednak oznacza to, że lista nie jest posortowana w kolejności chronologicznej.</span><span class="sxs-lookup"><span data-stu-id="2c722-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="2c722-148">Na przykład jeśli starszej wersji głównych jest obsługiwane w terminie później niż w nowszej wersji głównej, ta wersja obsługiwanych nie pojawi się w górnej części listy.</span><span class="sxs-lookup"><span data-stu-id="2c722-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="2c722-149">Jeśli chcesz, aby najnowszej wersji wydawanych przez *sygnatura czasowa*, po prostu posortować tablicę za `uploaded` ciągu.</span><span class="sxs-lookup"><span data-stu-id="2c722-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="2c722-150">To działa, ponieważ `uploaded` jest sygnatura czasowa [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) formatu, który być sortowane w porządku chronologicznym za pomocą sortowania lexicographical (czyli sortowania prostego ciągu).</span><span class="sxs-lookup"><span data-stu-id="2c722-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="2c722-151">`stage` Właściwość wskazuje, jak sprawdzonego jest ta wersja narzędzia.</span><span class="sxs-lookup"><span data-stu-id="2c722-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="2c722-152">Etap</span><span class="sxs-lookup"><span data-stu-id="2c722-152">Stage</span></span>              | <span data-ttu-id="2c722-153">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="2c722-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="2c722-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="2c722-154">EarlyAccessPreview</span></span> | <span data-ttu-id="2c722-155">Jeszcze nie są widoczne na [pobierania strony sieci web](https://www.nuget.org/downloads) i powinny być weryfikowane przez partnerów</span><span class="sxs-lookup"><span data-stu-id="2c722-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="2c722-156">Wydana</span><span class="sxs-lookup"><span data-stu-id="2c722-156">Released</span></span>           | <span data-ttu-id="2c722-157">Dostępne w witrynie pobierania, ale nie jest jeszcze zalecane w przypadku użycia rozprzestrzeniania się całej</span><span class="sxs-lookup"><span data-stu-id="2c722-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="2c722-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="2c722-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="2c722-159">Dostępne w witrynie pobierania i jest zalecane w przypadku użycia</span><span class="sxs-lookup"><span data-stu-id="2c722-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="2c722-160">Jeden proste podejście do posiadanie najnowszy, zalecana wersja ma mieć pierwszej wersji na liście, który ma `stage` wartość `ReleasedAndBlessed`.</span><span class="sxs-lookup"><span data-stu-id="2c722-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="2c722-161">To działa, ponieważ wersje są sortowane w kolejności SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="2c722-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="2c722-162">`NuGet.CommandLine` Pakietu w witrynie nuget.org są zazwyczaj aktualizowane tylko przy użyciu `ReleasedAndBlessed` wersji.</span><span class="sxs-lookup"><span data-stu-id="2c722-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="2c722-163">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="2c722-163">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="2c722-164">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="2c722-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
