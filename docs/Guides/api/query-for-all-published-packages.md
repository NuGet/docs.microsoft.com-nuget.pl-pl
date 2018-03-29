---
title: Zapytania dla wszystkich pakietów opublikowane nuget.org | Dokumentacja firmy Microsoft
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 11/02/2017
ms.topic: tutorial
ms.prod: nuget
ms.technology: ''
description: Przy użyciu interfejsu API programu NuGet, można wysyłać zapytania dotyczące wszystkich pakietów opublikowane nuget.org i aktualności wraz z upływem czasu.
keywords: Interfejs API NuGet wyliczyć wszystkie pakiety, replikowania pakiety NuGet interfejsu API, najnowszych pakietów opublikowany nuget.org
ms.reviewer:
- karann
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 5ea11e1b4edd87b6d30d3838986ca60aaa77870f
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="query-for-all-packages-published-to-nugetorg"></a><span data-ttu-id="6b233-104">Zapytania dla wszystkich pakietów opublikowane nuget.org</span><span class="sxs-lookup"><span data-stu-id="6b233-104">Query for all packages published to nuget.org</span></span>

<span data-ttu-id="6b233-105">Jeden wspólnego wzorca zapytania na starszego interfejsu API 2 OData został wyliczania wszystkie pakiety opublikowane nuget.org, uporządkowanych według Jeśli pakiet został opublikowany.</span><span class="sxs-lookup"><span data-stu-id="6b233-105">One common query pattern on the legacy OData V2 API was enumerating all packages published to nuget.org, ordered by when the package was published.</span></span> <span data-ttu-id="6b233-106">Scenariusze wymagające tego rodzaju zapytania dotyczącego nuget.org różnią się znacznie:</span><span class="sxs-lookup"><span data-stu-id="6b233-106">Scenarios requiring this kind of query against nuget.org vary widely:</span></span>

- <span data-ttu-id="6b233-107">Replikowanie całkowicie nuget.org</span><span class="sxs-lookup"><span data-stu-id="6b233-107">Replicating nuget.org entirely</span></span>
- <span data-ttu-id="6b233-108">Wykrywanie, gdy pakiety zawierają nowe wersje wydane</span><span class="sxs-lookup"><span data-stu-id="6b233-108">Detecting when packages have new versions released</span></span>
- <span data-ttu-id="6b233-109">Znajdowanie pakiety, które są zależne od pakietu</span><span class="sxs-lookup"><span data-stu-id="6b233-109">Finding packages that depend on your package</span></span>

<span data-ttu-id="6b233-110">Starsze sposobów to zwykle była uzależniona od sortowania jednostką OData pakietu przez sygnaturę czasową i stronicowania na ogromną wynik ustawić za pomocą `skip` i `top` parametrów (rozmiar strony).</span><span class="sxs-lookup"><span data-stu-id="6b233-110">The legacy way of doing this typically depended on sorting the OData package entity by a timestamp and paging across the massive result set using `skip` and `top` (page size) parameters.</span></span> <span data-ttu-id="6b233-111">Niestety ta metoda ma kilka wad:</span><span class="sxs-lookup"><span data-stu-id="6b233-111">Unfortunately, this approach has some drawbacks:</span></span>

- <span data-ttu-id="6b233-112">Możliwość brakujących pakietów, ponieważ zapytania są określane na dane, które często jest zmiana kolejności</span><span class="sxs-lookup"><span data-stu-id="6b233-112">Possibility of missing packages, because the queries are being made on data that is often changing order</span></span>
- <span data-ttu-id="6b233-113">Powolna czas odpowiedzi na zapytanie, ponieważ nie są zoptymalizowane (najbardziej zoptymalizowane zapytania są scenariusza połączeniach klienta NuGet oficjalny)</span><span class="sxs-lookup"><span data-stu-id="6b233-113">Slow query response time, because the queries are not optimized (the most optimized queries are ones that support a mainline scenario for the official NuGet client)</span></span>
- <span data-ttu-id="6b233-114">Użyj interfejsu API przestarzałe i nieudokumentowanej, co oznacza obsługę tych zapytań w przyszłości nie jest gwarantowana.</span><span class="sxs-lookup"><span data-stu-id="6b233-114">Use of deprecated and undocumented API, meaning the support of such queries in the future is not guaranteed</span></span>
- <span data-ttu-id="6b233-115">Brak możliwości powtarzania historii dokładnie w takiej kolejności, która okazało się</span><span class="sxs-lookup"><span data-stu-id="6b233-115">Inability to replay history in the exact order that it transpired</span></span>

<span data-ttu-id="6b233-116">Z tego powodu następującymi wskazówkami można wykonać w celu rozwiązania scenariuszy wyżej wymienione w sposób bardziej niezawodne i zabezpieczenie przyszłych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="6b233-116">For this reason, the following guide can be followed to address the aforementioned scenarios in a more reliable and future-proof way.</span></span>

## <a name="overview"></a><span data-ttu-id="6b233-117">Omówienie</span><span class="sxs-lookup"><span data-stu-id="6b233-117">Overview</span></span>

<span data-ttu-id="6b233-118">W Centrum w tym przewodniku jest zasobem w [NuGet API](../../api/overview.md) o nazwie **katalogu**.</span><span class="sxs-lookup"><span data-stu-id="6b233-118">At the center of this guide is resource in the [NuGet API](../../api/overview.md) called the **catalog**.</span></span> <span data-ttu-id="6b233-119">Katalog jest tylko do dołączania interfejsu API, który umożliwia obiekt wywołujący, aby wyświetlić pełną historię pakietów dodawać, modyfikować i usunięty z nuget.org. Jeśli interesuje Cię wszystkich lub nawet podzbiór pakietów opublikowane nuget.org, katalog jest to dobry sposób na bieżąco z zestawem pakiety aktualnie dostępne w.</span><span class="sxs-lookup"><span data-stu-id="6b233-119">The catalog is an append-only API that allows the caller to see a full history of packages added to, modified, and deleted from nuget.org. If you are interested in all or even a subset of packages published to nuget.org, the catalog is a great way to stay up-to-date with the set of currently available packages as time goes on.</span></span>

<span data-ttu-id="6b233-120">Ten przewodnik jest przeznaczony ogólnym opisem, ale jeśli planuje się szczegóły szczegółowe dzielenie katalogu, zobacz jego [dokumentu odwołania API](../../api/catalog-resource.md).</span><span class="sxs-lookup"><span data-stu-id="6b233-120">This guide is intended to be a high-level walk-through but if you are interested in the fine-grain details of the catalog, see its [API reference document](../../api/catalog-resource.md).</span></span>

<span data-ttu-id="6b233-121">Poniższe kroki można zaimplementować w dowolnym języku programowania wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6b233-121">The following steps can be implemented in any programming language of your choice.</span></span> <span data-ttu-id="6b233-122">Jeśli chcesz pełny przykład uruchomione, Przyjrzyjmy się [próbki C#](#c-sample-code) wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="6b233-122">If you want a full running sample, take a look at the [C# sample](#c-sample-code) mentioned below.</span></span>

<span data-ttu-id="6b233-123">W przeciwnym razie wykonaj przewodnik poniżej do utworzenia czytnika niezawodnej katalogu.</span><span class="sxs-lookup"><span data-stu-id="6b233-123">Otherwise, follow the guide below to build a reliable catalog reader.</span></span>

## <a name="initialize-a-cursor"></a><span data-ttu-id="6b233-124">Inicjowanie kursora</span><span class="sxs-lookup"><span data-stu-id="6b233-124">Initialize a cursor</span></span>

<span data-ttu-id="6b233-125">Pierwszym krokiem podczas tworzenia czytnika niezawodnej katalogu implementuje kursora.</span><span class="sxs-lookup"><span data-stu-id="6b233-125">The first step in building a reliable catalog reader is implementing a cursor.</span></span> <span data-ttu-id="6b233-126">Aby uzyskać szczegółowe informacje dotyczące projektowania kursora katalogu, zobacz [katalogu odwołania dokumentu](../../api/catalog-resource.md#cursor).</span><span class="sxs-lookup"><span data-stu-id="6b233-126">For full details about the design of a catalog cursor, see the [catalog reference document](../../api/catalog-resource.md#cursor).</span></span> <span data-ttu-id="6b233-127">Krótko mówiąc kursor jest punkt w czasie, do której zostały przetworzone zdarzenia w katalogu.</span><span class="sxs-lookup"><span data-stu-id="6b233-127">In short, cursor is a point in time up to which you have processed events in the catalog.</span></span> <span data-ttu-id="6b233-128">Zdarzenia w katalogu pakietu reprezentują publikuje i zmienia inny pakiet.</span><span class="sxs-lookup"><span data-stu-id="6b233-128">Events in the catalog represent package publishes and other package changes.</span></span> <span data-ttu-id="6b233-129">Jeśli interesują wszystkie pakiety kiedykolwiek opublikowane NuGet (od początku czasu), może ustawić kursor do sygnatury czasowej "minimalna wartość" (np. `DateTime.MinValue` w .NET).</span><span class="sxs-lookup"><span data-stu-id="6b233-129">If you care about all packages ever published to NuGet (since the beginning of time), you would initialize your cursor to a "minimum value" timestamp (e.g. `DateTime.MinValue` in .NET).</span></span> <span data-ttu-id="6b233-130">Jeśli Cię interesuje tylko pakiety opublikowane już teraz, można użyć jako wartość początkowego kursora bieżącą sygnaturę czasową.</span><span class="sxs-lookup"><span data-stu-id="6b233-130">If you care only about packages published starting now, you would use the current timestamp as your initial cursor value.</span></span>

<span data-ttu-id="6b233-131">Tego przewodnika firma Microsoft będzie zainicjować naszych kursora prowadzącego do sygnatury czasowej godzinę temu.</span><span class="sxs-lookup"><span data-stu-id="6b233-131">For this guide, we'll initialize our cursor to a timestamp one hour ago.</span></span> <span data-ttu-id="6b233-132">Teraz Zapisz ten znacznik w pamięci.</span><span class="sxs-lookup"><span data-stu-id="6b233-132">For now, just save that timestamp in memory.</span></span>

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a><span data-ttu-id="6b233-133">Określić adres URL katalogu indeksu</span><span class="sxs-lookup"><span data-stu-id="6b233-133">Determine catalog index URL</span></span>

<span data-ttu-id="6b233-134">Lokalizację każdego zasobu (punkt końcowy) w interfejsie API NuGet powinny zostać wykryte przy użyciu [indeksu usługi](../../api/service-index.md).</span><span class="sxs-lookup"><span data-stu-id="6b233-134">The location of every resource (endpoint) in the NuGet API should be discovered using the [service index](../../api/service-index.md).</span></span> <span data-ttu-id="6b233-135">Ponieważ ten przewodnik koncentruje się na nuget.org, będziemy używać indeksu usługi nuget.org.</span><span class="sxs-lookup"><span data-stu-id="6b233-135">Because this guide focuses on nuget.org, we'll be using nuget.org's service index.</span></span>

    GET https://api.nuget.org/v3/index.json

<span data-ttu-id="6b233-136">Dokument usługi jest zawierająca wszystkie zasoby na nuget.org dokumentu JSON. Wyszukaj o zasobów `@type` wartość właściwości `Catalog/3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="6b233-136">The service document is JSON document containing all of the resources on nuget.org. Look for the resource having the `@type` property value of `Catalog/3.0.0`.</span></span> <span data-ttu-id="6b233-137">Skojarzony `@id` wartość właściwości jest adres URL, który sam indeks katalogu.</span><span class="sxs-lookup"><span data-stu-id="6b233-137">The associated `@id` property value is the URL to the catalog index itself.</span></span> 

## <a name="find-new-catalog-leaves"></a><span data-ttu-id="6b233-138">Znajdowanie nowych pozostawia katalogu</span><span class="sxs-lookup"><span data-stu-id="6b233-138">Find new catalog leaves</span></span>

<span data-ttu-id="6b233-139">Przy użyciu `@id` indeks katalogu pobierania wartości właściwości w poprzednim kroku:</span><span class="sxs-lookup"><span data-stu-id="6b233-139">Using the `@id` property value found in the previous step, download the catalog index:</span></span>

    GET https://api.nuget.org/v3/catalog0/index.json

<span data-ttu-id="6b233-140">Deserializacja [indeks katalogu](../../api/catalog-resource.md#catalog-index).</span><span class="sxs-lookup"><span data-stu-id="6b233-140">Deserialize the [catalog index](../../api/catalog-resource.md#catalog-index).</span></span> <span data-ttu-id="6b233-141">Wszystkie odfiltrowane [katalogowania obiektów strony](../../api/catalog-resource.md#catalog-page-object-in-the-index) z `commitTimeStamp` mniejsza niż bieżąca wartość kursora.</span><span class="sxs-lookup"><span data-stu-id="6b233-141">Filter out all [catalog page objects](../../api/catalog-resource.md#catalog-page-object-in-the-index) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="6b233-142">W przypadku pozostałych stron katalogu, Pobierz przy użyciu pełnego dokumentu `@id` właściwości.</span><span class="sxs-lookup"><span data-stu-id="6b233-142">For each remaining catalog page, download the full document using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/page2926.json

<span data-ttu-id="6b233-143">Deserializacja [strona katalogu](../../api/catalog-resource.md#catalog-page).</span><span class="sxs-lookup"><span data-stu-id="6b233-143">Deserialize the [catalog page](../../api/catalog-resource.md#catalog-page).</span></span> <span data-ttu-id="6b233-144">Wszystkie odfiltrowane [katalogowania obiektów typu liść](../../api/catalog-resource.md#catalog-item-object-in-a-page) z `commitTimeStamp` mniejsza niż bieżąca wartość kursora.</span><span class="sxs-lookup"><span data-stu-id="6b233-144">Filter out all [catalog leaf objects](../../api/catalog-resource.md#catalog-item-object-in-a-page) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="6b233-145">Po pobraniu wszystkich stron katalogu nie odfiltrowany istnieje zestaw obiektów typu liść katalogu reprezentujących pakiety, które zostały opublikowane, nieznajdujące się na liście, listy lub usunięte w okresie między sygnatury czasowej użytkownika kursora, a teraz.</span><span class="sxs-lookup"><span data-stu-id="6b233-145">After you have downloaded all of the catalog pages not filtered out, you have a set of catalog leaf objects representing packages that have been published, unlisted, listed, or deleted in the time between your cursor timestamp and now.</span></span>

## <a name="process-catalog-leaves"></a><span data-ttu-id="6b233-146">Pozostawia katalogu procesu</span><span class="sxs-lookup"><span data-stu-id="6b233-146">Process catalog leaves</span></span>

<span data-ttu-id="6b233-147">W tym momencie można wykonywać żadnych niestandardowych przetwarzania, które mają na elementów katalogu.</span><span class="sxs-lookup"><span data-stu-id="6b233-147">At this point, you can perform any custom processing you'd like on the catalog items.</span></span> <span data-ttu-id="6b233-148">Jeśli wszystko, czego potrzebujesz Identyfikatora i wersję pakietu, możesz sprawdzić `nuget:id` i `nuget:version` znalezionych na stronach elementu właściwości w katalogu.</span><span class="sxs-lookup"><span data-stu-id="6b233-148">If all you need is the ID and version of the package, you can inspect the `nuget:id` and `nuget:version` properties on the catalog item objects found in the pages.</span></span> <span data-ttu-id="6b233-149">Upewnij się, że przyjrzeć się `@type` właściwości, aby dowiedzieć się, jeśli element katalogu dotyczy istniejącego pakietu lub usuniętych pakietów.</span><span class="sxs-lookup"><span data-stu-id="6b233-149">Make sure to look at the `@type` property to know if the catalog item concerns an existing package or a deleted package.</span></span>

<span data-ttu-id="6b233-150">Jeśli interesuje Cię w metadanych o pakiecie (na przykład opis, zależności, rozmiar .nupkg, itp.), można pobrać [dokumentu liścia katalogu](../../api/catalog-resource.md#catalog-leaf) przy użyciu `@id` właściwości.</span><span class="sxs-lookup"><span data-stu-id="6b233-150">If you are interested in the metadata about the package (such at the description, dependencies, .nupkg size, etc), you can fetch the [catalog leaf document](../../api/catalog-resource.md#catalog-leaf) using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

<span data-ttu-id="6b233-151">Ten dokument zawiera wszystkie zawarte w metadanych [pakietu zasobów metadanych](../../api/registration-base-url-resource.md)i nie tylko!</span><span class="sxs-lookup"><span data-stu-id="6b233-151">This document has all of the metadata included in the [package metadata resource](../../api/registration-base-url-resource.md), and more!</span></span>

<span data-ttu-id="6b233-152">Ten krok polega na tym, gdzie wdrożyć niestandardowej logiki.</span><span class="sxs-lookup"><span data-stu-id="6b233-152">This step is where you implement your custom logic.</span></span> <span data-ttu-id="6b233-153">Pozostałe kroki w tym przewodniku są implementowane w pretty znacznie taki sam sposób niezależnie od tego, czynności z liśćmi katalogu.</span><span class="sxs-lookup"><span data-stu-id="6b233-153">The other steps in this guide are implemented in pretty much the same way not matter what you are doing with the catalog leaves.</span></span>

### <a name="downloading-the-nupkg"></a><span data-ttu-id="6b233-154">Pobieranie .nupkg</span><span class="sxs-lookup"><span data-stu-id="6b233-154">Downloading the .nupkg</span></span>

<span data-ttu-id="6b233-155">Jeśli interesuje Cię w czasie pobierania pakietów .nupkg odnaleziono w katalogu, można użyć [pakietu zawartości zasobów](../../api/package-base-address-resource.md).</span><span class="sxs-lookup"><span data-stu-id="6b233-155">If you are interested in downloading the .nupkg's for packages found in the catalog, you can use the [package content resource](../../api/package-base-address-resource.md).</span></span> <span data-ttu-id="6b233-156">Jednak należy pamiętać, że krótkie opóźnienie podczas pakietu znajduje się w katalogu i gdy jest dostępny w zasobie zawartości pakietu.</span><span class="sxs-lookup"><span data-stu-id="6b233-156">However, note that there is a short delay between when a package is found in catalog and when it's available in the package content resource.</span></span> <span data-ttu-id="6b233-157">W związku z tym jeśli wystąpią `404 Not Found` podczas próby pobrania .nupkg dla pakietu, który można znaleźć w katalogu, po prostu ponownie przez krótki czas później.</span><span class="sxs-lookup"><span data-stu-id="6b233-157">Therefore, if you encounter `404 Not Found` when attempting to download a .nupkg for a package that you found in the catalog, simply retry a short time later.</span></span> <span data-ttu-id="6b233-158">Ustalenie to opóźnienie jest śledzony przez problem GitHub [&#3455; NuGet/NuGetGallery](https://github.com/NuGet/NuGetGallery/issues/3455).</span><span class="sxs-lookup"><span data-stu-id="6b233-158">Fixing this delay is tracked by GitHub issue [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span></span>

## <a name="move-the-cursor-forward"></a><span data-ttu-id="6b233-159">Przeniesienie kursora do przodu</span><span class="sxs-lookup"><span data-stu-id="6b233-159">Move the cursor forward</span></span>

<span data-ttu-id="6b233-160">Po pomyślnie zostały przetworzone elementy katalogu, należy określić nową wartość kursora do zapisania.</span><span class="sxs-lookup"><span data-stu-id="6b233-160">Once you have successfully processed the catalog items, you need to determine the new cursor value to save.</span></span> <span data-ttu-id="6b233-161">W tym celu Znajdź maksymalną (najnowsze porządku chronologicznym) `commitTimeStamp` wszystkich elementów katalogu, które zostanie przetworzone.</span><span class="sxs-lookup"><span data-stu-id="6b233-161">To do this, find the maximum (latest chronologically) `commitTimeStamp` of all catalog items that you processed.</span></span> <span data-ttu-id="6b233-162">Jest to z nową wartością kursora.</span><span class="sxs-lookup"><span data-stu-id="6b233-162">This is your new cursor value.</span></span> <span data-ttu-id="6b233-163">Zapisz go w niektórych magazynu trwałego, takich jak bazy danych, system plików lub magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="6b233-163">Save it to some persistent store, like a database, file system, or blob storage.</span></span> <span data-ttu-id="6b233-164">Aby uzyskać więcej elementów katalogu, należy po prostu Rozpocznij od [pierwszy krok](#initialize-a-cursor) przez inicjowanie wartość kursora z tego magazynu trwałego.</span><span class="sxs-lookup"><span data-stu-id="6b233-164">When you want to get more catalog items, simply start from the [first step](#initialize-a-cursor) by initializing your cursor value from this persistent store.</span></span>

<span data-ttu-id="6b233-165">Jeśli aplikacja zgłasza wyjątek lub błędy, nie przenoś kursora do przodu.</span><span class="sxs-lookup"><span data-stu-id="6b233-165">If your application throws an exception or faults, don't move the cursor forward.</span></span> <span data-ttu-id="6b233-166">Przesuń kursor do przodu ma znaczenie, nigdy nie ponownie potrzebne do przetwarzania elementów katalogu przed kursor.</span><span class="sxs-lookup"><span data-stu-id="6b233-166">Moving the cursor forward has the meaning that you never again need to process catalog items before your cursor.</span></span>

<span data-ttu-id="6b233-167">Jeśli z jakiegoś powodu masz pozostawia na usterkę w sposób przetwarzania katalogu, możesz po prostu przesuń wskaźnik do tyłu w czasie i kodu tak ponownie przetworzyć starych elementów katalogu.</span><span class="sxs-lookup"><span data-stu-id="6b233-167">If, for some reason, you have a bug in how you process catalog leaves, you can simply move your cursor backward in time and allow your code to reprocess the old catalog items.</span></span>

## <a name="c-sample-code"></a><span data-ttu-id="6b233-168">Przykładowy kod C#</span><span class="sxs-lookup"><span data-stu-id="6b233-168">C# sample code</span></span>

<span data-ttu-id="6b233-169">Ponieważ katalog jest zestawem dokumentów JSON, które są dostępne za pośrednictwem protokołu HTTP, może być interakcji z przy użyciu dowolnego języka programowania, klient HTTP i deserializacji JSON.</span><span class="sxs-lookup"><span data-stu-id="6b233-169">Because the catalog is a set of JSON documents available over HTTP, it can be interacted with using any programming language that has an HTTP client and JSON deserializer.</span></span>

<span data-ttu-id="6b233-170">Przykłady dotyczące języka C# są dostępne w [repozytorium NuGet/przykłady](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="6b233-170">C# samples are available in the [NuGet/Samples repository](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span></span>

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a><span data-ttu-id="6b233-171">W katalogu zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="6b233-171">Catalog SDK</span></span>

<span data-ttu-id="6b233-172">Najprostszym sposobem korzystania z katalogu jest użycie pakietu SDK katalogu .NET wersji wstępnej: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span><span class="sxs-lookup"><span data-stu-id="6b233-172">The easiest way to consume the catalog is to use the pre-release .NET catalog SDK package: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span></span> <span data-ttu-id="6b233-173">Ten pakiet jest dostępny na `nuget-build` MyGet źródła danych, dla którego używają adres URL źródła pakietu NuGet `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="6b233-173">This package is available on the `nuget-build` MyGet feed, for which you use the NuGet package source URL `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span></span>

<span data-ttu-id="6b233-174">Ten pakiet można zainstalować na projekt niezgodny z `netstandard1.3` lub nowszej (na przykład .NET Framework 4.6).</span><span class="sxs-lookup"><span data-stu-id="6b233-174">You can install this package to a project compatible with `netstandard1.3` or greater (such as .NET Framework 4.6).</span></span>

<span data-ttu-id="6b233-175">Przykład za pomocą tego pakietu jest dostępna w witrynie GitHub w [projektu NuGet.Protocol.Catalog.Sample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span><span class="sxs-lookup"><span data-stu-id="6b233-175">A sample using this package is available on GitHub in the [NuGet.Protocol.Catalog.Sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="6b233-176">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="6b233-176">Sample output</span></span>

```output
2017-11-10T22:16:44.8689025+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.2.
2017-11-10T22:16:54.6972769+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.1.
2017-11-10T22:19:20.6385542+00:00: Found package details leaf for Platform.EnUnity 1.0.8.
...
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.1.
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.2.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
Processing the catalog leafs failed. Retrying.
fail: NuGet.Protocol.Catalog.LoggerCatalogLeafProcessor[0]
      10 catalog commits have been processed. We will now simulate a failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      Failed to process leaf https://api.nuget.org/v3/catalog0/data/2017.11.10.23.07.23/veiculox.model.0.0.15.json (VeiculoX.Model 0.0.15, PackageDetails).
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      13 out of 59 leaves were left incomplete due to a processing failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      1 out of 1 pages were left incomplete due to a processing failure.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
2017-11-10T23:07:33.0212446+00:00: Found package details leaf for VeiculoX.Model 0.0.14.
2017-11-10T23:07:41.6621837+00:00: Found package details leaf for VeiculoX.Model 0.0.13.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for CreaSoft.Composition.Web.Extensions 1.1.0.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for DarkXaHTeP.Extensions.Configuration.Consul 0.0.4.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime 14.3.25407.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.Intellisense 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.StandardClassification 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.ManagedInterfaces 8.0.50727.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.2.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
```

### <a name="minimal-sample"></a><span data-ttu-id="6b233-177">Minimalny próbki</span><span class="sxs-lookup"><span data-stu-id="6b233-177">Minimal sample</span></span>

<span data-ttu-id="6b233-178">Na przykład z zależnościami mniej ilustrujący interakcji z katalogu bardziej szczegółowo w temacie [CatalogReaderExample przykładowy projekt](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="6b233-178">For an example with fewer dependencies that illustrates the interaction with the catalog in more detail, see the [CatalogReaderExample sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span></span> <span data-ttu-id="6b233-179">Obiekty docelowe projektu `netcoreapp2.0` i zależy od [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (na potrzeby rozpoznawania indeksu service) i [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (w przypadku deserializacji JSON).</span><span class="sxs-lookup"><span data-stu-id="6b233-179">The project targets `netcoreapp2.0` and depends on the [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (for resolving the service index) and [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (for JSON deserialization).</span></span>

<span data-ttu-id="6b233-180">Logiki główny kodu jest widoczny w [pliku Program.cs](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="6b233-180">The main logic of the code is visible in the [Program.cs file](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="6b233-181">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="6b233-181">Sample output</span></span>

```output
No cursor found. Defaulting to 11/2/2017 9:41:28 PM.
Fetched catalog index https://api.nuget.org/v3/catalog0/index.json.
Fetched catalog page https://api.nuget.org/v3/catalog0/page2935.json.
Processing 69 catalog leaves.
11/2/2017 9:32:35 PM: DotVVM.Compiler.Light 1.1.7 (type is nuget:PackageDetails)
11/2/2017 9:32:35 PM: Momentum.Pm.Api 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:32:44 PM: Momentum.Pm.PortalApi 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Standard 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Core 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.Serialization.Bond 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.AmazonS3 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.DocumentStores.DocumentDb 1.0.6 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.BlobStorage 1.0.5 (type is nuget:PackageDetails)
...
11/2/2017 10:23:54 PM: Cake.GitPackager 0.1.2 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet.AssemblyLoading 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Deployment 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Common.MSBuild 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: InstaClient 1.0.2 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: SecureStrConvertor.VARUN_RUSIYA 1.0.0.5 (type is nuget:PackageDetails)
Writing cursor value: 11/2/2017 10:26:36 PM.
```
