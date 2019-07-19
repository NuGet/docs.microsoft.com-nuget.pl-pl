---
title: Polecenie specyfikacji interfejsu wiersza polecenia NuGet
description: Dokumentacja polecenia NuGet. exe spec
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328274"
---
# <a name="spec-command-nuget-cli"></a>Spec — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** **obsługiwane wersje** tworzenia &bullet; pakietów: wszystkie

`.nuspec` Generuje plik dla nowego pakietu. W przypadku uruchomienia w tym samym folderze, w którym znajduje`.csproj`się plik `.fsproj`projektu ( `spec` , `.vbproj`,,) `.nuspec` , program tworzy plik z tokenami. Aby uzyskać dodatkowe informacje, zobacz [Tworzenie pakietu](../../create-packages/creating-a-package.md).

## <a name="usage"></a>Użycie

```cli
nuget spec [<packageID>] [options]
```

gdzie `<packageID>` jest opcjonalnym identyfikatorem pakietu, który ma `.nuspec` zostać zapisany w pliku.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| AssemblyPath | Określa ścieżkę do zestawu, który ma być używany dla metadanych. |
| Moc | Zastępuje istniejący `.nuspec` plik. |
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Help | Wyświetla informacje pomocy dla polecenia. |
| NonInteractive | Pomija monity o dane wejściowe lub potwierdzone przez użytkownika. |
| Verbosity | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*. |

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
