---
title: Odwołanie do wersji pakietu NuGet
description: Dokładne szczegóły dotyczące określania numerów wersji i zakresów dla innych pakietów, od których zależy pakiet NuGet i jak są instalowane zależności.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: c79976c2f4ded2fba3796fb847d3c90807d7b86c
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "80147451"
---
# <a name="package-versioning"></a>Przechowywanie wersji pakietów

Określony pakiet jest zawsze odwoływany przy użyciu jego identyfikator pakietu i dokładny numer wersji. Na przykład [entity framework](https://www.nuget.org/packages/EntityFramework/) na nuget.org ma kilkadziesiąt konkretnych pakietów dostępnych, od wersji *4.1.10311* do wersji *6.1.3* (najnowsza stabilna wersja) i różnych wersji przedpremierowych, takich jak *6.2.0-beta1*.

Podczas tworzenia pakietu należy przypisać określony numer wersji z opcjonalnym sufiksem tekstu w wersji wstępnej. Podczas korzystania z pakietów, z drugiej strony, można określić dokładny numer wersji lub zakres dopuszczalnych wersji.

W tym temacie:

- [Podstawy wersji,](#version-basics) w tym sufiksy wersji wstępnej.
- [Zakresy wersji](#version-ranges)
- [Znormalizowane numery wersji](#normalized-version-numbers)

## <a name="version-basics"></a>Podstawy wersji

Określony numer wersji jest w postaci *Major.Minor.Patch[-Sufiks]*, gdzie składniki mają następujące znaczenie:

- *Główne*: Przełomowe zmiany
- *Minor*: Nowe funkcje, ale wstecznie kompatybilne
- *Poprawka:* Tylko poprawki błędów zgodne z powrotem
- *-Sufiks* (opcjonalnie): myślnik, po którym następuje ciąg oznaczający wersję wstępną (po [konwencji Semantic Versioning lub SemVer 1.0).](https://semver.org/spec/v1.0.0.html)

**Przykłady:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org odrzuca wszystkie przesłane pakiety, które nie mają dokładnego numeru wersji. Wersja musi być określona `.nuspec` w pliku lub projektu użytym do utworzenia pakietu.

### <a name="pre-release-versions"></a>Wersje w wersji wstępnej

Technicznie rzecz biorąc twórcy pakietu mogą używać dowolnego ciągu jako sufiksu do oznaczania wersji wstępnej, ponieważ NuGet traktuje dowolną taką wersję jako wersję wstępną i nie wykonuje żadnej innej interpretacji. Oznacza to, że NuGet wyświetla ciąg pełnej wersji w cokolwiek interfejsu użytkownika jest zaangażowany, pozostawiając wszelkie interpretacji znaczenia sufiksu do konsumenta.

Mimo to deweloperzy pakietów zazwyczaj przestrzegają uznanych konwencji nazewnictwa:

- `-alpha`: Alpha release, zwykle używane do pracy w toku i eksperymentowania.
- `-beta`: Wersja beta, zazwyczaj taka, która jest kompletna dla następnej planowanej wersji, ale może zawierać znane błędy.
- `-rc`: Release candidate, zazwyczaj wydanie, które jest potencjalnie ostateczne (stabilne), chyba że pojawią się istotne błędy.

> [!Note]
> NuGet 4.3.0+ obsługuje [semver 2.0.0](https://semver.org/spec/v2.0.0.html), który obsługuje numery wersji wstępnej z notacją kropkową, jak w *1.0.1-build.23*. Notacja kropki nie jest obsługiwana w wersjach NuGet przed wersją 4.3.0. Można użyć formularza takiego jak *1.0.1-build23*.

Podczas rozwiązywania odwołań do pakietu i wielu wersji pakietu różnią się tylko przez sufiks, NuGet wybiera wersję bez sufiksu pierwszy, a następnie stosuje pierwszeństwo do wersji przed wydaniem w odwrotnej kolejności alfabetycznej. Na przykład w podanej kolejności zostaną wybrane następujące wersje:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Przechowywanie wersji semantycznych 2.0.0

Z NuGet 4.3.0+ i Visual Studio 2017 w wersji 15.3+, NuGet obsługuje [semantyczne przechowywanie wersji 2.0.0](https://semver.org/spec/v2.0.0.html).

Niektóre semantyki SemVer v2.0.0 nie są obsługiwane w starszych klientów. NuGet uważa, że wersja pakietu jest SemVer v2.0.0 specyficzne, jeśli którakolwiek z następujących instrukcji jest spełniony:

- Etykieta wydania wstępnego jest oddzielona kropkami, na przykład *1.0.0-alfa.1*
- Wersja ma build-metadane, na przykład *1.0.0+ githash*

Dla nuget.org pakiet jest zdefiniowany jako pakiet SemVer w wersji 2.0.0, jeśli spełniony jest jeden z następujących instrukcji:

- Wersja własna pakietu jest zgodna ze standardem SemVer v2.0.0, ale nie zgodna ze standardem SemVer v1.0.0, jak zdefiniowano powyżej.
- Każdy z zakresów wersji zależności pakietu ma minimalną lub maksymalną wersję, która jest zgodna z SemVer v2.0.0, ale nie jest zgodna z SemVer v1.0.0, zdefiniowana powyżej; na przykład *[1.0.0-alfa.1, ).*

Jeśli przekażesz pakiet specyficzny dla SemVer w wersji 2.0.0 do nuget.org, pakiet jest niewidoczny dla starszych klientów i dostępny tylko dla następujących klientów NuGet:

- NuGet 4.3.0+
- Visual Studio 2017 w wersji 15.3+
- Visual Studio 2015 z [NuGet VSIX w wersji 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore.exe (.NET SDK 2.0.0+)

Klienci zewnętrzni:

- JetBrains Rider
- Paket wersja 5.0+

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a>Zakresy wersji

Odnosząc się do zależności pakietów, NuGet obsługuje przy użyciu notacji interwału do określania zakresów wersji, podsumowane w następujący sposób:

| Notacja | Reguła stosowana | Opis |
|----------|--------------|-------------|
| 1.0 | x ≥ 1,0 | Wersja minimalna włącznie |
| (1.0,) | x > 1.0 | Wersja minimalna, ekskluzywna |
| [1.0] | x == 1,0 | Dokładne dopasowanie wersji |
| (,1.0] | x ≤ 1,0 | Maksymalna wersja włącznie |
| (,1.0) | x < 1.0 | Maksymalna wersja, ekskluzywna |
| [1.0,2.0] | 1,0 ≤ x ≤ 2,0 | Dokładny zakres, włącznie |
| (1.0,2.0) | 1,0 < x < 2,0 | Dokładny zakres, ekskluzywny |
| [1.0,2.0) | 1,0 ≤ x < 2,0 | Mieszana minimalna i ekskluzywna wersja maksymalna włącznie |
| (1.0)    | nieprawidłowe | nieprawidłowe |

Podczas korzystania z PackageReference format, NuGet obsługuje \*również przy użyciu zmiennoprzecinkowy notacji, dla głównych, minor, patch i pre-release sufiks części numeru. Wersje przestawne nie `packages.config` są obsługiwane w formacie.

> [!Note]
> Zakresy wersji w PackageReference obejmują wersje wstępne. Zgodnie z projektem wersje przestawne nie rozwiązują wersji wstępnej, chyba że zostanie to uwzględnione. Aby uzyskać stan powiązanego żądania funkcji, zobacz [problem 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).

### <a name="examples"></a>Przykłady

Zawsze określ zakres wersji lub wersji dla `packages.config` zależności pakietów w plikach, plikach i `.nuspec` plikach projektu. Bez zakresu wersji lub wersji NuGet 2.8.x i wcześniej wybiera najnowszą dostępną wersję pakietu podczas rozpoznawania zależności, podczas gdy NuGet 3.x i nowsze wybiera najniższą wersję pakietu. Określenie zakresu wersji lub wersji pozwala uniknąć tej niepewności.

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

**Odniesienia w: `packages.config`**

W `packages.config`obszarze , każda zależność `version` jest wyświetlana z dokładnym atrybutem, który jest używany podczas przywracania pakietów. Atrybut `allowedVersions` jest używany tylko podczas operacji aktualizacji, aby ograniczyć wersje, do których pakiet może być aktualizowany.

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

Atrybut `version` w elemencie `<dependency>` opisuje wersje zakresu, które są dopuszczalne dla zależności.

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
> Jest to przełomowa zmiana dla NuGet 3.4 i nowsze.

Podczas uzyskiwania pakietów z repozytorium podczas operacji instalacji, ponownej instalacji lub przywracania nuget 3.4+ traktuje numery wersji w następujący sposób:

- Zera wiodące są usuwane z numerów wersji:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Zero w czwartej części numeru wersji zostanie pominięte

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1
        
- Metadane kompilacji SemVer 2.0.0 są usuwane

        1.0.7+r3456 is treated as 1.0.7

`pack`i `restore` operacje normalizują wersje, gdy tylko jest to możliwe. W przypadku pakietów już utworzonych ta normalizacja nie wpływa na numery wersji w samych pakietach; wpływa tylko na to, jak NuGet dopasowuje wersje podczas rozpoznawania zależności.

Jednak repozytoria pakietów NuGet muszą traktować te wartości w taki sam sposób jak NuGet, aby zapobiec duplikowaniu wersji pakietu. W związku z tym repozytorium, które zawiera wersję *1.0* pakietu nie należy również hostować wersji *1.0.0* jako oddzielny i inny pakiet.
