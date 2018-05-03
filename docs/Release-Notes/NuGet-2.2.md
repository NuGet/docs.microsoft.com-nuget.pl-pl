---
title: Informacje o wersji 2,2 NuGet
description: Informacje o wersji dla tym znanych problemów, poprawki, dodatkowe funkcje i dcr 2.2 NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 21f212de53da5faf1ec0762f97a840968b615b19
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-22-release-notes"></a>Informacje o wersji 2,2 NuGet

[Informacje o wersji NuGet 2.1](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 informacje o wersji](../release-notes/nuget-2.2.1.md)

NuGet 2.2 został wydany 12 grudnia 2012.

## <a name="visual-studio-quick-launch"></a>Visual Studio Quick Launch
Jedną z nowych funkcji, które dodano w programie Visual Studio 2012 został [okno dialogowe Szybkie uruchamianie](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box). NuGet 2.2 rozszerza tego okna dialogowego, dzięki któremu można zainicjować okno dialogowe menedżera pakietu z warunkami wyszukiwania w szybkie uruchamianie. Na przykład wprowadź "jquery" Szybkie uruchamianie teraz zawiera opcję w wynikach wyszukiwania dopasowania "jquery" pakietów NuGet.

![NuGet w szybkiego uruchamiania programu Visual Studio](./media/quick-launch.png)

Wybranie tej opcji spowoduje uruchomienie NuGet pakietu Menedżera wyszukiwania standardowo terminu "jquery".

![Okno dialogowe Menedżera pakietów NuGet wstępnie wypełnione](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Określ cały Folder zawartości pakietu
NuGet 2.2 można teraz określić cały folder w `<file>` elementu `.nuspec` pliku, aby uwzględnić wszystkie zawartość tego folderu. Na przykład następujące spowoduje, że wszystkie skrypty w folderze skryptów pakietu do dodania do folderu contents\scripts podczas instalowania pakietu w projekcie.

```xml
<file src="scripts\" target="content\scripts"/>
```

**Zaktualizuj 6/24/16: puste foldery w folderze "zawartość" są ignorowane, podczas instalowania pakietu.**

## <a name="known-issues"></a>Znane problemy

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>Instalacja pakietu nie powiedzie się dla projektów języka F # przy użyciu konsoli Menedżera pakietów
Podczas próby zainstalowania pakietu NuGet w projekcie F # za pomocą konsoli Menedżera pakietów, jest zgłaszany wyjątku InvalidOperationException. Obecnie pracujemy z team F #, aby rozwiązać ten problem, ale do tego czasu jest obejście można zainstalować pakietów NuGet do projektów F # za pomocą okna dialogowego Menedżera pakietów NuGet, a nie w konsoli programu. [Więcej informacji znajduje się w witrynie CodePlex](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Poprawki błędów
NuGet 2.2 zawiera wiele poprawek usterek. Pełną listę prac elementów usunięto w wersji NuGet 2.2, sprawdź widok [NuGet Tracker problem w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
