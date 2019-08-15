---
title: Dokumentacja wersji pakietu NuGet
description: Dokładne szczegóły dotyczące określania numerów wersji i zakresów dla innych pakietów, od których zależy pakiet NuGet, oraz sposobu instalowania zależności.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 7c6992d6bf3142eb6aca70f1fa3c46f72efd25a0
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/14/2019
ms.locfileid: "69019997"
---
# <a name="package-versioning"></a>Przechowywanie wersji pakietów

Określony pakiet zawsze jest określany przy użyciu identyfikatora pakietu i dokładnego numeru wersji. Na przykład [Entity Framework](https://www.nuget.org/packages/EntityFramework/) w witrynie NuGet.org ma kilka dziesiątych dostępnych pakietów, od wersji *4.1.10311* do wersji *6.1.3* (Najnowsza stabilna wersja) i różne wersje wstępne, takie jak *6.2.0-beta1* .

Podczas tworzenia pakietu przypisujesz określony numer wersji z opcjonalnym sufiksem tekstu w wersji wstępnej. W przypadku używania pakietów, z drugiej strony, można określić dokładny numer wersji lub zakres akceptowalnych wersji.

W tym temacie:

- [Podstawy wersji](#version-basics) , w tym sufiksy wstępne.
- [Zakresy wersji i symbole wieloznaczne](#version-ranges-and-wildcards)
- [Znormalizowane numery wersji](#normalized-version-numbers)

## <a name="version-basics"></a>Podstawy wersji

Określony numer wersji ma postać *główna. pomocnicza. poprawka [-sufiks]* , gdzie składniki mają następujące znaczenie:

- *Wersja główna*: Fundamentalne zmiany
- *Drobny*: Nowe funkcje, ale zgodność z poprzednimi wersjami
- *Poprawka*: Tylko poprawki zgodne z poprzednimi usterkami
- *-Sufiks* (opcjonalnie): Łącznik, po którym następuje ciąg oznaczający wersję wstępną (zgodnie z Konwencją o [wersji semantycznej lub SemVer 1,0](http://semver.org/spec/v1.0.0.html)).

**Przykłady:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org odrzuca przekazywanie pakietów, które nie mają dokładnego numeru wersji. Wersja musi być określona w `.nuspec` pliku projektu lub użytym do utworzenia pakietu.

### <a name="pre-release-versions"></a>Wersje wstępne

Mówiąc technicznie, twórcy pakietów mogą używać dowolnego ciągu jako sufiksu do oznaczania wersji wstępnej, ponieważ NuGet traktuje wszystkie takie wersje jako wersji wstępnej i nie wykonuje żadnej innej interpretacji. Oznacza to, że pakiet NuGet wyświetla pełny ciąg wersji w dowolnym interfejsie użytkownika, pozostawiając wszelką interpretację znaczenia sufiksu dla konsumenta.

Wspomniane w ten sposób deweloperzy pakietów zazwyczaj przestrzegają rozpoznawanych konwencji nazewnictwa:

- `-alpha`: Wydanie Alpha, zwykle używane do pracy w toku i eksperymentowania.
- `-beta`: Wydanie beta — zwykle jest to funkcja zakończona dla następnej planowanej wersji, ale może zawierać znane usterki.
- `-rc`: Wersja Release Candidate, zazwyczaj wersja, która jest potencjalnie końcowa (stabilna), chyba że nastąpiły znaczne błędy.

> [!Note]
> Pakiet NuGet 4.3.0 + obsługuje [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), który obsługuje numery wersji wstępnej z notacją kropkową, tak jak w przypadku *1.0.1-Build. 23*. Notacja kropki nie jest obsługiwana w wersjach NuGet przed 4.3.0. Możesz użyć formularza, takiego jak *1.0.1-build23*.

Przy rozwiązywaniu odwołań do pakietów i wielu wersjach pakietów różni się tylko sufiksem, pakiet NuGet wybiera wersję bez sufiksu, a następnie stosuje pierwszeństwo w wersji wstępnej w odwrotnej kolejności alfabetycznej. Na przykład następujące wersje zostałyby wybrane w dokładnie pokazanej kolejności:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>2\.0.0 wersji semantycznej

Dzięki narzędziom NuGet 4.3.0 + i Visual Studio 2017 w wersji 15.3 + pakiet NuGet obsługuje [semantykę wersji 2.0.0](http://semver.org/spec/v2.0.0.html).

Niektóre semantyka SemVer v 2.0.0 nie są obsługiwane przez starszych klientów. Pakiet NuGet traktuje wersję pakietu jako SemVer v 2.0.0, jeśli jedno z następujących instrukcji jest prawdziwe:

- Etykieta wersji wstępnej jest oddzielona kropką, na przykład *1.0.0-alpha. 1*
- Wersja zawiera metadane kompilacji, na przykład *1.0.0 + githash*

W przypadku nuget.org pakiet jest zdefiniowany jako pakiet SemVer v 2.0.0, jeśli jest spełniony jeden z następujących instrukcji:

- Własna wersja pakietu to SemVer v 2.0.0 zgodna, ale nie SemVer v 1.0.0 zgodna, zgodnie z definicją powyżej.
- Dowolna z zakresów wersji zależności pakietu ma wersję minimalną lub maksymalną, która jest zgodna z SemVer v 2.0.0, ale nie SemVer v 1.0.0 zgodna z definicją powyżej; na przykład *[1.0.0-alpha. 1,)* .

W przypadku przekazania pakietu SemVer v 2.0.0 do nuget.org pakiet jest niewidoczny dla starszych klientów i dostępny tylko dla następujących klientów NuGet:

- NuGet 4.3.0+
- Visual Studio 2017 w wersji 15.3 +
- Visual Studio 2015 z pakietem [NuGet VSIX v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore. exe (zestaw SDK 2.0.0 +)

Klienci innych firm:

- JetBrains
- Paket w wersji 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Zakresy wersji i symbole wieloznaczne

W przypadku odwoływania się do zależności pakietów NuGet obsługuje używanie notacji interwału do określania zakresów wersji, podsumowywane w następujący sposób:

| Służąc | Zastosowana reguła | Opis |
|----------|--------------|-------------|
| 1.0 | x ≥ 1,0 | Minimalna wersja, włącznie |
| (1.0,) | x > 1,0 | Wersja minimalna, wyłączna |
| [1.0] | x == 1.0 | Dopasowanie dokładnej wersji |
| (,1.0] | x ≤ 1,0 | Maksymalna wersja, włącznie |
| (,1.0) | x < 1,0 | Maksymalna wersja, wyłączna |
| [1.0,2.0] | 1,0 ≤ x ≤ 2,0 | Dokładny zakres, włącznie |
| (1.0,2.0) | 1,0 < x < 2,0 | Dokładny zakres, wyłączny |
| [1.0,2.0) | 1,0 ≤ x < 2,0 | Mieszana wartość minimalna i wyłączna wersja Maksymalna |
| (1.0)    | nieprawidłowe | nieprawidłowe |

W przypadku korzystania z formatu PackageReference, pakiet NuGet obsługuje również korzystanie z notacji \*wieloznacznej, w przypadku elementów głównych, pomocniczych, poprawek i prefiksu w wersji wstępnej. Symbole wieloznaczne nie są obsługiwane w `packages.config` formacie.

> [!Note]
> Zakresy wersji w programie PackageReference obejmują wersje wstępne. Zgodnie z projektem wersje zmiennoprzecinkowe nie rozwiązują wersji wstępnych, chyba że zostały uwzględnione w. Aby uzyskać stan żądania powiązanej funkcji, zobacz [problem 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).

### <a name="examples"></a>Przykłady

Należy zawsze określać wersję lub zakres wersji dla zależności pakietów w plikach projektu `packages.config` , plikach i `.nuspec` plikach. Bez wersji lub zakresu wersji, program NuGet 2.8. x i wcześniejsza wersja wybiera najnowszą dostępną wersję pakietu podczas rozpoznawania zależności, natomiast w przypadku programu NuGet 3. x lub nowszego jest wybierana najniższa wersja pakietu. Określenie wersji lub zakresu wersji pozwala uniknąć tej niepewności.

#### <a name="references-in-project-files-packagereference"></a>Odwołania w plikach projektu (PackageReference)

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

**Odwołania w `packages.config`:**

W `packages.config`programie każda zależność jest wyświetlana z dokładnym `version` atrybutem używanym podczas przywracania pakietów. Ten `allowedVersions` atrybut jest używany tylko podczas operacji aktualizowania, aby ograniczyć wersje, do których pakiet może zostać zaktualizowany.

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

**Odwołania w `.nuspec` plikach**

`version` Atrybut`<dependency>` w elemencie opisuje wersje zakresu, które są akceptowalne dla zależności.

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a>Znormalizowane numery wersji

> [!Note]
> Jest to istotna zmiana dotycząca programu NuGet 3,4 i nowszych wersji.

Podczas uzyskiwania pakietów z repozytorium podczas operacji instalacji, ponownego instalowania lub przywracania program NuGet 3.4 + traktuje numery wersji w następujący sposób:

- Zera wiodące są usuwane z numerów wersji:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Zero w czwartej części numeru wersji zostanie pominięte

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

`pack`i `restore` operacje normalizuje wersje wszędzie tam, gdzie to możliwe. W przypadku pakietów, które zostały już skompilowane, normalizacja nie ma wpływu na numery wersji w samych pakietach; ma wpływ tylko na to, jak program NuGet dopasowuje wersje podczas rozpoznawania zależności.

Jednak repozytoria pakietów NuGet musi traktować te wartości w taki sam sposób jak NuGet, aby zapobiec duplikowaniu wersji pakietu. W ten sposób repozytorium zawierające wersję *1,0* pakietu nie powinno również hostować wersji *1.0.0* jako oddzielnego i innego pakietu.
