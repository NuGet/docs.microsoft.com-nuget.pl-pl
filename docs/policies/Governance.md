---
title: Zarządzanie projektem NuGet
description: Model ładu dla programu NuGet, w tym role i obowiązki dla twórców, współautorów i użytkowników.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 2edaac0218dc936ea6bfe1814c0aab963028ea87
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775586"
---
# <a name="nuget-governance"></a>Zarządzanie pakietem NuGet

> Ten dokument jest oparty na [modelu ładu Benevolent Dictator](http://www.oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel) przez Uniwersytet Oxford. Jest on licencjonowany w ramach [creative commons attribution Attribution-ShareAlike 2,0 UK: anglia & licencji na Walia](http://creativecommons.org/licenses/by-sa/2.0/uk/).

Projekt NuGet jest kierowany przez Benevolent Dictator i zarządzany przez społeczność. Oznacza to, że społeczność aktywnie uczestniczy w codziennym obsłudze projektu, ale Ogólna linia strategiczna jest rysowana przez Benevolent Dictator. W przypadku braku umowy Benevolent Dictator ma ostatni wyraz.

Jest to zadanie Benevolent Dictator w celu rozwiązania sporów w społeczności i zapewnienia, że projekt jest w sposób skoordynowany. Z kolei jest to zadanie społecznościowe, które ułatwiają podejmowanie decyzji dotyczących Benevolent Dictator w ramach aktywnego zaangażowania i udziału.

## <a name="roles-and-responsibilities"></a>Role i obowiązki

Poniżej opisano cztery role: Benevolent Dictator, osoby zatwierdzające, współautorzy i użytkownicy.

### <a name="benevolent-dictator"></a>Benevolent dictator

Główny zespół NuGet jest samopowoływany jako Benevolent Dictator lub potencjalny lider projektu. Jednak ze względu na to, że społeczność ma zawsze możliwość rozwidlenia, zespół jest w pełni odpowiadać społeczności. Potencjalny klient projektu powinien zrozumieć społeczność jako całość i dążyć do zaspokojenia możliwie największej liczby konfliktów, a jednocześnie zagwarantowania, że projekt przeżyje w długim okresie.

Na wiele sposobów rola Benevolent Dictator jest niższa dla dictatorship i więcej informacji na temat Diplomacy. Kluczem jest upewnienie się, że w miarę rozwijania projektu odpowiednie osoby mają wpływ na dział IT, a społeczność rallies za wizję liderów projektu. Zadanie potencjalnego klienta polega na zapewnieniu, że osoby zatwierdzające (patrz poniżej) podejmują właściwe decyzje w imieniu projektu. Ogólnie mówiąc, tak długo, jak osoby zatwierdzające są wyrównane z strategią projektu, potencjalni klienci projektu umożliwią im dalsze działanie.

Ponadto pracownicy platformy .NET Foundation uważają, że ten projekt prowadzi do głównego lub pierwszego punktu kontaktu dla programu NuGet w celach operacyjnych, takich jak rejestracje domen i usługi techniczne (np. podpisywanie kodu).

### <a name="committers"></a>Współtwórców

Osoby zatwierdzające to Współautorzy, którzy wykonali cenne udziały w NuGet i są mianowani przez Benevolent Dictator. Po wyznaczeniu, osoby zatwierdzające są zaangażowane w zarówno zapis kodu do repozytorium, jak i na ekranie. Twórcy są często deweloperami, ale mogą współtworzyć w inny sposób.

Zazwyczaj osoba przekazująca koncentruje się na konkretnym aspekcie projektu i udostępnia poziom wiedzy i zrozumienie, że uzyskuje je w związku ze społecznością i potencjalnym liderem projektu. Rola osoby zatwierdzającej nie jest oficjalna, to po prostu pozycja, która ma wpływ na członków społeczności przyjętych przez lidera projektu, aby uzyskać wskazówki i pomoc techniczną.

Program zatwierdzający nie ma żadnego urzędu, w którym znajduje się ogólny kierunek NuGet. Jednak są one dostępne na uszach lidera projektu. Jest to zadanie osoby zatwierdzającej, aby zapewnić, że potencjalny klient ma świadomość potrzeb Wspólnoty i celów zbiorowych oraz aby pomóc w opracowywaniu lub wytworzeniu odpowiednich wkładów do projektu. Często program zatwierdzający ma nieformalną kontrolę nad ich szczególnymi zakresami odpowiedzialności i ma przypisane prawa do bezpośredniego modyfikowania niektórych obszarów kodu źródłowego. Oznacza to, że chociaż osoby dokonujące wyboru nie mają jawnego urzędu decyzyjnego, często będą uważali, że ich działania są równoznaczne z decyzjami podjętymi przez lidera.

### <a name="contributors"></a>Współautorzy

Współautorzy są członkami społeczności, którzy przesyłają poprawki do narzędzia NuGet. Te poprawki mogą być wystąpieniem jednorazowym lub występować w czasie. Oczekiwania polegają na tym, że Współautorzy przesyłają w pierwszej kolejności poprawki, które są bardzo małe i zwiększają się, gdy współautor, osoby zatwierdzające i potencjalni klienci projektu mają pewność, że jakość poprawek współautora została skompilowana. Współautorzy są rozpoznawani w dokumencie informacje o wersji skojarzonego produktu.

Przed wprowadzeniem pierwszej poprawki współautora do repozytorium należy podpisać [umowę licencyjną współautora](http://en.wikipedia.org/wiki/Contributor_License_Agreement) lub umowę o przypisaniu do programu .NET Foundation. Poprawkę można przesłać i omówić, ale nie można jej faktycznie przekazać do repozytorium bez odpowiednich Paperwork. Aby uzyskać umowę licencyjną współautora, Wyślij żądanie w wiadomości e-mail na adres [contributions@nuget.org](mailto:contributions@nuget.org) .

Aby stać się współautorem, Prześlij żądanie ściągnięcia do jednego z następujących repozytoriów:

- [Klient NuGet](https://github.com/NuGet/NuGet.Client)
- [Galeria NuGet](https://github.com/nuget/nugetgallery)
- [Dokumenty NuGet](https://github.com/nuget/nugetdocs)

Szczegółowy proces przesyłania żądania ściągnięcia zależy od repozytorium:

- [Instrukcje dotyczące udziału dla klienta NuGet i galerii NuGet](https://github.com/NuGet/Home/wiki/Contributing-to-NuGet)
- [Instrukcje dotyczące udziału dokumentów NuGet](https://github.com/NuGet/NuGetDocs/wiki/Contributing-to-NuGet-Documentation)

### <a name="users"></a>Użytkownicy

Użytkownicy są członkami społeczności, którzy mają potrzebę korzystania z NuGet, jako odbiorców pakietu i/lub autorów. Użytkownicy są najważniejszymi członkami społeczności: bez nich, projekt nie będzie przeznaczenie. Każdy może być użytkownikiem; nie ma określonych wymagań.

Użytkownicy powinni zachęcać do uczestnictwa w życiu programu NuGet i społeczności tak jak to możliwe. Udziały użytkowników umożliwiają zespołowi projektu upewnienie się, że spełniają one potrzeby tych użytkowników. Typowe działania użytkowników obejmują, ale nie są ograniczone do następujących:

- Ambasador dla korzystania z projektu
- Informowanie deweloperów siły projektu i słabości z perspektywy nowego użytkownika
- Zapewnianie pomocy technicznej (Dziękujemy w długim czasie)
- Pisanie dokumentacji i samouczków
- Zgłaszanie raportów usterek i żądań funkcji
- Uczestnictwo w zdarzeniach społeczności, takich jak usterka bashes
- Uczestnictwo w dyskusjach lub forach dyskusyjnych

Użytkownicy, którzy kontynuują zaangażowanie się z projektem i jego społeczność często znajdą się coraz bardziej zaangażowani. Tacy użytkownicy mogą następnie przechodzić do współautorów, jak opisano powyżej.

## <a name="package-succession-under-special-circumstances"></a>Powodzenie pakietu w szczególnych okolicznościach

W sytuacji, gdy posiadacz konta NuGet jest incapacitated lub zakończył działanie, współpracujemy ze społecznością, aby dodać odpowiednich właścicieli/s do pakietu, w którym wymienione konto ma wyłączną własność, a pakiet jest publikowany w ramach [zatwierdzonej licencji na osi](https://opensource.org/licenses/alphabetical). Aby zażądać własności, musisz wysłać nam następujące dokumenty:

1. Fotokopia Twojego identyfikatora zdjęć wystawionego przez rząd.
1. Jeden z następujących dokumentów potwierdza status poprzedniego właściciela konta: 
    - Urzędowy, wydany przez rząd certyfikat zgonu, jeśli poprzedni właściciel konta jest zaprzestał lub
    - Dokument certyfikowany, taki jak certyfikat podpisany przez specjalistę medyczne odpowiedzialny za opiekę właściciela konta incapacitated.
1. Jeden z następujących dokumentów potwierdzających prawo własności: 
    - Certyfikat małżeństwa pokazujący, że jesteś pozostały współmałżonkiem posiadacza konta,
    - Podpisana moc prawnika,
    - Kopia a lub zaufana nazwa dokumentu jako wykonawca lub beneficjenta
    - Certyfikat urodzenia dla właściciela konta, jeśli jesteś ich rodzicem lub,
    - Opiekuna Paperwork, jeśli jesteś prawnym opiekunem właściciela konta.

Jeśli okaże się, że nie musisz wycofać tych zasad, Wyślij do nas wiadomość e-mail [support@nuget.org](mailto:support@nuget.org) z identyfikatorem i wersją pakietu.

## <a name="transparency"></a>Przejrzystość

Tworzenie zaufania społeczności w dziedzinie nadzoru nad projektem typu open source jest istotne dla sukcesu. W tym celu należy podjąć decyzję w przejrzysty, otwarty sposób. Dyskusja o kierunku projektu musi być prowadzona publicznie. Wspólnota nie powinna być nigdy przechwycona jako ochrona przed decyzją Benevolent Dictator. Ponadto należy zarchiwizować dyskusje na temat decyzji projektu, aby członkowie społeczności mogli zrozumieć całą historię decyzji i jej kontekstu.
