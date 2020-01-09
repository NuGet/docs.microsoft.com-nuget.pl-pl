---
title: Tworzenie pakietów NuGet dla platformy Xamarin (dla systemów iOS, Android i Windows) przy użyciu programu Visual Studio 2017 lub 2019
description: Kompleksowy przewodnik tworzenia pakietów NuGet dla platformy Xamarin, które używają natywnych interfejsów API w systemach iOS, Android i Windows.
author: karann-msft
ms.author: karann
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: fce3c9a92dfee325f9e914bf3d6444601fb38b6c
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385691"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a>Tworzenie pakietów dla platformy Xamarin za pomocą programu Visual Studio 2017 lub 2019

Pakiet dla platformy Xamarin zawiera kod, który używa natywnych interfejsów API w systemach iOS, Android i Windows, w zależności od systemu operacyjnego w czasie wykonywania. Chociaż jest to proste, zaleca się, aby deweloperzy zużywali pakiet z bibliotek PCL lub .NET Standard za pośrednictwem wspólnego obszaru powierzchni interfejsu API.

W tym instruktażu użyjesz programu Visual Studio 2017 lub 2019, aby utworzyć pakiet NuGet dla wielu platform, który może być używany w projektach mobilnych w systemach iOS, Android i Windows.

1. [Wymagania wstępne](#prerequisites)
1. [Tworzenie struktury projektu i kodu abstrakcji](#create-the-project-structure-and-abstraction-code)
1. [Napisz kod specyficzny dla platformy](#write-your-platform-specific-code)
1. [Utwórz i zaktualizuj plik. nuspec](#create-and-update-the-nuspec-file)
1. [Pakowanie składnika](#package-the-component)
1. [Tematy pokrewne](#related-topics)

## <a name="prerequisites"></a>Wymagania wstępne

1. Program Visual Studio 2017 lub 2019 z platforma uniwersalna systemu Windows (platformy UWP) i Xamarin. Zainstaluj bezpłatnie wersję Community z [VisualStudio.com](https://www.visualstudio.com/); Możesz również korzystać z wersji Professional i Enterprise. Aby dołączyć narzędzia platformy UWP i Xamarin Tools, wybierz instalację niestandardową i Sprawdź odpowiednie opcje.
1. Interfejs wiersza polecenia NuGet. Pobierz najnowszą wersję pliku NuGet. exe z [NuGet.org/downloads](https://nuget.org/downloads), zapisując ją w wybranej lokalizacji. Następnie Dodaj tę lokalizację do zmiennej środowiskowej PATH, jeśli nie została jeszcze.

> [!Note]
> NuGet. exe to narzędzie interfejsu wiersza polecenia, a nie Instalator, dlatego pamiętaj o zapisaniu pobranego pliku w przeglądarce zamiast uruchamiania go.

## <a name="create-the-project-structure-and-abstraction-code"></a>Tworzenie struktury projektu i kodu abstrakcji

1. Pobierz i uruchom [Międzyplatformowe rozszerzenie .NET Standard szablony wtyczek](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) dla programu Visual Studio. Te szablony ułatwiają tworzenie niezbędnej struktury projektu dla tego przewodnika.
1. W programie Visual Studio 2017 **plik > nowy > Project**, Wyszukaj `Plugin`, wybierz **Międzyplatformowy szablon wtyczki biblioteki .NET Standard** , Zmień nazwę na LoggingLibrary, a następnie kliknij przycisk OK.

    ![Nowa pusta aplikacja (Xamarin. Forms Portable) w programie VS 2017](media/CrossPlatform-NewProject.png)

    W programie Visual Studio 2019 **plik > nowy > Project**, Wyszukaj `Plugin`, wybierz **Międzyplatformowy szablon wtyczki biblioteki .NET Standard** , a następnie kliknij przycisk Dalej.

    ![Nowa pusta aplikacja (Xamarin. Forms Portable) w programie VS 2019](media/CrossPlatform-NewProject19-Part1.png)

    Zmień nazwę na LoggingLibrary, a następnie kliknij przycisk Utwórz.

    ![Konfiguracja nowej pustej aplikacji (Xamarin. Forms Portable) w programie VS 2019](media/CrossPlatform-NewProject19-Part2.png)

Otrzymane rozwiązanie zawiera dwa projekty udostępnione wraz z różnymi projektami specyficznymi dla platformy:

- Projekt `ILoggingLibrary`, który znajduje się w pliku `ILoggingLibrary.shared.cs`, definiuje publiczny interfejs (obszar powierzchniowy interfejsu API) składnika. Jest to miejsce, w którym można zdefiniować interfejs biblioteki.
- Inny udostępniony projekt zawiera kod w `CrossLoggingLibrary.shared.cs`, który będzie lokalizować implementację interfejsu abstrakcyjnego dla danej platformy w czasie wykonywania. Zazwyczaj nie trzeba modyfikować tego pliku.
- Projekty specyficzne dla platformy, takie jak `LoggingLibrary.android.cs`, każdy z nich zawierają natywną implementację interfejsu w odpowiednich `LoggingLibraryImplementation.cs` (VS 2017) lub `LoggingLibrary.<PLATFORM>.cs` (VS 2019). Jest to miejsce, w którym można utworzyć kod biblioteki.

Domyślnie plik ILoggingLibrary.shared.cs projektu `ILoggingLibrary` zawiera definicję interfejsu, ale nie ma żadnych metod. Na potrzeby tego instruktażu należy dodać metodę `Log` w następujący sposób:

```cs
using System;
using System.Collections.Generic;
using System.Text;

namespace Plugin.LoggingLibrary
{
    /// <summary>
    /// Interface for LoggingLibrary
    /// </summary>
    public interface ILoggingLibrary
    {
        /// <summary>
        /// Log a message
        /// </summary>
        void Log(string text);
    }
}
```

## <a name="write-your-platform-specific-code"></a>Napisz kod specyficzny dla platformy

Aby zaimplementować implementację interfejsu `ILoggingLibrary` i jego metod specyficznych dla platformy, wykonaj następujące czynności:

1. Otwórz plik `LoggingLibraryImplementation.cs` (VS 2017) lub `LoggingLibrary.<PLATFORM>.cs` (VS 2019) dla każdego projektu platformy i Dodaj wymagany kod. Na przykład (przy użyciu projektu platformy `Android`):

    ```cs
    using System;
    using System.Collections.Generic;
    using System.Text;

    namespace Plugin.LoggingLibrary
    {
        /// <summary>
        /// Implementation for Feature
        /// </summary>
        public class LoggingLibraryImplementation : ILoggingLibrary
        {
            /// <summary>
            /// Log a message
            /// </summary>
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log on Android");
            }
        }
    }
    ```

1. Powtórz tę implementację w projektach dla każdej platformy, która ma być obsługiwana.
1. Kliknij prawym przyciskiem myszy rozwiązanie, a następnie wybierz pozycję **Kompiluj rozwiązanie** , aby sprawdzić swoją służbę i utworzyć artefakty, które zostały umieszczone w dalszej kolejności. Jeśli pojawią się błędy dotyczące brakujących odwołań, kliknij prawym przyciskiem myszy rozwiązanie, wybierz polecenie **Przywróć pakiety NuGet** , aby zainstalować zależności i ponownie skompilować.

> [!Note]
> Jeśli używasz programu Visual Studio 2019, przed wybraniem opcji **Przywróć pakiety NuGet** i próbą odbudowy należy zmienić wersję `MSBuild.Sdk.Extras` na `2.0.54` w `LoggingLibrary.csproj`. Dostęp do tego pliku można uzyskać tylko przez kliknięcie prawym przyciskiem myszy projektu (poniżej rozwiązania) i wybranie `Unload Project`, po którym kliknij prawym przyciskiem myszy zwolnionego projektu i wybierz pozycję `Edit LoggingLibrary.csproj`.

> [!Note]
> Aby można było skompilować system iOS, potrzebny jest komputer Mac podłączony do programu Visual Studio, zgodnie z opisem w artykule [wprowadzenie do platformy Xamarin. iOS dla programu Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/). Jeśli nie masz dostępnego komputera Mac, wyczyść projekt systemu iOS w programie Configuration Manager (krok 3 powyżej).

## <a name="create-and-update-the-nuspec-file"></a>Utwórz i zaktualizuj plik. nuspec

1. Otwórz wiersz polecenia, przejdź do folderu `LoggingLibrary`, który znajduje się poniżej, w którym znajduje się plik `.sln`, i uruchom polecenie NuGet `spec`, aby utworzyć początkowy plik `Package.nuspec`:

    ```cli
    nuget spec
    ```

1. Zmień nazwę tego pliku na `LoggingLibrary.nuspec` i otwórz go w edytorze.
1. Zaktualizuj plik w taki sposób, aby pasował do następującej wartości YOUR_NAME. Wartość `<id>`, szczególnie, musi być unikatowa w obrębie nuget.org (zobacz Konwencje nazewnictwa opisane w temacie [Tworzenie pakietu](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)). Należy również pamiętać, że należy również zaktualizować Tagi autor i opis lub podczas kroku pakowania wystąpi błąd.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>LoggingLibrary.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>LoggingLibrary</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2018</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> Aby oznaczyć pakiet jako wersję wstępną, można uzyskać sufiks wersji pakietu z `-alpha`, `-beta` lub `-rc`. w tym celu sprawdź [wersje wstępne](../create-packages/prerelease-packages.md) , aby uzyskać więcej informacji na temat wersji wstępnych.

### <a name="add-reference-assemblies"></a>Dodaj zestawy referencyjne

Aby uwzględnić zestawy referencyjne specyficzne dla platformy, Dodaj następujące elementy do `<files>` elementu `LoggingLibrary.nuspec`, zgodnie z potrzebami dla obsługiwanych platform:

```xml
<!-- Insert below <metadata> element -->
<files>
    <!-- Cross-platform reference assemblies -->
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

    <!-- iOS reference assemblies -->
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

    <!-- Android reference assemblies -->
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

    <!-- UWP reference assemblies -->
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
</files>
```

> [!Note]
> Aby skrócić nazwy plików DLL i XML, kliknij prawym przyciskiem myszy dowolny dany projekt, wybierz kartę **Biblioteka** i Zmień nazwy zestawów.

### <a name="add-dependencies"></a>Dodaj zależności

Jeśli masz określone zależności dla implementacji natywnych, użyj elementu `<dependencies>` z elementami `<group>`, aby je określić, na przykład:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="MonoAndroid">
        <!--MonoAndroid dependencies go here-->
    </group>
    <group targetFramework="Xamarin.iOS10">
        <!--Xamarin.iOS10 dependencies go here-->
    </group>
    <group targetFramework="uap">
        <!--uap dependencies go here-->
    </group>
</dependencies>
```

Na przykład następujące polecenie ustawi iTextSharp jako zależność dla elementu docelowego UAP:

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a>Final. nuspec

Końcowy plik `.nuspec` powinien teraz wyglądać podobnie do poniższego, gdzie ponownie YOUR_NAME należy zastąpić odpowiednią wartością:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>LoggingLibrary.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>LoggingLibrary</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2018</copyright>
    <tags>logger logging logs</tags>
        <dependencies>
        <group targetFramework="MonoAndroid">
            <!--MonoAndroid dependencies go here-->
        </group>
        <group targetFramework="Xamarin.iOS10">
            <!--Xamarin.iOS10 dependencies go here-->
        </group>
        <group targetFramework="uap">
            <dependency id="iTextSharp" version="5.5.9" />
        </group>
    </dependencies>
    </metadata>
    <files>
        <!-- Cross-platform reference assemblies -->
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

        <!-- iOS reference assemblies -->
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

        <!-- Android reference assemblies -->
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

        <!-- UWP reference assemblies -->
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
    </files>
</package>
```

## <a name="package-the-component"></a>Pakowanie składnika

Wraz z `.nuspec` zakończonymi odwołującymi się do wszystkich plików, które należy uwzględnić w pakiecie, możesz uruchomić polecenie `pack`:

```cli
nuget pack LoggingLibrary.nuspec
```

Spowoduje to wygenerowanie `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`. Otwierając ten plik w narzędziu, takim jak [Eksplorator pakietów NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzając wszystkie węzły, zobaczysz następującą zawartość:

![Eksplorator pakietów NuGet przedstawiający pakiet LoggingLibrary](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> Plik `.nupkg` jest po prostu plikiem ZIP z innym rozszerzeniem. Możesz również przeanalizować zawartość pakietu, zmieniając `.nupkg` na `.zip`, pamiętając o przywróceniu rozszerzenia przed przekazaniem pakietu do nuget.org.

Aby udostępnić pakiet innym deweloperom, postępuj zgodnie z instrukcjami dotyczącymi [publikowania pakietu](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>Tematy pokrewne

- [Odwołanie nuspec](../reference/nuspec.md)
- [Pakiety symboli](../create-packages/symbol-packages.md)
- [Przechowywanie wersji pakietów](../concepts/package-versioning.md)
- [Obsługa wielu wersji .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Uwzględnij w pakiecie narzędzia i elementy docelowe programu MSBuild](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)