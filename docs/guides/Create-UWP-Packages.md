---
title: Utwórz pakiety NuGet dla platforma uniwersalna systemu Windows
description: Kompleksowy przewodnik tworzenia pakietów NuGet przy użyciu składnika środowisko wykonawcze systemu Windows dla platforma uniwersalna systemu Windows.
author: karann-msft
ms.author: karann
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: 1683349faacdf5ad47baafeef3457bbb3bb1baa9
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488993"
---
# <a name="create-uwp-packages"></a>Tworzenie pakietów platformy UWP

[Platforma uniwersalna systemu Windows (platformy UWP)](https://developer.microsoft.com/windows) zapewnia wspólną platformę aplikacji dla każdego urządzenia z systemem Windows 10. W ramach tego modelu aplikacje platformy UWP mogą wywoływać oba interfejsy API WinRT, które są wspólne dla wszystkich urządzeń, a także interfejsy API (w tym Win32 i .NET), które są specyficzne dla rodziny urządzeń, na których działa aplikacja.

W tym instruktażu utworzysz pakiet NuGet z natywnym składnikiem platformy UWP (łącznie z kontrolką XAML), który może być używany w projektach zarządzanych i natywnych.

## <a name="prerequisites"></a>Wymagania wstępne

1. Visual Studio 2017 lub Visual Studio 2015. Zainstaluj bezpłatnie wersję 2017 Community z [VisualStudio.com](https://www.visualstudio.com/); można również używać wersji Professional i Enterprise.

1. Interfejs wiersza polecenia NuGet. Pobierz najnowszą wersję `nuget.exe` z [NuGet.org/downloads](https://nuget.org/downloads), zapisując ją w wybranej lokalizacji (pobieranie jest `.exe` bezpośrednie). Następnie Dodaj tę lokalizację do zmiennej środowiskowej PATH, jeśli nie została jeszcze.

## <a name="create-a-uwp-windows-runtime-component"></a>Utwórz składnik środowisko wykonawcze systemu Windows platformy UWP

1. W programie Visual Studio wybierz kolejno opcje **plik > nowy > projekt**, rozwiń węzeł **Visual C++ > Windows > uniwersalny** , wybierz szablon **składnik środowisko wykonawcze systemu Windows (uniwersalny system Windows)** , Zmień nazwę na ImageEnhancer, a następnie kliknij przycisk OK. Po wyświetleniu monitu zaakceptuj wartości domyślne wersji docelowej i wersji minimalnej.

    ![Tworzenie nowego projektu składnika środowisko wykonawcze systemu Windows platformy UWP](media/UWP-NewProject.png)

1. Kliknij prawym przyciskiem myszy projekt w Eksplorator rozwiązań, wybierz pozycję **dodaj > nowy element**, kliknij węzeł **Visual C++ > XAML** , wybierz opcję **formant**z szablonem, Zmień nazwę na AwesomeImageControl. cpp, a następnie kliknij przycisk **Dodaj**:

    ![Dodawanie nowego elementu formantu XAML z szablonem do projektu](media/UWP-NewXAMLControl.png)

1. Kliknij prawym przyciskiem myszy projekt w Eksplorator rozwiązań i wybierz polecenie **właściwości.** Na stronie właściwości rozwiń węzeł **Właściwości konfiguracji > CC++ /** i kliknij pozycję **pliki wyjściowe**. W okienku po prawej stronie Zmień wartość opcji **Generuj pliki dokumentacji XML** na tak:

    ![Ustawienie Generuj pliki dokumentacji XML na tak](media/UWP-GenerateXMLDocFiles.png)

1. Kliknij teraz *rozwiązanie* prawym przyciskiem myszy, wybierz pozycję **kompilacja wsadowa**, a następnie sprawdź trzy pola debugowania w oknie dialogowym, jak pokazano poniżej. Daje to pewność, że po wykonaniu kompilacji zostanie wygenerowany pełen zestaw artefaktów dla każdego systemu docelowego obsługiwanego przez system Windows.

    ![Kompilacja wsadowa](media/UWP-BatchBuild.png)

1. W oknie dialogowym kompilacja wsadowa, a następnie kliknij przycisk **Kompiluj** , aby zweryfikować projekt i utworzyć pliki wyjściowe potrzebne dla pakietu NuGet.

> [!Note]
> W tym instruktażu użyjesz artefaktów debugowania dla pakietu. W przypadku pakietu bez debugowania Sprawdź opcje wydania w oknie dialogowym kompilacja wsadowa, a następnie zapoznaj się z folderem wydania w poniższej procedurze.

## <a name="create-and-update-the-nuspec-file"></a>Utwórz i zaktualizuj plik. nuspec

Aby utworzyć początkowy `.nuspec` plik, wykonaj trzy poniższe czynności. Poniższe sekcje przeprowadzą Cię przez inne niezbędne aktualizacje.

1. Otwórz wiersz polecenia i przejdź do folderu zawierającego `ImageEnhancer.vcxproj` (będzie to podfolder poniżej lokalizacji pliku rozwiązania).
1. Uruchom polecenie NuGet `spec` , aby wygenerować `ImageEnhancer.nuspec` (nazwa pliku jest pobierana `.vcxproj` z nazwy pliku):

    ```cli
    nuget spec
    ```

1. Otwórz `ImageEnhancer.nuspec` w edytorze i zaktualizuj go, aby pasował do następujących wartości, zastępując YOUR_NAME z odpowiednią wartością. Wartość, szczególnie, musi być unikatowa w obrębie NuGet.org (zobacz Konwencje nazewnictwa opisane w artykule [Tworzenie pakietu](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)). `<id>` Należy również pamiętać, że należy również zaktualizować Tagi autor i opis lub podczas kroku pakowania wystąpi błąd.

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
> W przypadku pakietów przeznaczonych do użycia publicznego należy zwrócić szczególną `<tags>` uwagę na element, ponieważ te Tagi ułatwiają innym znalezienie pakietu i zrozumienie jego działania.

### <a name="adding-windows-metadata-to-the-package"></a>Dodawanie metadanych systemu Windows do pakietu

Składnik środowisko wykonawcze systemu Windows wymaga metadanych, które opisują wszystkie dostępne publicznie typy, które umożliwiają korzystanie z składnika przez inne aplikacje i biblioteki. Te metadane są zawarte w pliku winmd, który jest tworzony podczas kompilowania projektu i musi być dołączony do pakietu NuGet. Plik XML z danymi IntelliSense jest również zbudowany w tym samym czasie i powinien być również dołączony.

Dodaj następujący `<files>` węzeł `.nuspec` do pliku:

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

Aby dołączyć kontrolkę XAML do składnika, należy dodać plik XAML, który ma szablon domyślny dla formantu (zgodnie z szablonem projektu). Jest `<files>` to również sekcja:

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

### <a name="adding-the-native-implementation-libraries"></a>Dodawanie natywnych bibliotek implementacji

W składniku podstawowa logika typu ImageEnhancer jest w kodzie natywnym, który jest zawarty w różnych `ImageEnhancer.dll` zestawach, które są generowane dla każdego docelowego środowiska uruchomieniowego (ARM, x86 i x64). Aby uwzględnić je w pakiecie, należy odwołać się do `<files>` nich w sekcji wraz ze skojarzonymi z nimi plikami zasobów. pri:

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

### <a name="adding-targets"></a>Dodawanie elementów docelowych

Następnie projekty C++ języka JavaScript, które mogą zużywać pakiet NuGet, potrzebują pliku. targets do identyfikowania niezbędnych zestawów i plików WinMD. (C# projekty Visual Basic są automatycznie.) Utwórz ten plik, kopiując poniższy tekst do `ImageEnhancer.targets` i Zapisz go w tym samym folderze, w którym znajduje `.nuspec` się plik. _Uwaga_: Ten `.targets` plik musi mieć taką samą nazwę jak identyfikator pakietu (np `<Id>` . element w `.nupspec` pliku):

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

Następnie zapoznaj `ImageEnhancer.targets` się z `.nuspec` plikiem w pliku:

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

### <a name="final-nuspec"></a>Final. nuspec

Końcowy `.nuspec` plik powinien teraz wyglądać podobnie do poniższego, gdzie YOUR_NAME należy zastąpić odpowiednią wartością:

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

## <a name="package-the-component"></a>Pakowanie składnika

Po zakończeniu `.nuspec` odwoływania się do wszystkich plików, które należy uwzględnić w pakiecie, możesz `pack` uruchomić polecenie:

```cli
nuget pack ImageEnhancer.nuspec
```

Spowoduje to `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`wygenerowanie. Otwierając ten plik w narzędziu, takim jak [Eksplorator pakietów NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzając wszystkie węzły, zobaczysz następującą zawartość:

![Eksplorator pakietów NuGet przedstawiający pakiet ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> `.nupkg` Plik jest po prostu plikiem ZIP z innym rozszerzeniem. Możesz również przeanalizować zawartość pakietu, a następnie zmienić `.nupkg` ją `.zip`na, ale pamiętaj, aby przywrócić rozszerzenie przed przekazaniem pakietu do NuGet.org.

Aby udostępnić pakiet innym deweloperom, postępuj zgodnie z instrukcjami dotyczącymi [publikowania pakietu](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>Tematy pokrewne

- [nuspec — odwołanie](../reference/nuspec.md)
- [Pakiety symboli](../create-packages/symbol-packages.md)
- [Przechowywanie wersji pakietów](../concepts/package-versioning.md)
- [Obsługa wielu wersji .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Uwzględnij w pakiecie narzędzia i elementy docelowe programu MSBuild](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
