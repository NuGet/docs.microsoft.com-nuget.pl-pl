---
title: Odwołanie do pakietu NuGet w wersji | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/23/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Dokładne szczegóły dotyczące określania numery wersji i zakresy dla innych pakietów, od którego zależy od pakietu NuGet i jak zależności są zainstalowane.
keywords: przechowywanie wersji, zależności pakietów NuGet, wersje zależności NuGet, numery wersji NuGet, wersja pakietu NuGet, zakresy wersji, specyfikacji wersji, numery wersji znormalizowane
ms.reviewer:
- anandr
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 678ad79d9106a9f592ae4f47bc93cc117496e2c9
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="package-versioning"></a>Przechowywanie wersji pakietu

Określony pakiet jest zawsze określone za pomocą jego identyfikatora pakietu i numer dokładnej wersji. Na przykład [Entity Framework](https://www.nuget.org/packages/EntityFramework/) nuget.org ma kilka dozen określonych pakietów dostępne począwszy od wersji *4.1.10311* do wersji *6.1.3* (najnowsze stały Zwolnij) i różne wersje wstępne, takich jak *6.2.0-beta1*.

Podczas tworzenia pakietu, należy przypisać numer określoną wersję z sufiksem opcjonalny tekst wersji wstępnej. Podczas używania pakietów, z drugiej strony, można określić liczby dokładnej wersji lub zakresu akceptowalnych wersji.

W tym temacie:

- [Podstawowe informacje o wersji](#version-basics) tym sufiksy wersji wstępnej.
- [Zakresy wersji i symboli wieloznacznych](#version-ranges-and-wildcards)
- [Numery wersji znormalizowane](#normalized-version-numbers)

## <a name="version-basics"></a>Podstawowe informacje o wersji

Numer wersji ma postać *Wersja_główna.WERSJA_POMOCNICZA.poprawka [-sufiks]*, których składniki mają następujące znaczenie:

- *Główne*: fundamentalne zmiany
- *Drobne*: nowe funkcje, ale wstecznie zgodne
- *Poprawka*: wstecznie zgodna tylko poprawki.
- *-Sufiks* (opcjonalnie): łącznika następuje ciąg oznaczający wersji wstępnej (następujące [Wersjonowania semantycznego lub 1.0 programu SemVer Konwencji](http://semver.org/spec/v1.0.0.html)).

**Przykłady:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org odrzuca wszystkie przekazywanie pakietu, który nie ma numer wersji dokładne. Wersja musi być określony w `.nuspec` lub plik projektu używany do utworzenia pakietu.

### <a name="pre-release-versions"></a>Wersje wstępne

Jak to działa, twórców pakietu można użyć jako sufiks dowolnego ciągu określający wersję wstępną NuGet traktuje takie wersji jako wstępną i sprawia, że nie inne interpretacji. Oznacza to pełną wersję ciąg w dowolnie wybrany interfejs użytkownika wyświetla NuGet uczestniczy, pozostawiając żadnej interpretacji znaczenie sufiks konsumenta.

Inaczej mówiąc, deweloperzy pakietu należy wykonać rozpoznanym konwencji nazewnictwa:

- `-alpha`: Wersja alfa zwykle używany w przypadku pracy w toku i eksperymenty.
- `-beta`: Wydania beta, zazwyczaj jest pełną Następna funkcja planowane wersji, ale może zawierać znanych błędów.
- `-rc`: Wersji release candidate, zwykle potencjalnie ostateczną zlecenia (stable), chyba że wyłonić znaczących usterki.

> [!Note]
> Obsługuje NuGet 4.3.0+ [programu SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), który obsługuje numerów wersji wstępnej mają kropkowego, podobnie jak w *1.0.1-build.23*. Kropkowego nie jest obsługiwany w wersjach NuGet przed 4.3.0. Można użyć formularza, takich jak *1.0.1-build23*.

Podczas rozpoznawania odwołania do pakietu i wiele wersji pakietu różnią się jedynie sufiks, NuGet wybierze wersji bez sufiksu najpierw, a następnie stosuje pierwszeństwo wersji wstępnych w odwrotnej kolejności alfabetycznej. Na przykład w pokazanej kolejności dokładne zostałaby wybrana następujące wersje:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Wersjonowania semantycznego 2.0.0

NuGet 4.3.0+ i Visual Studio 2017 wersji 15 ustęp 3 + obsługuje NuGet [Wersjonowania semantycznego 2.0.0](http://semver.org/spec/v2.0.0.html).

Niektóre semantyki v2.0.0 programu SemVer nie są obsługiwane w starszych klientów. NuGet uwzględnia wersja pakietu za v2.0.0 programu SemVer określone, jeśli jest spełniony jeden z następujących instrukcji:

- Etykieta wersji wstępnej jest oddzielona kropkami, na przykład *1.0.0-alpha.1*
- Wersja ma metadane kompilacji, na przykład *1.0.0+githash*

Dla nuget.org pakiet jest zdefiniowany jako pakiet v2.0.0 programu SemVer, jeśli spełniony jest jeden z następujących instrukcji:

- Wersja tego pakietu jest v2.0.0 programu SemVer zgodne, ale nie programu SemVer v1.0.0 zgodne, zgodnie z definicją powyżej.
- Wszelkie zakresy wersji zależności pakietu ma minimalną lub maksymalną wersję, która jest v2.0.0 programu SemVer zgodne, ale nie programu SemVer v1.0.0 zgodne, zdefiniowanych powyżej; na przykład *[1.0.0-alpha.1,)*.

Po wysłaniu pakietu v2.0.0 specyficzne dla programu SemVer do nuget.org pakiet jest niewidoczna dla starszych klientów i jest dostępny tylko dla następujących klientów NuGet:

- NuGet 4.3.0+
- Visual Studio 2017 wersji 15 ustęp 3 +
- Visual Studio 2015 z [v3.6.0 NuGet VSIX](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- DotNet.exe (2.0.0+ zestawu .NET SDK)

Klienci innych firm:

- Kierowcy JetBrains
- Paket w wersji 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Zakresy wersji i symboli wieloznacznych

W odniesieniu do zależności pakietów NuGet obsługuje przy użyciu notacji interwał służący do określania zakresu, podsumować w następujący sposób:

| Notacja | Reguła zastosowana | Opis |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | Minimalna wersja włącznie |
| (1.0,) | x > 1.0 | Minimalna wersja wyłączności |
| [1.0] | x == 1.0 | Wersja dokładnego dopasowania |
| (,1.0] | x ≤ 1.0 | Maksymalna wersja włącznie |
| (,1.0) | x < 1.0 | Maksymalna wersja wyłączności |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Dokładny zakres włącznie |
| (1.0,2.0) | 1.0 < x < 2.0 | Dokładny zakres wyłączności |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Mieszane z wartościami granicznymi minimalna i wyłącznego maksymalna wersja |
| (1.0)    | nieprawidłowe | nieprawidłowe |

Gdy w formacie PackageReference NuGet obsługuje również za pomocą notacji symboli wieloznacznych, \*, główna, pomocnicze, poprawki i sufiks wersji wstępnej części numeru. Symbole wieloznaczne nie są obsługiwane przez `packages.config` format.

> [!Note]
> Wersje wstępne nie są uwzględniane podczas rozpoznawania zakresu. Wersji wstępnych *są* uwzględnione przy użyciu symbolu wieloznacznego (\*). Zakres wersji *[1.0,2.0]*, na przykład nie zawiera wersji 2.0 beta, ale notacji symbolu wieloznacznego _2.0-*_ jest. Zobacz [wystawiać 912](https://github.com/NuGet/Home/issues/912) dla dalszego omówione symboli wieloznacznych wersji wstępnej.

### <a name="examples"></a>Przykłady

Zawsze podać wersja lub zakres wersji dla zależności pakietów w plikach projektu `packages.config` pliki, i `.nuspec` plików. Bez wersja lub zakres wersji, NuGet 2.8.x i wcześniej wybiera opcję najnowszą wersję pakietu dostępne podczas rozpoznawania zależności, podczas gdy NuGet 3.x, a później zdecyduje Najniższa wersja pakietu. Określanie wersji lub wersji tego niedokładność pozwala uniknąć zakresu.

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

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

**Odwołania w `packages.config`:**

W `packages.config`, co zależności znajduje się dokładnie `version` atrybut, który jest używany podczas przywracania pakietów. `allowedVersions` Atrybut jest używany tylko podczas operacji update Aby ograniczyć wersje, które mogły zostać zaktualizowane pakietu.

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

**Odwołania w `.nuspec` plików**

`version` Atrybutu w `<dependency>` element zawiera opis wersji zakresu, które są dozwolone dla zależności.

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

## <a name="normalized-version-numbers"></a>Numery wersji znormalizowane

> [!Note]
> Jest to istotne zmiany dla NuGet 3.4 i nowszych.

Uzyskiwanie pakietów z repozytorium podczas instalacji, ponowne zainstalowanie lub operacji, przywracania NuGet 3.4 + traktuje numery wersji w następujący sposób:

- Zera wiodące są usuwane z numerów wersji:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Zero w czwartym część numeru wersji zostaną pominięte.

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

Ta wartość nie wpływa na numery wersji pakietów. ma wpływ na sposób NuGet jest zgodny tylko wersje podczas rozpoznawania zależności.

Jednak repozytoriów pakietu NuGet należy traktować te wartości w taki sam sposób jak NuGet, aby uniknąć duplikowania wersji pakietu. W związku z tym repozytorium, która zawiera wersję *1.0* pakietu nie powinny również hostować wersji *1.0.0* jako osobne i inny pakiet.
