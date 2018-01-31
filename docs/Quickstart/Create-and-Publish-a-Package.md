---
title: "Przewodnik wprowadzający do tworzenia i pakietu NuGet publikowania | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/03/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Samouczek wskazówki na temat tworzenia i publikowania pakietu NuGet przy użyciu interfejsu wiersza polecenia nuget.exe i Visual Studio."
keywords: Tworzenie pakietu NuGet, pakietu NuGet publikowania, samouczek NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 53d29283c9e786fc27e9a608d7d251d8d0b5b0b2
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="create-and-publish-a-package"></a>Tworzenie i publikowanie pakietu

Jest to prosty proces tworzenia pakietu NuGet z biblioteki klas .NET i opublikowania go w usłudze nuget.org. Ten artykuł przeprowadzi Cię przez proces, korzystając z NuGet interfejsu wiersza polecenia (CLI) i Visual Studio.

## <a name="pre-requisites"></a>Wymagania wstępne

1. Zainstalowania dowolnej wersji programu Visual Studio 2017 z [visualstudio.com](https://www.visualstudio.com/).

1. Zainstaluj narzędzie interfejsu wiersza polecenia NuGet `nuget.exe`, pobierając najnowszą wersję `nuget.exe` z [nuget.org/downloads](https://nuget.org/downloads)i zapisywanie `.exe` do lokalizacji w ŚCIEŻCE. Należy pamiętać, że pobieranie *jest* samo narzędzie, nie Instalatora.

1. Utworzenie odpowiedniego projektu Biblioteka klas programu .NET dla kodu, który ma być pakietu. Jeśli nie masz już projekt, można utworzyć tylko jedna w następujący sposób:
    1. W programie Visual Studio, wybierz **Plik > Nowy > Projekt**, rozwiń węzeł **Visual C# > Windows** węzła, wybierz szablon "Biblioteki klas", nazwa projektu AppLogger i kliknij przycisk **OK**.
    1. Kliknij prawym przyciskiem myszy na wynikowy plik projektu i wybierz **kompilacji** się upewnić, że projekt został utworzony prawidłowo. Biblioteki DLL znajduje się w folderze debugowania (lub wersji, jeśli zamiast tego kompilacji tej konfiguracji).

    Oczywiście w rzeczywistym pakiecie NuGet, będzie wdrożenie wielu przydatnych funkcji, na których inne osoby mogą tworzyć aplikacje. W ramach tego przewodnika jednak nie będzie pisania jakiegokolwiek dodatkowego kodu ponieważ biblioteki klas z szablonu jest wystarczające, aby utworzyć pakiet.

## <a name="create-the-nuspec-package-manifest-file"></a>Utwórz plik manifestu pakietu .nuspec

Każdy pakiet NuGet musi manifestu&mdash; `.nuspec` pliku&mdash;do opisywania zawartością i jego zależności. `nuget spec` Polecenie tworzy plik dla Ciebie, którą można następnie dostosować. W tym przykładzie utworzysz `.nuspec` z pliku projektu; można też utworzyć manifestu w inny sposób zgodnie z opisem na [Utwórz pakiet](../create-packages/creating-a-package.md).

1. Otwórz wiersz polecenia i przejdź do folderu zawierającego plik projektu (`.csproj`).

1. Uruchamianie interfejsu wiersza polecenia NuGet `spec` polecenie, aby wygenerować manifest, nosi nazwę po projektu, takie jak `AppLogger.nuspec`:

    ```cli
    nuget spec
    ```

1. Otwórz plik w edytorze tekstów. Manifest wygląda kod poniżej, gdzie tokenów w postaci `<token>` (takie jak `$id$`) są zastępowane podczas procesu tworzenia pakietów z wartościami z pliku Properties/AssemblyInfo.cs projektu. Aby uzyskać więcej szczegółów na tokeny, zobacz [Tworzenie pliku .nuspec](../create-packages/creating-a-package.md#creating-the-nuspec-file).

    ```xml
    <?xml version="1.0"?>
    <package>
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
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. Wybierz identyfikator pakietu, który jest unikatowy w całej nuget.org. Firma Microsoft zaleca używanie konwencji nazewnictwa opisanego w [utworzenie pakietu](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number). Należy zaktualizować tagi autora oraz opis lub błąd pojawia się w następnym kroku. Oto zaktualizowaną `.nuspec` pliku, na przykład:

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> Skompilowany dla publicznych zużycia pakietów, należy zwrócić szczególną uwagę na `<tags>` element, jak te znaczniki ułatwiała innym pakietu odnaleźć i zrozumieć, jakie operacje.

## <a name="run-the-pack-command"></a>Uruchom polecenie pakietu

Aby utworzyć pakiet NuGet ( `.nupkg` plik) z projektem, uruchom `pack` polecenia:

```cli
nuget pack AppLogger.csproj
```

To polecenie tworzy `AppLogger.1.0.0.0.nupkg` za pomocą numeru nazwę i wersję pakietu z `.nuspec` pliku. Polecenie wystawia ostrzeżenia, jeśli nie zostały zaktualizowane różnych pól w `.nuspec` pliku z wartościami domyślnymi.

## <a name="publish-the-package"></a>Publikowanie pakietu

Po utworzeniu `.nupkg` pliku opublikowaniu go przy użyciu nuget.org `push` polecenia. (Alternatywnie można użyć [nuget.org publikowania przepływu pracy](../create-packages/publish-a-package.md#publish-to-nugetorg).

> [!Warning]
> Pakiety, które publikowania nuget.org są publicznie widoczne dla innych deweloperów. Do hostowania pakietów prywatnie, zobacz [Hosting pakiety](../hosting-packages/overview.md).

1. Utwórz bezpłatne konto na [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), lub jeśli już istnieje. Tworzenie nowego konta wysyła wiadomość e-mail z potwierdzeniem. Aby przekazać pakiet, musisz potwierdzić konto.

1. Po zalogowaniu, wybierz nazwę użytkownika (w prawym górnym rogu), a następnie wybierz **klucze interfejsu API**.

1. Wybierz **Utwórz**, podaj nazwę klucza, wybierz **wybierz zakresy > Push** w obszarze **klucz interfejsu API**, wprowadź * dla **wzorzec Glob**, następnie Wybierz **Utwórz**.

1. Po klucz zostanie utworzony, wybierz **kopiowania** można pobrać dostępu do klucza będziesz potrzebować na platformie interfejsu wiersza polecenia:

    ![Kopiowanie do Schowka klucz interfejsu API](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > Zapisz klucz w bezpiecznej lokalizacji, a nie ujawniaj go. Jeśli klucz zostanie przypadkowo ujawniony, można go odtworzyć w dowolnym momencie. Można również usunąć klucz interfejsu API, jeśli nie chcesz push pakietów za pomocą interfejsu wiersza polecenia.

1. W wierszu polecenia, uruchom następujące polecenie określając nazwę pakietu i zastępowanie klucza o wartości skopiowany w kroku 4:

    ```cli
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe wyświetla wyniki procesu publikowania:

    ```output
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. Z profilu nuget.org, wybierz **Zarządzaj pakietami** można znaleźć w jednym opublikowana. Otrzymasz również wiadomość e-mail z potwierdzeniem. Należy pamiętać, że może upłynąć trochę czasu pakietu indeksowane i wyświetlana w wynikach wyszukiwania, gdzie innym go znaleźć. W tym czasie stronę pakietu zawiera następujący komunikat:

    ![Ten pakiet nie ma jeszcze indeksowania. Zostanie wyświetlony w wynikach wyszukiwania, a będą dostępne do instalacji i przywracania po zakończeniu indeksowania.](media/QS_Create-03-NotIndexed.png)

> [!Note]
> **Skanowania antywirusowego**: wszystkie pakiety przekazane do nuget.org są skanowane pod kątem wirusów i odrzucone w przypadku znalezienia wirusy. Wszystkie pakiety wymienione na nuget.org również są skanowane okresowo.

I to już wszystko! Został właśnie opublikowany pakiet NuGet pierwszy [nuget.org](https://www.nuget.org/), który innych deweloperzy mogą używać w ich własnych projektów.

## <a name="related-topics"></a>Tematy pokrewne

- [Tworzenie pakietu](../create-packages/creating-a-package.md)
- [Publikowanie pakietu](../create-packages/publish-a-package.md)
- [Obsługuje wiele platform docelowych](../create-packages/supporting-multiple-target-frameworks.md)
- [Przechowywanie wersji pakietu](../reference/package-versioning.md)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
