---
title: Tworzenie i publikowanie pakietu platformy .NET Framework, za pomocą programu Visual Studio na Windows
description: Samouczek wskazówki na temat tworzenia i publikowania pakietu NuGet programu .NET Framework za pomocą programu Visual Studio 2017 na Windows.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: ffa2128b577673e980f4115f37f8685858c36250
ms.sourcegitcommit: 6cffa6ef59b922df2d87aa9c24034d00542983cd
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2018
ms.locfileid: "37963162"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a>Szybki Start: Tworzenie i publikowanie pakietu przy użyciu programu Visual Studio (.NET Framework, Windows)

Tworzenie pakietu NuGet w bibliotece klas programu .NET Framework obejmuje tworzenie biblioteki DLL w programie Visual Studio na Windows, a następnie przy użyciu narzędzia wiersza polecenia nuget.exe umożliwiającego tworzenie i publikowanie pakietu.

> [!Note]
> Ten przewodnik Szybki Start ma zastosowanie do programu Visual Studio 2017 for Windows tylko. Visual Studio dla komputerów Mac nie ma możliwości opisane w tym miejscu. Użyj [narzędzi interfejsu wiersza polecenia dotnet](create-and-publish-a-package-using-the-dotnet-cli.md) zamiast tego.

## <a name="prerequisites"></a>Wymagania wstępne

1. Instalowania dowolnej wersji programu Visual Studio 2017 z [visualstudio.com](https://www.visualstudio.com/) ze wszystkimi. Obciążenie związane z sieci. Po zainstalowaniu obciążenia platformy .NET, Visual Studio 2017 zawiera automatycznie możliwości NuGet.

1. Zainstaluj `nuget.exe` interfejsu wiersza polecenia, pobierając go z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), zapisywania, który `.exe` pliku do odpowiedniego folderu i dodawanie folderu do zmiennej środowiskowej PATH.

1. [Zarejestruj, aby utworzyć bezpłatne konto w witrynie nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Jeśli nie masz jeszcze takiego. Tworzenie nowego konta wysyła wiadomość e-mail z potwierdzeniem. Aby można było przekazać pakiet, należy potwierdzić konto.

## <a name="create-a-class-library-project"></a>Utwórz projekt biblioteki klas

Można użyć istniejącego projektu biblioteki klas .NET Framework dla kodu, który ma być pakietu lub Utwórz proste w następujący sposób:

1. W programie Visual Studio, wybierz **Plik > Nowy > Projekt**, wybierz opcję **Visual C#** węzła, wybierz szablon "Biblioteka klas (.NET Framework)", nazwij projekt AppLogger i kliknij przycisk **OK**.

1. Kliknij prawym przyciskiem myszy, wynikowy plik projektu, a następnie wybierz pozycję **kompilacji** się upewnić, że projekt został utworzony prawidłowo. Biblioteka DLL znajduje się w folderze debugowania (lub wydania, jeśli tworzysz tę konfigurację zamiast).

W ciągu rzeczywistą pakietu NuGet oczywiście, możesz zaimplementować wiele przydatnych funkcji, które inne osoby mogą tworzyć aplikacje. Można również ustawić platform docelowych w dowolny sposób. Na przykład, zapoznaj się z przewodnikami dla [platformy uniwersalnej systemu Windows](../guides/create-uwp-packages.md) i [Xamarin](../guides/create-packages-for-xamarin.md).

W tym przewodniku jednak nie będzie pisania żadnego dodatkowego kodu ponieważ biblioteki klas na podstawie tego szablonu jest wystarczające, aby utworzyć pakiet. Jednak jeśli chcesz funkcjonalności kodu dla pakietu, użyj następującego polecenia:

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
> Chyba że istnieje powód, aby wybrać inny sposób, .NET Standard jest preferowany cel pakiety NuGet, ponieważ zapewnia zgodność z szeroką gamą wykorzystywanie projektów. Zobacz [tworzenie i publikowanie pakietu przy użyciu programu Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).

## <a name="configure-project-properties-for-the-package"></a>Konfigurowanie właściwości projektu pakietu

Pakiet NuGet zawiera manifest ( `.nuspec` pliku), który zawiera istotne metadane, takie jak identyfikator pakietu, numer wersji, opis i. Niektóre z nich może być pobierana z właściwości projektu bezpośrednio, co pozwala uniknąć konieczności oddzielnie zaktualizować je w manifeście i projektu. W tej sekcji opisano, gdzie można ustawić odpowiednich właściwości.

1. Wybierz **projektu > właściwości** menu polecenia, a następnie wybierz **aplikacji** kartę.

1. W **nazwy zestawu** pola, nadaj Unikatowy identyfikator pakietu.

    > [!Important]
    > Musisz nadać pakietu, identyfikator, który jest unikatowa w obrębie nuget.org, lub niezależnie od rodzaju hoście jest używany. W ramach tego przewodnika firma Microsoft zaleca, tym "Próbny" lub "Test" w nazwie późniejszym etapie publikowania uwidocznić pakietu publicznie (choć jest mało prawdopodobne, każda osoba będzie faktycznie używać).
    >
    > Jeśli spróbujesz opublikować pakietu o nazwie, która już istnieje, zostanie wyświetlony błąd.

1. Wybierz **informacje o zestawie...**  przycisk, który wywołuje okno dialogowe, w którym należy wprowadzić inne właściwości, które zawierają do manifestu (zobacz [odwołanie do pliku .nuspec - zastąpienia tokenów](../reference/nuspec.md#replacement-tokens)). Najczęściej używanych pól są **tytuł**, **opis**, **firmy**, **Copyright**, i **wersji zestawu**. Te właściwości są wyświetlane ostatecznie z pakietem na hoście, np. nuget.org, dlatego upewnij się, że są one w pełni opisowe.

    ![Informacje o zestawie w projekcie programu .NET Framework w programie Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. Opcjonalnie: Aby wyświetlić i edytować właściwości bezpośrednio, otwórz `Properties/AssemblyInfo.cs` pliku w projekcie.

1. Po ustawieniu właściwości jest równa konfiguracji projektu **wersji** i ponownie skompiluj projekt, aby wygenerować zaktualizowanego pliku DLL.

## <a name="generate-the-initial-manifest"></a>Generuj manifest początkowej

Z biblioteki DLL w zestawie właściwości strony, a projekt, możesz teraz używać `nuget spec` polecenie, aby wygenerować początkową `.nuspec` pliku z projektem. Ten krok obejmuje odpowiednie zastąpienia tokenów pobierające informacje z pliku projektu.

Możesz uruchomić `nuget spec` tylko raz, aby wygenerować manifest początkowej. Podczas aktualizowania pakietu, można zmienić wartości w projekcie albo bezpośrednio edytować manifestu.

1. Otwórz wiersz polecenia i przejdź do folderu projektu zawierającego `AppLogger.csproj` pliku.

1. Uruchom następujące polecenie: `nuget spec AppLogger.csproj`. Określając projektu, NuGet tworzy manifest, który jest zgodna z nazwą projektu, w tym przypadku `AppLogger.nuspec`. To również obejmować zastąpienia tokenów w manifeście.

1. Otwórz `AppLogger.nuspec` w edytorze tekstów, aby zbadać jego zawartość, która powinna wyglądać następująco:

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

1. NuGet generuje błąd, Jeśli spróbujesz utworzyć pakiet z wartościami domyślnymi w swojej `.nuspec` plików, dlatego należy zmodyfikować następujące pola, przed kontynuowaniem. Zobacz [odwołanie do pliku .nuspec — pojedyncze elementy](../reference/nuspec.md#single-elements) opis jak są one używane.

    - licenseUrl
    - projectUrl
    - iconUrl
    - releaseNotes
    - tagi

1. Pakiety utworzone do użytku publicznego, należy zwrócić szczególną uwagę na **tagi** właściwości, jak tagi pomóc innym odnaleźć pakietu na źródeł, takich jak nuget.org i zrozumieć, co robi.

1. Można również dodać inne elementy do manifestu w tej chwili zgodnie z opisem na [odwołanie do pliku .nuspec](../reference/nuspec.md).

1. Zapisz plik przed kontynuowaniem.

## <a name="run-the-pack-command"></a>Uruchom polecenie pakietu

1. Z poziomu wiersza polecenia w folderze zawierającym swoje `.nuspec` pliku, uruchom polecenie `nuget pack`.

1. Generuje NuGet `.nupkg` pliku w postaci *version.nupkg identyfikator*, które znajdują się w bieżącym folderze.

## <a name="publish-the-package"></a>Publikowanie pakietu

Po utworzeniu `.nupkg` pliku opublikujesz go w witrynie nuget.org przy użyciu `nuget.exe` przy użyciu klucza interfejsu API uzyskanych z repozytorium nuget.org. Nuget.org należy używać `nuget.exe` 4.1.0 lub nowszej.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Uzyskiwanie klucza interfejsu API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>Publikowanie za pomocą wypychania nuget

1. Zmień folder zawierający `.nupkg` pliku.

1. Uruchom następujące polecenie, określając nazwę pakietu i zastępując wartość klucza swój klucz interfejsu API:

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe wyświetla wyniki proces publikowania:

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

Zobacz [wypychania nuget](../tools/cli-ref-push.md).

### <a name="publish-errors"></a>Publikowanie błędy

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Zarządzanie opublikowany pakiet

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>Tematy pokrewne

- [Utwórz pakiet](../create-packages/creating-a-package.md)
- [Publikowanie pakietu](../create-packages/publish-a-package.md)
- [Pakiety w wersji wstępnej](../create-packages/Prerelease-Packages.md)
- [Obsługa wielu platform docelowych](../create-packages/supporting-multiple-target-frameworks.md)
- [Przechowywanie wersji pakietów](../reference/package-versioning.md)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
