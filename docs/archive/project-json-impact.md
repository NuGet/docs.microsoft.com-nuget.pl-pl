---
title: wpływ pliku Project. JSON na autorów pakietów NuGet
description: Szczegółowe informacje o tym, jak implementacja pliku Project. JSON w pakiecie NuGet 3. x ma wpływ na autorów pakietów, takich jak Nieobsługiwane funkcje, zawartość i format pakietu.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 34b08f06f04efdcf7bf73efc2cbdb5a5494ae2d9
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488197"
---
# <a name="impact-of-projectjson-when-creating-packages"></a>Wpływ pliku Project. JSON podczas tworzenia pakietów

> [!Important]
> Ta zawartość jest przestarzała. Projekty powinny używać `packages.config` formatów lub PackageReference.

`project.json` System używany w programie NuGet 3 + ma wpływ na autorów pakietów na kilka sposobów, zgodnie z opisem w poniższych sekcjach.

## <a name="changes-affecting-existing-packages-usage"></a>Zmiany wpływające na użycie istniejących pakietów

Tradycyjne pakiety NuGet obsługują zestaw funkcji, które nie są przenoszone na świecie przechodnie.

### <a name="install-and-uninstall-scripts-are-ignored"></a>Skrypty instalacji i dezinstalacji są ignorowane

Model przywracania przechodniego opisany w temacie [rozpoznawanie zależności](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference)nie ma koncepcji "czas instalacji pakietu". Pakiet jest obecny lub nie istnieje, ale nie ma spójnego procesu, który występuje po zainstalowaniu pakietu.

Ponadto skrypty instalacji były obsługiwane tylko w programie Visual Studio. Inne środowisk IDE musiały zasymulować interfejs API rozszerzalności programu Visual Studio, aby próbować obsługiwać takie skrypty, a żadne wsparcie nie było dostępne w popularnych edytorach i narzędziach wiersza polecenia.

### <a name="content-transforms-are-not-supported"></a>Przekształcenia zawartości nie są obsługiwane

Podobnie jak w przypadku instalacji skryptów, przekształcenia są uruchamiane podczas instalacji pakietu i nie są zwykle idempotentne. Ponieważ nie ma już czasu instalacji, XDT przekształcenia i podobne funkcje nie są obsługiwane i są ignorowane, jeśli taki pakiet jest używany w scenariuszu przechodnim.

### <a name="content"></a>Zawartość

Tradycyjne pakiety NuGet to wysyłanie plików zawartości, takich jak kod źródłowy i pliki konfiguracji. Są zwykle używane w dwóch scenariuszach:

1. Początkowe pliki zostały opuszczone do projektu, dzięki czemu użytkownik może je edytować w późniejszym czasie. Typowym przykładem są domyślne pliki konfiguracji.

1. Pliki zawartości używane jako pomocniki do zestawów zainstalowanych w projekcie. Przykładem może być obraz logo używany przez zestaw.

Obsługa zawartości jest obecnie wyłączona dla podobnych przyczyn dotyczących skryptów i transformacji, ale jesteśmy w trakcie projektowania obsługi zawartości.

Pliki zawartości nadal mogą być przenoszone w pakietach i są obecnie ignorowane, jednak użytkownik końcowy nadal może skopiować je do odpowiednich miejsc.

Możesz zobaczyć jedną z propozycji do przenoszenia plików zawartości i postępować zgodnie z postępem, tutaj: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).

## <a name="impact-for-package-authors"></a>Wpływ na autorów pakietów

Pakiety korzystające z powyższych funkcji będą musiały korzystać z innego mechanizmu. Najczęściej używanym mechanizmem jest to, że elementy docelowe i właściwości programu MSBuild, które nadal są w pełni obsługiwane. System kompilacji może wybrać inne konwencje w pakiecie. Jest to sposób, w jaki elementy docelowe programu MSBuild są obsługiwane, a także analizatory Roslyn. Istnieje możliwość kompilowania pakietów, które obsługują obiekty docelowe i analizatory `packages.config` dla `project.json` i scenariuszy.

Pakiety próbujące zmodyfikować projekt w celu ułatwienia uruchamiania zwykle działają w bardzo ograniczonym zestawie scenariuszy i powinny zawierać plik Readme lub wskazówki dotyczące sposobu korzystania z pakietu.

W przypadku większości istniejących pakietów nie należy używać formatu pakietu opisanego poniżej.

Format umożliwia zawartości natywnej jako scenariusza pierwszej klasy. Oznacza to, że zarządzane zestawy są zależne od implementacji sprzętowych, aby dostarczać implementacje binarne wraz z zestawami zarządzanymi opartymi na platformie docelowej. Na przykład pakiet System. IO. Compression korzysta z tej technologii. [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

Podsumowując, jeśli powyższe funkcje nie są absolutnie niezbędne, zalecamy naklejenie w istniejącym formacie pakietu, ponieważ format opisany tutaj jest obsługiwany tylko przez program NuGet 3. x +.

Możliwe jest skompilowanie pakietów do pracy w ramach obu `packages.config` `project.json` scenariuszy za pomocą zastępowanie podkładką:, jednak często prostsze jest jedynie struktury pakietów w tradycyjny sposób, bez przestarzałych funkcji wymienionych powyżej.

## <a name="3x-package-format"></a>format pakietu 3. x

Format pakietu 3. x umożliwia korzystanie z kilku dodatkowych funkcji poza pakietem NuGet 2. x:

1. Definiowanie zestawu odwołania używanego do kompilowania i zestawu zestawów implementacji używanych do środowiska uruchomieniowego na różnych platformach/urządzeniach. Dzięki temu można korzystać z interfejsów API specyficznych dla platformy, jednocześnie zapewniając wspólną powierzchnię dla klientów. W ten sposób pisanie pośrednich bibliotek przenośnych jest łatwiejsze.

1. Umożliwia umieszczanie pakietów na platformach, np. w systemach operacyjnych lub architekturach procesora CPU.

1. Umożliwia rozdzielenie implementacji specyficznych dla platformy na pakiety pomocnika.

1. Obsługa natywnych zależności jako obywatela pierwszej klasy.
