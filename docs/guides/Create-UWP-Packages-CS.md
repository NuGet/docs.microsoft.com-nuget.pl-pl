---
title: Utwórz pakiety NuGet dla platforma uniwersalna systemu Windows
description: Kompleksowy przewodnik tworzenia pakietów NuGet przy użyciu składnika środowisko wykonawcze systemu Windows dla platforma uniwersalna systemu Windows w języku C#.
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 6f8037f439d627af158b6d5b7746a633b053e514
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238013"
---
# <a name="create-uwp-packages-c"></a>Tworzenie pakietów platformy UWP (C#)

[Platforma uniwersalna systemu Windows (platformy UWP)](/windows/uwp) zapewnia wspólną platformę aplikacji dla każdego urządzenia z systemem Windows 10. W ramach tego modelu aplikacje platformy UWP mogą wywoływać oba interfejsy API WinRT, które są wspólne dla wszystkich urządzeń, a także interfejsy API (w tym Win32 i .NET), które są specyficzne dla rodziny urządzeń, na których działa aplikacja.

W tym instruktażu utworzysz pakiet NuGet ze składnikiem platformy UWP języka C# (łącznie z kontrolką XAML), który może być używany w projektach zarządzanych i natywnych.

## <a name="prerequisites"></a>Wymagania wstępne

1. Program Visual Studio 2019. Zainstaluj bezpłatnie wersję 2019 Community z [VisualStudio.com](https://www.visualstudio.com/); można również używać wersji Professional i Enterprise.

1. Interfejs wiersza polecenia NuGet. Pobierz najnowszą wersję `nuget.exe` z [NuGet.org/downloads](https://nuget.org/downloads), zapisując ją w wybranej lokalizacji (pobieranie jest `.exe` bezpośrednie). Następnie Dodaj tę lokalizację do zmiennej środowiskowej PATH, jeśli nie została jeszcze. [Więcej szczegółów](../reference/nuget-exe-cli-reference.md#windows).

## <a name="create-a-uwp-windows-runtime-component"></a>Utwórz składnik środowisko wykonawcze systemu Windows platformy UWP

1. W programie Visual Studio wybierz kolejno pozycje **plik > nowy > projekt** , wyszukaj ciąg "platformy UWP c#", wybierz szablon **składnik środowisko wykonawcze systemu Windows (uniwersalny system Windows)** , kliknij przycisk Dalej, Zmień nazwę na ImageEnhancer, a następnie kliknij przycisk Utwórz. Po wyświetleniu monitu zaakceptuj wartości domyślne wersji docelowej i wersji minimalnej.

    ![Tworzenie nowego projektu składnika środowisko wykonawcze systemu Windows platformy UWP](media/UWP-NewProject-CS.png)

1. Kliknij prawym przyciskiem myszy projekt w Eksplorator rozwiązań, wybierz pozycję **dodaj > nowy element** , wybierz opcję **formant z szablonem** , Zmień nazwę na AwesomeImageControl.cs, a następnie kliknij przycisk **Dodaj** :

    ![Dodawanie nowego elementu formantu XAML z szablonem do projektu](media/UWP-NewXAMLControl-CS.png)

1. Kliknij prawym przyciskiem myszy projekt w Eksplorator rozwiązań i wybierz polecenie **właściwości.** Na stronie właściwości wybierz kartę **kompilacja** i Włącz **plik dokumentacji XML** :

    ![Ustawienie Generuj pliki dokumentacji XML na tak](media/UWP-GenerateXMLDocFiles-CS.png)

1. Kliknij teraz *rozwiązanie* prawym przyciskiem myszy, wybierz pozycję **kompilacja wsadowa** , a następnie sprawdź pięć pól kompilacji w oknie dialogowym, jak pokazano poniżej. Daje to pewność, że po wykonaniu kompilacji zostanie wygenerowany pełen zestaw artefaktów dla każdego systemu docelowego obsługiwanego przez system Windows.

    ![Kompilacja wsadowa](media/UWP-BatchBuild-CS.png)

1. W oknie dialogowym kompilacja wsadowa, a następnie kliknij przycisk **Kompiluj** , aby zweryfikować projekt i utworzyć pliki wyjściowe potrzebne dla pakietu NuGet.

> [!Note]
> W tym instruktażu użyjesz artefaktów debugowania dla pakietu. W przypadku pakietu bez debugowania Sprawdź opcje wydania w oknie dialogowym kompilacja wsadowa, a następnie zapoznaj się z folderem wydania w poniższej procedurze.

## <a name="create-and-update-the-nuspec-file"></a>Utwórz i zaktualizuj plik. nuspec

Aby utworzyć początkowy `.nuspec` plik, wykonaj trzy poniższe czynności. Poniższe sekcje przeprowadzą Cię przez inne niezbędne aktualizacje.

1. Otwórz wiersz polecenia i przejdź do folderu zawierającego `ImageEnhancer.csproj` (będzie to podfolder poniżej lokalizacji pliku rozwiązania).
1. Uruchom [`NuGet spec`](../reference/cli-reference/cli-ref-spec.md) polecenie, aby wygenerować `ImageEnhancer.nuspec` (nazwa pliku jest pobierana z nazwy `.csroj` pliku):

    ```cli
    nuget spec
    ```

1. Otwórz program `ImageEnhancer.nuspec` w edytorze i zaktualizuj go tak, aby pasował do następujących wartości, zastępując YOUR_NAME odpowiednią wartością. Nie pozostawiaj żadnych wartości $propertyName $. `<id>`Wartość, szczególnie, musi być unikatowa w obrębie NuGet.org (zobacz Konwencje nazewnictwa opisane w artykule [Tworzenie pakietu](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)). Należy również pamiętać, że należy również zaktualizować Tagi autor i opis lub podczas kroku pakowania wystąpi błąd.

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
        <copyright>Copyright 2020</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> W przypadku pakietów przeznaczonych do użycia publicznego należy zwrócić szczególną uwagę na `<tags>` element, ponieważ te Tagi ułatwiają innym znalezienie pakietu i zrozumienie jego działania.

### <a name="adding-windows-metadata-to-the-package"></a>Dodawanie metadanych systemu Windows do pakietu

Składnik środowisko wykonawcze systemu Windows wymaga metadanych, które opisują wszystkie dostępne publicznie typy, które umożliwiają korzystanie z składnika przez inne aplikacje i biblioteki. Te metadane są zawarte w pliku winmd, który jest tworzony podczas kompilowania projektu i musi być dołączony do pakietu NuGet. Plik XML z danymi IntelliSense jest również zbudowany w tym samym czasie i powinien być również dołączony.

Dodaj następujący `<files>` węzeł do `.nuspec` pliku:

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a>Dodawanie zawartości XAML

Aby dołączyć kontrolkę XAML do składnika, należy dodać plik XAML, który ma szablon domyślny dla formantu (zgodnie z szablonem projektu). Jest to również `<files>` sekcja:

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

W składniku podstawowa logika typu ImageEnhancer jest w kodzie natywnym, który jest zawarty w różnych `ImageEnhancer.winmd` zestawach, które są generowane dla każdego docelowego środowiska uruchomieniowego (ARM, arm64, x86 i x64). Aby uwzględnić je w pakiecie, należy odwołać się do nich w `<files>` sekcji wraz ze skojarzonymi z nimi plikami zasobów. pri:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

### <a name="final-nuspec"></a>Final. nuspec

Ostatni `.nuspec` plik powinien teraz wyglądać podobnie do poniższego, gdzie ponownie YOUR_NAME powinien zostać zastąpiony odpowiednią wartością:

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
    <copyright>Copyright 2020</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

## <a name="package-the-component"></a>Pakowanie składnika

Po zakończeniu `.nuspec` odwoływania się do wszystkich plików, które należy uwzględnić w pakiecie, możesz uruchomić [`nuget pack`](../reference/cli-reference/cli-ref-pack.md) polecenie:

```cli
nuget pack ImageEnhancer.nuspec
```

Spowoduje to wygenerowanie `ImageEnhancer.YOUR_NAME.1.0.0.nupkg` . Otwierając ten plik w narzędziu, takim jak [Eksplorator pakietów NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzając wszystkie węzły, zobaczysz następującą zawartość:

![Eksplorator pakietów NuGet przedstawiający pakiet ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> `.nupkg`Plik jest po prostu plikiem ZIP z innym rozszerzeniem. Możesz również przeanalizować zawartość pakietu, a następnie zmienić `.nupkg` ją na `.zip` , ale pamiętaj, aby przywrócić rozszerzenie przed przekazaniem pakietu do NuGet.org.

Aby udostępnić pakiet innym deweloperom, postępuj zgodnie z instrukcjami dotyczącymi [publikowania pakietu](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>Powiązane tematy

- [nuspec — odwołanie](../reference/nuspec.md)
- [Pakiety symboli](../create-packages/symbol-packages-snupkg.md)
- [Przechowywanie wersji pakietów](../concepts/package-versioning.md)
- [Obsługa wielu wersji .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Uwzględnij w pakiecie narzędzia i elementy docelowe programu MSBuild](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)