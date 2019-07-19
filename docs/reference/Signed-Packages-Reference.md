---
title: Podpisane pakiety
description: Wymagania dotyczące podpisywania pakietów NuGet.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: e02b2a241008b1b7096f20b351173fd3df7ed172
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317517"
---
# <a name="signed-packages"></a>Podpisane pakiety

*NuGet 4.6.0 + i Visual Studio 2017 w wersji 15,6 lub nowszej*

Pakiety NuGet mogą zawierać podpis cyfrowy zapewniający ochronę przed nienaruszoną zawartością. Ta sygnatura jest generowana na podstawie certyfikatu X. 509, który dodaje również potwierdzenia autentyczności do rzeczywistego źródła pakietu.

Pakiety podpisane zapewniają silny kompleksową weryfikację. Istnieją dwa różne typy podpisów NuGet:
- **Podpis autora**. Sygnatura autora gwarantuje, że pakiet nie został zmodyfikowany od momentu, gdy autor podpisał pakiet, niezależnie od tego, który z nich pochodzi lub w jakiej metodzie transportu pakiet został dostarczony. Ponadto pakiety podpisane przez autora zapewniają dodatkowy mechanizm uwierzytelniania w potoku publikowania nuget.org, ponieważ certyfikat podpisywania musi być zarejestrowany przed czasem. Aby uzyskać więcej informacji, zobacz [Rejestrowanie certyfikatów](#signature-requirements-on-nugetorg).
- **Sygnatura repozytorium**. Sygnatury repozytorium zapewniają gwarancję integralności dla **wszystkich** pakietów w repozytorium, niezależnie od tego, czy są one utworzone przez autora, nawet jeśli te pakiety są uzyskiwane z innej lokalizacji niż pierwotne repozytorium, w którym zostały podpisane.   

Aby uzyskać szczegółowe informacje na temat tworzenia pakietu podpisanego przez autora, zobacz Podpisywanie [pakietów](../create-packages/Sign-a-package.md) i [polecenie NuGet Sign](../reference/cli-reference/cli-ref-sign.md).

> [!Important]
> Podpisywanie pakietów jest obecnie obsługiwane tylko w przypadku korzystania z programu NuGet. exe w systemie Windows. Weryfikacja podpisanych pakietów jest obecnie obsługiwana tylko w przypadku korzystania z programu NuGet. exe lub Visual Studio w systemie Windows.

## <a name="certificate-requirements"></a>Wymagania certyfikatu

Podpisywanie pakietu wymaga certyfikatu podpisywania kodu, który jest specjalnym typem certyfikatu, który jest prawidłowy dla `id-kp-codeSigning` celu [[RFC 5280 sekcja 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Ponadto certyfikat musi mieć długość klucza publicznego RSA wynoszącą 2048 bitów lub wyższą.

## <a name="timestamp-requirements"></a>Wymagania dotyczące sygnatur czasowych

Podpisane pakiety powinny zawierać sygnaturę czasową RFC 3161, aby zapewnić Ważność podpisu poza okresem ważności certyfikatu podpisywania pakietu. Certyfikat używany do podpisywania sygnatury czasowej musi być prawidłowy dla `id-kp-timeStamping` celu [[RFC 5280 sekcja 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Ponadto certyfikat musi mieć długość klucza publicznego RSA wynoszącą 2048 bitów lub wyższą.

Dodatkowe szczegóły techniczne można znaleźć w tematach [techniczne sygnatury pakietu](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Wymagania dotyczące podpisu w witrynie NuGet.org

nuget.org ma dodatkowe wymagania dotyczące akceptowania podpisanego pakietu:

- Podpis podstawowy musi być podpisem autora.
- Podpis podstawowy musi mieć pojedynczą prawidłową sygnaturę czasową.
- Certyfikaty X. 509 zarówno dla podpisu autora, jak i sygnatury sygnatury czasowej:
  - Musi mieć klucz publiczny RSA 2048 bity lub nowszy.
  - Musi być w okresie ważności na bieżący czas UTC w czasie sprawdzania poprawności pakietu na nuget.org.
  - Musi być łańcuchem do zaufanego głównego urzędu certyfikacji, który domyślnie jest zaufany w systemie Windows. Pakiety podpisane przy użyciu certyfikatów z podpisem własnym są odrzucane.
  - Musi być prawidłowy w swoim przeznaczeniu: 
    - Certyfikat podpisywania autora musi być prawidłowy w przypadku podpisywania kodu.
    - Certyfikat sygnatury czasowej musi być prawidłowy dla sygnatury czasowej.
  - Nie może zostać odwołane w czasie podpisywania. (Może to nie być znane w czasie przesłania, więc nuget.org okresowo sprawdza stan odwołania).
  
  
## <a name="related-articles"></a>Pokrewne artykuły:

- [Podpisywanie pakietów NuGet](../create-packages/Sign-a-Package.md)
- [Zarządzanie granicami zaufania pakietów](../consume-packages/installing-signed-packages.md)
