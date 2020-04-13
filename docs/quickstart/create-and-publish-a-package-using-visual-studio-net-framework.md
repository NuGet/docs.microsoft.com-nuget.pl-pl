---
title: Tworzenie i publikowanie pakietu NuGet programu .NET Framework przy użyciu programu Visual Studio w systemie Windows
description: Samouczek instruktażowy dotyczący tworzenia i publikowania pakietu NuGet programu .NET Framework przy użyciu programu Visual Studio w systemie Windows.
author: karann-msft
ms.author: karann
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: e00aac83a710e2f745d5e4bb9aec741ee686e595
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380642"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a>Szybki start: tworzenie i publikowanie pakietu przy użyciu programu Visual Studio (.NET Framework, Windows)

Tworzenie pakietu NuGet z biblioteki klas .NET Framework polega na utworzeniu biblioteki DLL w programie Visual Studio w systemie Windows, a następnie przy użyciu narzędzia wiersza polecenia nuget.exe do tworzenia i publikowania pakietu.

> [!Note]
> Ten przewodnik Szybki start dotyczy programu Visual Studio 2017 i nowszych wersji tylko dla systemu Windows. Visual Studio dla komputerów Mac nie zawiera możliwości opisanych w tym miejscu. Zamiast tego użyj [narzędzi dotnet CLI.](create-and-publish-a-package-using-the-dotnet-cli.md)

## <a name="prerequisites"></a>Wymagania wstępne

1. Zainstaluj dowolną wersję programu Visual Studio 2017 lub nowszą z [visualstudio.com](https://www.visualstudio.com/) z dowolnym . Obciążenie związane z siecią. Visual Studio 2017 automatycznie zawiera funkcje NuGet po zainstalowaniu obciążenia platformy .NET.

1. Zainstaluj `nuget.exe` interfejsu wiersza polecenia, pobierając go `.exe` z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), zapisując ten plik do odpowiedniego folderu i dodając ten folder do zmiennej środowiskowej PATH.

1. [Zarejestruj się na darmowe konto w nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) jeśli jeszcze go nie masz. Utworzenie nowego konta wysyła wiadomość e-mail z potwierdzeniem. Musisz potwierdzić konto, zanim będzie można przesłać pakiet.

## <a name="create-a-class-library-project"></a>Tworzenie projektu biblioteki klas

Można użyć istniejącego projektu biblioteki klas programu .NET Framework dla kodu, który chcesz spakować, lub utworzyć prosty w następujący sposób:

1. W programie Visual Studio wybierz polecenie **Plik > Nowy projekt >**, wybierz węzeł Visual **C#,** wybierz szablon "Biblioteka klas (.NET Framework)" , nazwij projekt AppLogger i kliknij przycisk **OK**.

1. Kliknij prawym przyciskiem myszy wynikowy plik projektu i wybierz **polecenie Build,** aby upewnić się, że projekt został prawidłowo utworzony. Biblioteka DLL znajduje się w folderze debugowania (lub Release, jeśli zamiast tego skompilujesz tę konfigurację).

W ramach prawdziwego pakietu NuGet, oczywiście, można zaimplementować wiele przydatnych funkcji, za pomocą których inni mogą tworzyć aplikacje. Można również ustawić struktury docelowe, jak chcesz. Na przykład zobacz linie pomocnicze dotyczące [platformy uniwersalnej](../guides/create-uwp-packages.md) systemu i [platformy Xamarin](../guides/create-packages-for-xamarin.md).

W tym instruktażu jednak nie będzie pisać żadnego dodatkowego kodu, ponieważ biblioteka klas z szablonu jest wystarczająca do utworzenia pakietu. Mimo to, jeśli chcesz jakiś kod funkcjonalny dla pakietu, użyj następujących czynności:

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
> Jeśli nie masz powodu, aby wybrać inaczej, .NET Standard jest preferowanym obiektem docelowym dla pakietów NuGet, ponieważ zapewnia zgodność z najszerszym zakresem projektów zużywających. Zobacz [Tworzenie i publikowanie pakietu przy użyciu programu Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).

## <a name="configure-project-properties-for-the-package"></a>Konfigurowanie właściwości projektu dla pakietu

Pakiet NuGet zawiera manifest `.nuspec` (plik), który zawiera odpowiednie metadane, takie jak identyfikator pakietu, numer wersji, opis i inne. Niektóre z nich można wyciągnąć bezpośrednio z właściwości projektu, co pozwala uniknąć konieczności oddzielnej aktualizacji ich zarówno w projekcie, jak i w manifeście. W tej sekcji opisano, gdzie można ustawić odpowiednie właściwości.

1. Wybierz polecenie menu **Właściwości projektu >,** a następnie wybierz kartę **Aplikacja.**

1. W polu **Nazwa zestawu** nadaj pakietowi unikatowy identyfikator.

    > [!Important]
    > Należy nadać pakietowi identyfikator, który jest unikatowy w nuget.org lub niezależnie od hosta, którego używasz. W tym instruktażu zalecamy dołączenie "Przykład" lub "Test" w nazwie, ponieważ późniejszy krok publikowania powoduje, że pakiet jest publicznie widoczny (choć jest mało prawdopodobne, aby ktoś go faktycznie używał).
    >
    > Jeśli spróbujesz opublikować pakiet o nazwie, która już istnieje, zostanie wyświetlony błąd.

1. Wybierz przycisk **Informacje o złożeniu...** z wyświetlonym okszeniem dialogowym, w którym można wprowadzić inne właściwości, które przenoszą do manifestu (patrz [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)). Najczęściej używane pola to **Tytuł**, **Opis**, **Firma**, **Prawa autorskie**i Wersja **zestawu**. Te właściwości ostatecznie pojawiają się z pakietem na hoście, takim jak nuget.org, więc upewnij się, że są w pełni opisowe.

    ![Informacje o zestawie w projekcie programu .NET Framework w programie Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. Opcjonalnie: aby wyświetlić i edytować `Properties/AssemblyInfo.cs` właściwości bezpośrednio, otwórz plik w projekcie.

1. Po ustawieniu właściwości ustaw konfigurację projektu na **Zwolnij** i odbuduj projekt, aby wygenerować zaktualizowaną bibliotekę DLL.

## <a name="generate-the-initial-manifest"></a>Generowanie manifestu początkowego

Z DLL w ręku i właściwości projektu `nuget spec` zestaw, można `.nuspec` teraz użyć polecenia do wygenerowania pliku początkowego z projektu. Ten krok zawiera odpowiednie tokeny zastępcze do rysowania informacji z pliku projektu.

Uruchom `nuget spec` tylko raz, aby wygenerować manifest początkowy. Podczas aktualizowania pakietu, można zmienić wartości w projekcie lub edytować manifest bezpośrednio.

1. Otwórz wiersz polecenia i przejdź do `AppLogger.csproj` folderu projektu zawierającego plik.

1. Uruchom następujące polecenie: `nuget spec AppLogger.csproj`. Określając projekt, NuGet tworzy manifest, który pasuje do nazwy projektu, w tym przypadku. `AppLogger.nuspec` Zawiera również tokeny zastępowania w manifeście.

1. Otwórz `AppLogger.nuspec` w edytorze tekstu, aby sprawdzić jego zawartość, która powinna wyglądać następująco:

    ```xml
    <?xml version="1.0"?>
    <package >
      <metadata>
        <id>Package</id>
        <version>1.0.0</version>
        <authors>YourUsername</authors>
        <owners>YourUsername</owners>
        <license type="expression">MIT</license>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Package description</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2019</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a>Edytowanie manifestu

1. NuGet generuje błąd, jeśli spróbujesz utworzyć pakiet `.nuspec` z wartościami domyślnymi w pliku, więc należy edytować następujące pola przed kontynuowaniem. Zobacz [.nuspec odwołanie do pliku — opcjonalne elementy metadanych,](../reference/nuspec.md#optional-metadata-elements) aby uzyskać opis sposobu ich użycia.

    - licencjaUrl
    - projektUrl
    - ikonaUrl
    - releaseNotes
    - tags

1. W przypadku pakietów przeznaczonych do użytku publicznego należy zwrócić szczególną uwagę na właściwość **Tagi,** ponieważ tagi pomagają innym znaleźć pakiet w źródłach takich jak nuget.org i zrozumieć, co robi.

1. W tej chwili można również dodać dowolne inne elementy do manifestu, zgodnie z opisem w [pliku .nuspec.](../reference/nuspec.md)

1. Zapisz plik przed kontynuowaniem.

## <a name="run-the-pack-command"></a>Uruchamianie polecenia pack

1. W wierszu polecenia w folderze zawierającym `.nuspec` `nuget pack`plik uruchom polecenie .

1. NuGet generuje `.nupkg` plik w postaci *identyfikatora-version.nupkg*, który znajdziesz w bieżącym folderze.

## <a name="publish-the-package"></a>Publikowanie pakietu

Po opublikowaniu `.nupkg` pliku można go opublikować w `nuget.exe` celu nuget.org przy użyciu klucza interfejsu API uzyskanego z nuget.org. W przypadku nuget.org należy `nuget.exe` używać 4.1.0 lub nowszego.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Uzyskaj klucz interfejsu API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>Publikuj z nuget push

1. Otwórz wiersz polecenia i zmień folder `.nupkg` zawierający plik.

1. Uruchom następujące polecenie, określając nazwę pakietu i zastępując wartość klucza kluczem interfejsu API:

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe wyświetla wyniki procesu publikowania:

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

Zobacz [nuget push](../reference/cli-reference/cli-ref-push.md).

### <a name="publish-errors"></a>Błędy publikowania

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Zarządzanie opublikowanym pakietem

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a>Następne kroki

Gratulujemy stworzenia pierwszego pakietu NuGet!

> [!div class="nextstepaction"]
> [Tworzenie pakietu](../create-packages/creating-a-package.md)

Aby dowiedzieć się więcej, że NuGet ma do zaoferowania, wybierz poniższe łącza.

- [Publikowanie pakietu](../nuget-org/publish-a-package.md)
- [Pakiety w wersji wstępnej](../create-packages/Prerelease-Packages.md)
- [Obsługa wielu platform docelowych](../create-packages/supporting-multiple-target-frameworks.md)
- [Przechowywanie wersji pakietów](../concepts/package-versioning.md)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
