---
ms.openlocfilehash: 585537c5e3c7b27e0c7c312db19723d952421ce3
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859573"
---
Żaden udział nie jest zbyt duży lub za mały.

1. Odwiedź stronę, aby edytować [docs.Microsoft.com/NuGet](https://docs.microsoft.com/nuget/), a następnie kliknij przycisk **Edytuj** w prawym górnym rogu. Spowoduje to przeniesienie do odpowiedniej strony z promocji w repozytorium.
1. Edytuj promocji:
    1. Jeśli używasz obrazów (PNGs, ogólnie), umieść je w folderze Media, który znajduje się w folderze tematu. Linki są następnie `media/<image_name>.png` .
    1. Linki względne do innych stron w tym zestawie dokumentów powinny mieć postać `../<folder>/<topic-file>.md` obejmującą szkolenie `.md` . Jeśli łączysz się z innym tematem w tym samym folderze, `../<folder>/` można je pominąć. W przypadku korzystania z kotwic zawsze pamiętaj o uwzględnieniu `.md` przed `#` .
    1. W przypadku korzystania z linków zewnętrznych, w szczególności do docs.microsoft.com (lub msdn.microsoft.com dla dowolnej starszej zawartości), Pomiń wszystkie znaczniki języka, takie jak "en-us", aby czytelnik w innym języku był używany na stronie docelowej w tym samym języku, jeśli jest dostępny.
1. Gdy skończysz, wprowadź poniżej komunikat dotyczący zatwierdzenia, a następnie kliknij pozycję **Zaproponuj zmianę pliku**.
1. Wyślij żądanie ściągnięcia dla zmiany. Regularnie przeglądamy żądań ściągnięcia.
1. Dziękujemy!

W przypadku tworzenia nowego tematu należy również pamiętać o następujących kwestiach:

1. Zawsze umieszczaj nowy temat w odpowiednim podfolderze i postępuj zgodnie z konwencjami dotyczącymi nazw plików, ponieważ są one używane w tym miejscu.
1. Musisz dołączyć blok metadanych, jak widać w innych tematach. Typowe wartości domyślne (takie jak MS. obciążenia i MS. Reviewer) są ustawiane w ramach okna docs/docjx.js, więc należy zmienić tylko następujące elementy:

  - title: tytuł wyświetlany w wynikach wyszukiwania. W przypadku funkcji optymalizacji idealne rozwiązanie nie jest takie samo jak numer najwyższego poziomu (H1) artykułu.
  - Opis: streszczenie artykułu, które pojawia się w wynikach wyszukiwania.
  - Autor: Identyfikator GitHub autora, do którego są przypisane pliki problemów w tym artykule.
  - MS. Author: Jeśli autorem jest pracownik firmy Microsoft, jest to alias firmy Microsoft. Służy do raportowania i przekazywania opinii z innych kanałów.
  - Menedżer: alias Microsoft kierownika autora, jeśli ma zastosowanie.
  - MS. Date: Data ostatniej poprawki lub przeglądu artykułu w formacie mm/dd/rrrr (używaj wiodących zer). Jest to komunikacja z czytelnikem na temat aktualności, dlatego nie jest aktualizowana pod kątem drobnych zmian, tylko w przypadku bardziej znaczących poprawek lub w przypadku, gdy nie ma żadnych zmian.
  - MS. temat: służy do kategoryzowania artykułu w raportach. Zobacz poniższą tabelę. Większość artykułów to "koncepcyjne". 
1. Oprócz dodawania strony, edytuj dokumenty/TOC. MD, aby dodać łącze do tej strony.
1. Jeśli dodajesz węzeł najwyższego poziomu do spisu treści, Utwórz również wpis dla niego w witrynie docs/index. MD.

| Kategoria MS. temat | Opis |
| --- | --- |
| związane | Użyj dla dowolnej zawartości, która nie należy do innej. Ta wartość jest ustawiana jako wartość domyślna w docfx.js. |
| overview | Skorzystaj z dowolnego omówienia lub artykułów z przewodnikiem użytkownika, zwykle tylko tych, które znajdują się w węźle "przegląd" w spisie treści. |
| Start | Wszystko w węźle "Szybki Start" w spisie treści, który jest tworzony zgodnie z wytycznymi szybkiego startu. |
| samouczek | Wszystko w węźle "samouczek" w spisie treści, który jest tworzony zgodnie z instrukcjami samouczka. |
| reference | Dowolny artykuł typu referencyjnego, który nie został wygenerowany automatycznie. |
| artykuł | Używane dla zawartości pochodzącej z społeczności (to oznacza coś spoza zespołu inżynierów lub działu docs w firmie Microsoft. |
