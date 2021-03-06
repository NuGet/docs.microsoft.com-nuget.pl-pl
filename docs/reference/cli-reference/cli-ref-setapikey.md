---
title: Polecenie setapikey interfejsu wiersza polecenia NuGet
description: Odwołanie do nuget.exe setapikey polecenia
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3e0c2f84e336e0a642b1b5e815e74a1fb0878467
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780018"
---
# <a name="setapikey-command-nuget-cli"></a>setapikey — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** użycie pakietu, publikowanie &bullet; **obsługiwanych wersji:** wszystkie

Zapisuje klucz interfejsu API dla danego adresu URL serwera w `NuGet.Config` taki sposób, aby nie trzeba było go wprowadzać do kolejnych poleceń.

## <a name="usage"></a>Użycie

```cli
nuget setapikey <key> -Source <url> [options]
```

gdzie `<source>` identyfikuje serwer i `<key>` jest kluczem do zapisania. `<source>`W przypadku pominięcia zostanie założono NuGet.org. 

> [!NOTE]
> Klucz interfejsu API nie jest używany do uwierzytelniania w prywatnym źródle danych. Zapoznaj się z [ `nuget sources` poleceniem](../cli-reference/cli-ref-sources.md) , aby zarządzać poświadczeniami do uwierzytelniania ze źródłem.
> Klucze interfejsu API można uzyskać z poszczególnych serwerów NuGet. Aby utworzyć i zarządzać APIKeys for nuget.org, zobacz temat [pozyskiwanie-a-API-Key](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)

## <a name="options"></a>Opcje

- **`-ConfigFile`**

  Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.

- **`-?|-help`**

  Wyświetla informacje pomocy dla polecenia.

- **`-NonInteractive`**

  Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.

- **`-src|-Source`**

  Adres URL serwera, na którym klucz interfejsu API jest prawidłowy.

- **`-Verbosity [normal|quiet|detailed]`**

  Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
