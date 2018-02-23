---
title: "2.6.1 NuGet, aby uzyskać informacje o wersji programu WebMatrix | Dokumentacja firmy Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 119ea65b-b38b-4a8c-a4ed-6ea06f1aad09
description: "Informacje o wersji programu NuGet 2.6.1 dla programu WebMatrix, w tym znanych problemów, poprawki, dodatkowe funkcje i dcr."
keywords: "NuGet 2.6.1 informacje o wersji programu WebMatrix, poprawki, znanych problemów, nowe funkcje, dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 633b71011dd1bc897ad95fd706337cef3aeef34c
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/20/2018
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>2.6.1 NuGet, aby uzyskać informacje o wersji programu WebMatrix

[Informacje o wersji NuGet 2.6](../release-notes/nuget-2.6.md) | [NuGet 2.7 informacje o wersji](../release-notes/nuget-2.7.md)

Zespół NuGet wydany zaktualizowane rozszerzenie NuGet Package Manager dla programu WebMatrix 26 marca 2014 r.  Tę aktualizację można zainstalować z [galerii rozszerzeń programu WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) wykonując następujące czynności:

1. Otwórz program WebMatrix 3
1. Kliknij ikonę rozszerzeń na Wstążce głównej
1. Wybierz kartę aktualizacji
1. Kliknij, aby zaktualizować Menedżera pakietów NuGet do 2.6.1
1. Zamknij i uruchom ponownie program WebMatrix 3

## <a name="notable-changes"></a>Ważne zmiany

To rozszerzenie aktualizacji adresy dwa największych problemów użytkowników ma muszą ponosić odbierającą pakietów NuGet w programie WebMatrix.  Pierwszy błąd NuGet w wersji schematu, a drugi czasami jest usterka, co może prowadzić do biblioteki DLL zero bajtów w `bin` folderu.

### <a name="nuget-schema-version-error"></a>Błąd wersji schematu NuGet

Od czasu wydania programu WebMatrix 3, NuGet, która wymaga nowej wersji schematu do pakietów NuGet wprowadzono nowe funkcje.  Podczas próby Zarządzanie pakietów NuGet w witrynie sieci web, te nowe pakiety może prowadzić do błędów, które są wyświetlane w programie WebMatrix.

![Wystąpił błąd. Wersja schematu jest niezgodna. Należy uaktualnić program NuGet do najnowszej wersji.](./media/NuGet-2.8/webmatrix-schema-version.png)

Tej najnowszej wersji zapewnia zgodność z najnowszych pakietów NuGet, uniemożliwia wystąpienia tego błędu. Teraz można zainstalować nowe wersje pakietów w tym Microsoft.AspNet.WebPages w programie WebMatrix.  Niektóre z tych pakietów NuGet funkcji były używane takie jak [przekształca XDT config](../release-notes/nuget-2.6.md#xdt), który nie był obsługiwany w programie WebMatrix do tej pory.

### <a name="zero-byte-dlls-in-bin-folder"></a>Biblioteki DLL zero bajtów w pojemniku folderu

W przypadku niektórych użytkowników wykazały, że po instalowania NuGet pakietów w programie WebMatrix, obejmujących bibliotek DLL, które uzyskać skopiowane do bin, który Pokaż biblioteki dll w `bin` folderze co pliki 0 bajtów.  To spowoduje przerwanie aplikacji w czasie wykonywania.

[Ten problem](https://nuget.codeplex.com/workitem/4060) teraz został rozwiązany.

## <a name="other-recent-improvements"></a>Inne ulepszenia ostatnie

Po wydaniu został 2.8 Menedżera pakietów NuGet dla programu Visual Studio również opublikowano Menedżera pakietów NuGet 2.5.0 dla programu WebMatrix.  Gdy zostało to wymienione w [NuGet 2.8 wersji](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), firma Microsoft nie wspomina o konkretnym nowych funkcji tej aktualizacji wprowadzono.

### <a name="update-all"></a>Aktualizuj wszystkie

Można teraz zaktualizować wszystkich pakietów witryny sieci web w jednym kroku!  Po otwarciu rozszerzenie NuGet w programie WebMatrix zapoznać się z listą wszystkich pakietów w galerii, zainstalowani i sieci z dostępnych aktualizacji.  Wcześniej każdy pakiet musi zostać zaktualizowany pojedynczo, ale teraz znajduje się przydatne przycisk "Aktualizuj wszystkie", które są wyświetlane na karcie aktualizacje.

![Kliknij przycisk Aktualizuj wszystkie, można zaktualizować wszystkich pakietów o dostępności aktualizacji](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>Zastąpienie istniejących plików

Podczas instalowania pakietów zawierających pliki, które już istnieją w witrynie sieci web, NuGet zawsze w trybie dyskretnym zignorował tych plików (istniejące pliki pozostawiając bez zmian).  Może to prowadzić do wrażenie, że pakiet został zainstalowany ani poprawnie aktualizowany, gdy, w rzeczywistości nie był.  NuGet teraz wyświetli monit o podanie pliki zostaną zastąpione.

![Rozwiązywanie konfliktów plików](./media/NuGet-2.8/webmatrix-overwrite-file.png)
