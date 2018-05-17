---
title: Polecenie znak NuGet interfejsu wiersza polecenia
description: Informacje dotyczące polecenia znak nuget.exe
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7e84d794b802cfd69c785f720280fd5c022a46f6
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="sign-command-nuget-cli"></a>sign command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** pakietu tworzenia &bullet; **obsługiwane wersje:** 4.6 +

Rejestruje wszystkie pakiety dopasowania pierwszy argument przy użyciu certyfikatu. Z plikiem lub zainstalowanego w magazynie certyfikatów, podając nazwę podmiotu i odcisk palca certyfikatu można uzyskać certyfikatu z kluczem prywatnym.

Podpisywanie pakietu nie jest jeszcze obsługiwana w .NET Core, w obszarze Mono lub na różnych platformach z systemem innym niż Windows.

## <a name="usage"></a>Użycie

```cli
nuget sign <package(s)> [options]
```

gdzie `<package(s)>` jest co najmniej jeden `.nupkg` plików.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| CertificateFingerprint | Określa algorytm SHA-1 odcisk palca certyfikatu używanego do wyszukiwania lokalnego magazynu certyfikatów dla certyfikatu. |
| CertificatePassword | Określa hasło certyfikatu, jeśli to konieczne. Jeśli certyfikat jest chroniony hasłem, ale hasło nie jest dostępne, polecenie będzie monitować o hasło w czasie wykonywania, chyba że opcja nieinterakcyjnego jest przekazywana. |
| CertificatePath | Określa ścieżkę do certyfikatu, który ma być używana podczas podpisywania pakietu. |
| CertificateStoreLocation | Określa nazwę Użyj magazynu certyfikatu X.509 do wyszukiwania certyfikatu. Wartość domyślna to "CurrentUser" magazynu certyfikatu X.509, używanego przez bieżącego użytkownika. Tej opcji należy używać podczas określania certyfikatu przy użyciu opcji - CertificateSubjectName lub - CertificateFingerprint. |
| CertificateStoreName | Określa nazwę magazynu certyfikatu X.509 do służy do wyszukiwania certyfikatu. Wartość domyślna to "My", X.509 magazynu certyfikatów osobistych. Tej opcji należy używać podczas określania certyfikatu przy użyciu opcji - CertificateSubjectName lub - CertificateFingerprint. |
| CertificateSubjectName | Określa nazwę podmiotu certyfikatu używanego do wyszukiwania lokalnego magazynu certyfikatów dla certyfikatu.  Wyszukiwanie jest porównania bez uwzględniania wielkości liter ciągów za pomocą podana wartość, która znajdzie wszystkie certyfikaty z nazwą podmiotu, zawierającą ten ciąg, niezależnie od innych wartości podmiotu.  Magazyn certyfikatów można określić opcji - CertificateStoreName i - CertificateStoreLocation. |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.|
| ForceEnglishOutput | Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Algorytm skrótu | Algorytm wyznaczania wartości skrótu, który ma być używany do podpisywania pakietu. Wartość domyślna to SHA256. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| OutputDirectory | Określa katalog, w którym ma zostać zapisany pakiet podpisem. Domyślnie oryginalnego pakietu jest zastępowany przez pakiet podpisem. |
| Zastąp | Przełącz, aby wskazać, jeśli można zastąpić bieżący podpisu. Domyślnie polecenia zakończy się niepowodzeniem, jeśli pakiet zawiera już podpisu. |
| Timestamper | Adres URL serwera sygnatur RFC 3161. |
| TimestampHashAlgorithm | Algorytm wyznaczania wartości skrótu używanego przez serwer znaczników czasu RFC 3161. Wartość domyślna to SHA256. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*. |

## <a name="examples"></a>Przykłady

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```