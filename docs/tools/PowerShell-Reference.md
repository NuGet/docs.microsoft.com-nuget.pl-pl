---
title: Dokumentacja programu PowerShell NuGet
description: Pełną dokumentację poleceń programu PowerShell dostępnych w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 977e06d36962366abd69f1c7f21ef33eca4e5029
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426122"
---
# <a name="powershell-reference"></a>Dokumentacja programu PowerShell

Konsola Menedżera pakietów zapewnia interfejsu programu PowerShell w programie Visual Studio na Windows do interakcji z NuGet za pomocą określonych poleceń wymienionych poniżej. (Konsola nie jest obecnie dostępna w programie Visual Studio for Mac) Przewodnik dotyczący za pomocą konsoli, zobacz [instalowania i zarządzania pakietami przy użyciu programu PowerShell](../tools/package-manager-console.md) tematu.

> [!Tip]
> Wszystkie polecenia programu PowerShell odnosić się tylko do konsumpcji pakietu. Brak poleceń programu PowerShell odnoszą się do tworzenia i publikowania pakietów, z wyjątkiem w zakresie, w jakim pakietu może być również konsumenta innych pakietów.

> [!Important]
> Polecenia wymienione w tym miejscu są specyficzne dla konsoli Menedżera pakietów w programie Visual Studio i różnią się od [zarządzania pakietami modułu poleceń](/powershell/module/packagemanagement/?view=powershell-6) dostępnych w środowisku PowerShell ogólne. Każde środowisko ma polecenia, które nie są dostępne w drugim i poleceń o takiej samej nazwie może też różnią się w ich określonych argumentów. Korzystając z konsoli zarządzania pakietami w programie Visual Studio, mają zastosowanie polecenia i argumentów opisane w tym temacie obecne.

| Typowe polecenia | Opis | NuGet w wersji |
| --- | --- | --- |
| [Install-Package](ps-ref-install-package.md) | Instaluje pakiet i jego zależności w projekcie. | Wszystkie |
| [Update-Package](ps-ref-update-package.md) | Aktualizuje pakiet i jego zależności lub wszystkich pakietów w projekcie. | Wszystkie |
| [Find-Package](ps-ref-find-package.md) | Przeszukuje źródło pakietu przy użyciu Identyfikatora pakietu lub słów kluczowych. | 3.0+ |
| [Get-Package](ps-ref-get-package.md) | Pobranie listy pakietów zainstalowanych w lokalnym repozytorium, lub wyświetla ich listę pakietów, które są dostępne ze źródła pakietu. | Wszystkie |

| Dodatkowych poleceń | Opis | NuGet w wersji |
| --- | --- | --- |
| [Add-BindingRedirect](ps-ref-add-bindingredirect.md) | Sprawdza, czy wszystkie zestawy w ramach ścieżki wyjściowej dla projektu, a następnie dodaje przekierowania powiązań do `app.config` lub `web.config` w miarę potrzeby. | Wszystkie |
| [Get-Project](ps-ref-get-project.md) | Wyświetla informacje o domyślnej lub określony projekt. | 3.0+ |
| [Open-PackagePage](ps-ref-open-packagepage.md) | Uruchamia domyślną przeglądarkę z projektem, licencji lub adres URL do raportu nadużyć dla określonego pakietu. | Przestarzałe w 3.0 + |
| [Register-TabExpansion](ps-ref-register-tabexpansion.md) | Rejestruje rozszerzenia karty dla parametrów polecenia, co pozwala na tworzenie niestandardowych rozszerzeń dla wartości najczęściej używanych parametrów. | Wszystkie |
| [Sync-Package](ps-ref-sync-package.md) | Pobierz wersję zainstalowanego pakietu z określony projekt i synchronizuje wersji w pozostałej części projektów w rozwiązaniu. | 3.0+ |
| [Uninstall-Package](ps-ref-uninstall-package.md) | Usuwa pakiet z projektem, opcjonalnie usunięcie jego zależności. | Wszystkie |

Aby uzyskać pełne, szczegółowe uzyskać pomoc dotyczącą dowolnego z tych poleceń w konsoli uruchom następujące polecenie z nazwą polecenia w danym:

```ps
Get-Help <command> -full
```

Wszystkie polecenia konsoli Menedżera pakietów obsługują następujące elementy [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216):

- Debugowanie
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Pełny
- WarningAction
- WarningVariable

Aby uzyskać szczegółowe informacje, zapoznaj się [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) w dokumentacji programu PowerShell.
