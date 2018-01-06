---
title: "Tworzenie pakietów NuGet standardowe .NET z programem Visual Studio 2015 | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 29b3bceb-0f35-4cdd-bbc3-a04eb823164c
description: "Przewodnik end-to-end tworzenia pakietów NuGet programu .NET Standard przy użyciu narzędzia NuGet 3.x i programu Visual Studio 2015."
keywords: "Tworzenie pakietu, .NET Standard pakietów, .NET Standard tabeli mapowania"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e02888bf552997afe25e967f13e021e78e40d48d
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/05/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a>Utwórz pakiety .NET Standard z programem Visual Studio 2015

*Dotyczy NuGet 3.x. Zobacz [utworzyć .NET Standard pakiety z programu Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) do pracy z NuGet 4.x+.*

[Biblioteki standardowej .NET](/dotnet/articles/standard/library) jest formalną specyfikację interfejsów API architektury .NET mają być dostępne na wszystkich środowisk uruchomieniowych .NET, w związku z tym ustanawianie większej jednolitości w ekosystemie .NET. Standardowa biblioteka .NET definiuje zestaw uniform BCL (Biblioteka klasy podstawowej) interfejsów API dla wszystkich platform .NET zaimplementować, niezależnie od obciążenia. Go umożliwia deweloperom tworzenia PCLs, które będą używać dla wszystkich programów .NET, i zmniejsza Jeśli nie eliminuje dyrektywy kompilacja warunkowa specyficzne dla platformy w kodzie udostępnionego.

Ten przewodnik przeprowadzi Cię przez proces tworzenia pakietu nuget przeznaczonych dla platformy .NET Standard biblioteki 1.4. To będzie działać w .NET Framework 4.6.1, uniwersalnych systemu Windows 10 platformy .NET Core i Mono/Xamarin. Aby uzyskać więcej informacji, zobacz [.NET Standard tabeli mapowania](#net-standard-mapping-table) dalszej części tego tematu.

1. [Wymagania wstępne](#pre-requisites)
1. [Tworzenie projektu biblioteki klas](#create-the-class-library-project)
1. [Tworzenie i aktualizowanie pliku .nuspec](#create-and-update-the-nuspec-file)
1. [Pakiet składnika](#package-the-component)
1. [Dodatkowe opcje](#additional-options)
1. [.NET standard tabeli mapowania](#net-standard-mapping-table)
1. [Tematy pokrewne](#related-topics)


## <a name="pre-requisites"></a>Wymagania wstępne

1. Visual Studio 2015. Bezpłatnie zainstalować Community edition z [visualstudio.com](https://www.visualstudio.com/); oczywiście można również wersje Professional i Enterprise.
1. .NET core: Zainstaluj oprogramowanie .NET Core wraz z szablonów i innych narzędzi dla programu Visual Studio 2015 z [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).
1. Interfejs wiersza polecenia NuGet. Pobierz najnowszą wersję nuget.exe z [nuget.org/downloads](https://nuget.org/downloads), zapisać go do wybranej lokalizacji. Dodać tej lokalizacji do Twojej zmiennej środowiskowej PATH, gdy nie jest jeszcze.

> [!Note]
> nuget.exe to narzędzie interfejsu wiersza polecenia, nie Instalatora, dlatego należy Zapisz pobrany plik z przeglądarki, a jego uruchomieniem.



## <a name="create-the-class-library-project"></a>Tworzenie projektu biblioteki klas

1. W programie Visual Studio **Plik > Nowy > projektu**, rozwiń węzeł **Visual C# > Windows** węzła, wybierz opcję **biblioteki klas (przenośna)**, Zmień nazwę na AppLogger i kliknij przycisk OK.

    ![Tworzenie nowego projektu biblioteki klas](media/NetStandard-NewProject.png)

1. W **dodać przenośnej biblioteki klas** okno dialogowe zostanie wyświetlone, wybierz `.NET Framework 4.6` i `ASP.NET Core 1.0` opcje.
1. Kliknij prawym przyciskiem myszy `AppLogger (Portable)` w Eksploratorze rozwiązań wybierz **właściwości**, wybierz pozycję **biblioteki** , a następnie kliknij **docelowej platformy .NET Standard** w **Przeznaczonych dla** sekcji. Ten monit o potwierdzenie, po którym można wybrać `.NET Standard 1.4` z listy rozwijanej:

    ![Ustawienie docelowej platformy .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. Polecenie **kompilacji** Zmień **konfiguracji** do `Release`i pole wyboru dla **pliku dokumentacji XML**.
1. Dodaj swój kod do składnika, na przykład:

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log");
            }
        }
    }
    ```

1. Skompiluj projekt (przy użyciu konfiguracji Release) i sprawdź, czy biblioteka DLL, pliki XML są tworzone w folderze bin\Release.

## <a name="create-and-update-the-nuspec-file"></a>Tworzenie i aktualizowanie pliku .nuspec

1. Otwórz wiersz polecenia, przejdź do folderu zawierającego `AppLogg.csproj` folder (jeden poziom w dół where `.sln` pliku), i uruchom NuGet `spec` polecenie, aby utworzyć pierwszy `AppLogger.nuspec` pliku:

```
nuget spec
```

1. Otwórz `AppLogger.nuspec` w edytorze i zaktualizować je zgodnie z poniższym, zamieniając twoje_imie odpowiednią wartość. `<id>` Wartość, w szczególności musi być unikatowa w nuget.org (konwencje nazewnictwa opisane w temacie [utworzenie pakietu](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number). Należy również zauważyć, że należy również zaktualizować tagi autora oraz opis lub zostanie wyświetlony błąd podczas wykonywania kroku pakowania.

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
    <copyright>Copyright 2016 (c) Contoso Corporation. All rights reserved.</copyright>
    <tags>logger logging logs</tags>
    </metadata>
</package>
```

1. Dodaj zestawy odwołań `.nuspec` plików, to znaczy biblioteki DLL i pliku IntelliSense XML:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. Kliknij prawym przyciskiem myszy rozwiązanie, a następnie wybierz **Kompiluj rozwiązanie** do wygenerowania wszystkich plików w pakiecie.


## <a name="package-the-component"></a>Pakiet składnika

Z ukończonej `.nuspec` odwołuje się do wszystkich plików, które należy uwzględnić w pakiecie, wszystko jest gotowe do uruchomienia `pack` polecenia:

```
nuget pack AppLogger.nuspec
```

Spowoduje to wygenerowanie `AppLogger.YOUR_NAME.1.0.0.nupkg`. Otwarcie tego pliku w narzędzia, takiego jak [Explorer pakietu NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzanie wszystkich węzłów, zobaczysz następującą zawartość:

![Wyświetlanie pakietu AppLogger Explorer pakietu NuGet](media/NetStandard-PackageExplorer.png)

> [!Tip]
> A `.nupkg` plik jest tylko plik ZIP zawierający inne rozszerzenie. Można również sprawdzić zawartość pakietu, następnie zmieniając `.nupkg` do `.zip`, ale pamiętaj, aby przywrócić rozszerzenia przed przekazaniem do nuget.org pakietu.

Aby udostępnić pakietu inni deweloperzy, postępuj zgodnie z instrukcjami [opublikowania pakietu](../create-packages/publish-a-package.md).

Należy pamiętać, że `pack` wymaga Mono 4.4.2 w systemie Mac OS X i nie działa w systemach Linux. Na komputerze Mac, należy także przekonwertować nazwy ścieżek systemu Windows w `.nuspec` pliku do ścieżki typu Unix.

## <a name="additional-options"></a>Dodatkowe opcje

Poniższe sekcje przejdź do dodatkowe opcje tworzenia pakietu NuGet:

- [Deklarowanie zależności](#declaring-dependencies)
- [Obsługujący wiele platform docelowych](#supporting-multiple-target-frameworks)
- [Dodawanie elementów docelowych i właściwości dla programu MSBuild](#adding-targets-and-props-for-msbuild)
- [Tworzenie zlokalizowanych pakietów](#creating-localized-packages)
- [Dodawanie pliku readme](#adding-a-readme)

### <a name="declaring-dependencies"></a>Deklarowanie zależności

Jeśli jest zależne od innych pakietów NuGet, listy w `<dependencies>` element z `<group>` elementów. Na przykład aby zadeklarować zależność w NewtonSoft.Json 8.0.3 lub nowszym, należy dodać:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

Składnia *wersji* tutaj wskazuje, czy w wersji 8.0.3 lub nowszy jest dopuszczalne atrybutu. Aby określić inną wersję zakresów, zapoznaj się [wersji pakietu](../reference/package-versioning.md).

### <a name="supporting-multiple-target-frameworks"></a>Obsługujący wiele platform docelowych

Załóżmy, że chcesz korzystać z interfejsu API w .NET Framework 4.6.2, która nie jest dostępna w .NET Standard 1.4. Aby to zrobić, musisz najpierw upewnij się, że biblioteka jest kompilowany dla .NET 4.6.2 przy użyciu kompilacja warunkowa lub udostępnionych projektów. (W programie Visual Studio, możesz można utworzyć projekt NetCore, wiele sekcji framework dodać framework wyboru i późniejszego kompilowania.) Następnie można utworzyć pakietu przy użyciu prostego technika katalogu opartych na konwencjach pracy w następujący sposób:

1. W projekcie głównym folderu zawierającego Twojej `.nuspec` plików, Utwórz folder o nazwie `lib`.
1. Wewnątrz `lib`, tworzenie folderów na różnych platformach, które mają być obsługiwane:

        \lib
            \netstandard1.4
                \AppLogger.dll
            \net462
                \AppLogger.dll

1. W `.nuspec` plików, dodawanie `files` węźle `package` węzła i odwołują się do plików w `lib` przy użyciu symboli wieloznacznych. **Uwaga:** Token zamiany nie są obsługiwane z podejścia opartych na konwencjach katalog roboczy, aby je zastąpić wartości literałów:

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
        <files>
            <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. Utwórz pakiet ponownie, używając `nuget pack AppLogger.spec`.

Aby uzyskać więcej informacji na temat używania tej metody, zobacz [obsługi wielu wersje programu .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)

### <a name="adding-targets-and-props-for-msbuild"></a>Dodawanie elementów docelowych i właściwości dla programu MSBuild

W niektórych przypadkach można dodać elementów docelowych niestandardowej kompilacji lub właściwości w projektach używające pakietu, takie jak uruchomienie niestandardowego narzędzia lub procesu podczas kompilacji. Aby to zrobić, dodanie plików w `\build` folderu zgodnie z opisem w poniższych krokach. Podczas instalowania pakietu z plikami \build NuGet dodaje element programu MSBuild w pliku projektu wskazujące pliki .targets i .props.

> [!Note]
> Korzystając z `project.json`, elementy docelowe nie zostaną dodane do projektu, ale są udostępniane za pośrednictwem `project.lock.json`.


1. W projekcie folder zawierający Twoje `.nuspec` plików, Utwórz folder o nazwie `build`.
1. Wewnątrz `build`, tworzenie folderów dla każdego obsługiwane i umieść w obrębie tych sieci `.targets` i `.props` plików:

        \build
            \netstandard1.4
                \AppLogger.props
                \AppLogger.targets
            \net462
                \AppLogger.props
                \AppLogger.targets

1. W `.nuspec` plików, dodawanie `files` węźle `package` węzła i odwołują się do plików w `build` przy użyciu symboli wieloznacznych.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>...
        </metadata>
        <files>
            <file src="build\**" target="build" />
        </files>
    </package>
    ```

1. Utwórz pakiet ponownie, używając `nuget pack AppLogger.nuspec`.

Aby uzyskać więcej informacji, zapoznaj się [właściwości MSBuild obejmują i obiektów docelowych w pakiecie](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).


### <a name="creating-localized-packages"></a>Tworzenie zlokalizowanych pakietów

Aby utworzyć zlokalizowane wersje biblioteki, można utworzyć oddzielne pakiety dla innych języków lub zawierają zestawy zlokalizowanych zasobów w jednym pakiecie. Oto jak to zrobić to drugie podejście, niemieckim i hiszpańskim:

1. W ramach każdej docelowej framework folderze `lib`, tworzyć foldery dla każdego z obsługiwanych języków innych niż domyślne angielskiej wersji językowej. W tych folderach można umieścić zestawy zasobów i zlokalizowanych plików IntelliSense XML. Na przykład:

        lib
        ├───netstandard1.4
        │   │   AppLogger.dll
        │   │   AppLogger.xml
        │   │
        │   ├───de
        │   │       AppLogger.resources.dll
        │   │       AppLogger.xml
        │   │
        │   └───it
        │           AppLogger.resources.dll
        │           AppLogger.xml
        └───net462
            │   AppLogger.dll
            │   AppLogger.xml
            │
            ├───de
            │       AppLogger.resources.dll
            │       AppLogger.xml
            │
            └───it
                    AppLogger.resources.dll
                    AppLogger.xml

1. W `.nuspec` plików, odwołania tych plików w `<files>` węzła:

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>...
        </metadata>
        <files>
        <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. Utwórz pakiet ponownie, używając `nuget pack AppLogger.nuspec`.


### <a name="adding-a-readme"></a>Dodawanie pliku readme

Jeśli dołączysz `readme.txt` w katalogu głównym pakietu Visual Studio zostanie wyświetlona po zainstalowaniu pakietu bezpośrednio.

> [!Note]
> Pliki Readme nie są wyświetlane pakiety, które są zainstalowane jako zależność lub .NET Core projektów.


W tym celu należy utworzyć użytkownika `readme.txt` pliku, umieść go w folderze głównym projektu i odwołuje się do niego w `.nuspec` pliku:

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


## <a name="net-standard-mapping-table"></a>.NET standard tabeli mapowania

|Nazwa platformy |Alias|
|--------------|-----|
|.NET standard | krótkich nazw netstandard| 1.0| 1.1| 1.2| 1.3| 1.4| 1.5| 1.6|
|.NET Core | netcoreapp| & #x 2192;| & #x 2192;| & #x 2192;| & #x 2192;| & #x 2192;| & #x 2192;| 1.0|
|.NET Framework| NET| 4.5| 4.5.1| 4.6| 4.6.1| 4.6.2| 4.6.3|
|Platformy mono/Xamarin| & #x 2192;| & #x 2192;| & #x 2192;| & #x 2192;| & #x 2192;| & #x 2192;|
|Platforma uniwersalna systemu Windows| uap| & #x 2192;| & #x 2192;| & #x 2192;| & #x 2192;|10.0|
|Windows| win| & #x 2192;| 8.0| 8.1|
|Windows Phone| WPA| & #x 2192;| & #x 2192;|8.1|
|Windows Phone Silverlight| WP| 8.0|



## <a name="related-topics"></a>Tematy pokrewne

- [Plik Nuspec odwołania](../schema/nuspec.md)
- [Pakiety symboli](../create-packages/symbol-packages.md)
- [Przechowywanie wersji pakietu](../reference/package-versioning.md)
- [Obsługa wielu wersje programu .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Zawiera właściwości programu MSBuild i obiektów docelowych w pakiecie](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
- [Dokumentacja biblioteki standardowej .NET](/dotnet/articles/standard/library)
- [Eksportowanie do platformy .NET Core z .NET Framework](/dotnet/articles/core/porting/index)
