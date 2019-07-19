---
title: Polecenie podpisywania interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia Design NuGet. exe
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e941a9f34058f5ebed13a8f68c8cfa23ba5fb6d1
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328280"
---
# <a name="sign-command-nuget-cli"></a>sign command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** **obsługiwane wersje** tworzenia &bullet; pakietów: 4.6 +

Podpisuje wszystkie pakiety pasujące do pierwszego argumentu z certyfikatem. Certyfikat z kluczem prywatnym można uzyskać z pliku lub z certyfikatu zainstalowanego w magazynie certyfikatów przez podanie nazwy podmiotu lub odcisku palca.

Podpisywanie pakietów nie jest jeszcze obsługiwane w programie .NET Core, w obszarze mono lub na platformach innych niż Windows.

## <a name="usage"></a>Użycie

```cli
nuget sign <package(s)> [options]
```

gdzie `<package(s)>` jest co najmniej jeden `.nupkg` plik.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| CertificateFingerprint | Określa odcisk palca SHA-1 certyfikatu używanego do wyszukiwania certyfikatu w lokalnym magazynie certyfikatów. |
| certificatePassword | Określa hasło certyfikatu, w razie konieczności. Jeśli certyfikat jest chroniony hasłem, ale nie podano hasła, polecenie wyświetli monit o podanie hasła w czasie wykonywania, chyba że zostanie przekazana opcja-nieinteraktywna. |
| CertificatePath | Określa ścieżkę pliku do certyfikatu, który ma być używany podczas podpisywania pakietu. |
| CertificateStoreLocation | Określa nazwę magazynu certyfikatów X. 509 używanego do wyszukiwania certyfikatu. Wartość domyślna to "CurrentUser", magazyn certyfikatów X. 509 używany przez bieżącego użytkownika. Tej opcji należy użyć w przypadku określenia certyfikatu za pomocą opcji-CertificateSubjectName lub-CertificateFingerprint. |
| CertificateStoreName | Określa nazwę magazynu certyfikatów X. 509 do użycia w celu wyszukania certyfikatu. Wartość domyślna to "my", czyli magazyn certyfikatów X. 509 dla certyfikatów osobistych. Tej opcji należy użyć w przypadku określenia certyfikatu za pomocą opcji-CertificateSubjectName lub-CertificateFingerprint. |
| CertificateSubjectName | Określa nazwę podmiotu certyfikatu używanego do wyszukiwania certyfikatu w lokalnym magazynie certyfikatów.  Wyszukiwanie to porównanie ciągów bez uwzględniania wielkości liter przy użyciu podanej wartości, która będzie znajdować wszystkie certyfikaty z nazwą podmiotu zawierającą ten ciąg, niezależnie od innych wartości podmiotu.  Magazyn certyfikatów można określić za pomocą opcji-CertificateStoreName i-CertificateStoreLocation. |
| ConfigFile | Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).|
| ForceEnglishOutput | Wymusza uruchomienie NuGet. exe przy użyciu niezmiennej, opartej na języku angielskim kultury. |
| Algorytm | Algorytm wyznaczania wartości skrótu, który ma być używany do podpisywania pakietu. Wartość domyślna to SHA256. |
| Help | Wyświetla informacje pomocy dla polecenia. |
| NonInteractive | Pomija monity o dane wejściowe lub potwierdzone przez użytkownika. |
| OutputDirectory | Określa katalog, w którym ma zostać zapisany podpisany pakiet. Domyślnie oryginalny pakiet jest zastępowany przez podpisany pakiet. |
| Zastąp | Przełącz, aby wskazać, czy bieżący podpis powinien zostać nadpisany. Domyślnie polecenie zakończy się niepowodzeniem, jeśli pakiet ma już podpis. |
| Timestamper | Adres URL do serwera znacznika czasu RFC 3161. |
| TimestampHashAlgorithm | Algorytm wyznaczania wartości skrótu, który ma być używany przez serwer znacznika czasu RFC 3161. Wartość domyślna to SHA256. |
| Verbosity | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*. |

## <a name="examples"></a>Przykłady

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```