---
title: Polecenie podpisywania interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia nuget.exe Sign
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 84386f1752b98688f1fd34e453f5b72ae8afdd92
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622775"
---
# <a name="sign-command-nuget-cli"></a>Sign — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** &bullet; **obsługiwane wersje:** 4.6 +

Podpisuje wszystkie pakiety pasujące do pierwszego argumentu z certyfikatem. Certyfikat z kluczem prywatnym można uzyskać z pliku lub z certyfikatu zainstalowanego w magazynie certyfikatów przez podanie nazwy podmiotu lub odcisku palca.

> [!Note]
> Podpisywanie pakietów nie jest jeszcze obsługiwane w programie .NET Core, w obszarze mono lub na platformach innych niż Windows.

## <a name="usage"></a>Użycie

```cli
nuget sign <package(s)> [options]
```

gdzie `<package(s)>` jest co najmniej jeden `.nupkg` plik.

## <a name="options"></a>Opcje

- **`-CertificateFingerprint`**

  Określa odcisk palca SHA-1 certyfikatu używanego do wyszukiwania certyfikatu w lokalnym magazynie certyfikatów.

- **`-CertificatePassword`**

  Określa hasło certyfikatu, w razie konieczności. Jeśli certyfikat jest chroniony hasłem, ale nie podano hasła, polecenie wyświetli monit o podanie hasła w czasie wykonywania, chyba że `-NonInteractive` opcja zostanie przekazana.

- **`-CertificatePath`**

  Określa ścieżkę pliku do certyfikatu, który ma być używany podczas podpisywania pakietu.

- **`-CertificateStoreLocation`**

  Określa nazwę magazynu certyfikatów X. 509 używanego do wyszukiwania certyfikatu. Wartość domyślna to "CurrentUser", magazyn certyfikatów X. 509 używany przez bieżącego użytkownika. Ta opcja powinna być używana podczas określania certyfikatu za pośrednictwem `-CertificateSubjectName` `-CertificateFingerprint` opcji lub.

- **`-CertificateStoreName`**

  Określa nazwę magazynu certyfikatów X. 509 do użycia w celu wyszukania certyfikatu. Wartość domyślna to "my", czyli magazyn certyfikatów X. 509 dla certyfikatów osobistych. Ta opcja powinna być używana podczas określania certyfikatu za pośrednictwem `-CertificateSubjectName` `-CertificateFingerprint` opcji lub.

- **`-CertificateSubjectName`**

  Określa nazwę podmiotu certyfikatu używanego do wyszukiwania certyfikatu w lokalnym magazynie certyfikatów.  Wyszukiwanie to porównanie ciągów bez uwzględniania wielkości liter przy użyciu podanej wartości, która będzie znajdować wszystkie certyfikaty z nazwą podmiotu zawierającą ten ciąg, niezależnie od innych wartości podmiotu.  Magazyn certyfikatów można określić za pomocą `-CertificateStoreName` opcji i `-CertificateStoreLocation` .

- **`-ConfigFile`**

  Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.

- **`-ForceEnglishOutput`**

  Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.

- **`-HashAlgorithm`**

  Algorytm wyznaczania wartości skrótu, który ma być używany do podpisywania pakietu. Wartość domyślna to SHA256. Możliwe wartości to SHA256, SHA384 i SHA512.

- **`-?|-help`**

  Wyświetla informacje pomocy dla polecenia.

- **`-NonInteractive`**

  Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.

- **`-OutputDirectory`**

  Określa katalog, w którym ma zostać zapisany podpisany pakiet. Domyślnie oryginalny pakiet jest zastępowany przez podpisany pakiet.

- **`-Overwrite`**

  Przełącz, aby wskazać, czy bieżący podpis powinien zostać nadpisany. Domyślnie polecenie zakończy się niepowodzeniem, jeśli pakiet ma już podpis.

- **`-Timestamper`**

  Adres URL do serwera znacznika czasu RFC 3161.

- **`-TimestampHashAlgorithm`**

  Algorytm wyznaczania wartości skrótu, który ma być używany przez serwer znacznika czasu RFC 3161. Wartość domyślna to SHA256.

- **`-Verbosity [normal|quiet|detailed]`**

  Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .

## <a name="examples"></a>Przykłady

```cli
nuget sign MyPackage.nupkg -CertificatePath .\..\certificate.pfx -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -CertificateStoreLocation CurrentUser -CertificateStoreName My -CertificateSubjectName 'subject name' -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
