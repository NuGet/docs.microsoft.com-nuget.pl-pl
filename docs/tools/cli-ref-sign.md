---
title: Polecenie logowania interfejs wiersza polecenia NuGet
description: Dokumentacja dotycząca polecenie logowania nuget.exe
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e941a9f34058f5ebed13a8f68c8cfa23ba5fb6d1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546366"
---
# <a name="sign-command-nuget-cli"></a>sign command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** Tworzenie pakietu &bullet; **obsługiwane wersje:** 4.6 +

Rejestruje wszystkie pakiety dopasowania pierwszy argument przy użyciu certyfikatu. Z pliku lub zainstalowanego w magazynie certyfikatów, podając nazwę podmiotu lub odcisku palca certyfikatu można uzyskać certyfikat z kluczem prywatnym.

Podpisywanie pakietów nie jest jeszcze obsługiwana w platformę .NET Core, w ramach platformy Mono lub na platformach innych niż Windows.

## <a name="usage"></a>Użycie

```cli
nuget sign <package(s)> [options]
```

gdzie `<package(s)>` ma jeden lub więcej `.nupkg` plików.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| CertificateFingerprint | Określa odcisk palca SHA-1 certyfikatu używanego do wyszukania w lokalnym magazynie certyfikatów dla certyfikatu. |
| CertificatePassword | Określa hasło certyfikatu, jeśli to konieczne. Jeśli certyfikat jest chroniony hasłem, ale nie hasło jest podany, polecenie wyświetli monit o podanie hasła w czasie wykonywania, chyba że opcja nieinteraktywnych jest przekazywany. |
| CertificatePath | Określa ścieżkę do certyfikatu, który ma być używany z rejestracją pakietu. |
| CertificateStoreLocation | Określa nazwę magazynu certyfikatu X.509 użytkowania do wyszukania certyfikatu. Wartość domyślna to "CurrentUser" magazynu certyfikatu X.509, które są używane przez bieżącego użytkownika. Ta opcja powinna być używana podczas określania certyfikatu przy użyciu opcji - CertificateSubjectName lub - CertificateFingerprint. |
| CertificateStoreName | Określa nazwę magazynu certyfikatu X.509 na potrzeby wyszukiwania certyfikatu. Wartość domyślna to "Mój", magazynu certyfikatu X.509 do certyfikatów osobistych. Ta opcja powinna być używana podczas określania certyfikatu przy użyciu opcji - CertificateSubjectName lub - CertificateFingerprint. |
| CertificateSubjectName | Określa nazwę podmiotu certyfikatu używanego do wyszukania w lokalnym magazynie certyfikatów dla certyfikatu.  Wyszukiwanie jest porównanie bez uwzględniania wielkości liter ciągu przy użyciu podana wartość, która zawiera wszystkie certyfikaty z nazwą podmiotu, zawierającą ten ciąg, niezależnie od innych wartości podmiotu.  Magazyn certyfikatów można określić opcje - CertificateStoreName i - CertificateStoreLocation. |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.|
| ForceEnglishOutput | Wymusza nuget.exe do uruchamiania przy użyciu kultury niezmiennej, oparte na język angielski. |
| Algorytm | Algorytm wyznaczania wartości skrótu, który ma być używany do podpisania pakietu. Wartość domyślna to SHA256. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Nieinterakcyjnym | Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia. |
| OutputDirectory | Określa katalog, w którym chcesz zapisać pakiet podpisem. Domyślnie oryginalny pakiet jest zastępowany przez pakiet podpisem. |
| Zastąp | Przełącz, aby wskazać bieżący podpisu powinien zostać zastąpiony. Domyślnie polecenie zakończy się niepowodzeniem Jeżeli pakiet zawiera już podpisu. |
| Timestamper | Adres URL serwera timestamping RFC 3161. |
| TimestampHashAlgorithm | Algorytm wyznaczania wartości skrótu używanego przez serwer znacznik czasu RFC 3161. Wartość domyślna to SHA256. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*. |

## <a name="examples"></a>Przykłady

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```