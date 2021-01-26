---
title: Informacje o wersji pakietu NuGet 2.2.1
description: Informacje o wersji programu NuGet 2.2.1, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6058fd596e32d38042aa75027640a5e5baca472
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776809"
---
# <a name="nuget-221-release-notes"></a>Informacje o wersji pakietu NuGet 2.2.1

Informacje o wersji narzędzia [NuGet 2,2](../release-notes/nuget-2.2.md)  |  [Informacje o wersji narzędzia NuGet 2,5](../release-notes/nuget-2.5.md)

Program NuGet 2.2.1 został opublikowany 15 lutego 2013.  Numer wersji rozszerzenia programu VS to 2.2.40116.9051.

## <a name="localization-refresh"></a>Odświeżanie lokalizacji
Gdy pakiet NuGet dostarczany jako część programu Visual Studio 2012, został w pełni zlokalizowany w języku angielskim + 13 innych językach.  Od tego czasu NuGet 2,1 i 2,2 zostały wysłane, ale lokalizacja nie została odświeżona.  Wydanie NuGet 2.2.1 spowoduje odświeżenie naszej lokalizacji.

Interfejs użytkownika i konsola programu PowerShell narzędzia NuGet są zlokalizowane w następujących językach:

1. Chiński (uproszczony)
1. Chiński (tradycyjny)
1. Czeski
1. Angielski
1. Francuski
1. niemiecki
1. Włoski
1. japoński
1. koreański
1. polski
1. portugalski (Brazylia)
1. Rosyjski
1. Hiszpański
1. turecki

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Szablony programu Visual Studio obsługują wiele preinstalowanych repozytoriów pakietów
W przypadku tworzenia szablonów programu Visual Studio można użyć narzędzia NuGet do [preinstalacji pakietów](../visual-studio-extensibility/visual-studio-templates.md) jako części szablonu.  Do tej pory ta funkcja miała ograniczenie, że wszystkie pakiety muszą pochodzić z tego samego źródła.  W przypadku programu NuGet 2.2.1 mimo że pakiety są instalowane z wielu repozytoriów (w ramach szablonu, VSIX lub folderu na dysku zdefiniowanym w rejestrze).

Głównym scenariuszem tej funkcji są niestandardowe szablony projektów ASP.NET.  Wbudowane szablony ASP.NET używają wstępnie zainstalowanych pakietów, pobierając pakiety z dysku lokalnego.  Teraz można utworzyć niestandardowy szablon projektu ASP.NET, który używa istniejących pakietów instalowanych przez ASP.NET, ale dodając do szablonu dodatkowe pakiety NuGet.

## <a name="bug-fixes"></a>Poprawki błędów
Pakiet NuGet 2.2.1 zawiera kilka dokierowanych poprawek błędów. Aby zapoznać się z listą elementów roboczych ustalonych w NuGet 2.2.1, zobacz [monitor problemów NuGet dla tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).


## <a name="known-issues"></a>Znane problemy

W przypadku rozszerzania szablonów projektów ASP.NET wszystkie wstępnie zainstalowane repozytoria pakietów muszą używać tej samej wartości `isPreunzipped` atrybutu.
