---
title: wpływ pliku Project.JSON na autorom pakietów NuGet
description: Szczegółowe informacje dotyczące sposobu wykonania pliku project.json w NuGet 3.x ma wpływ na pakiet autorów, takich jak nieobsługiwane funkcje, zawartość i format pakietu.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 8c85c1a89469c491c6be1f81961197450744349c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545576"
---
# <a name="impact-of-projectjson-when-creating-packages"></a>Wpływ pliku project.json podczas tworzenia pakietów

> [!Important]
> Ta zawartość jest przestarzały. Projekty powinny używać albo `packages.config` lub PackageReference podzielony na fragmenty.

`project.json` Systemu NuGet 3 + wpływa na autorom pakietów na kilka sposobów, zgodnie z opisem w poniższych sekcjach.

## <a name="changes-affecting-existing-packages-usage"></a>Zmiany mające wpływ na istniejące użycie pakietów

Tradycyjne pakiety NuGet obsługuje zestaw funkcji, które nie są przenoszone do świata przechodnie.

### <a name="install-and-uninstall-scripts-are-ignored"></a>Instalowanie i odinstalowywanie skrypty są ignorowane.

Model przechodnie przywracania, opisanego w [rozpoznawania zależności](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference), nie ma koncepcji "Godzina instalacji pakietu". Pakiet jest obecne lub nieobecne, ale nie ma żadnych procesów spójne, który występuje, gdy pakiet jest zainstalowany.

Ponadto Zainstaluj skrypty były obsługiwane tylko w programie Visual Studio. Inne środowiska IDE było testowanie rozszerzalności programu Visual Studio API próbę obsługiwać te skrypty, a nie był dostępny w standardowych edytorów i narzędzia wiersza polecenia.

### <a name="content-transforms-are-not-supported"></a>Przekształcenia zawartości nie są obsługiwane.

Podobnie jak Zainstaluj skrypty, przekształcenia systemem pakietu Zainstaluj i zazwyczaj nie są idempotentne. Ponieważ to już czas instalacji, Przekształć XDT podobne funkcje nie są obsługiwane i są ignorowane, jeśli taki pakiet jest używany w scenariuszu przechodnie.

### <a name="content"></a>Zawartość

Tradycyjne pakiety NuGet są wysyłania plików zawartości, takich jak kod źródłowy i pliki konfiguracyjne. Są zwykle używane w przypadku dwóch scenariuszy:

1. Pliki początkowe upuszczonego do projektu, dzięki czemu użytkownik może edytować je w późniejszym czasie. Typowym przykładem są pliki konfiguracji domyślnej.

1. Pliki zawartości są używane jako towarzyszami do zestawów zainstalowana w projekcie. W tym przykładzie będzie używane przez zestaw obrazu logo.

Pomoc techniczna dla zawartości jest obecnie wyłączony dla podobnych powodów, dla skryptów i transformacji, ale jesteśmy w trakcie projektowania obsługę zawartości.

Zawartości plików może nadal znajdować się wewnątrz pakietów i są ignorowane obecnie jednak użytkownik końcowy może nadal skopiuj je do odpowiednich miejscach.

Zobacz jeden z propozycje ponownie przeniesienie zawartości plików i postępuj zgodnie z jego postęp, w tym miejscu: [ https://github.com/NuGet/Home/issues/627 ](https://github.com/NuGet/Home/issues/627).

## <a name="impact-for-package-authors"></a>Znaczenie dla autorów pakietu

Pakiety przy użyciu powyższych funkcje musiałby użyć innego mechanizmu. Najczęściej przydatny mechanizm to będzie MSBuild celów/arkuszy właściwości, które w dalszym ciągu uzyskać w pełni obsługiwane. System kompilacji można wczytać innych Konwencji w pakiecie. Jest to, jak obsługiwanych elementów docelowych MSBuild oraz analizatorów Roslyn. Istnieje możliwość tworzenia pakietów, które obsługuje elementy docelowe i analizatory do równoległego `packages.config` i `project.json` scenariuszy.

Pakiety, które próbuje zmodyfikować projekt, aby ułatwić uruchamiania zwykle działa w bardzo ograniczony zestaw scenariuszy, a zamiast tego powinien udostępnić plik readme lub wskazówki dotyczące sposobu używania pakietu.

Większość istniejących pakietów nie powinni używać formatu pakietu opisane poniżej.

Format umożliwia natywnego zawartości najwyższej klasy scenariusza. Oznacza to, że zestawy zarządzane są zależne od blisko implementacji sprzętu w celu wysłania binarne implementacje wraz z zestawów zarządzanych, w oparciu o platformę docelową. Na przykład pakiet System.IO.Compression wykorzystywanych tej technologii. [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

W podsumowaniu Jeśli powyżej funkcji nie jest to konieczne, firma Microsoft zaleca wyobrazić za pomocą istniejący format pakietu formacie opisanym tutaj jest obsługiwana tylko przez NuGet 3.x+.

Będzie można skompilować pakiety w celu pracy dla obu `packages.config` i `project.json` scenariuszy za pomocą zastępowanie podkładką:, ale często łatwiej jest tylko sposób tradycyjny struktury pakiety, bez przestarzałych funkcji, o których wspomniano powyżej.

## <a name="3x-package-format"></a>format pakietu 3.x

Format pakietu 3.x pozwala na kilka dodatkowych funkcji poza NuGet 2.x:

1. Definiowanie zestawu odwołania używane dla kompilacji i zbiór zestawów implementacji używany dla środowiska uruchomieniowego na różnych platformach/urządzeniach. Co pozwala korzystać z platformy określonych interfejsów API przy jednoczesnym zapewnieniu wspólnych obszaru powierzchni przez użytkowników. W szczególności to sprawia, że pisanie pośrednich bibliotek przenośnych łatwiejsze.

1. Zezwala na pakiety do tabeli przestawnej — na platformach np. systemy operacyjne i architektury Procesora.

1. Umożliwia rozdzielenie implementacji określonego platformy do pakietów pomocnika.

1. Obsługuje zależności natywnych jako najwyższej klasy dla obywateli.
