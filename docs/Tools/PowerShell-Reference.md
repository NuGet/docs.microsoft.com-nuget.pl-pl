---
title: NuGet w programie PowerShell | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/2/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: cd08b869-44c6-480e-90f7-494a6d08e6d0
description: "Pełną dokumentację poleceń programu PowerShell dostępne w konsoli Menedżera pakietów NuGet w programie Visual Studio."
keywords: "NuGet konsoli Menedżera pakietów, poleceń programu NuGet Powershell NuGet w programie PowerShell"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c0da5c88447784fdd49d824bbd03b11f73c22ebc
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="powershell-reference"></a>W programie PowerShell

Konsola Menedżera pakietów zawiera interfejsu programu PowerShell w programie Visual Studio w systemie Windows do interakcji z NuGet za pomocą określonych poleceń wymienionych poniżej. (Konsola nie jest obecnie dostępna w programie Visual Studio for Mac.) Przewodnik dotyczący za pomocą konsoli, zobacz [Konsola Menedżera pakietów](../tools/package-manager-console.md) tematu.

> [!Tip]
> Wszystkie polecenia programu PowerShell odnosić się tylko do użycia pakietu. Brak poleceń programu PowerShell odnoszą się do tworzenia i publikowania pakietów z wyjątkiem w zakresie, w jakim pakietu można też klient korzystający z innymi pakietami.

> [!Important]
> Polecenia wymienione w tym miejscu są specyficzne dla konsoli Menedżera pakietów w programie Visual Studio i różnią się od [pakietu administracyjnego modułu polecenia](https://msdn.microsoft.com/powershell/reference/6/packagemanagement/packagemanagement) dostępnych w środowisku PowerShell ogólne. Każde środowisko ma poleceń, które nie są dostępne w innych i poleceń o tej samej nazwie również może różnić się w ich określonych argumentów. Korzystając z konsoli zarządzania pakietów w programie Visual Studio, zastosowanie polecenia i argumentów opisane w niniejszym dokumencie obecny.

| Typowe polecenia | Opis | Wersja narzędzia NuGet |
| --- | --- | --- |
| [Pakiet instalacyjny](ps-ref-install-package.md) | Instaluje pakiet i jego zależności w projekcie. | Wszystkie |
| [Pakiet aktualizacji](ps-ref-update-package.md) | Aktualizuje pakiet i jego zależności lub wszystkie pakiety w projekcie. | Wszystkie |
| [Znajdź pakiet](ps-ref-find-package.md) | Wyszukuje źródło pakietu przy użyciu Identyfikatora pakietu lub słowa kluczowe. | 3.0+ |
| [Get pakietu](ps-ref-get-package.md) | Pobiera listę pakietów zainstalowanych w lokalnym repozytorium, lub wyświetla ich listę pakietów dostępnych ze źródła pakietu. | Wszystkie |

| Dodatkowej poleceń | Opis | Wersja narzędzia NuGet |
| --- | --- | --- |
| [Dodaj BindingRedirect](ps-ref-add-bindingredirect.md) | Sprawdza wszystkie zestawy w ścieżce wyjściowej dla projektu i dodaje przekierowania powiązania do `app.config` lub `web.config` w miarę potrzeby. | Wszystkie |
| [Get projektu](ps-ref-get-project.md) | Wyświetla informacje o domyślnych lub określony projekt. | 3.0+ |
| [Otwórz PackagePage](ps-ref-open-packagepage.md) | Uruchamia domyślnej przeglądarki z projektu, licencji lub adresu URL programu report nadużyć dla określonego pakietu. | Przestarzałe w 3.0 + |
| [Rejestr TabExpansion](ps-ref-register-tabexpansion.md) | Rejestruje rozszerzenia kartę parametrów polecenia umożliwiające tworzenie dostosowanego rozszerzenia dla wartości parametrów najczęściej używanych. | Wszystkie |
| [Synchronizacja pakietu](ps-ref-sync-package.md) | Pobierz wersję zainstalowanego pakietu z określony projekt i synchronizuje wersję z resztą projektów w rozwiązaniu. | 3.0+ |
| [Odinstaluj pakiet](ps-ref-uninstall-package.md) | Usuwa pakiet z projektu, opcjonalnie usunięcie jego zależności. | Wszystkie |

Pełne, szczegółowe pomocy w przypadku dowolnego z tych poleceń, w konsoli uruchom następujące polecenie z daną nazwą polecenia:

```ps
Get-Help <command> -full
```

Wszystkie polecenia konsoli Menedżera pakietów obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216):

- Debugowanie
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Pełny
- WarningAction
- WarningVariable

Aby uzyskać więcej informacji, zapoznaj się [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) w dokumentacji programu PowerShell.
