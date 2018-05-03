---
title: Omówienie obsługi źródła NuGet
description: Przegląd otwiera do obsługi własnych źródeł danych pakietu NuGet lub galerie lokalnie lub zdalnie.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 27f799ef69736c6cf718324e903049871430536f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="hosting-your-own-nuget-feeds"></a>Hosting NuGet własnych źródeł danych

Zamiast wprowadzania publicznie dostępnych pakietów, można zwolnić pakietów się tylko ograniczone odbiorców, takich jak organizacji lub grupy roboczej. Ponadto niektóre firmy mogą chcieć ograniczyć innych firm, które ma być biblioteki ich deweloperzy mogą przy użyciu, a w związku z tym bezpośrednie tych deweloperzy ma być rysowany od źródła pakietu ograniczone zamiast nuget.org.

W tym celu NuGet obsługuje Konfigurowanie źródła pakietów prywatnych w następujący sposób:

- Lokalne źródła danych: pakiety są po prostu dotyczącymi odpowiedniego sieciowego udziału plików, najlepiej przy użyciu `nuget init` i `nuget add` tworzenia struktury hierarchicznej folder (NuGet 3.3 +). Aby uzyskać więcej informacji, zobacz [lokalnych źródeł danych](../hosting-packages/local-feeds.md).
- NuGet.Server: Pakiety są udostępniane za pomocą lokalnego serwera HTTP. Aby uzyskać więcej informacji, zobacz [NuGet.Server](../hosting-packages/nuget-server.md).
- Galeria NuGet: Pakiety znajdują się na serwerze Internetu za pomocą [projektu galerii NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (witryną github.com). Galeria NuGet zawiera Zarządzanie użytkownikami i funkcje, takie jak szeroką gamę interfejsu użytkownika, który umożliwia wyszukiwanie i Przeglądanie pakietów z poziomu przeglądarki, podobnie jak nuget.org sieci web.

Dostępne są również kilka innych NuGet hosting produkty, które obsługują zdalnego prywatnych źródeł danych, takie jak następujące:

- [Visual Studio Team Services pakietu zarządzania](https://www.visualstudio.com/docs/package/nuget/publish), która jest również dostępna na Team Foundation Server 2017 lub nowszy.
- [MyGet](http://myget.org)
- [ProGet](http://inedo.com/proget) z Inedo
- [Serwer NuGet](http://nugetserver.net/), projekt społeczności z Inedo
- [Serwer NuGet (otwórz źródłowy)](http://nuget-server.net), podobnie jak w Inedo NuGet serwera implementację open source
- [Artifactory](https://www.jfrog.com/artifactory/) z JFrog.
- [Węzła](http://www.sonatype.org/nexus/) z Sonatype.
- [TeamCity](https://www.jetbrains.com/teamcity/) z JetBrains.

Niezależnie od tego, jak znajdują się pakiety, możesz uzyskać do nich dostęp przez dodanie ich do listy dostępnych źródeł w `NuGet.Config`. Można to zrobić w programie Visual Studio zgodnie z opisem w [źródła pakietów](../tools/package-manager-ui.md#package-sources), lub z wiersza polecenia przy użyciu [ `nuget sources` ](../tools/cli-ref-sources.md). Ścieżka do źródła może być nazwą ścieżki lokalnej folderu, Nazwa sieciowa lub adres URL.
