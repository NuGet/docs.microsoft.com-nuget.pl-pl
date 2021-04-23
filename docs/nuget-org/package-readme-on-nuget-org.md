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
# <a name="package-readme-on-nugetorg"></a><span data-ttu-id="0c9a8-103">Pakiet readme na NuGet.org</span><span class="sxs-lookup"><span data-stu-id="0c9a8-103">Package readme on NuGet.org</span></span>

<span data-ttu-id="0c9a8-104">[Dołącz plik readme do pakietu NuGet,](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) aby twoje szczegóły pakietu bardziej rozbudowane i bardziej rozbudowane dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0c9a8-104">[Include a readme file in your NuGet package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) to make your package details richer and more informative for your users!</span></span>

<span data-ttu-id="0c9a8-105">Jest to prawdopodobnie jeden z pierwszych elementów, które użytkownicy zobaczą podczas wyświetlania strony szczegółów pakietu na NuGet.org i jest niezbędny do zrobienia dobrego wrażenia.</span><span class="sxs-lookup"><span data-stu-id="0c9a8-105">This is likely one of the first elements users will see when they view your package details page on NuGet.org and is essential to making a good impression!</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0c9a8-106">NuGet.org obsługuje tylko pliki readme w [znacznikach Markdown](https://daringfireball.net/projects/markdown/) i obrazy z ograniczonego zestawu domen.</span><span class="sxs-lookup"><span data-stu-id="0c9a8-106">NuGet.org only supports readme files in [Markdown](https://daringfireball.net/projects/markdown/) and images from a limited set of domains.</span></span> <span data-ttu-id="0c9a8-107">Zobacz nasze [dozwolone domeny, aby zapoznać się z obrazami](#allowed-domains-for-images-and-badges) i obsługiwanymi [funkcjami znaczników Markdown,](#supported-markdown-features) aby upewnić się, że twój readme jest poprawnie renderowany NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="0c9a8-107">See our [allowed domains for images](#allowed-domains-for-images-and-badges) and [supported Markdown features](#supported-markdown-features) to ensure your readme renders correctly on NuGet.org.</span></span>

## <a name="what-should-my-readme-include"></a><span data-ttu-id="0c9a8-108">Co powinien zawierać mój readme?</span><span class="sxs-lookup"><span data-stu-id="0c9a8-108">What should my readme include?</span></span>

<span data-ttu-id="0c9a8-109">Rozważ uwzględnienia następujących elementów w swoim readme:</span><span class="sxs-lookup"><span data-stu-id="0c9a8-109">Consider including the following items in your readme:</span></span>
* <span data-ttu-id="0c9a8-110">Wprowadzenie do tego, czym jest i jak działa pakiet — jakie problemy rozwiązuje?</span><span class="sxs-lookup"><span data-stu-id="0c9a8-110">An introduction to what your package is and does - what problems does it solve?</span></span>
* <span data-ttu-id="0c9a8-111">Jak rozpocząć pracę z pakietem — czy istnieją określone wymagania?</span><span class="sxs-lookup"><span data-stu-id="0c9a8-111">How to get started with your package - are there any specific requirements?</span></span>
* <span data-ttu-id="0c9a8-112">Linki do bardziej kompleksowej dokumentacji, jeśli nie została uwzględniona w samym readme.</span><span class="sxs-lookup"><span data-stu-id="0c9a8-112">Links to more comprehensive documentation if not included in the readme itself.</span></span>
* <span data-ttu-id="0c9a8-113">Co najmniej kilka fragmentów kodu/przykładów lub przykładowych obrazów.</span><span class="sxs-lookup"><span data-stu-id="0c9a8-113">At least a few code snippets/samples or example images.</span></span>
* <span data-ttu-id="0c9a8-114">Gdzie i jak pozostawiać opinie, takie jak link do problemów z projektem, Twitter, śledzenie błędów lub inna platforma.</span><span class="sxs-lookup"><span data-stu-id="0c9a8-114">Where and how to leave feedback such as link to the project issues, Twitter, bug tracker, or other platform.</span></span>
* <span data-ttu-id="0c9a8-115">Jak współtwomentować, jeśli ma to zastosowanie.</span><span class="sxs-lookup"><span data-stu-id="0c9a8-115">How to contribute, if applicable.</span></span>

<span data-ttu-id="0c9a8-116">Pamiętaj, że odczyty o wysokiej jakości mogą być dostępne w różnych formatach, kształtach i rozmiarach.</span><span class="sxs-lookup"><span data-stu-id="0c9a8-116">Keep in mind, high quality readmes can come in a wide variety of formats, shapes, and sizes!</span></span> <span data-ttu-id="0c9a8-117">Jeśli masz już pakiet dostępny na platformie NuGet.org, istnieje prawdopodobieństwo, że masz już plik dokumentacji lub inny plik dokumentacji w repozytorium, który byłby doskonałym dodatkiem do strony szczegółów NuGet.org `readme.md` aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0c9a8-117">If you already have a package available on NuGet.org, chances are that you already have a `readme.md` or other documentation file in your repository that would be a great addition to your NuGet.org details page.</span></span>

## <a name="preview-your-readme"></a><span data-ttu-id="0c9a8-118">Wyświetlanie podglądu wersji readme</span><span class="sxs-lookup"><span data-stu-id="0c9a8-118">Preview your readme</span></span>

<span data-ttu-id="0c9a8-119">Aby wyświetlić podgląd pliku readme przed jego rozpoczęciem w ucieku NuGet.org, przekaż pakiet za pomocą portalu internetowego Upload Package w witrynie [NuGet.org i](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) przewiń w dół do sekcji "Plik Readme" w podglądzie metadanych.</span><span class="sxs-lookup"><span data-stu-id="0c9a8-119">To preview your readme file before it's live on NuGet.org, upload your package using the [Upload Package web portal on NuGet.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) and scroll down to the "Readme File" section of the metadata preview.</span></span> <span data-ttu-id="0c9a8-120">Powinna to wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="0c9a8-120">It should look something like this:</span></span>

![Wersja zapoznawcza pliku Readme](media\readme-upload-preview.PNG)

<span data-ttu-id="0c9a8-122">Rozważ przejrzenie i wyświetlenie podglądu [](#allowed-domains-for-images-and-badges) pliku readme w celu zapewnienia zgodności obrazu i obsługiwanego formatowania, aby upewnić się, że jest to doskonałe pierwsze wrażenie dla potencjalnych użytkowników. [](#supported-markdown-features)</span><span class="sxs-lookup"><span data-stu-id="0c9a8-122">Consider taking time to review and preview your readme file for [image compliance](#allowed-domains-for-images-and-badges) and [supported formatting](#supported-markdown-features) to make sure it gives a great first impression to potential users!</span></span> <span data-ttu-id="0c9a8-123">Aby naprawić błędy pliku readme pakietu po jego opublikowaniu w NuGet.org, należy wypchnąć zaktualizowaną wersję pakietu za pomocą poprawki.</span><span class="sxs-lookup"><span data-stu-id="0c9a8-123">To correct mistakes on your package readme once it's published to NuGet.org, you will need to push an updated package version with the fix.</span></span> <span data-ttu-id="0c9a8-124">Upewnienie się, że wszystko wygląda dobrze z wyprzedzeniem, może zaoszczędzić ci pracy.</span><span class="sxs-lookup"><span data-stu-id="0c9a8-124">Making sure everything looks good in advance may save you headache down the road.</span></span>
## <a name="allowed-domains-for-images-and-badges"></a><span data-ttu-id="0c9a8-125">Dozwolone domeny dla obrazów i wskaźników</span><span class="sxs-lookup"><span data-stu-id="0c9a8-125">Allowed domains for images and badges</span></span>

<span data-ttu-id="0c9a8-126">Ze względu na kwestie związane z zabezpieczeniami i NuGet.org ogranicza domeny, z których obrazy i znaczki mogą być renderowane na zaufanych hostach.</span><span class="sxs-lookup"><span data-stu-id="0c9a8-126">Due to security and privacy concerns, NuGet.org restricts the domains from which images and badges can be rendered to trusted hosts.</span></span> 

<span data-ttu-id="0c9a8-127">NuGet.org umożliwia renderowanie wszystkich obrazów, w tym identyfikatorów, z następujących zaufanych domen:</span><span class="sxs-lookup"><span data-stu-id="0c9a8-127">NuGet.org allows all images, including badges, from the following trusted domains to be rendered:</span></span>
* <span data-ttu-id="0c9a8-128">api.bintray.com</span><span class="sxs-lookup"><span data-stu-id="0c9a8-128">api.bintray.com</span></span>
* <span data-ttu-id="0c9a8-129">api.codacy.com</span><span class="sxs-lookup"><span data-stu-id="0c9a8-129">api.codacy.com</span></span>
* <span data-ttu-id="0c9a8-130">api.codeclimate.com</span><span class="sxs-lookup"><span data-stu-id="0c9a8-130">api.codeclimate.com</span></span>
* <span data-ttu-id="0c9a8-131">api.dependabot.com</span><span class="sxs-lookup"><span data-stu-id="0c9a8-131">api.dependabot.com</span></span>
* <span data-ttu-id="0c9a8-132">api.travis-ci.com</span><span class="sxs-lookup"><span data-stu-id="0c9a8-132">api.travis-ci.com</span></span>
* <span data-ttu-id="0c9a8-133">api.travis-ci.org</span><span class="sxs-lookup"><span data-stu-id="0c9a8-133">api.travis-ci.org</span></span>
* <span data-ttu-id="0c9a8-134">app.fossa.io</span><span class="sxs-lookup"><span data-stu-id="0c9a8-134">app.fossa.io</span></span>
* <span data-ttu-id="0c9a8-135">badge.fury.io</span><span class="sxs-lookup"><span data-stu-id="0c9a8-135">badge.fury.io</span></span>
* <span data-ttu-id="0c9a8-136">badgen.net</span><span class="sxs-lookup"><span data-stu-id="0c9a8-136">badgen.net</span></span>
* <span data-ttu-id="0c9a8-137">badges.gitter.im</span><span class="sxs-lookup"><span data-stu-id="0c9a8-137">badges.gitter.im</span></span>
* <span data-ttu-id="0c9a8-138">bettercodehub.com</span><span class="sxs-lookup"><span data-stu-id="0c9a8-138">bettercodehub.com</span></span>
* <span data-ttu-id="0c9a8-139">buildstats.info</span><span class="sxs-lookup"><span data-stu-id="0c9a8-139">buildstats.info</span></span>
* <span data-ttu-id="0c9a8-140">camo.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="0c9a8-140">camo.githubusercontent.com</span></span>
* <span data-ttu-id="0c9a8-141">ci.appveyor.com</span><span class="sxs-lookup"><span data-stu-id="0c9a8-141">ci.appveyor.com</span></span>
* <span data-ttu-id="0c9a8-142">circleci.com</span><span class="sxs-lookup"><span data-stu-id="0c9a8-142">circleci.com</span></span>
* <span data-ttu-id="0c9a8-143">codecov.io</span><span class="sxs-lookup"><span data-stu-id="0c9a8-143">codecov.io</span></span>
* <span data-ttu-id="0c9a8-144">codefactor.io</span><span class="sxs-lookup"><span data-stu-id="0c9a8-144">codefactor.io</span></span>
* <span data-ttu-id="0c9a8-145">coveralls.io</span><span class="sxs-lookup"><span data-stu-id="0c9a8-145">coveralls.io</span></span>
* <span data-ttu-id="0c9a8-146">dev.azure.com</span><span class="sxs-lookup"><span data-stu-id="0c9a8-146">dev.azure.com</span></span>
* <span data-ttu-id="0c9a8-147">github.com/.../workflows/.../badge.svg</span><span class="sxs-lookup"><span data-stu-id="0c9a8-147">github.com/.../workflows/.../badge.svg</span></span>
* <span data-ttu-id="0c9a8-148">gitlab.com</span><span class="sxs-lookup"><span data-stu-id="0c9a8-148">gitlab.com</span></span>
* <span data-ttu-id="0c9a8-149">img.shields.io</span><span class="sxs-lookup"><span data-stu-id="0c9a8-149">img.shields.io</span></span>
* <span data-ttu-id="0c9a8-150">isitmaintained.com</span><span class="sxs-lookup"><span data-stu-id="0c9a8-150">isitmaintained.com</span></span>
* <span data-ttu-id="0c9a8-151">opencollective.com</span><span class="sxs-lookup"><span data-stu-id="0c9a8-151">opencollective.com</span></span>
* <span data-ttu-id="0c9a8-152">raw.github.com</span><span class="sxs-lookup"><span data-stu-id="0c9a8-152">raw.github.com</span></span>
* <span data-ttu-id="0c9a8-153">raw.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="0c9a8-153">raw.githubusercontent.com</span></span>
* <span data-ttu-id="0c9a8-154">snyk.io</span><span class="sxs-lookup"><span data-stu-id="0c9a8-154">snyk.io</span></span>
* <span data-ttu-id="0c9a8-155">sonarcloud.io</span><span class="sxs-lookup"><span data-stu-id="0c9a8-155">sonarcloud.io</span></span>
* <span data-ttu-id="0c9a8-156">user-images.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="0c9a8-156">user-images.githubusercontent.com</span></span>

<span data-ttu-id="0c9a8-157">Jeśli uważasz, że do listy zezwalań powinna zostać [](https://github.com/NuGet/NuGetGallery/issues) dodana inna domena, możesz skontaktować się z naszym zespołem inżynierów, aby uzyskać informacje o problemie i zapewnić zgodność z zabezpieczeniami.</span><span class="sxs-lookup"><span data-stu-id="0c9a8-157">If you feel that another domain should be added to the allow-list, please feel free to [file an issue](https://github.com/NuGet/NuGetGallery/issues) and it will be reviewed by our engineering team for privacy and security compliance.</span></span> <span data-ttu-id="0c9a8-158">Obrazy ze względną ścieżką lokalną i obrazy hostowane z nieobsługiwanych domen nie będą renderowane i będą tworzyć ostrzeżenie na stronie podglądu pliku readme i szczegółów pakietu, która jest widoczna tylko dla właścicieli pakietu.</span><span class="sxs-lookup"><span data-stu-id="0c9a8-158">Images with relative local paths and images hosted from unsupported domains will not be rendered and will produce a warning on the readme file preview and package details page that is only visible to the package owners.</span></span>

## <a name="supported-markdown-features"></a><span data-ttu-id="0c9a8-159">Obsługiwane funkcje markdown</span><span class="sxs-lookup"><span data-stu-id="0c9a8-159">Supported Markdown features</span></span>
<span data-ttu-id="0c9a8-160">[Markdown](https://daringfireball.net/projects/markdown/) to lekki język znaczników ze składnią formatowania zwykłego tekstu.</span><span class="sxs-lookup"><span data-stu-id="0c9a8-160">[Markdown](https://daringfireball.net/projects/markdown/) is a lightweight markup language with plain text formatting syntax.</span></span> <span data-ttu-id="0c9a8-161">NuGet.org obsługują zgodny ze specyfikacją [CommonMark](https://commonmark.org/) znacznik markdown za pośrednictwem [aparatu analizowania Markdig.](https://github.com/lunet-io/markdig)</span><span class="sxs-lookup"><span data-stu-id="0c9a8-161">NuGet.org readmes support [CommonMark](https://commonmark.org/) compliant Markdown through the [Markdig](https://github.com/lunet-io/markdig) parsing engine.</span></span>

<span data-ttu-id="0c9a8-162">NuGet.org obecnie obsługuje następujące funkcje markdown:</span><span class="sxs-lookup"><span data-stu-id="0c9a8-162">NuGet.org currently supports the following Markdown features:</span></span>
* [<span data-ttu-id="0c9a8-163">Nagłówki</span><span class="sxs-lookup"><span data-stu-id="0c9a8-163">Headers</span></span>](https://spec.commonmark.org/0.29/#atx-headings)
* [<span data-ttu-id="0c9a8-164">Obrazy</span><span class="sxs-lookup"><span data-stu-id="0c9a8-164">Images</span></span>](https://spec.commonmark.org/0.29/#images)
* [<span data-ttu-id="0c9a8-165">Dodatkowe wyróżnienie</span><span class="sxs-lookup"><span data-stu-id="0c9a8-165">Extra emphasis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [<span data-ttu-id="0c9a8-166">Listy</span><span class="sxs-lookup"><span data-stu-id="0c9a8-166">Lists</span></span>](https://spec.commonmark.org/0.29/#lists)
* [<span data-ttu-id="0c9a8-167">Linki</span><span class="sxs-lookup"><span data-stu-id="0c9a8-167">Links</span></span>](https://spec.commonmark.org/0.29/#links)
* [<span data-ttu-id="0c9a8-168">Cytaty blokowe</span><span class="sxs-lookup"><span data-stu-id="0c9a8-168">Block quotes</span></span>](https://spec.commonmark.org/0.29/#block-quotes)
* [<span data-ttu-id="0c9a8-169">Ucieczki ukośnika odwrotnego</span><span class="sxs-lookup"><span data-stu-id="0c9a8-169">Backslash escapes</span></span>](https://spec.commonmark.org/0.29/#backslash-escapes)
* [<span data-ttu-id="0c9a8-170">Zakresy kodu</span><span class="sxs-lookup"><span data-stu-id="0c9a8-170">Code spans</span></span>](https://spec.commonmark.org/0.29/#code-spans)
* [<span data-ttu-id="0c9a8-171">Listy zadań</span><span class="sxs-lookup"><span data-stu-id="0c9a8-171">Task lists</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [<span data-ttu-id="0c9a8-172">Tabele</span><span class="sxs-lookup"><span data-stu-id="0c9a8-172">Tables</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [<span data-ttu-id="0c9a8-173">Emojis</span><span class="sxs-lookup"><span data-stu-id="0c9a8-173">Emojis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [<span data-ttu-id="0c9a8-174">Automatyczne linki</span><span class="sxs-lookup"><span data-stu-id="0c9a8-174">Auto-links</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

