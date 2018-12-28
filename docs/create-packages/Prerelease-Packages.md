---
title: Wersje wstępne w pakietach NuGet
description: Wskazówki dotyczące tworzenia pakiety w wersji wstępnej
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: d6925df63daf3096455a8205d6aeb07b4475f715
ms.sourcegitcommit: 5c5f0f0e1f79098e27d9566dd98371f6ee16f8b5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645636"
---
# <a name="building-pre-release-packages"></a>Tworzenie pakietów w wersji wstępnej

Zawsze, gdy zwolnieniu zaktualizowany pakiet za pomocą nowego numeru wersji NuGet uzna, że jeden jako "najnowsza stabilna wersja" jak pokazano na przykład w interfejsie użytkownika Menedżera pakietów w programie Visual Studio:

![Najnowsza stabilna wersja przedstawiający interfejs użytkownika Menedżera pakietów](media/Prerelease_01-LatestStable.png)

Stabilnej wersji jest taki, który jest uznawany za niezawodny, ma być używany w środowisku produkcyjnym. Najnowsza stabilna wersja jest również zainstalowanej aktualizacji pakietu lub podczas przywracania pakietów (podlegających ograniczeniom opisanym w [ponowne zainstalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md)).

Do obsługi cyklu życia wersji oprogramowania, NuGet w wersji 1.6 i nowszych umożliwia dystrybucja pakiety w wersji wstępnej, numer wersji uwzględniającym sufiks wersji semantycznej takich jak `-alpha`, `-beta`, lub `-rc`. Aby uzyskać więcej informacji, zobacz [przechowywanie wersji pakietów](../reference/package-versioning.md#pre-release-versions).

Należy określić taki wersji na dwa sposoby:

- `.nuspec` Plik: zawierać sufiks wersji semantycznej `version` elementu:

    ```xml
    <version>1.0.1-alpha</version>
    ```

- Zestawu atrybutów: podczas tworzenia pakietu z projektu programu Visual Studio (`.csproj` lub `.vbproj`), użyj `AssemblyInformationalVersionAttribute` do określenia wersji:

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    NuGet przejmuje tę wartość, a nie określona w `AssemblyVersion` atrybut, który nie obsługuje wersji semantycznej.

Gdy wszystko będzie gotowe do wydania stabilną wersję, po prostu usuń sufiks, a pakiet mają pierwszeństwo przed wszystkie wersje wstępne. Znajduje się w artykule [przechowywanie wersji pakietów](../reference/package-versioning.md#pre-release-versions).

## <a name="installing-and-updating-pre-release-packages"></a>Instalowanie i aktualizowanie pakietów w wersji wstępnej

Domyślnie podczas pracy z pakietami NuGet obejmuje wersje wstępne, ale można zmienić to zachowanie w następujący sposób:

- **Interfejs użytkownika Menedżera pakietów w programie Visual Studio**: W **Zarządzaj pakietami NuGet** interfejsu użytkownika, sprawdź **Uwzględnij wersję wstępną** pola:

    ![Wstępna pola wyboru Dołącz w programie Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    Ustawienie lub usunięcie zaznaczenia tego pola spowoduje odświeżenie interfejs użytkownika Menedżera pakietów i listę dostępnych wersji, które można zainstalować.

- **Konsola Menedżera pakietów**: Użyj `-IncludePrerelease` przełącznik z `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, i `Update-Package` poleceń. Zapoznaj się [dokumentacja programu PowerShell](../tools/powershell-reference.md).

- **Interfejs wiersza polecenia NuGet**: Użyj `-prerelease` przełącznik z `install`, `update`, `delete`, i `mirror` poleceń. Zapoznaj się [dokumentacja interfejsu wiersza polecenia NuGet](../tools/nuget-exe-cli-reference.md)

## <a name="semantic-versioning"></a>Przechowywanie wersji semantyczne

[Konwencji Semantic Versioning lub SemVer](http://semver.org/spec/v1.0.0.html) w tym artykule opisano sposób wykorzystywania ciągi numerów wersji w celu przekazania ich znaczenie odpowiedni kod.

W niniejszej Konwencji, każda wersja ma trzy części `Major.Minor.Patch`, mają następujące znaczenie:

- `Major`: Zmiany powodujące niezgodność
- `Minor`: Nowe funkcje, ale wstecznie zgodne
- `Patch`: Wstecznie zgodny poprawek błędów oprogramowania tylko

Wersje wstępne następnie są wskazywane przez dołączenie łącznika i ciąg po numer poprawki. Technicznie rzecz biorąc, można użyć *wszelkie* ciągu po NuGet i łącznika, będą traktować pakietu jako wersji wstępnej. NuGet następnie wyświetla pełny numer wersji w interfejsie użytkownika dotyczy pozostawienie w konsumentach napisanych interpretacji znaczenie dla siebie.

Pamiętając o tym, zazwyczaj dobrze jest postępuj zgodnie z rozpoznanym konwencji nazewnictwa, takie jak następujące:

- `-alpha`: Wersja alfa, zwykle używane do pracy w toku i eksperymentowanie
- `-beta`: Wydania beta, zazwyczaj taki, który jest funkcja ukończone przez następne zaplanowane wersji, ale może zawierać znanych błędów.
- `-rc`: W wersji Release candidate, zwykle wydania jest potencjalnie ostateczne (stable), chyba że wyłaniać znaczące błędy.

> [!Note]
> Obsługuje NuGet 4.3.0+ [v2.0.0 Semantic Versioning](http://semver.org/spec/v2.0.0.html), który obsługuje numerów wersji wstępnej przy użyciu notacji z kropką, podobnie jak w `1.0.1-build.23`. Kropkowego jest nieobsługiwane w przypadku wersje NuGet wcześniejsze niż 4.3.0. We wcześniejszych wersjach programu NuGet, można użyć formularza, takich jak `1.0.1-build23` , ale zawsze uznano wersji wstępnej.

Niezależnie od sufiksów, jednak należy użyć, NuGet da im pierwszeństwo w odwrotnej kolejności alfabetycznej:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

Jak widać, wersji bez dowolny sufiks ma zawsze pierwszeństwo wersje wstępne. Należy zauważyć, jeśli używasz sufiksy wartości liczbowych przy użyciu tagów wersji wstępnej, które mogą używać jednocyfrowy liczb (lub więcej), użyj zer wiodących beta01 i beta05 aby upewnić się, że są poprawne sortowanie podczas uzyskać większej liczby.
