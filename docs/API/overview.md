---
title: Omówienie programu NuGet interfejsu API
description: Interfejs API NuGet jest zestaw punktów końcowych HTTP, które mogą służyć do pobierania pakietów, pobrać metadanych, publikowanie nowych pakietów itp.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: a638dba005c14bff4b2e668e2d6ca527a67b94a9
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-api"></a>NuGet interfejsu API

Interfejs API NuGet jest zestaw punktów końcowych HTTP, które może służyć do pobierania pakietów, pobrać metadanych publikowanie nowych pakietów i wykonywać większości innych operacji dostępne oficjalnego klientów NuGet z.

Ten interfejs API jest używany przez klienta NuGet w Visual Studio, nuget.exe i interfejsu wiersza polecenia platformy .NET w celu wykonania operacji NuGet, takich jak [ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore), wyszukiwanie w interfejsie użytkownika programu Visual Studio i [ `nuget.exe push` ](../tools/cli-ref-push.md).

Należy pamiętać, w niektórych przypadkach nuget.org ma dodatkowe wymagania, które nie są wymuszane przez inne źródła pakietu. Te różnice są udokumentowane przez [protokołów nuget.org](nuget-protocols.md).

## <a name="service-index"></a>Indeks usługi

Punkt wejścia dla interfejsu API jest dokumentem JSON w znanej lokalizacji. Ten dokument jest nazywany **indeksu usługi**. Lokalizacja indeks usługi nuget.org jest `https://api.nuget.org/v3/index.json`.

Ten dokument JSON zawiera listę *zasobów* co mieć inne funkcje i spełnienia innych przypadków użycia.

Klienci, którzy obsługują interfejs API powinna obsługiwać co najmniej jednego z tych adresów URL indeksu usługi jako sposób nawiązywania połączenia źródła odpowiednich pakietów.

Aby uzyskać więcej informacji o indeksie usługi, zobacz [jego dokumentacja interfejsu API](service-index.md).

## <a name="versioning"></a>Przechowywanie wersji

Interfejs API jest w wersji 3 NuGet protokołu HTTP. Ten protokół jest czasami nazywany "API w wersji 3." Te dokumenty odwołanie będzie odwoływać się do tej wersji protokołu po prostu jako "interfejsu API."

Wersja schematu indeksu usługi jest określane przez `version` właściwości w indeksie usługi. Interfejs API wymaga, że ciąg wersji ma numer wersji głównej `3`. Nierozdzielające zmiany do schematu indeksu usługi, zostanie zwiększona wersja pomocnicza ciąg wersji.

Starszych klientów (takich jak nuget.exe 2.x) nie obsługują interfejsu API w wersji 3 i obsługują tylko starsze V2 interfejsu API, który nie jest opisane w tym miejscu.

Interfejsu API w wersji 3 NuGet nosi nazwę jako takie ponieważ jest on następnika interfejsu API w wersji 2, który został zaimplementowany przez wersję 2.x oficjalnego klienta NuGet protokół OData na podstawie. Interfejsu API w wersji 3 najpierw jest obsługiwana przez wersję 3.0 oficjalnego klienta NuGet i nadal jest najnowsza wersja główna protocol w wersji obsługiwany przez klienta NuGet, 4.0 i. 

Wprowadzono zmiany protokołu bez podziału do interfejsu API od czasu pierwszej wersji.

## <a name="resources-and-schema"></a>Zasoby i schematu

**Indeksu usługi** opisano różne zasoby. Bieżący zestaw zasobów obsługiwane są następujące:

Nazwa zasobu                                                          | Wymagane | Opis
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | Tak      | Wypychanie i usunąć lub unlist pakietów.
[`SearchQueryService`](search-query-service-resource.md)               | Tak      | Filtr i wyszukaj pakietów według słów kluczowych.
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | Tak      | Pobierz pakiet metadanych.
[`PackageBaseAddress`](package-base-address-resource.md)               | Tak      | Pobierz zawartość pakietu (.nupkg).
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | Brak       | Odnajdź identyfikatorów pakietów i wersje przez podciąg.
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | Brak       | Utworzyć adres URL "zgłaszania nadużyć" strona sieci web.
[`Catalog`](catalog-resource.md)                                       | Brak       | Pełną dokumentację wszystkie zdarzenia pakietu.

Ogólnie rzecz biorąc wszystkie dane nieznakowe zwrócony przez zasób interfejsu API są serializowane, za pomocą formatu JSON. Odpowiedź Schemat zwrócony przez każdy zasób w indeksie usługi zdefiniowano indywidualnie dla tego zasobu. Aby uzyskać więcej informacji na temat każdego z zasobów zobacz tematy wymienione powyżej.

> [!Note]
> Jeśli źródło nie implementuje `SearchAutocompleteService` wszystkie zachowania autouzupełniania, które powinny być wyłączone bezpiecznie. Gdy `ReportAbuseUriTemplate` nie jest zaimplementowana, oficjalnego powróci klienta NuGet do nuget.org raport nadużycia adresu URL (śledzonych przez [NuGet domowych #4924](https://github.com/NuGet/Home/issues/4924)). Inni klienci mogą zdecydować się na po prostu nie przedstawiają adres URL raportu nadużyć dla użytkownika.

## <a name="timestamps"></a>Znaczniki czasu

Wszystkie sygnatury czasowe zwracane przez interfejs API są UTC lub w przeciwnym razie są określane za pomocą [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) reprezentacji. 

## <a name="http-methods"></a>Metody HTTP

Zlecenie   | Zastosowanie
------ | -----------
POBIERZ    | Wykonuje operację tylko do odczytu, zazwyczaj podczas pobierania danych.
HEAD   | Pobiera nagłówki odpowiedzi dla odpowiedniego `GET` żądania.
UMIEŚĆ    | Tworzy z zasobem, który nie istnieje lub, jeśli istnieje, aktualizuje. Niektóre zasoby mogą nie obsługiwać aktualizacji.
DELETE | Usuwa lub unlists zasobu.

## <a name="http-status-codes"></a>Kody stanu HTTP

Kod | Opis
---- | -----
200  | Sukces, a treść odpowiedzi.
201  | Utworzono sukcesu i zasobu.
202  | Sukces, żądanie zostało zaakceptowane, ale niektóre pracy może być niekompletna i zakończonych asynchronicznie.
204  | Sukces, ale brak treści odpowiedzi.
301  | Stałe przekierowanie.
302  | Przekierowanie tymczasowe.
400  | Parametry w adresie URL lub w treści żądania są nieprawidłowe.
401  | Podane poświadczenia są nieprawidłowe.
403  | Akcja nie jest dozwolona w podanej podanych poświadczeń.
404  | Żądany zasób nie istnieje.
409  | Konflikty żądania z istniejącego zasobu.
500  | Usługa napotkała nieoczekiwany błąd.
503  | Usługa jest tymczasowo niedostępna.

Wszelkie `GET` żądania skierowane do punktu końcowego interfejsu API może zwrócić przekierowania HTTP (301 lub 302). Klienci powinna obsługiwać takie przekierowuje obserwując `Location` nagłówka oraz wydawanie kolejnej `GET`. Dokumentację dotyczącą określonych punktów końcowych nie zostanie jawnie wywoływać się, których można użyć przekierowania.

W przypadku kodu stanu 500 poziomu klienta można zaimplementować mechanizm ponawiania uzasadnione. Oficjalna NuGet klienta ponowne próby trzy razy, gdy wystąpią kod stanu 500 poziomu ani błędu TCP/serwera DNS.

## <a name="http-request-headers"></a>Nagłówki żądania HTTP

Nazwa                     | Opis
------------------------ | -----------
X-NuGet-ApiKey           | Wymagane do wypychania i usuwania, zobacz [ `PackagePublish` zasobów](package-publish-resource.md)
X-NuGet-Client-Version   | **Przestarzałe** i zastąpione przez `X-NuGet-Protocol-Version`
X-NuGet-Protocol-Version | W niektórych przypadkach tylko na nuget.org wymagane, zobacz [protokołów nuget.org](NuGet-Protocols.md)
X-NuGet-Session-Id       | *Opcjonalne*. NuGet klientów v4.7 + zidentyfikować żądania HTTP, które są częścią tej samej sesji klienta NuGet. Aby uzyskać `PackageReference` operacji przywracania nie jest identyfikatorem jednej sesji w innych sytuacjach, takich jak automatyczne uzupełnianie, i `packages.config` przywracania może istnieć kilka różnych identyfikatora sesji przez ze względu na sposób kod jest brana pod uwagę.

## <a name="authentication"></a>Uwierzytelnianie

Do wykonania źródła pakietu do definiowania pozostanie uwierzytelniania. Dla nuget.org tylko `PackagePublish` zasób wymaga uwierzytelnienia za pomocą specjalnych nagłówków klucza interfejsu API. Zobacz [ `PackagePublish` zasobów](package-publish-resource.md) szczegółowe informacje.
