---
title: Zapytanie dotyczące wszystkich pakietów opublikowanych w usłudze nuget.org
description: Za pomocą interfejsu API NuGet można wysyłać zapytania dotyczące wszystkich pakietów opublikowanych w nuget.org i zachować aktualność w miarę upływu czasu.
author: joelverhagen
ms.author: jver
ms.date: 11/02/2017
ms.topic: tutorial
ms.reviewer: kraigb
ms.openlocfilehash: 749d9466976d51c7cb65332c8b149e3a30862e63
ms.sourcegitcommit: 650c08f8bc3d48dfd206a111e5e2aaca3001f569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97523404"
---
# <a name="query-for-all-packages-published-to-nugetorg"></a>Zapytanie dotyczące wszystkich pakietów opublikowanych w usłudze nuget.org

Jeden wspólny wzorzec zapytania w starszym interfejsie API OData v2 wylicza wszystkie pakiety opublikowane w nuget.org, uporządkowane według czasu opublikowania pakietu. Scenariusze wymagające tego rodzaju zapytania dotyczące nuget.org są szeroko rozliczane:

- Całkowicie replikowanie nuget.org
- Wykrywanie, kiedy pakiety mają nowe wersje wydane
- Znajdowanie pakietów, które są zależne od pakietu

Starsza Metoda przeprowadzenia tej operacji zwykle zależy od sortowania jednostki pakietu OData przez sygnaturę czasową i stronicowanie w ramach ogromnego zestawu wyników przy użyciu `skip` `top` parametrów i (rozmiaru strony). Niestety, takie podejście ma pewne wady:

- Możliwość braku pakietów, ponieważ są wykonywane zapytania dotyczące danych, które często zmieniają kolejność
- Długi czas odpowiedzi na zapytanie, ponieważ zapytania nie są zoptymalizowane (najbardziej zoptymalizowane zapytania to te, które obsługują scenariusz linii głównej dla oficjalnego klienta NuGet)
- Użycie przestarzałego i nieudokumentowanego interfejsu API, co oznacza, że obsługa takich zapytań nie jest gwarantowana
- Niezdolność do powtarzania historii w dokładnej kolejności, w której transpired

Z tego powodu Poniższy przewodnik może posłużyć do rozwiązania powyższych scenariuszy w bardziej niezawodnej i przyszłej próbie.

## <a name="overview"></a>Omówienie

W centrum tego przewodnika jest zasób w [interfejsie API NuGet](../../api/overview.md) o nazwie **wykaz**. Katalog jest interfejsem API tylko do dołączania, który umożliwia wywołującemu wyświetlanie pełnej historii pakietów dodanych do, zmodyfikowanych i usuniętych z nuget.org. Jeśli interesuje Cię wszystkie lub nawet podzbiór pakietów opublikowanych w usłudze nuget.org, katalog jest doskonałym sposobem na utrzymanie Aktualności z zestawem aktualnie dostępnych pakietów jako czas, w którym się znajdują.

Ten przewodnik jest przeznaczony do ogólnego przechodzenia, ale jeśli interesuje Cię szczegółowe informacje o wykazie, zobacz jego [dokument referencyjny interfejsu API](../../api/catalog-resource.md).

Poniższe kroki można zaimplementować w dowolnym wybranym języku programowania. Jeśli chcesz wykonać pełny przykład, zapoznaj się z [przykładem w języku C#](#c-sample-code) opisanym poniżej.

W przeciwnym razie postępuj zgodnie z poniższym przewodnikiem, aby utworzyć niezawodny czytnik wykazu.

## <a name="initialize-a-cursor"></a>Inicjowanie kursora

Pierwszym krokiem tworzenia niezawodnego czytnika wykazu jest implementacja kursora. Aby uzyskać szczegółowe informacje na temat projektu kursora katalogu, zobacz [dokument odwołania do katalogu](../../api/catalog-resource.md#cursor). W skrócie kursor jest punktem w czasie, w którym przetworzono zdarzenia w wykazie. Zdarzenia w wykazie reprezentują publikowanie pakietów i inne zmiany pakietu. Jeśli postanowisz o wszystkich pakietach opublikowanych w pakiecie NuGet (od momentu rozpoczęcia), możesz zainicjować kursor do sygnatury czasowej "wartość minimalna" (np. `DateTime.MinValue` w programie .NET). Jeśli masz szczególną uwagę na to, że na bieżąco z opublikowanymi pakietami, Użyj bieżącej sygnatury czasowej jako początkowej wartości kursora.

W tym przewodniku zainicjujemy nasz kursor do sygnatury czasowej o godzinę temu. Na razie po prostu Zapisz tę sygnaturę czasową w pamięci.

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a>Określ adres URL indeksu katalogu

Lokalizację każdego zasobu (punkt końcowy) w interfejsie API NuGet należy odnaleźć przy użyciu [indeksu usługi](../../api/service-index.md). Ponieważ ten przewodnik koncentruje się na nuget.org, będziemy używać narzędzia NuGet. indeks usługi w organizacji.

    GET https://api.nuget.org/v3/index.json

Dokument usługi jest dokumentem JSON zawierającym wszystkie zasoby w nuget.org. Poszukaj zasobu mającego `@type` wartość właściwości `Catalog/3.0.0` . Skojarzona `@id` wartość właściwości jest adresem URL samego indeksu katalogu. 

## <a name="find-new-catalog-leaves"></a>Znajdź nowy wykaz liści

Korzystając z `@id` wartości właściwości znalezionej w poprzednim kroku, Pobierz indeks wykazu:

    GET https://api.nuget.org/v3/catalog0/index.json

Deserializacja [indeksu katalogu](../../api/catalog-resource.md#catalog-index). Odfiltruj wszystkie [obiekty strony katalogu](../../api/catalog-resource.md#catalog-page-object-in-the-index) `commitTimeStamp` , których wartość jest mniejsza lub równa bieżącej wartości kursora.

Dla każdej pozostałej strony wykazu Pobierz pełny dokument przy użyciu `@id` właściwości.

    GET https://api.nuget.org/v3/catalog0/page2926.json

Deserializacja [strony katalogu](../../api/catalog-resource.md#catalog-page). Odfiltruj wszystkie [obiekty liści wykazu](../../api/catalog-resource.md#catalog-item-object-in-a-page) z `commitTimeStamp` mniejszą lub równą bieżącej wartości kursora.

Po pobraniu wszystkich stron wykazu, które nie zostały odfiltrowane, istnieje zestaw obiektów liści wykazu reprezentujących pakiety, które zostały opublikowane, niewymienione na liście lub usunięte w czasie między znacznikiem czasu kursora a teraz.

## <a name="process-catalog-leaves"></a>Urlopy katalogu procesów

W tym momencie można wykonać dowolne niestandardowe przetwarzanie dla elementów katalogu. Jeśli wszystko, co jest potrzebne, to identyfikator i wersja pakietu, można sprawdzić `nuget:id` `nuget:version` właściwości i w obiektach elementów wykazu znalezionych na stronach. Zwróć uwagę na `@type` Właściwość, aby dowiedzieć się, czy element katalogu dotyczy istniejącego pakietu lub usuniętego pakietu.

Jeśli interesują Cię metadane dotyczące pakietu (na przykład opis, zależności, rozmiar NUPKG itp.), możesz pobrać [dokument liścia katalogu](../../api/catalog-resource.md#catalog-leaf) przy użyciu `@id` właściwości.

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

Ten dokument zawiera wszystkie metadane zawarte w [zasobie metadanych pakietu](../../api/registration-base-url-resource.md)i inne.

Ten krok polega na zaimplementowaniu logiki niestandardowej. Pozostałe kroki przedstawione w tym przewodniku są implementowane w taki sam sposób, jak w przypadku liści wykazu.

### <a name="downloading-the-nupkg"></a>Pobieranie NUPKG

Jeśli interesuje Cię pobieranie elementu. nupkg dla pakietów znalezionych w katalogu, możesz użyć [zasobu zawartości pakietu](../../api/package-base-address-resource.md). Należy jednak pamiętać, że istnieje krótkie opóźnienie między wykrytym pakietem w katalogu i udostępnieniem go w zasobie zawartości pakietu. W związku z tym, jeśli wystąpią `404 Not Found` próby pobrania elementu. nupkg dla pakietu znalezionego w wykazie, po prostu spróbuj ponownie później. Naprawianie tego opóźnienia jest śledzone w usłudze GitHub wydanie [NuGet/NuGetGallery # 3455](https://github.com/NuGet/NuGetGallery/issues/3455).

## <a name="move-the-cursor-forward"></a>Przesuń kursor do przodu

Po pomyślnym przetworzeniu elementów katalogu należy określić nową wartość kursora, która ma zostać zapisana. Aby to zrobić, Znajdź maksymalną (aktualną) `commitTimeStamp` wszystkie elementy katalogu, które zostały przetworzone. To jest nowa wartość kursora. Zapisz ją w magazynie trwałym, takim jak baza danych, system plików lub magazyn obiektów BLOB. Aby uzyskać więcej elementów katalogu, wystarczy zacząć od [pierwszego kroku](#initialize-a-cursor) , inicjując wartość kursora z tego magazynu trwałego.

Jeśli aplikacja zgłasza wyjątek lub błędy, nie przenoś kursora do przodu. Przesuwanie kursora do przodu ma znaczenie, że nie trzeba ponownie przetwarzać elementów katalogu przed kursorem.

Jeśli z jakiegoś powodu jest dostępna usterka w sposobie przetwarzania liści wykazu, można po prostu przesunąć kursor wstecz w czasie i zezwolić kodowi na ponowne przetwarzanie starych elementów katalogu.

## <a name="c-sample-code"></a>Przykładowy kod w języku C#

Ponieważ katalog jest zestawem dokumentów JSON dostępnych za pośrednictwem protokołu HTTP, można z nich korzystać przy użyciu dowolnego języka programowania, który ma klienta HTTP i Deserializator JSON.

Przykłady w języku C# są dostępne w [repozytorium NuGet/Samples](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a>Zestaw SDK katalogu

Najprostszym sposobem korzystania z wykazu jest użycie pakietu SDK katalogu platformy .NET w wersji wstępnej `NuGet.Protocol.Catalog` , który jest dostępny na Azure Artifacts przy użyciu następującego źródłowego adresu URL pakietu NuGet: `https://pkgs.dev.azure.com/dnceng/public/_packaging/nuget-build/nuget/v3/index.json` .

Ten pakiet można zainstalować w projekcie zgodnym z `netstandard1.3` lub większym (np. .NET Framework 4,6).

Przykład korzystania z tego pakietu jest dostępny w witrynie GitHub w [projekcie NuGet. Protocol. Catalog. sample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).

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

### <a name="minimal-sample"></a>Minimalny przykład

Przykład z mniejszą liczbą zależności, która ilustruje interakcję z katalogiem bardziej szczegółowym, można znaleźć w przykładowym [projekcie CatalogReaderExample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample). Obiekt docelowy projektu `netcoreapp2.0` i zależy od elementu [NuGet. Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (do rozpoznawania indeksu usługi) i [Newtonsoft.Jsna 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (dla deserializacji JSON).

Główna logika kodu jest widoczna w [pliku program.cs](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).

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
