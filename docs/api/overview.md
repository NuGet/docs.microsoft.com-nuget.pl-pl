---
title: Omówienie pakietu nuget interfejsu API
description: Interfejs API NuGet jest zestaw punktów końcowych HTTP, które mogą służyć do pobierania pakietów, pobierania metadanych, publikowanie nowych pakietów itp.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 770173d6b84048cf42a5da46cbc474d8cf604a08
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547506"
---
# <a name="nuget-api"></a>Interfejs API programu NuGet

Interfejs API NuGet jest zestaw punktów końcowych HTTP, które można pobrać pakiety, pobrać metadanych, opublikować nowe pakiety i wykonywać większości inne operacje dostępne w oficjalnym klientom programu NuGet.

Ten interfejs API jest używany przez klienta programu NuGet w Visual Studio, nuget.exe oraz interfejsu wiersza polecenia platformy .NET do wykonywania operacji NuGet, takich jak [ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore), wyszukiwanie w interfejsie użytkownika Visual Studio i [ `nuget.exe push` ](../tools/cli-ref-push.md).

Należy pamiętać, w niektórych przypadkach nuget.org ma dodatkowe wymagania, które nie są wymuszane przez inne źródła pakietu. Te różnice są opisane przez [protokoły nuget.org](nuget-protocols.md).

Wyliczenie proste i pobierania nuget.exe dostępnych wersji, zobacz [tools.json](tools-json.md) punktu końcowego.

## <a name="service-index"></a>Indeks usług

Punkt wejścia dla interfejsu API to dokument JSON w dobrze znanej lokalizacji. Ten dokument jest nazywany **indeks usług**. Lokalizacja indeks usługi nuget.org znajduje się `https://api.nuget.org/v3/index.json`.

Ten dokument JSON zawiera listę *zasobów* które oferują różne funkcje i realizowania różnych przypadków użycia.

Klientów, którzy obsługują interfejs API powinna obsługiwać co najmniej jedną z tych adresów URL indeksu usługi, co oznacza, że jest łączenie ze źródłami odpowiedniego pakietu.

Aby uzyskać więcej informacji na temat indeks usług zobacz [jego dokumentacja interfejsu API](service-index.md).

## <a name="versioning"></a>Przechowywanie wersji

Interfejs API jest w wersji 3 NuGet protokołu HTTP. Ten protokół jest czasami określane jako "w wersji 3 interfejsu API." Te dokumenty referencyjne będzie odnosił się do tej wersji protokołu, po prostu jako "interfejsu API."

Wersja schematu indeksu usługi jest wskazywane przez `version` właściwość w indeksie usługi. Interfejs API określającemu, że ciąg wersji zawiera numer wersji głównej `3`. Wprowadzaniu zmian niepowodujących niezgodności na schemat indeksu service, wersja pomocnicza ciąg wersji zostanie zwiększona.

Starsi klienci (takie jak nuget.exe 2.x) nie obsługują interfejsu API w wersji 3 i obsługują tylko starsze V2 interfejsu API, który nie jest opisane w tym miejscu.

Interfejsu API programu NuGet w wersji 3 nosi nazwę jako takie, ponieważ ta usługa jest następcą interfejsu API w wersji 2, który był protokół OData na podstawie implementowany przez oficjalne klienta programu NuGet w wersji 2.x. Interfejs API w wersji 3 pierwsze była obsługiwana przez wersję 3.0 oficjalne klienta programu NuGet i nadal jest najnowsza wersja główna protocol w wersji obsługiwany przez klienta programu NuGet 4.0, a także na. 

Wprowadzono zmiany protokołu bez podziału do interfejsu API od czasu pierwszej wersji.

## <a name="resources-and-schema"></a>Schemat i zasoby

**Indeks usług** zawiera opis różnych zasobów. Bieżący zestaw zasobów, obsługiwane są następujące:

Nazwa zasobu                                                          | Wymagane | Opis
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | Tak      | Wypychanie i usuwanie lub wyrejestrowanie pakietów.
[`SearchQueryService`](search-query-service-resource.md)               | Tak      | Filtr i wyszukiwanie pakietów według słowa kluczowego.
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | Tak      | Pobierz metadane pakietów.
[`PackageBaseAddress`](package-base-address-resource.md)               | Tak      | Pobierz zawartość pakietu (.nupkg).
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | Brak       | Odkryj identyfikatorów pakietu i wersje, podciąg.
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | Brak       | Skonstruuj adres URL "Zgłoś nadużycie" strona sieci web.
[`RepositorySignatures`](repository-signatures-resource.md)            | Brak       | Pobierz certyfikaty używane do podpisywania repozytorium.
[`Catalog`](catalog-resource.md)                                       | Brak       | Pełną dokumentację wszystkich zdarzeń pakietu.

Ogólnie rzecz biorąc wszystkie dane nieznakowe zwrócony przez zasobu interfejsu API są serializowane, przy użyciu formatu JSON. Schemat odpowiedzi zwrócony przez każdego zasobu w indeksie usługi zdefiniowano indywidualnie dla tego zasobu. Aby uzyskać więcej informacji na temat poszczególnych zasobów zobacz tematy wymienione powyżej.

> [!Note]
> Jeśli źródło nie implementuje `SearchAutocompleteService` każde zachowanie automatycznego uzupełniania, które powinny być wyłączone bezpiecznie. Gdy `ReportAbuseUriTemplate` nie zaimplementowaniu oficjalna powróci klienta NuGet do usługi nuget.org Zgłoś nadużycie adresu URL (śledzonych przez [domowych NuGet #4924](https://github.com/NuGet/Home/issues/4924)). Inni klienci mogą wybrać, czy po prostu nie przedstawiają nadużycie adresu URL raportu użytkownika.

## <a name="timestamps"></a>Sygnatury czasowe

Wszystkie sygnatury czasowe zwracane przez interfejs API to UTC lub w przeciwnym razie są określane za pomocą [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) reprezentacji. 

## <a name="http-methods"></a>Metody HTTP

zlecenia   | Zastosowanie
------ | -----------
POBIERZ    | Wykonuje operację tylko do odczytu, zazwyczaj podczas pobierania danych.
GŁÓWNY   | Pobiera nagłówki odpowiedzi dla odpowiedniego `GET` żądania.
PUT    | Tworzy zasób, który nie istnieje, lub jeśli istnieje, aktualizuje je. Niektóre zasoby mogą nie obsługiwać aktualizacji.
DELETE | Usuwa lub unlists zasobu.

## <a name="http-status-codes"></a>Kody stanu HTTP

Kod | Opis
---- | -----
200  | Sukces, a treść odpowiedzi.
201  | Powodzenie i zasób został utworzony.
202  | Sukces, żądanie zostało przyjęte, ale pewnej pracy może być niekompletna i zakończone asynchronicznie.
204  | Powodzenie, ale bez treści odpowiedzi.
301  | Trwałe przekierowanie.
302  | Przekierowanie tymczasowe.
400  | Parametry w adresie URL lub w treści żądania są nieprawidłowe.
401  | Podane poświadczenia są nieprawidłowe.
403  | Akcja jest niedozwolona, biorąc pod uwagę podanych poświadczeń.
404  | Żądany zasób nie istnieje.
409  | Konflikty żądań z istniejącego zasobu.
500  | Usługa napotkał nieoczekiwany błąd.
503  | Usługa jest tymczasowo niedostępna.

Wszelkie `GET` żądania wysłanego do punktu końcowego interfejsu API może zwrócić przekierowania HTTP (301 lub 302). Klienci bez problemu zmieniała powinna obsługiwać takie przekierowuje obserwując `Location` nagłówka i wydawanie kolejnej `GET`. Dokumentację dotyczącą określonych punktów końcowych nie zostanie jawnie wywołać się, których można użyć przekierowania.

W przypadku został zwrócony kod stanu 500 poziomu klienta można zaimplementować mechanizm ponawiania prób uzasadnione. Oficjalna NuGet klienta ponowne próby trzy razy, gdy wystąpią, kod stanu 500 poziomie dowolnej błąd TCP/DNS.

## <a name="http-request-headers"></a>Nagłówki żądania HTTP

Nazwa                     | Opis
------------------------ | -----------
X-NuGet-ApiKey           | Wymaganych na potrzeby wypychania i usuwania, zobacz [ `PackagePublish` zasobów](package-publish-resource.md)
X-NuGet-Client-Version   | **Przestarzałe** i zastąpione przez `X-NuGet-Protocol-Version`
X-NuGet-Protocol-Version | W niektórych przypadkach wymagane tylko w witrynie nuget.org, zobacz [protokoły nuget.org](NuGet-Protocols.md)
X-NuGet-Session-Id       | *Opcjonalnie*. NuGet klientów v4.7 na + identyfikowania żądań HTTP, które są częścią tej samej sesji klienta NuGet. Aby uzyskać `PackageReference` operacji przywracania nie jest identyfikatorem jednej sesji w innych scenariuszach, takich jak Autouzupełnianie, i `packages.config` przywracania może istnieć kilka różnych sesji identyfikatory z powodu jak kod jest brana pod uwagę.

## <a name="authentication"></a>Uwierzytelnianie

Uwierzytelnianie jest dużym implementację źródła pakietu do definiowania. Dla nuget.org tylko `PackagePublish` zasób wymaga uwierzytelnienia za pomocą specjalnych nagłówków klucza interfejsu API. Zobacz [ `PackagePublish` zasobów](package-publish-resource.md) Aby uzyskać szczegółowe informacje.
