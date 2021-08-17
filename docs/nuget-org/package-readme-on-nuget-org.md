---
title: Pakiet readme w NuGet.org
description: Szczegółowe wyjaśnienie sposobu renderowania plików readme w NuGet.org oraz tego, co należy zrobić w przypadku problemów.
author: chgill-MSFT
ms.author: chgill
ms.date: 02/23/2021
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: ac0e89c1f5ef9eb19c29646bcc76bcb0b460c5cd
ms.sourcegitcommit: adb261dd4b2a8cd75447f7b5ea6a9e5a1a54d61d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/16/2021
ms.locfileid: "122209946"
---
# <a name="package-readme-on-nugetorg"></a>Pakiet readme w NuGet.org

[Dołącz plik readme do pakietu NuGet,](/nuget/reference/msbuild-targets#packagereadmefile) aby szczegóły pakietu bardziej rozbudowane i bardziej rozbudowane dla użytkowników.

Jest to prawdopodobnie jeden z pierwszych elementów, które użytkownicy zobaczą podczas wyświetlania strony szczegółów pakietu w NuGet.org i jest niezbędny do zrobienia dobrego wrażenia.

> [!IMPORTANT]
> NuGet.org obsługuje tylko pliki readme w [znacznikach Markdown](https://daringfireball.net/projects/markdown/) i obrazy z ograniczonego zestawu domen. Zobacz dozwolone [domeny, aby zapoznać się z obrazami](#allowed-domains-for-images-and-badges) i obsługiwanymi [funkcjami znaczników Markdown,](#supported-markdown-features) aby upewnić się, że twój readme jest poprawnie renderowany NuGet.org.

## <a name="what-should-my-readme-include"></a>Co powinien zawierać mój readme?

Rozważ uwzględnienia następujących elementów w swoim readme:
* Wprowadzenie do tego, czym jest i jak działa pakiet — jakie problemy rozwiązuje?
* Jak rozpocząć pracę z pakietem — czy istnieją jakieś określone wymagania?
* Linki do bardziej kompleksowej dokumentacji, jeśli nie została uwzględniona w samym readme.
* Co najmniej kilka fragmentów kodu/przykładów lub przykładowych obrazów.
* Gdzie i jak pozostawiać opinie, takie jak link do problemów z projektem, Twitter, śledzenie błędów lub inna platforma.
* Jak współtwomentować, jeśli ma to zastosowanie.

Pamiętaj, że odczyty o wysokiej jakości mogą być dostępne w różnych formatach, kształtach i rozmiarach. Jeśli masz już pakiet dostępny na stronie NuGet.org, istnieje prawdopodobieństwo, że masz już plik dokumentacji lub inny plik dokumentacji w repozytorium, który byłby doskonałym dodatkiem do strony szczegółów witryny `readme.md` NuGet.org.

## <a name="preview-your-readme"></a>Wyświetlanie podglądu wersji readme

Aby wyświetlić podgląd pliku readme przed jego rozpoczęciem w witrynie NuGet.org, przekaż pakiet przy użyciu portalu internetowego pakietu Upload w witrynie [NuGet.org](/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) i przewiń w dół do sekcji "Plik Readme" w podglądzie metadanych. Powinna to wyglądać następująco:

![Wersja zapoznawcza pliku Readme](media\readme-upload-preview.PNG)

Rozważ poekspretowanie i wyświetlenie [](#allowed-domains-for-images-and-badges) podglądu [](#supported-markdown-features) pliku readme w celu zapewnienia zgodności obrazów i obsługiwanego formatowania, aby upewnić się, że jest to doskonałe pierwsze wrażenie dla potencjalnych użytkowników. Aby poprawić błędy pliku readme pakietu po jego opublikowaniu w NuGet.org, należy wypchnąć zaktualizowaną wersję pakietu za pomocą poprawki. Upewnienie się, że wszystko wygląda dobrze z wyprzedzeniem, może zaoszczędzić ci pracy.
## <a name="allowed-domains-for-images-and-badges"></a>Dozwolone domeny dla obrazów i identyfikatorów

Ze względu na kwestie związane z zabezpieczeniami i prywatnością NuGet.org ogranicza domeny, z których obrazy i znaczki mogą być renderowane na zaufanych hostach. 

NuGet.org umożliwia renderowanie wszystkich obrazów, w tym identyfikatorów, z następujących zaufanych domen:
* api.bintray.com
* api.codacy.com
* app.codacy.com
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
* cdn.jsdelivr.net
* ci.appveyor.com
* circleci.com
* codecov.io
* codefactor.io
* coveralls.io
* dev.azure.com
* github.com/.../workflows/.../badge.svg
* gitlab.com
* img.shields.io
* i.imgur.com
* isitmaintained.com
* opencollective.com
* raw.github.com
* raw.githubusercontent.com
* snyk.io
* sonarcloud.io
* user-images.githubusercontent.com

Jeśli uważasz, że do listy zezwalań powinna zostać [](https://github.com/NuGet/NuGetGallery/issues) dodana inna domena, możesz skontaktować się z naszym zespołem inżynierów, aby uzyskać informacje o problemie i zgodności z zabezpieczeniami. Obrazy ze względną ścieżką lokalną i obrazy hostowane z nieobsługiwanych domen nie będą renderowane i będą tworzyć ostrzeżenie na stronie podglądu pliku readme i szczegółów pakietu, która jest widoczna tylko dla właścicieli pakietu.

## <a name="supported-markdown-features"></a>Obsługiwane funkcje markdown
[Markdown](https://daringfireball.net/projects/markdown/) to lekki język znaczników ze składnią formatowania zwykłego tekstu. NuGet.org obsługuje zgodny ze specyfikacją [CommonMark](https://commonmark.org/) znacznik markdown za pośrednictwem [aparatu analizowania Markdig.](https://github.com/lunet-io/markdig)

NuGet.org obsługuje obecnie następujące funkcje markdown:
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
* [Linki automatyczne](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

