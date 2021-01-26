---
title: Informacje o wersji programu NuGet 3,0 beta
description: Informacje o wersji dla programu NuGet 3,0 beta, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7970c3d81c724edc743d7b2d38c4c157237a0271
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776626"
---
# <a name="nuget-30-beta-release-notes"></a>Informacje o wersji programu NuGet 3,0 beta

Informacje o wersji narzędzia [NuGet 3,0 Preview](../release-notes/nuget-3.0-preview.md)  |  [Informacje o wersji narzędzia NuGet 3,0 RC](../release-notes/nuget-3.0-rc.md)

Pakiet NuGet 3,0 beta został zwolniony 23 lutego 2015 dla programu Visual Studio 2015 CTP 6. Ta wersja oznacza, że nasz zespół ma wiele udoskonaleń architektury i wydajności, a firma Microsoft przyjemnością się na rozpoczęcie dostrajania ustawień wydajności usługi nuget.org.

Zdecydowanie zalecamy, aby odinstalować poprzednią wersję rozszerzenia NuGet Visual Studio 2015 przed zainstalowaniem tej nowej wersji.  Jeśli masz problemy z tą wersją rozszerzenia, zalecamy przywrócenie [poprzedniej wersji](http://nuget.codeplex.com/downloads/get/909582) do użycia z programem Visual Studio 2015 Preview.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Ten pakiet NuGet 3,0 beta jest dostępny do zainstalowania w galerii rozszerzeń programu Visual Studio 2015 CTP 6. Pracujemy nad rozpoczęciem korzystania z wersji zapoznawczej dla programu Visual Studio 2012 i Visual Studio 2013 bardzo szybko. Firma Microsoft udostępniła poprzednio zamiar w celu [zaniechania aktualizacji programu Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html)i wybraliśmy tę trudną decyzję.

## <a name="new-clientserver-api"></a>Nowy interfejs API klienta/serwera

Pracujemy nad niektórymi szczegółami implementacji protokołu klient/serwer narzędzia NuGet. Wykonana przez nas czynność polega na utworzeniu interfejsu API v3 dla programu NuGet, który jest przeznaczony dla wysokiej dostępności dla scenariuszy krytycznych, takich jak przywracanie pakietów i instalowanie pakietów. Nowy interfejs API jest oparty na REST i w pozostałej części, a jako nasz format został wybrany [kod JSON-LD](http://json-ld.org) .

W pakiecie NuGet 3,0 beta BITS zobaczysz nowe źródło pakietu o nazwie "api.nuget.org" na liście rozwijanej Źródło pakietu.   W przypadku wybrania tego źródła pakietów zostanie użyty nasz nowy interfejs API, a nie zostanie nawiązane połączenie z usługą nuget.org. W programie NuGet 3,0 RC to nowe źródło pakietów oparte na interfejsie API v3 spowoduje zastąpienie źródła pakietu "nuget.org" opartego na protokole v2.  Zalecamy wyłączenie wszystkich innych publicznych źródeł pakietów i pozostawienie tylko api.nuget.org jako jedynego repozytorium pakietu publicznego.

Oferujemy dużo czasu na kompilowanie interfejsu API v3 i kontynuowanie obsługi standardowego interfejsu API w wersji 2 dla starych klientów próbujących uzyskać dostęp do repozytorium publicznego.

## <a name="updated-ui"></a>Zaktualizowany interfejs użytkownika

W tej wersji Ulepszono interfejs użytkownika w celu uwzględnienia pola kombi, które umożliwi wybranie akcji do wykonania w pakiecie i przejście przycisku podglądu do pola wyboru w obszarze Opcje ekranu.  Obszar opcji nie jest już zwijany i udostępnia teraz łącze pomocy opisujące dostępne opcje.

![Nowy interfejs użytkownika narzędzia NuGet](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>Rejestrowanie operacji

Usunęliśmy okno modalne z informacjami rejestrowania, które mogą być szybko wyświetlane i ukrywane podczas instalowania lub odinstalowywania.  To okno nie dodaliśmy wartości, jeśli naprawdę chcesz zobaczyć informacje lub można je skopiować i wkleić.  Zamiast tego przekierowujemy wszystkie dane wyjściowe rejestrowania do okienka Menedżera pakietów w oknie danych wyjściowych.  Uważamy, że jest to bardziej wygodne i podobne do typowego raportu kompilacji, który chcesz sprawdzić.


### <a name="focus-on-performance"></a>Skup się na wydajności

Wprowadziliśmy wiele zmian w nazwie poprawy wydajności wyszukiwania NuGet i pobierania.  Jest to nasz numer z naszych klientów i chcemy się upewnić, że został on uwzględniony w tej wersji.  Dodaliśmy nasze serwery, opracowano nową sieć CDN i ulepszono logikę dopasowywania zapytania, aby miejmy nadzieję dostarczać bardziej odpowiednie i szybsze wyniki wyszukiwania pakietów.

W ramach tej fazy opracowywania programu NuGet 3,0 będziemy dostrajać i monitorować usługę nuget.org, aby zapewnić lepsze środowisko pracy.  Nie planuje się, aby nie podejmować żadnych przestojów, ale będą dodawać i zmieniać zasoby w usłudze.  Zadbaj [o to, aby uzyskać](http://twitter.com/nuget) szczegółowe informacje na temat zmiany konfiguracji usługi.

## <a name="building-nuget-with-nuget"></a>Kompilowanie NuGet przy użyciu narzędzia NuGet

Teraz możemy ponownie umieścić w architekturze naszych klientów NuGet kilka składników, które są wbudowane w pakiety NuGet. Ta ponowna próba użycia własnych bibliotek zmusza do tworzenia składników, które są ponownie używane, i które mogą zostać prawidłowo spakowane.  Mogliśmy wyeliminować zduplikowany kod i poznać, jak lepiej skonfigurować nasz proces tworzenia oprogramowania, aby obsługiwał potrzebę tworzenia pakietów w naszych rozwiązaniach.  Zapoznaj się z blogiem, aby dowiedzieć się więcej o tym, w jaki sposób projekty kodu są strukturalne i jak działa nasz proces kompilacji.

## <a name="stay-tuned"></a>Bądź na bieżąco

Obserwuj [nasz blog](http://blog.nuget.org) , aby uzyskać więcej informacji na temat postępu i anonsów dla programu NuGet 3,0!
