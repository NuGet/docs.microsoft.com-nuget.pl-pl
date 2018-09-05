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
# <a name="query-for-all-packages-published-to-nugetorg"></a>Wykonywanie zapytania o wszystkie pakiety opublikowane w witrynie nuget.org

Jeden typowy wzorzec zapytania w starszej wersji interfejsu API OData w wersji 2 została wyliczanie wszystkie pakiety opublikowane w witrynie nuget.org, uporządkowane według, gdy pakiet został opublikowany. Scenariusze wymagające tego rodzaju zapytania względem nuget.org są bardzo zróżnicowane:

- Replikowanie całkowicie nuget.org
- Wykrywanie, gdy nowe wersje wydane pakiety
- Wyszukuje pakietów, które są zależne od pakietu

Starszy sposób zrobić to zwykle zależą sortowanie jednostką pakietu OData przez sygnaturę czasową i stronicowanie w wyniku ogromnej, można ustawić przy użyciu `skip` i `top` parametrów (rozmiar strony). Niestety to podejście ma pewne wady:

- Możliwość brakujących pakietów, ponieważ zapytania są wykonywane na danych, które często jest zmiana kolejności
- Wolne czas odpowiedzi na zapytanie, ponieważ nie są zoptymalizowane (najbardziej zoptymalizowane zapytania są te, które obsługuje scenariusz linii głównej dla oficjalne klienta programu NuGet)
- Korzystanie z interfejsu API przestarzałe i nieudokumentowane, co oznacza obsługę takich zapytań w przyszłości nie ma żadnej gwarancji.
- Brak możliwości odtworzenia historii dokładnie w takiej kolejności, które okazało się

Z tego powodu można wykonać następującymi wskazówkami dla scenariuszy wyżej w sposób bardziej niezawodne i Zadbaj o przyszłość.

## <a name="overview"></a>Omówienie

W środkowej części tego przewodnika jest zasobem w [NuGet API](../../api/overview.md) o nazwie **katalogu**. Katalog jest tylko do dołączania interfejsu API, który umożliwia obiektowi wywołującemu wyświetlić pełną historię pakietów, dodawać, modyfikacji i usunąć z repozytorium nuget.org. Jeśli interesuje Cię w całości lub nawet podzbiór pakiety opublikowane w witrynie nuget.org, katalog jest doskonałym sposobem na bieżąco, korzystając z zestawu dostępnych pakietów w.

Ten przewodnik jest przeznaczony ogólnym opisem, ale jeśli interesują Cię szczegóły dokładną katalogu, zobacz jego [dokument referencyjny dotyczący interfejsu API](../../api/catalog-resource.md).

Następujące kroki można zaimplemetować w taki sposób, w dowolnym języku programowania wybranych przez użytkownika. Jeśli chcesz, aby uzyskać pełną próbkę uruchomione, Przyjrzyj się [przykładowy języka C#](#c-sample-code) wymienione poniżej.

W przeciwnym razie wykonaj przewodnik poniższe tworzenia czytnika niezawodne katalogu.

## <a name="initialize-a-cursor"></a>Inicjowanie kursora

Pierwszym krokiem w tworzeniu czytnik niezawodne katalogu implementuje kursora. Aby uzyskać szczegółowe informacje dotyczące projektowania kursora katalogu, zobacz [dokument referencyjny dotyczący katalogu](../../api/catalog-resource.md#cursor). Krótko mówiąc kursor znajduje się punkt w czasie, do której zostały przetworzone zdarzenia w wykazie. Publikuje zdarzenia w pakiecie reprezentują wykazu, i zmienia się inny pakiet. W przypadku interesujące Cię wszystkie pakiety, które kiedykolwiek publikowane NuGet (od początku czasu), użytkownik może ustawić kursor do sygnatury czasowej "wartość minimalna" (np. `DateTime.MinValue` na platformie .NET). Jeśli interesujące Cię tylko pakiety opublikowane już teraz, należy użyć bieżącą sygnaturę czasową jako wartość początkowego kursora.

W tym przewodniku firma Microsoft będzie zainicjować naszych kursor do sygnatury czasowej godzinę temu. Teraz po prostu zapisz tej sygnatury czasowej w pamięci.

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a>Określenia adresu URL indeksu katalogu

Lokalizację każdego zasobu (punkt końcowy) w interfejsie API NuGet powinny zostać wykryte przy użyciu [indeks usług](../../api/service-index.md). Ponieważ ten przewodnik skupia się w witrynie nuget.org, będziemy używać indeks usług w witrynie nuget.org.

    GET https://api.nuget.org/v3/index.json

Dokument usługi jest dokument JSON zawierający wszystkie zasoby w witrynie nuget.org. Poszukaj zasobów having `@type` wartość właściwości `Catalog/3.0.0`. Skojarzone `@id` wartość właściwości jest adres URL, który indeks katalogu sam. 

## <a name="find-new-catalog-leaves"></a>Znajdź nowe liście katalogu

Za pomocą `@id` wartości właściwości w poprzednim kroku, Pobierz indeks katalogu:

    GET https://api.nuget.org/v3/catalog0/index.json

Deserializacji [indeks katalogu](../../api/catalog-resource.md#catalog-index). Odfiltrować wszystkie [strony obiektów katalogu](../../api/catalog-resource.md#catalog-page-object-in-the-index) z `commitTimeStamp` mniejsza niż bieżąca wartość kursora.

W przypadku pozostałych stron wykazu, Pobierz pełny dokument, za pomocą `@id` właściwości.

    GET https://api.nuget.org/v3/catalog0/page2926.json

Deserializacji [strona katalogu](../../api/catalog-resource.md#catalog-page). Odfiltrować wszystkie [liścia obiektów katalogu](../../api/catalog-resource.md#catalog-item-object-in-a-page) z `commitTimeStamp` mniejsza niż bieżąca wartość kursora.

Po pobraniu wszystkich stron wykazu nie odfiltrowany masz zestaw obiektów typu liść katalogu reprezentujących pakiety, które zostały opublikowane, nieznajdujące się na liście, listy lub usunięte w okresie między Twoja sygnatura czasowa kursora, a teraz.

## <a name="process-catalog-leaves"></a>Pozostawia proces katalogu

W tym momencie można wykonywać niestandardowe przetwarzania, które Twoim zdaniem na elementy katalogu. Jeśli potrzebna jest Identyfikatorem i wersją pakietu, można sprawdzić `nuget:id` i `nuget:version` właściwości w wykazie elementów znalezionych na stronach. Pamiętaj przyjrzeć się `@type` właściwości, aby dowiedzieć się, jeśli element katalogu dotyczy istniejącego pakietu lub usuniętych pakietów.

Jeśli interesuje Cię w metadanych o pakiecie (na przykład na opis, zależności, rozmiar .nupkg, itp.), możesz pobrać [dokumentu liścia katalogu](../../api/catalog-resource.md#catalog-leaf) przy użyciu `@id` właściwości.

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

Ten dokument zawiera wszystkie metadane objęte [zasób metadanych pakietu](../../api/registration-base-url-resource.md)i nie tylko!

Ten krok polega na tym, gdzie wdrożyć logikę niestandardowego. Kroki opisane w tym przewodniku są implementowane w pretty podobnie sposób niezależnie od tego, co robisz z liśćmi katalogu.

### <a name="downloading-the-nupkg"></a>Pobieranie .nupkg

Jeśli interesuje Cię pobierania pakietów .nupkg znalezione w wykazie, można użyć [pakietu zawartości zasobów](../../api/package-base-address-resource.md). Jednak należy pamiętać, że krótkie opóźnienie podczas pakietu znajduje się w katalogu i gdy jest on dostępny w zasób zawartości pakietu. W związku z tym jeśli wystąpią `404 Not Found` podczas próby pobierania .nupkg pakietu w katalogu, po prostu ponownie przez krótki czas później. Naprawianie to opóźnienie jest śledzona przez problem w usłudze GitHub [3455 # NuGet/NuGetGallery](https://github.com/NuGet/NuGetGallery/issues/3455).

## <a name="move-the-cursor-forward"></a>Przenieś kursor do przodu

Po pomyślnym przetworzeniu elementów katalogu należy określić nową wartość kursor do zapisania. W tym celu należy znaleźć maksymalną (najnowsze chronologicznie) `commitTimeStamp` wszystkich elementów katalogu, które zostanie przetworzone. Jest to nowa wartość kursora. Zapisz go niektóre magazynu trwałego, takich jak bazy danych, system plików lub usługi blob storage. Aby uzyskać więcej elementów katalogu, należy po prostu zacznij od [pierwszego kroku](#initialize-a-cursor) przez inicjowanie wartość kursora z tego magazynu trwałego.

Jeśli aplikacja zgłasza wyjątek lub błędów, nie przenoś kursora do przodu. Przenoszenie do przodu kursora ma co oznacza, że nie będą już ponownie potrzebne do przetwarzania elementów katalogu przed kursor.

Jeśli z jakiegoś powodu masz pozostawia usterkę w sposób przetwarzania wykazu, możesz po prostu przesuń kursor w tył i kodu ponownie przetworzyć starych elementów katalogu.

## <a name="c-sample-code"></a>Przykładowy kod języka C#

Ponieważ katalog jest zestaw dokumentów JSON, które są dostępne za pośrednictwem protokołu HTTP, może być interakcji z przy użyciu dowolnego języka programowania, którego klient HTTP i JSON Deserializator.

Przykłady w języku C# są dostępne w [repozytorium NuGet/Samples](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a>Katalog zestawu SDK

Najprostszym sposobem korzystania z wykazu jest użyć pakietu SDK katalogu .NET wersji wstępnej: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog). Ten pakiet jest dostępny na `nuget-build` MyGet źródła danych, dla którego możesz użyć pakietu NuGet źródłowy adres URL `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.

Ten pakiet można zainstalować na projekt niezgodny z `netstandard1.3` lub nowszej (np. .NET Framework 4.6).

Przykład za pomocą tego pakietu jest dostępny w witrynie GitHub w [projektu NuGet.Protocol.Catalog.Sample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).

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

### <a name="minimal-sample"></a>Minimalny przykładowy

Aby uzyskać przykład zależności w mniej ilustrujący interakcji z katalogu, które bardziej szczegółowo, zobacz [CatalogReaderExample przykładowy projekt](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample). Projekt jest ukierunkowany `netcoreapp2.0` i zależy od [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (w przypadku rozwiązywania indeks usług) i [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (w przypadku deserializacji JSON).

Główne logikę kodu jest widoczna w [pliku Program.cs](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).

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
