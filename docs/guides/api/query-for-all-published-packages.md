---
title: Zapytanie dla wszystkich pakietów opublikowanych w celu nuget.org
description: Za pomocą interfejsu API NuGet, można zbadać dla wszystkich pakietów opublikowanych do nuget.org i bądź na bieżąco w czasie.
author: joelverhagen
ms.author: jver
ms.date: 11/02/2017
ms.topic: tutorial
ms.reviewer: kraigb
ms.openlocfilehash: 0bd21c427b5b89ae9e5f1500d75e1bf63a96e828
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498232"
---
# <a name="query-for-all-packages-published-to-nugetorg"></a><span data-ttu-id="b1153-103">Zapytanie dla wszystkich pakietów opublikowanych w celu nuget.org</span><span class="sxs-lookup"><span data-stu-id="b1153-103">Query for all packages published to nuget.org</span></span>

<span data-ttu-id="b1153-104">Jeden typowy wzorzec kwerendy na starszych OData V2 API było wyliczenie wszystkich pakietów opublikowanych do nuget.org, uporządkowane przez kiedy pakiet został opublikowany.</span><span class="sxs-lookup"><span data-stu-id="b1153-104">One common query pattern on the legacy OData V2 API was enumerating all packages published to nuget.org, ordered by when the package was published.</span></span> <span data-ttu-id="b1153-105">Scenariusze wymagające tego rodzaju zapytania względem nuget.org różnią się znacznie:</span><span class="sxs-lookup"><span data-stu-id="b1153-105">Scenarios requiring this kind of query against nuget.org vary widely:</span></span>

- <span data-ttu-id="b1153-106">Całkowicie replikując nuget.org</span><span class="sxs-lookup"><span data-stu-id="b1153-106">Replicating nuget.org entirely</span></span>
- <span data-ttu-id="b1153-107">Wykrywanie, kiedy pakiety mają nowe wersje wydane</span><span class="sxs-lookup"><span data-stu-id="b1153-107">Detecting when packages have new versions released</span></span>
- <span data-ttu-id="b1153-108">Znajdowanie pakietów zależnych od pakietu</span><span class="sxs-lookup"><span data-stu-id="b1153-108">Finding packages that depend on your package</span></span>

<span data-ttu-id="b1153-109">Starszy sposób wykonywania tego zwykle zależy od sortowania jednostki pakietu OData przez sygnaturę `skip` `top` czasową i stronicowania w ogromnej zestaw wyników przy użyciu i (rozmiar strony) parametry.</span><span class="sxs-lookup"><span data-stu-id="b1153-109">The legacy way of doing this typically depended on sorting the OData package entity by a timestamp and paging across the massive result set using `skip` and `top` (page size) parameters.</span></span> <span data-ttu-id="b1153-110">Niestety, takie podejście ma pewne wady:</span><span class="sxs-lookup"><span data-stu-id="b1153-110">Unfortunately, this approach has some drawbacks:</span></span>

- <span data-ttu-id="b1153-111">Możliwość brakujących pakietów, ponieważ zapytania są dokonywane na danych, które często zmieniają kolejność</span><span class="sxs-lookup"><span data-stu-id="b1153-111">Possibility of missing packages, because the queries are being made on data that is often changing order</span></span>
- <span data-ttu-id="b1153-112">Powolny czas odpowiedzi na kwerendy, ponieważ kwerendy nie są zoptymalizowane (najbardziej zoptymalizowane zapytania to te, które obsługują scenariusz linii głównej dla oficjalnego klienta NuGet)</span><span class="sxs-lookup"><span data-stu-id="b1153-112">Slow query response time, because the queries are not optimized (the most optimized queries are ones that support a mainline scenario for the official NuGet client)</span></span>
- <span data-ttu-id="b1153-113">Korzystanie z przestarzałego i nieudokumentowanego INTERFEJSU API, co oznacza, że obsługa takich zapytań w przyszłości nie jest gwarantowana</span><span class="sxs-lookup"><span data-stu-id="b1153-113">Use of deprecated and undocumented API, meaning the support of such queries in the future is not guaranteed</span></span>
- <span data-ttu-id="b1153-114">Niezdolność do powtórki historii w dokładnie kolejności, w jakiej się wydarzyła</span><span class="sxs-lookup"><span data-stu-id="b1153-114">Inability to replay history in the exact order that it transpired</span></span>

<span data-ttu-id="b1153-115">Z tego powodu można śledzić poniższy przewodnik, aby rozwiązać wyżej wymienione scenariusze w bardziej niezawodny i przyszłościowy sposób.</span><span class="sxs-lookup"><span data-stu-id="b1153-115">For this reason, the following guide can be followed to address the aforementioned scenarios in a more reliable and future-proof way.</span></span>

## <a name="overview"></a><span data-ttu-id="b1153-116">Omówienie</span><span class="sxs-lookup"><span data-stu-id="b1153-116">Overview</span></span>

<span data-ttu-id="b1153-117">W centrum tego przewodnika znajduje się zasób w [interfejsie API NuGet](../../api/overview.md) o nazwie **katalog**.</span><span class="sxs-lookup"><span data-stu-id="b1153-117">At the center of this guide is resource in the [NuGet API](../../api/overview.md) called the **catalog**.</span></span> <span data-ttu-id="b1153-118">Katalog jest interfejsem API tylko do dołączania, który umożliwia wywołującemu, aby zobaczyć pełną historię pakietów dodanych, zmodyfikowanych i usuniętych z nuget.org. Jeśli jesteś zainteresowany wszystkim lub nawet podzbiorem pakietów opublikowanych w nuget.org, katalog jest świetnym sposobem, aby być na bieżąco z zestawem aktualnie dostępnych pakietów w miarę upływu czasu.</span><span class="sxs-lookup"><span data-stu-id="b1153-118">The catalog is an append-only API that allows the caller to see a full history of packages added to, modified, and deleted from nuget.org. If you are interested in all or even a subset of packages published to nuget.org, the catalog is a great way to stay up-to-date with the set of currently available packages as time goes on.</span></span>

<span data-ttu-id="b1153-119">Ten przewodnik ma być przejściem wysokiego poziomu, ale jeśli jesteś zainteresowany szczegółowymi szczegółami katalogu, zobacz jego [dokument referencyjny interfejsu API](../../api/catalog-resource.md).</span><span class="sxs-lookup"><span data-stu-id="b1153-119">This guide is intended to be a high-level walk-through but if you are interested in the fine-grain details of the catalog, see its [API reference document](../../api/catalog-resource.md).</span></span>

<span data-ttu-id="b1153-120">Poniższe kroki można zaimplementować w dowolnym wybranym języku programowania.</span><span class="sxs-lookup"><span data-stu-id="b1153-120">The following steps can be implemented in any programming language of your choice.</span></span> <span data-ttu-id="b1153-121">Jeśli chcesz pełnego uruchomionego przykładu, spójrz na [przykład języka C#,](#c-sample-code) o którym mowa poniżej.</span><span class="sxs-lookup"><span data-stu-id="b1153-121">If you want a full running sample, take a look at the [C# sample](#c-sample-code) mentioned below.</span></span>

<span data-ttu-id="b1153-122">W przeciwnym razie postępuj zgodnie z poniższym przewodnikiem, aby utworzyć niezawodny czytnik katalogów.</span><span class="sxs-lookup"><span data-stu-id="b1153-122">Otherwise, follow the guide below to build a reliable catalog reader.</span></span>

## <a name="initialize-a-cursor"></a><span data-ttu-id="b1153-123">Inicjowanie kursora</span><span class="sxs-lookup"><span data-stu-id="b1153-123">Initialize a cursor</span></span>

<span data-ttu-id="b1153-124">Pierwszym krokiem w tworzeniu niezawodnego czytnika katalogów jest wdrożenie kursora.</span><span class="sxs-lookup"><span data-stu-id="b1153-124">The first step in building a reliable catalog reader is implementing a cursor.</span></span> <span data-ttu-id="b1153-125">Aby uzyskać szczegółowe informacje na temat projektowania kursora katalogu, zobacz [dokument referencyjny katalogu](../../api/catalog-resource.md#cursor).</span><span class="sxs-lookup"><span data-stu-id="b1153-125">For full details about the design of a catalog cursor, see the [catalog reference document](../../api/catalog-resource.md#cursor).</span></span> <span data-ttu-id="b1153-126">Krótko mówiąc, kursor jest punktem w czasie, do którego zostały przetworzone zdarzenia w katalogu.</span><span class="sxs-lookup"><span data-stu-id="b1153-126">In short, cursor is a point in time up to which you have processed events in the catalog.</span></span> <span data-ttu-id="b1153-127">Zdarzenia w katalogu reprezentują pakiet publikuje i inne zmiany pakietu.</span><span class="sxs-lookup"><span data-stu-id="b1153-127">Events in the catalog represent package publishes and other package changes.</span></span> <span data-ttu-id="b1153-128">Jeśli zależy Ci na wszystkich pakietach kiedykolwiek opublikowanych w NuGet (od początku czasu), należy zainicjować kursor do `DateTime.MinValue` "minimalnej wartości" sygnatury czasowej (np. w .NET).</span><span class="sxs-lookup"><span data-stu-id="b1153-128">If you care about all packages ever published to NuGet (since the beginning of time), you would initialize your cursor to a "minimum value" timestamp (e.g. `DateTime.MinValue` in .NET).</span></span> <span data-ttu-id="b1153-129">Jeśli zależy Ci tylko na pakietach opublikowanych od teraz, użyjesz bieżącego sygnatury czasowej jako początkowej wartości kursora.</span><span class="sxs-lookup"><span data-stu-id="b1153-129">If you care only about packages published starting now, you would use the current timestamp as your initial cursor value.</span></span>

<span data-ttu-id="b1153-130">W tym przewodniku zainicjujemy nasz kursor do sygnatury czasowej godzinę temu.</span><span class="sxs-lookup"><span data-stu-id="b1153-130">For this guide, we'll initialize our cursor to a timestamp one hour ago.</span></span> <span data-ttu-id="b1153-131">Na razie po prostu zapisz ten sygnatura czasowa w pamięci.</span><span class="sxs-lookup"><span data-stu-id="b1153-131">For now, just save that timestamp in memory.</span></span>

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a><span data-ttu-id="b1153-132">Określanie adresu URL indeksu wykazu</span><span class="sxs-lookup"><span data-stu-id="b1153-132">Determine catalog index URL</span></span>

<span data-ttu-id="b1153-133">Lokalizacja każdego zasobu (punktu końcowego) w interfejsie API NuGet powinna zostać odkryta przy użyciu [indeksu usługi.](../../api/service-index.md)</span><span class="sxs-lookup"><span data-stu-id="b1153-133">The location of every resource (endpoint) in the NuGet API should be discovered using the [service index](../../api/service-index.md).</span></span> <span data-ttu-id="b1153-134">Ponieważ ten przewodnik koncentruje się na nuget.org, będziemy używać indeksu usługi nuget.org.</span><span class="sxs-lookup"><span data-stu-id="b1153-134">Because this guide focuses on nuget.org, we'll be using nuget.org's service index.</span></span>

    GET https://api.nuget.org/v3/index.json

<span data-ttu-id="b1153-135">Dokument serwisu jest dokumentem JSON zawierającym wszystkie zasoby na nuget.org. Poszukaj zasobu `@type` o `Catalog/3.0.0`wartości właściwości .</span><span class="sxs-lookup"><span data-stu-id="b1153-135">The service document is JSON document containing all of the resources on nuget.org. Look for the resource having the `@type` property value of `Catalog/3.0.0`.</span></span> <span data-ttu-id="b1153-136">Skojarzona `@id` wartość właściwości jest adresem URL samego indeksu katalogu.</span><span class="sxs-lookup"><span data-stu-id="b1153-136">The associated `@id` property value is the URL to the catalog index itself.</span></span> 

## <a name="find-new-catalog-leaves"></a><span data-ttu-id="b1153-137">Znajdź nowe liście katalogu</span><span class="sxs-lookup"><span data-stu-id="b1153-137">Find new catalog leaves</span></span>

<span data-ttu-id="b1153-138">Korzystając `@id` z wartości właściwości znalezionej w poprzednim kroku, pobierz indeks katalogu:</span><span class="sxs-lookup"><span data-stu-id="b1153-138">Using the `@id` property value found in the previous step, download the catalog index:</span></span>

    GET https://api.nuget.org/v3/catalog0/index.json

<span data-ttu-id="b1153-139">Deserialize [indeksu katalogu](../../api/catalog-resource.md#catalog-index).</span><span class="sxs-lookup"><span data-stu-id="b1153-139">Deserialize the [catalog index](../../api/catalog-resource.md#catalog-index).</span></span> <span data-ttu-id="b1153-140">Odfiltruj wszystkie `commitTimeStamp` obiekty strony [katalogu](../../api/catalog-resource.md#catalog-page-object-in-the-index) z mniejszą lub równą bieżącej wartości kursora.</span><span class="sxs-lookup"><span data-stu-id="b1153-140">Filter out all [catalog page objects](../../api/catalog-resource.md#catalog-page-object-in-the-index) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="b1153-141">Dla każdej pozostałej strony katalogu pobierz `@id` pełny dokument przy użyciu właściwości.</span><span class="sxs-lookup"><span data-stu-id="b1153-141">For each remaining catalog page, download the full document using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/page2926.json

<span data-ttu-id="b1153-142">Deserializacji [strony katalogu](../../api/catalog-resource.md#catalog-page).</span><span class="sxs-lookup"><span data-stu-id="b1153-142">Deserialize the [catalog page](../../api/catalog-resource.md#catalog-page).</span></span> <span data-ttu-id="b1153-143">Odfiltruj wszystkie `commitTimeStamp` [obiekty liścia katalogu](../../api/catalog-resource.md#catalog-item-object-in-a-page) z mniejszą lub równą bieżącej wartości kursora.</span><span class="sxs-lookup"><span data-stu-id="b1153-143">Filter out all [catalog leaf objects](../../api/catalog-resource.md#catalog-item-object-in-a-page) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="b1153-144">Po pobraniu wszystkich stron katalogu, które nie zostały odfiltrowane, masz zestaw obiektów liścia katalogu reprezentujących pakiety, które zostały opublikowane, niepubliczne, wymienione lub usunięte w czasie między sygnaturą czasową kursora a teraz.</span><span class="sxs-lookup"><span data-stu-id="b1153-144">After you have downloaded all of the catalog pages not filtered out, you have a set of catalog leaf objects representing packages that have been published, unlisted, listed, or deleted in the time between your cursor timestamp and now.</span></span>

## <a name="process-catalog-leaves"></a><span data-ttu-id="b1153-145">Liście katalogu przetwarzania</span><span class="sxs-lookup"><span data-stu-id="b1153-145">Process catalog leaves</span></span>

<span data-ttu-id="b1153-146">W tym momencie można wykonać dowolne niestandardowe przetwarzanie, które chcesz na elementach katalogu.</span><span class="sxs-lookup"><span data-stu-id="b1153-146">At this point, you can perform any custom processing you'd like on the catalog items.</span></span> <span data-ttu-id="b1153-147">Jeśli potrzebujesz tylko identyfikatora i wersji pakietu, można `nuget:id` sprawdzić `nuget:version` właściwości i właściwości na obiektach elementu katalogu znajdujących się na stronach.</span><span class="sxs-lookup"><span data-stu-id="b1153-147">If all you need is the ID and version of the package, you can inspect the `nuget:id` and `nuget:version` properties on the catalog item objects found in the pages.</span></span> <span data-ttu-id="b1153-148">Upewnij się, aby `@type` spojrzeć na właściwość, aby dowiedzieć się, czy element katalogu dotyczy istniejącego pakietu lub usuniętego pakietu.</span><span class="sxs-lookup"><span data-stu-id="b1153-148">Make sure to look at the `@type` property to know if the catalog item concerns an existing package or a deleted package.</span></span>

<span data-ttu-id="b1153-149">Jeśli jesteś zainteresowany metadanych o pakiecie (takich w opisie, zależności, .nupkg rozmiar, itp.), `@id` można pobrać [dokument liścia katalogu](../../api/catalog-resource.md#catalog-leaf) przy użyciu właściwości.</span><span class="sxs-lookup"><span data-stu-id="b1153-149">If you are interested in the metadata about the package (such at the description, dependencies, .nupkg size, etc), you can fetch the [catalog leaf document](../../api/catalog-resource.md#catalog-leaf) using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

<span data-ttu-id="b1153-150">Ten dokument zawiera wszystkie metadane zawarte w [zasobie metadanych pakietu](../../api/registration-base-url-resource.md)i nie tylko!</span><span class="sxs-lookup"><span data-stu-id="b1153-150">This document has all of the metadata included in the [package metadata resource](../../api/registration-base-url-resource.md), and more!</span></span>

<span data-ttu-id="b1153-151">Ten krok jest, gdzie można zaimplementować logikę niestandardową.</span><span class="sxs-lookup"><span data-stu-id="b1153-151">This step is where you implement your custom logic.</span></span> <span data-ttu-id="b1153-152">Inne kroki w tym przewodniku są realizowane w prawie taki sam sposób, nie ma znaczenia, co robisz z liści katalogu.</span><span class="sxs-lookup"><span data-stu-id="b1153-152">The other steps in this guide are implemented in pretty much the same way not matter what you are doing with the catalog leaves.</span></span>

### <a name="downloading-the-nupkg"></a><span data-ttu-id="b1153-153">Pobieranie pliku .nupkg</span><span class="sxs-lookup"><span data-stu-id="b1153-153">Downloading the .nupkg</span></span>

<span data-ttu-id="b1153-154">Jeśli chcesz pobrać pakiety .nupkg znajdujące się w katalogu, możesz użyć [zasobu zawartości pakietu](../../api/package-base-address-resource.md).</span><span class="sxs-lookup"><span data-stu-id="b1153-154">If you are interested in downloading the .nupkg's for packages found in the catalog, you can use the [package content resource](../../api/package-base-address-resource.md).</span></span> <span data-ttu-id="b1153-155">Należy jednak pamiętać, że istnieje krótkie opóźnienie między, gdy pakiet znajduje się w katalogu i gdy jest on dostępny w zasobie zawartości pakietu.</span><span class="sxs-lookup"><span data-stu-id="b1153-155">However, note that there is a short delay between when a package is found in catalog and when it's available in the package content resource.</span></span> <span data-ttu-id="b1153-156">W związku z `404 Not Found` tym jeśli wystąpi podczas próby pobrania .nupkg dla pakietu, który został znaleziony w katalogu, po prostu ponów próbę chwilę później.</span><span class="sxs-lookup"><span data-stu-id="b1153-156">Therefore, if you encounter `404 Not Found` when attempting to download a .nupkg for a package that you found in the catalog, simply retry a short time later.</span></span> <span data-ttu-id="b1153-157">Naprawienie tego opóźnienia jest śledzone przez gitHub problem [NuGet/NuGetGallery #3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span><span class="sxs-lookup"><span data-stu-id="b1153-157">Fixing this delay is tracked by GitHub issue [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span></span>

## <a name="move-the-cursor-forward"></a><span data-ttu-id="b1153-158">Przesuwanie kursora do przodu</span><span class="sxs-lookup"><span data-stu-id="b1153-158">Move the cursor forward</span></span>

<span data-ttu-id="b1153-159">Po pomyślnym przetworzeniu elementów katalogu należy określić nową wartość kursora do zapisania.</span><span class="sxs-lookup"><span data-stu-id="b1153-159">Once you have successfully processed the catalog items, you need to determine the new cursor value to save.</span></span> <span data-ttu-id="b1153-160">Aby to zrobić, znajdź maksymalną (najnowszą chronologicznie) `commitTimeStamp` wszystkich przetworzonych elementów katalogu.</span><span class="sxs-lookup"><span data-stu-id="b1153-160">To do this, find the maximum (latest chronologically) `commitTimeStamp` of all catalog items that you processed.</span></span> <span data-ttu-id="b1153-161">Jest to nowa wartość kursora.</span><span class="sxs-lookup"><span data-stu-id="b1153-161">This is your new cursor value.</span></span> <span data-ttu-id="b1153-162">Zapisz go w niektórych trwałych magazynów, takich jak baza danych, system plików lub magazyn obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="b1153-162">Save it to some persistent store, like a database, file system, or blob storage.</span></span> <span data-ttu-id="b1153-163">Jeśli chcesz uzyskać więcej elementów katalogu, po prostu zacznij od [pierwszego kroku,](#initialize-a-cursor) inicjując wartość kursora z tego magazynu trwałego.</span><span class="sxs-lookup"><span data-stu-id="b1153-163">When you want to get more catalog items, simply start from the [first step](#initialize-a-cursor) by initializing your cursor value from this persistent store.</span></span>

<span data-ttu-id="b1153-164">Jeśli aplikacja zgłasza wyjątek lub błędy, nie należy przenosić kursora do przodu.</span><span class="sxs-lookup"><span data-stu-id="b1153-164">If your application throws an exception or faults, don't move the cursor forward.</span></span> <span data-ttu-id="b1153-165">Przesunięcie kursora do przodu ma znaczenie, że nigdy więcej nie trzeba przetwarzać elementów katalogu przed kursorem.</span><span class="sxs-lookup"><span data-stu-id="b1153-165">Moving the cursor forward has the meaning that you never again need to process catalog items before your cursor.</span></span>

<span data-ttu-id="b1153-166">Jeśli z jakiegoś powodu masz błąd w sposobie przetwarzania liści katalogu, możesz po prostu przesunąć kursor do tyłu w czasie i zezwolić na ponowne przetworzenie kodu starych elementów katalogu.</span><span class="sxs-lookup"><span data-stu-id="b1153-166">If, for some reason, you have a bug in how you process catalog leaves, you can simply move your cursor backward in time and allow your code to reprocess the old catalog items.</span></span>

## <a name="c-sample-code"></a><span data-ttu-id="b1153-167">Przykładowy kod języka C#</span><span class="sxs-lookup"><span data-stu-id="b1153-167">C# sample code</span></span>

<span data-ttu-id="b1153-168">Ponieważ katalog jest zestawem dokumentów JSON dostępnych za pośrednictwem protokołu HTTP, można go wchodzić w interakcje z przy użyciu dowolnego języka programowania, który ma klienta HTTP i deserializatorA JSON.</span><span class="sxs-lookup"><span data-stu-id="b1153-168">Because the catalog is a set of JSON documents available over HTTP, it can be interacted with using any programming language that has an HTTP client and JSON deserializer.</span></span>

<span data-ttu-id="b1153-169">Próbki języka C# są dostępne w [repozytorium NuGet/Samples](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="b1153-169">C# samples are available in the [NuGet/Samples repository](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span></span>

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a><span data-ttu-id="b1153-170">Katalog SDK</span><span class="sxs-lookup"><span data-stu-id="b1153-170">Catalog SDK</span></span>

<span data-ttu-id="b1153-171">Najprostszym sposobem wykorzystania katalogu jest użycie pakietu zestawu SDK katalogu .NET w wersji wstępnej: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span><span class="sxs-lookup"><span data-stu-id="b1153-171">The easiest way to consume the catalog is to use the pre-release .NET catalog SDK package: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span></span> <span data-ttu-id="b1153-172">Ten pakiet jest `nuget-build` dostępny w kanale MyGet, dla którego `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`używasz adresu URL źródła pakietu NuGet .</span><span class="sxs-lookup"><span data-stu-id="b1153-172">This package is available on the `nuget-build` MyGet feed, for which you use the NuGet package source URL `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span></span>

<span data-ttu-id="b1153-173">Ten pakiet można zainstalować w `netstandard1.3` projekcie zgodnym z projektem lub większym (takim jak .NET Framework 4.6).</span><span class="sxs-lookup"><span data-stu-id="b1153-173">You can install this package to a project compatible with `netstandard1.3` or greater (such as .NET Framework 4.6).</span></span>

<span data-ttu-id="b1153-174">Przykład przy użyciu tego pakietu jest dostępny w usłudze GitHub w [projekcie NuGet.Protocol.Catalog.Sample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span><span class="sxs-lookup"><span data-stu-id="b1153-174">A sample using this package is available on GitHub in the [NuGet.Protocol.Catalog.Sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="b1153-175">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="b1153-175">Sample output</span></span>

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

### <a name="minimal-sample"></a><span data-ttu-id="b1153-176">Minimalna próbka</span><span class="sxs-lookup"><span data-stu-id="b1153-176">Minimal sample</span></span>

<span data-ttu-id="b1153-177">Na przykład z mniejszą liczbą zależności, która ilustruje interakcję z katalogiem bardziej szczegółowo, zobacz [CatalogReaderExample przykładowego projektu](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="b1153-177">For an example with fewer dependencies that illustrates the interaction with the catalog in more detail, see the [CatalogReaderExample sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span></span> <span data-ttu-id="b1153-178">Projekt jest `netcoreapp2.0` przeznaczony i zależy od [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (do rozpoznawania indeksu usługi) i [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (dla deserializacji JSON).</span><span class="sxs-lookup"><span data-stu-id="b1153-178">The project targets `netcoreapp2.0` and depends on the [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (for resolving the service index) and [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (for JSON deserialization).</span></span>

<span data-ttu-id="b1153-179">Główna logika kodu jest widoczna w [pliku Program.cs](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="b1153-179">The main logic of the code is visible in the [Program.cs file](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="b1153-180">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="b1153-180">Sample output</span></span>

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
