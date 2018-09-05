---
title: Sprawdź interfejs wiersza polecenia NuGet, polecenie
description: Dokumentacja dotycząca nuget.exe sprawdź polecenia
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 127f7a549c0a213f319c8820293646b302830436
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545216"
---
# <a name="verify-command-nuget-cli"></a>verify command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** 4.6 +

Weryfikuje pakietu.

Weryfikacja podpisanych pakietów nie jest jeszcze obsługiwana w platformę .NET Core, w ramach platformy Mono lub na platformach innych niż Windows.

## <a name="usage"></a>Użycie

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

gdzie `<package(s)>` ma jeden lub więcej `.nupkg` plików.

## <a name="nuget-verify--all"></a>Weryfikuj nuget — wszystkie

Określa, że wszystkie sprawdzenia możliwe powinno być przeprowadzane w pakiety.

## <a name="nuget-verify--signatures"></a>Sprawdzanie nuget — podpisów

Określa, że powinno być przeprowadzane Weryfikacja podpisu pakietu.

## <a name="options-for-verify--signatures"></a>Opcje "Weryfikuj - sygnatury"

| Opcja | Opis |
| --- | --- |
| CertificateFingerprint | Określa co najmniej jeden algorytm SHA-256 certyfikatu odcisków palców certyfikatów (s), które podpisane pakiety muszą być podpisane za pomocą. Odcisk palca certyfikatu SHA-256 jest Skrót SHA-256 wymagany certyfikat. Wielu danych wejściowych powinien być średnikami. |

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.|
| ForceEnglishOutput | Wymusza nuget.exe do uruchamiania przy użyciu kultury niezmiennej, oparte na język angielski. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*. |

## <a name="examples"></a>Przykłady

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```