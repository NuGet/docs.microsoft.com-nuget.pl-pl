---
title: wpływ project.json na autorów pakietów NuGet
description: Szczegółowe informacje na temat implementacji pliku project.json w nuget 3.x wpływa na autorów pakietów, takich jak nieobsługiwał funkcje, zawartość i format pakietu.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 34b08f06f04efdcf7bf73efc2cbdb5a5494ae2d9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488197"
---
# <a name="impact-of-projectjson-when-creating-packages"></a>Wpływ pliku project.json podczas tworzenia pakietów

> [!Important]
> Ta zawartość jest przestarzała. Projekty powinny używać `packages.config` formatów lub PackageReference.

`project.json` System używany w NuGet 3+ wpływa na autorów pakietów na kilka sposobów, zgodnie z opisem w poniższych sekcjach.

## <a name="changes-affecting-existing-packages-usage"></a>Zmiany wpływające na użycie istniejących pakietów

Tradycyjne pakiety NuGet obsługują zestaw funkcji, które nie są przenoszone do świata przechodniów.

### <a name="install-and-uninstall-scripts-are-ignored"></a>Instalowanie i odinstalowywanie skryptów jest ignorowane

Przejściowy model przywracania, opisany w [rozdzielczości zależności,](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference)nie ma pojęcia "czas instalacji pakietu". Pakiet jest obecny lub nie obecny, ale nie ma spójnego procesu, który występuje po zainstalowaniu pakietu.

Ponadto skrypty instalacji były obsługiwane tylko w programie Visual Studio. Inne identyfikatory IDE musiały być szydercze z interfejsu API rozszerzalności programu Visual Studio, aby spróbować obsługiwać takie skrypty, a w typowych edytorach i narzędziach wiersza polecenia nie było dostępne żadne wsparcie.

### <a name="content-transforms-are-not-supported"></a>Transformacje zawartości nie są obsługiwane

Podobnie jak w instalowanych skryptach, transformacje są uruchamiane podczas instalowania pakietów i zazwyczaj nie są idempotentne. Ponieważ nie ma już czasu instalacji, XDT Transform i podobne funkcje nie są obsługiwane i są ignorowane, jeśli taki pakiet jest używany w scenariuszu przechodni.

### <a name="content"></a>Zawartość

Tradycyjne pakiety NuGet są wysyłka plików zawartości, takich jak kod źródłowy i pliki konfiguracyjne. Istnieją zazwyczaj używane w dwóch scenariuszach:

1. Początkowe pliki porzucone w projekcie, dzięki czemu użytkownik może edytować je w późniejszym czasie. Typowym przykładem są domyślne pliki konfiguracyjne.

1. Pliki zawartości używane jako towarzysze zestawów zainstalowanych w projekcie. Przykładem w tym miejscu może być obraz logo używany przez zespół.

Obsługa zawartości jest obecnie wyłączona z podobnych powodów dla skryptów i przekształceń, ale jesteśmy w trakcie projektowania obsługi zawartości.

Pliki zawartości mogą być nadal przenoszone wewnątrz pakietów i są obecnie ignorowane, jednak użytkownik końcowy nadal może skopiować je w odpowiednim miejscu.

Możesz zobaczyć jedną z propozycji przywrócenia plików zawartości i śledzić [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)jego postępy, tutaj: .

## <a name="impact-for-package-authors"></a>Wpływ na autorów pakietów

Pakiety korzystające z powyższych funkcji musiałyby korzystać z innego mechanizmu. Najczęściej przydatnym mechanizmem tego będzie cele/rekwizyty MSBuild, który nadal jest w pełni obsługiwany. System kompilacji można wybrać, aby podnieść inne konwencje w pakiecie. W ten sposób obsługiwane są obiekty docelowe MSBuild, a także analizatory Roslyn. Istnieje możliwość tworzenia pakietów, które obsługuje `packages.config` `project.json` obiekty docelowe i analizatory dla i scenariuszy.

Pakiety, które próbują zmodyfikować projekt w celu ułatwienia uruchamiania zazwyczaj działają w bardzo ograniczonym zestawie scenariuszy i zamiast tego powinny dostarczyć readme lub wskazówki dotyczące korzystania z pakietu.

Większość istniejących pakietów nie powinna używać formatu pakietu opisanego poniżej.

Format umożliwia natywną zawartość jako scenariusz pierwszej klasy. Oznacza to, że zestawy zarządzane zależą od blisko implementacji sprzętu do wysyłki implementacji binarnych wraz z zarządzanych zestawów opartych na platformie docelowej. Na przykład system.IO.Compression pakiet wykorzystuje tę technologię. [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

Podsumowując, jeśli powyższe funkcje nie są absolutnie konieczne, zaleca się trzymanie się istniejącego formatu pakietu, ponieważ format opisany w tym miejscu jest obsługiwany tylko przez NuGet 3.x+.

Byłoby możliwe do tworzenia pakietów `packages.config` do `project.json` pracy dla obu i scenariuszy poprzez shimming, jednak często łatwiej jest po prostu struktury pakietów tradycyjny sposób, bez przestarzałych funkcji wymienionych powyżej.

## <a name="3x-package-format"></a>Format pakietu 3.x

Format pakietu 3.x pozwala na kilka dodatkowych funkcji poza NuGet 2.x:

1. Definiowanie zestawu referencyjnego używanego do kompilacji i zestawu zestawów implementacji używanych w czasie wykonywania na różnych platformach/urządzeniach. Co pozwala na korzystanie z interfejsów API specyficznych dla platformy, zapewniając jednocześnie wspólną powierzchnię dla konsumentów. W szczególności ułatwia to pisanie pośrednich przenośnych bibliotek.

1. Umożliwia obracanie pakietów na platformach, takich jak systemy operacyjne lub architektura procesora.

1. Umożliwia oddzielenie implementacji specyficznych dla platformy do pakietów towarzyszących.

1. Obsługa zależności natywnych jako obywatel pierwszej klasy.
