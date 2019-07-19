---
title: Polecenie weryfikacji interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia VERIFY. exe programu NuGet
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9510f7323fe0cb860e0dbde51c1eda761846ee27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328253"
---
# <a name="verify-command-nuget-cli"></a>verify command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** **obsługiwane wersje** pakietów &bullet; : 4.6 +

Weryfikuje pakiet.

Weryfikacja podpisanych pakietów nie jest jeszcze obsługiwana w programie .NET Core, w obszarze mono lub na platformach innych niż Windows.

## <a name="usage"></a>Użycie

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

gdzie `<package(s)>` jest co najmniej jeden `.nupkg` plik.

## <a name="nuget-verify--all"></a>Weryfikacja NuGet — wszystkie

Określa, że wszystkie możliwe weryfikacje powinny być wykonywane na pakietach.

## <a name="nuget-verify--signatures"></a>Weryfikacja przez pakiet NuGet — sygnatury

Określa, że należy przeprowadzić weryfikację podpisu pakietu.

## <a name="options-for-verify--signatures"></a>Opcje "Weryfikuj sygnaturę"

| Opcja | Opis |
| --- | --- |
| CertificateFingerprint | Określa co najmniej jeden odcisk palca certyfikatu SHA-256 certyfikatów, które podpisane pakiety muszą być podpisane. Odcisk palca SHA-256 certyfikatu jest skrótem SHA-256 certyfikatu. Wielokrotne dane wejściowe powinny być rozdzielone średnikami. |

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).|
| ForceEnglishOutput | Wymusza uruchomienie NuGet. exe przy użyciu niezmiennej, opartej na języku angielskim kultury. |
| Help | Wyświetla informacje pomocy dla polecenia. |
| Verbosity | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*. |

## <a name="examples"></a>Przykłady

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```