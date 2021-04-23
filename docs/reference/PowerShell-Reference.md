---
title: NuGet PowerShell Reference
description: Pełne odwołanie do poleceń programu PowerShell dostępnych w konsoli Menedżer pakietów NuGet w Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 7bc0395a98e75fe006e048b91d84cb5c17220161
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901892"
---
# <a name="powershell-reference"></a>Informacje dotyczące programu PowerShell

Konsola Menedżer pakietów udostępnia interfejs programu PowerShell w programie Visual Studio w systemie Windows do interakcji z programem NuGet za pomocą określonych poleceń wymienionych poniżej. (Konsola nie jest obecnie dostępna w programie Visual Studio dla komputerów Mac). Przewodnik dotyczący korzystania z konsoli programu można znaleźć w temacie Instalowanie pakietów i zarządzanie [nimi przy użyciu Menedżer pakietów Console.](../consume-packages/install-use-packages-powershell.md)

> [!Tip]
> Wszystkie polecenia programu PowerShell odnoszą się tylko do użycia pakietów. Żadne polecenia programu PowerShell nie odnoszą się do tworzenia i publikowania pakietów z wyjątkiem tego, że pakiet może być również konsumentem innych pakietów.

> [!Important]
> Polecenia wymienione w tym miejscu są specyficzne dla konsoli Menedżer pakietów w programie Visual Studio i różnią się od poleceń modułu [Zarządzanie pakietami](/powershell/module/packagemanagement) dostępnych w ogólnym środowisku programu PowerShell. W szczególności każde środowisko ma polecenia, które nie są dostępne w drugim, a polecenia o tej samej nazwie mogą również różnić się pod określonymi argumentami. W przypadku korzystania Zarządzanie pakietami Console w Visual Studio, mają zastosowanie polecenia i argumenty udokumentowane w tym temacie.

| Typowe polecenia | Opis | Wersja nuGet |
| --- | --- | --- |
| [Install-Package](ps-reference/ps-ref-install-package.md) | Instaluje pakiet i jego zależności w projekcie. | Wszystko |
| [Update-Package](ps-reference/ps-ref-update-package.md) | Aktualizuje pakiet i jego zależności lub wszystkie pakiety w projekcie. | Wszystko |
| [Find-Package](ps-reference/ps-ref-find-package.md) | Wyszukuje źródło pakietu przy użyciu identyfikatora pakietu lub słów kluczowych. | 3.0+ |
| [Get-Package](ps-reference/ps-ref-get-package.md) | Pobiera listę pakietów zainstalowanych w repozytorium lokalnym lub wyświetla listę pakietów dostępnych ze źródła pakietu. | Wszystko |

| Polecenia pomocnicze | Opis | Wersja nuGet |
| --- | --- | --- |
| [Add-BindingRedirect](ps-reference/ps-ref-add-bindingredirect.md) | Sprawdza wszystkie zestawy w ścieżce wyjściowej projektu i dodaje przekierowania powiązań do pliku lub w `app.config` `web.config` razie potrzeby. | Wszystko |
| [Get-Project](ps-reference/ps-ref-get-project.md) | Wyświetla informacje o domyślnym lub określonym projekcie. | 3.0+ |
| [Open-PackagePage](ps-reference/ps-ref-open-packagepage.md) | Uruchamia domyślną przeglądarkę z projektem, licencją lub adresem URL zgłaszania nadużycie dla określonego pakietu. | Przestarzałe w programie 3.0+ |
| [Register-TabExpansion](ps-reference/ps-ref-register-tabexpansion.md) | Rejestruje rozszerzenie karty dla parametrów polecenia, co umożliwia tworzenie dostosowanych rozszerzeń dla często używanych wartości parametrów. | Wszystko |
| [Sync-Package](ps-reference/ps-ref-sync-package.md) | Pobierz wersję zainstalowanego pakietu z określonego projektu i zsynchronizuj wersję z resztą projektów w rozwiązaniu. | 3.0+ |
| [Uninstall-Package](ps-reference/ps-ref-uninstall-package.md) | Usuwa pakiet z projektu, opcjonalnie usuwając jego zależności. | Wszystko |

Aby uzyskać pełną, szczegółową pomoc na temat dowolnego z tych poleceń w konsoli, po prostu uruchom następujące polecenie z nazwą polecenia:

```ps
Get-Help <command> -full
```

Wszystkie Menedżer pakietów konsoli programu obsługują następujące [typowe parametry programu PowerShell:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)

- Debugowanie
- Erroraction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Pełny
- Warningaction
- WarningVariable

Aby uzyskać szczegółowe informacje, zobacz [about_CommonParameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters) w dokumentacji programu PowerShell.