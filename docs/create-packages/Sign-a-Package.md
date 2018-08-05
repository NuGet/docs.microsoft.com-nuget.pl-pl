---
title: Podpisywanie pakietów NuGet
description: Wyjaśnia, jak podpisanych pakietów może służyć do włączyć weryfikację zawartości integralności.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 8bbbc785a50e49530bbbd4e88bbd71a8a7bfe911
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508182"
---
# <a name="signing-nuget-packages"></a>Podpisywanie pakietów NuGet

Podpisywanie pakietu jest procesem, który sprawia, że pakiet nie został zmodyfikowany od czasu jego utworzenia.

## <a name="prerequisites"></a>Wymagania wstępne

1. Pakiet ( `.nupkg` plików) do podpisywania. Zobacz [Tworzenie pakietu](creating-a-package.md).

1. nuget.exe 4.6.0 lub nowszej. Zobacz jak [zainstalować interfejs wiersza polecenia NuGet](../install-nuget-client-tools.md#nugetexe-cli).

1. [Certyfikat podpisywania kodu](../reference/signed-packages-reference.md#get-a-code-signing-certificate).

## <a name="sign-a-package"></a>Podpisywanie pakietu

Aby zarejestrować pakiet, należy użyć [logowania nuget](../tools/cli-ref-sign.md):

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

Zgodnie z opisem w dokumentacji poleceń, można użyć certyfikatu jest dostępny w magazynie certyfikatów lub używany certyfikat z pliku.

### <a name="common-problems-when-signing-a-package"></a>Typowe problemy podczas podpisywania pakietu

- Certyfikat nie jest prawidłowy do podpisywania kodu. Upewnij się, że określony certyfikat ma odpowiednią rozszerzone użycie klucza (EKU 1.3.6.1.5.5.7.3.3).
- Certyfikat nie spełnia wymagania podstawowe, takie jak algorytm podpisu RSA, SHA-256 lub publicznej klucza 2048 bitów lub nowszej.
- Certyfikat wygasł lub został odwołany.
- Serwera znacznika czasowego nie spełnia wymagań dotyczących certyfikatów.

> [!Note]
> Podpisanych pakietów powinien zawierać sygnaturę czasową, aby upewnić się, że podpis pozostaje ważny, gdy wygasł certyfikat podpisywania. Generuje operacji logowania [ostrzeżenie NU3002](../reference/errors-and-warnings/NU3002.md) podczas logowania się bez sygnatury czasowej.

## <a name="verify-a-signed-package"></a>Sprawdź podpisanych pakietów

Użyj [Sprawdź nuget](../tools/cli-ref-verify.md) szczegóły podpisu danego pakietu:

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a>Zainstaluj pakiet podpisem

Podpisanych pakietów nie wymagają żadnych określone działanie prowadzące do zainstalowania; jednak zawartość została zmodyfikowana po podpisaniu, instalacja będzie zablokowany, a następnie tworzy [błąd NU3008](../reference/errors-and-warnings/NU3008.md).

> [!Warning]
> Pakiety podpisany przy użyciu niezaufane certyfikaty są traktowane jako jako bez znaku i są instalowane bez żadnych ostrzeżeń ani błędów, takich jak każdy inny pakiet bez znaku.

## <a name="see-also"></a>Zobacz także

[Dokumentacja podpisanych pakietów](../reference/Signed-Packages-Reference.md)
