---
title: Tworzenie i publikowanie pakietu .NET Framework NuGet przy użyciu programu Visual Studio w systemie Windows
description: Samouczek instruktażowy dotyczący tworzenia i publikowania pakietu .NET Framework NuGet przy użyciu programu Visual Studio w systemie Windows.
author: karann-msft
ms.author: karann
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: 75160bf2b01f6d4707162e019a6263ddc64a6f5e
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342518"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a>Szybki start: Tworzenie i publikowanie pakietu przy użyciu programu Visual Studio (.NET Framework, Windows)

Tworzenie pakietu NuGet z biblioteki klas .NET Framework obejmuje tworzenie biblioteki DLL w programie Visual Studio w systemie Windows, a następnie użycie narzędzia wiersza polecenia NuGet. exe do utworzenia i opublikowania pakietu.

> [!Note]
> Ten przewodnik Szybki Start dotyczy tylko programu Visual Studio 2017 dla systemu Windows. Visual Studio dla komputerów Mac nie obejmuje funkcji opisanych w tym miejscu. Zamiast tego użyj [narzędzi interfejsu wiersza polecenia dotnet](create-and-publish-a-package-using-the-dotnet-cli.md) .

## <a name="prerequisites"></a>Wymagania wstępne

1. Zainstaluj dowolną wersję programu Visual Studio 2017 z [VisualStudio.com](https://www.visualstudio.com/) z dowolnym. Obciążenie związane z usługą SIECIową. Program Visual Studio 2017 automatycznie zawiera funkcje NuGet podczas instalacji obciążenia .NET.

1. Zainstaluj interfejs wiersza polecenia, pobierając go z [NuGet.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), zapisując `.exe` ten plik w odpowiednim folderze i dodając go do zmiennej środowiskowej PATH. `nuget.exe`

1. [Zarejestruj się, aby korzystać z bezpłatnego konta w usłudze NuGet.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) , jeśli jeszcze go nie masz. Utworzenie nowego konta spowoduje wysłanie wiadomości e-mail z potwierdzeniem. Musisz potwierdzić konto, aby można było przekazać pakiet.

## <a name="create-a-class-library-project"></a>Tworzenie projektu biblioteki klas

Można użyć istniejącego projektu biblioteki klas .NET Framework dla kodu, który ma zostać spakowany, lub utworzyć prosty jeden w następujący sposób:

1. W programie Visual Studio wybierz kolejno pozycje **plik > Nowy > projekt**, wybierz węzeł  **C# wizualizacji** , wybierz szablon "Biblioteka klas (.NET Framework)", nazwij projekt AppLogger i kliknij przycisk **OK**.

1. Kliknij prawym przyciskiem myszy plik projektu powstały i wybierz pozycję **kompilacja** , aby upewnić się, że projekt został utworzony prawidłowo. Biblioteka DLL znajduje się w folderze debugowania (lub zwolnij, jeśli zostanie utworzona ta konfiguracja).

Oczywiście w rzeczywistym pakiecie NuGet zaimplementowano wiele przydatnych funkcji, z którymi inne mogą tworzyć aplikacje. Możesz również ustawić Platformy docelowe. Na przykład zapoznaj się z przewodnikami dla [platformy UWP](../guides/create-uwp-packages.md) i [Xamarin](../guides/create-packages-for-xamarin.md).

W tym instruktażu nie można jednak napisać żadnego dodatkowego kodu, ponieważ biblioteka klas z szablonu jest wystarczająca do utworzenia pakietu. Nadal, jeśli chcesz, aby w pakiecie był jakiś kod funkcjonalny, użyj następujących czynności:

```cs
using System;

namespace AppLogger
{
    public class Logger
    {
        public void Log(string text)
        {
            Console.WriteLine(text);
        }
    }
}
```

> [!Tip]
> O ile nie istnieje powód, aby wybrać inny sposób, .NET Standard jest preferowanym celem dla pakietów NuGet, ponieważ zapewnia zgodność z najszerszym zakresem zużywanych projektów. Zobacz [Tworzenie i publikowanie pakietu przy użyciu programu Visual Studio (.NET standard)](create-and-publish-a-package-using-visual-studio.md).

## <a name="configure-project-properties-for-the-package"></a>Konfigurowanie właściwości projektu dla pakietu

Pakiet NuGet zawiera manifest ( `.nuspec` plik), który zawiera odpowiednie metadane, takie jak identyfikator pakietu, numer wersji, opis i inne. Niektóre z nich mogą być narysowane bezpośrednio we właściwościach projektu, co pozwala uniknąć konieczności osobnego aktualizowania ich zarówno w projekcie, jak i w manifeście. W tej sekcji opisano, gdzie ustawić odpowiednie właściwości.

1. Wybierz polecenie menu **> właściwości projektu** , a następnie wybierz kartę **aplikacja** .

1. W polu **Nazwa zestawu** nadaj pakietowi unikatowy identyfikator.

    > [!Important]
    > Należy nadać pakietowi identyfikator, który jest unikatowy w obrębie nuget.org lub dowolnego hosta, który jest używany. W tym instruktażu Zalecamy uwzględnienie "przykładowego" lub "testowego" w nazwie, jak w późniejszym kroku publikowania sprawia, że pakiet jest widoczny publicznie (chociaż prawdopodobnie nikt się nie używa).
    >
    > Jeśli spróbujesz opublikować pakiet o nazwie, która już istnieje, zostanie wyświetlony komunikat o błędzie.

1. Wybierz przycisk **Informacje o zestawie** , który umożliwia wyświetlenie okna dialogowego, w którym można wprowadzić inne właściwości, które są umieszczane w manifeście (zobacz [. nuspec plik — tokeny zastępcze](../reference/nuspec.md#replacement-tokens)). Najczęściej używane pola to **tytuł**, **Opis**, **firma**, **prawa autorskie**i **wersja zestawu**. Te właściwości ostatecznie pojawiają się wraz z pakietem na hoście, takim jak nuget.org, więc upewnij się, że są one w pełni opisowe.

    ![Informacje o zestawie w projekcie .NET Framework w programie Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. Opcjonalne: Aby wyświetlić i edytować właściwości bezpośrednio, Otwórz `Properties/AssemblyInfo.cs` plik w projekcie.

1. Po ustawieniu właściwości ustaw konfigurację projektu na Zwolnij i skompiluj  ponownie projekt w celu wygenerowania zaktualizowanej biblioteki DLL.

## <a name="generate-the-initial-manifest"></a>Generuj początkowy manifest

Z biblioteką DLL w oddziałach i ustawionych właściwościach projektu można `nuget spec` teraz użyć polecenia, aby `.nuspec` wygenerować początkowy plik z projektu. Ten krok obejmuje odpowiednie tokeny zastępcze do rysowania informacji z pliku projektu.

Uruchamia `nuget spec` się tylko raz, aby wygenerować początkowy manifest. Podczas aktualizowania pakietu należy zmienić wartości w projekcie lub bezpośrednio edytować manifest.

1. Otwórz wiersz polecenia i przejdź do folderu projektu zawierającego `AppLogger.csproj` plik.

1. Uruchom następujące polecenie: `nuget spec AppLogger.csproj`. Określając projekt, pakiet NuGet tworzy manifest, który jest zgodny z nazwą projektu, w tym przypadku `AppLogger.nuspec`. Zawiera również tokeny zastępcze w manifeście.

1. Otwórz `AppLogger.nuspec` w edytorze tekstów, aby przejrzeć jego zawartość, która powinna wyglądać następująco:

    ```xml
    <?xml version="1.0"?>
    <package >
      <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2018</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a>Edytuj manifest

1. Pakiet NuGet generuje błąd w przypadku próby utworzenia pakietu z wartościami domyślnymi w `.nuspec` pliku, dlatego przed kontynuowaniem należy edytować następujące pola. Zobacz [. nuspec — odwołanie do pliku — opcjonalne elementy metadanych](../reference/nuspec.md#optional-metadata-elements) opisujące sposób ich użycia.

    - licenseUrl
    - projectUrl
    - iconUrl
    - releaseNotes
    - tagi

1. W przypadku pakietów przeznaczonych do użycia publicznego należy zwrócić szczególną uwagę na właściwości **Tagi** , ponieważ Tagi ułatwiają innym znalezienie pakietu na źródłach, takich jak NuGet.org, i zrozumienie jego działania.

1. W tym momencie można również dodać wszystkie inne elementy do manifestu, zgodnie z opisem w [dokumentacji pliku. nuspec](../reference/nuspec.md).

1. Zapisz plik przed kontynuowaniem.

## <a name="run-the-pack-command"></a>Uruchom pakiet polecenie

1. W wierszu polecenia w folderze zawierającym `.nuspec` plik Uruchom polecenie. `nuget pack`

1. Pakiet NuGet generuje `.nupkg` plik w postaci *identyfikatora-Version. nupkg*, który znajduje się w bieżącym folderze.

## <a name="publish-the-package"></a>Publikowanie pakietu

Po utworzeniu `nuget.exe` pliku opublikuj go w celu NuGet.org przy użyciu klucza interfejsu API uzyskanego z NuGet.org. `.nupkg` W przypadku NuGet.org należy użyć `nuget.exe` 4.1.0 lub wyższej.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Pozyskiwanie klucza interfejsu API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>Publikowanie przy użyciu wypychania NuGet

1. Otwórz wiersz polecenia i przejdź do folderu zawierającego `.nupkg` plik.

1. Uruchom następujące polecenie, określając nazwę pakietu i zastępując wartość klucza kluczem interfejsu API:

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. NuGet. exe wyświetla wyniki procesu publikowania:

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

Zobacz [wypychanie NuGet](../reference/cli-reference/cli-ref-push.md).

### <a name="publish-errors"></a>Błędy publikowania

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Zarządzanie opublikowanym pakietem

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a>Następne kroki

Gratulujemy utworzenia pierwszego pakietu NuGet!

> [!div class="nextstepaction"]
> [Tworzenie pakietu](../create-packages/creating-a-package.md)

Aby poznać więcej informacji o tym, że pakiet NuGet jest oferowany, wybierz poniższe linki.

- [Publikowanie pakietu](../nuget-org/publish-a-package.md)
- [Pakiety wersji wstępnej](../create-packages/Prerelease-Packages.md)
- [Obsługa wielu platform docelowych](../create-packages/supporting-multiple-target-frameworks.md)
- [Przechowywanie wersji pakietów](../reference/package-versioning.md)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
