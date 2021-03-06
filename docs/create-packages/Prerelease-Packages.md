---
title: Wersje wstępne w pakietach NuGet
description: Wskazówki dotyczące tworzenia pakietów w wersji wstępnej
author: JonDouglas
ms.author: jodou
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: ae6628efa6d97ff5ba2c4c359b9565a3214cb346
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774658"
---
# <a name="building-pre-release-packages"></a>Tworzenie pakietów w wersji wstępnej

Za każdym razem, gdy zostanie wydane zaktualizowanego pakietu przy użyciu nowego numeru wersji, program NuGet uważa, że jest on wyświetlany jako "Najnowsza stabilna wersja", na przykład w interfejsie użytkownika Menedżera pakietów w programie Visual Studio:

![Interfejs użytkownika Menedżera pakietów przedstawiający najnowszą stabilną wersję](media/Prerelease_01-LatestStable.png)

Stabilna wersja jest uważana za wystarczającą do użycia w środowisku produkcyjnym. Najnowsza stabilna wersja jest również taka, która zostanie zainstalowana jako aktualizacja pakietu lub podczas przywracania pakietu (z uwzględnieniem ograniczeń opisanych w temacie [ponowne instalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md)).

Aby można było obsługiwać cykl wydawania oprogramowania, program NuGet 1,6 i nowsze umożliwiają dystrybucję pakietów w wersji wstępnej, gdzie numer wersji zawiera sufiks wersji semantycznej, taki jak `-alpha` , `-beta` lub `-rc` . Aby uzyskać więcej informacji, zobacz [przechowywanie wersji pakietu](../concepts/package-versioning.md#pre-release-versions).

Możesz określić takie wersje przy użyciu jednego z następujących sposobów:

- **Jeśli używany [`PackageReference`](../consume-packages/package-references-in-project-files.md) jest projekt**: Dołącz sufiks wersji semantycznej do `.csproj` elementu pliku [`PackageVersion`](/dotnet/core/tools/csproj#packageversion) :

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- **Jeśli projekt zawiera [`packages.config`](../reference/packages-config.md) plik**: Dołącz sufiks wersji semantycznej do [`.nuspec`](../reference/nuspec.md) [`version`](../reference/nuspec.md#version) elementu pliku:

    ```xml
    <version>1.0.1-alpha</version>
    ```

Gdy wszystko będzie gotowe do zwolnienia stabilnej wersji, wystarczy usunąć sufiks, a pakiet ma pierwszeństwo przed wszystkimi wersjami wstępnymi. Ponownie zapoznaj się z artykułem [wersja pakietu](../concepts/package-versioning.md#pre-release-versions).

## <a name="installing-and-updating-pre-release-packages"></a>Instalowanie i aktualizowanie pakietów wersji wstępnej

Domyślnie NuGet nie uwzględnia wersji wstępnych podczas pracy z pakietami, ale można zmienić to zachowanie w następujący sposób:

- **Interfejs użytkownika Menedżera pakietów w programie Visual Studio**: w interfejsie użytkownika **Zarządzanie pakietami NuGet** zaznacz pole **Uwzględnij wersję wstępną** :

    ![Pole wyboru Uwzględnij wersję wstępną w programie Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    Ustawienie lub wyczyszczenie tego pola spowoduje odświeżenie interfejsu użytkownika Menedżera pakietów oraz listę dostępnych wersji, które można zainstalować.

- **Konsola Menedżera pakietów**: Użyj `-IncludePrerelease` przełącznika z `Find-Package` poleceniami,,, `Get-Package` `Install-Package` `Sync-Package` i `Update-Package` . Zapoznaj się z dokumentacją [programu PowerShell](../reference/powershell-reference.md).

- **Interfejs wiersza polecenia NuGet**: Użyj `-prerelease` przełącznika z `install` `update` `delete` poleceniami,, i `mirror` . Zapoznaj się z dokumentacją [interfejsu wiersza polecenia NuGet](../reference/nuget-exe-cli-reference.md)

## <a name="semantic-versioning"></a>Semantyczna obsługa wersji

W przypadku [semantyki wersji lub Konwencji SemVer](https://semver.org/spec/v1.0.0.html) opisano, jak używać ciągów w numerach wersji do przekazywania znaczenia kodu bazowego.

W tej Konwencji każda wersja ma trzy części, `Major.Minor.Patch` i ma następujące znaczenie:

- `Major`: Istotne zmiany
- `Minor`: Nowe funkcje, ale zgodność z poprzednimi wersjami
- `Patch`: Tylko poprawki zgodne z poprzednimi usterkami

Wersje wstępne są następnie oznaczane przez dołączenie łącznika i ciągu po numerze poprawki. Mówiąc technicznie, można użyć *dowolnego* ciągu po łączniku i NuGet będzie traktować pakiet jako wersję wstępną. Następnie pakiet NuGet wyświetla pełny numer wersji w odpowiednim interfejsie użytkownika, pozostawiając konsumentom interpretację znaczenia dla siebie.

Z tego względu zazwyczaj warto przestrzegać rozpoznanych konwencji nazewnictwa, takich jak następujące:

- `-alpha`: Wydanie alfa, zwykle używane do pracy w toku i eksperymentowanie
- `-beta`: Wydanie beta, zazwyczaj takie, które jest kompletne dla następnej planowanej wersji, ale może zawierać znane usterki.
- `-rc`: Release Candidate, zwykle wydanie, które jest potencjalnie ostateczne (stabilne), chyba że nastąpiły znaczne błędy.

> [!Note]
> Pakiet NuGet 4.3.0 + obsługuje [semantykę wersji v 2.0.0](https://semver.org/spec/v2.0.0.html), która obsługuje numery wersji wstępnej z notacją kropkową, jak w `1.0.1-build.23` . Notacja kropki nie jest obsługiwana w wersjach NuGet przed 4.3.0. We wcześniejszych wersjach programu NuGet możesz użyć takiego formularza, `1.0.1-build23` ale jest on zawsze traktowany jako wersja wstępna.

Jednak wszelkie używane sufiksy NuGet będą mieć pierwszeństwo w odwrotnej kolejności alfabetycznej:

```
1.0.1
1.0.1-zzz
1.0.1-rc
1.0.1-open
1.0.1-beta.12
1.0.1-beta.5
1.0.1-beta
1.0.1-alpha.2
1.0.1-alpha
```

Jak pokazano, wersja bez żadnego sufiksu zawsze będzie mieć pierwszeństwo przed wersjami wstępnymi.

Wiodące 0s nie są potrzebne w przypadku semver2, ale są z starym schematem wersji. Jeśli używasz sufiksów liczbowych ze znacznikami wersji wstępnej, które mogą używać cyfr dwucyfrowych (lub więcej), użyj wiodących zer jako wersji beta. 01 i beta. 05, aby upewnić się, że są one sortowane prawidłowo, gdy liczby są większe. To zalecenie dotyczy tylko starszego schematu wersji.
