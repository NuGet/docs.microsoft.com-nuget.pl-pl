---
title: Zarządzanie NuGet projektu
description: Model ładu NuGet, w tym role i obowiązki committers, współautorzy i użytkowników.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 658901a86b42d6451e41c2c26906a6b6f444faf6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818065"
---
# <a name="nuget-governance"></a>Zarządzanie NuGet

> Ten dokument jest oparty na [dobroczynne modelu ładu Dictator](http://www.oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel) przez University Oxford. Jest objęte [Creative Commons autorstwa ShareAlike 2.0 UK: Anglii & licencji Walia](http://creativecommons.org/licenses/by-sa/2.0/uk/).

Projekt NuGet jest przez dobroczynne Dictator i zarządzane przez społeczność. Oznacza to społeczności aktywnie wspiera codziennej konserwacji projektu, ale ogólne strategicznych wiersza jest rysowany przez dobroczynne dictator. W przypadku niezgodności dobroczynne dictator ma ostatniego wyrazu.

To zadanie dictator dobroczynne rozwiązywanie sporów, w ramach społeczności i upewnij się, że projekt jest w stanie postęp w skoordynowany sposób. Z kolei jest zadania przez społeczność prowadzące decyzje dobroczynne dictator za pośrednictwem aktywnego zaangażowania i udziału.

## <a name="roles-and-responsibilities"></a>Role i obowiązki

Istnieją cztery role opisane tutaj: dobroczynne Dictator, Committers, współautorzy i użytkowników.

### <a name="benevolent-dictator"></a>Dobroczynne dictator

Zespół core NuGet jest własnym wyznaczone jako realizacji dobroczynne Dictator lub projekt. Jednak ponieważ społeczności zawsze ma możliwość rozwidlenia, zespół jest pełni którą można odpowiedzieć społeczności. Realizacji projektu powinien zrozumieć Wspólnoty jako całości i dążyć do zaspokojenia potrzeb wiele powodujące konflikt jak to możliwe, zapewniając, że projekt przeżyje w perspektywie długoterminowej.

Na wiele sposobów rola dobroczynne dictator jest mniejsza o dyktatury i więcej informacji na temat dyplomacji. Klucz jest zapewnienie, że projekt zostanie rozszerzony, odpowiednich osób mających wpływ na jego oraz społeczności rallies za wizji realizacji projektu. Realizacji zadania jest następnie upewnić committers (patrz poniżej) prawidłowych decyzji w imieniu projektu. Ogólnie rzecz biorąc tak długo, jak committers są zgodne z strategii projektu, realizacji projektu umożliwiają postępować według potrzeby.

Ponadto personel .NET Foundation należy wziąć pod uwagę realizacji projektu podstawowego lub pierwszy punkt kontaktu NuGet do celów działalności firmy, w tym rejestracje domeny i obsługę techniczną (np. podpisywania kodu).

### <a name="committers"></a>Committers

Committers są współautorzy, którzy wprowadził utrzymujących wartościowych wpisów NuGet i są wyznaczone przez dobroczynne Dictator. Mianowany committers są stosowane do pisania kodu bezpośrednio do repozytorium i ekranu wkładów innych osób. Committers są często deweloperów, ale może przyczynić się w inny sposób.

Zazwyczaj zatwierdzający koncentruje się na konkretnych aspektów projektu i oferuje poziomu doświadczenie i opis przynosi ich przestrzegania społeczności i realizacji projektu. Rola zatwierdzający nie jest oficjalną, jest po prostu pozycji znaczenie członków społeczności założono, jak wygląda realizacji projektu do nich wskazówki i pomocy technicznej.

Committers mają nie uprawnień, których to dotyczy kierunek NuGet. Jednak mają czyść z realizacji projektu. To zadanie zatwierdzający w celu zapewnienia pamiętać potrzeb i celów zbiorowe przez społeczność potencjalnego klienta, a także aby pomóc rozwijać lub wywołać odpowiednie udziały do projektu. Często committers podano nieformalne kontrolę nad ich określone obszary odpowiedzialności i są przypisane uprawnienia do modyfikowania bezpośrednio niektórych obszarach kodu źródłowego. Oznacza to mimo że committers nie mają uprawnień decyzyjnych jawne, często znajdą synonimem decyzje przez potencjalnego klienta czy ich działania.

### <a name="contributors"></a>Współautorzy

Współautorzy są członkami społeczności, przesyłający poprawek NuGet. Poprawki te mogą być wystąpieniem jednorazowym lub na czas. Oczekiwań są, których współautorzy przesyłać poprawki, które są małe na początku i coraz większe, gdy Współautor committers i realizacji projektu utworzone zaufania jakości poprawki dla współautorów. Współautorzy są rozpoznawane w dokumencie informacje o wersji produktu skojarzone.

Przed wprowadzeniem poprawek pierwszy dla współautorów do repozytorium, należy zarejestrować [umowy licencyjnej współautora](http://en.wikipedia.org/wiki/Contributor_License_Agreement) lub umowę przypisania .NET Foundation. Poprawka mogą być przesłane i opisem, ale faktycznie nie może być przekazane do repozytorium bez odpowiedniej dokumentacji w miejscu. Uzyskanie współautora umowy licencyjnej, Wyślij żądanie w wiadomości e-mail do [ contributions@nuget.org ](mailto:contributions@nuget.org).

Jako współtwórca, należy przesłać żądanie ściągnięcia do jednej z następujących repozytoria:

- [NuGet Client](https://github.com/NuGet/NuGet.Client)
- [Galeria NuGet](https://github.com/nuget/nugetgallery)
- [Dokumentacja NuGet](https://github.com/nuget/nugetdocs)

Szczegółowe proces przesyłania żądania ściągnięcia jest zależna od repozytorium:

- [Instrukcje wkład klienta NuGet i galerii NuGet](https://github.com/NuGet/Home/wiki/Contributing-to-NuGet)
- [Instrukcje wkład NuGet Docs](https://github.com/NuGet/NuGetDocs/wiki/Contributing-to-NuGet-Documentation)

### <a name="users"></a>Użytkownicy

Użytkownicy są członkami społeczności, którzy potrzebują i użycie narzędzia NuGet, jako konsumentów pakietu i/lub autorów. Użytkownicy są najważniejsze członków społeczności: bez obawy, projekt musi bezcelowe. Każda osoba, która może być użytkownika; nie istnieją określone wymagania.

Użytkownicy jest wspierany brać udziału w cyklu życia NuGet i możliwie społeczności. Udziały użytkownika włączyć zespołu projektu upewnić się, że spełniają potrzeby takich użytkowników. Obejmują typowych działań użytkownika, ale nie są ograniczone do następujących:

- Postulować projektu do użytku
- Informuje o dostępności deweloperów o sile projektu i słabe strony z punktu widzenia nowego użytkownika
- Zapewnianie obsługi autorskie (Dziękujemy przejdzie do innych użytkowników)
- Zapisywanie dokumentacja i samouczki
- Składanie raportów usterek i żądania funkcji
- Udział w społeczności zdarzenia, takie jak bashes usterki
- Udział na tablice dyskusyjne i fora

Użytkownicy, którzy współpracować z projektu i jego społeczności w dalszym ciągu będzie często muszą się staje się coraz bardziej zaangażowany. Takie użytkowników może następnie przejdź do stają się współautorzy, zgodnie z powyższym opisem.

## <a name="package-succession-under-special-circumstances"></a>Kolejne pakietu w obszarze specjalne okoliczności

W sytuacji niefortunne, których właścicielem konta NuGet jest unieruchomionych lub zmarły, będzie współpracujemy z społeczności, aby dodać odpowiedni właściciel/s do pakietu, gdy wspomnianej konto ma wyłącznie własność, a pakiet jest opublikowana w obszarze [OSI zatwierdzone licencji](https://opensource.org/licenses/alphabetical). Aby zażądać własność, musisz wysłać nam następujących dokumentach:

1. Fotokopię Twojego identyfikatora fotografii wystawiony dla instytucji rządowych.
1. Jeden z następujących dokumentach potwierdzających poprzedniego właściciela konta: 
    - Certyfikat śmierci urzędnika, wystawiony dla instytucji rządowych, jeśli poprzednie właścicielem konta jest śmierci, lub,
    - Certyfikowanych dokument, takich jak certyfikatu podpisanego przez medyczne odpowiedzialnym za opieki posiadacz niezdolny konta.
1. Jeden z następujących dokumentów, co dowodzi prawo własności: 
    - Certyfikatu unieważnienie wskazującego, czy masz poprawny współmałżonka właściciela konta
    - Podpisem power of prawnikiem,
    - Kopię dokumentu zostanie lub relacji zaufania nazewnictwa jako moduł wykonujący lub beneficjent,
    - Certyfikat urodzenia dla właściciela konta, jeśli ich nadrzędnego, lub
    - Opieki dokumentacji w przypadku prawnych ochrona właściciela konta.

Jeśli okaże się, wymaga wywołania tych zasad, Wyślij nam wiadomość e-mail na [ support@nuget.org ](mailto:support@nuget.org) o identyfikatorze i wersję pakietu.

## <a name="transparency"></a>Przezroczystość

Tworzenie zaufania społeczności w zarządzanie projekt typu open source jest niezbędne do jej powodzenie. W tym celu należy w sposób przezroczysty, otwórz podejmowania decyzji. Omówienie projektu kierunek musi odbywać się publicznie. Społeczności nigdy nie powinien podlegać zaskoczyć decyzją przez dobroczynne Dictator. Ponadto omówienie decyzje dotyczące projektu należy zarchiwizować, przez co członków społeczności zrozumiałe dla całej historii decyzji i jego kontekstu.
