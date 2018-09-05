---
title: Informacje o wersji programu NuGet w wersji 3.0 Beta
description: Informacje o wersji programu NuGet 3.0 Beta, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9f9fec6a1af8dfbcfdcfa05a301ff52409521228
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550916"
---
# <a name="nuget-30-beta-release-notes"></a>Informacje o wersji programu NuGet w wersji 3.0 Beta

[Informacje o wersji zapoznawczej NuGet 3.0](../release-notes/nuget-3.0-preview.md) | [informacje o wersji programu NuGet 3.0 RC](../release-notes/nuget-3.0-rc.md)

NuGet 3.0 w wersji Beta została wydana 23 lutego 2015 w wersji programu Visual Studio 2015 CTP 6. Ta wersja oznacza znacznie do naszego zespołu oferujemy szereg ulepszeń architektury i wydajność udostępniania i cieszymy w celu rozpoczęcia strojenia ustawienia wydajności w naszej usłudze nuget.org.

Zdecydowanie zaleca się odinstalowanie wszelkie poprzedniej wersji rozszerzenia NuGet programu Visual Studio 2015 przed zainstalowaniem nowej wersji.  Jeśli masz jakiekolwiek problemy z tej wersji rozszerzenia, zaleca się powrócić do [poprzedniej wersji](http://nuget.codeplex.com/downloads/get/909582) do użytku z programem Visual Studio 2015 (wersja zapoznawcza).

## <a name="visual-studio-2012"></a>Visual Studio 2012+

Tej wersji NuGet 3.0 Beta jest dostępny do zainstalowania w programie Visual Studio 2015 CTP 6 galerii rozszerzeń. Pracujemy nad bój spadnie (wersja zapoznawcza) dla programu Visual Studio 2012 i Visual Studio 2013 bardzo szybko. Wcześniej zaprezentowaliśmy naszym zamiarem [przerwanie aktualizacji dla programu Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), i firma Microsoft została wprowadzona trudne decyzji.

## <a name="new-clientserver-api"></a>Nowy klient/serwer interfejsu API

Firma Microsoft pracowano niektórych szczegółów implementacji protokołu klient/serwer NuGet. Dotychczasowej pracy jest utworzenie "Wersji 3 interfejsu API" dla pakietów NuGet zaprojektowany pod kątem wysokiej dostępności dla scenariuszy o kluczowym znaczeniu, takich jak Przywracanie pakietu i instalowania pakietów. Nowy interfejs API jest oparta na REST i wybranych hipermedialnych, a my [JSON-LD](http://json-ld.org) naszych wartość w formacie zasobów.

W bitach NuGet 3.0 w wersji Beta zobaczysz nowe źródło pakietu o nazwie "api.nuget.org" w menu rozwijanym źródła pakietu.   Wybranie tego źródła pakietów, użyjemy naszego nowego interfejsu API zamiast połączyć się z repozytorium nuget.org. W programie NuGet 3.0 RC to nowe źródło pakiet w wersji 3 interfejsu API spowoduje zastąpienie źródła pakietu na podstawie v2 "nuget.org".  Firma Microsoft zaleca się wyłączenie wszystkich źródeł pakietów publicznych i pozostaw tylko api.nuget.org repozytorium pakietów tylko publiczne.

Firma Microsoft została utworzona dużo czasu na tworzenie nasze interfejsy API w wersji 3 i będzie w dalszym ciągu Obsługa interfejsu API v2 standardowa starych klientów zamierzających uzyskać dostępu do repozytorium publicznego.

## <a name="updated-ui"></a>Zaktualizowany interfejs użytkownika

Ulepszyliśmy interfejsu użytkownika w tej wersji do uwzględnienia combobox pozwoli wybrać akcję do wykonania przy użyciu pakietu, która przeszła przycisku (wersja zapoznawcza) do pola wyboru w obszarze Opcje ekranu.  W obszarze opcji nie jest już zwijany i udostępnia teraz zawierająca opis dostępnych opcji łącza pomocy.

![Nowy interfejs użytkownika NuGet](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>Rejestrowanie operacji

Usunęliśmy okno modalne informacje rejestrowania, które pojawiają się szybko i ukrywanie podczas instalowania lub odinstalowywania.  To okno nie usprawniło, gdy czy na pewno chcesz zapoznaj się z informacjami lub mieć możliwość kopiowania i wklejania z niego.  Zamiast tego będziemy są teraz przekierowanie wszystkie dane wyjściowe rejestrowania do okienka Menedżera pakietów w oknie danych wyjściowych.  Uważamy, że jest to bardziej wygodne i podobne do raportu typowe kompilacji, który ma zostać sprawdzony.


### <a name="focus-on-performance"></a>Skup się na wydajności

Wprowadziliśmy wiele zmian nazwę poprawę wydajności wyszukiwania NuGet i odczyty.  Jest to naszym najwyższym kwestią od naszych klientów, a Chcieliśmy aby upewnić się, że firma Microsoft rozwiązanych w tej wersji.  Firma Microsoft została dostosowana naszych serwerów, wbudowane się nowej sieci CDN i ulepszona zapytania dopasowania logikę miejmy nadzieję dostarczy użytkownikowi istotniejsze i wyniki szybciej pakietu wyszukiwania.

Jak firma Microsoft postępowania na tym etapie opracowywania pakietów NuGet 3.0, Rozpoczniemy można dostrajanie i monitorowanie usługi nuget.org, aby upewnić się, że możemy dostarczać udoskonalony interfejs użytkownika.  Firma Microsoft nie planujesz podejmować żadnych przestojów, ale będzie można Dodawanie i zmiana zasoby w usłudze.  Zwracaj uwagę naszych [kanału informacyjnego w usłudze twitter](http://twitter.com/nuget) szczegółowe informacje na temat gdy zmienimy konfiguracji usługi.

## <a name="building-nuget-with-nuget"></a>Tworzenie NuGet z NuGet

Firma Microsoft teraz rearchitected naszym klientom programu NuGet w kilka składników, które znajdują się wbudowywaniu pakietów NuGet. Ponownego użycia naszych bibliotek wymusza nam do tworzenia składników, które są do ponownego użycia i że można spakować prawidłowo.  Byliśmy w stanie wyeliminować zduplikowany kodem i znasz już lepiej konfigurowania naszym procesie tworzenia oprogramowania do obsługi konieczność skompilować pakiety w całym nasze rozwiązania.  Wyszukaj wpis w blogu wkrótce gdzie zostaną omówione struktury projektów kodu, i sposobu działania procesu kompilacji.

## <a name="stay-tuned"></a>Obserwuj na bieżąco

Można nadzorować [naszym blogu](http://blog.nuget.org) więcej postępu i anonsów dla pakietów NuGet 3.0!
