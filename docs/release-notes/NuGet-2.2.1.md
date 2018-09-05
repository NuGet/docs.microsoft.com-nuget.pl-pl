---
title: Informacje o wersji NuGet 2.2.1
description: Informacje o wersji programu NuGet 2.2.1 tym — znane problemy, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: abbd3a9d9c51132477ceb236fed22cb63ccda209
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550701"
---
# <a name="nuget-221-release-notes"></a>Informacje o wersji NuGet 2.2.1

[Informacje o wersji NuGet 2.2](../release-notes/nuget-2.2.md) | [informacjach o wersji NuGet 2.5](../release-notes/nuget-2.5.md)

NuGet 2.2.1 15 lutego 2013 został wydany.  Numer wersji rozszerzenia programu VS jest 2.2.40116.9051.

## <a name="localization-refresh"></a>Lokalizacja odświeżania
Gdy NuGet jest dostarczana jako część programu Visual Studio 2012, w pełni został zlokalizowany do języka angielskiego + 13 innych języków.  Od tamtej pory NuGet 2.1 i 2.2 zostały wprowadzone do użytku, ale nie miał zostały odświeżone lokalizacji.  Wersji NuGet 2.2.1 odświeża naszych lokalizacji.

Konsoli programu PowerShell i interfejsu użytkownika NuGet są zlokalizowane w następujących językach:

1. Chiński uproszczony
1. Chiński (tradycyjny)
1. czeski
1. Angielski
1. francuski
1. niemiecki
1. Włoski
1. japoński
1. koreański
1. polski
1. portugalski (Brazylia)
1. Rosyjski
1. Hiszpański
1. turecki

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Szablony programu Visual Studio obsługują wiele repozytoriów preinstalowanych pakietu
W przypadku utworzenia szablonów programu Visual Studio, można użyć NuGet, aby [przed instalacją pakietów](../visual-studio-extensibility/visual-studio-templates.md) jako część szablonu.  Do tej pory ta funkcja ma ograniczenie, wszystkie pakiety wymagane pochodziły z tego samego źródła.  Jednak z NuGet 2.2.1 może mieć zainstalowane pakiety z wielu repozytoriów (w szablonie VSIX lub folderu na dysku, zdefiniowana w rejestrze).

Scenariusz głównego dla tej funkcji jest niestandardowe szablony projektów programu ASP.NET.  Wbudowane szablony platformy ASP.NET za pomocą pakietów wstępnie zainstalowane, ściąganie pakiety z dysku lokalnego.  Można teraz utworzyć szablonu niestandardowego projektu ASP.NET, który wykorzystuje istniejące pakiety instalowane przez platformę ASP.NET, ale Dodaj dodatkowe pakiety NuGet do szablonu.

## <a name="bug-fixes"></a>Poprawki błędów
NuGet 2.2.1 zawiera kilka poprawek błędów docelowych. Lista prac elementów rozwiązane w NuGet 2.2.1, sprawdź widok [NuGet narzędzie do śledzenia problemów w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).


## <a name="known-issues"></a>Znane problemy

Jeśli rozszerzania szablony projektów programu ASP.NET, wszystkie repozytoria pakiet wstępnie zainstalowane, należy użyć taką samą wartość `isPreunzipped` atrybutu.
