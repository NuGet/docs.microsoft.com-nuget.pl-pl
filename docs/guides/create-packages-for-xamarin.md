---
title: Tworzenie pakietów NuGet dla platformy Xamarin (dla systemów iOS, Android i Windows) za pomocą programu Visual Studio 2017 lub 2019
description: End-to-end instruktaż tworzenia pakietów NuGet dla platformy Xamarin, które używają natywnych interfejsów API w systemach iOS, Android i Windows.
author: karann-msft
ms.author: karann
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: 0cb653bad9e853d908039b3f7a94e1dd7eefdde5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230905"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a>Tworzenie pakietów dla platformy Xamarin za pomocą programu Visual Studio 2017 lub 2019

Pakiet dla platformy Xamarin zawiera kod, który używa natywnych interfejsów API w systemach iOS, Android i Windows, w zależności od systemu operacyjnego w czasie wykonywania. Mimo że jest to proste do zrobienia, lepiej jest pozwolić deweloperom korzystać z pakietu z bibliotek PCL lub .NET Standard za pośrednictwem wspólnego obszaru powierzchni interfejsu API.

W tym instruktażu można użyć programu Visual Studio 2017 lub 2019 do utworzenia wieloplatformowego pakietu NuGet, który może być używany w projektach mobilnych w systemach iOS, Android i Windows.

1. [Wymagania wstępne](#prerequisites)
1. [Tworzenie struktury projektu i kodu abstrakcji](#create-the-project-structure-and-abstraction-code)
1. [Napisz kod specyficzny dla platformy](#write-your-platform-specific-code)
1. [Tworzenie i aktualizowanie pliku nuspec](#create-and-update-the-nuspec-file)
1. [Zapakuj składnik](#package-the-component)
1. [Tematy pokrewne](#related-topics)

## <a name="prerequisites"></a>Wymagania wstępne

1. Visual Studio 2017 lub 2019 z uniwersalną platformą systemu Windows (UWP) i platformą Xamarin. Zainstaluj wersję wspólnotową bezpłatnie od [visualstudio.com;](https://www.visualstudio.com/) oczywiście można również korzystać z wersji Professional i Enterprise. Aby uwzględnić narzędzia platformy uniwersalnej systemu Windows i platformy Xamarin, wybierz instalację niestandardową i sprawdź odpowiednie opcje.
1. Funkcja Interfejsu wiersza polecenia NuGet. Pobierz najnowszą wersję nuget.exe z [nuget.org/downloads](https://nuget.org/downloads), zapisując ją w wybranej lokalizacji. Następnie dodaj tę lokalizację do zmiennej środowiskowej PATH, jeśli jeszcze jej nie ma.

> [!Note]
> nuget.exe jest samo narzędzie CLI, a nie instalator, więc pamiętaj, aby zapisać pobrany plik z przeglądarki, zamiast go uruchamiać.

## <a name="create-the-project-structure-and-abstraction-code"></a>Tworzenie struktury projektu i kodu abstrakcji

1. Pobierz i uruchom [rozszerzenie szablonów standardowych wtyczek platformy .NET](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) dla programu Visual Studio. Te szablony ułatwią tworzenie niezbędnej struktury projektu dla tego przewodnika.
1. W programie Visual Studio 2017 **> plik nowego projektu**> `Plugin`, wyszukaj , wybierz szablon **wtyczki biblioteki standardowej .NET na wielu platformach,** zmień nazwę na LoggingLibrary i kliknij przycisk OK.

    ![Nowy projekt pustej aplikacji (Xamarin.Forms Portable) w programie VS 2017](media/CrossPlatform-NewProject.png)

    W programie Visual Studio 2019 **> plik nowego projektu**> `Plugin`, wyszukaj , wybierz szablon **wtyczki biblioteki standardowej platformy .NET** i kliknij przycisk Dalej.

    ![Nowy projekt pustej aplikacji (Xamarin.Forms Portable) w programie VS 2019](media/CrossPlatform-NewProject19-Part1.png)

    Zmień nazwę na LoggingLibrary i kliknij przycisk Utwórz.

    ![Nowa pusta aplikacja (Xamarin.Forms Portable) w programie VS 2019](media/CrossPlatform-NewProject19-Part2.png)

Wynikowe rozwiązanie zawiera dwa projekty współużytkowane, wraz z różnymi projektami specyficznymi dla platformy:

- Projekt, `ILoggingLibrary` który znajduje się `ILoggingLibrary.shared.cs` w pliku, definiuje interfejs publiczny (obszar powierzchni INTERFEJSU API) składnika. W tym miejscu można zdefiniować interfejs do biblioteki.
- Inny udostępniony projekt zawiera `CrossLoggingLibrary.shared.cs` kod, w którym będzie zlokalizować implementacji specyficzne dla platformy abstrakcyjnego interfejsu w czasie wykonywania. Zazwyczaj nie trzeba modyfikować tego pliku.
- Projekty specyficzne dla platformy, `LoggingLibrary.android.cs`takie jak , każdy zawiera natywną implementację interfejsu w odpowiednich plikach `LoggingLibraryImplementation.cs` (VS 2017) lub `LoggingLibrary.<PLATFORM>.cs` (VS 2019). W tym miejscu można utworzyć kod biblioteki.

Domyślnie ILoggingLibrary.shared.cs plik `ILoggingLibrary` projektu zawiera definicję interfejsu, ale nie ma metod. Na potrzeby tego przewodnika należy dodać `Log` metodę w następujący sposób:

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

Aby zaimplementować implementację `ILoggingLibrary` interfejsu i jego metod specyficznych dla platformy, wykonaj następujące czynności:

1. Otwórz `LoggingLibraryImplementation.cs` plik (VS 2017) lub `LoggingLibrary.<PLATFORM>.cs` (VS 2019) każdego projektu platformy i dodaj niezbędny kod. Na przykład (przy użyciu projektu `Android` platformy):

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

1. Powtórz tę implementację w projektach dla każdej platformy, którą chcesz obsługiwać.
1. Kliknij prawym przyciskiem myszy rozwiązanie i wybierz opcję **Buduj rozwiązanie,** aby sprawdzić swoją pracę i utworzyć artefakty, które można spakować w następnej kolejności. Jeśli pojawia się błędy dotyczące brakujących odwołań, kliknij prawym przyciskiem myszy rozwiązanie, wybierz **pozycję Przywróć pakiety NuGet,** aby zainstalować zależności i odbudować.

> [!Note]
> Jeśli używasz programu Visual Studio 2019, przed wybraniem **opcji Przywróć pakiety NuGet** i próbą przebudowy należy zmienić wersję `MSBuild.Sdk.Extras` `2.0.54` na w `LoggingLibrary.csproj`programie . Dostęp do tego pliku można uzyskać tylko po kliknięciu prawym przyciskiem `Unload Project`myszy projektu (poniżej rozwiązania) i `Edit LoggingLibrary.csproj`wybraniu , po czym kliknij prawym przyciskiem myszy niezaładowany projekt i wybierz .

> [!Note]
> Do tworzenia dla systemu iOS potrzebny jest komputer Mac połączony z programem Visual Studio zgodnie z opisem w [programie Wprowadzenie do pliku Xamarin.iOS for Visual Studio.](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/) Jeśli nie masz dostępnego komputera Mac, wyczyść projekt systemu iOS w menedżerze konfiguracji (krok 3 powyżej).

## <a name="create-and-update-the-nuspec-file"></a>Tworzenie i aktualizowanie pliku nuspec

1. Otwórz wiersz polecenia, przejdź `LoggingLibrary` do folderu znajdującego `.sln` się na jednym poziomie `spec` poniżej miejsca, `Package.nuspec` w którym znajduje się plik, i uruchom polecenie NuGet, aby utworzyć plik początkowy:

    ```cli
    nuget spec
    ```

1. Zmień nazwę tego `LoggingLibrary.nuspec` pliku i otwórz go w edytorze.
1. Zaktualizuj plik, aby dopasować go do następujących, zastępując YOUR_NAME odpowiednią wartością. Wartość, `<id>` w szczególności, musi być unikatowa w nuget.org (zobacz konwencje nazewnictwa opisane w [Tworzenie pakietu](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)). Należy również pamiętać, że należy również zaktualizować tagi autora i opisu lub pojawi się błąd podczas kroku pakowania.

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
> Możesz sufiks wersji `-alpha`pakietu `-beta` `-rc` z , lub oznaczyć pakiet jako wersji wstępnej, sprawdź [wersje przed wydaniem, aby](../create-packages/prerelease-packages.md) uzyskać więcej informacji na temat wersji przed wydaniem.

### <a name="add-reference-assemblies"></a>Dodawanie zestawów referencyjnych

Aby uwzględnić zestawy odwołań specyficzne dla `<files>` platformy, `LoggingLibrary.nuspec` dodaj następujące elementy do elementu odpowiednio dla obsługiwanych platform:

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
> Aby skrócić nazwy plików DLL i XML, kliknij prawym przyciskiem myszy dowolny projekt, wybierz kartę **Biblioteka** i zmień nazwy zestawów.

### <a name="add-dependencies"></a>Dodawanie zależności

Jeśli masz określone zależności dla implementacji `<dependencies>` natywnych, użyj elementu z `<group>` elementami, aby je określić, na przykład:

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

Na przykład następujące ustawić iTextSharp jako zależność dla obiektu docelowego UAP:

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a>Końcowy .nuspec

Plik `.nuspec` końcowy powinien teraz wyglądać następująco, gdzie ponownie YOUR_NAME należy zastąpić odpowiednią wartością:

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

## <a name="package-the-component"></a>Zapakuj składnik

Po zakończeniu `.nuspec` odwoływania się do wszystkich plików, które należy uwzględnić `pack` w pakiecie, możesz uruchomić polecenie:

```cli
nuget pack LoggingLibrary.nuspec
```

Spowoduje to `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`wygenerowanie . Otwierając ten plik w narzędziu, takim jak [Eksplorator pakietów NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozwijając wszystkie węzły, zostanie wyświetleni następująca zawartość:

![NuGet Package Explorer przedstawiający pakiet LoggingLibrary](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> Plik `.nupkg` to tylko plik ZIP z innym rozszerzeniem. Możesz również sprawdzić zawartość pakietu, `.nupkg` a `.zip`następnie, zmieniając na , ale pamiętaj, aby przywrócić rozszerzenie przed przesłaniem pakietu do nuget.org.

Aby udostępnić pakiet innym deweloperom, postępuj zgodnie z instrukcjami dotyczącymi [publikowania pakietu](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>Powiązane tematy

- [Referencje Nuspec](../reference/nuspec.md)
- [Pakiety symboli](../create-packages/symbol-packages.md)
- [Przechowywanie wersji pakietów](../concepts/package-versioning.md)
- [Obsługa wielu wersji programu .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Uwzględnij rekwizyty i obiekty docelowe MSBuild w pakiecie](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
