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
# <a name="query-for-all-packages-published-to-nugetorg"></a>Zapytanie dla wszystkich pakietów opublikowanych w celu nuget.org

Jeden typowy wzorzec kwerendy na starszych OData V2 API było wyliczenie wszystkich pakietów opublikowanych do nuget.org, uporządkowane przez kiedy pakiet został opublikowany. Scenariusze wymagające tego rodzaju zapytania względem nuget.org różnią się znacznie:

- Całkowicie replikując nuget.org
- Wykrywanie, kiedy pakiety mają nowe wersje wydane
- Znajdowanie pakietów zależnych od pakietu

Starszy sposób wykonywania tego zwykle zależy od sortowania jednostki pakietu OData przez sygnaturę `skip` `top` czasową i stronicowania w ogromnej zestaw wyników przy użyciu i (rozmiar strony) parametry. Niestety, takie podejście ma pewne wady:

- Możliwość brakujących pakietów, ponieważ zapytania są dokonywane na danych, które często zmieniają kolejność
- Powolny czas odpowiedzi na kwerendy, ponieważ kwerendy nie są zoptymalizowane (najbardziej zoptymalizowane zapytania to te, które obsługują scenariusz linii głównej dla oficjalnego klienta NuGet)
- Korzystanie z przestarzałego i nieudokumentowanego INTERFEJSU API, co oznacza, że obsługa takich zapytań w przyszłości nie jest gwarantowana
- Niezdolność do powtórki historii w dokładnie kolejności, w jakiej się wydarzyła

Z tego powodu można śledzić poniższy przewodnik, aby rozwiązać wyżej wymienione scenariusze w bardziej niezawodny i przyszłościowy sposób.

## <a name="overview"></a>Omówienie

W centrum tego przewodnika znajduje się zasób w [interfejsie API NuGet](../../api/overview.md) o nazwie **katalog**. Katalog jest interfejsem API tylko do dołączania, który umożliwia wywołującemu, aby zobaczyć pełną historię pakietów dodanych, zmodyfikowanych i usuniętych z nuget.org. Jeśli jesteś zainteresowany wszystkim lub nawet podzbiorem pakietów opublikowanych w nuget.org, katalog jest świetnym sposobem, aby być na bieżąco z zestawem aktualnie dostępnych pakietów w miarę upływu czasu.

Ten przewodnik ma być przejściem wysokiego poziomu, ale jeśli jesteś zainteresowany szczegółowymi szczegółami katalogu, zobacz jego [dokument referencyjny interfejsu API](../../api/catalog-resource.md).

Poniższe kroki można zaimplementować w dowolnym wybranym języku programowania. Jeśli chcesz pełnego uruchomionego przykładu, spójrz na [przykład języka C#,](#c-sample-code) o którym mowa poniżej.

W przeciwnym razie postępuj zgodnie z poniższym przewodnikiem, aby utworzyć niezawodny czytnik katalogów.

## <a name="initialize-a-cursor"></a>Inicjowanie kursora

Pierwszym krokiem w tworzeniu niezawodnego czytnika katalogów jest wdrożenie kursora. Aby uzyskać szczegółowe informacje na temat projektowania kursora katalogu, zobacz [dokument referencyjny katalogu](../../api/catalog-resource.md#cursor). Krótko mówiąc, kursor jest punktem w czasie, do którego zostały przetworzone zdarzenia w katalogu. Zdarzenia w katalogu reprezentują pakiet publikuje i inne zmiany pakietu. Jeśli zależy Ci na wszystkich pakietach kiedykolwiek opublikowanych w NuGet (od początku czasu), należy zainicjować kursor do `DateTime.MinValue` "minimalnej wartości" sygnatury czasowej (np. w .NET). Jeśli zależy Ci tylko na pakietach opublikowanych od teraz, użyjesz bieżącego sygnatury czasowej jako początkowej wartości kursora.

W tym przewodniku zainicjujemy nasz kursor do sygnatury czasowej godzinę temu. Na razie po prostu zapisz ten sygnatura czasowa w pamięci.

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a>Określanie adresu URL indeksu wykazu

Lokalizacja każdego zasobu (punktu końcowego) w interfejsie API NuGet powinna zostać odkryta przy użyciu [indeksu usługi.](../../api/service-index.md) Ponieważ ten przewodnik koncentruje się na nuget.org, będziemy używać indeksu usługi nuget.org.

    GET https://api.nuget.org/v3/index.json

Dokument serwisu jest dokumentem JSON zawierającym wszystkie zasoby na nuget.org. Poszukaj zasobu `@type` o `Catalog/3.0.0`wartości właściwości . Skojarzona `@id` wartość właściwości jest adresem URL samego indeksu katalogu. 

## <a name="find-new-catalog-leaves"></a>Znajdź nowe liście katalogu

Korzystając `@id` z wartości właściwości znalezionej w poprzednim kroku, pobierz indeks katalogu:

    GET https://api.nuget.org/v3/catalog0/index.json

Deserialize [indeksu katalogu](../../api/catalog-resource.md#catalog-index). Odfiltruj wszystkie `commitTimeStamp` obiekty strony [katalogu](../../api/catalog-resource.md#catalog-page-object-in-the-index) z mniejszą lub równą bieżącej wartości kursora.

Dla każdej pozostałej strony katalogu pobierz `@id` pełny dokument przy użyciu właściwości.

    GET https://api.nuget.org/v3/catalog0/page2926.json

Deserializacji [strony katalogu](../../api/catalog-resource.md#catalog-page). Odfiltruj wszystkie `commitTimeStamp` [obiekty liścia katalogu](../../api/catalog-resource.md#catalog-item-object-in-a-page) z mniejszą lub równą bieżącej wartości kursora.

Po pobraniu wszystkich stron katalogu, które nie zostały odfiltrowane, masz zestaw obiektów liścia katalogu reprezentujących pakiety, które zostały opublikowane, niepubliczne, wymienione lub usunięte w czasie między sygnaturą czasową kursora a teraz.

## <a name="process-catalog-leaves"></a>Liście katalogu przetwarzania

W tym momencie można wykonać dowolne niestandardowe przetwarzanie, które chcesz na elementach katalogu. Jeśli potrzebujesz tylko identyfikatora i wersji pakietu, można `nuget:id` sprawdzić `nuget:version` właściwości i właściwości na obiektach elementu katalogu znajdujących się na stronach. Upewnij się, aby `@type` spojrzeć na właściwość, aby dowiedzieć się, czy element katalogu dotyczy istniejącego pakietu lub usuniętego pakietu.

Jeśli jesteś zainteresowany metadanych o pakiecie (takich w opisie, zależności, .nupkg rozmiar, itp.), `@id` można pobrać [dokument liścia katalogu](../../api/catalog-resource.md#catalog-leaf) przy użyciu właściwości.

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

Ten dokument zawiera wszystkie metadane zawarte w [zasobie metadanych pakietu](../../api/registration-base-url-resource.md)i nie tylko!

Ten krok jest, gdzie można zaimplementować logikę niestandardową. Inne kroki w tym przewodniku są realizowane w prawie taki sam sposób, nie ma znaczenia, co robisz z liści katalogu.

### <a name="downloading-the-nupkg"></a>Pobieranie pliku .nupkg

Jeśli chcesz pobrać pakiety .nupkg znajdujące się w katalogu, możesz użyć [zasobu zawartości pakietu](../../api/package-base-address-resource.md). Należy jednak pamiętać, że istnieje krótkie opóźnienie między, gdy pakiet znajduje się w katalogu i gdy jest on dostępny w zasobie zawartości pakietu. W związku z `404 Not Found` tym jeśli wystąpi podczas próby pobrania .nupkg dla pakietu, który został znaleziony w katalogu, po prostu ponów próbę chwilę później. Naprawienie tego opóźnienia jest śledzone przez gitHub problem [NuGet/NuGetGallery #3455](https://github.com/NuGet/NuGetGallery/issues/3455).

## <a name="move-the-cursor-forward"></a>Przesuwanie kursora do przodu

Po pomyślnym przetworzeniu elementów katalogu należy określić nową wartość kursora do zapisania. Aby to zrobić, znajdź maksymalną (najnowszą chronologicznie) `commitTimeStamp` wszystkich przetworzonych elementów katalogu. Jest to nowa wartość kursora. Zapisz go w niektórych trwałych magazynów, takich jak baza danych, system plików lub magazyn obiektów blob. Jeśli chcesz uzyskać więcej elementów katalogu, po prostu zacznij od [pierwszego kroku,](#initialize-a-cursor) inicjując wartość kursora z tego magazynu trwałego.

Jeśli aplikacja zgłasza wyjątek lub błędy, nie należy przenosić kursora do przodu. Przesunięcie kursora do przodu ma znaczenie, że nigdy więcej nie trzeba przetwarzać elementów katalogu przed kursorem.

Jeśli z jakiegoś powodu masz błąd w sposobie przetwarzania liści katalogu, możesz po prostu przesunąć kursor do tyłu w czasie i zezwolić na ponowne przetworzenie kodu starych elementów katalogu.

## <a name="c-sample-code"></a>Przykładowy kod języka C#

Ponieważ katalog jest zestawem dokumentów JSON dostępnych za pośrednictwem protokołu HTTP, można go wchodzić w interakcje z przy użyciu dowolnego języka programowania, który ma klienta HTTP i deserializatorA JSON.

Próbki języka C# są dostępne w [repozytorium NuGet/Samples](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a>Katalog SDK

Najprostszym sposobem wykorzystania katalogu jest użycie pakietu zestawu SDK katalogu .NET w wersji wstępnej: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog). Ten pakiet jest `nuget-build` dostępny w kanale MyGet, dla którego `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`używasz adresu URL źródła pakietu NuGet .

Ten pakiet można zainstalować w `netstandard1.3` projekcie zgodnym z projektem lub większym (takim jak .NET Framework 4.6).

Przykład przy użyciu tego pakietu jest dostępny w usłudze GitHub w [projekcie NuGet.Protocol.Catalog.Sample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).

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

### <a name="minimal-sample"></a>Minimalna próbka

Na przykład z mniejszą liczbą zależności, która ilustruje interakcję z katalogiem bardziej szczegółowo, zobacz [CatalogReaderExample przykładowego projektu](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample). Projekt jest `netcoreapp2.0` przeznaczony i zależy od [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (do rozpoznawania indeksu usługi) i [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (dla deserializacji JSON).

Główna logika kodu jest widoczna w [pliku Program.cs](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).

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
