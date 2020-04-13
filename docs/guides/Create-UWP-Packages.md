---
title: Tworzenie pakietów NuGet dla uniwersalnej platformy systemu Windows
description: End-to-end instruktaż tworzenia pakietów NuGet przy użyciu składnika środowiska wykonawczego systemu Windows dla platformy uniwersalnego systemu Windows.
author: karann-msft
ms.author: karann
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: 77aa186291122a8d05018ecacd1329da459badad
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380764"
---
# <a name="create-uwp-packages"></a>Tworzenie pakietów platformy UWP

[Platforma uniwersalna systemu Windows (UWP)](https://developer.microsoft.com/windows) zapewnia wspólną platformę aplikacji dla każdego urządzenia z systemem Windows 10. W ramach tego modelu aplikacje platformy uniwersalnej systemu Windows mogą wywoływać zarówno interfejsy API platformy WinRT, które są wspólne dla wszystkich urządzeń, jak i interfejsy API (w tym Win32 i .NET), które są specyficzne dla rodziny urządzeń, na których jest uruchomiona aplikacja.

W tym instruktażu można utworzyć pakiet NuGet z natywnego składnika platformy uniwersalnej systemu Uniwersalnego (w tym kontrolki XAML), który może być używany zarówno w projektach zarządzanych i natywnych.

## <a name="prerequisites"></a>Wymagania wstępne

1. Visual Studio 2017 lub Visual Studio 2015. Zainstaluj edycję społeczności 2017 bezpłatnie od [visualstudio.com;](https://www.visualstudio.com/) można również korzystać z wersji Professional i Enterprise.

1. Funkcja Interfejsu wiersza polecenia NuGet. Pobierz najnowszą `nuget.exe` wersję z [nuget.org/downloads](https://nuget.org/downloads), zapisując ją w wybranej lokalizacji `.exe` (pobieranie jest bezpośrednio). Następnie dodaj tę lokalizację do zmiennej środowiskowej PATH, jeśli jeszcze jej nie ma.

## <a name="create-a-uwp-windows-runtime-component"></a>Tworzenie składnika środowiska wykonawczego systemu Windows platformy uniwersalnej systemu Windows

1. W programie Visual Studio wybierz polecenie **Plik > nowy projekt >**, rozwiń węzeł Visual **C++ > Windows > uniwersalny,** wybierz szablon **Składnika Wykonawczego systemu Windows (Uniwersalny Windows),** zmień nazwę na ImageEnhancer i kliknij przycisk OK. Po wyświetleniu monitu zaakceptuj wartości domyślne dla wersji docelowej i wersji minimalnej.

    ![Tworzenie nowego projektu składnika środowiska wykonawczego systemu Windows platformy uniwersalnej systemu Windows](media/UWP-NewProject.png)

1. Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań, wybierz pozycję **Dodaj > nowy element**, kliknij węzeł Visual **C++ > XAML,** wybierz pozycję **Formant szablonu,** zmień nazwę na AwesomeImageControl.cpp i kliknij przycisk **Dodaj:**

    ![Dodawanie nowego elementu formantu szablonu XAML do projektu](media/UWP-NewXAMLControl.png)

1. Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań i wybierz **polecenie Właściwości.** Na stronie Właściwości rozwiń pozycję **Właściwości konfiguracji > C/C++** i kliknij pozycję **Pliki wyjściowe**. W okienku po prawej stronie zmień wartość **generowania plików dokumentacji XML** na Tak:

    ![Ustawienie Generowanie plików dokumentacji XML na Tak](media/UWP-GenerateXMLDocFiles.png)

1. Kliknij prawym przyciskiem myszy *rozwiązanie* teraz, wybierz **polecenie Kompilacja wsadowa**, zaznacz trzy pola debugowania w oknie dialogowym, jak pokazano poniżej. Dzięki temu podczas wykonywania kompilacji, można wygenerować pełny zestaw artefaktów dla każdego z systemów docelowych, które obsługuje system Windows.

    ![Kompilacja wsadowego](media/UWP-BatchBuild.png)

1. W oknie dialogowym Kompilacja wsadowa i kliknij przycisk **Buduj,** aby zweryfikować projekt i utworzyć pliki wyjściowe potrzebne dla pakietu NuGet.

> [!Note]
> W tym instruktażu należy użyć artefaktów debugowania dla pakietu. W przypadku pakietu nie debugowania sprawdź opcje wydania w oknie dialogowym kompilacji wsadowej i zapoznaj się z wynikowymi folderami release w kolejnych krokach.

## <a name="create-and-update-the-nuspec-file"></a>Tworzenie i aktualizowanie pliku nuspec

Aby utworzyć `.nuspec` plik początkowy, wykonaj trzy kroki poniżej. Sekcje, które następują, następnie poprowadzi Cię przez inne niezbędne aktualizacje.

1. Otwórz wiersz polecenia i przejdź do `ImageEnhancer.vcxproj` folderu zawierającego (będzie to podfolder poniżej, gdzie znajduje się plik rozwiązania).
1. Uruchom polecenie `spec` NuGet, `ImageEnhancer.nuspec` aby wygenerować (nazwa pliku `.vcxproj` pochodzi od nazwy pliku):

    ```cli
    nuget spec
    ```

1. Otwórz `ImageEnhancer.nuspec` w edytorze i zaktualizuj go, aby dopasować go do następujących, zastępując YOUR_NAME odpowiednią wartością. Wartość, `<id>` w szczególności, musi być unikatowa w nuget.org (zobacz konwencje nazewnictwa opisane w [Tworzenie pakietu](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)). Należy również pamiętać, że należy również zaktualizować tagi autora i opisu lub pojawi się błąd podczas kroku pakowania.

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
> W przypadku pakietów przeznaczonych do `<tags>` użytku publicznego należy zwrócić szczególną uwagę na element, ponieważ te tagi pomagają innym znaleźć pakiet i zrozumieć, co robi.

### <a name="adding-windows-metadata-to-the-package"></a>Dodawanie metadanych systemu Windows do pakietu

Składnik środowiska wykonawczego systemu Windows wymaga metadanych, które opisują wszystkie jego publicznie dostępne typy, co umożliwia innym aplikacjom i bibliotekom korzystanie ze składnika. Te metadane są zawarte w pliku .winmd, który jest tworzony podczas kompilowania projektu i musi być uwzględniony w pakiecie NuGet. Plik XML z danymi IntelliSense jest również zbudowany w tym samym czasie i powinien być również dołączony.

Dodaj do `<files>` `.nuspec` pliku następujący węzeł:

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

Aby dołączyć formant XAML do składnika, należy dodać plik XAML, który ma domyślny szablon formantu (wygenerowany przez szablon projektu). Dotyczy to również `<files>` sekcji:

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

W ramach składnika podstawowa logika imageenhancer typu jest w kodzie `ImageEnhancer.dll` macierzystym, który jest zawarty w różnych zestawów, które są generowane dla każdego docelowego środowiska uruchomieniowego (ARM, x86 i x64). Aby uwzględnić je w pakiecie, `<files>` odwołaj się do nich w sekcji wraz z skojarzonymi z nimi plikami zasobów .pri:

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

Następnie projekty W++ i JavaScript, które mogą korzystać z pakietu NuGet, potrzebują pliku .targets do identyfikowania niezbędnych plików zestawu i winmd. (Projekty języka C# i Visual Basic robią to automatycznie). Utwórz ten plik, kopiując poniższy `ImageEnhancer.targets` tekst i `.nuspec` zapisując go w tym samym folderze co plik. _Uwaga:_ `.targets` Ten plik musi mieć taką samą nazwę jak identyfikator `<Id>` pakietu `.nupspec` (np. element w pliku):

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

Następnie zapoznaj `ImageEnhancer.targets` się `.nuspec` z plikiem:

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

### <a name="final-nuspec"></a>Końcowy .nuspec

Plik `.nuspec` końcowy powinien teraz wyglądać następująco, gdzie ponownie YOUR_NAME należy zastąpić odpowiednią wartością:

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

## <a name="package-the-component"></a>Zapakuj składnik

Po zakończeniu `.nuspec` odwoływania się do wszystkich plików, które należy uwzględnić `pack` w pakiecie, możesz uruchomić polecenie:

```cli
nuget pack ImageEnhancer.nuspec
```

To generuje `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`. Otwierając ten plik w narzędziu, takim jak [Eksplorator pakietów NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozwijając wszystkie węzły, zostanie wyświetleni następująca zawartość:

![NuGet Package Explorer przedstawiający pakiet ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> Plik `.nupkg` to tylko plik ZIP z innym rozszerzeniem. Możesz również sprawdzić zawartość pakietu, `.nupkg` a `.zip`następnie, zmieniając na , ale pamiętaj, aby przywrócić rozszerzenie przed przesłaniem pakietu do nuget.org.

Aby udostępnić pakiet innym deweloperom, postępuj zgodnie z instrukcjami dotyczącymi [publikowania pakietu](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>Powiązane tematy

- [.nuspec Odwołanie](../reference/nuspec.md)
- [Pakiety symboli](../create-packages/symbol-packages-snupkg.md)
- [Przechowywanie wersji pakietów](../concepts/package-versioning.md)
- [Obsługa wielu wersji programu .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Uwzględnij rekwizyty i obiekty docelowe MSBuild w pakiecie](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
