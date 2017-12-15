---
title: Interfejs wiersza polecenia NuGet Dodaj polecenie | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 4f68a016-ad4e-41fc-b869-88910fc5121e
description: "Dodaj odwołanie do nuget.exe — polecenie"
keywords: "Dodaj odwołanie nuget, należy dodać polecenie pakietu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: bf9a6e51dfbf1716ba40273487b76ae04c18e948
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="add-command-nuget-cli"></a>Dodawanie polecenia (NuGet CLI)

**Dotyczy**: publikowanie pakietu &bullet; **obsługiwane wersje**: 3.3 +

Dodaje określony pakiet do źródła pakietu protokołu HTTP (folder lub ścieżka UNC) w układzie hierarchicznym, w którym są tworzone foldery numeru identyfikator i wersję pakietu. Na przykład:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

Podczas przywracania lub aktualizowania źródle pakietu, hierarchiczna układ zapewnia znacznie wyższą wydajność.

Aby rozwinąć wszystkie pliki w pakiecie do docelowego źródła pakietu, należy użyć `-Expand` przełącznika. Zazwyczaj powoduje to dodatkowe podfolderów znajdujących się w lokalizacji docelowej, takie jak `tools` i `lib`.

## <a name="usage"></a>Użycie

```
nuget add <packagePath> -Source <sourcePath> [options]
```

gdzie `<packagePath>` jest ścieżka do pakietu, aby dodać, a `<sourcePath>` określa źródła pakietu na podstawie folderu, do którego zostanie dodany pakiet. Źródła HTTP nie są obsługiwane.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany.| 
| Rozwiń węzeł | Dodaje wszystkie pliki w pakiecie do źródła pakietu. |
| ForceEnglishOutput | *(3.5 +)*  Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
