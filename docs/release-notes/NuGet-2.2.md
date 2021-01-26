---
title: Informacje o wersji narzędzia NuGet 2,2
description: Informacje o wersji programu NuGet 2,2, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780431"
---
# <a name="nuget-22-release-notes"></a>Informacje o wersji narzędzia NuGet 2,2

Informacje o wersji narzędzia [NuGet 2,1](../release-notes/nuget-2.1.md)  |  [Informacje o wersji pakietu NuGet 2.2.1](../release-notes/nuget-2.2.1.md)

Pakiet NuGet 2,2 został opublikowany 12 grudnia 2012.

## <a name="visual-studio-quick-launch"></a>Szybkie uruchamianie programu Visual Studio
Jedną z nowych funkcji, które zostały dodane w programie Visual Studio 2012, jest [okno dialogowe szybkiego uruchamiania](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box). Program NuGet 2,2 rozszerza to okno dialogowe, umożliwiając mu zainicjowanie okna dialogowego Menedżera pakietów z warunkami wyszukiwania wprowadzonymi w ramach szybkiego uruchamiania. Na przykład wprowadzenie "jQuery" w szybkim uruchomieniu zawiera teraz opcję w wynikach wyszukiwania pakietów NuGet pasujących do "jQuery".

![Pakiet NuGet w programie Visual Studio — Szybki Start](./media/quick-launch.png)

Wybranie tej opcji spowoduje uruchomienie standardowego środowiska wyszukiwania Menedżera pakietów NuGet dla terminu "jQuery".

![Wstępnie wypełnione okno dialogowe Menedżera pakietów NuGet](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Określ cały folder dla zawartości pakietu
Pakiet NuGet 2,2 umożliwia teraz określenie całego folderu w `<file>` elemencie `.nuspec` pliku w celu uwzględnienia całej zawartości tego folderu. Na przykład poniższe elementy spowodują dodanie wszystkich skryptów w folderze skryptów pakietu do folderu contents\scripts, gdy pakiet zostanie zainstalowany w projekcie.

```xml
<file src="scripts\" target="content\scripts"/>
```

**Aktualizacja 6/24/16: puste foldery w folderze "Content" są ignorowane podczas instalacji pakietu.**

## <a name="known-issues"></a>Znane problemy

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>Instalacja pakietu kończy się niepowodzeniem dla projektów języka F # w przypadku korzystania z konsoli Menedżera pakietów
Podczas próby zainstalowania pakietu NuGet w projekcie języka F # przy użyciu konsoli Menedżera pakietów jest zgłaszany InvalidOperationException. Aktywnie pracujemy z zespołem F # w celu rozwiązania problemu, ale w międzyczasie obejście polega na zainstalowaniu pakietów NuGet w projektach języka F # za pośrednictwem okna dialogowego Menedżera pakietów NuGet, a nie konsoli programu. [Więcej informacji można znaleźć w witrynie CodePlex](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Poprawki błędów
Pakiet NuGet 2,2 zawiera wiele poprawek błędów. Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 2,2, zobacz [Śledzenie problemów NuGet dla tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
