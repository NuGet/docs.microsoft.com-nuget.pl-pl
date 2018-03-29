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
# <a name="query-for-all-packages-published-to-nugetorg"></a>Zapytania dla wszystkich pakietów opublikowane nuget.org

Jeden wspólnego wzorca zapytania na starszego interfejsu API 2 OData został wyliczania wszystkie pakiety opublikowane nuget.org, uporządkowanych według Jeśli pakiet został opublikowany. Scenariusze wymagające tego rodzaju zapytania dotyczącego nuget.org różnią się znacznie:

- Replikowanie całkowicie nuget.org
- Wykrywanie, gdy pakiety zawierają nowe wersje wydane
- Znajdowanie pakiety, które są zależne od pakietu

Starsze sposobów to zwykle była uzależniona od sortowania jednostką OData pakietu przez sygnaturę czasową i stronicowania na ogromną wynik ustawić za pomocą `skip` i `top` parametrów (rozmiar strony). Niestety ta metoda ma kilka wad:

- Możliwość brakujących pakietów, ponieważ zapytania są określane na dane, które często jest zmiana kolejności
- Powolna czas odpowiedzi na zapytanie, ponieważ nie są zoptymalizowane (najbardziej zoptymalizowane zapytania są scenariusza połączeniach klienta NuGet oficjalny)
- Użyj interfejsu API przestarzałe i nieudokumentowanej, co oznacza obsługę tych zapytań w przyszłości nie jest gwarantowana.
- Brak możliwości powtarzania historii dokładnie w takiej kolejności, która okazało się

Z tego powodu następującymi wskazówkami można wykonać w celu rozwiązania scenariuszy wyżej wymienione w sposób bardziej niezawodne i zabezpieczenie przyszłych potrzeb.

## <a name="overview"></a>Omówienie

W Centrum w tym przewodniku jest zasobem w [NuGet API](../../api/overview.md) o nazwie **katalogu**. Katalog jest tylko do dołączania interfejsu API, który umożliwia obiekt wywołujący, aby wyświetlić pełną historię pakietów dodawać, modyfikować i usunięty z nuget.org. Jeśli interesuje Cię wszystkich lub nawet podzbiór pakietów opublikowane nuget.org, katalog jest to dobry sposób na bieżąco z zestawem pakiety aktualnie dostępne w.

Ten przewodnik jest przeznaczony ogólnym opisem, ale jeśli planuje się szczegóły szczegółowe dzielenie katalogu, zobacz jego [dokumentu odwołania API](../../api/catalog-resource.md).

Poniższe kroki można zaimplementować w dowolnym języku programowania wybranych przez użytkownika. Jeśli chcesz pełny przykład uruchomione, Przyjrzyjmy się [próbki C#](#c-sample-code) wymienione poniżej.

W przeciwnym razie wykonaj przewodnik poniżej do utworzenia czytnika niezawodnej katalogu.

## <a name="initialize-a-cursor"></a>Inicjowanie kursora

Pierwszym krokiem podczas tworzenia czytnika niezawodnej katalogu implementuje kursora. Aby uzyskać szczegółowe informacje dotyczące projektowania kursora katalogu, zobacz [katalogu odwołania dokumentu](../../api/catalog-resource.md#cursor). Krótko mówiąc kursor jest punkt w czasie, do której zostały przetworzone zdarzenia w katalogu. Zdarzenia w katalogu pakietu reprezentują publikuje i zmienia inny pakiet. Jeśli interesują wszystkie pakiety kiedykolwiek opublikowane NuGet (od początku czasu), może ustawić kursor do sygnatury czasowej "minimalna wartość" (np. `DateTime.MinValue` w .NET). Jeśli Cię interesuje tylko pakiety opublikowane już teraz, można użyć jako wartość początkowego kursora bieżącą sygnaturę czasową.

Tego przewodnika firma Microsoft będzie zainicjować naszych kursora prowadzącego do sygnatury czasowej godzinę temu. Teraz Zapisz ten znacznik w pamięci.

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a>Określić adres URL katalogu indeksu

Lokalizację każdego zasobu (punkt końcowy) w interfejsie API NuGet powinny zostać wykryte przy użyciu [indeksu usługi](../../api/service-index.md). Ponieważ ten przewodnik koncentruje się na nuget.org, będziemy używać indeksu usługi nuget.org.

    GET https://api.nuget.org/v3/index.json

Dokument usługi jest zawierająca wszystkie zasoby na nuget.org dokumentu JSON. Wyszukaj o zasobów `@type` wartość właściwości `Catalog/3.0.0`. Skojarzony `@id` wartość właściwości jest adres URL, który sam indeks katalogu. 

## <a name="find-new-catalog-leaves"></a>Znajdowanie nowych pozostawia katalogu

Przy użyciu `@id` indeks katalogu pobierania wartości właściwości w poprzednim kroku:

    GET https://api.nuget.org/v3/catalog0/index.json

Deserializacja [indeks katalogu](../../api/catalog-resource.md#catalog-index). Wszystkie odfiltrowane [katalogowania obiektów strony](../../api/catalog-resource.md#catalog-page-object-in-the-index) z `commitTimeStamp` mniejsza niż bieżąca wartość kursora.

W przypadku pozostałych stron katalogu, Pobierz przy użyciu pełnego dokumentu `@id` właściwości.

    GET https://api.nuget.org/v3/catalog0/page2926.json

Deserializacja [strona katalogu](../../api/catalog-resource.md#catalog-page). Wszystkie odfiltrowane [katalogowania obiektów typu liść](../../api/catalog-resource.md#catalog-item-object-in-a-page) z `commitTimeStamp` mniejsza niż bieżąca wartość kursora.

Po pobraniu wszystkich stron katalogu nie odfiltrowany istnieje zestaw obiektów typu liść katalogu reprezentujących pakiety, które zostały opublikowane, nieznajdujące się na liście, listy lub usunięte w okresie między sygnatury czasowej użytkownika kursora, a teraz.

## <a name="process-catalog-leaves"></a>Pozostawia katalogu procesu

W tym momencie można wykonywać żadnych niestandardowych przetwarzania, które mają na elementów katalogu. Jeśli wszystko, czego potrzebujesz Identyfikatora i wersję pakietu, możesz sprawdzić `nuget:id` i `nuget:version` znalezionych na stronach elementu właściwości w katalogu. Upewnij się, że przyjrzeć się `@type` właściwości, aby dowiedzieć się, jeśli element katalogu dotyczy istniejącego pakietu lub usuniętych pakietów.

Jeśli interesuje Cię w metadanych o pakiecie (na przykład opis, zależności, rozmiar .nupkg, itp.), można pobrać [dokumentu liścia katalogu](../../api/catalog-resource.md#catalog-leaf) przy użyciu `@id` właściwości.

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

Ten dokument zawiera wszystkie zawarte w metadanych [pakietu zasobów metadanych](../../api/registration-base-url-resource.md)i nie tylko!

Ten krok polega na tym, gdzie wdrożyć niestandardowej logiki. Pozostałe kroki w tym przewodniku są implementowane w pretty znacznie taki sam sposób niezależnie od tego, czynności z liśćmi katalogu.

### <a name="downloading-the-nupkg"></a>Pobieranie .nupkg

Jeśli interesuje Cię w czasie pobierania pakietów .nupkg odnaleziono w katalogu, można użyć [pakietu zawartości zasobów](../../api/package-base-address-resource.md). Jednak należy pamiętać, że krótkie opóźnienie podczas pakietu znajduje się w katalogu i gdy jest dostępny w zasobie zawartości pakietu. W związku z tym jeśli wystąpią `404 Not Found` podczas próby pobrania .nupkg dla pakietu, który można znaleźć w katalogu, po prostu ponownie przez krótki czas później. Ustalenie to opóźnienie jest śledzony przez problem GitHub [&#3455; NuGet/NuGetGallery](https://github.com/NuGet/NuGetGallery/issues/3455).

## <a name="move-the-cursor-forward"></a>Przeniesienie kursora do przodu

Po pomyślnie zostały przetworzone elementy katalogu, należy określić nową wartość kursora do zapisania. W tym celu Znajdź maksymalną (najnowsze porządku chronologicznym) `commitTimeStamp` wszystkich elementów katalogu, które zostanie przetworzone. Jest to z nową wartością kursora. Zapisz go w niektórych magazynu trwałego, takich jak bazy danych, system plików lub magazynu obiektów blob. Aby uzyskać więcej elementów katalogu, należy po prostu Rozpocznij od [pierwszy krok](#initialize-a-cursor) przez inicjowanie wartość kursora z tego magazynu trwałego.

Jeśli aplikacja zgłasza wyjątek lub błędy, nie przenoś kursora do przodu. Przesuń kursor do przodu ma znaczenie, nigdy nie ponownie potrzebne do przetwarzania elementów katalogu przed kursor.

Jeśli z jakiegoś powodu masz pozostawia na usterkę w sposób przetwarzania katalogu, możesz po prostu przesuń wskaźnik do tyłu w czasie i kodu tak ponownie przetworzyć starych elementów katalogu.

## <a name="c-sample-code"></a>Przykładowy kod C#

Ponieważ katalog jest zestawem dokumentów JSON, które są dostępne za pośrednictwem protokołu HTTP, może być interakcji z przy użyciu dowolnego języka programowania, klient HTTP i deserializacji JSON.

Przykłady dotyczące języka C# są dostępne w [repozytorium NuGet/przykłady](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a>W katalogu zestawu SDK

Najprostszym sposobem korzystania z katalogu jest użycie pakietu SDK katalogu .NET wersji wstępnej: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog). Ten pakiet jest dostępny na `nuget-build` MyGet źródła danych, dla którego używają adres URL źródła pakietu NuGet `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.

Ten pakiet można zainstalować na projekt niezgodny z `netstandard1.3` lub nowszej (na przykład .NET Framework 4.6).

Przykład za pomocą tego pakietu jest dostępna w witrynie GitHub w [projektu NuGet.Protocol.Catalog.Sample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).

#### <a name="sample-output"></a>Przykładowe dane wyjściowe

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

### <a name="minimal-sample"></a>Minimalny próbki

Na przykład z zależnościami mniej ilustrujący interakcji z katalogu bardziej szczegółowo w temacie [CatalogReaderExample przykładowy projekt](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample). Obiekty docelowe projektu `netcoreapp2.0` i zależy od [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (na potrzeby rozpoznawania indeksu service) i [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (w przypadku deserializacji JSON).

Logiki główny kodu jest widoczny w [pliku Program.cs](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).

#### <a name="sample-output"></a>Przykładowe dane wyjściowe

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
