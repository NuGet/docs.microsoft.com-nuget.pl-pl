---
title: Polecenie setapikey interfejsu wiersza polecenia NuGet
description: Dokumentacja polecenia NuGet. exe setapikey
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e2119953e6d07cd3571f156fa0b2665de49f963
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383972"
---
# <a name="setapikey-command-nuget-cli"></a>setapikey — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** użycie pakietu, publikowanie &bullet; **obsługiwanych wersji:** wszystkie

Zapisuje klucz interfejsu API dla danego adresu URL serwera w `NuGet.Config`, aby nie trzeba było go wprowadzać do kolejnych poleceń.

## <a name="usage"></a>Pomiar

```cli
nuget setapikey <key> -Source <url> [options]
```

gdzie `<source>` identyfikuje serwer, a `<key>` jest kluczem lub hasłem do zapisania. W przypadku pominięcia `<source>` zostanie przyjęty nuget.org.

> [!NOTE]
> Klucz interfejsu API nie jest używany do uwierzytelniania w prywatnym źródle danych. Zapoznaj się z [`nuget sources` polecenie](../cli-reference/cli-ref-sources.md) , aby zarządzać poświadczeniami do uwierzytelniania ze źródłem.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony, używany jest `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla informacje pomocy dla polecenia. |
| NonInteractive | Pomija monity o dane wejściowe lub potwierdzone przez użytkownika. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*. |

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
