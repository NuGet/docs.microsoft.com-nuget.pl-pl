---
title: Informacje o wersji narzędzia NuGet 3,1
description: Informacje o wersji programu NuGet 3,1, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776530"
---
# <a name="nuget-31-release-notes"></a>Informacje o wersji narzędzia NuGet 3,1

Informacje o wersji narzędzia [NuGet 3,0](../release-notes/nuget-3.0.0.md)  |  [Informacje o wersji NuGet 3.1.1](../release-notes/nuget-3.1.1.md)

Pakiet NuGet 3,1 został opublikowany w dniu 27 lipca 2015 jako dołączone rozszerzenie zestawu SDK platforma uniwersalna systemu Windows dla programu Visual Studio 2015. Ta wersja została dostarczona z zestawem SDK platformy Windows, aby środowisko programistyczne dla systemu Windows mogło korzystać z pracy międzyplatformowej NuGet, która została wcześniej uruchomiona. Ta wersja rozszerzenia NuGet jest dostępna tylko dla programu Visual Studio 2015.

Zalecamy, aby Ci deweloperzy mieli dostęp do aktualizacji galerii programu Visual Studio do najnowszej dostępnej wersji, ponieważ zawsze są publikowane aktualizacje z poprawkami błędów i nowymi funkcjami.

## <a name="nuget-visual-studio-extension"></a>Rozszerzenie NuGet programu Visual Studio

Problemy i funkcje w tej wersji są otagowane w witrynie GitHub z punktem 3,1 67 [kontrolnym "3,1 RTM platformy uwpe"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  .

### <a name="new-features"></a>Nowe funkcje

* `project.json` Obsługa systemów Windows platformy UWP i ASP.NET 5
* Instalacja pakietu przechodniego

Opisy i definicje tych funkcji można znaleźć w innym miejscu w dokumentacji.

### <a name="deprecated"></a>Przestarzałe

Następujące funkcje nie są już dostępne dla programu Visual Studio 2015:

* Nie można już zainstalować pakietów na poziomie rozwiązania

Następujące funkcje nie są już dostępne dla programu Visual Studio 2015 i projektów korzystających ze `project.json` specyfikacji

* `install.ps1` i `uninstall.ps1` — te skrypty zostaną zignorowane podczas instalowania pakietu, przywracania, aktualizowania i odinstalowywania
* Przekształcenia konfiguracji zostaną zignorowane
* Zawartość zostanie przeniesiona, ale nie zostanie skopiowana do projektu.
    * Zespół pracuje nad ponowną implementacją tej funkcji, postępuj zgodnie z dyskusjami i postępem: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Znane problemy

Wykryto kilka znanych problemów z tą wersją.

* Instalacja wersji 3,1 z zestawem SDK systemu Windows 10 spowoduje obniżenie wersji rozszerzenia NuGet, która została wcześniej zainstalowana

## <a name="nuget-command-line"></a>Wiersz polecenia NuGet

Plik wykonywalny wiersza polecenia NuGet został zaktualizowany i przeniesiony do nowej lokalizacji dystrybucyjnej, aby można było dalej udostępnić historyczne wersje nuget.exe.  Wersję 3,1 dla systemu Windows w nuget.exe wersji beta można pobrać pod adresem: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

Nowa lokalizacja dystrybucji znajduje się na hoście dist.nuget.org z strukturą folderów, która jest zgodna z tym szablonem:

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a>Nowe funkcje

* nuget.exe może przywrócić i zainstalować pakiety w projektach korzystających z `project.json` pliku.
* nuget.exe może nawiązać połączenie z protokołem NuGet v3 i korzystać z niego w: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Znane problemy ##

1.    Nie można wykonać pakietu dla `project.json` pliku- [928](https://github.com/NuGet/Home/issues/928)
2.    Nie jest obsługiwane w przypadku mono- [1059](https://github.com/NuGet/Home/issues/1059)
3.    Nie jest zlokalizowany- [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)
4.    Nie jest podpisany, podobnie jak istniejący http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)
