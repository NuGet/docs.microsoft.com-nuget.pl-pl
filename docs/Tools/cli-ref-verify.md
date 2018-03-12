---
title: "Interfejs wiersza polecenia NuGet Sprawdź polecenie | Dokumentacja firmy Microsoft"
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Dokumentacja dotycząca nuget.exe Sprawdź polecenie"
keywords: "nuget zweryfikować odwołania, sprawdź, polecenie"
ms.reviewer:
- karann
- rmpablos
ms.openlocfilehash: 2747491eb35d8685a44e86fcc1b572013982c754
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/08/2018
---
# <a name="verify-command-nuget-cli"></a>Sprawdź polecenia (NuGet CLI)

**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** 4.6 +

Sprawdza, czy pakiet.

## <a name="usage"></a>Użycie

```cli
nuget verify <package(s)> [options]
```

gdzie `<package(s)>` jest co najmniej jeden `.nupkg` plików.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| Wszystkie | Określa, że wszystkie sprawdzenia możliwe powinien być wykonywany na pakietów. |
| CertificateFingerprint | Określa co najmniej jeden algorytm SHA-256 certyfikatu odciski palców certyfikatów (s), które podpisem pakiety muszą być podpisane przy. Odcisk palca certyfikatu algorytmu SHA-256 jest Skrót SHA-256 certyfikatu. Wielu danych wejściowych powinny być oddzielone średnikami. |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany. |
| ForceEnglishOutput | Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| Podpisy | Określa, należy wykonać weryfikacji podpisu pakietu. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*. |

## <a name="examples"></a>Przykłady

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```