---
title: Projekt NuGet nadzoru
description: Model nadzoru NuGet, w tym role i obowiązki współtwórców, współautorów i użytkowników.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 2aaaf41b3fc4ef3621333e5099780b5d7ef393bc
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549453"
---
# <a name="nuget-governance"></a>Zarządzanie NuGet

> Ten dokument jest oparty na [dobroczynne modelu nadzoru Dictator](http://www.oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel) przez University Oxford. Jest licencjonowane w ramach [Creative Commons Attribution-ShareAlike 2.0 Zjednoczone Królestwo: Anglii & licencję Walia](http://creativecommons.org/licenses/by-sa/2.0/uk/).

Projekt NuGet jest prowadzone przez dobroczynne Dictator i zarządzane przez społeczność. Oznacza to, że społeczności aktywnie przyczynia się do codziennej konserwacji projektu, ale ogólne strategicznych linia jest rysowana przez dobroczynne dictator. W przypadku niezgodności dobroczynne dictator ma ostatni wyraz.

To zadanie dobroczynne dictator rozstrzygania sporów w społeczności oraz aby upewnić się, że projekt jest w stanie kontynuować w skoordynowany sposób. Z kolei jest zadanie społeczności przeprowadzenie decyzje dobroczynne dictator za pośrednictwem aktywnego zaangażowania i udział.

## <a name="roles-and-responsibilities"></a>Role i obowiązki

Istnieją cztery role opisane w tym miejscu: dobroczynne Dictator, współtwórców, współautorów i użytkowników.

### <a name="benevolent-dictator"></a>Dobroczynne dictator

Zespół core NuGet jest własnym wyznaczone jako potencjalnych klientów dobroczynne Dictator lub projektu. Ponieważ jednak społeczności zawsze ma możliwość rozwidlenia, zespół jest pełni którą można odpowiedzieć społeczności. Kierownik projektu powinna zrozumieć społeczności jako całość i dążyć do zaspokojenia potrzeb wiele powodujących konflikt jak to możliwe, przy jednoczesnym zapewnieniu, że projekt przeżyje w perspektywie długoterminowej.

Na wiele sposobów rolą dobroczynne dictator jest mniej o dyktatury i więcej informacji na temat dyplomacji. Klucz jest zapewnienie, ponieważ projekt jest rozszerzany, odpowiednich osób mających wpływ na jej i społeczności rallies za wizji kierownika projektu. Zadanie potencjalnego klienta jest następnie podejmij właściwe decyzje w imieniu projektu w współtwórców (patrz poniżej). Ogólnie rzecz biorąc tak długo, jak współtwórców są wyrównane z projektu strategii, kierownika projektu pozwala postępować zgodnie z ich działanie.

Ponadto personel .NET Foundation należy wziąć pod uwagę kierownika projektu podstawowego lub pierwszy punkt kontaktu NuGet na potrzeby operacji biznesowych łącznie z rejestracji domeny i obsługę techniczną (np. podpisywania kodu).

### <a name="committers"></a>Współtwórców

Współtwórców są współautorami, którzy przyczyniła stałą przydatne do narzędzia NuGet i są wyznaczone przez dobroczynne Dictator. Mianowany współtwórców są stosowane w celu pisania kodu bezpośrednio do repozytorium i wkłady innym ekranie. Współtwórców często są deweloperów, ale może współtworzyć zawartość w inny sposób.

Zazwyczaj osobą zatwierdzającą koncentruje się na konkretnej kwestii projektu i oferuje poziomu umiejętności i zrozumienie, które zarabiają je w odniesieniu do społeczności i Kierownik projektu. Rola osobą zatwierdzającą nie jest oficjalnym, jest po prostu pozycji wpływowi członkowie społeczności przyjęto założenie, jak wygląda realizacji projektu do nich dla wskazówki i pomoc techniczna.

Współtwórców mają nie uprawnienia, których to dotyczy kierunek NuGet. Jednak mają one wyczyść projekt potencjalnego klienta. To zadanie osobą zatwierdzającą, upewnij się, że potencjalnego klienta pamiętać potrzeb i celów zbiorowe społeczności i rozwijać lub wywołać odpowiednie wkładu do projektu. Często współtwórców otrzymują nieformalne kontrolę nad ich określonych zakres odpowiedzialności i mają przypisanych uprawnień bezpośrednio zmodyfikować niektóre obszary kodu źródłowego. Oznacza to mimo że współtwórców nie mają jawnych uprawnień podejmowania decyzji, często znajdą że ich działania są tożsame z decyzjami przez potencjalnego klienta.

### <a name="contributors"></a>Współautorzy

Współautorzy są członkami społeczności, którzy przesłać poprawki do narzędzia NuGet. Poprawki te mogą być jednorazowe lub zaistniałe w czasie. Oczekiwania są, których współautorzy przesyłać poprawek, które są małe, na początku i powiększać większa podczas Współautor, współtwórców i Kierownik projektu mają zaufania do jakości poprawki współautora. Współautorzy są rozpoznawane w dokumencie informacje o wersji produktu skojarzone.

Przed wprowadzeniem poprawek pierwszy współautora w repozytorium, muszą się zalogować [umowę licencyjną współautora](http://en.wikipedia.org/wiki/Contributor_License_Agreement) lub umowę przypisania .NET Foundation. Poprawki, które mogą być przesłane i omówiono, ale faktycznie nie można zatwierdzić repozytorium bez odpowiedniej dokumentacji w miejscu. Uzyskanie współautorem umowy licencyjnej, Wyślij wniosek w wiadomości e-mail do [ contributions@nuget.org ](mailto:contributions@nuget.org).

Aby zostać współautorem, należy przesłać żądanie ściągnięcia do jednej z następujących repozytoriów:

- [NuGet Client](https://github.com/NuGet/NuGet.Client)
- [Galeria NuGet](https://github.com/nuget/nugetgallery)
- [Dokumentów NuGet](https://github.com/nuget/nugetdocs)

Szczegółowe proces przesyłania żądania ściągnięcia różni się w repozytorium:

- [Instrukcje wkład klienta programu NuGet i galerii pakietów NuGet](https://github.com/NuGet/Home/wiki/Contributing-to-NuGet)
- [Instrukcje wkład do dokumentacji systemu NuGet](https://github.com/NuGet/NuGetDocs/wiki/Contributing-to-NuGet-Documentation)

### <a name="users"></a>Użytkownicy

Użytkownicy są członkami społeczności, którzy potrzebują a przy użyciu pakietów NuGet jako konsumentów pakietu i/lub autorów. Użytkownicy są najważniejsze członkami społeczności: bez nich, projekt musi bezcelowe. Każda osoba może być użytkownikiem; nie istnieją określone wymagania.

Powinno się zachęcać użytkowników do wzięcia udziału w życiu społeczności możliwie i NuGet. Wkład użytkownika umożliwiają zespołu projektu upewnić się, że spełniają one potrzeby tych użytkowników. Typowych działań użytkownika obejmują, ale nie są ograniczone do następujących:

- Promujące do użytku projektu
- Informacją o tym, deweloperzy projektu zalety i słabe strony z punktu widzenia nowego użytkownika
- Zapewnianie obsługi fizyczną (podziękowaniem wykracza to)
- Pisanie dokumentacji i samouczków
- Żądania funkcji i zgłaszania raportów usterek
- Udział w wydarzenia dla społeczności, takich jak bashes usterki
- Uczestnictwa na tablice dyskusyjne i fora

Użytkownicy, którzy w dalszym ciągu korzystaj z projektu i jego społeczności będzie często stawia staje się coraz bardziej zaangażowane. Takich użytkowników może następnie przejdź do stają się współautorów, zgodnie z powyższym opisem.

## <a name="package-succession-under-special-circumstances"></a>Kolejne pakietu w szczególnych okolicznościach

Niefortunne sytuacji, gdy właściciel konta NuGet jest unieruchomionych lub zmarły, firma Microsoft będzie pracować nad do społeczności, aby dodać odpowiednie właściciela/s do pakietu, gdzie wspomniane konto ma jedynego właściciela, a pakiet jest publikowany [OSI zatwierdzone licencji](https://opensource.org/licenses/alphabetical). Aby zażądać własności musi wyślesz do nas następujące dokumenty:

1. Fotokopię swój identyfikator zdjęcia wystawiony dla instytucji rządowych.
1. Jeden z następujących dokumentów potwierdzających poprzedniego właściciela konta: 
    - Certyfikat śmierci urzędnika, wystawiony dla instytucji rządowych, w przypadku poprzedniego właściciela konta zgon, lub
    - Certyfikowane dokument, takich jak certyfikatu podpisanego przez medycznych professional odpowiedzialnym za opieki nad posiadacz konta niemogących odpowiedzieć.
1. Jeden z następujących dokumentów potwierdzających prawa do użytkowania: 
    - Certyfikat małżeństwa przedstawiający czy poprawny współmałżonka właściciela konta
    - Podpisany sądowych of zasilania,
    - Kopię dokumentu będą lub zaufania nazewnictwa jako wykonawca lub beneficjenta,
    - Urodzenia certyfikat dla właściciela konta, jeśli ich nadrzędnego, lub
    - Opieki do niej, jeśli jesteś Opiekun prawny właściciela konta.

Jeśli okaże się, wymagające wywoływanie tych zasad, Wyślij nam wiadomość e-mail na [ support@nuget.org ](mailto:support@nuget.org) o identyfikatorze i wersję pakietu.

## <a name="transparency"></a>Przezroczystości

Tworzenie zaufania społeczności w nadzoru projektu open-source jest jej sukces. W tym celu należy przeprowadzić proces podejmowania decyzji w sposób przezroczysty, Otwórz. Dyskusję na temat kierunku projektu musi odbywać się publicznie. Społeczność nigdy nie powinien zostać przechwycony wyłączona ochrona decyzji przez dobroczynne Dictator. Ponadto dyskusję na temat decyzji dotyczących projektu muszą być archiwizowane, tak aby członkowie społeczności mogą zrozumieć całą historię decyzji i kontekst.
