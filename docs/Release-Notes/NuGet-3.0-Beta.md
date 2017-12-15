---
title: Informacje o wersji Beta NuGet 3.0 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 4153ff3f-f97f-4e54-b638-e844f70edf22
description: "Informacje o wersji programu NuGet 3.0 Beta tym znanych problemów, poprawki, dodatkowe funkcje i dcr."
keywords: NuGet 3.0 Beta informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 46b2a81845f5ac06b8c80975c55fcfc33b86636e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-30-beta-release-notes"></a>Informacje o wersji NuGet 3.0 w wersji Beta

[Informacje o wersji NuGet 3.0 w wersji zapoznawczej](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC informacje o wersji](../release-notes/nuget-3.0-rc.md)

NuGet 3.0 Beta został wydany 23 lutego 2015 w wersji Visual Studio 2015 CTP 6. Ta wersja oznacza, że partia nasz zespół mamy liczba ulepszenia wydajności i architektura do udostępniania, a my się cieszymy do rozpoczęcia strojenia ustawienia wydajności w naszej usługi nuget.org.

Zdecydowanie zaleca się, odinstaluj wszelkie wcześniejsze niż wersja rozszerzenia NuGet programu Visual Studio 2015 przed zainstalowaniem nowej wersji.  Jeśli masz problemy z tą wersją rozszerzenia, zaleca się przywrócenie do [wcześniejsze niż wersja](http://nuget.codeplex.com/downloads/get/909582) do użytku z wersji zapoznawczej programu Visual Studio 2015.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Ta wersja NuGet 3.0 Beta jest dostępny do zainstalowania w programie Visual Studio 2015 CTP 6 galerii rozszerzeń. Pracujemy, aby uzyskać podgląd porzucania dla programu Visual Studio 2012 i Visual Studio 2013 bardzo szybko. Wcześniej poinformowaliśmy naszych zamiarze [przerwanie aktualizacji dla programu Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), i wykonujemy tej decyzji trudne.

## <a name="new-clientserver-api"></a>Nowy klient/serwer interfejsu API

Firma Microsoft już wcześniej Praca niektóre szczegóły implementacji protokołu NuGet klient/serwer. Czynności, które firma Microsoft wykonane jest utworzenie "V3 interfejsu API" programu NuGet, który jest zaprojektowana dla wysokiej dostępności dla scenariuszy o kluczowym znaczeniu, takie jak Przywracanie pakietu i instalowania pakietów. Nowy interfejs API jest oparta na REST i wybranych hipermedialnych i my [JSON-LD](http://json-ld.org) jako naszych format zasobów.

W bitach NuGet 3.0 w wersji Beta zostanie wyświetlone nowe źródło pakietów o nazwie "api.nuget.org" w menu rozwijanym źródła pakietu.   W przypadku wybrania tego źródła pakietu, użyjemy naszego nowy interfejs API zamiast do nawiązania połączenia nuget.org. W wersji NuGet 3.0 RC to nowe źródło pakietów na podstawie v3 interfejsu API spowoduje zastąpienie źródła pakietu na podstawie v2 "nuget.org".  Zaleca się wyłączenie wszystkich źródeł publicznych pakietu i pozostaw tylko api.nuget.org Twojego repozytorium pakietów tylko publiczne.

Firma Microsoft zostały poddane tworzenia interfejsach API v3 dużo czasu i będą w dalszym ciągu Obsługa interfejsu API w wersji standard 2 dla klientów starego próbująca dostępu publicznego repozytorium.

## <a name="updated-ui"></a>Zaktualizowany interfejs użytkownika

Firma Microsoft zostały rozszerzone interfejsu użytkownika w tej wersji, aby uwzględnić combobox, będzie można wybrać akcję do wykonania z pakietem i przekształcona przycisk do wyboru w obszarze Opcje ekranu.  Obszar opcji nie jest już zwijanej i udostępnia teraz opisujące dostępne opcje łącza pomocy.

![Nowy interfejs użytkownika NuGet](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>Rejestrowanie operacji

Firma Microsoft usunęła modalne okno z informacje rejestrowania może szybko pojawiają się i Ukryj podczas instalowania lub odinstalowywania.  To okno dodano żadnej wartości podczas czy na pewno chcesz zapoznaj się z informacjami lub być w stanie skopiować i wkleić z niego.  Zamiast tego firma Microsoft są teraz przekierowywanie wszystkie dane wyjściowe rejestrowania w okienku Menedżera pakietów w oknie danych wyjściowych.  Mamy nadzieję, że jest to bardziej wygodne i podobne do raportu typowe kompilacji, który chcesz sprawdzić.


### <a name="focus-on-performance"></a>Skupić się na wydajności

Wprowadziliśmy wiele zmian nazwy poprawia wydajność wyszukiwania NuGet i pobiera.  To mamy jednym problemów klientów i możemy aby się upewnić się, że firma Microsoft rozwiązane w tej wersji.  Wprowadzeniu dopasowane nasze serwery wbudowane się nowych CDN i ulepszona zapytania logika miejmy nadzieję, że dostarczyć użytkownikowi dokładniejsze dopasowywania i powoduje szybsze wyszukiwanie pakietu.

Jak możemy kontynuować za pomocą tej fazy rozwoju NuGet 3.0, możemy zostanie dostrajanie i monitorowanie usługi nuget.org, aby upewnić się, że dostarczamy udoskonalone środowisko.  Firma Microsoft nie planowanie do podejmowania żadnych przestojów, ale zostanie Dodawanie i zmiana zasobów w usłudze.  Śledzić na naszych [kanału informacyjnego w usłudze twitter](http://twitter.com/nuget) szczegółowe informacje na temat kiedy możemy zmienić konfigurację usługi.

## <a name="building-nuget-with-nuget"></a>NuGet Building nuget

Mamy teraz rearchitected klienci NuGet do kilka składników, które same są wbudowane w pakietach NuGet. Ponownego użycia własnej bibliotek wymusza firmie Microsoft w celu tworzenia składników, które są wielokrotnego użytku i które można spakować poprawnie.  Byliśmy w stanie wyeliminowania zduplikowanych kodu i uzyskanych lepiej konfigurowania procesu tworzenia trzeba utworzyć pakiety w naszych rozwiązań do obsługi.  Wyszukaj wpis w blogu wkrótce gdzie będą omawianiu struktury projektów kodu i działania procesu kompilacji.

## <a name="stay-tuned"></a>Wkrótce

Można śledzić na [naszym blogu](http://blog.nuget.org) więcej i powiadomień dla NuGet 3.0!
