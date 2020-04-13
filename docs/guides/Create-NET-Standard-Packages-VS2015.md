---
title: Tworzenie pakietów NuGet standard i platformy .NET Framework za pomocą programu Visual Studio 2015
description: End-to-end instruktaż tworzenia pakietów NuGet .NET Standard i .NET Framework przy użyciu nuget 3.x i Visual Studio 2015.
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: b16bf422e2627be3b8516a875d749639734064a9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380725"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a>Tworzenie pakietów programu .NET Standard i .NET Framework za pomocą programu Visual Studio 2015

**Uwaga:** Visual Studio 2017 jest zalecane do tworzenia bibliotek .NET Standard. Visual Studio 2015 może działać, ale narzędzia .NET Core został przeniesiony tylko do stanu wersji zapoznawczej. Zobacz [Tworzenie i publikowanie pakietu z programem Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) do pracy z NuGet 4.x+ i Visual Studio 2017.

[Biblioteka standardowa platformy .NET](/dotnet/articles/standard/library) jest formalną specyfikacją interfejsów API platformy .NET, które mają być dostępne we wszystkich środowiskach uruchomieniowych platformy .NET, co zapewnia większą jednorodność w ekosystemie platformy .NET. Biblioteka standardowa platformy .NET definiuje jednolity zestaw interfejsów API BCL (Biblioteka klas podstawowych) dla wszystkich platform .NET do zaimplementowania, niezależnie od obciążenia. Umożliwia deweloperom do tworzenia kodu, który jest użyteczny we wszystkich środowiskach uruchomieniowych .NET i zmniejsza, jeśli nie eliminuje dyrektywy kompilacji warunkowej specyficzne dla platformy w kodzie udostępnionym.

W tym przewodniku znajdziesz informacje o utworzeniu pakietu NuGet kierowanego na pakiet .NET Standard Library 1.4 lub pakietu docelowego .NET Framework 4.6. Biblioteka .NET Standard 1.4 działa w programie .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core i Mono/Xamarin. Aby uzyskać szczegółowe informacje, zobacz [tabelę mapowania .NET Standard](/dotnet/standard/net-standard#net-implementation-support) (dokumentacja.NET). W razie potrzeby można wybrać inną wersję biblioteki standardowej platformy .NET.

## <a name="prerequisites"></a>Wymagania wstępne

1. Visual Studio 2015 Update 3
1. (tylko standard NET) [Podstawowy SDK .NET](https://www.microsoft.com/net/download/)
1. Funkcja Interfejsu wiersza polecenia NuGet. Pobierz najnowszą wersję nuget.exe z [nuget.org/downloads](https://nuget.org/downloads), zapisując ją w wybranej lokalizacji. Następnie dodaj tę lokalizację do zmiennej środowiskowej PATH, jeśli jeszcze jej nie ma.

    > [!Note]
    > nuget.exe jest samo narzędzie CLI, a nie instalator, więc pamiętaj, aby zapisać pobrany plik z przeglądarki, zamiast go uruchamiać.

## <a name="create-the-class-library-project"></a>Tworzenie projektu biblioteki klas

1. W programie Visual Studio **> programem File > Project**rozwiń węzeł > systemu Windows w programie Visual **C#,** wybierz **pozycję Biblioteka klas (przenośna)**, zmień nazwę na AppLogger i wybierz **przycisk OK**.

    ![Tworzenie nowego projektu biblioteki klas](media/NetStandard-NewProject.png)

1. W wyświetlonym oknie dialogowym **Dodawanie biblioteki klas przenośnych** wybierz opcje dla `.NET Framework 4.6` i `ASP.NET Core 1.0`. (Jeśli kierowanie .NET Framework, można wybrać, które opcje są odpowiednie.)

1. Jeśli kierowanie .NET Standard, `AppLogger (Portable)` kliknij prawym przyciskiem myszy w Eksploratorze **rozwiązań,** wybierz polecenie Właściwości , wybierz kartę **Biblioteka,** a następnie wybierz pozycję **Target .NET Platform Standard** w sekcji **Kierowanie.** Ta akcja monituje o potwierdzenie, `.NET Standard 1.4` po czym można wybrać (lub inną dostępną wersję) z listy rozwijanej:

    ![Ustawianie obiektu docelowego na .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. Kliknij kartę **Kompilacja,** zmień `Release` **konfigurację** na , a następnie zaznacz pole wyboru pliku dokumentacji **XML**.

1. Dodaj kod do składnika, na przykład:

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

1. Ustaw konfigurację na Zwolnij, skompiluj projekt i sprawdź, `bin\Release` czy pliki DLL i XML są tworzone w folderze.

## <a name="create-and-update-the-nuspec-file"></a>Tworzenie i aktualizowanie pliku nuspec

1. Otwórz wiersz polecenia, przejdź do `AppLogger.csproj` folderu zawierającego folder `.sln` (jeden poziom poniżej, gdzie znajduje się plik) i uruchom polecenie NuGet, `spec` aby utworzyć plik początkowy: `AppLogger.nuspec`

    ```cli
    nuget spec
    ```

1. Otwórz `AppLogger.nuspec` w edytorze i zaktualizuj go, aby dopasować go do następujących, zastępując YOUR_NAME odpowiednią wartością. Wartość, `<id>` w szczególności, musi być unikatowa w nuget.org (zobacz konwencje nazewnictwa opisane w [Tworzenie pakietu](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number). Należy również pamiętać, że należy również zaktualizować tagi autora i opisu lub pojawi się błąd podczas kroku pakowania.

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

1. Dodaj zestawy odwołań `.nuspec` do pliku, a mianowicie biblioteki DLL i pliku IntelliSense XML:

    W przypadku kierowania na standard .NET wpisy są podobne do następujących:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    Jeśli kierowanie .NET Framework, wpisy są podobne do następujących:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. Kliknij prawym przyciskiem myszy rozwiązanie i wybierz pozycję **Build Solution,** aby wygenerować wszystkie pliki dla pakietu.

### <a name="declaring-dependencies"></a>Deklarowanie zależności

Jeśli masz żadnych zależności od innych pakietów NuGet, `<dependencies>` lista `<group>` tych w manifeście elementu z elementami. Na przykład, aby zadeklarować zależność od NewtonSoft.Json 8.0.3 lub wyższej, dodaj następujące elementy:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

Składnia atrybutu *wersji* w tym miejscu wskazuje, że wersja 8.0.3 lub powyżej jest dopuszczalna. Aby określić różne zakresy wersji, zobacz [Przechowywanie wersji pakietu](../concepts/package-versioning.md).

### <a name="adding-a-readme"></a>Dodawanie readme

Utwórz `readme.txt` plik, umieść go w folderze głównym projektu `.nuspec` i odnieś się do niego w pliku:

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

Visual Studio `readme.txt` wyświetla, gdy pakiet jest zainstalowany w projekcie. Plik nie jest wyświetlany po zainstalowaniu w projektach .NET Core lub dla pakietów, które są instalowane jako zależność.

## <a name="package-the-component"></a>Zapakuj składnik

Po zakończeniu `.nuspec` odwoływania się do wszystkich plików, które należy uwzględnić `pack` w pakiecie, możesz uruchomić polecenie:

```cli
nuget pack AppLogger.nuspec
```

To generuje `AppLogger.YOUR_NAME.1.0.0.nupkg`. Otwierając ten plik w narzędziu, takim jak [Eksplorator pakietów NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozwijając wszystkie węzły, zostanie wyświetlona następująca zawartość (pokazana dla platformy .NET Standard):

![Eksplorator pakietów NuGet z pakietem AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> Plik `.nupkg` to tylko plik ZIP z innym rozszerzeniem. Możesz również sprawdzić zawartość pakietu, `.nupkg` a `.zip`następnie, zmieniając na , ale pamiętaj, aby przywrócić rozszerzenie przed przesłaniem pakietu do nuget.org.

Aby udostępnić pakiet innym deweloperom, postępuj zgodnie z instrukcjami dotyczącymi [publikowania pakietu](../nuget-org/publish-a-package.md).

Należy `pack` pamiętać, że wymaga Mono 4.4.2 na Mac OS X i nie działa na systemach Linux. Na komputerze Mac należy również przekonwertować `.nuspec` nazwy ścieżek systemu Windows w pliku na ścieżki w stylu Uniksa.

## <a name="related-topics"></a>Powiązane tematy

- [Odwołanie .nuspec](../reference/nuspec.md)
- [Obsługa wielu wersji programu .NET framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Uwzględnij rekwizyty i obiekty docelowe MSBuild w pakiecie](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
- [Pakiety symboli](../create-packages/symbol-packages-snupkg.md)
- [Przechowywanie wersji pakietów](../concepts/package-versioning.md)
- [Dokumentacja biblioteki standardowej platformy .NET](/dotnet/articles/standard/library)
- [Przenoszenie do rdzenia net z platformy .NET Framework](/dotnet/articles/core/porting/index)
