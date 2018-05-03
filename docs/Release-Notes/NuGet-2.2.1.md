---
title: Informacje o wersji NuGet 2.2.1
description: Informacje o wersji programu NuGet 2.2.1 tym — znane problemy, poprawki, dodatkowe funkcje i dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fddeb4e8c9fb2d85ba1876360862461e8ef025af
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-221-release-notes"></a>Informacje o wersji NuGet 2.2.1

[Informacje o wersji NuGet 2.2](../release-notes/nuget-2.2.md) | [NuGet 2.5 informacje o wersji](../release-notes/nuget-2.5.md)

NuGet 2.2.1 został wydany 15 lutego 2013.  Numer wersji rozszerzenia VS jest 2.2.40116.9051.

## <a name="localization-refresh"></a>Lokalizacja odświeżania
Gdy NuGet jest dostarczane jako część programu Visual Studio 2012, został pełni zlokalizowanych na angielski + 13 innych języków.  Od tego czasu NuGet 2.1 i 2.2 został wysłany, ale lokalizacji gdyby nie zostały odświeżone.  W wersji NuGet 2.2.1 odświeża naszych lokalizacji.

Interfejs użytkownika i konsoli programu PowerShell w narzędziu NuGet są zlokalizowane w następujących językach:

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

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Szablony Visual Studio obsługują wielu repozytoriów pakietu preinstalowane
Jeśli musisz utworzyć szablony programu Visual Studio, można użyć NuGet do [preinstalowane pakiety](../visual-studio-extensibility/visual-studio-templates.md) w ramach szablonu.  Do tej pory, ta funkcja ma ograniczenie wszystkich pakietów konieczne pochodzą z tego samego źródła.  Jednak dzięki NuGet 2.2.1 mogą mieć pakiety zainstalowane z wielu repozytoriów (w szablonie, VSIX lub folderu na dysku zdefiniowana w rejestrze).

Scenariusz głównego dla tej funkcji jest niestandardowe szablony projektów programu ASP.NET.  Wbudowane szablony ASP.NET użyć wstępnie zainstalowane pakiety ściąganie pakiety z dysku lokalnego.  Można teraz utworzyć szablon niestandardowy projektu ASP.NET, który wykorzystuje istniejące pakiety zainstalowane przez platformę ASP.NET, ale Dodaj dodatkowe pakiety NuGet do szablonu.

## <a name="bug-fixes"></a>Poprawki błędów
NuGet 2.2.1 obejmuje kilka poprawek błędów docelowych. Lista prac elementów ustalone w NuGet 2.2.1, sprawdź widok [NuGet Tracker problem w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).


## <a name="known-issues"></a>Znane problemy

Jeśli rozszerzania szablony projektów programu ASP.NET, wszystkie repozytoria preinstalowane pakietu należy używać tej samej wartości dla `isPreunzipped` atrybutu.
