---
title: Dokumentacja programu PowerShell NuGet
description: Kompletne odwołanie do poleceń programu PowerShell dostępnych w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 4f8b42847cbc155393fe6d2afbe2e0857b619da3
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236883"
---
# <a name="powershell-reference"></a>Informacje dotyczące programu PowerShell

Konsola Menedżera pakietów udostępnia interfejs programu PowerShell w programie Visual Studio w systemie Windows, który umożliwia współpracę z pakietem NuGet za pomocą określonych poleceń wymienionych poniżej. (Konsola nie jest obecnie dostępna w Visual Studio dla komputerów Mac). Przewodnik dotyczący korzystania z konsoli programu znajduje się w temacie [Instalowanie pakietów i zarządzanie nimi za pomocą konsoli Menedżera pakietów](../consume-packages/install-use-packages-powershell.md) .

> [!Tip]
> Wszystkie polecenia programu PowerShell odnoszą się tylko do zużycia pakietów. Żadne polecenia programu PowerShell nie są związane z tworzeniem i publikowaniem pakietów, z wyjątkiem przypadków, w których pakiet może być również odbiorcą innych pakietów.

> [!Important]
> Polecenia wymienione tutaj są specyficzne dla konsoli Menedżera pakietów w programie Visual Studio i różnią się od [poleceń modułu Zarządzanie pakietami](/powershell/module/packagemanagement/?view=powershell-6) , które są dostępne w ogólnym środowisku programu PowerShell. W każdym środowisku istnieją polecenia, które nie są dostępne w innym, a polecenia o tej samej nazwie mogą również różnić się do określonych argumentów. W przypadku korzystania z konsoli Zarządzanie pakietami w programie Visual Studio stosowane są polecenia i argumenty opisane w tym temacie.

| Typowe polecenia | Opis | Wersja programu NuGet |
| --- | --- | --- |
| [Install-Package](ps-reference/ps-ref-install-package.md) | Instaluje pakiet i jego zależności w projekcie. | Wszystko |
| [Update-Package](ps-reference/ps-ref-update-package.md) | Aktualizuje pakiet i jego zależności lub wszystkie pakiety w projekcie. | Wszystko |
| [Find-Package](ps-reference/ps-ref-find-package.md) | Wyszukuje źródło pakietu przy użyciu identyfikatora lub słów kluczowych pakietu. | 3.0 + |
| [Get-Package](ps-reference/ps-ref-get-package.md) | Pobiera listę pakietów zainstalowanych w repozytorium lokalnym lub wyświetla listę pakietów dostępnych ze źródła pakietu. | Wszystko |

| Polecenia pomocnicze | Opis | Wersja programu NuGet |
| --- | --- | --- |
| [Add-BindingRedirect](ps-reference/ps-ref-add-bindingredirect.md) | Bada wszystkie zestawy w ścieżce wyjściowej projektu i dodaje przekierowania powiązań do `app.config` lub w `web.config` miarę potrzeb. | Wszystko |
| [Get-Project](ps-reference/ps-ref-get-project.md) | Wyświetla informacje dotyczące domyślnego lub określonego projektu. | 3.0 + |
| [Open-PackagePage](ps-reference/ps-ref-open-packagepage.md) | Uruchamia domyślną przeglądarkę z adresem URL nadużycia projektu, licencji lub raportu dla określonego pakietu. | Przestarzałe w wersji 3.0 + |
| [Register-TabExpansion](ps-reference/ps-ref-register-tabexpansion.md) | Rejestruje rozwinięcie tabulatora dla parametrów polecenia, co pozwala na tworzenie dostosowanych rozszerzeń dla najczęściej używanych wartości parametrów. | Wszystko |
| [Sync-Package](ps-reference/ps-ref-sync-package.md) | Pobierz wersję zainstalowanego pakietu z określonego projektu i zsynchronizuj wersję z pozostałymi projektami w rozwiązaniu. | 3.0 + |
| [Uninstall-Package](ps-reference/ps-ref-uninstall-package.md) | Usuwa pakiet z projektu, opcjonalnie usuwając jego zależności. | Wszystko |

Aby uzyskać pełną, szczegółową pomoc dotyczącą dowolnego z tych poleceń w konsoli programu, po prostu uruchom następujące polecenie z nazwą polecenia:

```ps
Get-Help <command> -full
```

Wszystkie polecenia konsoli Menedżera pakietów obsługują następujące [typowe parametry programu PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters):

- Debugowanie
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Pełny
- WarningAction
- WarningVariable

Aby uzyskać szczegółowe informacje, zobacz [about_CommonParameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters) w dokumentacji programu PowerShell.