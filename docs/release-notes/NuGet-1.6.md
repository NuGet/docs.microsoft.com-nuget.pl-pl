---
title: Informacje o wersji narzędzia NuGet 1,6
description: Informacje o wersji programu NuGet 1,6, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 08b1cb3736e645d6efcc33f920f521c9c0fc7507
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777020"
---
 # <a name="nuget-16-release-notes"></a>Informacje o wersji narzędzia NuGet 1,6

Informacje o wersji narzędzia [NuGet 1,5](../release-notes/nuget-1.5.md)  |  [Informacje o wersji narzędzia NuGet 1,7](../release-notes/nuget-1.7.md)

Pakiet NuGet 1,6 został opublikowany 13 grudnia 2011.

## <a name="known-installation-issue"></a>Znany problem z instalacją
W przypadku korzystania z programu VS 2010 z dodatkiem SP1 można napotkać błąd instalacji podczas próby uaktualnienia narzędzia NuGet, jeśli jest zainstalowana starsza wersja.

Obejście polega na prostu odinstalować pakiet NuGet, a następnie zainstalować go z galerii rozszerzeń programu VS.  Aby uzyskać więcej informacji, zobacz <https://support.microsoft.com/kb/2581019>.

Uwaga: Jeśli program Visual Studio nie zezwoli na odinstalowanie rozszerzenia (przycisk Odinstaluj jest wyłączony), prawdopodobnie trzeba będzie ponownie uruchomić program Visual Studio za pomocą polecenia "Uruchom jako administrator".

## <a name="features"></a>Funkcje

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Obsługa wersji semantycznych i pakietów wstępnych
Pakiet NuGet 1,6 wprowadza obsługę wersji semantycznej (SemVer). Aby uzyskać więcej informacji na temat korzystania z SemVer, Przeczytaj [dokumentację dotyczącą wersji](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>Używanie narzędzia NuGet bez sprawdzania pakietów (Przywracanie pakietu)
Pakiet NuGet 1,6 ma teraz obsługę pierwszej klasy dla przepływu pracy, w którym pakiety NuGet nie są dodawane do kontroli źródła, ale w razie braku są przywracane w czasie kompilacji. Aby uzyskać więcej informacji, zapoznaj się z tematem [Używanie narzędzia NuGet bez zatwierdzania pakietów do kontroli źródła](../consume-packages/packages-and-source-control.md) .

### <a name="item-templates-that-install-nuget-packages"></a>Szablony elementów instalujących pakiety NuGet
Kompilowanie pracy w celu obsługi wstępnie zainstalowanego pakietu NuGet w szablonach projektów programu Visual Studio, NuGet 1,6 również dodaje obsługę szablonów elementów programu Visual Studio. Szablony elementów mogą mieć skojarzone pakiety NuGet, które są instalowane, gdy szablon jest wywoływany.

Aby uzyskać więcej informacji na temat zmiany szablonu projektu/elementu w celu zainstalowania pakietów NuGet, przeczytaj temat [pakiety w temacie szablony programu Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) .

### <a name="support-for-disabling-package-sources"></a>Obsługa wyłączania źródeł pakietów
W przypadku skonfigurowania wielu źródeł pakietów pakiet NuGet będzie wyglądał dla pakietów podczas instalacji pakietu i jego zależności. Źródło pakietu, które nie działa z jakiegoś powodu, może poważnie spowalniać działanie programu NuGet.

Przed pakietem NuGet 1,6 można było usunąć źródło pakietu, ale należy pamiętać o tym, że trzeba będzie je dodać z powrotem do programu.

Pakiet NuGet 1,6 umożliwia odszukanie źródła pakietu, aby je wyłączyć, ale zachować jego zachowanie.

![Wyłączanie pakietu](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Poprawki błędów
Pakiet NuGet 1,6 zawiera łącznie 106 elementów roboczych. 95 z tych elementów zostało sklasyfikowanych jako błędy i 10 z nich.

Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 1,6, zobacz [Śledzenie problemów NuGet dla tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
