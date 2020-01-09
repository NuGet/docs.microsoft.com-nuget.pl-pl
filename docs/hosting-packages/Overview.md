---
title: Przegląd hostingu własnych źródeł danych NuGet
description: Omówienie otwierania w celu hostowania własnych kanałów informacyjnych lub Galerii pakietów NuGet lokalnie lub zdalnie.
author: karann-msft
ms.author: karann
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 81acf15ac69d78d39d2784e77c18ba38bfea126d
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385545"
---
# <a name="hosting-your-own-nuget-feeds"></a>Hosting własnych źródeł danych NuGet

Zamiast udostępniać pakiety publicznie, możesz chcieć zwolnić pakiety tylko do ograniczonych odbiorców, takich jak organizacja lub Grupa robocza. Ponadto niektóre firmy mogą chcieć ograniczyć dostęp do bibliotek innych firm, które mogą być używane przez deweloperów, i w ten sposób kierować tych deweloperów na podstawie ograniczonego źródła pakietów, a nie nuget.org.

Dla wszystkich takich celów NuGet obsługuje Konfigurowanie prywatnych źródeł pakietów w następujący sposób:

- Lokalne źródło danych: pakiety są po prostu umieszczane w odpowiednim udziale plików sieciowych, najlepiej przy użyciu `nuget init` i `nuget add` do tworzenia hierarchicznej struktury folderów (NuGet 3.3 +). Aby uzyskać szczegółowe informacje, zobacz [lokalne źródła danych](../hosting-packages/local-feeds.md).
- NuGet. Server: pakiety są udostępniane za pośrednictwem lokalnego serwera HTTP. Aby uzyskać szczegółowe informacje, zobacz [NuGet. Server](../hosting-packages/nuget-server.md).
- Galeria NuGet: pakiety są hostowane na serwerze internetowym przy użyciu [projektu galerii NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (GitHub.com). Galeria NuGet umożliwia zarządzanie użytkownikami i ich funkcje, takie jak obszerny interfejs użytkownika sieci Web, który umożliwia wyszukiwanie i eksplorowanie pakietów z poziomu przeglądarki, podobnie jak nuget.org.

Istnieje także kilka innych produktów hostingowych NuGet, takich jak [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish) i [Rejestr pakietów usługi GitHub](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry) , które obsługują zdalne źródła danych. Poniżej znajduje się lista takich produktów:

- [Artifactory](https://www.jfrog.com/artifactory/) z JFrog.
- [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish), która jest również dostępna na Team Foundation Server 2017 i nowszych.
- [BaGet](https://github.com/loic-sharma/BaGet), implementacja typu "open source" serwera NuGet v3 skompilowanego na ASP.NET Core
- [Cloudsmith](https://cloudsmith.io/l/nuget-feed/), w pełni zarządzane zarządzanie pakietami SaaS
- [Rejestr pakietów usługi GitHub](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)
- [LiGet](https://github.com/ai-traders/liget), implementacja typu "open source" serwera NuGet v2 działającego na platformie Kestrel w Docker
- [MyGet](https://myget.org)
- [Nexus REPOZYTORIUM OSS](https://www.sonatype.com/nexus-repository-oss) z Sonatype.
- [Serwer NuGet (Open Source)](https://github.com/svenkle/nuget-server)— implementacja "open source" podobna do serwera NuGet Inedo
- [Serwer NuGet](http://nugetserver.net/), projekt społecznościowy z Inedo
- [ProGet](https://inedo.com/proget) z Inedo
- [Sleet](https://github.com/emgarten/sleet), generator statycznego źródła danych NuGet w wersji 3 (Open Source)
- [TeamCity](https://www.jetbrains.com/teamcity/) z JetBrains.

Niezależnie od tego, jak są hostowane pakiety, można uzyskać do nich dostęp, dodając je do listy dostępnych źródeł w `NuGet.Config`. Można to zrobić w programie Visual Studio zgodnie z opisem w artykule [źródła pakietów](../consume-packages/install-use-packages-visual-studio.md#package-sources)lub z wiersza polecenia przy użyciu [`nuget sources`](../reference/cli-reference/cli-ref-sources.md). Ścieżka do źródła może być ścieżką do folderu lokalnego, nazwą sieci lub adresem URL.
