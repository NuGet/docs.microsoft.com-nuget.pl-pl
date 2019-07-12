---
title: Tworzenie pakietów NuGet dla platformy Universal Windows
description: End-to-end Przewodnik tworzenia pakietów NuGet dla platformy uniwersalnej Windows za pomocą składnika środowiska wykonawczego Windows.
author: karann-msft
ms.author: karann
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: 344c8d764180d0f33c1bce77b721e3657297e74e
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842122"
---
# <a name="create-uwp-packages"></a>Tworzenie pakietów platformy UWP

[Windows platformy Uniwersalnej](https://developer.microsoft.com/windows) udostępnia wspólną platformę aplikacji dla każdego urządzenia z systemem Windows 10. W tym modelu aplikacji platformy UWP może wywoływać zarówno interfejsów API WinRT, które są wspólne dla wszystkich urządzeń, a także interfejsów API (w tym Win32 i platformy .NET), które są specyficzne dla rodziny urządzeń, na którym działa aplikacja.

W tym przewodniku tworzenia pakietów NuGet za pomocą natywnego platformy uniwersalnej systemu Windows składnik (w tym kontrolki XAML) używanej w zarządzanych i natywnych projektów.

## <a name="prerequisites"></a>Wymagania wstępne

1. Program Visual Studio 2017 lub Visual Studio 2015. Zainstaluj 2017 Community edition bezpłatnie z [visualstudio.com](https://www.visualstudio.com/); można użyć również wersje Professional i Enterprise.

1. Interfejs wiersza polecenia NuGet. Pobierz najnowszą wersję `nuget.exe` z [nuget.org/downloads](https://nuget.org/downloads), zapisanie go do wybranej lokalizacji (pliki do pobrania jest `.exe` bezpośrednio). Następnie dodaj tej lokalizacji do zmiennej środowiskowej PATH, jeśli jeszcze tego nie zrobiono.

## <a name="create-a-uwp-windows-runtime-component"></a>Tworzenie składników środowiska wykonawczego Windows platformy uniwersalnej systemu Windows

1. W programie Visual Studio, wybierz **Plik > Nowy > Projekt**, rozwiń węzeł **Visual C++ > Windows > Universal** węzła, wybierz opcję **składnika środowiska wykonawczego Windows (Windows Universal)** szablonu, Zmień nazwę na ImageEnhancer, a następnie kliknij przycisk OK. Zaakceptuj wartości domyślne dla wersji docelowej i wersję minimalną po wyświetleniu monitu.

    ![Tworzenie nowego projektu składnika wykonawczego Windows platformy uniwersalnej systemu Windows](media/UWP-NewProject.png)

1. Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań, wybierz pozycję **Dodaj > Nowy element**, kliknij przycisk **Visual C++ > XAML** węzeł **formant z szablonem**, Zmień nazwę na AwesomeImageControl.cpp, a następnie kliknij przycisk **Dodaj**:

    ![Dodawanie nowego elementu kontrolka z szablonem XAML do projektu](media/UWP-NewXAMLControl.png)

1. Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań i wybierz **właściwości.** Na stronie właściwości rozwiń węzeł **właściwości konfiguracji > C/C++** i kliknij przycisk **pliki wyjściowe**. W okienku po prawej stronie Zmień wartość **Generuj pliki dokumentacji XML** tak:

    ![Ustawienia Generuj pliki dokumentacji XML tak](media/UWP-GenerateXMLDocFiles.png)

1. Kliknij prawym przyciskiem myszy *rozwiązania* Wybierz teraz **tworzenie partii**, trzy pola debugowania w oknie dialogowym Sprawdź, jak pokazano poniżej. Dzięki temu po wykonaniu kompilacji wygenerować pełny zestaw artefaktów dla każdego z docelowych systemach, które obsługuje Windows.

    ![Kompilacji wsadowej](media/UWP-BatchBuild.png)

1. W zadaniu wsadowym Tworzenie okna dialogowego, a następnie kliknij przycisk **kompilacji** w celu sprawdzenia projektu i utworzyć pliki wyjściowe, które są potrzebne dla pakietu NuGet.

> [!Note]
> W tym przewodniku użyjesz artefaktów debugowania dla pakietu. Pakietu bez debugowania zamiast tego wybierz opcje wersji w oknie dialogowym Tworzenie usługi Batch i odwołać się do wynikowego folderów wydania w opisanych poniżej.

## <a name="create-and-update-the-nuspec-file"></a>Tworzenie i aktualizowanie pliku .nuspec

Aby utworzyć początkowy `.nuspec` plików, wykonaj następujące trzy kroki. Sekcje, które należy wykonać, a następnie prowadzi przez innych wymaganych aktualizacji.

1. Otwórz wiersz polecenia i przejdź do folderu zawierającego `ImageEnhancer.vcxproj` (będzie podfolder poniżej, gdzie jest to plik rozwiązania).
1. Uruchom rozszerzenie NuGet `spec` polecenie, aby wygenerować `ImageEnhancer.nuspec` (nazwa pliku jest pobierana z nazwy `.vcxproj` plików):

    ```cli
    nuget spec
    ```

1. Otwórz `ImageEnhancer.nuspec` w edytorze i zaktualizuj go zgodnie z poniższym, zamieniając twoja_nazwa odpowiednią wartość. `<id>` Wartość, w szczególności musi być unikatowa w witrynie nuget.org (konwencje nazewnictwa, opisane w temacie [Tworzenie pakietu](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)). Należy również zauważyć, że należy również zaktualizować autor i opis znaczników lub wystąpi błąd podczas wykonywania kroku pakowania.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>ImageEnhancer.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>ImageEnhancer</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome Image Enhancer</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> W przypadku pakietów utworzone do użytku publicznego należy zwrócić szczególną uwagę na `<tags>` elementu, jak te znaczniki pomóc innym odnaleźć pakietu i zrozumieć, co robi.

### <a name="adding-windows-metadata-to-the-package"></a>Dodanie metadanych Windows do pakietu

Składnik środowiska wykonawczego Windows wymaga metadane opisujące wszystkich typów publicznie dostępny, co umożliwia dla innych aplikacji i bibliotek korzystanie z komponentu. Te metadane są zawarte w pliku winmd, która jest tworzona podczas kompilowania projektu i muszą być zawarte w pakiecie NuGet. Plik XML z danymi IntelliSense jest również zbudowana w tym samym czasie i mają zostać uwzględnione również.

Dodaj następujący kod `<files>` węzeł `.nuspec` pliku:

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a>Dodawanie zawartości XAML

Aby dołączyć kontrolki XAML przy użyciu składnika, należy dodać plik XAML, którego szablonu domyślnego dla formantu (wygenerowane przez szablon projektu). Prowadzi to również `<files>` sekcji:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- XAML controls -->
        <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    </files>
</package>
```

### <a name="adding-the-native-implementation-libraries"></a>Dodawanie bibliotek natywnych implementacji

W ramach składnika, podstawowe zasady logiczne typu ImageEnhancer jest w kodzie natywnym, która jest zawarta w różnych `ImageEnhancer.dll` zestawów, które są generowane dla każdego docelowe środowisko uruchomieniowe (x 86 i x64 ARM). Aby uwzględnić je w pakiecie, odwoływać się do nich w `<files>` sekcji wraz z plikami zasobów .pri skojarzone:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- DLLs and resources -->
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>

        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a>Dodawanie .targets

Następnie projektów C++ i JavaScript, które może używać pakietu NuGet muszą pliku .targets w celu identyfikowania niezbędne pliki zestawu i winmd. (Projektów C# i Visual Basic to zrobić automatycznie.) Utwórz ten plik, kopiując poniższy tekst do `ImageEnhancer.targets` i zapisz go w tym samym folderze co `.nuspec` pliku. _Uwaga_: To `.targets` pliku musi mieć taką samą nazwę jak identyfikator pakietu (np. `<Id>` element `.nupspec` plików):

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <ImageEnhancer-Platform Condition="'$(Platform)' == 'Win32'">x86</ImageEnhancer-Platform>
        <ImageEnhancer-Platform Condition="'$(Platform)' != 'Win32'">$(Platform)</ImageEnhancer-Platform>
    </PropertyGroup>
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Reference Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\ImageEnhancer.winmd">
            <Implementation>ImageEnhancer.dll</Implementation>
        </Reference>
    <ReferenceCopyLocalPaths Include="$(MSBuildThisFileDirectory)..\..\runtimes\win10-$(ImageEnhancer-Platform)\native\ImageEnhancer.dll" />
    </ItemGroup>
</Project>
```

Następnie zapoznaj się `ImageEnhancer.targets` w swojej `.nuspec` pliku:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- .targets -->
        <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

### <a name="final-nuspec"></a>Końcowe .nuspec

Ostateczna `.nuspec` plik powinien teraz wyglądać podobnie do poniższego, gdzie ponownie twoja_nazwa należy zamienić na odpowiednie wartości:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>ImageEnhancer.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>ImageEnhancer</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome Image Enhancer</description>
    <releaseNotes>First Release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- DLLs and resources -->
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>     
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

## <a name="package-the-component"></a>Pakiet składnika

Za pomocą ukończoną `.nuspec` odwołuje się do wszystkich plików, które należy uwzględnić w pakiecie, wszystko jest gotowe do uruchomienia `pack` polecenia:

```cli
nuget pack ImageEnhancer.nuspec
```

Spowoduje to wygenerowanie `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`. Otwarcie tego pliku w narzędzia, takiego jak [Eksplorator pakietów NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzając wszystkie węzły, zobacz następującą zawartość:

![Wyświetlanie pakietu ImageEnhancer Eksplorator pakietów NuGet](media/UWP-PackageExplorer.png)

> [!Tip]
> A `.nupkg` plik jest po prostu plikiem ZIP z innym rozszerzeniem. Można także sprawdzić zawartość pakietu, następnie zmieniając `.nupkg` do `.zip`, ale należy pamiętać przywrócić rozszerzenia przed przekazaniem pakietu na stronie nuget.org.

Aby udostępnić pakietu innym deweloperom, postępuj zgodnie z instrukcjami [publikowanie pakietu](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>Tematy pokrewne

- [odwołanie .nuspec](../reference/nuspec.md)
- [Pakiety symboli](../create-packages/symbol-packages.md)
- [Przechowywanie wersji pakietów](../reference/package-versioning.md)
- [Obsługiwanie wielu wersji programu .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Zawiera właściwości programu MSBuild i obiektów docelowych w pakiecie](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
