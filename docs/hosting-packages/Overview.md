---
title: Omówienie obsługi źródła NuGet
description: Przegląd zostanie otwarta do hostowania własnych kanały informacyjne pakietu NuGet lub we własnych galeriach, lokalnie lub zdalnie.
author: karann-msft
ms.author: karann
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: f05c3a7a51bdc0760097422004cfc4339bf9ee2c
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426606"
---
# <a name="hosting-your-own-nuget-feeds"></a>Hosting NuGet własne źródła danych

Zamiast udostępniania pakietów publicznie, możesz chcieć wersji pakietów wyłącznie ograniczonej grupie osób, takich jak Twojej organizacji lub grupy roboczej. Ponadto niektóre firmy mogą chcieć ograniczyć bibliotek innych firm, które może używać deweloperów, a ten sposób kierowania tych deweloperów, które ma być rysowany od źródła pakietu ograniczona, a nie adres nuget.org.

W tych celach NuGet obsługuje konfigurowanie prywatnych źródeł pakietów w następujący sposób:

- Lokalne źródło danych: Pakiety po prostu są umieszczane w odpowiedniej sieci udziału plików, najlepiej przy użyciu `nuget init` i `nuget add` do utworzenia hierarchicznej struktury folderów (NuGet 3.3 +). Aby uzyskać więcej informacji, zobacz [ze źródeł lokalnych](../hosting-packages/local-feeds.md).
- NuGet.Server: Pakiety są udostępniane za pośrednictwem lokalnego serwera HTTP. Aby uzyskać więcej informacji, zobacz [NuGet.Server](../hosting-packages/nuget-server.md).
- Galeria NuGet: Pakiety są hostowane w serwera internetowego przy użyciu [projektu galerii NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com). Galeria NuGet zawiera zarządzania użytkownikami i ich funkcje, takie jak rozbudowana interfejsu użytkownika, która umożliwia wyszukiwanie i eksplorowanie pakietów z przeglądarki, podobnie jak nuget.org.

Dostępne są również kilka innych NuGet hostingu produktami, które obsługują zdalny prywatnej źródła danych, takie jak następujące:

- [Systemu Azure](https://www.visualstudio.com/docs/package/nuget/publish), który jest także dostępny w Team Foundation Server 2017 i nowsze.
- [MyGet](http://myget.org)
- [ProGet](http://inedo.com/proget) z Inedo
- [Rejestr pakiet GitHub](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)
- [Serwer NuGet](http://nugetserver.net/), to projekt Społecznościowy z Inedo
- [Serwer NuGet (Otwórz źródło)](http://nuget-server.net), podobnie jak serwer NuGet Inedo przez implementację typu open-source
- [LiGet](https://github.com/ai-traders/liget), implementacją open source serwera NuGet w wersji 2, który jest uruchamiany na kestrel na platformie docker
- [BaGet](https://github.com/loic-sharma/BaGet), implementacją open source serwera NuGet w wersji 3 oparta na programie ASP.NET Core
- [Sleet](https://github.com/emgarten/sleet), statycznej NuGet w wersji 3 typu open-source kanału informacyjnego generator
- [Artifactory](https://www.jfrog.com/artifactory/) z JFrog.
- [Nexus](http://www.sonatype.org/nexus/) z Sonatype.
- [TeamCity](https://www.jetbrains.com/teamcity/) firmy JetBrains.

Niezależnie od tego, w jaki sposób są hostowane pakiety, możesz uzyskiwać do nich dostęp, dodając je do listy dostępnych źródeł w `NuGet.Config`. Można to zrobić w programie Visual Studio zgodnie z opisem w [źródeł pakietów](../tools/package-manager-ui.md#package-sources), lub z wiersza polecenia przy użyciu [ `nuget sources` ](../tools/cli-ref-sources.md). Ścieżka do źródła może być nazwą ścieżki folderu lokalnego, Nazwa sieciowa lub adres URL.
