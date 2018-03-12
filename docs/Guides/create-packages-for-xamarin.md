---
title: "Tworzenie pakietów NuGet i Platform (dla systemu iOS, Android i Windows) | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Przewodnik end-to-end tworzenia pakietów NuGet dla platformy Xamarin w systemie macierzystych interfejsów API dla systemu iOS, Android i Windows."
keywords: "Utwórz pakiet, pakietów dla platformy Xamarin, pakietów i platform"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 185a0e1e424d1ceb2d8bacbcc1502b38412c4c41
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/08/2018
---
# <a name="create-cross-platform-packages"></a>Tworzenie pakietów i platform

Pakiet wieloplatformowych zawiera kod, który używa macierzystych interfejsów API w systemach iOS, Android i Windows, w zależności od środowiska wykonawczego systemu operacyjnego. Chociaż jest to prosty zrobić, zaleca się pozwala deweloperom korzystać z pakietu z PCL lub powierzchnia .NET standardowych bibliotek za pośrednictwem wspólnego interfejsu API.

W tym przewodniku tworzenia pakietu NuGet i platform, który może być używana w przenośnych projekty w systemach iOS, Android i Windows.

1. [Wymagania wstępne](#prerequisites)
1. [Tworzenie projektu kodu struktury i abstrakcji](#create-the-project-structure-and-abstraction-code)
1. [Wpisz swój kod specyficzne dla platformy](#write-your-platform-specific-code)
1. [Tworzenie i aktualizowanie pliku .nuspec](#create-and-update-the-nuspec-file)
1. [Pakiet składnika](#package-the-component)
1. [Tematy pokrewne](#related-topics)

## <a name="prerequisites"></a>Wymagania wstępne

1. Visual Studio 2015 z platformy uniwersalnej systemu Windows (UWP) i Xamarin. Bezpłatnie zainstalować Community edition z [visualstudio.com](https://www.visualstudio.com/); oczywiście można również wersje Professional i Enterprise. Aby dołączyć narzędzia platformy uniwersalnej systemu Windows i program Xamarin, wybierz Instalacja niestandardowa, a następnie wybierz odpowiednie opcje.
1. Interfejs wiersza polecenia NuGet. Pobierz najnowszą wersję nuget.exe z [nuget.org/downloads](https://nuget.org/downloads), zapisać go do wybranej lokalizacji. Dodać tej lokalizacji do Twojej zmiennej środowiskowej PATH, gdy nie jest jeszcze.

> [!Note]
> nuget.exe to narzędzie interfejsu wiersza polecenia, nie Instalatora, dlatego należy Zapisz pobrany plik z przeglądarki, a jego uruchomieniem.

## <a name="create-the-project-structure-and-abstraction-code"></a>Tworzenie projektu kodu struktury i abstrakcji

1. Pobierz i uruchom [wtyczki dla rozszerzenia szablonów Xamarin](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) dla programu Visual Studio. Te szablony ułatwi późniejszą tworzenia struktury projektu na potrzeby tego przewodnika.
1. W programie Visual Studio **Plik > Nowy > Projekt**, wyszukiwania `Plugin`, wybierz pozycję **dodatek plug-in dla platformy Xamarin** szablonu, Zmień nazwę na LoggingLibrary, a następnie kliknij przycisk OK.

    ![Nowy projekt pusta aplikacja (przenośna platformy Xamarin.Forms) w programie Visual Studio](media/CrossPlatform-NewProject.png)

Wynikowa rozwiązania zawiera dwa projekty PCL, wraz z różnych projektów specyficzne dla platformy:

- PCL o nazwie `Plugin.LoggingLibrary.Abstractions (Portable)`, w tym przypadku definiuje interfejs publiczny (powierzchni interfejsu API) składnika `ILoggingLibrary` zawarte w pliku ILoggingLibrary.cs interfejsu. Jest to, gdzie zdefiniować interfejs do biblioteki.
- Inne PCL `Plugin.LoggingLibrary (Portable)`, zawiera kod w CrossLoggingLibrary.cs, który będzie zlokalizować specyficzne dla platformy implementację abstrakcyjnej interfejsu w czasie wykonywania. Zwykle nie należy do modyfikowania tego pliku.
- Projekty poszczególnych platform, takich jak `Plugin.LoggingLibrary.Android`, każdy zawiera zawierają natywnych implementacji interfejsu w ich odpowiednich plików LoggingLibraryImplementation.cs. Jest to, które służy do tworzenia biblioteki kodu.

Domyślnie plik ILoggingLibrary.cs projektu abstrakcje zawiera definicję interfejsu, ale żadnych metod. Na potrzeby tego przewodnika, Dodaj `Log` metody w następujący sposób:

```cs
using System;

namespace Plugin.LoggingLibrary.Abstractions
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

## <a name="write-your-platform-specific-code"></a>Wpisz swój kod specyficzne dla platformy

Aby zaimplementować implementacja specyficzna dla platformy `ILoggingLibrary` interfejsu i jego metod, wykonaj następujące czynności:

1. Otwórz `LoggingLibraryImplementation.cs` pliku każdej platformy projektu i dodać wymagany kod. Na przykład (przy użyciu `Plugin.LoggingLibrary.Android` projektu):

    ```cs
    using Plugin.LoggingLibrary.Abstractions;
    using System;

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

1. Powtórz tej implementacji w projektach dla wszystkich platform, które mają być obsługiwane.
1. Kliknij prawym przyciskiem myszy projekt iOS, wybierz **właściwości**, kliknij przycisk **kompilacji** i Usuń "\iPhone" z **ścieżka wyjściowa** i **pliku dokumentacji XML**  ustawienia. Dotyczy to tylko nowsze wygodę w tym przewodniku. Zapisz plik po zakończeniu.
1. Kliknij prawym przyciskiem myszy rozwiązanie, wybierz **programu Configuration Manager...** i sprawdź **kompilacji** pól PCLs i poszczególnych platform w przypadku obsługi.
1. Kliknij prawym przyciskiem myszy rozwiązanie, a następnie wybierz **Kompiluj rozwiązanie** Sprawdź swoją pracę i utworzyć artefaktów, które można następnie pakietu. Jeśli występują błędy dotyczące brakujących odwołań, kliknij prawym przyciskiem myszy rozwiązanie, wybierz **przywracania pakietów NuGet** zainstalować zależności i skompiluj ponownie.

> [!Note]
> Aby utworzyć dla systemu iOS należy Mac sieciowe podłączone do programu Visual Studio, zgodnie z opisem w [wprowadzenie do platformy Xamarin.iOS dla programu Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/). Jeśli nie masz dostępnych Mac, należy wyczyścić projektu systemu iOS w programie configuration manager (krok 3 powyżej).

## <a name="create-and-update-the-nuspec-file"></a>Tworzenie i aktualizowanie pliku .nuspec

1. Otwórz wiersz polecenia, przejdź do `LoggingLibrary` folderu o jeden poziom poniżej where `.sln` pliku jest i uruchom NuGet `spec` polecenie, aby utworzyć pierwszy `Package.nuspec` pliku:

```cli
nuget spec
```

1. Zmień nazwę tego pliku do `LoggingLibrary.nuspec` i otwórz go w edytorze.
1. Zaktualizuj plik zgodnie z poniższym, zamieniając twoje_imie odpowiednią wartość. `<id>` Wartość, w szczególności musi być unikatowa w nuget.org (konwencje nazewnictwa opisane w temacie [utworzenie pakietu](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)). Należy również zauważyć, że należy również zaktualizować tagi autora oraz opis lub wystąpi błąd podczas wykonywania kroku pakowania.

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
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> Można sufiks wersji pakietu z `-alpha`, `-beta` lub `-rc` aby oznaczyć do pakietu jako wersji wstępnej, sprawdź [wersje wstępne](../create-packages/prerelease-packages.md) uzyskać więcej informacji o wersji wstępnych.

### <a name="add-reference-assemblies"></a>Dodawanie zestawów odwołań

Aby uwzględnić zestawy referencyjne specyficzne dla platformy, Dodaj następujący kod do `<files>` elementu `LoggingLibrary.nuspec` odpowiednio dla obsługiwanych platform:

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
> Aby skrócić nazwy plików DLL i kod XML, kliknij prawym przyciskiem myszy na żadnym konkretnym projektem, wybierz opcję **biblioteki** , a następnie zmień nazwy zestawu.

### <a name="add-dependencies"></a>Dodaj zależności

Jeśli masz określonych zależności dla implementacji native użyj `<dependencies>` element z `<group>` elementy, aby określić, na przykład:

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

Na przykład następujące ustawiał iTextSharp jako zależność UAP docelowych:

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a>Końcowe .nuspec

Twoje final `.nuspec` pliku powinna wyglądać podobnie do następującego: gdzie ponownie twoje_imie należy zamienić na odpowiednie wartości:

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
    <copyright>Copyright 2016</copyright>
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

## <a name="package-the-component"></a>Pakiet składnika

Z ukończonej `.nuspec` odwołuje się do wszystkich plików, które należy uwzględnić w pakiecie, wszystko jest gotowe do uruchomienia `pack` polecenia:

```cli
nuget pack LoggingLibrary.nuspec
```

Spowoduje to wygenerowanie `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`. Otwarcie tego pliku w narzędzia, takiego jak [Explorer pakietu NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzanie wszystkich węzłów, zobacz następującą zawartość:

![Wyświetlanie pakietu LoggingLibrary Explorer pakietu NuGet](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> A `.nupkg` plik jest tylko plik ZIP zawierający inne rozszerzenie. Można również sprawdzić zawartość pakietu, następnie zmieniając `.nupkg` do `.zip`, ale pamiętaj, aby przywrócić rozszerzenia przed przekazaniem do nuget.org pakietu.

Aby udostępnić pakietu inni deweloperzy, postępuj zgodnie z instrukcjami [opublikowania pakietu](../create-packages/publish-a-package.md).

## <a name="related-topics"></a>Tematy pokrewne

- [Plik Nuspec odwołania](../reference/nuspec.md)
- [Pakiety symboli](../create-packages/symbol-packages.md)
- [Przechowywanie wersji pakietów](../reference/package-versioning.md)
- [Obsługa wielu wersje programu .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [W tym właściwości programu MSBuild i obiektów docelowych w pakiecie](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)