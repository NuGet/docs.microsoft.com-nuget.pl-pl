---
title: NuGet 2.6.1 dla programu WebMatrix informacje o wersji
description: Informacje o wersji programu NuGet 2.6.1 dla programu WebMatrix, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 10d80a921cbc34b537f91644da97efc44530fa75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550320"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>NuGet 2.6.1 dla programu WebMatrix informacje o wersji

[Informacje o wersji NuGet 2.6](../release-notes/nuget-2.6.md) | [informacjach o wersji NuGet w wersji 2.7](../release-notes/nuget-2.7.md)

Zespół NuGet wydany zaktualizowane rozszerzenie Menedżera pakietów NuGet dla programu WebMatrix 26 marca 2014.  Tę aktualizację można zainstalować z [galerii rozszerzeń programu WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) wykonując następujące czynności:

1. Otwórz program WebMatrix 3
1. Kliknij ikonę rozszerzenia na karcie wstążki Narzędzia główne
1. Wybierz kartę Aktualizacje
1. Kliknij, aby zaktualizować Menedżera pakietów NuGet do 2.6.1
1. Zamknij i ponownie uruchom program WebMatrix 3

## <a name="notable-changes"></a>Znaczące zmiany

To rozszerzenie aktualizacji adresy dwóch największych problemów użytkowników mają zmierzyła się dużo pakietów NuGet w programie WebMatrix.  Pierwszy wystąpił błąd w wersji schematu NuGet i drugim była usterkę, co prowadzi do dll zero bajtów w `bin` folderu.

### <a name="nuget-schema-version-error"></a>Błąd wersji schematu NuGet

Ponieważ program WebMatrix 3 został wydany, nowe funkcje zostały wprowadzone do pakietu NuGet, który wymaga nowej wersji schematu dla pakietów NuGet.  Podczas próby zarządzaniem Twoimi pakietami NuGet w witrynie sieci web, te nowe pakiety może prowadzić do błędów, które są wyświetlane w programie WebMatrix.

![Wystąpił błąd. Wersja schematu jest niezgodna. Uaktualnij NuGet do najnowszej wersji.](./media/NuGet-2.8/webmatrix-schema-version.png)

Najnowsza wersja zapewnia zgodność z najnowszych pakietów NuGet, uniemożliwiając wystąpienia tego błędu. Teraz można zainstalować nowe wersje pakietów w tym Microsoft.AspNet.WebPages w programie WebMatrix.  Niektóre z tych pakietów zostały przy użyciu funkcji NuGet takich jak [przekształca XDT config](../release-notes/nuget-2.6.md#xdt), który nie był obsługiwany w programie WebMatrix do tej pory.

### <a name="zero-byte-dlls-in-bin-folder"></a>DLL zero bajtów w pojemniku folderu

Niektórzy użytkownicy wykazały, że po zainstalowaniu NuGet pakietów w programie WebMatrix, który zawiera biblioteki dll, skopiowania do pojemnika, który show biblioteki dll w `bin` folderze co pliki 0 bajtów.  Spowoduje to podzielenie aplikacji w czasie wykonywania.

[Ten problem](https://nuget.codeplex.com/workitem/4060) teraz został rozwiązany.

## <a name="other-recent-improvements"></a>Inne ulepszenia ostatnie

Gdy 2.8 Menedżera pakietów NuGet został wydany dla programu Visual Studio, opublikowano także Menedżera pakietów NuGet 2.5.0 dla programu WebMatrix.  Gdy to zostało opisane w [informacjach o wersji programu NuGet 2.8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), firma Microsoft nie wspomnieć o konkretnym nowe funkcje tej aktualizacji wprowadzono.

### <a name="update-all"></a>Aktualizuj wszystkie

Można teraz zaktualizować wszystkich pakietów witryny sieci web w jednym kroku!  Po otwarciu rozszerzenie NuGet w programie WebMatrix, zobaczysz listę wszystkich pakietów w galerii, zainstalowanych i wiedzę dzięki dostępne aktualizacje.  Wcześniej każdy pakiet musi być aktualizowane pojedynczo, ale teraz ma przydatne przycisk "Aktualizuj wszystkie", który pojawia się na karcie aktualizacje.

![Kliknij przycisk Aktualizuj wszystkie, aby zaktualizować wszystkich pakietów wraz z dostępnymi aktualizacjami](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>Nadpisz istniejące pliki

Podczas instalowania pakietów, które zawierają pliki, które już istnieją w witrynie sieci web, NuGet ma zawsze dyskretnie ignorowana tych plików (autonomicznie pozostawiając istniejące pliki).  Może to prowadzić do wrażenie, że pakiet został zainstalowany lub poprawnie aktualizowany, gdy w rzeczywistości nie był to.  NuGet teraz wyświetli monit o pliki zostaną zastąpione.

![Rozwiązywanie konfliktów plików](./media/NuGet-2.8/webmatrix-overwrite-file.png)
