---
title: Polecenie setapikey interfejsu wiersza polecenia NuGet
description: Dokumentacja polecenia NuGet. exe setapikey
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e06cfb5b355dfae8104090db7babdecdf9e9fec1
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231230"
---
# <a name="setapikey-command-nuget-cli"></a>setapikey — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** użycie pakietu, publikowanie &bullet; **obsługiwanych wersji:** wszystkie

Zapisuje klucz interfejsu API dla danego adresu URL serwera w `NuGet.Config`, aby nie trzeba było go wprowadzać do kolejnych poleceń.

## <a name="usage"></a>Sposób użycia

```cli
nuget setapikey <key> -Source <url> [options]
```

gdzie `<source>` identyfikuje serwer, a `<key>` jest kluczem do zapisania. W przypadku pominięcia `<source>` zostanie przyjęty nuget.org. 

> [!NOTE]
> Klucz interfejsu API nie jest używany do uwierzytelniania w prywatnym źródle danych. Zapoznaj się z [`nuget sources` polecenie](../cli-reference/cli-ref-sources.md) , aby zarządzać poświadczeniami do uwierzytelniania ze źródłem.
> Klucze interfejsu API można uzyskać z poszczególnych serwerów NuGet. Aby utworzyć i zarządzać APIKeys for nuget.org, zobacz temat [Publikowanie-API-Key](../../quickstart/includes/publish-api-key.md)

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony, używany jest `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Wymusza uruchomienie NuGet. exe przy użyciu niezmiennej, opartej na języku angielskim kultury. |
| Pomoc | Wyświetla informacje pomocy dla polecenia. |
| NonInteractive | Pomija monity o dane wejściowe lub potwierdzone przez użytkownika. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*. |

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
