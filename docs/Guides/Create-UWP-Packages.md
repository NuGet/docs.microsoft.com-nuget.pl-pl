---
title: Tworzenie pakietów NuGet dla platformy uniwersalnej systemu Windows | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/21/2017
ms.topic: tutorial
ms.prod: nuget
ms.technology: ''
description: End-to-end Przewodnik tworzenia pakietów NuGet dla platformy uniwersalnej systemu Windows przy użyciu składnika środowiska wykonawczego systemu Windows.
keywords: Utwórz pakiet, pakietów dla platformy uniwersalnej systemu Windows, składników środowiska wykonawczego systemu Windows
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 6923cdc87b0a550abb51316e384c79137eeaf63a
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="create-uwp-packages"></a>Tworzenie pakietów platformy uniwersalnej systemu Windows

[Windows platformy Uniwersalnej](https://developer.microsoft.com/windows) zapewnia platformę aplikacji wspólne dla wszystkich urządzeń z systemem Windows 10. W tym modelu aplikacji platformy uniwersalnej systemu Windows można wywołać zarówno WinRT interfejsów API, które są wspólne dla wszystkich urządzeń, a także interfejsów API (w tym Win32 i .NET), które są specyficzne dla rodziny urządzeń, na którym jest uruchomiona aplikacja.

W tym przewodniku tworzenia pakietu NuGet z natywnego platformy uniwersalnej systemu Windows składnika (w tym formancie XAML) używanego w zarządzanego i natywnego projektów.

## <a name="prerequisites"></a>Wymagania wstępne

1. 2017 usługi Visual Studio lub Visual Studio 2015. Bezpłatnie zainstalować 2017 Community edition z [visualstudio.com](https://www.visualstudio.com/); można także wersje Professional i Enterprise.

1. Interfejs wiersza polecenia NuGet. Pobierz najnowszą wersję `nuget.exe` z [nuget.org/downloads](https://nuget.org/downloads), zapisać go do wybranej lokalizacji (pobierania `.exe` bezpośrednio). Dodać tej lokalizacji do Twojej zmiennej środowiskowej PATH, gdy nie jest jeszcze.

## <a name="create-a-uwp-windows-runtime-component"></a>Tworzenie składnika środowiska wykonawczego systemu Windows platformy uniwersalnej systemu Windows

1. W programie Visual Studio, wybierz **Plik > Nowy > projektu**, rozwiń węzeł **Visual C++ > Windows > uniwersalnych** węzła, wybierz opcję **składnika środowiska wykonawczego systemu Windows (uniwersalny system Windows)**szablonu, Zmień nazwę na ImageEnhancer, a następnie kliknij przycisk OK. Zaakceptuj wartości domyślne dla wersji docelowej i minimalna wersja po wyświetleniu monitu.

    ![Tworzenie nowego projektu składnika środowiska wykonawczego systemu Windows platformy uniwersalnej systemu Windows](media/UWP-NewProject.png)

1. Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań wybierz **Dodaj > Nowy element**, kliknij przycisk **Visual C++ > XAML** węzła, wybierz opcję **kontrolki z szablonem**, Zmień nazwę, aby AwesomeImageControl.cpp, a następnie kliknij przycisk **Dodaj**:

    ![Dodawanie nowego elementu opartego na szablonie kontrolki XAML do projektu](media/UWP-NewXAMLControl.png)

1. Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań i wybierz **właściwości.** Na stronie właściwości rozwiń **właściwości konfiguracji > C/C++** i kliknij przycisk **pliki wyjściowe**. W okienku po prawej stronie Zmień wartość atrybutu **generować pliki dokumentacji XML** tak:

    ![Ustawienia Generuj pliki dokumentacji XML tak.](media/UWP-GenerateXMLDocFiles.png)

1. Kliknij prawym przyciskiem myszy *rozwiązania* teraz, wybierz **tworzenia partii**, sprawdź trzy pola debugowania w oknie dialogowym, jak pokazano poniżej. Dzięki temu się upewnić, że w po wykonaniu kompilacji wygenerować pełny zestaw artefaktów dla poszczególnych systemów docelowych, obsługiwanych przez usługę systemu Windows.

    ![Wsadowe kompilacji](media/UWP-BatchBuild.png)

1. W zadaniu wsadowym Tworzenie okna dialogowego, a następnie kliknij przycisk **kompilacji** Sprawdź projektu i tworzenia plików wyjściowych wymagające pakietu NuGet.

> [!Note]
> W tym przewodniku używasz artefakty debugowania dla pakietu. Dla pakietu bez debugowania zamiast tego Sprawdź opcje wersji w oknie dialogowym Tworzenie partii i zapoznaj się wynikowy folderów wersji w kolejnych krokach.

## <a name="create-and-update-the-nuspec-file"></a>Tworzenie i aktualizowanie pliku .nuspec

Aby utworzyć pierwszy `.nuspec` plików, wykonaj poniższe trzy kroki. Sekcje, które należy wykonać, a następnie przedstawiono inne niezbędne aktualizacje.

1. Otwórz wiersz polecenia i przejdź do folderu zawierającego `ImageEnhancer.vcxproj` (są to podfolder poniżej, gdzie to plik rozwiązania).
1. Uruchom NuGet `spec` polecenie, aby wygenerować `ImageEnhancer.nuspec` (nazwa pliku jest pobierana z nazwy `.vcxproj` plików):

    ```cli
    nuget spec
    ```

1. Otwórz `ImageEnhancer.nuspec` w edytorze i zaktualizować je zgodnie z poniższym, zamieniając twoje_imie odpowiednią wartość. `<id>` Wartość, w szczególności musi być unikatowa w nuget.org (konwencje nazewnictwa opisane w temacie [utworzenie pakietu](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)). Należy również zauważyć, że należy również zaktualizować tagi autora oraz opis lub wystąpi błąd podczas wykonywania kroku pakowania.

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
> Skompilowany dla publicznych zużycia pakietów, należy zwrócić szczególną uwagę na `<tags>` element, jak te znaczniki ułatwiała innym pakietu odnaleźć i zrozumieć, jakie operacje.

### <a name="adding-windows-metadata-to-the-package"></a>Dodawanie metadanych systemu Windows do pakietu

Składnik środowiska uruchomieniowego systemu Windows wymaga metadanych, które opisują wszystkich typów publicznie dostępnych, co umożliwia dla innych aplikacji i bibliotek użycie składnika. Te metadane znajduje się w pliku winmd, który jest tworzony podczas kompilowania projektu i muszą być zawarte w pakiecie NuGet. Plik XML z danymi IntelliSense jest również zbudowana w tym samym czasie i powinna być również uwzględnione.

Dodaj następujące `<files>` węzeł `.nuspec` pliku:

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

Aby uwzględnić XAML formantu o składnika, należy dodać pliku XAML, który ma szablonu domyślnego dla formantu (wygenerowane przez szablon projektu). Może to również przechodzi `<files>` sekcji:

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

### <a name="adding-the-native-implementation-libraries"></a>Dodawanie bibliotek implementacji natywnej

W ramach składnika, logiki core typu ImageEnhancer jest w kodzie natywnym, który znajduje się w różnych `ImageEnhancer.dll` zestawy, które są generowane dla poszczególnych docelowych runtime (x 86 i x64 ARM). Aby uwzględnić je w pakiecie, odwoływać je w `<files>` sekcji wraz z ich plików zasobów .pri skojarzone:

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

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a>Dodawanie .targets

Następnie projektów C++ i JavaScript, które mogą korzystać z pakietu NuGet muszą pliku .targets w celu identyfikowania niezbędne pliki zestawu i winmd. (C# i Visual Basic, projekty w tym automatycznie.) Utwórz ten plik przez skopiowanie poniższy tekst do `ImageEnhancer.targets` i zapisz go w tym samym folderze co `.nuspec` pliku. _Uwaga_: to `.targets` pliku musi mieć taką samą nazwę jak identyfikator pakietu (np. `<Id>` element `.nupspec` pliku):

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

Następnie można znaleźć `ImageEnhancer.targets` w Twojej `.nuspec` pliku:

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

Twoje final `.nuspec` pliku powinna wyglądać podobnie do następującego: gdzie ponownie twoje_imie należy zamienić na odpowiednie wartości:

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

Z ukończonej `.nuspec` odwołuje się do wszystkich plików, które należy uwzględnić w pakiecie, wszystko jest gotowe do uruchomienia `pack` polecenia:

```cli
nuget pack ImageEnhancer.nuspec
```

Spowoduje to wygenerowanie `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`. Otwarcie tego pliku w narzędzia, takiego jak [Explorer pakietu NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzanie wszystkich węzłów, zobacz następującą zawartość:

![Wyświetlanie pakietu ImageEnhancer Explorer pakietu NuGet](media/UWP-PackageExplorer.png)

> [!Tip]
> A `.nupkg` plik jest tylko plik ZIP zawierający inne rozszerzenie. Można również sprawdzić zawartość pakietu, następnie zmieniając `.nupkg` do `.zip`, ale pamiętaj, aby przywrócić rozszerzenia przed przekazaniem do nuget.org pakietu.

Aby udostępnić pakietu inni deweloperzy, postępuj zgodnie z instrukcjami [opublikowania pakietu](../create-packages/publish-a-package.md).

## <a name="related-topics"></a>Tematy pokrewne

- [odwołanie .nuspec](../reference/nuspec.md)
- [Pakiety symboli](../create-packages/symbol-packages.md)
- [Przechowywanie wersji pakietów](../reference/package-versioning.md)
- [Obsługa wielu wersje programu .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Zawiera właściwości programu MSBuild i obiektów docelowych w pakiecie](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
