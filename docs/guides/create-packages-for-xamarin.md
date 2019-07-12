---
title: Tworzenie pakietów NuGet dla platformy Xamarin (dla systemu iOS, Android i Windows), w programie Visual Studio 2015
description: Przewodnik end-to-end tworzenia pakietów NuGet dla platformy Xamarin w systemie natywnych interfejsów API systemu iOS, Android i Windows.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: tutorial
ms.openlocfilehash: 81f78de02d9b6510f195e04c78436e38f9b7353d
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842422"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2015"></a>Tworzenie pakietów dla platformy Xamarin za pomocą programu Visual Studio 2015

Pakiet dla programu Xamarin zawiera kod, który używa natywnych interfejsów API w systemach iOS, Android i Windows, w zależności od systemu operacyjnego w czasie wykonywania. Chociaż jest to proste, zaleca się umożliwiają deweloperom używanie pakietu z aplikacji PCL lub obszar powierzchni biblioteki .NET Standard za pomocą wspólnego interfejsu API.

W tym przewodniku, którego używasz programu Visual Studio 2015 Utwórz pakiet NuGet dla wielu platform, który może służyć w projektach mobilnych w systemach iOS, Android i Windows.

1. [Wymagania wstępne](#prerequisites)
1. [Tworzenie projektu kodu struktury i pozyskiwania](#create-the-project-structure-and-abstraction-code)
1. [Pisanie kodu specyficznego dla platformy](#write-your-platform-specific-code)
1. [Tworzenie i aktualizowanie pliku .nuspec](#create-and-update-the-nuspec-file)
1. [Pakiet składnika](#package-the-component)
1. [Tematy pokrewne](#related-topics)

## <a name="prerequisites"></a>Wymagania wstępne

1. Visual Studio 2015 z platforma Universal Windows (UWP) i środowisku Xamarin. Zainstaluj wersję Community za darmo z [visualstudio.com](https://www.visualstudio.com/); możesz oczywiście użyć także wersje Professional i Enterprise. Aby dołączyć narzędzia platformy uniwersalnej systemu Windows i Xamarin, wybierz opcję instalacji niestandardowe, a następnie wybierz odpowiednie opcje.
1. Interfejs wiersza polecenia NuGet. Pobierz najnowszą wersję programu nuget.exe z [nuget.org/downloads](https://nuget.org/downloads), zapisanie go do wybranej lokalizacji. Następnie dodaj tej lokalizacji do zmiennej środowiskowej PATH, jeśli jeszcze tego nie zrobiono.

> [!Note]
> nuget.exe to narzędzie interfejsu wiersza polecenia, nie Instalatora, więc Pamiętaj zapisać pobrany plik z przeglądarki, zamiast uruchamiać go.

## <a name="create-the-project-structure-and-abstraction-code"></a>Tworzenie projektu kodu struktury i pozyskiwania

1. Pobierz i uruchom [wtyczki dla szablonów Xamarin rozszerzenia](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) dla programu Visual Studio. Te szablony będą ułatwiają tworzenia struktury projektu na potrzeby tego przewodnika.
1. W programie Visual Studio **Plik > Nowy > Projekt**, wyszukaj `Plugin`, wybierz opcję **wtyczkę dla platformy Xamarin** szablonu, Zmień nazwę na LoggingLibrary, a następnie kliknij przycisk OK.

    ![Nowy projekt pusta aplikacja (Xamarin.Forms przenośna) w programie Visual Studio](media/CrossPlatform-NewProject.png)

Wynikowy rozwiązanie zawiera dwa projekty PCL, wraz z różnych projektów specyficznych dla platformy:

- PCL o nazwie `Plugin.LoggingLibrary.Abstractions (Portable)`, definiuje interfejs publiczny (obszar powierzchni interfejsu API) składnika, w tym przypadku `ILoggingLibrary` zawarte w pliku ILoggingLibrary.cs interfejsu. Jest to, gdzie definiuje interfejs do biblioteki.
- Inne PCL `Plugin.LoggingLibrary (Portable)`, zawiera kod w CrossLoggingLibrary.cs, który będzie zlokalizować specyficznymi dla platformy implementacji abstrakcyjny interfejs w czasie wykonywania. Zazwyczaj nie należy modyfikować tego pliku.
- Projekty określonych platform, takich jak `Plugin.LoggingLibrary.Android`, każdy zawiera zawierają natywnych implementacji interfejsu w ich odpowiednich plików LoggingLibraryImplementation.cs. Jest to, gdy kompilujesz kod biblioteki programu.

Domyślnie plik ILoggingLibrary.cs projektu abstrakcje zawiera definicję interfejsu, lecz nie metod. Dla celów tego przewodnika, Dodaj `Log` metody w następujący sposób:

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

## <a name="write-your-platform-specific-code"></a>Pisanie kodu specyficznego dla platformy

Do zaimplementowania implementacji specyficznych dla platformy `ILoggingLibrary` interfejsu i jego metod, wykonaj następujące czynności:

1. Otwórz `LoggingLibraryImplementation.cs` pliku każdej z platform projektu, a następnie dodać niezbędny kod. Na przykład (przy użyciu `Plugin.LoggingLibrary.Android` projektu):

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

1. Powtórz tę implementację w projektach dla wszystkich platform, które mają być obsługiwane.
1. Kliknij prawym przyciskiem myszy projekt iOS, wybierz **właściwości**, kliknij przycisk **kompilacji** , a następnie usuń "\iPhone" z **ścieżkę wyjściową** i **pliku dokumentacji XML**  ustawienia. Te informacje dotyczą tylko nowsze wygodę w tym przewodniku. Zapisz plik po zakończeniu.
1. Kliknij prawym przyciskiem myszy rozwiązanie, wybierz **programu Configuration Manager...** i sprawdź **kompilacji** pola PCLs i każdej platformy w przypadku obsługi.
1. Kliknij prawym przyciskiem myszy rozwiązanie, a następnie wybierz pozycję **Kompiluj rozwiązanie** Sprawdź swoją pracę i wygenerować artefaktów, które możesz dalej pakietów. Jeśli występują błędy dotyczące brakujących odwołań, kliknij prawym przyciskiem myszy rozwiązanie, wybierz opcję **Przywróć pakiety NuGet** zainstalować zależności i ponownie skompilować.

> [!Note]
> Kompilacji dla systemu iOS potrzebny jest komputer Mac sieciowe podłączone do programu Visual Studio, zgodnie z opisem na [wprowadzenie do rozwiązania Xamarin.iOS dla programu Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/). Jeśli użytkownik nie ma dostępnych komputera Mac, wyczyść projekt dla systemu iOS w programie configuration manager (krok 3 powyżej).

## <a name="create-and-update-the-nuspec-file"></a>Tworzenie i aktualizowanie pliku .nuspec

1. Otwórz wiersz polecenia, przejdź do `LoggingLibrary` folderu, który jest jeden poziom poniżej miejsca `.sln` plik jest i Uruchom rozszerzenie NuGet `spec` polecenie, aby utworzyć początkowy `Package.nuspec` pliku:

    ```cli
    nuget spec
    ```

1. Zmień nazwę tego pliku do `LoggingLibrary.nuspec` i otwórz go w edytorze.
1. Zaktualizuj plik, aby dopasować następujące polecenie, zastępując twoja_nazwa odpowiednią wartość. `<id>` Wartość, w szczególności musi być unikatowa w witrynie nuget.org (konwencje nazewnictwa, opisane w temacie [Tworzenie pakietu](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)). Należy również zauważyć, że należy również zaktualizować autor i opis znaczników lub wystąpi błąd podczas wykonywania kroku pakowania.

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
> Można sufiks usługi wersję pakietu za pomocą `-alpha`, `-beta` lub `-rc` aby oznaczyć pakietu jako wersji wstępnej, zapoznaj się z [wersje wstępne](../create-packages/prerelease-packages.md) Aby uzyskać więcej informacji o wersjach wstępnych.

### <a name="add-reference-assemblies"></a>Dodawanie odwołań do zestawów

Aby dołączyć zestawy referencyjne specyficzne dla platformy, należy dodać następujące polecenie, aby `<files>` elementu `LoggingLibrary.nuspec` odpowiednio dla obsługiwanych platform:

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
> Aby skrócić nazwy plików DLL i XML, kliknij prawym przyciskiem myszy dowolnego danego projektu, wybierz opcję **biblioteki** , a następnie zmienić nazwy zestawu.

### <a name="add-dependencies"></a>Dodaj zależności

Jeśli określonych zależności dla natywnych implementacji należy używać `<dependencies>` element z `<group>` elementy, aby określić, na przykład:

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

Na przykład następujące ustawiał iTextSharp jako zależność dla elementu docelowego UAP:

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a>Końcowe .nuspec

Ostateczna `.nuspec` plik powinien teraz wyglądać podobnie do poniższego, gdzie ponownie twoja_nazwa należy zamienić na odpowiednie wartości:

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

Za pomocą ukończoną `.nuspec` odwołuje się do wszystkich plików, które należy uwzględnić w pakiecie, wszystko jest gotowe do uruchomienia `pack` polecenia:

```cli
nuget pack LoggingLibrary.nuspec
```

Spowoduje to wygenerowanie `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`. Otwarcie tego pliku w narzędzia, takiego jak [Eksplorator pakietów NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzając wszystkie węzły, zobacz następującą zawartość:

![Wyświetlanie pakietu LoggingLibrary Eksplorator pakietów NuGet](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> A `.nupkg` plik jest po prostu plikiem ZIP z innym rozszerzeniem. Można także sprawdzić zawartość pakietu, następnie zmieniając `.nupkg` do `.zip`, ale należy pamiętać przywrócić rozszerzenia przed przekazaniem pakietu na stronie nuget.org.

Aby udostępnić pakietu innym deweloperom, postępuj zgodnie z instrukcjami [publikowanie pakietu](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>Tematy pokrewne

- [Odwołanie Nuspec](../reference/nuspec.md)
- [Pakiety symboli](../create-packages/symbol-packages.md)
- [Przechowywanie wersji pakietów](../reference/package-versioning.md)
- [Obsługiwanie wielu wersji programu .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Zawiera właściwości programu MSBuild i obiektów docelowych w pakiecie](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)