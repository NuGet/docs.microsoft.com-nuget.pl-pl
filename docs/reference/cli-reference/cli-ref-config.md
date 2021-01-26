---
title: Polecenie konfiguracji interfejsu wiersza polecenia NuGet
description: Informacje dotyczące polecenia nuget.exe config
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3d50c12e34f71d7a62fe177da1dbb33eb702347a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775965"
---
# <a name="config-command-nuget-cli"></a>config — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** wszystkie &bullet; **obsługiwane wersje**: wszystkie

Pobiera lub ustawia wartości konfiguracji NuGet. Aby uzyskać dodatkowe użycie, zobacz [typowe konfiguracje NuGet](../../consume-packages/configuring-nuget-behavior.md). Szczegółowe informacje na temat dozwolonych nazw kluczy można znaleźć w [dokumentacji pliku konfiguracji NuGet](../nuget-config-file.md).

## <a name="usage"></a>Użycie

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

gdzie `<name>` i `<value>` określić parę klucz-wartość, która ma zostać ustawiona w konfiguracji. Można określić dowolną liczbę par. Aby usunąć wartość, określ nazwę i `=` znak, ale nie wartości.

Aby uzyskać dozwolone nazwy kluczy, zobacz [Dokumentacja pliku konfiguracji programu NuGet](../nuget-config-file.md).

W programie NuGet 3.4 + `<value>` można używać [zmiennych środowiskowych](cli-ref-environment-variables.md).

## <a name="options"></a>Opcje


- **`AsPath`**

  Zwraca wartość konfiguracji jako ścieżkę, która jest ignorowana, gdy `-Set` jest używana.

- **`-ConfigFile`**

  Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.

- **`-?|-help`**

  Wyświetla informacje pomocy dla polecenia.

- **`-NonInteractive`**

  Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.

- **`-Set`**

  Jeden na więcej par klucz-wartość, które mają być ustawiane w konfiguracji.

- **`-Verbosity [normal|quiet|detailed]`**

  Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

### <a name="examples"></a>Przykłady

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
