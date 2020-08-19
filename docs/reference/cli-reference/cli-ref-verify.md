---
title: Polecenie weryfikacji interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia nuget.exe verify
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 2c501753a16820c5d027441001561c6b637ccda9
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622606"
---
# <a name="verify-command-nuget-cli"></a>VERIFY — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** &bullet; **obsługiwane wersje pakietów:** 4.6 +

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

- **`-CertificateFingerprint`**

  Określa co najmniej jeden odcisk palca certyfikatu SHA-256 certyfikatów, które podpisane pakiety muszą być podpisane. Odcisk palca SHA-256 certyfikatu jest skrótem SHA-256 certyfikatu. Wielokrotne dane wejściowe powinny być rozdzielone średnikami.

## <a name="options"></a>Opcje

- **`-ConfigFile`**

  Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.

- **`-ForceEnglishOutput`**

  Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.

- **`-?|-help`**

  Wyświetla informacje pomocy dla polecenia.

- **`-NonInteractive`**

  Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.

- **`-Verbosity [normal|quiet|detailed]`**

  Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .

## <a name="examples"></a>Przykłady

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```