---
title: Tworzenie i publikowanie pakietu .NET Framework w systemie Windows przy użyciu programu Visual Studio
description: Samouczek wskazówki na temat tworzenia i publikowania pakietu NuGet programu .NET Framework w systemie Windows za pomocą programu Visual Studio 2017 r.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: ffa2128b577673e980f4115f37f8685858c36250
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818272"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a>Szybki Start: Tworzenie i publikowanie pakietu programu Visual Studio (.NET Framework, system Windows)

Tworzenie pakietu NuGet w bibliotece klas programu .NET Framework obejmuje tworzenie biblioteki DLL w programie Visual Studio w systemie Windows, a następnie tworzyć i publikować pakietu przy użyciu narzędzia wiersza polecenia nuget.exe.

> [!Note]
> Ta opcja szybkiego startu dotyczy programu Visual Studio 2017 r dla systemu Windows tylko. Visual Studio for Mac nie ma możliwości opisane w tym miejscu. Użyj [narzędzi interfejsu wiersza polecenia platformy dotnet](create-and-publish-a-package-using-the-dotnet-cli.md) zamiast tego.

## <a name="prerequisites"></a>Wymagania wstępne

1. Zainstalowania dowolnej wersji programu Visual Studio 2017 z [visualstudio.com](https://www.visualstudio.com/) ze wszystkimi. Obciążenia związane z sieci. Visual Studio 2017 automatycznie uwzględnia możliwości NuGet obciążenia .NET jest zainstalowany.

1. Zainstaluj `nuget.exe` interfejsu wiersza polecenia, pobierając go z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), zapisywanie, który `.exe` pliku do odpowiedniego folderu, a następnie dodanie tego folderu do Twojej zmiennej środowiskowej PATH.

1. [Zarejestruj bezpłatne konto na nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Jeśli nie masz już. Tworzenie nowego konta wysyła wiadomość e-mail z potwierdzeniem. Aby przekazać pakiet, musisz potwierdzić konto.

## <a name="create-a-class-library-project"></a>Tworzenie projektu biblioteki klas

Można użyć istniejącego projektu biblioteki klas programu .NET Framework dla kodu, który ma być pakietu lub Utwórz proste w następujący sposób:

1. W programie Visual Studio, wybierz **Plik > Nowy > Projekt**, wybierz pozycję **Visual C#** węzła, wybierz szablon "Biblioteki klas (.NET Framework)", nazwa projektu AppLogger i kliknij przycisk **OK**.

1. Kliknij prawym przyciskiem myszy na wynikowy plik projektu i wybierz **kompilacji** się upewnić, że projekt został utworzony prawidłowo. Biblioteki DLL znajduje się w folderze debugowania (lub wersji, jeśli zamiast tego kompilacji tej konfiguracji).

W rzeczywistym pakiecie NuGet oczywiście zaimplementowaniem wielu przydatnych funkcji, które inne osoby mogą tworzyć aplikacje. Można również ustawić docelowych platform w dowolny sposób. Na przykład, zobacz wskazówki dotyczące [UWP](../guides/create-uwp-packages.md) i [Xamarin](../guides/create-packages-for-xamarin.md).

W ramach tego przewodnika jednak nie będzie pisania jakiegokolwiek dodatkowego kodu ponieważ biblioteki klas z szablonu jest wystarczające, aby utworzyć pakiet. Nadal Jeśli chcesz funkcjonalności kodu dla pakietu, użyj następującego polecenia:

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
> Chyba że masz powód, w przeciwnym razie wybierz .NET Standard preferowanych celem jest pakietów NuGet, ponieważ zapewnia zgodność z szeroką gamą korzystanie z projektów. Zobacz [tworzenie i publikowanie pakietu programu Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).

## <a name="configure-project-properties-for-the-package"></a>Skonfiguruj właściwości projektu dla pakietu

Pakiet NuGet zawiera manifest ( `.nuspec` pliku), który zawiera odpowiednie metadane, takie jak identyfikator pakietu, numer wersji, opis i. Niektóre z nich może być pobierana właściwości projektu, który pozwala uniknąć konieczności zaktualizowania ich osobno w manifeście i projektu. Ta sekcja zawiera wskazówki dotyczące Ustaw odpowiednie właściwości.

1. Wybierz **projektu > właściwości** menu polecenie, a następnie wybierz **aplikacji** kartę.

1. W **nazwy zestawu** pola, nadaj Unikatowy identyfikator pakietu.

    > [!Important]
    > Podaj pakiet używany unikatowy identyfikator w nuget.org lub niezależnie od hosta można. W ramach tego przewodnika, zaleca się tym "Sample" lub "Test" w nazwie, ponieważ kolejnych kroków publikowania pakietu widocznego publicznie (chociaż jest mało prawdopodobne, każda osoba, która zostanie rzeczywiście używane).
    >
    > Jeśli spróbujesz opublikować pakiet o nazwie, która już istnieje, zostanie wyświetlony błąd.

1. Wybierz **informacji o zestawie...**  przycisku, który wywołuje okno dialogowe, w którym należy wprowadzić w manifeście innych właściwości, które obsługują (zobacz [odwołania do pliku .nuspec — zastępczy tokenów](../reference/nuspec.md#replacement-tokens)). Najczęściej używane pola są **tytuł**, **opis**, **firmy**, **Copyright**, i **wersja zestawu**. Dlatego te właściwości są wyświetlane ostatecznie w pakiecie na hoście, takich jak nuget.org, upewnij się, że są one w pełni opisowy.

    ![Informacje o zestawie w projekcie programu .NET Framework w programie Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. Opcjonalnie: Aby wyświetlić i edytować właściwości bezpośrednio, otwórz `Properties/AssemblyInfo.cs` pliku w projekcie.

1. Właściwości ustawione, ustaw dla konfiguracji projektu **wersji** i skompiluj ponownie projekt, aby wygenerować zaktualizowanej biblioteki DLL.

## <a name="generate-the-initial-manifest"></a>Generuj manifest początkowej

Z biblioteki DLL w zestawie właściwości strony, a projekt, można teraz używać `nuget spec` polecenie, aby wygenerować początkowego `.nuspec` plik z projektu. Ten krok obejmuje tokeny zastępczy odpowiednie do rysowania informacji z pliku projektu.

Uruchomienie `nuget spec` tylko jeden raz, aby wygenerować manifest początkowej. Podczas aktualizowania pakietu, można zmienić wartości w projekcie albo bezpośredniego edytowania manifestu.

1. Otwórz wiersz polecenia i przejdź do folderu projektu zawierającego `AppLogger.csproj` pliku.

1. Uruchom następujące polecenie: `nuget spec AppLogger.csproj`. Określając projektu NuGet tworzy manifestu, który pasuje do nazwy projektu, w tym przypadku `AppLogger.nuspec`. Również obejmować tokeny zastąpienia w manifeście.

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

1. NuGet powoduje błąd przy próbie utworzenia pakietu z wartościami domyślnymi w Twojej `.nuspec` plików, dlatego należy zmodyfikować następujące pola przed kontynuowaniem. Zobacz [odwołania do pliku .nuspec — pojedyncze elementy](../reference/nuspec.md#single-elements) opis jak są one używane.

    - licenseUrl
    - projectUrl
    - iconUrl
    - releaseNotes
    - tagi

1. Skompilowany dla publicznych zużycia pakietów, należy zwrócić szczególną uwagę na **tagi** właściwości, jak tagi ułatwiała innym pakietu na źródeł, takich jak nuget.org odnaleźć i zrozumieć, jakie operacje.

1. Możesz także dodać inne elementy do manifestu w tej chwili zgodnie z opisem na [odwołania do pliku .nuspec](../reference/nuspec.md).

1. Zapisz plik przed kontynuowaniem.

## <a name="run-the-pack-command"></a>Uruchom polecenie pakietu

1. Z wiersza polecenia w folder zawierający Twoje `.nuspec` plików, uruchom polecenie `nuget pack`.

1. Generuje NuGet `.nupkg` pliku w postaci *version.nupkg identyfikator*, które znajdują się w bieżącym folderze.

## <a name="publish-the-package"></a>Publikowanie pakietu

Po utworzeniu `.nupkg` pliku opublikowaniu go przy użyciu nuget.org `nuget.exe` przy użyciu klucza interfejsu API uzyskane z nuget.org. W przypadku nuget.org należy użyć `nuget.exe` 4.1.0 lub nowszej.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Uzyskanie klucza interfejsu API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>Publikowanie za pomocą wypychania nuget

1. Zmień folder zawierający `.nupkg` pliku.

1. Uruchom następujące polecenie, określając nazwę pakietu i zamianę klucza wartość klucza interfejsu API:

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

Zobacz [wypychania nuget](../tools/cli-ref-push.md).

### <a name="publish-errors"></a>Publikowanie błędów

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Zarządzanie opublikowanego pakietu

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>Tematy pokrewne

- [Tworzenie pakietu](../create-packages/creating-a-package.md)
- [Publikowanie pakietu](../create-packages/publish-a-package.md)
- [Pakiety wersji wstępnej](../create-packages/Prerelease-Packages.md)
- [Obsługuje wiele platform docelowych](../create-packages/supporting-multiple-target-frameworks.md)
- [Przechowywanie wersji pakietów](../reference/package-versioning.md)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
