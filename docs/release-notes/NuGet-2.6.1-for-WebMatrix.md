---
title: Informacje o wersji programu NuGet DataMatrix
description: Informacje o wersji programu NuGetobject dla programu WebMatrix, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de568829efd5060f3b02c3129ccfee2b27782821
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780416"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>Informacje o wersji programu NuGet DataMatrix

Informacje o wersji narzędzia [NuGet 2,6](../release-notes/nuget-2.6.md)  |  [Informacje o wersji narzędzia NuGet 2,7](../release-notes/nuget-2.7.md)

Zespół NuGet udostępnił zaktualizowane rozszerzenie Menedżera pakietów NuGet dla programu WebMatrix w dniu 26 marca 2014.  Tę aktualizację można zainstalować z [galerii rozszerzeń WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) , wykonując następujące czynności:

1. Otwórz WebMatrix 3
1. Kliknij ikonę rozszerzenia na Wstążce Narzędzia główne.
1. Wybierz kartę aktualizacje
1. Kliknij, aby zaktualizować Menedżera pakietów NuGet do
1. Zamknij i uruchom ponownie aplikację WebMatrix 3

## <a name="notable-changes"></a>Istotne zmiany

Ta aktualizacja rozszerzenia dotyczy dwóch największych problemów, w których użytkownicy mają zużywać pakiety NuGet w programie WebMatrix.  Pierwszy był błędem wersji schematu NuGet, a drugi był usterką wiodącą w przypadku bibliotek DLL o zerowej bajcie w `bin` folderze.

### <a name="nuget-schema-version-error"></a>Błąd wersji schematu NuGet

Ponieważ program WebMatrix 3 został wystawiony, w pakiecie NuGet wprowadzono nowe funkcje, które wymagają nowej wersji schematu dla pakietów NuGet.  Podczas próby zarządzania pakietami NuGet w witrynie sieci Web te nowe pakiety mogą prowadzić do błędów, które są widoczne w programie WebMatrix.

![Wystąpił błąd. Wersja schematu jest niezgodna. Uaktualnij pakiet NuGet do najnowszej wersji.](./media/NuGet-2.8/webmatrix-schema-version.png)

Ta Najnowsza wersja zapewnia zgodność z najnowszymi pakietami NuGet, zapobiegając wystąpieniu tego błędu. W programie WebMatrix można teraz zainstalować nowe wersje pakietów, w tym Microsoft. AspNet. Webpages.  Niektóre z tych pakietów korzystają z funkcji NuGet, takich jak [XDT config](../release-notes/nuget-2.6.md#xdt), które nie były obsługiwane w programie WebMatrix do chwili obecnej.

### <a name="zero-byte-dlls-in-bin-folder"></a>Zero-Byte bibliotek DLL w folderze bin

Niektórzy użytkownicy zgłosili, że po zainstalowaniu pakietów NuGet w programie WebMatrix, które zawierają biblioteki DLL, które są kopiowane do pliku bin, są wyświetlane w `bin` folderze jako pliki 0-bajtowe.  Spowoduje to przerwanie działania aplikacji w czasie wykonywania.

[Ten problem](https://nuget.codeplex.com/workitem/4060) został rozwiązany.

## <a name="other-recent-improvements"></a>Inne Ostatnie ulepszenia

Gdy Menedżer pakietów NuGet 2,8 został opublikowany dla programu Visual Studio, wydano również 2.5.0 Menedżera pakietów NuGet dla WebMatrix.  Chociaż został on wymieniony w [informacjach o wersji NuGet 2,8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), nie wspominamy o określonych nowych funkcjach wprowadzonych przez aktualizację.

### <a name="update-all"></a>Aktualizuj wszystkie

Teraz możesz zaktualizować wszystkie pakiety witryny sieci Web w jednym kroku.  Po otwarciu rozszerzenia NuGet w programie WebMatrix zostanie wyświetlona lista wszystkich pakietów z galerii, zainstalowanych i dostępnych aktualizacji.  Wcześniej każdy pakiet musiał zostać zaktualizowany pojedynczo, ale teraz istnieje przydatny przycisk "Aktualizuj wszystko", który jest wyświetlany na karcie Aktualizacje.

![Kliknij przycisk Aktualizuj wszystko, aby zaktualizować wszystkie pakiety z dostępnymi aktualizacjami](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>Zastąp istniejące pliki

W przypadku instalowania pakietów zawierających pliki, które już istnieją w witrynie sieci Web, pakiet NuGet zawsze po prostu zignorował te pliki (pozostawiając istniejące pliki).  Może to prowadzić do tego, że pakiet został zainstalowany lub zaktualizowany prawidłowo, gdy w rzeczywistości nie był.  Pakiet NuGet będzie teraz monitował o pliki do zastąpienia.

![Rozwiązywanie konfliktów plików](./media/NuGet-2.8/webmatrix-overwrite-file.png)
