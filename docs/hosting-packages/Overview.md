---
title: Przegląd hostingu własnych kanałów NuGet
description: Omówienie otwiera dla hostingu własnych nuget pakietów kanałów informacyjnych lub galerii lokalnie lub zdalnie.
author: karann-msft
ms.author: karann
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 81acf15ac69d78d39d2784e77c18ba38bfea126d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "75385545"
---
# <a name="hosting-your-own-nuget-feeds"></a>Hostowanie własnych kanałów NuGet

Zamiast udostępniać pakiety publicznie, można udostępnić pakiety tylko ograniczonej grupie odbiorców, takiej jak organizacja lub grupa robocza. Ponadto niektóre firmy mogą chcieć ograniczyć biblioteki innych firm, z których mogą korzystać ich deweloperzy, a tym samym skierować tych deweloperów do rysowania z ograniczonego źródła pakietu, a nie nuget.org.

Dla wszystkich takich celów NuGet obsługuje konfigurowanie prywatnych źródeł pakietów w następujący sposób:

- Lokalny kanał informacyjny: Pakiety są po prostu umieszczane w odpowiednim udziale plików sieciowych, najlepiej używając `nuget init` i `nuget add` tworząc hierarchiczną strukturę folderów (NuGet 3.3+). Aby uzyskać szczegółowe informacje, zobacz [Lokalne kanały informacyjne](../hosting-packages/local-feeds.md).
- NuGet.Server: Pakiety są udostępniane za pośrednictwem lokalnego serwera HTTP. Aby uzyskać szczegółowe informacje, zobacz [NuGet.Server](../hosting-packages/nuget-server.md).
- Galeria NuGet: Pakiety są hostowane na serwerze internetowym przy użyciu [projektu NuGet Gallery](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com). Galeria NuGet udostępnia zarządzanie użytkownikami i funkcje, takie jak rozbudowany interfejs użytkownika sieci Web, który umożliwia wyszukiwanie i eksplorowanie pakietów z poziomu przeglądarki, podobnie jak nuget.org.

Istnieje również kilka innych produktów hostingowych NuGet, takich jak [artefakty platformy Azure](https://www.visualstudio.com/docs/package/nuget/publish) i rejestr [pakietów GitHub,](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry) które obsługują zdalne prywatne źródła danych. Poniżej znajduje się lista takich produktów:

- [Artifactory](https://www.jfrog.com/artifactory/) z JFrog.
- [Artefakty platformy Azure](https://www.visualstudio.com/docs/package/nuget/publish), który jest również dostępny na Team Foundation Server 2017 i nowsze.
- [BaGet](https://github.com/loic-sharma/BaGet), implementacja open-source serwera NuGet V3 zbudowana na ASP.NET Core
- [Cloudsmith](https://cloudsmith.io/l/nuget-feed/), w pełni zarządzane zarządzanie pakietami SaaS
- [Rejestr pakietów GitHub](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)
- [LiGet](https://github.com/ai-traders/liget), implementacja open-source serwera NuGet V2, który działa na pustułce w docker
- [MyGet](https://myget.org)
- [Nexus Repozytorium OSS](https://www.sonatype.com/nexus-repository-oss) z Sonatype.
- [NuGet Server (Open Source)](https://github.com/svenkle/nuget-server)— implementacja typu open source podobna do serwera NuGet Server firmy Inedo
- [NuGet Server](http://nugetserver.net/), projekt społeczności z Inedo
- [ProGet](https://inedo.com/proget) od Inedo
- [Sleet](https://github.com/emgarten/sleet), generator statyczny NuGet V3 typu open source
- [TeamCity](https://www.jetbrains.com/teamcity/) firmy JetBrains.

Niezależnie od sposobu hosta pakietów, można uzyskać do nich dostęp, `NuGet.Config`dodając je do listy dostępnych źródeł w programie . Można to zrobić w programie Visual Studio zgodnie z opisem [`nuget sources`](../reference/cli-reference/cli-ref-sources.md)w programie Źródła [pakietów](../consume-packages/install-use-packages-visual-studio.md#package-sources)lub z wiersza polecenia przy użyciu programu . Ścieżką do źródła może być nazwa ścieżki folderu lokalnego, nazwa sieciowa lub adres URL.
