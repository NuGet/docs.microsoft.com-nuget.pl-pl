---
title: Najlepsze rozwiązania dotyczące tworzenia pakietów
description: Ogólny przewodnik po najlepszych rozwiązaniach w zakresie tworzenia pakietów NuGet o wysokiej jakości.
author: chgill-MSFT
ms.author: chgill
ms.date: 09/17/2020
ms.topic: conceptual
ms.openlocfilehash: 358e574339688514448b684aadc6911f9d83611f
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901450"
---
# <a name="package-authoring-best-practices"></a>Najlepsze rozwiązania dotyczące tworzenia pakietów

Te wskazówki mają na celu zapewnienie autorom pakietów NuGet lekkiego odwołania do tworzenia i publikowania pakietów wysokiej jakości. Koncentruje się on głównie na najlepszych rozwiązaniach specyficznych dla pakietu, takich jak metadane i pakowanie. Aby uzyskać bardziej szczegółowe sugestie dotyczące tworzenia bibliotek wysokiej jakości, zobacz .NET [Open-source library guidance](/dotnet/standard/library-guidance/)(Wskazówki dotyczące bibliotek typu open source dla programu .NET).

## <a name="types-of-recommendations"></a>Typy rekomendacji

Każdy artykuł zawiera cztery typy zaleceń: **Nie,** **Rozważ,** **Unikaj** i **Nie .** Typ zalecenia wskazuje, jak blisko powinno być stosowane.

Prawie zawsze należy postępować zgodnie z **zaleceniem Wykonaj.** Na przykład:

✔️ DO zawierają krótki opis pakietu, który opisuje jego zawartość.

Z drugiej **strony,** należy wziąć pod uwagę zalecenia, które powinny być stosowane, ale istnieją uzasadnione wyjątki od reguły:

✔️ ROZWAŻYĆ wybranie nazwy pakietu NuGet z prefiksem spełniającym kryteria rezerwacji [prefiksu](../nuget-org/id-prefix-reservation.md)NuGet.

**Należy** unikać zaleceń, jeśli chodzi o rzeczy, które zazwyczaj nie są dobrym pomysłem, ale czasami naruszenie reguły ma sens:

❌ UNIKAJ odwołań do pakietów NuGet, które wymagają dokładnej wersji.

I na **koniec: Nie zalecenia** wskazują czegoś, czego prawie nigdy nie należy robić:

❌ NIE UŻYWAJ `LicenseUrl` właściwości metadanych.

## <a name="create-a-nuget-package"></a>Tworzenie pakietu NuGet

Najnowszy zalecany sposób tworzenia pakietu NuGet to projekt w [stylu zestawu SDK.](../resources/check-project-format.md) Właściwości projektu w stylu zestawu SDK, w tym [docelowa framework](/dotnet/standard/frameworks) i [metadane pakietu,](#package-metadata)są definiowane w [pliku projektu](/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file).

Utwórz pakiet z projektu w stylu zestawu SDK, [](../quickstart/create-and-publish-a-package-using-visual-studio.md?tabs=netcore-cli) definiując wymagane właściwości i pakowanie w Visual Studio lub interfejsie wiersza polecenia [dotnet.](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)

✔️ UTWORZYĆ projekt w stylu zestawu SDK i utworzyć (spakować) pakiet przy użyciu Visual Studio lub interfejsu wiersza polecenia dotnet.

Aby uzyskać bardziej szczegółowe wskazówki dotyczące tworzenia pakietów, w tym niezbędne narzędzia klienckie, przykładowy plik projektu i polecenia, zobacz [Create a NuGet package using the dotnet CLI](./creating-a-package-dotnet-cli.md)(Tworzenie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet).

Aby ułatwić podjęcie decyzji o tym, które platformy .NET mają być przeznaczone dla użytkowników docelowych, zobacz nasze najnowsze wskazówki dotyczące określania platform [docelowych.](/dotnet/standard/library-guidance/cross-platform-targeting)

## <a name="package-metadata"></a>Metadane pakietu

Metadane to składnik podstaw każdego pakietu NuGet. Jakość metadanych może mieć duży wpływ na wykrywalność, użyteczność i wiarygodność pakietu.

W Visual Studio zalecanym sposobem określenia metadanych pakietu jest użycie właściwości Project > [Project Name] > Package.

Elementy metadanych pakietu można również [określić bezpośrednio w pliku projektu](./creating-a-package-msbuild.md#set-properties).

Poniżej znajduje się mapowanie tabeli i opisywanie dostępnych elementów metadanych pakietu:

| Visual Studio nazwy właściwości                       | [Plik projektu/ nazwa właściwości MSBuild](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                            | [Nazwa właściwości nuspec](https://docs.microsoft.com/nuget/reference/nuspec#general-form-and-schema)     | Opis                                                                                                           |
|-----------------------------------------------    |-----------------------------------------------------------------------------------------------------------------------------------------  |---------------------------------------------------------------------------------------------------    |-------------------------------------------------------------------------------------------------------------------    |
| [`Package id`](#package-id)                       | [`PackageId`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                                             | [`id`](https://docs.microsoft.com/nuget/reference/nuspec#id)                                          | Nazwa lub identyfikator pakietu.                                                                                       |
| [`Package version`](#package-version)             | [`PackageVersion`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                                    | [`version`](https://docs.microsoft.com/nuget/reference/nuspec#version)                                | Wersja pakietu NuGet.                                                                                                |
| [`Authors`](#authors)                             | [`Authors`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                                                   | [`authors`](https://docs.microsoft.com/nuget/reference/nuspec#authors)                                | Rozdzielana przecinkami lista autorów pakietów, często używająca "dobrej nazwy" osoby lub organizacji.           |
| [`Description`](#description)                     | [`Description`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                                           | [`description`](https://docs.microsoft.com/nuget/reference/nuspec#description)                        | Opis pakietu.                                                                                         |
| [`Copyright`](#copyright)                         | [`Copyright`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                                             | [`copyright`](https://docs.microsoft.com/nuget/reference/nuspec#copyright)                            | Szczegóły praw autorskich dla pakietu.                                                                                    |
| [`Licensing - Expression`](#licensing)            | [`PackageLicenseExpression`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)   | [`license type="expression"`](https://docs.microsoft.com/nuget/reference/nuspec#license)              | Wyrażenie licencji SPDX.                                                                                           |
| [`Licensing - File`](#licensing)                  | [`PackageLicenseFile`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)         | [`license type="file"`](https://docs.microsoft.com/nuget/reference/nuspec#license)                    | Ścieżka do niestandardowego pliku licencji.                                                                                        |
| [`Project URL`](#project-url)                     | `PackageProjectUrl`                                                                                                                       | [`projectUrl`](https://docs.microsoft.com/nuget/reference/nuspec#projecturl)                          | Adres URL strony głównej projektu.                                                                                       |
| [`Icon File`](#icon)                              | [`PackageIcon`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file)                                    | [`icon`](https://docs.microsoft.com/nuget/reference/nuspec#icon)                                      | Ścieżka do pliku obrazu ikony pakietu.                                                                                  |
| [`Repository URL`](#repository-type-and-url)      | [`RepositoryUrl`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                                     | [`repository url`](https://docs.microsoft.com/nuget/reference/nuspec#repository)                      | Adres URL repozytorium, z którego został sbudowaną zawartość pakietu.                                                               |
| [`Repository type`](#repository-type-and-url)     | [`RespositoryType`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                                   | [`repository type`](https://docs.microsoft.com/nuget/reference/nuspec#repository)                     | Typ repozytorium, na który wskazują adresy URL repozytorium (np. "git").                                                    |
| [`Tags`](#tags)                                   | [`PackageTags`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                                           | [`tags`](https://docs.microsoft.com/nuget/reference/nuspec#tags)                                      | Rozdzielana spacjami lista tagów i słów kluczowych opisujących pakiet. Tagi są używane podczas wyszukiwania pakietów.     |
| [`Release notes`](#release-notes)                 | [`PackageReleaseNotes`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                           | [`releaseNotes`](https://docs.microsoft.com/nuget/reference/nuspec#releasenotes)                      | Opis zmian wprowadzonych w tej wersji pakietu.                                                     |
### <a name="package-id"></a>Identyfikator pakietu

Jeśli publikujesz zupełnie nowy pakiet:

✔️ NALEŻY wybrać identyfikator pakietu, który jest unikatowy i wyraźnie odróżniany od istniejących pakietów w NuGet.org.
> Możesz sprawdzić, czy identyfikator pakietu jest unikatowy i można go odróżnić, wyszukując identyfikator na stronie NuGet.org lub sprawdzając, czy istnieje następujący link: https://www.nuget.org/packages/<package name \> .

✔️ ROZWAŻYĆ wybranie nazwy pakietu NuGet z prefiksem spełniającym kryteria rezerwacji [prefiksu](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria)NuGet.
> Zarezerwowanie identyfikatora prefiksu dla pakietu pozwoli uzyskać zweryfikowany znacznik wyboru: ![ image](media/Verified-check-mark.png)
> 
> Zapoznaj się z [dokumentami rezerwacji prefiksów identyfikatorów pakietów,](../nuget-org/id-prefix-reservation.md) aby dowiedzieć się więcej.

### <a name="package-version"></a>Wersja pakietu

✔️ rozważyć użycie [narzędzia SemVer do](https://semver.org/) wersji pakietu NuGet.
> Zasadniczo oznacza to użycie formatu Major.Minor.Patch[-prerelease].

✔️ OPUBLIKOWAĆ pakiet jako pakiet [wersji wstępnej,](./prerelease-packages.md) jeśli nie jest stabilny lub w wersji zapoznawczej.

Bardziej zaawansowane wskazówki można znaleźć w [przewodniku obsługi wersji biblioteki .NET.](/dotnet/standard/library-guidance/versioning)

### <a name="authors"></a>Autorzy

✔️ NALEŻY użyć pola author (autor) dla "pretty name" (dosyć nazwa) organizacji.
> Jeśli na przykład nazwa NuGet.org użytkownika to "jdoe", użycie pola "Jane Doe" w polu autora może ułatwić użytkownikom rozpoznawanie mnie jako autora. Jeśli nazwa użytkownika mojej NuGet.org to "ContosoToolkit", użycie nazwy "Contoso Corporation" może być bardziej rozpoznawalne i zainspirowane do większej zaufania klientów.
### <a name="description"></a>Opis

✔️ DO zawierają krótki opis (do 4000 znaków) opisujący pakiet.
> Opisy pakietów są jednym z najbardziej widocznych pól widocznych w wyszukiwaniu NuGet i prawdopodobnie będą pierwszą rzeczą, którą potencjalni klienci będą szukać, aby określić, czy pakiet jest dla nich odpowiedni.

### <a name="copyright"></a>Prawa autorskie

✔️ SIĘ O prawach autorskich do pakietu z "Copyright (c) <name/company \> <\> year".
>Informacja o prawach autorskich zasadniczo wskazuje, że nie można skopiować twojej pracy bez Twojej zgody. Powiadomienie o prawach autorskich w pakiecie jest łatwe i nie spowoduje żadnych szkód.

Przykład: Copyright (c) Contoso 2020

### <a name="licensing"></a>Licencjonowanie

✔️ DO [obejmują wyrażenie licencji lub plik licencji w pakiecie](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).
> [!IMPORTANT]
> Projekt bez licencji domyślnie ma wyłączną [wartość](https://choosealicense.com/no-permission/)praw autorskich, co oznacza, że nie udzielono nikomu uprawnień do korzystania z projektu.

❌ NIE UŻYWAJ przestarzałej `LicenseUrl` właściwości metadanych.
> Jest to niejednoznaczność prawna, ponieważ zmiany licencji pod adresem URL wstecznie zmienią wyświetloną licencję dla poprzednich wersji pakietu.

#### <a name="if-your-package-is-open-source"></a>Jeśli pakiet jest [open source](https://opensource.org/osd)

✔️ NALEŻY [wybrać licencję open source,](https://choosealicense.com/) aby pakiet open source.
> *"Licencje typu open source to licencje zgodne z definicją open source — w skrócie umożliwiają one bezpłatne wykorzystanie, modyfikację i współużytkowanie oprogramowania".* — Inicjatywa open source. Aby dowiedzieć się więcej na temat open source oprogramowania i inicjatywy open source, zapoznaj się z https://opensource.org/ tematem .

✔️ rozważ [uwzględnienie wyrażenia licencji w pakiecie](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).
> Wyrażenia licencji są widoczne w sposób najbardziej czytelny i bardziej oczywiste dla użytkowników, jeśli mogą korzystać z Twojego pakietu lub jeśli licencja została zmieniona. 
> [!Note]
> NuGet.org akceptuje tylko wyrażenia licencji dla licencji zatwierdzonych przez inicjatywę Open Source Initiative lub Free Software Foundation.

#### <a name="if-your-package-is-not-open-source"></a>Jeśli pakiet nie jest open source

✔️ DO [obejmują plik licencji w pakiecie](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).
> Do pakietu można dodać dowolny plik licencji (txt lub md), w tym licencje standardowe. 

### <a name="project-url"></a>Adres URL projektu

✔️ rozważyć do uwzględnienia linku do skojarzonego projektu, repozytorium lub witryny internetowej firmy.
> Witryna projektu powinna mieć wszystko, co użytkownicy muszą wiedzieć o pakiecie, i prawdopodobnie będzie tam, gdzie użytkownicy poszukaj dokumentacji.

### <a name="icon"></a>Ikona

✔️ rozważyć [dodaniem ikony z pakietem,](../reference/msbuild-targets.md#packing-an-icon-image-file) aby ułatwić jego wizualne rozróżnienie. Jest to stosunkowo mały dodatek, który może poprawić postrzeganie jakości pakietu.
> Ikony mogą być specyficzne dla poszczególnych pakietów lub być logo marki.

✔️ UŻYWAĆ obrazu o rozdzielczości 128 x 128 i z przezroczystym tłem (PNG) w celu najlepszego wyświetlania wyników.
> Program NuGet automatycznie przeskaluje obraz do klienta, na który jest wyświetlany.

❌ NIE UŻYWAJ przestarzałej `IconUrl` właściwości metadanych.

### <a name="repository-type-and-url"></a>Typ i adres URL repozytorium

✔️ skonfigurowanie linku [źródłowego](/dotnet/standard/library-guidance/sourcelink) w celu automatycznego dodawania metadanych kontroli źródła do pakietu NuGet i ułatwienia debugowania biblioteki.
> Link źródłowy automatycznie dodaje `Repository URL` i `Repository Type` do metadanych pakietu. Dodaje również określone zatwierdzenie skojarzone z wersją pakietu.

### <a name="tags"></a>Tagi

✔️ DO obejmują kilka tagów z kluczowymi terminami związanymi z pakietem w celu zwiększenia możliwości odnajdywania.
> Tagi są brane pod uwagę w algorytmie wyszukiwania nuGet.org i są szczególnie przydatne w przypadku terminów, które nie znajdują się w identyfikatorze pakietu, ale są istotne.

Jeśli na przykład opublikowano pakiet w celu rejestrowania ciągów w konsoli, obejmowałbym następujące dane: "rejestrowanie, dziennik, konsola, ciąg, dane wyjściowe"

### <a name="release-notes"></a>Informacje o wersji

✔️ uwzględnianie informacji o wersji z każdą aktualizacją opisujących, jakie zmiany zostały wprowadzone.
> Chociaż informacje o wersji nie mają określonego formatu, zalecamy m.in.:
>
> 1. Fundamentalne zmiany
> 2. Nowe funkcje
> 3. Poprawki błędów
> 
> Jeśli już śledzisz informacje o wersji lub dziennik zmian w swoim repocie, możesz również dołączyć link do odpowiedniego pliku.

## <a name="related-topics"></a>Powiązane tematy

- [Tworzenie i publikowanie pakietu (wiersz polecenia dotnet)](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [Tworzenie i publikowanie pakietu (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio.md?tabs=netcore-cli)
