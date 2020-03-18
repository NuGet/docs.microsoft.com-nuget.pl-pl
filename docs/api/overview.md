---
title: Omówienie interfejsu API serwera NuGet
description: Interfejs API serwera NuGet to zbiór punktów końcowych HTTP, których można użyć do pobierania pakietów, pobierania metadanych, publikowania nowych pakietów itd.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: aacf56a5dc5af9abf6f60d42bc7fd530a128d0d8
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428710"
---
# <a name="nuget-server-api"></a>Interfejs API serwera NuGet

Interfejs API serwera NuGet to zbiór punktów końcowych HTTP, których można użyć do pobierania pakietów, pobierania metadanych, publikowania nowych pakietów i wykonywania większości innych operacji dostępnych w oficjalnych klientach programu NuGet.

Ten interfejs API jest używany przez klienta NuGet w programie Visual Studio, NuGet. exe i interfejsu wiersza polecenia platformy .NET do wykonywania operacji NuGet, takich jak [`dotnet restore`](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), wyszukiwania w interfejsie użytkownika programu Visual Studio i [`nuget.exe push`](../reference/cli-reference/cli-ref-push.md).

Uwaga w niektórych przypadkach nuget.org ma dodatkowe wymagania, które nie są wymuszane przez inne źródła pakietów. Te różnice są udokumentowane przez [protokoły NuGet.org](nuget-protocols.md).

Aby zapoznać się z prostym wyliczeniem i pobieraniem dostępnych wersji programu NuGet. exe, zobacz punkt końcowy [Tools. JSON](tools-json.md) .

## <a name="service-index"></a>Indeks usług

Punkt wejścia dla interfejsu API jest dokumentem JSON w dobrze znanej lokalizacji. Ten dokument jest nazywany **indeksem usługi**. Lokalizacja indeksu usługi dla nuget.org jest `https://api.nuget.org/v3/index.json`.

Ten dokument JSON zawiera listę *zasobów* , które zapewniają różne funkcje i spełniają różne przypadki użycia.

Klienci, którzy obsługują interfejs API, powinni akceptować co najmniej jeden adres URL indeksu usługi jako sposób łączenia się z odpowiednimi źródłami pakietów.

Aby uzyskać więcej informacji na temat indeksu usługi, zobacz [jego dokumentacja interfejsu API](service-index.md).

## <a name="versioning"></a>Obsługa wersji

Interfejs API jest w wersji 3 protokołu HTTP programu NuGet. Ten protokół jest czasami określany jako "interfejs API v3". Te dokumenty referencyjne odnoszą się do tej wersji protokołu po prostu jako "interfejs API".

Wersja schematu indeksu usługi jest wskazywana przez właściwość `version` w indeksie usługi. Interfejs API wymaga, aby ciąg wersji miał numer wersji głównej `3`. Ponieważ zmiany niekrytyczne są wprowadzane do schematu indeksu usługi, zostanie zwiększona wersja pomocnicza ciągu wersji.

Starsze komputery klienckie (takie jak NuGet. exe 2. x) nie obsługują interfejsu API v3 i obsługują tylko starszy interfejs API v2, który nie jest udokumentowany w tym miejscu.

Interfejs API programu NuGet V3 jest nazwany jako taki, ponieważ jest następnikiem interfejsu API v2, który był protokołem opartym na protokole OData wdrożonym przez wersję 2. x oficjalnego klienta NuGet. Interfejs API v3 został po raz pierwszy obsługiwany przez wersję 3,0 oficjalnego klienta NuGet i nadal jest Najnowsza wersja głównego protokołu obsługiwana przez klienta NuGet, 4,0 i w systemie. 

W interfejsie API wprowadzono nieprzerwane zmiany protokołu, ponieważ zostały one po raz pierwszy wydane.

## <a name="resources-and-schema"></a>Zasoby i schemat

**Indeks usługi** zawiera opis różnych zasobów. Bieżący zestaw obsługiwanych zasobów jest następujący:

Nazwa zasobu                                                        | Wymagany | Opis
-------------------------------------------------------------------- | -------- | -----------
[Wykaz](catalog-resource.md)                                       | nie       | Pełny rekord wszystkich zdarzeń pakietu.
[PackageBaseAddress](package-base-address-resource.md)               | tak      | Pobierz zawartość pakietu (. nupkg).
[PackageDetailsUriTemplate](package-details-template-resource.md)    | nie       | Utwórz adres URL, aby uzyskać dostęp do strony sieci Web szczegółów pakietu.
[PackagePublish](package-publish-resource.md)                        | tak      | Pakiety wypychania i usuwania (lub z listy).
[RegistrationsBaseUrl](registration-base-url-resource.md)            | tak      | Pobierz metadane pakietu.
[ReportAbuseUriTemplate](report-abuse-resource.md)                   | nie       | Utwórz adres URL, aby uzyskać dostęp do strony sieci Web nadużycia raportu.
[RepositorySignatures](repository-signatures-resource.md)            | nie       | Pobierz certyfikaty używane do podpisywania repozytorium.
[SearchAutocompleteService](search-autocomplete-service-resource.md) | nie       | Wykryj identyfikatory pakietów i wersje według podciągu.
[SearchQueryService](search-query-service-resource.md)               | tak      | Filtrowanie i wyszukiwanie pakietów według słowa kluczowego.
[SymbolPackagePublish](symbol-package-publish-resource.md)           | nie       | Pakiety symboli wypychania.

Ogólnie rzecz biorąc, wszystkie dane niebinarne zwrócone przez zasób interfejsu API są serializowane przy użyciu formatu JSON. Schemat odpowiedzi zwracany przez każdy zasób w indeksie usługi jest definiowany indywidualnie dla tego zasobu. Aby uzyskać więcej informacji na temat poszczególnych zasobów, zobacz tematy wymienione powyżej.

W przyszłości w miarę rozwoju protokołu nowe właściwości mogą zostać dodane do odpowiedzi JSON. Aby klient mógł działać w przyszłości, implementacja nie powinna zakładać, że schemat odpowiedzi jest końcowy i nie może zawierać dodatkowych danych. Wszystkie właściwości, które nie są rozpoznawane przez implementację, powinny być ignorowane.

> [!Note]
> Gdy źródło nie implementuje `SearchAutocompleteService` wszelkie zachowania autouzupełniania należy wyłączyć bezpiecznie. Gdy `ReportAbuseUriTemplate` nie zostanie zaimplementowana, Oficjalny klient NuGet powróci do programu NuGet. adres URL nadużycia raportu w organizacji (śledzony przez [NuGet/Home # 4924](https://github.com/NuGet/Home/issues/4924)). Inni klienci mogą zrezygnować z pokazywania adresu URL nadużycia raportu dla użytkownika.

### <a name="undocumented-resources-on-nugetorg"></a>Zasoby nieudokumentowane w witrynie nuget.org

Indeks usługi v3 na nuget.org zawiera zasoby, które nie zostały opisane powyżej. Istnieje kilka przyczyn niedokumentowania zasobu.

Najpierw nie dokumentuje zasobów używanych jako szczegóły implementacji NuGet.org. `SearchGalleryQueryService` należy do tej kategorii. [NuGetGallery](https://github.com/NuGet/NuGetGallery) używa tego zasobu do delegowania niektórych zapytań v2 (OData) do naszego indeksu wyszukiwania zamiast przy użyciu bazy danych. Ten zasób został wprowadzony ze względu na skalowalność i nie jest przeznaczony do użytku zewnętrznego.

Po drugie nie są udokumentowane zasoby, które nigdy nie zostały dostarczone w wersji RTM oficjalnego klienta.
`PackageDisplayMetadataUriTemplate` i `PackageVersionDisplayMetadataUriTemplate` należeć do tej kategorii.

W trzecim przypadku nie dokumentuje zasobów, które są ściśle powiązane z protokołem v2, który sam jest celowo. Zasób `LegacyGallery` należy do tej kategorii. Ten zasób umożliwia indeksowi usługi v3 wskazanie odpowiedniego źródłowego adresu URL w wersji 2. Ten zasób obsługuje `nuget.exe list`.

Jeśli zasób nie jest tutaj udokumentowany, *zdecydowanie* zalecamy, aby nie korzystać z nich zależnych. Firma Microsoft może usunąć lub zmienić zachowanie tych nieudokumentowanych zasobów, co może spowodować uszkodzenie implementacji w nieoczekiwany sposób.

## <a name="timestamps"></a>Znaczniki czasu

Wszystkie sygnatury czasowe zwracane przez interfejs API są UTC lub w przeciwnym razie są określone przy użyciu reprezentacji [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) . 

## <a name="http-methods"></a>Metody HTTP

Czasownik   | Użycie
------ | -----------
GET    | Wykonuje operację tylko do odczytu, zazwyczaj pobierając dane.
MTP   | Pobiera nagłówki odpowiedzi dla odpowiedniego żądania `GET`.
PUT    | Tworzy zasób, który nie istnieje lub, jeśli istnieje, aktualizuje go. Niektóre zasoby mogą nie obsługiwać aktualizacji.
DELETE | Usuwa zasób lub go wystawia.

## <a name="http-status-codes"></a>Kody stanu HTTP

Kod | Opis
---- | -----
200  | Powodzenie i istnieje treść odpowiedzi.
201  | Zakończyło się pomyślnie, a zasób został utworzony.
202  | Żądanie zostało zaakceptowane, ale niektóre zadania mogą być nadal niekompletne i wykonane asynchronicznie.
204  | Sukces, ale nie ma treści odpowiedzi.
301  | Stałe przekierowanie.
302  | Tymczasowe przekierowanie.
400  | Parametry w adresie URL lub w treści żądania są nieprawidłowe.
401  | Podane poświadczenia są nieprawidłowe.
403  | Akcja nie jest dozwolona przy użyciu podanych poświadczeń.
404  | Żądany zasób nie istnieje.
409  | Żądanie powoduje konflikt z istniejącym zasobem.
500  | Usługa napotkała nieoczekiwany błąd.
503  | Usługa jest tymczasowo niedostępna.

Każde żądanie `GET` skierowane do punktu końcowego interfejsu API może zwrócić Przekierowanie HTTP (301 lub 302). Klienci powinni bezpiecznie obsługiwać takie przekierowania, przestrzegając nagłówka `Location` i wydając kolejne `GET`. Dokumentacja dotycząca określonych punktów końcowych nie zostanie jawnie wywołana, gdzie można używać przekierowań.

W przypadku kodu stanu 500 na poziomie, klient może zaimplementować rozsądny mechanizm ponawiania prób. Oficjalny klient NuGet ponawia próbę trzykrotnie podczas napotkania dowolnego kodu stanu 500 lub błędu TCP/DNS.

## <a name="http-request-headers"></a>Nagłówki żądań HTTP

Name (Nazwa)                     | Opis
------------------------ | -----------
X-NuGet-ApiKey           | Wymagane do wypychania i usuwania, zobacz [`PackagePublish` Resource](package-publish-resource.md)
X-NuGet-Client-Version   | **Przestarzałe** i zastąpione przez `X-NuGet-Protocol-Version`
X-NuGet-Protocol-Version | Wymagane w niektórych przypadkach tylko na nuget.org, zobacz [NuGet.org Protocols](NuGet-Protocols.md)
X-NuGet-Session-Id       | *Opcjonalnie*. Klienci NuGet v 4.7 + identyfikują żądania HTTP, które są częścią tej samej sesji klienta NuGet.

`X-NuGet-Session-Id` ma jedną wartość dla wszystkich operacji związanych z pojedynczym przywracaniem w `PackageReference`. W przypadku innych scenariuszy, takich jak Autouzupełnianie i `packages.config` przywracanie może istnieć kilka różnych identyfikatorów sesji ze względu na sposób, w jaki kod jest rozliczane.

## <a name="authentication"></a>Uwierzytelnianie

Uwierzytelnianie jest pozostawiane do wdrożenia źródła pakietu do zdefiniowania. W przypadku nuget.org tylko zasób `PackagePublish` wymaga uwierzytelniania za pośrednictwem specjalnego nagłówka klucza interfejsu API. Aby uzyskać szczegółowe informacje, zobacz [`PackagePublish` Resource](package-publish-resource.md) .
