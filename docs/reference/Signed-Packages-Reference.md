---
title: Podpisanych pakietów
description: Wymagania dotyczące podpisywania pakietu NuGet.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 952256a24246543ecd4c37285cd001622aa2bc46
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426176"
---
# <a name="signed-packages"></a>Podpisane pakiety

*NuGet 4.6.0+ i Visual Studio 2017 w wersji 15.6 i nowszych*

Pakiety NuGet może zawierać podpis cyfrowy, który zapewnia ochronę przed zmodyfikowany zawartości. Ta sygnatura jest generowany z certyfikat X.509, który dodaje również autentyczności dowody do rzeczywistego źródła pakietu.

Podpisanych pakietów zapewnia najsilniejszą weryfikacji end-to-end. Istnieją dwa różne typy podpisów NuGet:
- **Tworzenie sygnatury**. Autor podpis gwarantuje, że pakiet nie został zmodyfikowany od czasu Autor podpisania pakietu, niezależnie od którego repozytorium lub co transportu metody jest dostarczany w pakiecie. Ponadto podpisane przez autora pakietów zapewniają mechanizm uwierzytelniania dodatkowego do potoku publikowania w witrynie nuget.org, ponieważ certyfikatu podpisywania musi być zarejestrowany wcześniej. Aby uzyskać więcej informacji, zobacz [rejestrowanie certyfikatów](#signature-requirements-on-nugetorg).
- **Podpis repozytorium**. Podpisy repozytorium zapewniają gwarancji spójności dla **wszystkich** pakietów w repozytorium, czy są one podpisane lub nie, autor, nawet wtedy, gdy te pakiety są uzyskiwane z innej lokalizacji niż oryginalny repozytorium, gdzie znajdowały się podpisany.   

Aby uzyskać szczegółowe informacje na temat tworzenia pakietu podpisem autora, zobacz [podpisywanie pakietów](../create-packages/Sign-a-package.md) i [polecenie logowania nuget](../tools/cli-ref-sign.md).

> [!Important]
> Podpisywanie pakietów jest obecnie obsługiwana tylko wtedy, gdy za pomocą nuget.exe na Windows. Weryfikacja podpisanych pakietów jest obecnie obsługiwana tylko wtedy, gdy za pomocą nuget.exe lub Visual Studio na Windows.

## <a name="certificate-requirements"></a>Wymagania certyfikatu

Podpisywanie pakietów wymaga podpisywania certyfikatu, który to specjalny typ certyfikatu, który nadaje się do kodu `id-kp-codeSigning` cel [[RFC 5280 sekcji 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Ponadto certyfikat musi mieć publicznego długość klucza RSA 2048 bitów lub nowszej.

## <a name="timestamp-requirements"></a>Wymagania dotyczące znacznik czasu:

Podpisanych pakietów powinien zawierać znacznik czasu RFC 3161 w celu zapewnienia walidacji podpisu poza podpisywania okresu ważności certyfikatu pakietu. Certyfikat używany do podpisywania to sygnatura czasowa muszą być prawidłowe dla `id-kp-timeStamping` cel [[RFC 5280 sekcji 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Ponadto certyfikat musi mieć publicznego długość klucza RSA 2048 bitów lub nowszej.

Dodatkowe szczegóły techniczne można znaleźć w [specyfikacje techniczne podpisu pakietu](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Wymagania dotyczące podpisu w witrynie NuGet.org

nuget.org ma dodatkowe wymagania dotyczące zaakceptowanie podpisanych pakietów:

- Podpis podstawowy musi mieć podpis autora.
- Podpis podstawowy musi mieć pojedynczy prawidłową sygnaturę czasową.
- Certyfikaty X.509 dla podpisu autora i jeho signatura sygnatura czasowa:
  - Musi mieć klucz publiczny RSA 2048 bitów lub nowszej.
  - Musi być w okresie ważności na bieżący czas UTC, podczas weryfikacji pakietu w witrynie nuget.org.
  - Muszą być powiązane z zaufanego głównego urzędu certyfikacji, który jest zaufany domyślnie w systemie Windows. Pakiety podpisany przy użyciu własnym wystawionych certyfikatów są odrzucane.
  - Musi być ważny przez jej przeznaczenie: 
    - Tworzenie certyfikatu podpisywania musi być prawidłowy do podpisywania kodu.
    - Znacznik czasu: musi to być nieprawidłowy dla użycia.
  - Nie musi zostać cofnięta podczas podpisywania czasu. (To nie będzie knowable w chwili przesyłania, więc nuget.org okresowo sprawdza ponownie stanu odwołania).
  
  
## <a name="related-articles"></a>Pokrewne artykuły:

- [Podpisywanie pakietów NuGet](../create-packages/Sign-a-Package.md)
- [Zarządzanie granicami zaufania pakietu](../consume-packages/installing-signed-packages.md)
