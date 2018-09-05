---
title: Wykonywanie zapytania o wszystkie pakiety opublikowane w witrynie nuget.org
description: Za pomocą interfejsu API programu NuGet, można wykonywać zapytania o wszystkie pakiety opublikowane w witrynie nuget.org i najnowsze informacje wraz z upływem czasu.
author: joelverhagen
ms.author: jver
ms.date: 11/02/2017
ms.topic: tutorial
ms.reviewer: kraigb
ms.openlocfilehash: 0bd21c427b5b89ae9e5f1500d75e1bf63a96e828
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551081"
---
# <a name="query-for-all-packages-published-to-nugetorg"></a><span data-ttu-id="5f715-103">Wykonywanie zapytania o wszystkie pakiety opublikowane w witrynie nuget.org</span><span class="sxs-lookup"><span data-stu-id="5f715-103">Query for all packages published to nuget.org</span></span>

<span data-ttu-id="5f715-104">Jeden typowy wzorzec zapytania w starszej wersji interfejsu API OData w wersji 2 została wyliczanie wszystkie pakiety opublikowane w witrynie nuget.org, uporządkowane według, gdy pakiet został opublikowany.</span><span class="sxs-lookup"><span data-stu-id="5f715-104">One common query pattern on the legacy OData V2 API was enumerating all packages published to nuget.org, ordered by when the package was published.</span></span> <span data-ttu-id="5f715-105">Scenariusze wymagające tego rodzaju zapytania względem nuget.org są bardzo zróżnicowane:</span><span class="sxs-lookup"><span data-stu-id="5f715-105">Scenarios requiring this kind of query against nuget.org vary widely:</span></span>

- <span data-ttu-id="5f715-106">Replikowanie całkowicie nuget.org</span><span class="sxs-lookup"><span data-stu-id="5f715-106">Replicating nuget.org entirely</span></span>
- <span data-ttu-id="5f715-107">Wykrywanie, gdy nowe wersje wydane pakiety</span><span class="sxs-lookup"><span data-stu-id="5f715-107">Detecting when packages have new versions released</span></span>
- <span data-ttu-id="5f715-108">Wyszukuje pakietów, które są zależne od pakietu</span><span class="sxs-lookup"><span data-stu-id="5f715-108">Finding packages that depend on your package</span></span>

<span data-ttu-id="5f715-109">Starszy sposób zrobić to zwykle zależą sortowanie jednostką pakietu OData przez sygnaturę czasową i stronicowanie w wyniku ogromnej, można ustawić przy użyciu `skip` i `top` parametrów (rozmiar strony).</span><span class="sxs-lookup"><span data-stu-id="5f715-109">The legacy way of doing this typically depended on sorting the OData package entity by a timestamp and paging across the massive result set using `skip` and `top` (page size) parameters.</span></span> <span data-ttu-id="5f715-110">Niestety to podejście ma pewne wady:</span><span class="sxs-lookup"><span data-stu-id="5f715-110">Unfortunately, this approach has some drawbacks:</span></span>

- <span data-ttu-id="5f715-111">Możliwość brakujących pakietów, ponieważ zapytania są wykonywane na danych, które często jest zmiana kolejności</span><span class="sxs-lookup"><span data-stu-id="5f715-111">Possibility of missing packages, because the queries are being made on data that is often changing order</span></span>
- <span data-ttu-id="5f715-112">Wolne czas odpowiedzi na zapytanie, ponieważ nie są zoptymalizowane (najbardziej zoptymalizowane zapytania są te, które obsługuje scenariusz linii głównej dla oficjalne klienta programu NuGet)</span><span class="sxs-lookup"><span data-stu-id="5f715-112">Slow query response time, because the queries are not optimized (the most optimized queries are ones that support a mainline scenario for the official NuGet client)</span></span>
- <span data-ttu-id="5f715-113">Korzystanie z interfejsu API przestarzałe i nieudokumentowane, co oznacza obsługę takich zapytań w przyszłości nie ma żadnej gwarancji.</span><span class="sxs-lookup"><span data-stu-id="5f715-113">Use of deprecated and undocumented API, meaning the support of such queries in the future is not guaranteed</span></span>
- <span data-ttu-id="5f715-114">Brak możliwości odtworzenia historii dokładnie w takiej kolejności, które okazało się</span><span class="sxs-lookup"><span data-stu-id="5f715-114">Inability to replay history in the exact order that it transpired</span></span>

<span data-ttu-id="5f715-115">Z tego powodu można wykonać następującymi wskazówkami dla scenariuszy wyżej w sposób bardziej niezawodne i Zadbaj o przyszłość.</span><span class="sxs-lookup"><span data-stu-id="5f715-115">For this reason, the following guide can be followed to address the aforementioned scenarios in a more reliable and future-proof way.</span></span>

## <a name="overview"></a><span data-ttu-id="5f715-116">Omówienie</span><span class="sxs-lookup"><span data-stu-id="5f715-116">Overview</span></span>

<span data-ttu-id="5f715-117">W środkowej części tego przewodnika jest zasobem w [NuGet API](../../api/overview.md) o nazwie **katalogu**.</span><span class="sxs-lookup"><span data-stu-id="5f715-117">At the center of this guide is resource in the [NuGet API](../../api/overview.md) called the **catalog**.</span></span> <span data-ttu-id="5f715-118">Katalog jest tylko do dołączania interfejsu API, który umożliwia obiektowi wywołującemu wyświetlić pełną historię pakietów, dodawać, modyfikacji i usunąć z repozytorium nuget.org. Jeśli interesuje Cię w całości lub nawet podzbiór pakiety opublikowane w witrynie nuget.org, katalog jest doskonałym sposobem na bieżąco, korzystając z zestawu dostępnych pakietów w.</span><span class="sxs-lookup"><span data-stu-id="5f715-118">The catalog is an append-only API that allows the caller to see a full history of packages added to, modified, and deleted from nuget.org. If you are interested in all or even a subset of packages published to nuget.org, the catalog is a great way to stay up-to-date with the set of currently available packages as time goes on.</span></span>

<span data-ttu-id="5f715-119">Ten przewodnik jest przeznaczony ogólnym opisem, ale jeśli interesują Cię szczegóły dokładną katalogu, zobacz jego [dokument referencyjny dotyczący interfejsu API](../../api/catalog-resource.md).</span><span class="sxs-lookup"><span data-stu-id="5f715-119">This guide is intended to be a high-level walk-through but if you are interested in the fine-grain details of the catalog, see its [API reference document](../../api/catalog-resource.md).</span></span>

<span data-ttu-id="5f715-120">Następujące kroki można zaimplemetować w taki sposób, w dowolnym języku programowania wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5f715-120">The following steps can be implemented in any programming language of your choice.</span></span> <span data-ttu-id="5f715-121">Jeśli chcesz, aby uzyskać pełną próbkę uruchomione, Przyjrzyj się [przykładowy języka C#](#c-sample-code) wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="5f715-121">If you want a full running sample, take a look at the [C# sample](#c-sample-code) mentioned below.</span></span>

<span data-ttu-id="5f715-122">W przeciwnym razie wykonaj przewodnik poniższe tworzenia czytnika niezawodne katalogu.</span><span class="sxs-lookup"><span data-stu-id="5f715-122">Otherwise, follow the guide below to build a reliable catalog reader.</span></span>

## <a name="initialize-a-cursor"></a><span data-ttu-id="5f715-123">Inicjowanie kursora</span><span class="sxs-lookup"><span data-stu-id="5f715-123">Initialize a cursor</span></span>

<span data-ttu-id="5f715-124">Pierwszym krokiem w tworzeniu czytnik niezawodne katalogu implementuje kursora.</span><span class="sxs-lookup"><span data-stu-id="5f715-124">The first step in building a reliable catalog reader is implementing a cursor.</span></span> <span data-ttu-id="5f715-125">Aby uzyskać szczegółowe informacje dotyczące projektowania kursora katalogu, zobacz [dokument referencyjny dotyczący katalogu](../../api/catalog-resource.md#cursor).</span><span class="sxs-lookup"><span data-stu-id="5f715-125">For full details about the design of a catalog cursor, see the [catalog reference document](../../api/catalog-resource.md#cursor).</span></span> <span data-ttu-id="5f715-126">Krótko mówiąc kursor znajduje się punkt w czasie, do której zostały przetworzone zdarzenia w wykazie.</span><span class="sxs-lookup"><span data-stu-id="5f715-126">In short, cursor is a point in time up to which you have processed events in the catalog.</span></span> <span data-ttu-id="5f715-127">Publikuje zdarzenia w pakiecie reprezentują wykazu, i zmienia się inny pakiet.</span><span class="sxs-lookup"><span data-stu-id="5f715-127">Events in the catalog represent package publishes and other package changes.</span></span> <span data-ttu-id="5f715-128">W przypadku interesujące Cię wszystkie pakiety, które kiedykolwiek publikowane NuGet (od początku czasu), użytkownik może ustawić kursor do sygnatury czasowej "wartość minimalna" (np. `DateTime.MinValue` na platformie .NET).</span><span class="sxs-lookup"><span data-stu-id="5f715-128">If you care about all packages ever published to NuGet (since the beginning of time), you would initialize your cursor to a "minimum value" timestamp (e.g. `DateTime.MinValue` in .NET).</span></span> <span data-ttu-id="5f715-129">Jeśli interesujące Cię tylko pakiety opublikowane już teraz, należy użyć bieżącą sygnaturę czasową jako wartość początkowego kursora.</span><span class="sxs-lookup"><span data-stu-id="5f715-129">If you care only about packages published starting now, you would use the current timestamp as your initial cursor value.</span></span>

<span data-ttu-id="5f715-130">W tym przewodniku firma Microsoft będzie zainicjować naszych kursor do sygnatury czasowej godzinę temu.</span><span class="sxs-lookup"><span data-stu-id="5f715-130">For this guide, we'll initialize our cursor to a timestamp one hour ago.</span></span> <span data-ttu-id="5f715-131">Teraz po prostu zapisz tej sygnatury czasowej w pamięci.</span><span class="sxs-lookup"><span data-stu-id="5f715-131">For now, just save that timestamp in memory.</span></span>

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a><span data-ttu-id="5f715-132">Określenia adresu URL indeksu katalogu</span><span class="sxs-lookup"><span data-stu-id="5f715-132">Determine catalog index URL</span></span>

<span data-ttu-id="5f715-133">Lokalizację każdego zasobu (punkt końcowy) w interfejsie API NuGet powinny zostać wykryte przy użyciu [indeks usług](../../api/service-index.md).</span><span class="sxs-lookup"><span data-stu-id="5f715-133">The location of every resource (endpoint) in the NuGet API should be discovered using the [service index](../../api/service-index.md).</span></span> <span data-ttu-id="5f715-134">Ponieważ ten przewodnik skupia się w witrynie nuget.org, będziemy używać indeks usług w witrynie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="5f715-134">Because this guide focuses on nuget.org, we'll be using nuget.org's service index.</span></span>

    GET https://api.nuget.org/v3/index.json

<span data-ttu-id="5f715-135">Dokument usługi jest dokument JSON zawierający wszystkie zasoby w witrynie nuget.org. Poszukaj zasobów having `@type` wartość właściwości `Catalog/3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="5f715-135">The service document is JSON document containing all of the resources on nuget.org. Look for the resource having the `@type` property value of `Catalog/3.0.0`.</span></span> <span data-ttu-id="5f715-136">Skojarzone `@id` wartość właściwości jest adres URL, który indeks katalogu sam.</span><span class="sxs-lookup"><span data-stu-id="5f715-136">The associated `@id` property value is the URL to the catalog index itself.</span></span> 

## <a name="find-new-catalog-leaves"></a><span data-ttu-id="5f715-137">Znajdź nowe liście katalogu</span><span class="sxs-lookup"><span data-stu-id="5f715-137">Find new catalog leaves</span></span>

<span data-ttu-id="5f715-138">Za pomocą `@id` wartości właściwości w poprzednim kroku, Pobierz indeks katalogu:</span><span class="sxs-lookup"><span data-stu-id="5f715-138">Using the `@id` property value found in the previous step, download the catalog index:</span></span>

    GET https://api.nuget.org/v3/catalog0/index.json

<span data-ttu-id="5f715-139">Deserializacji [indeks katalogu](../../api/catalog-resource.md#catalog-index).</span><span class="sxs-lookup"><span data-stu-id="5f715-139">Deserialize the [catalog index](../../api/catalog-resource.md#catalog-index).</span></span> <span data-ttu-id="5f715-140">Odfiltrować wszystkie [strony obiektów katalogu](../../api/catalog-resource.md#catalog-page-object-in-the-index) z `commitTimeStamp` mniejsza niż bieżąca wartość kursora.</span><span class="sxs-lookup"><span data-stu-id="5f715-140">Filter out all [catalog page objects](../../api/catalog-resource.md#catalog-page-object-in-the-index) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="5f715-141">W przypadku pozostałych stron wykazu, Pobierz pełny dokument, za pomocą `@id` właściwości.</span><span class="sxs-lookup"><span data-stu-id="5f715-141">For each remaining catalog page, download the full document using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/page2926.json

<span data-ttu-id="5f715-142">Deserializacji [strona katalogu](../../api/catalog-resource.md#catalog-page).</span><span class="sxs-lookup"><span data-stu-id="5f715-142">Deserialize the [catalog page](../../api/catalog-resource.md#catalog-page).</span></span> <span data-ttu-id="5f715-143">Odfiltrować wszystkie [liścia obiektów katalogu](../../api/catalog-resource.md#catalog-item-object-in-a-page) z `commitTimeStamp` mniejsza niż bieżąca wartość kursora.</span><span class="sxs-lookup"><span data-stu-id="5f715-143">Filter out all [catalog leaf objects](../../api/catalog-resource.md#catalog-item-object-in-a-page) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="5f715-144">Po pobraniu wszystkich stron wykazu nie odfiltrowany masz zestaw obiektów typu liść katalogu reprezentujących pakiety, które zostały opublikowane, nieznajdujące się na liście, listy lub usunięte w okresie między Twoja sygnatura czasowa kursora, a teraz.</span><span class="sxs-lookup"><span data-stu-id="5f715-144">After you have downloaded all of the catalog pages not filtered out, you have a set of catalog leaf objects representing packages that have been published, unlisted, listed, or deleted in the time between your cursor timestamp and now.</span></span>

## <a name="process-catalog-leaves"></a><span data-ttu-id="5f715-145">Pozostawia proces katalogu</span><span class="sxs-lookup"><span data-stu-id="5f715-145">Process catalog leaves</span></span>

<span data-ttu-id="5f715-146">W tym momencie można wykonywać niestandardowe przetwarzania, które Twoim zdaniem na elementy katalogu.</span><span class="sxs-lookup"><span data-stu-id="5f715-146">At this point, you can perform any custom processing you'd like on the catalog items.</span></span> <span data-ttu-id="5f715-147">Jeśli potrzebna jest Identyfikatorem i wersją pakietu, można sprawdzić `nuget:id` i `nuget:version` właściwości w wykazie elementów znalezionych na stronach.</span><span class="sxs-lookup"><span data-stu-id="5f715-147">If all you need is the ID and version of the package, you can inspect the `nuget:id` and `nuget:version` properties on the catalog item objects found in the pages.</span></span> <span data-ttu-id="5f715-148">Pamiętaj przyjrzeć się `@type` właściwości, aby dowiedzieć się, jeśli element katalogu dotyczy istniejącego pakietu lub usuniętych pakietów.</span><span class="sxs-lookup"><span data-stu-id="5f715-148">Make sure to look at the `@type` property to know if the catalog item concerns an existing package or a deleted package.</span></span>

<span data-ttu-id="5f715-149">Jeśli interesuje Cię w metadanych o pakiecie (na przykład na opis, zależności, rozmiar .nupkg, itp.), możesz pobrać [dokumentu liścia katalogu](../../api/catalog-resource.md#catalog-leaf) przy użyciu `@id` właściwości.</span><span class="sxs-lookup"><span data-stu-id="5f715-149">If you are interested in the metadata about the package (such at the description, dependencies, .nupkg size, etc), you can fetch the [catalog leaf document](../../api/catalog-resource.md#catalog-leaf) using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

<span data-ttu-id="5f715-150">Ten dokument zawiera wszystkie metadane objęte [zasób metadanych pakietu](../../api/registration-base-url-resource.md)i nie tylko!</span><span class="sxs-lookup"><span data-stu-id="5f715-150">This document has all of the metadata included in the [package metadata resource](../../api/registration-base-url-resource.md), and more!</span></span>

<span data-ttu-id="5f715-151">Ten krok polega na tym, gdzie wdrożyć logikę niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="5f715-151">This step is where you implement your custom logic.</span></span> <span data-ttu-id="5f715-152">Kroki opisane w tym przewodniku są implementowane w pretty podobnie sposób niezależnie od tego, co robisz z liśćmi katalogu.</span><span class="sxs-lookup"><span data-stu-id="5f715-152">The other steps in this guide are implemented in pretty much the same way not matter what you are doing with the catalog leaves.</span></span>

### <a name="downloading-the-nupkg"></a><span data-ttu-id="5f715-153">Pobieranie .nupkg</span><span class="sxs-lookup"><span data-stu-id="5f715-153">Downloading the .nupkg</span></span>

<span data-ttu-id="5f715-154">Jeśli interesuje Cię pobierania pakietów .nupkg znalezione w wykazie, można użyć [pakietu zawartości zasobów](../../api/package-base-address-resource.md).</span><span class="sxs-lookup"><span data-stu-id="5f715-154">If you are interested in downloading the .nupkg's for packages found in the catalog, you can use the [package content resource](../../api/package-base-address-resource.md).</span></span> <span data-ttu-id="5f715-155">Jednak należy pamiętać, że krótkie opóźnienie podczas pakietu znajduje się w katalogu i gdy jest on dostępny w zasób zawartości pakietu.</span><span class="sxs-lookup"><span data-stu-id="5f715-155">However, note that there is a short delay between when a package is found in catalog and when it's available in the package content resource.</span></span> <span data-ttu-id="5f715-156">W związku z tym jeśli wystąpią `404 Not Found` podczas próby pobierania .nupkg pakietu w katalogu, po prostu ponownie przez krótki czas później.</span><span class="sxs-lookup"><span data-stu-id="5f715-156">Therefore, if you encounter `404 Not Found` when attempting to download a .nupkg for a package that you found in the catalog, simply retry a short time later.</span></span> <span data-ttu-id="5f715-157">Naprawianie to opóźnienie jest śledzona przez problem w usłudze GitHub [3455 # NuGet/NuGetGallery](https://github.com/NuGet/NuGetGallery/issues/3455).</span><span class="sxs-lookup"><span data-stu-id="5f715-157">Fixing this delay is tracked by GitHub issue [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span></span>

## <a name="move-the-cursor-forward"></a><span data-ttu-id="5f715-158">Przenieś kursor do przodu</span><span class="sxs-lookup"><span data-stu-id="5f715-158">Move the cursor forward</span></span>

<span data-ttu-id="5f715-159">Po pomyślnym przetworzeniu elementów katalogu należy określić nową wartość kursor do zapisania.</span><span class="sxs-lookup"><span data-stu-id="5f715-159">Once you have successfully processed the catalog items, you need to determine the new cursor value to save.</span></span> <span data-ttu-id="5f715-160">W tym celu należy znaleźć maksymalną (najnowsze chronologicznie) `commitTimeStamp` wszystkich elementów katalogu, które zostanie przetworzone.</span><span class="sxs-lookup"><span data-stu-id="5f715-160">To do this, find the maximum (latest chronologically) `commitTimeStamp` of all catalog items that you processed.</span></span> <span data-ttu-id="5f715-161">Jest to nowa wartość kursora.</span><span class="sxs-lookup"><span data-stu-id="5f715-161">This is your new cursor value.</span></span> <span data-ttu-id="5f715-162">Zapisz go niektóre magazynu trwałego, takich jak bazy danych, system plików lub usługi blob storage.</span><span class="sxs-lookup"><span data-stu-id="5f715-162">Save it to some persistent store, like a database, file system, or blob storage.</span></span> <span data-ttu-id="5f715-163">Aby uzyskać więcej elementów katalogu, należy po prostu zacznij od [pierwszego kroku](#initialize-a-cursor) przez inicjowanie wartość kursora z tego magazynu trwałego.</span><span class="sxs-lookup"><span data-stu-id="5f715-163">When you want to get more catalog items, simply start from the [first step](#initialize-a-cursor) by initializing your cursor value from this persistent store.</span></span>

<span data-ttu-id="5f715-164">Jeśli aplikacja zgłasza wyjątek lub błędów, nie przenoś kursora do przodu.</span><span class="sxs-lookup"><span data-stu-id="5f715-164">If your application throws an exception or faults, don't move the cursor forward.</span></span> <span data-ttu-id="5f715-165">Przenoszenie do przodu kursora ma co oznacza, że nie będą już ponownie potrzebne do przetwarzania elementów katalogu przed kursor.</span><span class="sxs-lookup"><span data-stu-id="5f715-165">Moving the cursor forward has the meaning that you never again need to process catalog items before your cursor.</span></span>

<span data-ttu-id="5f715-166">Jeśli z jakiegoś powodu masz pozostawia usterkę w sposób przetwarzania wykazu, możesz po prostu przesuń kursor w tył i kodu ponownie przetworzyć starych elementów katalogu.</span><span class="sxs-lookup"><span data-stu-id="5f715-166">If, for some reason, you have a bug in how you process catalog leaves, you can simply move your cursor backward in time and allow your code to reprocess the old catalog items.</span></span>

## <a name="c-sample-code"></a><span data-ttu-id="5f715-167">Przykładowy kod języka C#</span><span class="sxs-lookup"><span data-stu-id="5f715-167">C# sample code</span></span>

<span data-ttu-id="5f715-168">Ponieważ katalog jest zestaw dokumentów JSON, które są dostępne za pośrednictwem protokołu HTTP, może być interakcji z przy użyciu dowolnego języka programowania, którego klient HTTP i JSON Deserializator.</span><span class="sxs-lookup"><span data-stu-id="5f715-168">Because the catalog is a set of JSON documents available over HTTP, it can be interacted with using any programming language that has an HTTP client and JSON deserializer.</span></span>

<span data-ttu-id="5f715-169">Przykłady w języku C# są dostępne w [repozytorium NuGet/Samples](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="5f715-169">C# samples are available in the [NuGet/Samples repository](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span></span>

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a><span data-ttu-id="5f715-170">Katalog zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="5f715-170">Catalog SDK</span></span>

<span data-ttu-id="5f715-171">Najprostszym sposobem korzystania z wykazu jest użyć pakietu SDK katalogu .NET wersji wstępnej: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span><span class="sxs-lookup"><span data-stu-id="5f715-171">The easiest way to consume the catalog is to use the pre-release .NET catalog SDK package: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span></span> <span data-ttu-id="5f715-172">Ten pakiet jest dostępny na `nuget-build` MyGet źródła danych, dla którego możesz użyć pakietu NuGet źródłowy adres URL `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="5f715-172">This package is available on the `nuget-build` MyGet feed, for which you use the NuGet package source URL `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span></span>

<span data-ttu-id="5f715-173">Ten pakiet można zainstalować na projekt niezgodny z `netstandard1.3` lub nowszej (np. .NET Framework 4.6).</span><span class="sxs-lookup"><span data-stu-id="5f715-173">You can install this package to a project compatible with `netstandard1.3` or greater (such as .NET Framework 4.6).</span></span>

<span data-ttu-id="5f715-174">Przykład za pomocą tego pakietu jest dostępny w witrynie GitHub w [projektu NuGet.Protocol.Catalog.Sample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span><span class="sxs-lookup"><span data-stu-id="5f715-174">A sample using this package is available on GitHub in the [NuGet.Protocol.Catalog.Sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="5f715-175">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="5f715-175">Sample output</span></span>

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

### <a name="minimal-sample"></a><span data-ttu-id="5f715-176">Minimalny przykładowy</span><span class="sxs-lookup"><span data-stu-id="5f715-176">Minimal sample</span></span>

<span data-ttu-id="5f715-177">Aby uzyskać przykład zależności w mniej ilustrujący interakcji z katalogu, które bardziej szczegółowo, zobacz [CatalogReaderExample przykładowy projekt](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="5f715-177">For an example with fewer dependencies that illustrates the interaction with the catalog in more detail, see the [CatalogReaderExample sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span></span> <span data-ttu-id="5f715-178">Projekt jest ukierunkowany `netcoreapp2.0` i zależy od [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (w przypadku rozwiązywania indeks usług) i [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (w przypadku deserializacji JSON).</span><span class="sxs-lookup"><span data-stu-id="5f715-178">The project targets `netcoreapp2.0` and depends on the [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (for resolving the service index) and [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (for JSON deserialization).</span></span>

<span data-ttu-id="5f715-179">Główne logikę kodu jest widoczna w [pliku Program.cs](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="5f715-179">The main logic of the code is visible in the [Program.cs file](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="5f715-180">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="5f715-180">Sample output</span></span>

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
