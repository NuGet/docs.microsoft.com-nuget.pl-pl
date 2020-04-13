---
title: Wersje wstępne w pakietach NuGet
description: Wskazówki dotyczące tworzenia pakietów przedpremierowych
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 1c19f962dc9e42154c0f4374432548e867e9538a
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610714"
---
# <a name="building-pre-release-packages"></a>Tworzenie pakietów przedpremierowych

Za każdym razem, gdy zwalniasz zaktualizowany pakiet z nowym numerem wersji, NuGet uważa, że jeden jako "najnowsze stabilne wydanie", jak pokazano, na przykład w interfejsie użytkownika Menedżera pakietów w programie Visual Studio:

![Interfejs użytkownika Menedżera pakietów przedstawiający najnowszą stabilną wersję](media/Prerelease_01-LatestStable.png)

Stabilne wydanie jest jednym, który jest uważany za wystarczająco wiarygodne, aby być używane w produkcji. Najnowsza stabilna wersja jest również tą, która zostanie zainstalowana jako aktualizacja pakietu lub podczas przywracania pakietu (z zastrzeżeniem ograniczeń opisanych w [temacie Ponowna instalacja i aktualizacja pakietów).](../consume-packages/reinstalling-and-updating-packages.md)

Aby obsługiwać cykl życia wydania oprogramowania, NuGet 1.6 i nowsze umożliwia dystrybucję pakietów wersji wstępnej, gdzie `-alpha` `-beta`numer `-rc`wersji zawiera semantyczny sufiks przechowywania wersji, taki jak , lub . Aby uzyskać więcej informacji, zobacz [Przechowywanie wersji pakietu](../concepts/package-versioning.md#pre-release-versions).

Takie wersje można określić za pomocą jednego z następujących sposobów:

- **Jeśli projekt używa [`PackageReference`](../consume-packages/package-references-in-project-files.md) **: dołącz sufiks wersji semantycznej [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) w elemencie `.csproj` pliku:

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- **Jeśli projekt ma [`packages.config`](../reference/packages-config.md) plik:** dołącz sufiks wersji semantycznej [`version`](../reference/nuspec.md#version) w elemencie [`.nuspec`](../reference/nuspec.md) pliku:

    ```xml
    <version>1.0.1-alpha</version>
    ```

Gdy będziesz gotowy do wydania stabilnej wersji, po prostu usuń sufiks, a pakiet ma pierwszeństwo przed dowolnymi wersjami wersji wstępnej. Ponownie, zobacz [Przechowywanie wersji pakietu](../concepts/package-versioning.md#pre-release-versions).

## <a name="installing-and-updating-pre-release-packages"></a>Instalowanie i aktualizowanie pakietów wersji wstępnej

Domyślnie NuGet nie zawiera wersji wstępnych podczas pracy z pakietami, ale można zmienić to zachowanie w następujący sposób:

- **Interfejs użytkownika Menedżera pakietów w programie Visual Studio:** W interfejsie użytkownika **zarządzania pakietami NuGet** zaznacz pole wyboru **Dołącz zawartość wstępną:**

    ![Pole wyboru Uwzględnij wydanie wstępne w programie Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    Ustawienie lub wyczyszczenie tego pola spowoduje odświeżenie interfejsu użytkownika Menedżera pakietów i listy dostępnych wersji, które można zainstalować.

- **Konsola Menedżera pakietów:** Użyj przełącznika `-IncludePrerelease` z poleceniami `Find-Package`, `Get-Package` `Install-Package`, `Sync-Package`, i. `Update-Package` Zapoznaj się z [odwołaniem programu PowerShell](../reference/powershell-reference.md).

- **NuGet CLI**: `-prerelease` Użyj `install`przełącznika `delete`z `mirror` , `update`, , i polecenia. Zapoznaj się z [odwołaniem nuget cli](../reference/nuget-exe-cli-reference.md)

## <a name="semantic-versioning"></a>Przechowywanie wersji semantycznych

[Semantyczne przechowywanie wersji lub SemVer konwencji](https://semver.org/spec/v1.0.0.html) opisuje, jak korzystać z ciągów w numerach wersji do przekazywania znaczenia kodu źródłowego.

W tej konwencji każda wersja `Major.Minor.Patch`ma trzy części, o następującym znaczeniu:

- `Major`: Przełomowe zmiany
- `Minor`: Nowe funkcje, ale wstecznie kompatybilne
- `Patch`: Korekty błędów zgodne ze standardem wstecz

Wersje w wersji wstępnej są następnie oznaczane przez dołączenie łącznika i ciągu po numerze poprawki. Technicznie rzecz biorąc, można użyć *dowolnego* ciągu po łącznika i NuGet będzie traktować pakiet jako wersji wstępnej. Następnie NuGet wyświetla pełny numer wersji w odpowiednim interfejsie użytkownika, pozostawiając konsumentów do interpretacji znaczenia dla siebie.

Mając to na uwadze, ogólnie dobrze jest przestrzegać uznanych konwencji nazewnictwa, takich jak:

- `-alpha`: Alpha release, zwykle używany do pracy w toku i eksperymentowania
- `-beta`: Wersja beta, zazwyczaj taka, która jest kompletna dla następnej planowanej wersji, ale może zawierać znane błędy.
- `-rc`: Release candidate, zazwyczaj wydanie, które jest potencjalnie ostateczne (stabilne), chyba że pojawią się istotne błędy.

> [!Note]
> NuGet 4.3.0+ obsługuje [semantyczne przechowywanie wersji v2.0.0](https://semver.org/spec/v2.0.0.html), które obsługuje numery wersji `1.0.1-build.23`wstępnej z notacją kropkową, jak w . Notacja kropki nie jest obsługiwana w wersjach NuGet przed wersją 4.3.0. We wcześniejszych wersjach NuGet można użyć `1.0.1-build23` formularza, jak ale to zawsze było uważane za wersję wstępną.

Niezależnie od używanych przyrostków, jednak NuGet da im pierwszeństwo w odwrotnej kolejności alfabetycznej:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta.12
    1.0.1-beta.5
    1.0.1-beta
    1.0.1-alpha.2
    1.0.1-alpha

Jak pokazano, wersja bez sufiksu zawsze będzie mieć pierwszeństwo przed wersjami wersji wstępnej.

Wiodące 0s nie są potrzebne z semver2, ale są one ze starym schematem wersji. Jeśli używasz sufiksów numerycznych z tagami wersji wstępnej, które mogą używać liczb dwucyfrowych (lub więcej), użyj zer wiodących, jak w wersjach beta.01 i beta.05, aby upewnić się, że są one sortowane poprawnie, gdy liczby stają się większe. To zalecenie dotyczy tylko starego schematu wersji.
