---
title: Najlepsze rozwiązania dotyczące tworzenia pakietów
description: Ogólny przewodnik z najlepszymi rozwiązaniami dotyczącymi tworzenia pakietów NuGet o wysokiej jakości.
author: chgill-MSFT
ms.author: chgill
ms.date: 09/17/2020
ms.topic: conceptual
ms.openlocfilehash: 7475cf655876f2c127e79a16ccf67c0c723d164f
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859073"
---
# <a name="package-authoring-best-practices"></a>Najlepsze rozwiązania dotyczące tworzenia pakietów

Te wskazówki mają na celu umożliwienie autorom pakietu NuGet uproszczonego odwołania do tworzenia i publikowania pakietów o wysokiej jakości. Przede wszystkim koncentrują się na najlepszych rozwiązaniach dotyczących pakietów, takich jak metadane i pakowanie. Aby uzyskać bardziej szczegółowe sugestie dotyczące tworzenia bibliotek o wysokiej jakości, zobacz [wskazówki dotyczące biblioteki Open Source](https://docs.microsoft.com/dotnet/standard/library-guidance/)dla platformy .NET.

## <a name="types-of-recommendations"></a>Typy zaleceń

W każdym artykule przedstawiono cztery typy zaleceń: **czy** należy **rozważyć**, **unikać** i **nie**. Typ zalecenia wskazuje, jak blisko należy postępować.

Prawie zawsze należy **przestrzegać zalecenia.** Na przykład:

✔️ zawierać Krótki opis pakietu, który opisuje jego znaczenie.

Z drugiej strony należy **rozważyć** zalecenia, które powinny być przestrzegane, ale istnieją uzasadnione wyjątki dla reguły:

✔️ ROZWAŻYĆ wybranie nazwy pakietu NuGet z prefiksem spełniającym [kryteria](https://docs.microsoft.com/nuget/reference/id-prefix-reservation)rezerwacji prefiksu NuGet.

**Należy unikać występowania** zaleceń, które zwykle nie są dobrym pomysłem, ale przerwanie reguły czasami ma sens:

❌ UNIKAj odwołań do pakietów NuGet, które wymagają dokładnej wersji.

A wreszcie **nie są** zalecenia wskazują coś, co należy prawie nigdy nie robić:

❌ NIE należy używać `LicenseUrl` Właściwości Metadata.

## <a name="create-a-nuget-package"></a>Tworzenie pakietu NuGet

Najnowsza zalecana metoda tworzenia pakietu NuGet pochodzi z [projektu w stylu zestawu SDK](https://docs.microsoft.com/nuget/resources/check-project-format). Właściwości projektu w stylu zestawu SDK, w tym [platformy docelowej](https://docs.microsoft.com/dotnet/standard/frameworks) i [metadanych pakietu](#package-metadata), są zdefiniowane w [pliku projektu](https://docs.microsoft.com/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file).

Utwórz pakiet z projektu w stylu zestawu SDK, definiując wymagane właściwości i pakowanie w programie [Visual Studio](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli) lub [interfejsie wiersza polecenia dotnet](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli).

✔️ utworzyć projekt w stylu zestawu SDK i utworzyć pakiet (pakiet) przy użyciu programu Visual Studio lub interfejsu wiersza polecenia dotnet.

Aby uzyskać bardziej szczegółowe wskazówki dotyczące tworzenia pakietów, w tym niezbędnych narzędzi klienta, przykładu pliku projektu i poleceń, zobacz [Tworzenie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet](https://docs.microsoft.com/nuget/create-packages/creating-a-package-dotnet-cli).

Aby ułatwić podjęcie decyzji o tym, które platformy .NET Framework mają być przeznaczone, zobacz nasze [najnowsze wskazówki dotyczące ukierunkowanych na wiele platform](https://docs.microsoft.com/dotnet/standard/library-guidance/cross-platform-targeting).

## <a name="package-metadata"></a>Metadane pakietu

Metadane to podstawowe składniki dowolnego pakietu NuGet. Jakość metadanych może mieć ogromny wpływ na wykrywalność, użyteczność i wiarygodność pakietu.

W programie Visual Studio zalecaną metodą określania metadanych pakietu jest przechodzenie do > projektu [nazwa projektu] > pakietu.

Elementy metadanych pakietu można także [określić bezpośrednio w pliku projektu](https://docs.microsoft.com/nuget/create-packages/creating-a-package-msbuild#set-properties).

Poniżej znajduje się mapowanie tabeli i opisywanie dostępnych elementów metadanych pakietu:

| Nazwa właściwości programu Visual Studio                   | [Plik projektu/nazwa właściwości programu MSBuild](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                          | [Nazwa właściwości nuspec](https://docs.microsoft.com/nuget/reference/nuspec#general-form-and-schema) | Opis                                                                                                       |
|-----------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| [`Package id`](#package-id)                   | [`PackageId`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageid)                                                            | [`id`](https://docs.microsoft.com/nuget/reference/nuspec#id)                                      | Nazwa lub identyfikator pakietu.                    |
| [`Package version`](#package-version)         | [`PackageVersion`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageversion)                                                  | [`version`](https://docs.microsoft.com/nuget/reference/nuspec#version)                            | Wersja pakietu NuGet.                                           |
| [`Authors`](#authors)                         | [`Authors`](https://docs.microsoft.com/dotnet/core/tools/csproj#authors)                                                                | [`authors`](https://docs.microsoft.com/nuget/reference/nuspec#authors)                            | Rozdzielana przecinkami lista autorów pakietów, często wykorzystująca nazwę "dbname" danej osoby lub organizacji.                             |
| [`Description`](#description)                 | [`Description`](https://docs.microsoft.com/dotnet/core/tools/csproj#description)                                                        | [`description`](https://docs.microsoft.com/nuget/reference/nuspec#description)                    | Opis pakietu.                                                                |
| [`Copyright`](#copyright)                     | [`Copyright`](https://docs.microsoft.com/dotnet/core/tools/csproj#copyright)                                                            | [`copyright`](https://docs.microsoft.com/nuget/reference/nuspec#copyright)                        | Szczegóły dotyczące praw autorskich pakietu.                                                                      |
| [`Licensing - Expression`](#licensing)        | [`PackageLicenseExpression`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file) | [`license type="expression"`](https://docs.microsoft.com/nuget/reference/nuspec#license)          | Wyrażenie licencji SPDX.       |
| [`Licensing - File`](#licensing)              | [`PackageLicenseFile`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)       | [`license type="file"`](https://docs.microsoft.com/nuget/reference/nuspec#license)                | Ścieżka do niestandardowego pliku licencji.                                               |
| [`Project URL`](#project-url)                 | `PackageProjectUrl`                                                                                                                     | [`projectUrl`](https://docs.microsoft.com/nuget/reference/nuspec#projecturl)                      | Adres URL strony głównej projektu.                                                                                   |
| [`Icon File`](#icon)                          | [`PackageIcon`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file)                                  | [`icon`](https://docs.microsoft.com/nuget/reference/nuspec#icon)                                  | Ścieżka do pliku obrazu ikony pakietu.                                                                      |
| [`Repository URL`](#repository-type-and-url)  | [`RepositoryUrl`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositoryurl)                                                    | [`repository url`](https://docs.microsoft.com/nuget/reference/nuspec#repository)               | Adres URL repozytorium, z którego został skompilowany pakiet.                                                           |
| [`Repository type`](#repository-type-and-url) | [`RepositoryType`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositorytype)                                                 | [`repository type`](https://docs.microsoft.com/nuget/reference/nuspec#repository)              | Typ repozytorium, do którego jest wskazywany adres URL repozytorium (tj. "Git").                                                   |
| [`Tags`](#tags)                               | [`PackageTags`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagetags)                                                        | [`tags`](https://docs.microsoft.com/nuget/reference/nuspec#tags)                                  | Rozdzielana spacjami Lista tagów i słów kluczowych, które opisują pakiet. Tagi są używane podczas wyszukiwania pakietów. |
| [`Release notes`](#release-notes)             | [`PackageReleaseNotes`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                                          | [`releaseNotes`](https://docs.microsoft.com/nuget/reference/nuspec#releasenotes)                  | Opis zmian wprowadzonych w tej wersji pakietu.                                                 |

### <a name="package-id"></a>Identyfikator pakietu

Jeśli publikujesz zupełnie nowy pakiet:

✔️ Wybierz identyfikator pakietu, który jest unikatowy i wyraźnie odróżnia się od istniejących pakietów w witrynie NuGet.org.
> Możesz sprawdzić, czy identyfikator pakietu jest unikatowy i differentiable, wyszukując identyfikator NuGet.org lub sprawdzając, czy istnieje następujące łącze: https://www.nuget.org/packages/<package nazwa \> .

✔️ ROZWAŻYĆ wybranie nazwy pakietu NuGet z prefiksem spełniającym [kryteria rezerwacji prefiksu](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation#id-prefix-reservation-criteria)NuGet.
> Zarezerwowanie identyfikatora prefiksu dla pakietu pozwoli uzyskać zweryfikowany znacznik wyboru: ![ obraz](media/Verified-check-mark.png)
> 
> Sprawdź [prefiks identyfikatora pakietu dokumentów rezerwacji](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation) , aby dowiedzieć się więcej.

### <a name="package-version"></a>Wersja pakietu

✔️ ROZWAŻYĆ użycie [SemVer](https://semver.org/) do wersji pakietu NuGet.
> Zasadniczo oznacza to użycie formatu główna. pomocnicza. poprawka [-wersja wstępna].

✔️ opublikować pakiet jako [pakiet w wersji wstępnej](https://docs.microsoft.com/nuget/create-packages/prerelease-packages) , jeśli jest on niestabilny lub w wersji zapoznawczej.

Zapoznaj się z przewodnikiem dotyczącym obsługi [wersji biblioteki .NET](https://docs.microsoft.com/dotnet/standard/library-guidance/versioning) , aby uzyskać bardziej zaawansowane wskazówki.

### <a name="authors"></a>Autorzy

✔️ Użyj pola Autor dla swojej organizacji lub "dbname".
> Na przykład jeśli moja NuGet.org Nazwa użytkownika to "JKowalski", a następnie użycie "Jan Nowak" dla pola Author może pomóc konsumentom rozpoznać mnie jako autora. Jeśli nazwa użytkownika NuGet.org organizacji jest "ContosoToolkit", użycie "Contoso Corporation" może być bardziej rozpoznawalne i stanowić bardziej zaufanie dla klientów.
### <a name="description"></a>Opis

✔️ zawierać Krótki opis (do 4000 znaków), aby opisać swój pakiet.
> Opisy pakietów to jedno z najbardziej widocznych pól, które zostały wyszukane w usłudze NuGet i prawdopodobnie jest to pierwsze, co potencjalni klienci będą mogli ustalić, czy pakiet jest dla nich odpowiedni.

### <a name="copyright"></a>Prawa autorskie

✔️ ROZWAŻYĆ prawa autorskie do pakietu "Copyright (c) <Name/Company \> <Year \> ".
>Informacja o prawach autorskich zasadniczo wskazuje, że nie można skopiować pracy bez zgody użytkownika. Dołączenie informacji o prawach autorskich do pakietu jest proste i nie powoduje żadnych szkód!

Przykład: Copyright (c) contoso 2020

### <a name="licensing"></a>Licencjonowanie

✔️ [uwzględnić w pakiecie wyrażenie licencji lub plik licencji](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).
> [!IMPORTANT]
> Projekt bez licencji domyślnej na [wyłączne prawa autorskie](https://choosealicense.com/no-permission/), co oznacza, że nie przyznano nikomu uprawnienia do korzystania z Twojego projektu.

❌ NIE należy używać przestarzałej `LicenseUrl` właściwości metadanych.
> Spowoduje to powstanie niejednoznaczności, ponieważ zmiany licencji w adresie URL spowodują wsteczną zmianę wyświetlonej licencji dla poprzednich wersji pakietu.

#### <a name="if-your-package-is-open-source"></a>Jeśli pakiet jest [otwartym źródłem](https://opensource.org/osd)

✔️ [Wybierz licencję Open Source](https://choosealicense.com/) , aby udostępnić pakiet jako aplikację Open Source.
> *"Licencje Open Source to licencje, które są zgodne z definicją Open Source — w skrócie umożliwiają one swobodne używanie, modyfikowanie i udostępnianie oprogramowania".* -Inicjatywa Open Source. Aby dowiedzieć się więcej na temat oprogramowania Open Source i inicjatywy Open Source, zapoznaj się z tematem https://opensource.org/ .

✔️ Rozważ [uwzględnienie wyrażenia licencji w pakiecie](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).
> Wyrażenia licencji są wyrzucane najbardziej jasno i sprawiają, że użytkownicy mogą korzystać z pakietu lub w przypadku zmiany licencji. 
> [!Note]
> NuGet.org akceptuje tylko wyrażenia licencji dla licencji zatwierdzonych przez inicjatywę Open Source lub bezpłatny program Software Foundation.

#### <a name="if-your-package-is-not-open-source"></a>Jeśli pakiet nie jest otwarty jako źródło

✔️ [uwzględnić w pakiecie plik licencji](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).
> Dowolny plik licencji (. txt lub. MD) można dodać do pakietu, w tym z licencjami niestandardowymi. 

### <a name="project-url"></a>Adres URL projektu

✔️ Rozważ uwzględnienie linku do skojarzonego projektu, repozytorium lub witryny sieci Web firmy.
> Witryna projektu powinna mieć dostęp do wszystkich użytkowników, którzy muszą znać pakiet i prawdopodobnie będą szukać dokumentacji.

### <a name="icon"></a>Ikona

✔️ Rozważ [uwzględnienie ikony z pakietem](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file) , aby ułatwić jej wizualne odróżnienie. Jest to stosunkowo małe dodanie, które może poprawić postrzeganie jakości pakietów.
> Ikony mogą być specyficzne dla poszczególnych pakietów lub być logo marki.

✔️ Użyj obrazu 128 x 128 i ma przezroczyste tło (PNG), aby uzyskać najlepsze wyniki.
> Pakiet NuGet automatycznie skaluje obraz do klienta, na którym jest wyświetlany.

❌ NIE należy używać przestarzałej `IconUrl` właściwości metadanych.

### <a name="repository-type-and-url"></a>Typ i adres URL repozytorium

✔️ ROZWAŻYĆ skonfigurowanie [linku źródłowego](https://docs.microsoft.com/dotnet/standard/library-guidance/sourcelink) , aby automatycznie dodawać metadane kontroli źródła do pakietu NuGet i ułatwić debugowanie biblioteki.
> Link źródłowy automatycznie dodaje `Repository URL` i `Repository Type` do metadanych pakietu. Dodaje również określone zatwierdzenie skojarzone z wersją pakietu.

### <a name="tags"></a>Tagi

✔️ Uwzględnij kilka tagów z kluczowymi terminami związanymi z pakietem, aby zwiększyć możliwości odnajdywania.
> Tagi są brane pod uwagę w pakiecie NuGet. algorytm wyszukiwania w organizacji i są szczególnie przydatne w przypadku warunków, które nie znajdują się w IDENTYFIKATORze pakietu, ale są istotne.

Na przykład, jeśli opublikowano pakiet w celu rejestrowania ciągów do konsoli programu, dołączam: "rejestrowanie, rejestrowanie, konsole, ciąg, wyjście"

### <a name="release-notes"></a>Informacje o wersji

✔️ Rozważ uwzględnienie informacji o wersji każdej aktualizacji opisującej, jakie zmiany zostały wprowadzone.
> Chociaż nie jest wymagany żaden konkretny format informacji o wersji, zalecamy włączenie:
>
> 1. Fundamentalne zmiany
> 2. Nowe funkcje
> 3. Poprawki błędów
> 
> Jeśli już śledzisz informacje o wersji lub dziennik zmian w repozytorium, możesz również dołączyć link do odpowiedniego pliku.

## <a name="related-topics"></a>Powiązane tematy

- [Tworzenie i publikowanie pakietu (wiersz polecenia dotnet)](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli)
- [Tworzenie i publikowanie pakietu (Visual Studio)](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli)
