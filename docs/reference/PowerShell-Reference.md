---
title: Dokumentacja programu PowerShell NuGet
description: Kompletne odwołanie do poleceń programu PowerShell dostępnych w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 142af9c4f7d25c3b0d986524313851cceb1e4c60
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328382"
---
# <a name="powershell-reference"></a>Dokumentacja programu PowerShell

Konsola Menedżera pakietów udostępnia interfejs programu PowerShell w programie Visual Studio w systemie Windows, który umożliwia współpracę z pakietem NuGet za pomocą określonych poleceń wymienionych poniżej. (Konsola nie jest obecnie dostępna w Visual Studio dla komputerów Mac). Przewodnik dotyczący korzystania z konsoli programu znajduje się w temacie [Instalowanie pakietów i zarządzanie nimi za pomocą konsoli Menedżera pakietów](../consume-packages/install-use-packages-powershell.md) .

> [!Tip]
> Wszystkie polecenia programu PowerShell odnoszą się tylko do zużycia pakietów. Żadne polecenia programu PowerShell nie są związane z tworzeniem i publikowaniem pakietów, z wyjątkiem przypadków, w których pakiet może być również odbiorcą innych pakietów.

> [!Important]
> Polecenia wymienione tutaj są specyficzne dla konsoli Menedżera pakietów w programie Visual Studio i różnią się od [poleceń modułu Zarządzanie pakietami](/powershell/module/packagemanagement/?view=powershell-6) , które są dostępne w ogólnym środowisku programu PowerShell. W każdym środowisku istnieją polecenia, które nie są dostępne w innym, a polecenia o tej samej nazwie mogą również różnić się do określonych argumentów. W przypadku korzystania z konsoli Zarządzanie pakietami w programie Visual Studio stosowane są polecenia i argumenty opisane w tym temacie.

| Typowe polecenia | Opis | Wersja programu NuGet |
| --- | --- | --- |
| [Install-Package](ps-reference/ps-ref-install-package.md) | Instaluje pakiet i jego zależności w projekcie. | Wszystkie |
| [Update-Package](ps-reference/ps-ref-update-package.md) | Aktualizuje pakiet i jego zależności lub wszystkie pakiety w projekcie. | Wszystkie |
| [Find-Package](ps-reference/ps-ref-find-package.md) | Wyszukuje źródło pakietu przy użyciu identyfikatora lub słów kluczowych pakietu. | 3.0+ |
| [Get-Package](ps-reference/ps-ref-get-package.md) | Pobiera listę pakietów zainstalowanych w repozytorium lokalnym lub wyświetla listę pakietów dostępnych ze źródła pakietu. | Wszystkie |

| Polecenia pomocnicze | Opis | Wersja programu NuGet |
| --- | --- | --- |
| [Add-BindingRedirect](ps-reference/ps-ref-add-bindingredirect.md) | Bada wszystkie zestawy w ścieżce wyjściowej projektu i dodaje przekierowania powiązań do lub `app.config` `web.config` w miarę potrzeb. | Wszystkie |
| [Get-Project](ps-reference/ps-ref-get-project.md) | Wyświetla informacje dotyczące domyślnego lub określonego projektu. | 3.0+ |
| [Open-PackagePage](ps-reference/ps-ref-open-packagepage.md) | Uruchamia domyślną przeglądarkę z adresem URL nadużycia projektu, licencji lub raportu dla określonego pakietu. | Przestarzałe w wersji 3.0 + |
| [Register-TabExpansion](ps-reference/ps-ref-register-tabexpansion.md) | Rejestruje rozwinięcie tabulatora dla parametrów polecenia, co pozwala na tworzenie dostosowanych rozszerzeń dla najczęściej używanych wartości parametrów. | Wszystkie |
| [Sync-Package](ps-reference/ps-ref-sync-package.md) | Pobierz wersję zainstalowanego pakietu z określonego projektu i zsynchronizuj wersję z pozostałymi projektami w rozwiązaniu. | 3.0+ |
| [Uninstall-Package](ps-reference/ps-ref-uninstall-package.md) | Usuwa pakiet z projektu, opcjonalnie usuwając jego zależności. | Wszystkie |

Aby uzyskać pełną, szczegółową pomoc dotyczącą dowolnego z tych poleceń w konsoli programu, po prostu uruchom następujące polecenie z nazwą polecenia:

```ps
Get-Help <command> -full
```

Wszystkie polecenia konsoli Menedżera pakietów obsługują następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216):

- Debugowanie
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Pełny
- WarningAction
- WarningVariable

Aby uzyskać szczegółowe informacje, zobacz [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) w dokumentacji programu PowerShell.
