---
title: Interfejs wiersza polecenia NuGet źródeł, polecenie
description: Dokumentacja dotycząca nuget.exe źródeł, polecenie
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610625"
---
# <a name="sources-command-nuget-cli"></a>sources command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** zużycie pakietów, publikowania &bullet; **obsługiwane wersje:** wszystkie

Zarządza listę identyfikatorów źródeł znajduje się w pliku konfiguracji zakresu użytkownika lub określonego pliku konfiguracji. Plik konfiguracji zakresu użytkownika znajduje się w `%appdata%\NuGet\NuGet.Config` (Windows) i `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).

Należy zauważyć, że adres URL źródła nuget.org `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Użycie

```cli
nuget sources <operation> -Name <name> -Source <source>
```

gdzie `<operation>` jest jednym z *listy, dodawanie, usuwanie, włączanie, wyłączanie,* lub *aktualizacji*, `<name>` jest nazwą źródła, a `<source>` jest adres URL źródła. Jednocześnie może działać na tylko jedno źródło.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Format | Dotyczy `list` akcji i może być `Detailed` (ustawienie domyślne) lub `Short`. |
| Help | Wyświetla Pomoc dla polecenia. |
| NonInteractive | Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia. |
| Hasło | Określa hasło do uwierzytelniania za pomocą źródła. |
| StorePasswordInClearText | Wskazuje, aby zapisać hasło nieszyfrowane tekstu zamiast domyślnego zachowania przechowywania w postaci zaszyfrowanej. |
| UserName | Określa nazwę użytkownika do uwierzytelniania za pomocą źródła. |
| Verbosity | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*. |

> [!Note]
> Upewnij się, że dodanie hasła źródeł, w tym samym kontekście użytkownika, ponieważ nuget.exe jest później używany do uzyskiwania dostępu do źródła pakietu. Hasło będzie przechowywany zaszyfrowany w pliku konfiguracji, a odszyfrować je mogą tylko w tym samym kontekście użytkownika, ponieważ został on zaszyfrowany. Dlatego na przykład używając serwera kompilacji do przywracania pakietów NuGet, które hasło musi być szyfrowana przy użyciu tego samego użytkownika Windows, na którym będzie uruchamiana zadanie serwera kompilacji.

Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
