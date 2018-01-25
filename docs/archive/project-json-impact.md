---
title: "Project.JSON wpływ na autora pakietu NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Więcej informacji na temat formatu implementacja project.json w NuGet 3.x wpływa na autora pakietu, takich jak nieobsługiwane funkcje zawartości i pakietu."
keywords: "Pakiet NuGet i project.json, wpływ project.json tworzenia zagadnienia, funkcje project.json"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6104b4dac330869bc5724ffcf15cc0ac9ee26c1f
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="impact-of-projectjson-when-creating-packages"></a>Wpływ project.json podczas tworzenia pakietów

> [!Important]
> Ta zawartość jest przestarzały. Projekty powinny używać albo `packages.config` lub PackageReference formatów.

`project.json` System używany w NuGet 3 + wpływa na autora pakietu na kilka sposobów, zgodnie z opisem w poniższych sekcjach.

## <a name="changes-affecting-existing-packages-usage"></a>Zmiany mające wpływ na istniejące pakiety użycie

Tradycyjne pakiety NuGet obsługuje zestaw funkcji, które nie są przenoszone do przechodnie world.

### <a name="install-and-uninstall-scripts-are-ignored"></a>Instalowanie i odinstalowywanie skrypty są ignorowane.

Model przechodnie przywracania, opisanego w [rozpoznawania zależności](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference), nie ma pojęcie "Godzina instalacji pakietu". Pakiet jest obecny lub nie jest obecne, ale nie ma żadnych procesów spójne, gdy jest zainstalowany pakiet.

Ponadto Zainstaluj skrypty są obsługiwane tylko w programie Visual Studio. Inne IDEs musiały mock rozszerzalności programu Visual Studio interfejsu API na próbę obsługiwać te skrypty i nie obsługuje był dostępny w typowych edytory i narzędzia wiersza polecenia.

### <a name="content-transforms-are-not-supported"></a>Transformacje zawartości nie są obsługiwane.

Podobnie jak instalowanie skryptów, transformacje Uruchom w pakiecie instalacji i nie są zwykle idempotentności. Ponieważ nie istnieje już nie czas instalacji, XDT transformacji i podobne funkcje nie są obsługiwane i są ignorowane, jeśli taki pakiet jest używany w scenariuszu przechodnie.

### <a name="content"></a>Zawartość

Tradycyjne pakiety NuGet są wysyłania plików zawartości, takich jak kodu źródłowego i pliki konfiguracyjne. Są zwykle używane w przypadku dwóch scenariuszy:

1. Pliki początkowe upuścić na projektu, więc użytkownik może edytować je w późniejszym czasie. Typowym przykładem są pliki konfiguracji domyślnej.

1. Pliki zawartości są używane jako towarzyszami do zestawów zainstalowanych w projekcie. W tym przykładzie będzie używana przez zestaw obraz logo.

Obsługa zawartości jest obecnie wyłączona podobnych przyczyn dla skryptów i transformacje, ale trwa projektowania obsługę zawartości.

Zawartość plików może nadal znajdować się wewnątrz pakietów i są ignorowane obecnie, jednak użytkownik końcowy może nadal skopiuj je do odpowiednim miejscem.

Znajduje się propozycje ponownie Przywracanie plików zawartości i wykonaj jego postępu, w tym miejscu: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).

## <a name="impact-for-package-authors"></a>Wpływ dla autorów pakietu

Pakiety przy użyciu funkcji powyżej musi używać różnych mechanizmów. Najczęściej przydatne mechanizm ten będzie MSBuild celów/arkuszy właściwości, które w dalszym ciągu uzyskać w pełni obsługiwane. System kompilacji można wybrać do pobrania innych Konwencji w pakiecie. Jest to, jak docelowych elementów MSBuild są obsługiwane, jak również analizatory Roslyn. Istnieje możliwość tworzenia pakietów, które obsługuje cele i analizatorów dla `packages.config` i `project.json` scenariuszy.

Pakiety, które próbuje zmodyfikować projektu, aby ułatwić uruchamiania zwykle działają w bardzo ograniczony zestaw scenariusze, a zamiast tego powinien udostępnić plik readme lub wskazówki dotyczące sposobu używania pakietu.

Większość istniejących pakietów nie jest konieczna Użyj formatu pakietu opisane poniżej.

Format umożliwia natywnego zawartości jako pierwszej klasie scenariusza. Oznacza to, że zarządzane zestawy w zależności od bliski implementacje sprzętu na potrzeby wysłania binarne implementacje równolegle z zarządzanych zestawów oparte na platformie docelowej. Na przykład pakiet System.IO.Compression jest przy użyciu tej technologii. [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

W podsumowaniu Jeśli powyżej funkcji nie jest to konieczne, zalecamy spełni format istniejącego pakietu, format opisany jest obsługiwana tylko przez NuGet 3.x+.

Będzie można skompilować pakiety w celu pracy dla obu `packages.config` i `project.json` scenariuszy za pośrednictwem shimming, jednak często łatwiej jest po prostu struktury pakiety w tradycyjny sposób, bez przestarzałe funkcje wymienione powyżej.

## <a name="3x-package-format"></a>format pakietu 3.x

Format pakietu 3.x pozwala na kilka dodatkowych funkcji poza NuGet 2.x:

1. Definiowanie zestawu odwołania używany dla kompilacji i zestaw używany do środowiska uruchomieniowego na różnych platformach/urządzeń zestawy implementacji. Co pozwala korzystać z platformy określonych interfejsów API, zapewniając wspólnej powierzchni przez użytkowników. W szczególności w ten sposób zapisywania pośredniego bibliotek przenośnych łatwiejsze.

1. Umożliwia pakietów do tabeli przestawnej — na platformach np. systemy operacyjne i architektury Procesora.

1. Umożliwia rozdzielenie implementacji określonych platform do pakietów pomocnika.

1. Obsługa natywnego zależności jako pierwszej klasie obywateli.