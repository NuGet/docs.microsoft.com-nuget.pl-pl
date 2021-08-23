---
title: Przestarzałe pakiety na nuget.org
description: Szczegółowy opis procesu oznaczania pakietów jako przestarzałych i sposobu, w jaki klienci pokazują te informacje
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 4a6dbd645cb72b0085fd0347def58ade134fc5ee
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726967"
---
# <a name="deprecating-packages"></a>Przestarzałe pakiety

Jeśli pakiet nie jest już utrzymywany lub chcesz zachęcić użytkowników pakietu do przeniesienia go do innego pakietu, możesz go wycofać. 

Cofanieprepacji pakietu różni się od **cofania jego** listy, jak wyjaśniono poniżej:
* **Wycofanie pakietu z listy** zapobiega jego odnajdywaniu, ponieważ jest ukryty w wynikach wyszukiwania. 
* **Wycofanie pakietu** pozwala istniejącym użytkownikom pakietu dowiedzieć się, czy został on zainstalowany lub używany w swoich projektach. Informuje również o przyczynach cofania i alternatywnym zalecanym pakiecie określonym przez użytkownika (wydawcę pakietu). Oznaczanie pakietu jako przestarzałego nie powoduje jego unlistowania. 

Jako wydawca możesz zarówno wyebrać, jak i wycofać pakiety.

## <a name="deprecation-workflow"></a>Przepływ pracy w celu cofania obsługi
1. Aby wycofać pakiet, przejdź do opcji **Zarządzaj pakietami** i wybierz pozycję **Wycofaj:**

    ![Przejdź do opcji przestarzałego pakietu](media/deprecation-select-option.png)

2. Wybierz wersję, która ma być przestarzała. Jeśli chcesz wycofać całą wersję, wybierz **opcję Wybierz wszystkie** wersje.

    ![Wybieranie wersji pakietu do wycofania](media/deprecation-select-version.png)

3. Wybierz przyczynę cofania pracy. Jeśli pakiet nie jest już utrzymywany, wybierz opcję **Starsza** wersja. Jeśli w określonej wersji znajduje się błąd krytyczny, wybierz opcję **ma krytyczne usterki.** Z dowolnej innej przyczyny wybierz pozycję **Inne.** Zawsze możesz określić alternatywny zalecany pakiet (i wersję) i niestandardowy komunikat do właścicieli. 

    ![Wybieranie przyczyn alternatywnego zalecenia dotyczącego pakietu i niestandardowego komunikatu](media/deprecation-save.png)

> [!Note]
> Komunikat niestandardowy jest wyświetlany tylko na nuget.org ale nie z klientów. Obecnie klienci, tacy `dotnet.exe` jak i NuGet Menedżer pakietów, nie pokazują niestandardowego komunikatu.

## <a name="client-experience-for-deprecated-packages"></a>Środowisko klienta dla przestarzałych pakietów
Po wycofanym pakiecie odbiorcy są o nim powiadamiani w następujący sposób (w zależności od używanego klienta).

### <a name="visual-studio"></a>Visual Studio 
*Dostępne od Visual Studio 2019 r. w wersji 16.3*

Visual Studio ostrzega o użyciu przestarzałego pakietu na `Installed` karcie . Spowoduje to wyświetlanie ostrzeżenia dla pakietu i informacji o jego wycofaniu (w tym przyczyny jego przestarzałości i alternatywnego pakietu do użycia, jeśli jest obecny).

   ![Przestarzałe pakiety na Visual Studio zainstalowanej karty Menedżera pakietów](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet.exe
*Dostępne od zestawu .NET SDK 3.0*

Jeśli używasz dotnet.exe, możesz uruchomić polecenie w folderze rozwiązania lub projektu, aby uzyskać listę przestarzałych pakietów wraz z informacjami o `dotnet list package --deprecated` wycofaniu:

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```

## <a name="transfer-popularity-to-a-newer-package"></a>Przenoszenie popularności do nowszego pakietu

Autorzy pakietów, którzy wycofali starszy pakiet, mogą zdecydować się na przeniesienie jego "popularności" do nowszego pakietu w celu zwiększenia klasyfikacji wyszukiwania nowszego pakietu. Ułatwia to klientom odnajdywanie nowszego pakietu zamiast przestarzałego pakietu.

Załóżmy na przykład, że mam dwa pakiety:

* Mój przestarzały pakiet ze starszymi wersjami z `Contoso.Legacy` 3 milionami pobrań
* Mój najnowszy pakiet z `Contoso.Latest` 5 plikami do pobrania

NuGet.org preferuje wyniki wyszukiwania o wyższych pobraniach/popularności. Biorąc pod uwagę zapytanie wyszukiwania "Contoso", mój przestarzały pakiet prawdopodobnie będzie miał klasyfikację powyżej mojego najnowszego `Contoso.Legacy` pakietu `Contoso.Latest` w wynikach wyszukiwania.

Aby rozwiązać ten problem, mogę zastosować przeniesienie popularności mojego przestarzałego starszego pakietu do mojego najnowszego pakietu. Spowoduje to `Contoso.Latest` wyższą rangę w wynikach wyszukiwania, a `Contoso.Legacy` klasyfikację niższą. Ma to wpływ tylko na wewnętrzne oceny popularności pakietów. Nie wpłynie to na rzeczywistą liczbę pobierania dla każdego pakietu.

> [!Note]
> Transfery popularności mogą znacznie utrudnić klientom znalezienie starszego pakietu.

Zobacz tabelę poniżej, aby dowiedzieć się, jak transfer popularności może wpływać na rankingi wyszukiwania dla zapytania "Contoso":

| Klasyfikacja wyszukiwania    | Przed przeniesieniem popularności        | Po przeniesieniu popularności         |
|----------------   |--------------------------------   |--------------------------------   |
| 1                 | *Contoso.Legacy, pliki do pobrania: 3 mln*    | *Contoso.Latest, 5 plików do pobrania*     |
| 2                 | Contoso.Scanner, pliki do pobrania 2 mln     | Contoso.Scanner, pliki do pobrania 2 mln     |
| 3                 | Contoso.Core, pliki do pobrania w 1,5 mln     | Contoso.Core, pliki do pobrania w 1,5 mln     |
| 4                 | Pliki do pobrania contoso.UI, 1 mln          | Pliki do pobrania contoso.UI, 1 mln          |
| ...               | ...                               | ...                               |
| 20                | *Contoso.Latest, 5 plików do pobrania*     | *Contoso.Legacy, pliki do pobrania: 3 mln*    |

### <a name="popularity-transfer-application-process"></a>Proces aplikacji do transferu popularności

1. Przejrzyj wymagania [dotyczące transferu popularności](#popularity-transfer-requirements).
2. Wyślij wiadomość e-mail z przestarzałym pakietem, którego popularność powinna zostać przeniesiona, oraz listę stabilnych pakietów, które powinny otrzymać [account@nuget.org](mailto:account@nuget.org) transfer popularności.

Po przesłaniu aplikacji powiadomimy Cię o zaakceptowaniu lub odrzuceniu aplikacji (z kryteriami, które spowodowały odrzucenie). Może być konieczne zadawanie dodatkowych pytań identyfikacyjnych w celu potwierdzenia tożsamości właściciela.

#### <a name="popularity-transfer-requirements"></a>Wymagania dotyczące transferu popularności

* Starsze pakiety i nowe pakiety muszą współdzielić wszystkich właścicieli.
* Nowe pakiety muszą być wyraźnie powiązane ze starszymi pakietami w nazewnictwa i funkcji (tj. ewolucji lub nowej generacji).
* Wszystkie wersje starszych pakietów muszą być przestarzałe i wskazują nowe pakiety odbierające transfer.
* Transfer popularności nie może powodować dezorientacji NuGet użytkowników ani nie NuGet wyszukiwania.
* Nowe pakiety muszą mieć stabilną wersję.
* Starszy pakiet nie może odbierać transferów popularności z innego przestarzałego pakietu.

### <a name="advanced-popularity-transfer-scenarios"></a>Zaawansowane scenariusze transferu popularności

#### <a name="package-consolidations"></a>Konsolidacje pakietów

Mogę przenieść popularność wielu przestarzałych pakietów na rzecz jednego nowego pakietu. Załóżmy na przykład, że mam 3 pakiety:

* Mój pierwszy przestarzały starszy pakiet `Contoso.Legacy1`
* Mój drugi przestarzały, starszy pakiet `Contoso.Legacy2`
* Mój nowy skonsolidowany pakiet `Contoso.Latest`

Po wycofaniu i mogę złożyć wniosek o `Contoso.Legacy1` przeniesienie ich popularności na `Contoso.Legacy2` `Contoso.Latest` .

#### <a name="package-splits"></a>Podziały pakietów

Popularność przestarzałego pakietu można przenieść do maksymalnie 5 nowych pakietów i podzielić na nie. Jest to przydatne, jeśli funkcjonalność przestarzałego pakietu została podzielona między wiele nowych pakietów. Załóżmy na przykład, że mam 3 pakiety:

* Mój przestarzały pakiet, `Contoso.Legacy`
* Mój pierwszy nowy pakiet `Contoso.Web`
* Mój drugi nowy pakiet `Contoso.Cloud`

`Contoso.Legacy` Obejmuje funkcje internetowe i w chmurze, ale zdecydowałem się rozdzielić te funkcje na różne pakiety na następną generację. Po wycofaniu funkcji można złożyć wniosek o `Contoso.Legacy` przeniesienie jego popularności na `Contoso.Web` zarówno, jak i `Contoso.Cloud` .

> [!Warning]
> Przeniesiona popularność zostanie podzielona równomiernie między wszystkie nowe pakiety. W związku z tym zalecamy przeniesienie popularności przestarzałego pakietu do jak najrzadziej.

#### <a name="popularity-transfer-chains"></a>Łańcuchy transferu popularności

Przestarzały pakiet nie może przenieść popularności, jeśli już otrzymuje popularność z innego przestarzałego pakietu. Załóżmy na przykład, że mam 3 pakiety:

* Mój przestarzały pakiet, `Contoso.First`
* Mój przestarzały pakiet, `Contoso.Second`
* Mój nowy pakiet, `Contoso.Latest`

Jeśli `Contoso.First` popularność zostanie przesłana do , `Contoso.Second,` `Contoso.Second` wówczas nie będzie można przenieść popularności na . `Contoso.Latest` Zamiast tego zalecamy przeniesienie popularności obu tych pakietów do `Contoso.First` `Contoso.Second` , zgodnie ze `Contoso.Latest` [scenariuszem konsolidacji](#package-consolidations) pakietów.
