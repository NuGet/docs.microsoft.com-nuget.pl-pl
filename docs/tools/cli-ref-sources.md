---
title: Polecenie źródeł NuGet interfejsu wiersza polecenia
description: Dokumentacja dotycząca nuget.exe źródeł polecenia
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7c416d92c11328ecb020154981b0ddcc5ba9c5e8
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818350"
---
# <a name="sources-command-nuget-cli"></a>sources command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** zużycie pakietu, publikowanie &bullet; **obsługiwane wersje:** wszystkie

Zarządza listy źródeł znajduje się w pliku konfiguracji zakresu użytkownika lub pliku konfiguracyjnym. Plik konfiguracji zakresu użytkownika znajduje się w `%appdata%\NuGet\NuGet.Config` (system Windows) i `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux).

Należy zauważyć, że adres URL źródła dla nuget.org `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Użycie

```cli
nuget sources <operation> -Name <name> -Source <source>
```

gdzie `<operation>` jest jednym z *listy, dodawanie, usuwanie, włączanie i wyłączanie,* lub *aktualizacji*, `<name>` to nazwa źródła i `<source>` jest adres URL źródła.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Format | Dotyczy `list` akcji i może być `Detailed` (ustawienie domyślne) lub `Short`. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| Hasło | Określa hasło do uwierzytelniania w źródle. |
| StorePasswordInClearText | Wskazuje, aby zapisać hasło w tekście niezaszyfrowane zamiast domyślnego zachowania przechowywania zaszyfrowane. |
| UserName | Określa nazwę użytkownika do uwierzytelniania w źródle. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*. |

> [!Note]
> Upewnij się, że dodanie hasła źródeł w tym samym kontekście użytkownika, ponieważ nuget.exe jest później używany do uzyskiwania dostępu do źródła pakietu. Hasło będzie przechowywany zaszyfrowany w pliku konfiguracji i mogły być odszyfrowane tylko w kontekście tego samego użytkownika, ponieważ został on zaszyfrowany. Tak na przykład jeśli używasz serwera kompilacji do przywracania pakietów NuGet, które muszą być szyfrowane hasło z tego samego użytkownika systemu Windows, uruchamiania zadań serwera kompilacji.

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
