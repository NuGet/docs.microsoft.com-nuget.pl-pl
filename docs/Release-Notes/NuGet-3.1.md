---
title: Informacje o wersji NuGet 3.1 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informacje o wersji dla tym znanych problemów, poprawki, dodatkowe funkcje i dcr 3.1 NuGet."
keywords: NuGet 3.1 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a7aa43b8701b3bbef8f6ebce9a5d636ee1bc6abe
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-31-release-notes"></a>Informacje o wersji 3.1 NuGet

[Informacje o wersji NuGet 3.0](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 informacje o wersji](../release-notes/nuget-3.1.1.md)

NuGet 3.1 został wydany w dniu 27 lipca 2015 roku jako rozszerzenie powiązane do uniwersalnego zestawu SDK platformy Windows dla programu Visual Studio 2015. Dostarczana tej wersji przy użyciu zestawu SDK platformy systemu Windows tak, aby środowisko programistyczne systemu Windows można wykorzystać do pracy i platform NuGet, które zostało wcześniej uruchomione. Ta wersja rozszerzenia NuGet jest dostępna tylko dla programu Visual Studio 2015.

Firma Microsoft zaleca tych projektantów, którzy mają dostęp do galerii Visual Studio aktualizacji do najnowszej wersji, która jest dostępna, ponieważ firma Microsoft zawsze publikują aktualizacji za pomocą poprawki i nowe funkcje.

## <a name="nuget-visual-studio-extension"></a>Rozszerzenie programu NuGet dla programu Visual Studio

Problemy i funkcji w tej wersji są oznaczone w serwisie GitHub z [punkt kontrolny "3.1 Obsługa przechodnie RTM platformy uniwersalnej systemu Windows"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) w całości, możemy zamknięte 67 problemów w wersji 3.1.

### <a name="new-features"></a>Nowe funkcje

* `project.json`Obsługa pomocy technicznej systemu Windows i programu ASP.NET 5
* Instalacja pakietu przechodnie

Opis i definicji pojęć dotyczących tych funkcji można znaleźć w innym miejscu, w dokumentacji.

### <a name="deprecated"></a>Przestarzałe

Następujące funkcje nie są już dostępne dla programu Visual Studio 2015:

* Nie można zainstalować pakietów poziomu rozwiązania

Następujące funkcje nie są już dostępne dla programu Visual Studio 2015 i projekty, które używają `project.json` specyfikacji

* `install.ps1`i `uninstall.ps1` -te skrypty zostaną zignorowane podczas instalacji pakietu, przywracania, aktualizacji i odinstalowywania
* Transformacje konfiguracji zostaną zignorowane.
* Zawartość będzie wykonywane, ale nie został skopiowany do projektu.
    * Zespół pracuje nad ponownie zaimplementować tę funkcję, wykonaj dyskusji i postępu w: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Znane problemy

Wystąpiły znane problemy występujące w dostarczone w tej wersji.

* Instalacja wersji 3.1 z zestawu Windows 10 SDK będzie obniżyć dowolnej wersji rozszerzenia NuGet, który został wcześniej zainstalowany

## <a name="nuget-command-line"></a>NuGet wiersza polecenia

Plik wykonywalny wiersza polecenia NuGet został zaktualizowany i przeniesione do nowej lokalizacji dystrybucyjnego historię wersji nuget.exe mogą w dalszym ciągu udostępnione.  Możesz pobrać dla systemu operacyjnego Windows w wersji 3.1 beta nuget.exe: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

Nową lokalizację dystrybucyjnego znajduje się na tym hoście dist.nuget.org ze strukturą folder znajdujący się tego szablonu:

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>Nowe funkcje

* nuget.exe można przywrócić i zainstalować pakiety w projektach, które używają `project.json` pliku.
* łączyć się i korzystać z protokołu NuGet w wersji 3 w nuget.exe: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Znane problemy ##

1.    Nie można wykonać pakiet przed `project.json` pliku - [928](https://github.com/NuGet/Home/issues/928)
2.    Nie jest obsługiwany w jedno - [1059](https://github.com/NuGet/Home/issues/1059)
3.    Nie jest lokalizowany - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)
4.    Nie jest podpisany, podobnie jak istniejące http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)
