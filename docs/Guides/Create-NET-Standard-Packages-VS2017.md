---
title: "Tworzenie pakietów NuGet 2.0 standardowe .NET z programu Visual Studio 2017 | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 5/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c1de334-fdc9-4e1e-8ef6-a90b3e77ff0f
description: "Przewodnik end-to-end tworzenia pakietów NuGet programu .NET Standard 2.0 przy użyciu narzędzia NuGet 4.x i Visual Studio 2017 r."
keywords: "Utwórz pakiet, .NET Standard pakietów platformy .NET Core"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 82e413119b12503336becd6019e4fa3e4ac0b1f3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a>Utwórz pakiety .NET 2.0 standardowe z programu Visual Studio 2017 r.

*Dotyczy NuGet 4.x+ i MSBuild 15 ustęp 3 + zgodnie z programu Visual Studio 2017 Update 3. W przypadku wcześniejszych wersji programu Visual Studio 2017 te instrukcje dotyczą 1.4 standardowe .NET do wersji 1.6, zmieniając \<TargetFramework\> właściwości. Zobacz też [utworzyć .NET Standard pakiety z programem Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md) do pracy z NuGet 3.x+.*

[Biblioteki standardowej .NET](https://docs.microsoft.com/dotnet/articles/standard/library) jest formalną specyfikację interfejsów API architektury .NET mają być dostępne na wszystkich środowisk uruchomieniowych .NET, w związku z tym ustanawianie większej jednolitości w ekosystemie .NET. Standardowa biblioteka .NET definiuje zestaw uniform BCL (Biblioteka klasy podstawowej) interfejsów API dla wszystkich platform .NET zaimplementować, niezależnie od obciążenia. Go umożliwia deweloperom tworzenia PCLs, które będą używać dla wszystkich programów .NET, i zmniejsza Jeśli nie eliminuje dyrektywy kompilacja warunkowa specyficzne dla platformy w kodzie udostępnionego.

Ten przewodnik przeprowadzi Cię przez proces tworzenia pakietu nuget przeznaczonych dla platformy .NET Standard biblioteki 2.0 z Visual Studio 2017 Update 3 i NuGet 4.0.

1. [Wymagania wstępne](#pre-requisites)
1. [Tworzenie projektu biblioteki klas](#create-the-netstandard-class-library-project)
1. [Edytuj metadane w pliku .csproj](#edit-metadata-in-the-csproj-file)
1. [Pakiet składnika](#package-the-component)
1. [Tematy pokrewne](#related-topics)

## <a name="pre-requisites"></a>Wymagania wstępne

W tym przewodniku wymaga programu Visual Studio 2017 Update 3 z **aplikacji dla wielu platform .NET Core** obciążenia. Można zainstalować Community edition bezpłatnie z [visualstudio.com](https://www.visualstudio.com/), lub użyj wersje Professional i Enterprise.

Wymagaj obciążenia wygląda następująco w Instalatorze programu Visual Studio:

![Obciążenie wiele platform .NET core w Instalatorze programu Visual Studio](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a>Utwórz .NET Standard projektu biblioteki klas

1. W programie Visual Studio **Plik > Nowy > projektu**, rozwiń węzeł **Visual C# > .NET Standard** węzła, wybierz opcję **biblioteki klas (Net Standard)**, Zmień nazwę na AppLogger, i Kliknij przycisk OK.

    ![Tworzenie nowego projektu biblioteki klas](media/NuGet4-02-NewProject.png)

1. Zmień konfigurację kompilacji, aby **wersji**.
1. Kliknij prawym przyciskiem myszy `AppLogger` projekt w Eksploratorze rozwiązań wybierz **właściwości**, wybierz pozycję **kompilacji** karcie, pole wyboru dla **pliku dokumentacji XML**i ustaw Nazwa pliku, aby dokładnie `AppLogger.xml`. Następnie zapisz projekt.

1. Dodaj swój kod do składnika, takich jak (która wyraźnie tylko wysyła komunikaty do konsoli):

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

1. Skompiluj projekt (przy użyciu konfiguracji Release) i sprawdź, czy biblioteka DLL, pliki XML są tworzone w ramach `bin\Release\netstandard2.0` folderu.

## <a name="edit-metadata-in-the-csproj-file"></a>Edytuj metadane w pliku .csproj

Z projektów NuGet 4.0 i .NET Core, metadane pakietów znajduje się bezpośrednio w `.csproj` plików zamiast plików zewnętrznych, takich jak `.nuspec`. Pełny opis tych metadanych znajduje się w [NuGet pakietu i ich przywracania docelowych elementów MSBuild](../schema/msbuild-targets.md#pack-target).

1. Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań wybierz **Edytuj AppLogger.csproj**, a następnie edytuj pierwszy grupę właściwości, aby uwzględnić informacje o pakiecie podobny do następującego:

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. Zapisz projekt, a następnie kliknij rozwiązanie prawym przyciskiem myszy i wybierz **Kompiluj rozwiązanie** można ponownie wygenerować wszystkich plików w pakiecie, tym razem z prawidłowych metadanych.


## <a name="package-the-component"></a>Pakiet składnika

NuGet 4.0 obsługuje obiektu docelowego pakietu przy użyciu programu MSBuild w wersji 15.1 + (łącznie z 15 MSBuild ustęp 3 jako część programu Visual Studio 2017 Update 3) Jeśli projekt zawiera metadanych potrzebny pakiet został dodany w poprzedniej sekcji. Aby wywołać program MSBuild w ten sposób, po prostu Określ cel pakietu w wierszu polecenia, w tym samym folderze co `.csproj` pliku:

    msbuild /t:pack /p:Configuration=Release

Aby uzyskać dodatkowe opcje z `msbuild /t:pack`, takich jak dołączanie plików zawartości, symbole i kod źródłowy, zobacz [NuGet pakietu i ich przywracania docelowych elementów MSBuild](../schema/msbuild-targets.md#pack-target).

W każdym przypadku generuje polecenie powyżej `AppLogger.YOUR_NAME.1.0.0.nupkg` w `bin\Release` folder domyślny, ponieważ tworzy tej konfiguracji. W przypadku pominięcia `/p` przełącznik, będzie domyślna konfiguracja `Debug`. 

Otwarcie tego pliku w narzędzia, takiego jak [Explorer pakietu NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzanie wszystkich węzłów, zobaczysz następującą zawartość:

![Wyświetlanie pakietu AppLogger Explorer pakietu NuGet](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> A `.nupkg` plik jest tylko plik ZIP zawierający inne rozszerzenie. Można również sprawdzić zawartość pakietu, następnie zmieniając `.nupkg` do `.zip`, ale pamiętaj, aby przywrócić rozszerzenia przed przekazaniem do nuget.org pakietu.

Aby udostępnić pakietu inni deweloperzy, postępuj zgodnie z instrukcjami [opublikowania pakietu](../create-packages/publish-a-package.md).

## <a name="related-topics"></a>Tematy pokrewne

- [Pakiet odwołań w plikach projektu](../consume-packages/package-references-in-project-files.md) opisano wszystkie szczegóły opisujące pakiet bezpośrednio w pliku projektu.
- [NuGet pakietu i ich przywracania docelowych elementów MSBuild](../schema/msbuild-targets.md) opisuje wszystkie opcje przy użyciu `msbuild /t:pack` do utworzenia pakietu.
- [Dokumentacja biblioteki standardowej .NET](https://docs.microsoft.com/dotnet/articles/standard/library)
- [Eksportowanie do platformy .NET Core z .NET Framework](https://docs.microsoft.com/dotnet/articles/core/porting/index)
