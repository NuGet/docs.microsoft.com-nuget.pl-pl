---
title: Pakiet readme na NuGet.org
description: Szczegółowe wyjaśnienie sposobu renderowania plików readme NuGet.org oraz tego, co należy zrobić w przypadku problemów.
author: chgill-MSFT
ms.author: chgill
ms.date: 02/23/2021
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a5d68329128c9e9d047fe10e08ce41f1ae0895b4
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107902254"
---
# <a name="package-readme-on-nugetorg"></a>Pakiet readme na NuGet.org

[Dołącz plik readme do pakietu NuGet,](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) aby twoje szczegóły pakietu bardziej rozbudowane i bardziej rozbudowane dla użytkowników.

Jest to prawdopodobnie jeden z pierwszych elementów, które użytkownicy zobaczą podczas wyświetlania strony szczegółów pakietu na NuGet.org i jest niezbędny do zrobienia dobrego wrażenia.

> [!IMPORTANT]
> NuGet.org obsługuje tylko pliki readme w [znacznikach Markdown](https://daringfireball.net/projects/markdown/) i obrazy z ograniczonego zestawu domen. Zobacz nasze [dozwolone domeny, aby zapoznać się z obrazami](#allowed-domains-for-images-and-badges) i obsługiwanymi [funkcjami znaczników Markdown,](#supported-markdown-features) aby upewnić się, że twój readme jest poprawnie renderowany NuGet.org.

## <a name="what-should-my-readme-include"></a>Co powinien zawierać mój readme?

Rozważ uwzględnienia następujących elementów w swoim readme:
* Wprowadzenie do tego, czym jest i jak działa pakiet — jakie problemy rozwiązuje?
* Jak rozpocząć pracę z pakietem — czy istnieją określone wymagania?
* Linki do bardziej kompleksowej dokumentacji, jeśli nie została uwzględniona w samym readme.
* Co najmniej kilka fragmentów kodu/przykładów lub przykładowych obrazów.
* Gdzie i jak pozostawiać opinie, takie jak link do problemów z projektem, Twitter, śledzenie błędów lub inna platforma.
* Jak współtwomentować, jeśli ma to zastosowanie.

Pamiętaj, że odczyty o wysokiej jakości mogą być dostępne w różnych formatach, kształtach i rozmiarach. Jeśli masz już pakiet dostępny na platformie NuGet.org, istnieje prawdopodobieństwo, że masz już plik dokumentacji lub inny plik dokumentacji w repozytorium, który byłby doskonałym dodatkiem do strony szczegółów NuGet.org `readme.md` aplikacji.

## <a name="preview-your-readme"></a>Wyświetlanie podglądu wersji readme

Aby wyświetlić podgląd pliku readme przed jego rozpoczęciem w ucieku NuGet.org, przekaż pakiet za pomocą portalu internetowego Upload Package w witrynie [NuGet.org i](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) przewiń w dół do sekcji "Plik Readme" w podglądzie metadanych. Powinna to wyglądać następująco:

![Wersja zapoznawcza pliku Readme](media\readme-upload-preview.PNG)

Rozważ przejrzenie i wyświetlenie podglądu [](#allowed-domains-for-images-and-badges) pliku readme w celu zapewnienia zgodności obrazu i obsługiwanego formatowania, aby upewnić się, że jest to doskonałe pierwsze wrażenie dla potencjalnych użytkowników. [](#supported-markdown-features) Aby naprawić błędy pliku readme pakietu po jego opublikowaniu w NuGet.org, należy wypchnąć zaktualizowaną wersję pakietu za pomocą poprawki. Upewnienie się, że wszystko wygląda dobrze z wyprzedzeniem, może zaoszczędzić ci pracy.
## <a name="allowed-domains-for-images-and-badges"></a>Dozwolone domeny dla obrazów i wskaźników

Ze względu na kwestie związane z zabezpieczeniami i NuGet.org ogranicza domeny, z których obrazy i znaczki mogą być renderowane na zaufanych hostach. 

NuGet.org umożliwia renderowanie wszystkich obrazów, w tym identyfikatorów, z następujących zaufanych domen:
* api.bintray.com
* api.codacy.com
* api.codeclimate.com
* api.dependabot.com
* api.travis-ci.com
* api.travis-ci.org
* app.fossa.io
* badge.fury.io
* badgen.net
* badges.gitter.im
* bettercodehub.com
* buildstats.info
* camo.githubusercontent.com
* ci.appveyor.com
* circleci.com
* codecov.io
* codefactor.io
* coveralls.io
* dev.azure.com
* github.com/.../workflows/.../badge.svg
* gitlab.com
* img.shields.io
* isitmaintained.com
* opencollective.com
* raw.github.com
* raw.githubusercontent.com
* snyk.io
* sonarcloud.io
* user-images.githubusercontent.com

Jeśli uważasz, że do listy zezwalań powinna zostać [](https://github.com/NuGet/NuGetGallery/issues) dodana inna domena, możesz skontaktować się z naszym zespołem inżynierów, aby uzyskać informacje o problemie i zapewnić zgodność z zabezpieczeniami. Obrazy ze względną ścieżką lokalną i obrazy hostowane z nieobsługiwanych domen nie będą renderowane i będą tworzyć ostrzeżenie na stronie podglądu pliku readme i szczegółów pakietu, która jest widoczna tylko dla właścicieli pakietu.

## <a name="supported-markdown-features"></a>Obsługiwane funkcje markdown
[Markdown](https://daringfireball.net/projects/markdown/) to lekki język znaczników ze składnią formatowania zwykłego tekstu. NuGet.org obsługują zgodny ze specyfikacją [CommonMark](https://commonmark.org/) znacznik markdown za pośrednictwem [aparatu analizowania Markdig.](https://github.com/lunet-io/markdig)

NuGet.org obecnie obsługuje następujące funkcje markdown:
* [Nagłówki](https://spec.commonmark.org/0.29/#atx-headings)
* [Obrazy](https://spec.commonmark.org/0.29/#images)
* [Dodatkowe wyróżnienie](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [Listy](https://spec.commonmark.org/0.29/#lists)
* [Linki](https://spec.commonmark.org/0.29/#links)
* [Cytaty blokowe](https://spec.commonmark.org/0.29/#block-quotes)
* [Ucieczki ukośnika odwrotnego](https://spec.commonmark.org/0.29/#backslash-escapes)
* [Zakresy kodu](https://spec.commonmark.org/0.29/#code-spans)
* [Listy zadań](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [Tabele](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [Emojis](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [Automatyczne linki](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

