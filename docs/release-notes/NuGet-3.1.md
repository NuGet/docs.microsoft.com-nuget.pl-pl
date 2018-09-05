---
title: Informacje o wersji 3.1 NuGet
description: Informacje o wersji programu NuGet 3.1, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 779567d94a5a9a1b3eacddaa4c882201a446cb4b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545350"
---
# <a name="nuget-31-release-notes"></a>Informacje o wersji 3.1 NuGet

[Informacje o wersji NuGet 3.0](../release-notes/nuget-3.0.0.md) | [informacjach o wersji NuGet 3.1.1](../release-notes/nuget-3.1.1.md)

NuGet 3.1 została wydana 27 lipca 2015 r. jako powiązane rozszerzenie do zestawu Universal Windows Platform SDK dla programu Visual Studio 2015. Dostarczona przez nas tej wersji przy użyciu zestawu SDK platformy Windows tak, aby środowisko programistyczne Windows można korzystać z zalet pracy dla wielu platform NuGet, który zostało wcześniej uruchomione. Ta wersja rozszerzenia NuGet jest dostępna tylko dla programu Visual Studio 2015.

Firma Microsoft zaleca tych deweloperów, które mają dostęp do aktualizacji galerii programu Visual Studio do najnowszej wersji, która jest dostępna, ponieważ obecnie publikujemy zawsze aktualizacji za pomocą poprawki i nowe funkcje.

## <a name="nuget-visual-studio-extension"></a>Rozszerzenie programu NuGet Visual Studio

Problemy i funkcje w tej wersji są oznaczone w serwisie GitHub przy użyciu [punktu kontrolnego "3.1 platformy uniwersalnej systemu Windows w wersji RTM przechodnie support"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) ogółem, firma Microsoft zamknięte 67 problemy w wersji 3.1.

### <a name="new-features"></a>Nowe funkcje

* `project.json` Obsługa pomocy technicznej Windows platformy uniwersalnej systemu Windows i program ASP.NET 5
* Instalacja pakietów przechodnich

Opis i definicji tych funkcji można znaleźć innym miejscu, w dokumentacji.

### <a name="deprecated"></a>przestarzałe

Następujące funkcje nie są już dostępne dla programu Visual Studio 2015:

* Nie można zainstalować pakietów poziomu rozwiązania

Następujące funkcje nie są już dostępne dla programu Visual Studio 2015 i projekty, które używają `project.json` specyfikacji

* `install.ps1` i `uninstall.ps1` — te skrypty będą ignorowane podczas instalowania pakietu, przywracanie, aktualizacji i Odinstaluj
* Transformacje konfiguracji zostaną zignorowane.
* Zawartość zostanie przekazane, ale nie są kopiowane do projektu.
    * Zespół dokłada starań, aby ponownie zaimplementować tę funkcję, Śledź dyskusję i postęp na: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Znane problemy

Wystąpiły szereg znanych problemów dostarczone w tej wersji.

* Instalacji w wersji 3.1 za pomocą zestawu Windows 10 SDK spowoduje obniżenia poziomu dowolnej wersji rozszerzenia NuGet, który został wcześniej zainstalowany

## <a name="nuget-command-line"></a>Wiersza polecenia NuGet

Plik wykonywalny wiersza polecenia NuGet został zaktualizowany i przeniesione do nowej lokalizacji dystrybucyjny wersji historycznych tego nuget.exe mogą w dalszym ciągu być udostępniane.  Można pobrać wersji 3.1 beta nuget.exe dla Windows na: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

Nowa lokalizacja dystrybucyjny znajduje się na hoście dist.nuget.org przy użyciu struktury folderów, który następuje po ten szablon:

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>Nowe funkcje

* nuget.exe można przywrócić i zainstaluj pakiety do projektów, które używają `project.json` pliku.
* nuget.exe mogą połączyć się i wykorzystywać protokołu NuGet w wersji 3 na: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Znane problemy ##

1.    Nie można wykonać pakiet względem `project.json` pliku — [928](https://github.com/NuGet/Home/issues/928)
2.    Nie jest obsługiwana w Mono - [1059](https://github.com/NuGet/Home/issues/1059)
3.    Element nie jest lokalizowany - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)
4.    Nie jest podpisany, podobnie jak istniejące http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)
