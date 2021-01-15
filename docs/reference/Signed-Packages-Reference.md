---
title: Podpisane pakiety
description: Wymagania dotyczące podpisywania pakietów NuGet.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: ac9efadc1d29bec86ca9b7821d5587e0171613aa
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235714"
---
# <a name="signed-packages"></a>Podpisane pakiety

*NuGet 4.6.0 + i Visual Studio 2017 w wersji 15,6 lub nowszej*

Pakiety NuGet mogą zawierać podpis cyfrowy zapewniający ochronę przed nienaruszoną zawartością. Ta sygnatura jest generowana na podstawie certyfikatu X. 509, który dodaje również potwierdzenia autentyczności do rzeczywistego źródła pakietu.

Pakiety podpisane zapewniają silny kompleksową weryfikację. Istnieją dwa różne typy podpisów NuGet:
- **Podpis autora**. Sygnatura autora gwarantuje, że pakiet nie został zmodyfikowany od momentu, gdy autor podpisał pakiet, niezależnie od tego, który z nich pochodzi lub w jakiej metodzie transportu pakiet został dostarczony. Ponadto pakiety podpisane przez autora zapewniają dodatkowy mechanizm uwierzytelniania w potoku publikowania nuget.org, ponieważ certyfikat podpisywania musi być zarejestrowany przed czasem. Aby uzyskać więcej informacji, zobacz [Rejestrowanie certyfikatów](#signature-requirements-on-nugetorg).
- **Sygnatura repozytorium**. Sygnatury repozytorium zapewniają gwarancję integralności dla **wszystkich** pakietów w repozytorium, niezależnie od tego, czy są one utworzone przez autora, nawet jeśli te pakiety są uzyskiwane z innej lokalizacji niż pierwotne repozytorium, w którym zostały podpisane.   

Aby uzyskać szczegółowe informacje na temat tworzenia pakietu podpisanego przez autora, zobacz [podpisywanie pakietów](../create-packages/Sign-a-package.md) i [polecenie NuGet Sign](../reference/cli-reference/cli-ref-sign.md). Podpisy pakietów można sprawdzić za pomocą poleceń [Weryfikuj](/dotnet/core/tools/dotnet-nuget-verify.md) lub [NuGet](../reference/cli-reference/cli-ref-verify.md) NuGet programu dotnet.

> [!Important]
> Tworzenie pakietów podpisywania jest obsługiwane tylko przez nuget.exe w systemie Windows. Wszystkie pakiety przekazane do nuget.org są jednak automatycznie podpisane repozytorium.

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
- [Weryfikowanie podpisanych pakietów przy użyciu interfejsu wiersza polecenia dotnet](/dotnet/core/tools/dotnet-nuget-verify.md)
- [Weryfikuj podpisane pakiety przy użyciu nuget.exe](../reference/cli-reference/cli-ref-verify.md)
- [Zarządzanie granicami zaufania pakietów](../consume-packages/installing-signed-packages.md)
