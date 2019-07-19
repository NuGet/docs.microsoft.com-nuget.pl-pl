---
title: Przegląd hostingu własnych źródeł danych NuGet
description: Omówienie otwierania w celu hostowania własnych kanałów informacyjnych lub Galerii pakietów NuGet lokalnie lub zdalnie.
author: karann-msft
ms.author: karann
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 737b13be70de9aaa7dec7904d4c2a4ec494ef7b3
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317552"
---
# <a name="hosting-your-own-nuget-feeds"></a>Hosting własnych źródeł danych NuGet

Zamiast udostępniać pakiety publicznie, możesz chcieć zwolnić pakiety tylko do ograniczonych odbiorców, takich jak organizacja lub Grupa robocza. Ponadto niektóre firmy mogą chcieć ograniczyć dostęp do bibliotek innych firm, które mogą być używane przez deweloperów, i w ten sposób kierować tych deweloperów na podstawie ograniczonego źródła pakietów, a nie nuget.org.

Dla wszystkich takich celów NuGet obsługuje Konfigurowanie prywatnych źródeł pakietów w następujący sposób:

- Lokalne źródło danych: Pakiety są po prostu umieszczane w odpowiednim sieciowym udziale plików, najlepiej `nuget init` przy `nuget add` użyciu i do tworzenia hierarchicznej struktury folderów (NuGet 3.3 +). Aby uzyskać szczegółowe informacje, zobacz [lokalne źródła danych](../hosting-packages/local-feeds.md).
- NuGet.Server: Pakiety są udostępniane za pośrednictwem lokalnego serwera HTTP. Aby uzyskać szczegółowe informacje, zobacz [NuGet. Server](../hosting-packages/nuget-server.md).
- Galeria NuGet: Pakiety są hostowane na serwerze internetowym przy użyciu [projektu galerii NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (GitHub.com). Galeria NuGet umożliwia zarządzanie użytkownikami i ich funkcje, takie jak obszerny interfejs użytkownika sieci Web, który umożliwia wyszukiwanie i eksplorowanie pakietów z poziomu przeglądarki, podobnie jak nuget.org.

Istnieje także kilka innych produktów hostingowych NuGet, które obsługują zdalne źródła danych, w tym następujące:

- [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish), która jest również dostępna na Team Foundation Server 2017 i nowszych.
- [MyGet](http://myget.org)
- [ProGet](http://inedo.com/proget) z Inedo
- [Rejestr pakietów usługi GitHub](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)
- [Serwer NuGet](http://nugetserver.net/), projekt społecznościowy z Inedo
- [Serwer NuGet (Open Source)](http://nuget-server.net)— implementacja "open source" podobna do serwera NuGet Inedo
- [LiGet](https://github.com/ai-traders/liget), implementacja typu "open source" serwera NuGet v2 działającego na platformie Kestrel w Docker
- [BaGet](https://github.com/loic-sharma/BaGet), implementacja typu "open source" serwera NuGet v3 skompilowanego na ASP.NET Core
- [Sleet](https://github.com/emgarten/sleet), generator statycznego źródła danych NuGet w wersji 3 (Open Source)
- [Artifactory](https://www.jfrog.com/artifactory/) z JFrog.
- [Nexus](http://www.sonatype.org/nexus/) z Sonatype.
- [TeamCity](https://www.jetbrains.com/teamcity/) z JetBrains.

Niezależnie od tego, jak są hostowane pakiety, można uzyskać do nich dostęp, dodając je do listy `NuGet.Config`dostępnych źródeł w. Można to zrobić w programie Visual Studio zgodnie z opisem w artykule [źródła pakietów](../consume-packages/install-use-packages-visual-studio.md#package-sources)lub z wiersza polecenia przy [`nuget sources`](../reference/cli-reference/cli-ref-sources.md)użyciu. Ścieżka do źródła może być ścieżką do folderu lokalnego, nazwą sieci lub adresem URL.
