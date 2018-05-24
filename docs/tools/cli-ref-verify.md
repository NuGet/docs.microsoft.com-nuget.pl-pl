---
title: Sprawdź NuGet interfejsu wiersza polecenia, polecenie
description: Dokumentacja dotycząca nuget.exe Sprawdź polecenie
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c80334104f7d8b2ccbf16ea2c11dc37b39408eeb
ms.sourcegitcommit: c8485dc61469511485367d2067b97d6f74b49f6e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/23/2018
---
# <a name="verify-command-nuget-cli"></a>verify command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** 4.6 +

Sprawdza, czy pakiet.

Weryfikacja podpisanych pakietów nie jest jeszcze obsługiwana w .NET Core, w obszarze Mono lub na różnych platformach z systemem innym niż Windows.

## <a name="usage"></a>Użycie

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

gdzie `<package(s)>` jest co najmniej jeden `.nupkg` plików.

## <a name="nuget-verify--all"></a>Sprawdź nuget — wszystkie

Określa, że wszystkie sprawdzenia możliwe powinien być wykonywany na pakietów.

## <a name="nuget-verify--signatures"></a>Sprawdź nuget - podpisów

Określa, należy wykonać weryfikacji podpisu pakietu.

## <a name="options-for-verify--signatures"></a>Opcje "Weryfikuj - podpisów"

| Opcja | Opis |
| --- | --- |
| CertificateFingerprint | Określa co najmniej jeden algorytm SHA-256 certyfikatu odciski palców certyfikatów (s), które podpisem pakiety muszą być podpisane przy. Odcisk palca certyfikatu algorytmu SHA-256 jest Skrót SHA-256 certyfikatu. Wielu danych wejściowych powinny być oddzielone średnikami. |

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.|
| ForceEnglishOutput | Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*. |

## <a name="examples"></a>Przykłady

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```