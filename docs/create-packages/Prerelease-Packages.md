---
title: Wersje wstępne w pakietach NuGet
description: Wskazówki dotyczące tworzenia pakietów w wersji wstępnej
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 1c19f962dc9e42154c0f4374432548e867e9538a
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610714"
---
# <a name="building-pre-release-packages"></a>Tworzenie pakietów w wersji wstępnej

Za każdym razem, gdy zostanie wydane zaktualizowanego pakietu przy użyciu nowego numeru wersji, program NuGet uważa, że jest on wyświetlany jako "Najnowsza stabilna wersja", na przykład w interfejsie użytkownika Menedżera pakietów w programie Visual Studio:

![Interfejs użytkownika Menedżera pakietów przedstawiający najnowszą stabilną wersję](media/Prerelease_01-LatestStable.png)

Stabilna wersja jest uważana za wystarczającą do użycia w środowisku produkcyjnym. Najnowsza stabilna wersja jest również taka, która zostanie zainstalowana jako aktualizacja pakietu lub podczas przywracania pakietu (z uwzględnieniem ograniczeń opisanych w temacie [ponowne instalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md)).

Aby można było obsługiwać cykl wydawania oprogramowania, program NuGet 1,6 i nowsze umożliwiają dystrybucję pakietów w wersji wstępnej, gdzie numer wersji zawiera sufiks wersji semantycznej, taki jak `-alpha`, `-beta`lub `-rc`. Aby uzyskać więcej informacji, zobacz [przechowywanie wersji pakietu](../concepts/package-versioning.md#pre-release-versions).

Możesz określić takie wersje przy użyciu jednego z następujących sposobów:

- **Jeśli projekt używa [`PackageReference`](../consume-packages/package-references-in-project-files.md)** : Uwzględnij sufiks wersji semantycznej w [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) pliku `.csproj`:

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- **Jeśli projekt zawiera plik [`packages.config`](../reference/packages-config.md)** : Uwzględnij sufiks wersji semantycznej w [`version`](../reference/nuspec.md#version) pliku [`.nuspec`](../reference/nuspec.md) :

    ```xml
    <version>1.0.1-alpha</version>
    ```

Gdy wszystko będzie gotowe do zwolnienia stabilnej wersji, wystarczy usunąć sufiks, a pakiet ma pierwszeństwo przed wszystkimi wersjami wstępnymi. Ponownie zapoznaj się z artykułem [wersja pakietu](../concepts/package-versioning.md#pre-release-versions).

## <a name="installing-and-updating-pre-release-packages"></a>Instalowanie i aktualizowanie pakietów wersji wstępnej

Domyślnie NuGet nie uwzględnia wersji wstępnych podczas pracy z pakietami, ale można zmienić to zachowanie w następujący sposób:

- **Interfejs użytkownika Menedżera pakietów w programie Visual Studio**: w interfejsie użytkownika **Zarządzanie pakietami NuGet** zaznacz pole **Uwzględnij wersję wstępną** :

    ![Pole wyboru Uwzględnij wersję wstępną w programie Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    Ustawienie lub wyczyszczenie tego pola spowoduje odświeżenie interfejsu użytkownika Menedżera pakietów oraz listę dostępnych wersji, które można zainstalować.

- **Konsola Menedżera pakietów**: użyj przełącznika `-IncludePrerelease` z poleceniami `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`i `Update-Package`. Zapoznaj się z dokumentacją [programu PowerShell](../reference/powershell-reference.md).

- **Interfejs wiersza polecenia NuGet**: użyj przełącznika `-prerelease` za pomocą poleceń `install`, `update`, `delete`i `mirror`. Zapoznaj się z dokumentacją [interfejsu wiersza polecenia NuGet](../reference/nuget-exe-cli-reference.md)

## <a name="semantic-versioning"></a>Wersja semantyczna

W przypadku [semantyki wersji lub Konwencji SemVer](https://semver.org/spec/v1.0.0.html) opisano, jak używać ciągów w numerach wersji do przekazywania znaczenia kodu bazowego.

W tej Konwencji każda wersja ma trzy części, `Major.Minor.Patch`i ma następujące znaczenie:

- `Major`: przerywanie zmian
- `Minor`: nowe funkcje, ale zgodność z poprzednimi wersjami
- `Patch`: tylko zgodność z poprzednimi poprawkami błędów

Wersje wstępne są następnie oznaczane przez dołączenie łącznika i ciągu po numerze poprawki. Mówiąc technicznie, można użyć *dowolnego* ciągu po łączniku i NuGet będzie traktować pakiet jako wersję wstępną. Następnie pakiet NuGet wyświetla pełny numer wersji w odpowiednim interfejsie użytkownika, pozostawiając konsumentom interpretację znaczenia dla siebie.

Z tego względu zazwyczaj warto przestrzegać rozpoznanych konwencji nazewnictwa, takich jak następujące:

- `-alpha`: wydanie Alpha, zwykle używane do pracy w toku i eksperymentowanie
- `-beta`: wydanie beta, zazwyczaj takie, które jest kompletne dla następnej planowanej wersji, ale mogą zawierać znane usterki.
- `-rc`: Release Candidate, zazwyczaj wersja, która jest potencjalnie końcowa (stabilna), chyba że nastąpiły znaczne błędy.

> [!Note]
> Pakiet NuGet 4.3.0 + obsługuje [semantykę wersji 2.0.0](https://semver.org/spec/v2.0.0.html), która obsługuje numery wersji wstępnej z notacją kropkową, jak w `1.0.1-build.23`. Notacja kropki nie jest obsługiwana w wersjach NuGet przed 4.3.0. We wcześniejszych wersjach programu NuGet można użyć formularza, takiego jak `1.0.1-build23`, ale jest on zawsze traktowany jako wersja wstępna.

Jednak wszelkie używane sufiksy NuGet będą mieć pierwszeństwo w odwrotnej kolejności alfabetycznej:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta.12
    1.0.1-beta.5
    1.0.1-beta
    1.0.1-alpha.2
    1.0.1-alpha

Jak pokazano, wersja bez żadnego sufiksu zawsze będzie mieć pierwszeństwo przed wersjami wstępnymi.

Wiodące 0s nie są potrzebne w przypadku semver2, ale są z starym schematem wersji. Jeśli używasz sufiksów liczbowych ze znacznikami wersji wstępnej, które mogą używać cyfr dwucyfrowych (lub więcej), użyj wiodących zer jako wersji beta. 01 i beta. 05, aby upewnić się, że są one sortowane prawidłowo, gdy liczby są większe. To zalecenie dotyczy tylko starszego schematu wersji.
