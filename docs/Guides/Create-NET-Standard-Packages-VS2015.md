---
title: "Tworzenie pakietów NuGet standardowe .NET z programem Visual Studio 2015 | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Przewodnik end-to-end tworzenia pakietów NuGet programu .NET Standard przy użyciu narzędzia NuGet 3.x i programu Visual Studio 2015."
keywords: "Tworzenie pakietu, .NET Standard pakietów, .NET Standard tabeli mapowania"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c15ffd709856fc9d5b9a9fb2fe87c0029b82650d
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/08/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a>Utwórz pakiety .NET Standard z programem Visual Studio 2015

*Dotyczy NuGet 3.x. Zobacz [tworzenie i publikowanie pakietu z programu Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) do pracy z NuGet 4.x+.*

[Biblioteki standardowej .NET](/dotnet/articles/standard/library) jest formalną specyfikację interfejsów API architektury .NET mają być dostępne na wszystkich środowisk uruchomieniowych .NET, w związku z tym ustanawianie większej jednolitości w ekosystemie .NET. Standardowa biblioteka .NET definiuje zestaw uniform BCL (Biblioteka klasy podstawowej) interfejsów API dla wszystkich platform .NET zaimplementować, niezależnie od obciążenia. Umożliwia ona deweloperom tworzyć kod, który jest można używać we wszystkich programów .NET i zmniejsza Jeśli nie eliminuje dyrektywy kompilacja warunkowa specyficzne dla platformy w kodzie udostępnionego.

Ten przewodnik przeprowadzi Cię przez proces tworzenia pakietu NuGet przeznaczonych dla platformy .NET Standard biblioteki 1.4. Takie biblioteki działa za pośrednictwem platformy .NET Framework 4.6.1, uniwersalnych systemu Windows 10 platformy .NET Core i Mono/Xamarin. Aby uzyskać więcej informacji, zobacz [.NET Standard tabeli mapowania](#net-standard-mapping-table) dalszej części tego tematu.

## <a name="prerequisites"></a>Wymagania wstępne

1. Visual Studio 2015 Update 3
1. [Oprogramowanie .NET core SDK](https://www.microsoft.com/net/download/)
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
                Console.WriteLine(text);
            }
        }
    }
    ```

1. Ustaw konfigurację do wersji, skompilować projekt i sprawdź, czy biblioteka DLL, pliki XML są tworzone w ramach `bin\Release` folderu.

## <a name="create-and-update-the-nuspec-file"></a>Tworzenie i aktualizowanie pliku .nuspec

1. Otwórz wiersz polecenia, przejdź do folderu zawierającego `AppLogger.csproj` folder (jeden poziom w dół where `.sln` pliku), i uruchom NuGet `spec` polecenie, aby utworzyć pierwszy `AppLogger.nuspec` pliku:

```cli
nuget spec
```

1. Otwórz `AppLogger.nuspec` w edytorze i zaktualizować je zgodnie z poniższym, zamieniając twoje_imie odpowiednią wartość. `<id>` Wartość, w szczególności musi być unikatowa w nuget.org (konwencje nazewnictwa opisane w temacie [utworzenie pakietu](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number). Należy również zauważyć, że należy również zaktualizować tagi autora oraz opis lub wystąpi błąd podczas wykonywania kroku pakowania.

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
    <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
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

### <a name="declaring-dependencies"></a>Deklarowanie zależności

Jeśli jest zależne od innych pakietów NuGet, listy w manifeście `<dependencies>` element z `<group>` elementów. Na przykład aby zadeklarować zależność w NewtonSoft.Json 8.0.3 lub nowszym, należy dodać:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

Składnia *wersji* tutaj wskazuje, czy w wersji 8.0.3 lub nowszy jest dopuszczalne atrybutu. Aby określić inną wersję zakresów, zapoznaj się [wersji pakietu](../reference/package-versioning.md).

### <a name="adding-a-readme"></a>Dodawanie pliku readme

Tworzenie sieci `readme.txt` pliku, umieść go w folderze głównym projektu i odwołuje się do niego w `.nuspec` pliku:

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

Visual Studio wyświetlania `readme.txt` po zainstalowaniu pakietu do projektu. Plik nie jest wyświetlane, gdy zainstalowane w projektach platformy .NET Core lub pakietów, które są zainstalowane jako zależność.

## <a name="package-the-component"></a>Pakiet składnika

Z ukończonej `.nuspec` odwołuje się do wszystkich plików, które należy uwzględnić w pakiecie, wszystko jest gotowe do uruchomienia `pack` polecenia:

```cli
nuget pack AppLogger.nuspec
```

Spowoduje to wygenerowanie `AppLogger.YOUR_NAME.1.0.0.nupkg`. Otwarcie tego pliku w narzędzia, takiego jak [Explorer pakietu NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzanie wszystkich węzłów, zobacz następującą zawartość:

![Wyświetlanie pakietu AppLogger Explorer pakietu NuGet](media/NetStandard-PackageExplorer.png)

> [!Tip]
> A `.nupkg` plik jest tylko plik ZIP zawierający inne rozszerzenie. Można również sprawdzić zawartość pakietu, następnie zmieniając `.nupkg` do `.zip`, ale pamiętaj, aby przywrócić rozszerzenia przed przekazaniem do nuget.org pakietu.

Aby udostępnić pakietu inni deweloperzy, postępuj zgodnie z instrukcjami [opublikowania pakietu](../create-packages/publish-a-package.md).

Należy pamiętać, że `pack` wymaga Mono 4.4.2 w systemie Mac OS X i nie działa w systemach Linux. Na komputerze Mac, należy także przekonwertować nazwy ścieżek systemu Windows w `.nuspec` pliku do ścieżki typu Unix.

## <a name="net-standard-mapping-table"></a>.NET standard tabeli mapowania

| Nazwa platformy | Alias |
| --- | --- |
| .NET standard | krótkich nazw netstandard | 1.0 | 1.1 | 1.2 | 1.3 | 1.4 | 1.5 | 1.6 |
| .NET Core | netcoreapp | &#x2192; | &#x2192; | &#x2192; | &#x2192; | &#x2192; | &#x2192; | 1.0 |
| .NET Framework | NET | 4.5 | 4.5.1 | 4.6 | 4.6.1 | 4.6.2 | 4.6.3 |
| Platformy mono/Xamarin | &#x2192; | &#x2192; | &#x2192; | &#x2192; | &#x2192; | &#x2192; |
| Platforma uniwersalna systemu Windows | uap | &#x2192; | &#x2192; | &#x2192; | &#x2192; |10.0 |
| Windows | win| &#x2192; | 8.0 | 8.1 |
| Windows Phone | WPA| &#x2192;| &#x2192; | 8.1 |
| Windows Phone Silverlight | WP | 8.0 |

## <a name="related-topics"></a>Tematy pokrewne

- [odwołanie .nuspec](../reference/nuspec.md)
- [Obsługa wielu wersje programu .NET framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Zawiera właściwości programu MSBuild i obiektów docelowych w pakiecie](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
- [Pakiety symboli](../create-packages/symbol-packages.md)
- [Przechowywanie wersji pakietów](../reference/package-versioning.md)
- [Dokumentacja biblioteki standardowej .NET](/dotnet/articles/standard/library)
- [Eksportowanie do platformy .NET Core z .NET Framework](/dotnet/articles/core/porting/index)
