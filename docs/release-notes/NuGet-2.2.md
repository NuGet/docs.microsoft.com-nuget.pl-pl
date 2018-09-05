---
title: Informacje o wersji 2,2 NuGet
description: Informacje o wersji programu NuGet 2.2, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a968ced3c58b7187a8bd9a8b14baa92f61f0140f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545995"
---
# <a name="nuget-22-release-notes"></a>Informacje o wersji 2,2 NuGet

[Informacje o wersji NuGet 2.1](../release-notes/nuget-2.1.md) | [informacjach o wersji NuGet 2.2.1](../release-notes/nuget-2.2.1.md)

NuGet 2.2 został wydany 12 grudnia 2012.

## <a name="visual-studio-quick-launch"></a>Visual Studio Quick Launch
Jedną z nowych funkcji, które zostało dodane w programie Visual Studio 2012 [okno dialogowe Szybkie uruchamianie](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box). NuGet 2.2 rozszerza to okno dialogowe, dzięki któremu zainicjować okno dialogowe Menedżer pakietów z wyszukiwane terminy wprowadzane w obszarze szybkiego uruchamiania. Na przykład wprowadzenie "jquery" w szybkie uruchamianie teraz obejmuje opcję w wynikach wyszukiwania pakietów NuGet dopasowania "jquery".

![NuGet w szybkiego uruchamiania programu Visual Studio](./media/quick-launch.png)

Wybranie tej opcji spowoduje uruchomienie standardowego NuGet pakietu Menedżera środowisko wyszukiwania dla terminu "jquery".

![Okno Menedżera pakietów NuGet wstępnie wypełnione](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Określ cały Folder zawartości pakietu
NuGet 2.2 umożliwia teraz określenie całego folderu w `<file>` elementu `.nuspec` pliku, aby uwzględnić wszystkie zawartość tego folderu. Na przykład poniżej spowoduje, że wszystkie skrypty w folderze skrypty pakietu mają zostać dodane do folderu contents\scripts, po zainstalowaniu pakietu do projektu.

```xml
<file src="scripts\" target="content\scripts"/>
```

**Aktualizuj 6/24/16: puste foldery w folderze "treści" są ignorowane, podczas instalowania pakietu.**

## <a name="known-issues"></a>Znane problemy

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>Instalacja pakietu nie powiedzie się projekty języka F # przy użyciu konsoli Menedżera pakietów
Podczas próby zainstalowania pakietu NuGet w projekcie programu F # za pomocą konsoli Menedżera pakietów, jest zgłaszany InvalidOperationException. Aktywnie współpracujemy z zespołu F #, aby rozwiązać ten problem, ale w międzyczasie, obejście polega na instalowanie pakietów NuGet w projektach F # za pomocą okno dialogowe Menedżer pakietów NuGet, a nie w konsoli. [Więcej informacji znajduje się w witrynie CodePlex](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Poprawki błędów
NuGet 2.2 obejmuje wiele poprawek błędów. Pełną listę prac elementy rozwiązane w NuGet 2.2, widok [NuGet narzędzie do śledzenia problemów w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
