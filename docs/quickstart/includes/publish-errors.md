---
ms.openlocfilehash: b0af2000b1f43cd0b91f2c95dfc0c11540a94cab
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496061"
---
Błędy z `push` polecenia zazwyczaj wskazują na problem. Na przykład może zapomniane, aby zaktualizować numer wersji w projekcie i dlatego próbuje opublikować pakiet, który już istnieje.

Błędy są również widoczne podczas próby opublikowania pakietu przy użyciu identyfikatora, który już istnieje na hoście. Nazwa "AppLogger", na przykład, już istnieje. W takim przypadku `push` polecenie podaje następujący błąd:

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

Jeśli używasz prawidłowego klucza interfejsu API, który właśnie został utworzony, ten komunikat wskazuje konflikt nazewnictwa, który nie jest całkowicie jasne z "uprawnienia" część błędu. Zmień identyfikator pakietu, odbuduj projekt, `.nupkg` ponownie stwórz `push` plik i ponów próbę wykonania polecenia.