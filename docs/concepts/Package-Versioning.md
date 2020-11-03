---
title: Dokumentacja wersji pakietu NuGet
description: Dokładne szczegóły dotyczące określania numerów wersji i zakresów dla innych pakietów, od których zależy pakiet NuGet, oraz sposobu instalowania zależności.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 4cb12f439d796d583f52d657225c39418d5a4836
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237364"
---
# <a name="package-versioning"></a>Przechowywanie wersji pakietów

Określony pakiet zawsze jest określany przy użyciu identyfikatora pakietu i dokładnego numeru wersji. Na przykład [Entity Framework](https://www.nuget.org/packages/EntityFramework/) w NuGet.org ma kilka dziesiątych dostępnych pakietów, od wersji *4.1.10311* do wersji *6.1.3* (najnowszej stabilnej wersji) i różne wersje wstępne, takie jak *6.2.0-beta1* .

Podczas tworzenia pakietu przypisujesz określony numer wersji z opcjonalnym sufiksem tekstu w wersji wstępnej. W przypadku używania pakietów, z drugiej strony, można określić dokładny numer wersji lub zakres akceptowalnych wersji.

W tym temacie:

- [Podstawy wersji](#version-basics) , w tym sufiksy wstępne.
- [Zakresy wersji](#version-ranges)
- [Znormalizowane numery wersji](#normalized-version-numbers)

## <a name="version-basics"></a>Podstawy wersji

Określony numer wersji ma postać *główna. pomocnicza. poprawka [-sufiks]* , gdzie składniki mają następujące znaczenie:

- *Główna: istotne* zmiany
- *Pomocniczy* : nowe funkcje, ale zgodność z poprzednimi wersjami
- *Poprawka* : tylko poprawki zgodności z poprzednimi wersjami
- *-Sufiks* (opcjonalnie): Łącznik, po którym następuje ciąg oznaczający wersję wstępną (zgodnie z [Konwencją o wersji semantyki lub SemVer 1,0](https://semver.org/spec/v1.0.0.html)).

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

- `-alpha`: Wersja alfa, zazwyczaj używana do pracy w toku i eksperymentowania.
- `-beta`: Wydanie beta, zazwyczaj takie, które jest kompletne dla następnej planowanej wersji, ale może zawierać znane usterki.
- `-rc`: Release Candidate, zwykle wydanie, które jest potencjalnie ostateczne (stabilne), chyba że nastąpiły znaczne błędy.

> [!Note]
> Pakiet NuGet 4.3.0 + obsługuje [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), który obsługuje numery wersji wstępnej z notacją kropkową, tak jak w przypadku *1.0.1-Build. 23* . Notacja kropki nie jest obsługiwana w wersjach NuGet przed 4.3.0. Możesz użyć formularza, takiego jak *1.0.1-build23* .

Przy rozwiązywaniu odwołań do pakietów i wielu wersjach pakietów różni się tylko sufiksem, pakiet NuGet wybiera wersję bez sufiksu, a następnie stosuje pierwszeństwo w wersji wstępnej w odwrotnej kolejności alfabetycznej. Na przykład następujące wersje zostałyby wybrane w dokładnie pokazanej kolejności:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Semantyczne przechowywanie wersji 2.0.0

Dzięki narzędziom NuGet 4.3.0 + i Visual Studio 2017 w wersji 15.3 + pakiet NuGet obsługuje [semantykę wersji 2.0.0](https://semver.org/spec/v2.0.0.html).

Niektóre semantyka SemVer v 2.0.0 nie są obsługiwane przez starszych klientów. Pakiet NuGet traktuje wersję pakietu jako SemVer v 2.0.0, jeśli jedno z następujących instrukcji jest prawdziwe:

- Etykieta wersji wstępnej jest oddzielona kropką, na przykład *1.0.0-alpha. 1*
- Wersja zawiera metadane kompilacji, na przykład *1.0.0 + githash*

W przypadku nuget.org pakiet jest zdefiniowany jako pakiet SemVer v 2.0.0, jeśli jest spełniony jeden z następujących instrukcji:

- Własna wersja pakietu to SemVer v 2.0.0 zgodna, ale nie SemVer v 1.0.0 zgodna, zgodnie z definicją powyżej.
- Dowolna z zakresów wersji zależności pakietu ma wersję minimalną lub maksymalną, która jest zgodna z SemVer v 2.0.0, ale nie SemVer v 1.0.0 zgodna z definicją powyżej; na przykład *[1.0.0-alpha. 1,)* .

W przypadku przekazania pakietu SemVer v 2.0.0 do nuget.org pakiet jest niewidoczny dla starszych klientów i dostępny tylko dla następujących klientów NuGet:

- 4.3.0 NuGet +
- Visual Studio 2017 w wersji 15.3 +
- Visual Studio 2015 z pakietem [NuGet VSIX v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore.exe (ZESTAW SDK .NET 2.0.0 +)

Klienci innych firm:

- JetBrains
- Paket w wersji 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a>Zakresy wersji

W przypadku odwoływania się do zależności pakietów NuGet obsługuje używanie notacji interwału do określania zakresów wersji, podsumowywane w następujący sposób:

| Notacja | Zastosowana reguła | Opis |
|----------|--------------|-------------|
| 1.0 | x ≥ 1,0 | Wersja minimalna, włącznie |
| (1.0,) | x > 1.0 | Wersja minimalna, wyłącznie |
| [1.0] | x == 1.0 | Dokładne dopasowanie wersji |
| (,1.0] | x ≤ 1.0 | Wersja maksymalna, włącznie |
| (,1.0) | x < 1.0 | Wersja maksymalna, wyłącznie |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Dokładny zakres, włącznie |
| (1.0,2.0) | 1.0 < x < 2.0 | Dokładny zakres, wyłącznie |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Mieszany — wartość minimalna włącznie i wartość maksymalna wyłącznie |
| (1.0)    | nieprawidłowe | nieprawidłowe |

W przypadku korzystania z formatu PackageReference, pakiet NuGet obsługuje również używanie notacji zmiennoprzecinkowej, \* dla elementów głównych, pomocniczych, poprawek i prefiksu w wersji wstępnej. Wersje zmiennoprzecinkowe nie są obsługiwane w `packages.config` formacie. W przypadku określenia wersji zmiennoprzecinkowej reguła jest rozpoznawana jako najwyższa istniejąca wersja zgodna z opisem wersji. Przykłady wersji zmiennoprzecinkowych i rozdzielczości są poniżej.

> [!Note]
> Zakresy wersji w programie PackageReference obejmują wersje wstępne. Zgodnie z projektem wersje zmiennoprzecinkowe nie rozwiązują wersji wstępnych, chyba że zostały uwzględnione w. Aby uzyskać stan żądania powiązanej funkcji, zobacz [problem 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).

### <a name="examples"></a>Przykłady

Należy zawsze określać wersję lub zakres wersji dla zależności pakietów w plikach projektu, `packages.config` plikach i `.nuspec` plikach. Bez wersji lub zakresu wersji, program NuGet 2.8. x i wcześniejsza wersja wybiera najnowszą dostępną wersję pakietu podczas rozpoznawania zależności, natomiast w przypadku programu NuGet 3. x lub nowszego jest wybierana najniższa wersja pakietu. Określenie wersji lub zakresu wersji pozwala uniknąć tej niepewności.

#### <a name="references-in-project-files-packagereference"></a>Odwołania w plikach projektu (PackageReference)

```xml
<!-- Accepts any version 6.1 and above.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version.
     Will resolve to the highest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.*" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. 
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. 
     Will resolve to the smallest acceptable stable version.
     -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher.
     Will resolve to the smallest acceptable stable version. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

#### <a name="floating-version-resolutions"></a>Rozdzielczości zmiennoprzecinkowe 

| Wersja | Wersje obecne na serwerze | Rozwiązanie | Przyczyna | Uwagi |
|----------|--------------|-------------|-------------|-------------|
| * | 1.1.0 <br> 1.1.1 <br> 1.2.0 <br> 1.3.0 — alfa  | 1.2.0 | Największa stabilna wersja. |
| 1,1. * | 1.1.0 <br> 1.1.1 <br> 1.1.2 — Alpha <br> 1.2.0 — alfa | 1.1.1 | Największa stabilna wersja, która szanuje określony wzorzec.|
| * - * | 1.1.0 <br> 1.1.1 <br> 1.1.2 — Alpha <br> 1.3.0 — wersja beta  | 1.3.0 — wersja beta | Najwyższa wersja, w tym niestabilne wersje. | Dostępne w programie Visual Studio w wersji 16,6, NuGet w wersji 5,6, zestaw .NET Core SDK wersja 3.1.300 |
| 1,1. *-* | 1.1.0 <br> 1.1.1 <br> 1.1.2 — Alpha <br> 1.1.2 — beta <br> 1.3.0 — wersja beta  | 1.1.2 — beta | Największa wersja z uwzględnieniem wzorca i wraz z niestabilnymi wersjami. | Dostępne w programie Visual Studio w wersji 16,6, NuGet w wersji 5,6, zestaw .NET Core SDK wersja 3.1.300 |

**Odwołania w `packages.config` :**

W programie `packages.config` każda zależność jest wyświetlana z dokładnym `version` atrybutem używanym podczas przywracania pakietów. Ten `allowedVersions` atrybut jest używany tylko podczas operacji aktualizowania, aby ograniczyć wersje, do których pakiet może zostać zaktualizowany.

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

`version`Atrybut w `<dependency>` elemencie opisuje wersje zakresu, które są akceptowalne dla zależności.

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
        
- Metadane kompilacji SemVer 2.0.0 są usuwane

        1.0.7+r3456 is treated as 1.0.7

`pack` i `restore` operacje normalizuje wersje wszędzie tam, gdzie to możliwe. W przypadku pakietów, które zostały już skompilowane, normalizacja nie ma wpływu na numery wersji w samych pakietach; ma wpływ tylko na to, jak program NuGet dopasowuje wersje podczas rozpoznawania zależności.

Jednak repozytoria pakietów NuGet musi traktować te wartości w taki sam sposób jak NuGet, aby zapobiec duplikowaniu wersji pakietu. W ten sposób repozytorium zawierające wersję *1,0* pakietu nie powinno również hostować wersji *1.0.0* jako oddzielnego i innego pakietu.
