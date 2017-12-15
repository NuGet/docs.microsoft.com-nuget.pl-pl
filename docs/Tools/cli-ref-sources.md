---
title: "Polecenie źródła interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 997ce736-91ba-4cd2-88c9-b4b168e3130a
description: "Dokumentacja dotycząca nuget.exe źródeł polecenia"
keywords: "nuget źródeł odwołania, źródłem polecenia"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 52c46dba168e7395d50cb8d8f9775839389e614c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="sources-command-nuget-cli"></a>polecenie źródeł (NuGet CLI)

**Dotyczy:** zużycie pakietu, publikowanie &bullet; **obsługiwane wersje:** wszystkie

Zarządza listy źródeł znajduje się w `%AppData%\NuGet\NuGet.Config` lub określonego pliku konfiguracji.

## <a name="usage"></a>Użycie

```
nuget sources <operation> -Name <name> -Source <source>
```

gdzie `<operation>` jest jednym z *listy, dodawanie, usuwanie, włączanie i wyłączanie,* lub *aktualizacji*, `<name>` to nazwa źródła i `<source>` jest adres URL źródła.


## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | *(2.5 +)*  Pliku konfiguracji NuGet w celu zastosowania. Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany. |
| ForceEnglishOutput | *(3.5 +)*  Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Format | Dotyczy `list` akcji i może być `Detailed` (ustawienie domyślne) lub `Short`. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| Hasło | Określa hasło do uwierzytelniania w źródle. |
| StorePasswordInClearText | Wskazuje, aby zapisać hasło w tekście niezaszyfrowane zamiast domyślnego zachowania przechowywania zaszyfrowane. |
| UserName | Określa nazwę użytkownika do uwierzytelniania w źródle. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe (2.5 +)*. |

> [!Note]
> Upewnij się, że dodanie hasła źródeł w tym samym kontekście użytkownika, ponieważ nuget.exe jest później używany do uzyskiwania dostępu do źródła pakietu. Hasło będzie przechowywany zaszyfrowany w pliku konfiguracji i mogły być odszyfrowane tylko w kontekście tego samego użytkownika, ponieważ został on zaszyfrowany. Tak na przykład jeśli używasz serwera kompilacji do przywracania pakietów NuGet, które muszą być szyfrowane hasło z tego samego użytkownika systemu Windows, uruchamiania zadań serwera kompilacji.

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
