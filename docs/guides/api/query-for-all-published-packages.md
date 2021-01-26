---
title: Zapytanie dotyczące wszystkich pakietów opublikowanych w usłudze nuget.org
description: Za pomocą interfejsu API NuGet można wysyłać zapytania dotyczące wszystkich pakietów opublikowanych w nuget.org i zachować aktualność w miarę upływu czasu.
author: joelverhagen
ms.author: jver
ms.date: 11/02/2017
ms.topic: tutorial
ms.reviewer: kraigb
ms.openlocfilehash: 7e611b568538e0acfcbad2e5d986a0f9382ac8fd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774113"
---
# <a name="query-for-all-packages-published-to-nugetorg"></a><span data-ttu-id="bbbc3-103">Zapytanie dotyczące wszystkich pakietów opublikowanych w usłudze nuget.org</span><span class="sxs-lookup"><span data-stu-id="bbbc3-103">Query for all packages published to nuget.org</span></span>

<span data-ttu-id="bbbc3-104">Jeden wspólny wzorzec zapytania w starszym interfejsie API OData v2 wylicza wszystkie pakiety opublikowane w nuget.org, uporządkowane według czasu opublikowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-104">One common query pattern on the legacy OData V2 API was enumerating all packages published to nuget.org, ordered by when the package was published.</span></span> <span data-ttu-id="bbbc3-105">Scenariusze wymagające tego rodzaju zapytania dotyczące nuget.org są szeroko rozliczane:</span><span class="sxs-lookup"><span data-stu-id="bbbc3-105">Scenarios requiring this kind of query against nuget.org vary widely:</span></span>

- <span data-ttu-id="bbbc3-106">Całkowicie replikowanie nuget.org</span><span class="sxs-lookup"><span data-stu-id="bbbc3-106">Replicating nuget.org entirely</span></span>
- <span data-ttu-id="bbbc3-107">Wykrywanie, kiedy pakiety mają nowe wersje wydane</span><span class="sxs-lookup"><span data-stu-id="bbbc3-107">Detecting when packages have new versions released</span></span>
- <span data-ttu-id="bbbc3-108">Znajdowanie pakietów, które są zależne od pakietu</span><span class="sxs-lookup"><span data-stu-id="bbbc3-108">Finding packages that depend on your package</span></span>

<span data-ttu-id="bbbc3-109">Starsza Metoda przeprowadzenia tej operacji zwykle zależy od sortowania jednostki pakietu OData przez sygnaturę czasową i stronicowanie w ramach ogromnego zestawu wyników przy użyciu `skip` `top` parametrów i (rozmiaru strony).</span><span class="sxs-lookup"><span data-stu-id="bbbc3-109">The legacy way of doing this typically depended on sorting the OData package entity by a timestamp and paging across the massive result set using `skip` and `top` (page size) parameters.</span></span> <span data-ttu-id="bbbc3-110">Niestety, takie podejście ma pewne wady:</span><span class="sxs-lookup"><span data-stu-id="bbbc3-110">Unfortunately, this approach has some drawbacks:</span></span>

- <span data-ttu-id="bbbc3-111">Możliwość braku pakietów, ponieważ są wykonywane zapytania dotyczące danych, które często zmieniają kolejność</span><span class="sxs-lookup"><span data-stu-id="bbbc3-111">Possibility of missing packages, because the queries are being made on data that is often changing order</span></span>
- <span data-ttu-id="bbbc3-112">Długi czas odpowiedzi na zapytanie, ponieważ zapytania nie są zoptymalizowane (najbardziej zoptymalizowane zapytania to te, które obsługują scenariusz linii głównej dla oficjalnego klienta NuGet)</span><span class="sxs-lookup"><span data-stu-id="bbbc3-112">Slow query response time, because the queries are not optimized (the most optimized queries are ones that support a mainline scenario for the official NuGet client)</span></span>
- <span data-ttu-id="bbbc3-113">Użycie przestarzałego i nieudokumentowanego interfejsu API, co oznacza, że obsługa takich zapytań nie jest gwarantowana</span><span class="sxs-lookup"><span data-stu-id="bbbc3-113">Use of deprecated and undocumented API, meaning the support of such queries in the future is not guaranteed</span></span>
- <span data-ttu-id="bbbc3-114">Niezdolność do powtarzania historii w dokładnej kolejności, w której transpired</span><span class="sxs-lookup"><span data-stu-id="bbbc3-114">Inability to replay history in the exact order that it transpired</span></span>

<span data-ttu-id="bbbc3-115">Z tego powodu Poniższy przewodnik może posłużyć do rozwiązania powyższych scenariuszy w bardziej niezawodnej i przyszłej próbie.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-115">For this reason, the following guide can be followed to address the aforementioned scenarios in a more reliable and future-proof way.</span></span>

## <a name="overview"></a><span data-ttu-id="bbbc3-116">Omówienie</span><span class="sxs-lookup"><span data-stu-id="bbbc3-116">Overview</span></span>

<span data-ttu-id="bbbc3-117">W centrum tego przewodnika jest zasób w [interfejsie API NuGet](../../api/overview.md) o nazwie **wykaz**.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-117">At the center of this guide is resource in the [NuGet API](../../api/overview.md) called the **catalog**.</span></span> <span data-ttu-id="bbbc3-118">Katalog jest interfejsem API tylko do dołączania, który umożliwia wywołującemu wyświetlanie pełnej historii pakietów dodanych do, zmodyfikowanych i usuniętych z nuget.org. Jeśli interesuje Cię wszystkie lub nawet podzbiór pakietów opublikowanych w usłudze nuget.org, katalog jest doskonałym sposobem na utrzymanie Aktualności z zestawem aktualnie dostępnych pakietów jako czas, w którym się znajdują.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-118">The catalog is an append-only API that allows the caller to see a full history of packages added to, modified, and deleted from nuget.org. If you are interested in all or even a subset of packages published to nuget.org, the catalog is a great way to stay up-to-date with the set of currently available packages as time goes on.</span></span>

<span data-ttu-id="bbbc3-119">Ten przewodnik jest przeznaczony do ogólnego przechodzenia, ale jeśli interesuje Cię szczegółowe informacje o wykazie, zobacz jego [dokument referencyjny interfejsu API](../../api/catalog-resource.md).</span><span class="sxs-lookup"><span data-stu-id="bbbc3-119">This guide is intended to be a high-level walk-through but if you are interested in the fine-grain details of the catalog, see its [API reference document](../../api/catalog-resource.md).</span></span>

<span data-ttu-id="bbbc3-120">Poniższe kroki można zaimplementować w dowolnym wybranym języku programowania.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-120">The following steps can be implemented in any programming language of your choice.</span></span> <span data-ttu-id="bbbc3-121">Jeśli chcesz wykonać pełny przykład, zapoznaj się z [przykładem w języku C#](#c-sample-code) opisanym poniżej.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-121">If you want a full running sample, take a look at the [C# sample](#c-sample-code) mentioned below.</span></span>

<span data-ttu-id="bbbc3-122">W przeciwnym razie postępuj zgodnie z poniższym przewodnikiem, aby utworzyć niezawodny czytnik wykazu.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-122">Otherwise, follow the guide below to build a reliable catalog reader.</span></span>

## <a name="initialize-a-cursor"></a><span data-ttu-id="bbbc3-123">Inicjowanie kursora</span><span class="sxs-lookup"><span data-stu-id="bbbc3-123">Initialize a cursor</span></span>

<span data-ttu-id="bbbc3-124">Pierwszym krokiem tworzenia niezawodnego czytnika wykazu jest implementacja kursora.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-124">The first step in building a reliable catalog reader is implementing a cursor.</span></span> <span data-ttu-id="bbbc3-125">Aby uzyskać szczegółowe informacje na temat projektu kursora katalogu, zobacz [dokument odwołania do katalogu](../../api/catalog-resource.md#cursor).</span><span class="sxs-lookup"><span data-stu-id="bbbc3-125">For full details about the design of a catalog cursor, see the [catalog reference document](../../api/catalog-resource.md#cursor).</span></span> <span data-ttu-id="bbbc3-126">W skrócie kursor jest punktem w czasie, w którym przetworzono zdarzenia w wykazie.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-126">In short, cursor is a point in time up to which you have processed events in the catalog.</span></span> <span data-ttu-id="bbbc3-127">Zdarzenia w wykazie reprezentują publikowanie pakietów i inne zmiany pakietu.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-127">Events in the catalog represent package publishes and other package changes.</span></span> <span data-ttu-id="bbbc3-128">Jeśli postanowisz o wszystkich pakietach opublikowanych w pakiecie NuGet (od momentu rozpoczęcia), możesz zainicjować kursor do sygnatury czasowej "wartość minimalna" (np. `DateTime.MinValue` w programie .NET).</span><span class="sxs-lookup"><span data-stu-id="bbbc3-128">If you care about all packages ever published to NuGet (since the beginning of time), you would initialize your cursor to a "minimum value" timestamp (e.g. `DateTime.MinValue` in .NET).</span></span> <span data-ttu-id="bbbc3-129">Jeśli masz szczególną uwagę na to, że na bieżąco z opublikowanymi pakietami, Użyj bieżącej sygnatury czasowej jako początkowej wartości kursora.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-129">If you care only about packages published starting now, you would use the current timestamp as your initial cursor value.</span></span>

<span data-ttu-id="bbbc3-130">W tym przewodniku zainicjujemy nasz kursor do sygnatury czasowej o godzinę temu.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-130">For this guide, we'll initialize our cursor to a timestamp one hour ago.</span></span> <span data-ttu-id="bbbc3-131">Na razie po prostu Zapisz tę sygnaturę czasową w pamięci.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-131">For now, just save that timestamp in memory.</span></span>

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a><span data-ttu-id="bbbc3-132">Określ adres URL indeksu katalogu</span><span class="sxs-lookup"><span data-stu-id="bbbc3-132">Determine catalog index URL</span></span>

<span data-ttu-id="bbbc3-133">Lokalizację każdego zasobu (punkt końcowy) w interfejsie API NuGet należy odnaleźć przy użyciu [indeksu usługi](../../api/service-index.md).</span><span class="sxs-lookup"><span data-stu-id="bbbc3-133">The location of every resource (endpoint) in the NuGet API should be discovered using the [service index](../../api/service-index.md).</span></span> <span data-ttu-id="bbbc3-134">Ponieważ ten przewodnik koncentruje się na nuget.org, będziemy używać narzędzia NuGet. indeks usługi w organizacji.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-134">Because this guide focuses on nuget.org, we'll be using nuget.org's service index.</span></span>

```
GET https://api.nuget.org/v3/index.json
```

<span data-ttu-id="bbbc3-135">Dokument usługi jest dokumentem JSON zawierającym wszystkie zasoby w nuget.org. Poszukaj zasobu mającego `@type` wartość właściwości `Catalog/3.0.0` .</span><span class="sxs-lookup"><span data-stu-id="bbbc3-135">The service document is JSON document containing all of the resources on nuget.org. Look for the resource having the `@type` property value of `Catalog/3.0.0`.</span></span> <span data-ttu-id="bbbc3-136">Skojarzona `@id` wartość właściwości jest adresem URL samego indeksu katalogu.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-136">The associated `@id` property value is the URL to the catalog index itself.</span></span> 

## <a name="find-new-catalog-leaves"></a><span data-ttu-id="bbbc3-137">Znajdź nowy wykaz liści</span><span class="sxs-lookup"><span data-stu-id="bbbc3-137">Find new catalog leaves</span></span>

<span data-ttu-id="bbbc3-138">Korzystając z `@id` wartości właściwości znalezionej w poprzednim kroku, Pobierz indeks wykazu:</span><span class="sxs-lookup"><span data-stu-id="bbbc3-138">Using the `@id` property value found in the previous step, download the catalog index:</span></span>

```
GET https://api.nuget.org/v3/catalog0/index.json
```

<span data-ttu-id="bbbc3-139">Deserializacja [indeksu katalogu](../../api/catalog-resource.md#catalog-index).</span><span class="sxs-lookup"><span data-stu-id="bbbc3-139">Deserialize the [catalog index](../../api/catalog-resource.md#catalog-index).</span></span> <span data-ttu-id="bbbc3-140">Odfiltruj wszystkie [obiekty strony katalogu](../../api/catalog-resource.md#catalog-page-object-in-the-index) `commitTimeStamp` , których wartość jest mniejsza lub równa bieżącej wartości kursora.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-140">Filter out all [catalog page objects](../../api/catalog-resource.md#catalog-page-object-in-the-index) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="bbbc3-141">Dla każdej pozostałej strony wykazu Pobierz pełny dokument przy użyciu `@id` właściwości.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-141">For each remaining catalog page, download the full document using the `@id` property.</span></span>

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

<span data-ttu-id="bbbc3-142">Deserializacja [strony katalogu](../../api/catalog-resource.md#catalog-page).</span><span class="sxs-lookup"><span data-stu-id="bbbc3-142">Deserialize the [catalog page](../../api/catalog-resource.md#catalog-page).</span></span> <span data-ttu-id="bbbc3-143">Odfiltruj wszystkie [obiekty liści wykazu](../../api/catalog-resource.md#catalog-item-object-in-a-page) z `commitTimeStamp` mniejszą lub równą bieżącej wartości kursora.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-143">Filter out all [catalog leaf objects](../../api/catalog-resource.md#catalog-item-object-in-a-page) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="bbbc3-144">Po pobraniu wszystkich stron wykazu, które nie zostały odfiltrowane, istnieje zestaw obiektów liści wykazu reprezentujących pakiety, które zostały opublikowane, niewymienione na liście lub usunięte w czasie między znacznikiem czasu kursora a teraz.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-144">After you have downloaded all of the catalog pages not filtered out, you have a set of catalog leaf objects representing packages that have been published, unlisted, listed, or deleted in the time between your cursor timestamp and now.</span></span>

## <a name="process-catalog-leaves"></a><span data-ttu-id="bbbc3-145">Urlopy katalogu procesów</span><span class="sxs-lookup"><span data-stu-id="bbbc3-145">Process catalog leaves</span></span>

<span data-ttu-id="bbbc3-146">W tym momencie można wykonać dowolne niestandardowe przetwarzanie dla elementów katalogu.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-146">At this point, you can perform any custom processing you'd like on the catalog items.</span></span> <span data-ttu-id="bbbc3-147">Jeśli wszystko, co jest potrzebne, to identyfikator i wersja pakietu, można sprawdzić `nuget:id` `nuget:version` właściwości i w obiektach elementów wykazu znalezionych na stronach.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-147">If all you need is the ID and version of the package, you can inspect the `nuget:id` and `nuget:version` properties on the catalog item objects found in the pages.</span></span> <span data-ttu-id="bbbc3-148">Zwróć uwagę na `@type` Właściwość, aby dowiedzieć się, czy element katalogu dotyczy istniejącego pakietu lub usuniętego pakietu.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-148">Make sure to look at the `@type` property to know if the catalog item concerns an existing package or a deleted package.</span></span>

<span data-ttu-id="bbbc3-149">Jeśli interesują Cię metadane dotyczące pakietu (na przykład opis, zależności, rozmiar NUPKG itp.), możesz pobrać [dokument liścia katalogu](../../api/catalog-resource.md#catalog-leaf) przy użyciu `@id` właściwości.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-149">If you are interested in the metadata about the package (such at the description, dependencies, .nupkg size, etc), you can fetch the [catalog leaf document](../../api/catalog-resource.md#catalog-leaf) using the `@id` property.</span></span>

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

<span data-ttu-id="bbbc3-150">Ten dokument zawiera wszystkie metadane zawarte w [zasobie metadanych pakietu](../../api/registration-base-url-resource.md)i inne.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-150">This document has all of the metadata included in the [package metadata resource](../../api/registration-base-url-resource.md), and more!</span></span>

<span data-ttu-id="bbbc3-151">Ten krok polega na zaimplementowaniu logiki niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-151">This step is where you implement your custom logic.</span></span> <span data-ttu-id="bbbc3-152">Pozostałe kroki przedstawione w tym przewodniku są implementowane w taki sam sposób, jak w przypadku liści wykazu.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-152">The other steps in this guide are implemented in pretty much the same way not matter what you are doing with the catalog leaves.</span></span>

### <a name="downloading-the-nupkg"></a><span data-ttu-id="bbbc3-153">Pobieranie NUPKG</span><span class="sxs-lookup"><span data-stu-id="bbbc3-153">Downloading the .nupkg</span></span>

<span data-ttu-id="bbbc3-154">Jeśli interesuje Cię pobieranie elementu. nupkg dla pakietów znalezionych w katalogu, możesz użyć [zasobu zawartości pakietu](../../api/package-base-address-resource.md).</span><span class="sxs-lookup"><span data-stu-id="bbbc3-154">If you are interested in downloading the .nupkg's for packages found in the catalog, you can use the [package content resource](../../api/package-base-address-resource.md).</span></span> <span data-ttu-id="bbbc3-155">Należy jednak pamiętać, że istnieje krótkie opóźnienie między wykrytym pakietem w katalogu i udostępnieniem go w zasobie zawartości pakietu.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-155">However, note that there is a short delay between when a package is found in catalog and when it's available in the package content resource.</span></span> <span data-ttu-id="bbbc3-156">W związku z tym, jeśli wystąpią `404 Not Found` próby pobrania elementu. nupkg dla pakietu znalezionego w wykazie, po prostu spróbuj ponownie później.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-156">Therefore, if you encounter `404 Not Found` when attempting to download a .nupkg for a package that you found in the catalog, simply retry a short time later.</span></span> <span data-ttu-id="bbbc3-157">Naprawianie tego opóźnienia jest śledzone w usłudze GitHub wydanie [NuGet/NuGetGallery # 3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span><span class="sxs-lookup"><span data-stu-id="bbbc3-157">Fixing this delay is tracked by GitHub issue [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span></span>

## <a name="move-the-cursor-forward"></a><span data-ttu-id="bbbc3-158">Przesuń kursor do przodu</span><span class="sxs-lookup"><span data-stu-id="bbbc3-158">Move the cursor forward</span></span>

<span data-ttu-id="bbbc3-159">Po pomyślnym przetworzeniu elementów katalogu należy określić nową wartość kursora, która ma zostać zapisana.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-159">Once you have successfully processed the catalog items, you need to determine the new cursor value to save.</span></span> <span data-ttu-id="bbbc3-160">Aby to zrobić, Znajdź maksymalną (aktualną) `commitTimeStamp` wszystkie elementy katalogu, które zostały przetworzone.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-160">To do this, find the maximum (latest chronologically) `commitTimeStamp` of all catalog items that you processed.</span></span> <span data-ttu-id="bbbc3-161">To jest nowa wartość kursora.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-161">This is your new cursor value.</span></span> <span data-ttu-id="bbbc3-162">Zapisz ją w magazynie trwałym, takim jak baza danych, system plików lub magazyn obiektów BLOB.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-162">Save it to some persistent store, like a database, file system, or blob storage.</span></span> <span data-ttu-id="bbbc3-163">Aby uzyskać więcej elementów katalogu, wystarczy zacząć od [pierwszego kroku](#initialize-a-cursor) , inicjując wartość kursora z tego magazynu trwałego.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-163">When you want to get more catalog items, simply start from the [first step](#initialize-a-cursor) by initializing your cursor value from this persistent store.</span></span>

<span data-ttu-id="bbbc3-164">Jeśli aplikacja zgłasza wyjątek lub błędy, nie przenoś kursora do przodu.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-164">If your application throws an exception or faults, don't move the cursor forward.</span></span> <span data-ttu-id="bbbc3-165">Przesuwanie kursora do przodu ma znaczenie, że nie trzeba ponownie przetwarzać elementów katalogu przed kursorem.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-165">Moving the cursor forward has the meaning that you never again need to process catalog items before your cursor.</span></span>

<span data-ttu-id="bbbc3-166">Jeśli z jakiegoś powodu jest dostępna usterka w sposobie przetwarzania liści wykazu, można po prostu przesunąć kursor wstecz w czasie i zezwolić kodowi na ponowne przetwarzanie starych elementów katalogu.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-166">If, for some reason, you have a bug in how you process catalog leaves, you can simply move your cursor backward in time and allow your code to reprocess the old catalog items.</span></span>

## <a name="c-sample-code"></a><span data-ttu-id="bbbc3-167">Przykładowy kod w języku C#</span><span class="sxs-lookup"><span data-stu-id="bbbc3-167">C# sample code</span></span>

<span data-ttu-id="bbbc3-168">Ponieważ katalog jest zestawem dokumentów JSON dostępnych za pośrednictwem protokołu HTTP, można z nich korzystać przy użyciu dowolnego języka programowania, który ma klienta HTTP i Deserializator JSON.</span><span class="sxs-lookup"><span data-stu-id="bbbc3-168">Because the catalog is a set of JSON documents available over HTTP, it can be interacted with using any programming language that has an HTTP client and JSON deserializer.</span></span>

<span data-ttu-id="bbbc3-169">Przykłady w języku C# są dostępne w [repozytorium NuGet/Samples](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="bbbc3-169">C# samples are available in the [NuGet/Samples repository](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span></span>

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a><span data-ttu-id="bbbc3-170">Zestaw SDK katalogu</span><span class="sxs-lookup"><span data-stu-id="bbbc3-170">Catalog SDK</span></span>

<span data-ttu-id="bbbc3-171">Najprostszym sposobem korzystania z wykazu jest użycie pakietu SDK katalogu platformy .NET w wersji wstępnej `NuGet.Protocol.Catalog` , który jest dostępny na Azure Artifacts przy użyciu następującego źródłowego adresu URL pakietu NuGet: `https://pkgs.dev.azure.com/dnceng/public/_packaging/nuget-build/nuget/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="bbbc3-171">The easiest way to consume the catalog is to use the pre-release .NET catalog SDK package `NuGet.Protocol.Catalog`, which is available on Azure Artifacts using the following NuGet package source URL: `https://pkgs.dev.azure.com/dnceng/public/_packaging/nuget-build/nuget/v3/index.json`.</span></span>

<span data-ttu-id="bbbc3-172">Ten pakiet można zainstalować w projekcie zgodnym z `netstandard1.3` lub większym (np. .NET Framework 4,6).</span><span class="sxs-lookup"><span data-stu-id="bbbc3-172">You can install this package to a project compatible with `netstandard1.3` or greater (such as .NET Framework 4.6).</span></span>

<span data-ttu-id="bbbc3-173">Przykład korzystania z tego pakietu jest dostępny w witrynie GitHub w [projekcie NuGet. Protocol. Catalog. sample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span><span class="sxs-lookup"><span data-stu-id="bbbc3-173">A sample using this package is available on GitHub in the [NuGet.Protocol.Catalog.Sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="bbbc3-174">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="bbbc3-174">Sample output</span></span>

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

### <a name="minimal-sample"></a><span data-ttu-id="bbbc3-175">Minimalny przykład</span><span class="sxs-lookup"><span data-stu-id="bbbc3-175">Minimal sample</span></span>

<span data-ttu-id="bbbc3-176">Przykład z mniejszą liczbą zależności, która ilustruje interakcję z katalogiem bardziej szczegółowym, można znaleźć w przykładowym [projekcie CatalogReaderExample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="bbbc3-176">For an example with fewer dependencies that illustrates the interaction with the catalog in more detail, see the [CatalogReaderExample sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span></span> <span data-ttu-id="bbbc3-177">Obiekt docelowy projektu `netcoreapp2.0` i zależy od elementu [NuGet. Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (do rozpoznawania indeksu usługi) i [Newtonsoft.Jsna 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (dla deserializacji JSON).</span><span class="sxs-lookup"><span data-stu-id="bbbc3-177">The project targets `netcoreapp2.0` and depends on the [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (for resolving the service index) and [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (for JSON deserialization).</span></span>

<span data-ttu-id="bbbc3-178">Główna logika kodu jest widoczna w [pliku program.cs](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="bbbc3-178">The main logic of the code is visible in the [Program.cs file](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="bbbc3-179">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="bbbc3-179">Sample output</span></span>

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
