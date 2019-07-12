---
title: Tworzenie .NET Standard i pakiety NuGet programu .NET Framework przy użyciu programu Visual Studio 2015
description: End-to-end Przewodnik tworzenia pakietów .NET Standard i NuGet programu .NET Framework za pomocą narzędzia NuGet 3.x, a program Visual Studio 2015.
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: 1198a781543e581f55740cc0ae5a212d3f8a8b61
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842443"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a>Tworzenie pakietów .NET Standard i .NET Framework w programie Visual Studio 2015

**Uwaga:** Program Visual Studio 2017, zaleca się do tworzenia biblioteki .NET Standard. Program Visual Studio 2015 można pracować, ale zestaw narzędzi .NET Core została udostępniona tylko do stanu (wersja zapoznawcza). Zobacz [tworzenie i publikowanie pakietu programu Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) do pracy z NuGet 4.x+ i programu Visual Studio 2017.

[Biblioteka .NET Standard](/dotnet/articles/standard/library) jest formalną specyfikację interfejsów API platformy .NET, które mają być dostępne na wszystkie środowiska uruchomieniowe platformy .NET, dlatego ustanawiania większej jednolitości należący do ekosystemu platformy .NET. Biblioteka .NET Standard definiuje zbiór jednolitych BCL (Biblioteka klasy podstawowej) interfejsów API dla wszystkich platform .NET zaimplementować, niezależnie od obciążenia. Umożliwia ona deweloperom tworzenia kodu, które są wykorzystywane przez wszystkie środowiska uruchomieniowe platformy .NET i zmniejsza, jeśli nie eliminuje dyrektywy kompilacji warunkowej specyficzne dla platformy w udostępnionego kodu.

Ten przewodnik przeprowadzi Cię przez tworzenie pakietu NuGet określanie wartości docelowej platformy .NET Standard 1.4 biblioteki lub pakietu przeznaczonych dla platformy .NET Framework 4.6. Biblioteki .NET Standard 1.4 działa w .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core i platformy Mono/Xamarin. Aby uzyskać więcej informacji, zobacz [.NET Standard tabeli mapowania](/dotnet/standard/net-standard#net-implementation-support) (dokumentacja platformy .NET). Druga wersja biblioteka .NET Standard można wybrać, jeśli chcesz.

## <a name="prerequisites"></a>Wymagania wstępne

1. Visual Studio 2015 Update 3
1. (Tylko .NET standard) [Platformy .NET core SDK](https://www.microsoft.com/net/download/)
1. Interfejs wiersza polecenia NuGet. Pobierz najnowszą wersję programu nuget.exe z [nuget.org/downloads](https://nuget.org/downloads), zapisanie go do wybranej lokalizacji. Następnie dodaj tej lokalizacji do zmiennej środowiskowej PATH, jeśli jeszcze tego nie zrobiono.

    > [!Note]
    > nuget.exe to narzędzie interfejsu wiersza polecenia, nie Instalatora, więc Pamiętaj zapisać pobrany plik z przeglądarki, zamiast uruchamiać go.

## <a name="create-the-class-library-project"></a>Utwórz projekt biblioteki klas

1. W programie Visual Studio **Plik > Nowy > Projekt**, rozwiń węzeł **Visual C# > Windows** węzła, wybierz opcję **Biblioteka klas (przenośna)** , Zmień nazwę na AppLogger i wybierz **OK**.

    ![Utwórz nowy projekt biblioteki klas](media/NetStandard-NewProject.png)

1. W **Dodaj Portable Class Library** wyświetlonym oknie dialogowym Wybierz opcje dla `.NET Framework 4.6` i `ASP.NET Core 1.0`. (Jeśli przeznaczony dla .NET Framework, możesz wybrać jednego z tych opcji są odpowiednie.)

1. Przeznaczonych dla platformy .NET Standard, kliknij prawym przyciskiem myszy `AppLogger (Portable)` w Eksploratorze rozwiązań wybierz **właściwości**, wybierz opcję **biblioteki** kartę, a następnie wybierz **docelowej platformy .NET Standard** w **Ustawianie elementów docelowych** sekcji. Ta akcja monituje o potwierdzenie, po którym można wybrać `.NET Standard 1.4` (lub inna wersja dostępna) z listy rozwijanej:

    ![Ustawienia obiektu docelowego .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. Kliknij pozycję **kompilacji** kartę, zmień **konfiguracji** do `Release`i pole wyboru dla **pliku dokumentacji XML**.

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

1. Ustaw konfigurację do wersji, skompiluj projekt i sprawdź, czy biblioteka DLL, pliki XML są tworzone w ramach `bin\Release` folderu.

## <a name="create-and-update-the-nuspec-file"></a>Tworzenie i aktualizowanie pliku .nuspec

1. Otwórz wiersz polecenia, przejdź do folderu zawierającego `AppLogger.csproj` folder (jeden poziom poniżej miejsca `.sln` plik jest), i Uruchom rozszerzenie NuGet `spec` polecenie, aby utworzyć początkowy `AppLogger.nuspec` pliku:

    ```cli
    nuget spec
    ```

1. Otwórz `AppLogger.nuspec` w edytorze i zaktualizuj go zgodnie z poniższym, zamieniając twoja_nazwa odpowiednią wartość. `<id>` Wartość, w szczególności musi być unikatowa w witrynie nuget.org (konwencje nazewnictwa, opisane w temacie [Tworzenie pakietu](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number). Należy również zauważyć, że należy również zaktualizować autor i opis znaczników lub wystąpi błąd podczas wykonywania kroku pakowania.

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

1. Dodaj zestawy referencyjne do `.nuspec` pliku, a mianowicie biblioteki DLL i pliku IntelliSense XML:

    Jeśli przeznaczonych dla platformy .NET Standard, wpisy zostaną wyświetlone podobne do następujących:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    Jeśli przeznaczony dla .NET Framework, wpisy zostaną wyświetlone podobne do następujących:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. Kliknij prawym przyciskiem myszy rozwiązanie, a następnie wybierz pozycję **Kompiluj rozwiązanie** wygenerować pliki pakietu.

### <a name="declaring-dependencies"></a>Deklarowanie zależności

Jeśli masz jakieś zależności, w innych pakietach NuGet listy w manifeście `<dependencies>` element z `<group>` elementów. Na przykład, aby zadeklarować zależność w NewtonSoft.Json 8.0.3 lub nowszej, Dodaj następujący kod:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

Składnia *wersji* atrybut wskazuje, w tym miejscu tę wersję 8.0.3 lub powyżej jest dopuszczalna. Aby określić zakresy innej wersji, zapoznaj się [przechowywanie wersji pakietów](../reference/package-versioning.md).

### <a name="adding-a-readme"></a>Dodawanie pliku readme

Utwórz swoje `readme.txt` pliku, umieść go w folderze głównym projektu i odwoływać się do niego w `.nuspec` pliku:

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

Visual Studio wyświetlanie `readme.txt` po zainstalowaniu pakietu do projektu. Plik nie jest wyświetlany, gdy zainstalowane w projektach .NET Core lub pakietów, które są zainstalowane jako zależność.

## <a name="package-the-component"></a>Pakiet składnika

Za pomocą ukończoną `.nuspec` odwołuje się do wszystkich plików, które należy uwzględnić w pakiecie, wszystko jest gotowe do uruchomienia `pack` polecenia:

```cli
nuget pack AppLogger.nuspec
```

Spowoduje to wygenerowanie `AppLogger.YOUR_NAME.1.0.0.nupkg`. Otwarcie tego pliku w narzędzia, takiego jak [Eksplorator pakietów NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzając wszystkie węzły, zobacz następującą zawartość (wyświetlana dla platformy .NET Standard):

![Wyświetlanie pakietu AppLogger Eksplorator pakietów NuGet](media/NetStandard-PackageExplorer.png)

> [!Tip]
> A `.nupkg` plik jest po prostu plikiem ZIP z innym rozszerzeniem. Można także sprawdzić zawartość pakietu, następnie zmieniając `.nupkg` do `.zip`, ale należy pamiętać przywrócić rozszerzenia przed przekazaniem pakietu na stronie nuget.org.

Aby udostępnić pakietu innym deweloperom, postępuj zgodnie z instrukcjami [publikowanie pakietu](../nuget-org/publish-a-package.md).

Należy pamiętać, że `pack` wymaga platformy Mono 4.4.2 w systemie Mac OS X, a nie działa w systemach Linux. Na komputerze Mac, należy także przekonwertować nazwy Windows ścieżek w `.nuspec` plik do ścieżki stylu systemu Unix.

## <a name="related-topics"></a>Tematy pokrewne

- [odwołanie .nuspec](../reference/nuspec.md)
- [Obsługiwanie wielu wersji programu .NET framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Zawiera właściwości programu MSBuild i obiektów docelowych w pakiecie](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
- [Pakiety symboli](../create-packages/symbol-packages.md)
- [Przechowywanie wersji pakietów](../reference/package-versioning.md)
- [Dokumentacja .NET biblioteki standardowej](/dotnet/articles/standard/library)
- [Eksportowanie do programu .NET Core z .NET Framework](/dotnet/articles/core/porting/index)
