---
title: Informacje o wersji 1.6 NuGet
description: Informacje o wersji w tym znanych problemów, poprawki, funkcje dodane i DCRs NuGet w wersji 1.6.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 351303ca3ae27a37c19e59d84dfc9b4629fe0ca5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549015"
---
 # <a name="nuget-16-release-notes"></a>Informacje o wersji 1.6 NuGet

[Informacje o wersji NuGet w wersji 1.5](../release-notes/nuget-1.5.md) | [informacjach o wersji NuGet w wersji 1.7](../release-notes/nuget-1.7.md)

NuGet w wersji 1.6 został wydany 13 grudnia 2011.

## <a name="known-installation-issue"></a>Problem z instalacją znane
Jeśli używasz programu VS 2010 z dodatkiem SP1, możesz napotkać błąd instalacji podczas próby uaktualnienia NuGet, jeśli masz starszą wersję zainstalowane.

Obejście polega na po prostu Odinstaluj NuGet, a następnie zainstalować go z galerii rozszerzeń programu VS.  Zobacz [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Aby uzyskać więcej informacji.

Uwaga: Jeśli program Visual Studio nie pozwalają na odinstalować rozszerzenie (przycisk Odinstaluj jest wyłączony), prawdopodobnie musisz ponownie program Visual Studio za pomocą polecenia "Uruchom jako Administrator".

## <a name="features"></a>Funkcje

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Obsługa Semantic Versioning i pakiety w wersjach wstępnych
NuGet w wersji 1.6 wprowadzono obsługę Semantic Versioning (SemVer). Więcej informacji o używaniu go SemVer [dokumentacja wersji](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>Za pomocą narzędzia NuGet bez sprawdzania, czy w pakietach (Przywracanie pakietu)
NuGet 1.6 teraz obsługuje najwyższej klasy dla przepływu pracy, w których NuGet nie są dodawane do kontroli źródła pakietów, ale zamiast tego są przywracane podczas kompilacji Jeśli brak. Aby uzyskać więcej informacji, przeczytaj [za pomocą NuGet, nie poświęcając pakietów do kontroli źródła](../consume-packages/packages-and-source-control.md) tematu.

### <a name="item-templates-that-install-nuget-packages"></a>Szablony elementów, które instalowanie pakietów NuGet
Opierając się na pracy do obsługi wstępnie zainstalowane pakietu NuGet szablony projektu Visual Studio, NuGet w wersji 1.6 dodają także obsługę szablony elementów Visual Studio. Szablony elementów może być skojarzony pakiety NuGet są instalowane podczas wywoływania szablon na liście.

Aby uzyskać więcej informacji na temat zmiany szablonu projektu/elementu, aby zainstalować pakiety NuGet, przeczytaj [pakietów w szablony programu Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) tematu.

### <a name="support-for-disabling-package-sources"></a>Obsługa wyłączenie źródła pakietów
Jeśli skonfigurowano wiele źródeł pakietów NuGet będzie wyglądać w każdej z nich pakietów podczas instalowania pakietu i jego zależności. Źródło pakietu, który nie działa dla jakiegoś powodu może poważnie wolno dół NuGet.

Przed NuGet w wersji 1.6 można usunąć źródła pakietu, ale musisz pamiętać, że szczegółowe informacje, gdy chcesz dodać go ponownie.

NuGet w wersji 1.6 umożliwia, usuwając zaznaczenie pola wyboru źródła pakietu, aby ją wyłączyć, ale zachować ją wokół.

![Wyłączanie pakietu](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Poprawki błędów
NuGet w wersji 1.6 miał daje w sumie 106 stałej elementów roboczych. 95 tych zostały sklasyfikowane jako usterki i 10 tych były funkcji.

Aby uzyskać pełną listę prac elementy rozwiązane w NuGet w wersji 1.6, widok [NuGet narzędzie do śledzenia problemów w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
