---
title: Podpisane pakiety
description: Wymagania dotyczące podpisywania pakietów NuGet.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 85fdf7a41cc033d92bbd0326648142aec27a9970
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508803"
---
# <a name="signed-packages"></a>Podpisane pakiety

*NuGet 4.6.0+ i Visual Studio 2017 w wersji 15.6 lub nowszej*

Pakiety NuGet mogą zawierać podpis cyfrowy, który zapewnia ochronę przed naruszoną zawartością. Ten podpis jest wytwarzanych na podstawie certyfikatu X.509, który dodaje również weryfikacje autentyczności do rzeczywistego źródła pakietu.

Podpisane pakiety zapewniają najsilniejszą, end-to-end weryfikację. Istnieją dwa różne typy sygnatur NuGet:
- **Tworzenie podpisu**. Podpis autora gwarantuje, że pakiet nie został zmodyfikowany od momentu podpisania pakietu przez autora, niezależnie od tego, z którego repozytorium lub jakiej metody transportu pakiet jest dostarczany. Ponadto pakiety podpisane przez autora zapewniają dodatkowy mechanizm uwierzytelniania dla potoku publikowania nuget.org, ponieważ certyfikat podpisywania musi zostać wcześniej zarejestrowany. Aby uzyskać więcej informacji, zobacz [Rejestrowanie certyfikatów](#signature-requirements-on-nugetorg).
- **Sygnatura repozytorium.** Podpisy repozytorium zapewniają gwarancję  integralności dla wszystkich pakietów w repozytorium bez względu na to, czy są podpisane przez autora, nawet jeśli te pakiety są uzyskiwane z innej lokalizacji niż oryginalne repozytorium, w którym zostały podpisane.   

Aby uzyskać szczegółowe informacje na temat tworzenia pakietu podpisanego przez autora, zobacz [Podpisywanie pakietów](../create-packages/Sign-a-package.md) i [polecenie podpisywania nuget](../reference/cli-reference/cli-ref-sign.md). Podpisy pakietów można zweryfikować przy użyciu poleceń [dotnet nuget verify lub](/dotnet/core/tools/dotnet-nuget-verify) [nuget verify.](../reference/cli-reference/cli-ref-verify.md)

> [!Important]
> Tworzenie pakietów podpisywania jest obecnie obsługiwane nuget.exe w systemie Windows. Jednak wszystkie pakiety przekazane do nuget.org są automatycznie podpisane w repozytorium.

## <a name="certificate-requirements"></a>Wymagania certyfikatu

Podpisywanie pakietu wymaga certyfikatu podpisywania kodu, który jest specjalnym typem certyfikatu, który jest ważny do tego celu `id-kp-codeSigning` [[RFC 5280 sekcja 4.2.1.12].](https://tools.ietf.org/html/rfc5280#section-4.2.1.12) Ponadto certyfikat musi mieć długość klucza publicznego RSA co najmniej 2048 bitów.

## <a name="timestamp-requirements"></a>Wymagania dotyczące sygnatury czasowej

Podpisane pakiety powinny zawierać znacznik czasu RFC 3161 w celu zapewnienia ważności podpisu poza okresem ważności certyfikatu podpisywania pakietu. Certyfikat używany do podpisania sygnatury czasowej musi być ważny do celów `id-kp-timeStamping` [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Ponadto certyfikat musi mieć klucz publiczny RSA o długości co najmniej 2048 bitów.

Dodatkowe szczegóły techniczne można znaleźć w specyfikacji technicznej [sygnatury pakietu](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Wymagania dotyczące podpisu w NuGet.org

nuget.org wymagania dotyczące akceptowania podpisanego pakietu:

- Podpis podstawowy musi być podpisem autora.
- Podpis podstawowy musi mieć jeden prawidłowy znacznik czasu.
- Certyfikaty X.509 dla podpisu autora i jego sygnatury czasowej:
  - Musi mieć co najmniej 2048 bitów klucza publicznego RSA.
  - Musi znajdować się w okresie ważności dla bieżącego czasu UTC w czasie weryfikacji pakietu na nuget.org.
  - Musi być łączona łańcuchowo z zaufanym głównym urządem, który jest domyślnie zaufany w systemie Windows. Pakiety podpisane za pomocą samodzielnie wystawionych certyfikatów są odrzucane.
  - Musi być prawidłowy w swoim celu: 
    - Certyfikat podpisywania autora musi być prawidłowy dla podpisywania kodu.
    - Certyfikat sygnatury czasowej musi być prawidłowy dla sygnatury czasowej.
  - Nie można odwołać w czasie podpisywania. (Może to nie być wiadomo w czasie przesyłania, więc nuget.org okresowo ponownie sprawdza stan odwołania).
  
  
## <a name="related-articles"></a>Pokrewne artykuły:

- [Podpisywanie pakietów NuGet](../create-packages/Sign-a-Package.md)
- [Weryfikowanie podpisanych pakietów przy użyciu interfejsu wiersza polecenia dotnet](/dotnet/core/tools/dotnet-nuget-verify)
- [Weryfikowanie podpisanych pakietów przy użyciu nuget.exe](../reference/cli-reference/cli-ref-verify.md)
- [Zarządzanie granicami zaufania pakietów](../consume-packages/installing-signed-packages.md)
