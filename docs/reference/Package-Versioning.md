---
title: Odwołanie do wersji pakietu NuGet
description: Szczegółowymi informacjami na temat na temat określania numerów wersji i zakresy dla innych pakietów, od którego zależy od pakietu NuGet i jak zależności są zainstalowane.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: b980c1084fe8e31573053a4dcf38bbfa6146e6de
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549776"
---
# <a name="package-versioning"></a>Przechowywanie wersji pakietów

Określony pakiet zawsze jest określany za pomocą jego identyfikatora pakietu i liczbą dokładna wersja. Na przykład [Entity Framework](https://www.nuget.org/packages/EntityFramework/) w witrynie nuget.org zawiera kilka tuzinów określone pakiety dostępne od wersji *4.1.10311* do wersji *6.1.3* (Najnowsza wersja stabilna wydania) i różne wersje wstępne, takie jak *6.2.0-beta1*.

Tworząc pakiet, możesz przypisać odpowiedniego numeru wersji sufiks opcjonalny tekst wersji wstępnej. Podczas korzystania z pakietów, z drugiej strony, można określić numeru wersji dokładne lub zakres dopuszczalnych wersji.

W tym temacie:

- [Podstawowe informacje o wersji](#version-basics) tym sufiksy wersji wstępnej.
- [Zakresów wersji i symboli wieloznacznych](#version-ranges-and-wildcards)
- [Numery wersji znormalizowana](#normalized-version-numbers)

## <a name="version-basics"></a>Podstawowe informacje o wersji

Numer wersji określonego ma postać *Wersja_główna.WERSJA_POMOCNICZA.poprawka [-sufiks]*, których składniki mają następujące znaczenie:

- *Główne*: fundamentalne zmiany
- *Drobne*: nowe funkcje, ale wstecznie zgodne
- *Poprawka*: wstecznie zgodna tylko poprawki.
- *-Sufiks* (opcjonalnie): łącznik następuje ciąg oznaczający wersji wstępnej (następujących [Konwencji Semantic Versioning lub SemVer 1.0](http://semver.org/spec/v1.0.0.html)).

**Przykłady:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org odrzuca wszelkie przekazywania pakietu, który nie ma numeru wersji dokładne. Wersja musi być określona w `.nuspec` lub plik projektu do utworzenia pakietu.

### <a name="pre-release-versions"></a>Wersje wstępne

Technicznie rzecz biorąc, twórców pakietów można użyć jako sufiks dowolnego ciągu do oznaczania wersji wstępnej, jak NuGet traktuje takie wersji jako wersji wstępnej i sprawia, że nie inne interpretacji. Oznacza to wyświetla NuGet pełną wersję ciągu, niezależnie od interfejsu użytkownika uczestniczy, pozostawiając żadnej interpretacji znaczenie tego sufiksu konsumenta.

Inaczej mówiąc, deweloperów pakietu zazwyczaj korzystają z rozpoznanym konwencji nazewnictwa:

- `-alpha`: Wydanie alfa, zwykle używane do pracy w toku i eksperymentowanie.
- `-beta`: Wydania beta, zazwyczaj taki, który jest funkcja ukończone przez następne zaplanowane wersji, ale może zawierać znanych błędów.
- `-rc`: W wersji Release candidate, zwykle wydania jest potencjalnie ostateczne (stable), chyba że wyłaniać znaczące błędy.

> [!Note]
> Obsługuje NuGet 4.3.0+ [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), który obsługuje numerów wersji wstępnej przy użyciu notacji z kropką, podobnie jak w *1.0.1-build.23*. Kropkowego jest nieobsługiwane w przypadku wersje NuGet wcześniejsze niż 4.3.0. Można użyć formy, takich jak *1.0.1-build23*.

Podczas rozpoznawania odwołań do pakietów i wiele wersji pakietu różnią się jedynie sufiks, NuGet najpierw wybierze wersji bez sufiksu, a następnie stosuje pierwszeństwo wersji wstępnych w odwrotnej kolejności alfabetycznej. Na przykład następujące wersje powinny być wybierane w takiej kolejności, które są wyświetlane:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Semantic Versioning 2.0.0

Za pomocą NuGet 4.3.0+ i programu Visual Studio 2017 w wersji 15.3 + obsługuje NuGet [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).

Niektóre semantyki SemVer v2.0.0 nie są obsługiwane w starszych klientów. NuGet uwzględnia wersję pakietu do określonego v2.0.0 SemVer, jeśli jest spełniony jeden z następujących instrukcji:

- Przed wydaniem etykieta jest oddzielona, na przykład *1.0.0-alpha.1*
- Wersja ma metadane kompilacji, na przykład *1.0.0+githash*

Dla nuget.org pakiet jest zdefiniowana jako pakiet v2.0.0 SemVer, jeśli spełniony jest dowolny z następujących instrukcji:

- Wersja tego pakietu jest v2.0.0 SemVer zgodne, ale nie SemVer 1.0.0 zgodne, jak określono powyżej.
- Żadnego z zakresów wersji zależności pakietu ma minimalnych i maksymalnych wersji v2.0.0 SemVer zgodne, ale nie SemVer 1.0.0 zgodne, zdefiniowane powyżej. na przykład *[1.0.0-alpha.1,)*.

Jeśli załadujesz pakietu specyficzne dla v2.0.0 SemVer na stronie nuget.org, pakiet jest niewidoczne dla starszych klientów i dostępne, aby tylko następujących klientów NuGet:

- NuGet 4.3.0+
- Visual Studio 2017 w wersji 15.3 +
- Visual Studio 2015 z [v3.6.0 NuGet VSIX](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- polecenia DotNet
  - dotnetcore.exe (2.0.0+ zestawu .NET SDK)

Klienci firm:

- Kierowcy JetBrains
- Paket w wersji 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Zakresów wersji i symboli wieloznacznych

W odniesieniu do zależności pakietów NuGet obsługuje przy użyciu notacji interwału do określania zakresów wersji, podsumować w następujący sposób:

| Notacja | Zastosowana reguła | Opis |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | Minimalna wersja (włącznie) |
| (1.0,) | x > 1.0 | Minimalna wersja wyłączne |
| [1.0] | x == 1.0 | Dokładna wersja dopasowania |
| (,1.0] | x ≤ 1.0 | Maksymalna wersja (włącznie) |
| (,1.0) | x < 1.0 | Maksymalna wersja wyłączne |
| [1.0,2.0] | X ≤ 1.0 ≤ w wersji 2.0 | Dokładny zakres (włącznie) |
| (1.0,2.0) | 1.0 < x < w wersji 2.0 | Dokładny zakres wyłączne |
| [1.0,2.0) | 1.0 ≤ x < w wersji 2.0 | Mieszane włącznie minimalną i wyłączne maksymalna wersja |
| (1.0)    | nieprawidłowe | nieprawidłowe |

Gdy w formacie PackageReference NuGet obsługuje również za pomocą notacji symbolu wieloznacznego, \*, główne, pomocnicze, poprawki i sufiks wersji wstępnej części numeru. Symbole wieloznaczne nie są obsługiwane z `packages.config` formatu.

> [!Note]
> Wersje wstępne nie są uwzględniane podczas rozpoznawania zakresów wersji. Wersji wstępnych *są* uwzględniana podczas użycie symbolu wieloznacznego (\*). Zakres wersji *[1.0,2.0]*, na przykład, nie ma w wersji 2.0 w wersji beta, ale notacji symbolu wieloznacznego _w wersji 2.0 — *_ jest. Zobacz [wystawiać 912](https://github.com/NuGet/Home/issues/912) do dalszego dyskusji na temat symboli wieloznacznych w wersji wstępnej.

### <a name="examples"></a>Przykłady

Zawsze określać wersja lub zakres wersji w przypadku zależności pakietów w plikach projektu `packages.config` plików, a `.nuspec` plików. Bez wersji lub zakres wersji, NuGet 2.8.x, a wcześniej najnowszej wersji pakietu dostępne podczas rozpoznawania zależności natomiast NuGet 3.x, a później Najniższa wersja pakietu. Określanie wersji lub czy zakres pozwala uniknąć niepewności.

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

**Przywoływane w `packages.config`:**

W `packages.config`, zależności, co jest wyświetlany na liście dokładnie `version` atrybut, który jest używany podczas przywracania pakietów. `allowedVersions` Atrybut jest używany tylko podczas operacji aktualizacji, ograniczenie wersji, do których pakiet mogły zostać zaktualizowane.

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

**Przywoływane w `.nuspec` plików**

`version` Atrybutu w `<dependency>` element zawiera opis wersji zakresu, które mogą być stosowane dla zależności.

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any 6.x.y version. -->
<dependency id="ExamplePackage" version="6.*" />

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

## <a name="normalized-version-numbers"></a>Numery wersji znormalizowana

> [!Note]
> Jest to istotną zmianę dla NuGet 3.4 i nowszych.

Podczas uzyskiwania pakietów z repozytorium, podczas instalacji, ponownie zainstaluj lub operacji przywracania NuGet 3.4 + traktuje numery wersji w następujący sposób:

- Zer wiodących są usuwane z numerami wersji:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- W czwartej części numeru wersji wartość zero zostanie pominięta.

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

Ta normalizacji nie ma wpływu na numery wersji pakietów. ma to wpływ, jak NuGet jest zgodny tylko wersje podczas rozpoznawania zależności.

Jednak repozytoriów pakietów NuGet musi traktować te wartości w taki sam sposób jak NuGet, aby uniknąć duplikowania wersji pakietu. Tym samym repozytorium, które zawiera wersję *1.0* pakietu nie powinien również hostować wersji *1.0.0* jako oddzielny i inny pakiet.
