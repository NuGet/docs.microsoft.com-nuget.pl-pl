---
title: Podpisywanie pakietów NuGet | Dokumentacja firmy Microsoft
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Wyjaśniono, jak podpisanych pakietów można włączyć weryfikację zawartości integralności.
keywords: Pakiet NuGet podpisywania zabezpieczeń NuGet, tworzenie pakietów podpisem
ms.reviewer:
- karann-msft
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 61d90066e8cf75c8f49c7cc9390d45e1cd8afd0d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="signing-nuget-packages"></a>Podpisywanie pakietów NuGet

Podpisywanie pakietu jest procesem, który sprawia, że pakiet nie został zmodyfikowany od czasu jego utworzenia.

## <a name="prerequisites"></a>Wymagania wstępne

1. Pakiet ( `.nupkg` pliku) do podpisywania. Zobacz [utworzenie pakietu](creating-a-package.md).

1. nuget.exe 4.6.0 lub nowszym. Zobacz temat jak [zainstaluj interfejs wiersza polecenia NuGet](../install-nuget-client-tools.md#nugetexe-cli).

1. [Certyfikat podpisywania kodu](../reference/signed-packages-reference.md#get-a-code-signing-certificate).

> [!Warning]
> nuget.org nie akceptuje obecnie podpisanych pakietów. Możesz zarejestrować pakietów do publikowania do niestandardowych źródeł danych.

## <a name="sign-a-package"></a>Podpisywanie pakietu

Aby zarejestrować pakiet, należy użyć [znak nuget](../tools/cli-ref-sign.md):

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

Zgodnie z opisem w dokumentacji poleceń, można użyć dostępny certyfikat w magazynie certyfikatów lub używania certyfikatu z pliku.

### <a name="common-problems-when-signing-a-package"></a>Typowe problemy podczas podpisywania pakietu

- Certyfikat nie jest prawidłowy do podpisywania kodu. Należy się upewnić się, że określony certyfikat ma odpowiednie rozszerzone użycie klucza (EKU 1.3.6.1.5.5.7.3.3).
- Certyfikat nie spełnia podstawowe wymagania, np. RSA, SHA-256 algorytm podpisu lub publicznego klucza 2048 bitów lub większej.
- Certyfikat wygasł lub został odwołany.
- Serwer znaczników czasu nie spełnia wymagań dotyczących certyfikatów.

> [!Note]
> Pakiety podpisem powinna zawierać sygnaturę czasową, aby upewnić się, że podpis pozostaje ważny po wygaśnięciu certyfikatu podpisywania. Tworzy operacji logowania [ostrzeżenie NU3002](../reference/Errors-and-Warnings.md#nu3002) przy logowaniu się bez sygnatury czasowej.

## <a name="verify-a-signed-package"></a>Sprawdź podpisanego pakietu

Użyj [nuget Sprawdź](../tools/cli-ref-verify.md) Aby wyświetlić szczegóły sygnatury danego pakietu:

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a>Zainstaluj pakiet podpisem

Podpisanych pakietów nie wymagają żadnych określonych czynności w celu zainstalowania; Jednak jeśli zawartość została zmodyfikowana po podpisaniu, podczas instalacji będzie zablokowane i tworzy [błąd NU3008](../reference/Errors-and-Warnings.md#nu3008).

> [!Warning]
> Uwzględniane są podpisane za pomocą certyfikatów niezaufanych pakiety jako bez znaku i są instalowane bez żadnych ostrzeżeń ani błędów, takich jak niepodpisanego pakietu.

## <a name="see-also"></a>Zobacz także

[Podpisana pakietów odniesienia](../reference/Signed-Packages-Reference.md)
