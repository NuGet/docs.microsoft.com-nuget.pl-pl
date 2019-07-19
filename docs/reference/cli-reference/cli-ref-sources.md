---
title: Polecenie źródeł interfejsu wiersza polecenia NuGet
description: Dokumentacja polecenia NuGet. exe sources
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328283"
---
# <a name="sources-command-nuget-cli"></a>sources command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** użycie pakietu, publikowanie &bullet; **obsługiwanych wersji:** wszystkie

Zarządza listą źródeł znajdujących się w pliku konfiguracyjnym zakresu użytkownika lub w określonym pliku konfiguracji. Plik konfiguracji zakresu użytkownika znajduje się w lokalizacji `%appdata%\NuGet\NuGet.Config` (Windows) i `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).

Należy pamiętać, że źródłowy adres URL dla `https://api.nuget.org/v3/index.json`NuGet.org to.

## <a name="usage"></a>Użycie

```cli
nuget sources <operation> -Name <name> -Source <source>
```

gdzie `<operation>` to jeden z elementów *list, Add, Remove, Enable, Disable* lub *Update*, `<name>` jest nazwą źródła i `<source>` jest adresem URL źródła. Jednocześnie można wykonywać tylko jedno źródło.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Format | Dotyczy akcji i może być `Detailed` (wartość domyślna) lub `Short`. `list` |
| Help | Wyświetla informacje pomocy dla polecenia. |
| NonInteractive | Pomija monity o dane wejściowe lub potwierdzone przez użytkownika. |
| Hasło | Określa hasło do uwierzytelniania ze źródłem. |
| StorePasswordInClearText | Wskazuje, że hasło ma być przechowywane w niezaszyfrowanym tekście zamiast w domyślnym zachowaniu zaszyfrowanego formularza. |
| UserName | Określa nazwę użytkownika do uwierzytelniania ze źródłem. |
| Verbosity | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*. |

> [!Note]
> Pamiętaj o dodaniu hasła źródeł w tym samym kontekście użytkownika, co plik NuGet. exe jest później używany do uzyskiwania dostępu do źródła pakietu. Hasło będzie przechowywane w pliku konfiguracyjnym i może zostać odszyfrowane tylko w tym samym kontekście użytkownika, w którym został zaszyfrowany. Na przykład w przypadku przywracania pakietów NuGet przy użyciu serwera kompilacji hasło musi być szyfrowane za pomocą tego samego użytkownika systemu Windows, w którym zostanie uruchomione zadanie serwera kompilacji.

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
