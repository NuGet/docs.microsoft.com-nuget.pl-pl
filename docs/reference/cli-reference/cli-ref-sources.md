---
title: Polecenie źródeł interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia nuget.exe sources
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 73c9cea8200a1ab1937d25a9a611ae7f2a943dba
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622593"
---
# <a name="sources-command-nuget-cli"></a>sources — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** użycie pakietu, publikowanie &bullet; **obsługiwanych wersji:** wszystkie

Zarządza listą źródeł znajdujących się w pliku konfiguracyjnym zakresu użytkownika lub w określonym pliku konfiguracji. Plik konfiguracji zakresu użytkownika znajduje się w lokalizacji `%appdata%\NuGet\NuGet.Config` (Windows) i `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).

Należy pamiętać, że źródłowy adres URL dla nuget.org to `https://api.nuget.org/v3/index.json` .

## <a name="usage"></a>Użycie

```cli
nuget sources <operation> -Name <name> -Source <source>
```

gdzie `<operation>` to jeden z elementów *list, Add, Remove, Enable, Disable* lub *Update*, `<name>` jest nazwą źródła i `<source>` jest adresem URL źródła. Jednocześnie można wykonywać tylko jedno źródło.

## <a name="options"></a>Opcje

- **`-ConfigFile`**

  Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.

- **`-Format`**

  Dotyczy `list` akcji i może być `Detailed` (wartość domyślna) lub `Short` .

- **`-?|-help`**

  Wyświetla informacje pomocy dla polecenia.

- **`-Name`**

  Nazwa źródła.

- **`-NonInteractive`**

  Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.

- **`-Password`**

  Określa hasło do uwierzytelniania ze źródłem.

- **`-src|-Source`**

  Ścieżka do źródła pakietu.

- **`-StorePasswordInClearText`**

  Wskazuje, że hasło ma być przechowywane w niezaszyfrowanym tekście zamiast w domyślnym zachowaniu zaszyfrowanego formularza.

- **`-UserName`**

  Określa nazwę użytkownika do uwierzytelniania ze źródłem.

- **`-ValidAuthenticationTypes`**

  Rozdzielana przecinkami lista prawidłowych typów uwierzytelniania dla tego źródła. Domyślnie wszystkie typy uwierzytelniania są prawidłowe. Przykład: `basic,negotiate`.

- **`-Verbosity [normal|quiet|detailed]`**

  Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .

> [!Note]
> Pamiętaj o dodaniu hasła źródeł pod tym samym kontekstem użytkownika co nuget.exe jest później używany do uzyskiwania dostępu do źródła pakietu. Hasło będzie przechowywane w pliku konfiguracyjnym i może zostać odszyfrowane tylko w tym samym kontekście użytkownika, w którym został zaszyfrowany. Na przykład w przypadku przywracania pakietów NuGet przy użyciu serwera kompilacji hasło musi być szyfrowane za pomocą tego samego użytkownika systemu Windows, w którym zostanie uruchomione zadanie serwera kompilacji.

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
