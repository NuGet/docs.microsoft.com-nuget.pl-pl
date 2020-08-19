---
title: Polecenie usunięcia interfejsu wiersza polecenia NuGet
description: Odwołanie do nuget.exe usuwania polecenia
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: bec1a778d4986a4cb7ee87e1ef8a98550c96ed57
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622866"
---
# <a name="delete-command-nuget-cli"></a>DELETE — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** &bullet; **obsługiwane wersje** publikowania pakietów: wszystkie

Usuwa pakiet ze źródła pakietu. W przypadku nuget.org polecenie Delete [wystawia pakiet](../../nuget-org/policies/deleting-packages.md).

## <a name="usage"></a>Użycie

```cli
nuget delete <packageID> <packageVersion> [options]
```

gdzie `<packageID>` i `<packageVersion>` Zidentyfikuj dokładny pakiet do usunięcia lub Wycofaj listy. Dokładne zachowanie zależy od źródła. Na przykład dla folderów lokalnych pakiet jest usuwany; dla nuget.org pakiet nie znajduje się na liście.

## <a name="options"></a>Opcje

- **`-ApiKey`**

  Klucz interfejsu API repozytorium docelowego. Jeśli nie istnieje, jest używany określony w pliku konfiguracji.

- **`-ConfigFile`**

  Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.

- **`-?|-help`**

  Wyświetla informacje pomocy dla polecenia.

- **`-NonInteractive`**

  Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.

 - **`-np|-NoPrompt`**

   Nie Monituj podczas usuwania.

 - **`-NoServiceEndpoint`** Nie dołącza "API/v2/Packages" do źródłowego adresu URL.

- **`-src|-Source`**

  Określa adres URL serwera. Adres URL nuget.org ma wartość `https://api.nuget.org/v3/index.json` . W przypadku prywatnych kanałów informacyjnych należy zastąpić nazwę hosta, na przykład *% hostname%/API/v3*.

- **`-Verbosity [normal|quiet|detailed]`**

  Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
