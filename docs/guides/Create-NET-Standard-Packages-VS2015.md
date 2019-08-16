---
title: Tworzenie pakietów NuGet .NET Standard i .NET Framework za pomocą programu Visual Studio 2015
description: Kompleksowy przewodnik tworzenia pakietów NuGet .NET Standard i .NET Framework przy użyciu programu NuGet 3. x i programu Visual Studio 2015.
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: 11dce27b93c3d09a2d27dc79f8d4fed86df879ba
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488973"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a>Tworzenie pakietów .NET Standard i .NET Framework za pomocą programu Visual Studio 2015

**Uwaga:** Program Visual Studio 2017 jest zalecany do tworzenia bibliotek .NET Standard. Program Visual Studio 2015 może współpracować, ale narzędzia .NET Core zostały przesunięte tylko do stanu wersji zapoznawczej. Zobacz [Tworzenie i publikowanie pakietu przy użyciu programu Visual studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) do pracy z pakietem NuGet 4. x + i Visual Studio 2017.

[Biblioteka .NET Standard](/dotnet/articles/standard/library) jest formalną specyfikacją interfejsów API platformy .NET, które mają być dostępne we wszystkich środowiskach uruchomieniowych platformy .NET, a tym samym ustanowienie większej jednorodności w ekosystemie platformy .NET. Biblioteka .NET Standard definiuje jednolity zestaw interfejsów API BCL (Biblioteka klas bazowych) dla wszystkich platform .NET do implementacji, niezależnie od obciążenia. Umożliwia deweloperom tworzenie kodu, który jest użyteczny dla wszystkich środowisk uruchomieniowych platformy .NET, i zmniejsza, czy nie eliminuje specyficznych dla platformy dyrektyw kompilacji warunkowej w kodzie udostępnionym.

Ten przewodnik przeprowadzi Cię przez proces tworzenia pakietu NuGet przeznaczony do .NET Standard biblioteki 1,4 lub pakietu docelowego .NET Framework 4,6. Biblioteka .NET Standard 1,4 działa w .NET Framework 4.6.1, platforma uniwersalna systemu Windows 10, .NET Core i mono/Xamarin. Aby uzyskać szczegółowe informacje, zobacz [tabelę mapowania .NET Standard](/dotnet/standard/net-standard#net-implementation-support) (dokumentacja platformy .NET). Jeśli chcesz, możesz wybrać inną wersję biblioteki .NET Standard.

## <a name="prerequisites"></a>Wymagania wstępne

1. Visual Studio 2015 Update 3
1. (Tylko .NET Standard) [Zestaw .NET Core SDK](https://www.microsoft.com/net/download/)
1. Interfejs wiersza polecenia NuGet. Pobierz najnowszą wersję pliku NuGet. exe z [NuGet.org/downloads](https://nuget.org/downloads), zapisując ją w wybranej lokalizacji. Następnie Dodaj tę lokalizację do zmiennej środowiskowej PATH, jeśli nie została jeszcze.

    > [!Note]
    > NuGet. exe to narzędzie interfejsu wiersza polecenia, a nie Instalator, dlatego pamiętaj o zapisaniu pobranego pliku w przeglądarce zamiast uruchamiania go.

## <a name="create-the-class-library-project"></a>Utwórz projekt biblioteki klas

1. W programie Visual Studio, **plik > nowy > projektu**, rozwiń **węzeł C# Visual > Windows** , wybierz pozycję **Biblioteka klas (przenośna)** , Zmień nazwę na AppLogger i wybierz **przycisk OK**.

    ![Utwórz nowy projekt biblioteki klas](media/NetStandard-NewProject.png)

1. W wyświetlonym oknie dialogowym **Dodaj przenośną bibliotekę klas** wybierz opcje dla `.NET Framework 4.6` i `ASP.NET Core 1.0`. (Jeśli .NET Framework określania wartości docelowej, możesz wybrać opcje, które są odpowiednie.)

1. Jeśli element docelowy jest .NET Standard, kliknij prawym `AppLogger (Portable)` przyciskiem myszy w Eksplorator rozwiązań, wybierz pozycję **Właściwości**, wybierz kartę **Biblioteka** , a następnie wybierz pozycję docelowa **platforma .NET Standard** w sekcji **Określanie wartości docelowej** . Ta akcja monituje o potwierdzenie, a następnie można wybrać `.NET Standard 1.4` (lub inną dostępną wersję) z listy rozwijanej:

    ![Ustawianie elementu docelowego na .NET Standard 1,4](media/NetStandard-ChangeTarget.png)

1. Kliknij kartę **kompilacja** , Zmień **konfigurację** na `Release`, a następnie zaznacz pole wyboru **plik dokumentacji XML**.

1. Dodaj kod do składnika, na przykład:

    ```cs
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

1. Ustaw konfigurację na wydawanie, Skompiluj projekt i sprawdź, czy pliki dll i XML są tworzone w `bin\Release` folderze.

## <a name="create-and-update-the-nuspec-file"></a>Utwórz i zaktualizuj plik. nuspec

1. Otwórz wiersz polecenia, przejdź `AppLogger.csproj` do folderu zawierającego folder (jeden poziom poniżej `.sln` lokalizacji pliku) i uruchom polecenie NuGet `spec` , aby utworzyć plik początkowy `AppLogger.nuspec` :

    ```cli
    nuget spec
    ```

1. Otwórz `AppLogger.nuspec` w edytorze i zaktualizuj go, aby pasował do następujących wartości, zastępując YOUR_NAME z odpowiednią wartością. Wartość, szczególnie, musi być unikatowa w obrębie NuGet.org (zobacz Konwencje nazewnictwa opisane w artykule [Tworzenie pakietu.](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) `<id>` Należy również pamiętać, że należy również zaktualizować Tagi autor i opis lub podczas kroku pakowania wystąpi błąd.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

1. Dodaj zestawy odwołań do `.nuspec` pliku, a mianowicie biblioteki dll biblioteki i pliku XML IntelliSense:

    W przypadku .NET Standard określania wartości docelowej wpisy są podobne do następujących:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    W przypadku .NET Framework określania wartości docelowej wpisy są podobne do następujących:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. Kliknij prawym przyciskiem myszy rozwiązanie i wybierz pozycję **Kompiluj rozwiązanie** , aby wygenerować wszystkie pliki pakietu.

### <a name="declaring-dependencies"></a>Deklarowanie zależności

Jeśli masz jakiekolwiek zależności od innych pakietów NuGet, wystaw je w `<dependencies>` elemencie manifestu z `<group>` elementami. Na przykład, aby zadeklarować zależność w NewtonSoft. JSON 8.0.3 lub powyżej, Dodaj następujące elementy:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

Składnia atrybutu *Version* w tym miejscu wskazuje, że wersja 8.0.3 lub nowsza jest akceptowalna. Aby określić różne zakresy wersji, zapoznaj się z artykułem [wersja pakietu](../concepts/package-versioning.md).

### <a name="adding-a-readme"></a>Dodawanie pliku Readme

Utwórz plik, umieść go w folderze głównym projektu i odwołaj się do niego `.nuspec` w pliku: `readme.txt`

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```

Program Visual Studio `readme.txt` jest wyświetlany, gdy pakiet jest instalowany w projekcie. Plik nie jest wyświetlany, gdy jest zainstalowany w projektach .NET Core lub dla pakietów zainstalowanych jako zależność.

## <a name="package-the-component"></a>Pakowanie składnika

Po zakończeniu `.nuspec` odwoływania się do wszystkich plików, które należy uwzględnić w pakiecie, możesz `pack` uruchomić polecenie:

```cli
nuget pack AppLogger.nuspec
```

Spowoduje to `AppLogger.YOUR_NAME.1.0.0.nupkg`wygenerowanie. Otwieranie tego pliku w narzędziu, takim jak [Eksplorator pakietów NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzanie wszystkich węzłów, zostanie wyświetlona następująca zawartość (pokazana dla .NET standard):

![Eksplorator pakietów NuGet przedstawiający pakiet AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> `.nupkg` Plik jest po prostu plikiem ZIP z innym rozszerzeniem. Możesz również przeanalizować zawartość pakietu, a następnie zmienić `.nupkg` ją `.zip`na, ale pamiętaj, aby przywrócić rozszerzenie przed przekazaniem pakietu do NuGet.org.

Aby udostępnić pakiet innym deweloperom, postępuj zgodnie z instrukcjami dotyczącymi [publikowania pakietu](../nuget-org/publish-a-package.md).

Należy pamiętać `pack` , że wymaga mono 4.4.2 w Mac OS X i nie działa w systemach Linux. Na komputerze Mac należy również skonwertować nazwy ścieżek systemu Windows w `.nuspec` pliku na ścieżki w stylu systemu UNIX.

## <a name="related-topics"></a>Tematy pokrewne

- [nuspec — odwołanie](../reference/nuspec.md)
- [Obsługa wielu wersji programu .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Uwzględnij w pakiecie narzędzia i elementy docelowe programu MSBuild](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
- [Pakiety symboli](../create-packages/symbol-packages.md)
- [Przechowywanie wersji pakietów](../concepts/package-versioning.md)
- [Dokumentacja biblioteki .NET Standard](/dotnet/articles/standard/library)
- [Przenoszenie do programu .NET Core z .NET Framework](/dotnet/articles/core/porting/index)
