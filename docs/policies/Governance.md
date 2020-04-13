---
title: Zarządzanie projektami NuGet
description: Model nadzoru dla NuGet, w tym role i obowiązki dla committers, współautorów i użytkowników.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 2aaaf41b3fc4ef3621333e5099780b5d7ef393bc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "64500395"
---
# <a name="nuget-governance"></a>Zarządzanie uciążliwością

> Dokument ten jest oparty na [dobroczynnym modelu rządzenia dyktatorem](http://www.oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel) przez Uniwersytet Oksfordzki. Jest licencjonowany na licencji [Creative Commons Uznanie autorstwa-ShareAlike 2.0 UK: England & Wales License](http://creativecommons.org/licenses/by-sa/2.0/uk/).

Projekt NuGet jest prowadzony przez życzliwego dyktatora i zarządzany przez społeczność. Oznacza to, że społeczność aktywnie przyczynia się do codziennego utrzymania projektu, ale ogólna linia strategiczna jest rysowana przez życzliwego dyktatora. W przypadku braku porozumienia życzliwy dyktator ma ostatnie słowo.

Zadaniem życzliwego dyktatora jest rozwiązywanie sporów wewnątrz społeczności i zapewnienie, że projekt jest w stanie rozwijać się w skoordynowany sposób. Z kolei zadaniem społeczności jest kierowanie decyzjami życzliwego dyktatora poprzez aktywne zaangażowanie i wkład.

## <a name="roles-and-responsibilities"></a>Role i obowiązki

Istnieją cztery role opisane tutaj: Życzliwy dyktator, committers, współpracowników i użytkowników.

### <a name="benevolent-dictator"></a>Życzliwy dyktator

Podstawowy zespół NuGet jest samozwańczy jako życzliwy dyktator lub kierownik projektu. Jednakże, ponieważ społeczność zawsze ma możliwość rozwidlić, zespół jest w pełni odpowiedzialny przed społecznością. Oczekuje się, że prowadzący projekt zrozumie całą społeczność i będzie dążyć do zaspokojenia jak największej liczby sprzecznych potrzeb, przy jednoczesnym zapewnieniu, że projekt przetrwa w dłuższej perspektywie.

Pod wieloma względami rola życzliwego dyktatora polega w mniejszym stopniu na dyktaturze, a bardziej na dyplomacji. Kluczem jest zapewnienie, że w miarę rozwoju projektu, odpowiednie osoby mają wpływ na niego i społeczności zbiera się za wizją lidera projektu. Zadaniem potencjalnego klienta jest następnie zapewnienie, że osoby zobowiązujące (patrz poniżej) podejmują właściwe decyzje w imieniu projektu. Ogólnie rzecz biorąc, tak długo, jak committers są zgodne ze strategią projektu, kierownik projektu pozwoli im postępować zgodnie z ich życzeniem.

Ponadto pracownicy fundacji .NET uważają, że projekt jest głównym lub pierwszym punktem kontaktowym dla nugeta na potrzeby operacji biznesowych, w tym rejestracji domen i usług technicznych (np. podpisywania kodu).

### <a name="committers"></a>Zrzeszacze

Committers są współpracownikami, którzy wnieśli trwały cenny wkład do NuGet i są mianowani przez życzliwego dyktatora. Po wyznaczeniu, committers są powoływane zarówno napisać kod bezpośrednio do repozytorium i ekran składek innych. Committers są często deweloperzy, ale może przyczynić się w inny sposób.

Zazwyczaj committer koncentruje się na konkretnym aspekcie projektu i wnosi poziom wiedzy i zrozumienia, który przynosi im szacunek społeczności i lidera projektu. Rola committer nie jest oficjalna, to po prostu stanowisko, które wpływowi członkowie społeczności zakładają, jak prowadzić projekt patrzy na nich wskazówek i wsparcia.

Committers nie mają uprawnień, gdzie ogólny kierunek NuGet dotyczy. Jednak mają ucho lidera projektu. Zadaniem osoby zobowiązującej jest dbanie o to, aby potencjalny klient był świadomy potrzeb i wspólnych celów społeczności, a także pomagać w opracowywaniu lub wywoływaniu odpowiedniego wkładu w projekt. Często committers otrzymują nieformalną kontrolę nad ich określonych obszarach odpowiedzialności i są przypisane prawa do bezpośredniego modyfikowania niektórych obszarów kodu źródłowego. Oznacza to, że chociaż committers nie mają wyraźnego uprawnienia decyzyjnego, często stwierdzają, że ich działania są synonimem decyzji podejmowanych przez lidera.

### <a name="contributors"></a>Współautorzy

Współautorzy są członkami społeczności, którzy przesyłają poprawki do NuGet. Te poprawki mogą być jednorazowym wystąpieniem lub wystąpić w czasie. Oczekuje się, że współautorzy przesyłają poprawki, które są małe na początku i powiększają się, gdy współautor, osoby zatwierdzacze i potencjalny klient projektu zbudowali zaufanie do jakości poprawek współautora. Współautorzy są rozpoznawani w skojarzonym dokumencie informacji o wersji produktu.

Zanim pierwsza poprawka współautora zostanie umieszczona w repozytorium, musi podpisać [umowę licencyjną współautora](http://en.wikipedia.org/wiki/Contributor_License_Agreement) lub umowę cesji do platformy .NET Foundation. Łatka może być przesłana i omówiona, ale w rzeczywistości nie może być zaangażowana w repozytorium bez odpowiedniej dokumentacji. Aby uzyskać umowę licencyjną współautora, wyślij [contributions@nuget.org](mailto:contributions@nuget.org)prośbę w wiadomości e-mail na adres .

Aby zostać współautorem, prześlij żądanie ściągnięcia do jednego z następujących repozytoriów:

- [Klient NuGet](https://github.com/NuGet/NuGet.Client)
- [Galeria NuGet](https://github.com/nuget/nugetgallery)
- [Dokumenty NuGet](https://github.com/nuget/nugetdocs)

Szczegółowy proces przesyłania żądania ściągnięcia różni się w zależności od repozytorium:

- [Instrukcje dotyczące wkładu dla klienta NuGet i galerii NuGet](https://github.com/NuGet/Home/wiki/Contributing-to-NuGet)
- [Instrukcje dotyczące wkładu dla NuGet Docs](https://github.com/NuGet/NuGetDocs/wiki/Contributing-to-NuGet-Documentation)

### <a name="users"></a>Użytkownicy

Użytkownicy są członkami społeczności, którzy potrzebują i używają NuGet, jako konsumentów pakietów i/lub autorów. Użytkownicy są najważniejszymi członkami społeczności: bez nich projekt nie miałby żadnego celu. Każdy może być użytkownikiem; nie ma żadnych szczególnych wymagań.

Użytkownicy powinni być zachęcani do udziału w życiu NuGet i społeczności jak najwięcej. Wkład użytkowników umożliwia zespołowi projektowego upewnienie się, że zaspokaja potrzeby tych użytkowników. Typowe działania użytkownika obejmują między innymi następujące czynności:

- Popieranie wykorzystania projektu
- Informowanie twórców o mocnych i słabych stronach projektu z perspektywy nowego użytkownika
- Zapewnienie wsparcia moralnego (dziękuję przechodzi długą drogę)
- Pisanie dokumentacji i samouczków
- Zgłaszanie raportów o błędach i żądań funkcji
- Uczestnictwo w wydarzeniach społecznościowych, takich jak błędy
- Udział w forach dyskusyjnych lub forach

Użytkownicy, którzy nadal angażują się w projekt i jego społeczność, często stają się coraz bardziej zaangażowani. Tacy użytkownicy mogą następnie stać się współautorami, jak opisano powyżej.

## <a name="package-succession-under-special-circumstances"></a>Dziedziczenie pakietów w szczególnych okolicznościach

W niefortunnej sytuacji, gdy posiadacz konta NuGet jest ubezwłasnowolniony lub zmarły, będziemy współpracować ze społecznością, aby dodać odpowiedniego właściciela / s do pakietu, w którym wspomniane konto ma wyłączną własność, a pakiet jest publikowany na [licencji zatwierdzonej](https://opensource.org/licenses/alphabetical)przez OSI. Aby zażądać własności, należy przesłać nam następujące dokumenty:

1. Kserokopia doładowego do zdjęcia wydanego przez rząd.
1. Jeden z następujących dokumentów potwierdzających status poprzedniego posiadacza konta: 
    - Urzędowy, wydany przez rząd akt zgonu, jeżeli poprzedni posiadacz konta nie żyje, lub,
    - Poświadczony dokument, taki jak zaświadczenie podpisane przez lekarza odpowiedzialnego za opiekę nad posiadaczem konta niezdolnego do pracy.
1. Jeden z następujących dokumentów potwierdzających prawo własności: 
    - Akt małżeństwa wskazujący, że jesteś żyjącym współmałżonkiem posiadacza rachunku,
    - Podpisane pełnomocnictwo,
    - Kopia dokumentu woli lub zaufania, nazywając Cię wykonawcą lub beneficjentem,
    - Akt urodzenia posiadacza konta, jeśli jesteś jego rodzicem, lub
    - Dokumenty opiekuńcza, jeśli jesteś prawnym opiekunem właściciela konta.

Jeśli potrzebujesz powołania się na te zasady, wyślij [support@nuget.org](mailto:support@nuget.org) do nas wiadomość e-mail z identyfikatorem i wersją pakietu.

## <a name="transparency"></a>Przezroczystość

Budowanie zaufania społeczności do zarządzania projektem open source ma kluczowe znaczenie dla jego sukcesu. W tym celu proces podejmowania decyzji musi odbywać się w sposób przejrzysty i otwarty. Dyskusja na temat kierunku projektu musi być emidacją do publicznej wiadomości. Społeczność nigdy nie powinna być złapana na gorącym uczynku przez decyzję życzliwego dyktatora. Ponadto dyskusja na temat decyzji dotyczących projektu musi zostać zarchiwizowana, aby członkowie społeczności mogli zrozumieć całą historię decyzji i jej kontekst.
