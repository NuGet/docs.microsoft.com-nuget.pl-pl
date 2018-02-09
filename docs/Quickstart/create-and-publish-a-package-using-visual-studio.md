---
title: "Przewodnik wprowadzający do tworzenia i publikowania pakietu NuGet, za pomocą programu Visual Studio | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Samouczek wskazówki na temat tworzenia i publikowania pakietu NuGet przy użyciu programu Visual Studio 2017 r."
keywords: "Pakiet NuGet tworzenie, publikowanie pakietu NuGet, samouczek NuGet programu Visual Studio Utwórz pakiet NuGet, pakiet programu msbuild"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a4d60fdc0f27f9c4080266e212ac1cfe470ba925
ms.sourcegitcommit: eabd401616a98dda2ae6293612acb3b81b584967
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/09/2018
---
# <a name="create-and-publish-a-package-using-visual-studio"></a>Tworzenie i publikowanie pakietu programu Visual Studio

Jest to prosty proces, aby utworzyć pakiet NuGet z biblioteki klas .NET w programie Visual Studio, a następnie opublikować nuget.org za pomocą narzędzia interfejsu wiersza polecenia.

## <a name="pre-requisites"></a>Wymagania wstępne

1. Zainstalowania dowolnej wersji programu Visual Studio 2017 z [visualstudio.com](https://www.visualstudio.com/) ze wszystkimi. Obciążenia związane z sieci. Visual Studio 2017 automatycznie uwzględnia możliwości NuGet obciążenia .NET jest zainstalowany.

1. Zainstaluj `nuget.exe` interfejsu wiersza polecenia, pobierając go z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), zapisywanie, który `.exe` pliku do odpowiedniego folderu, a następnie dodanie tego folderu do Twojej zmiennej środowiskowej PATH.

    Alternatywnie Jeśli masz [.NET Core SDK](https://www.microsoft.com/net/download/) zainstalowana, można użyć `dotnet` interfejsu wiersza polecenia.

1. [Zarejestruj bezpłatne konto na nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Jeśli nie masz już. Tworzenie nowego konta wysyła wiadomość e-mail z potwierdzeniem. Aby przekazać pakiet, musisz potwierdzić konto.

## <a name="create-a-class-library-project"></a>Tworzenie projektu biblioteki klas

Można użyć istniejącego projektu biblioteki klas .NET dla kodu, który ma być pakietu lub Utwórz proste w następujący sposób:

1. W programie Visual Studio, wybierz **Plik > Nowy > Projekt**, rozwiń węzeł **Visual C# > .NET Standard** węzła, wybierz szablon "Biblioteki klas (.NET Standard)", nazwa projektu AppLogger i kliknij przycisk **OK**.

1. Kliknij prawym przyciskiem myszy na wynikowy plik projektu i wybierz **kompilacji** się upewnić, że projekt został utworzony prawidłowo. Biblioteki DLL znajduje się w folderze debugowania (lub wersji, jeśli zamiast tego kompilacji tej konfiguracji).

W rzeczywistym pakiecie NuGet oczywiście zaimplementowaniem wielu przydatnych funkcji, które inne osoby mogą tworzyć aplikacje. W ramach tego przewodnika jednak nie będzie pisania jakiegokolwiek dodatkowego kodu ponieważ biblioteki klas z szablonu jest wystarczające, aby utworzyć pakiet. Nadal Jeśli chcesz funkcjonalności kodu dla pakietu, użyj następującego polecenia:

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

> [!Tip]
> Chyba że masz powód, w przeciwnym razie wybierz .NET Standard preferowanych celem jest pakietów NuGet, ponieważ zapewnia zgodność z szeroką gamą korzystanie z projektów.

## <a name="configure-package-properties"></a>Konfigurowanie właściwości pakietu

1. Wybierz **projektu > właściwości** menu polecenie, a następnie wybierz **pakietu** karty:

    ![Właściwości pakietu NuGet w projekcie programu Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > Skompilowany dla publicznych zużycia pakietów, należy zwrócić szczególną uwagę na **tagi** właściwości, jak tagi ułatwiała innym pakietu odnaleźć i zrozumieć, jakie operacje.

1. Nadaj Unikatowy identyfikator pakietu i wypełnij wszystkie odpowiednie właściwości. Opis różnych właściwości, zobacz [odwołania do pliku .nuspec](../reference/nuspec.md). Wszystkie właściwości w tym miejscu są przekazywane do `.nuspec` manifest tworzonego projektu programu Visual Studio.

    > [!Important]
    > Podaj pakiet używany unikatowy identyfikator w nuget.org lub niezależnie od hosta można. W ramach tego przewodnika, zaleca się tym "Sample" lub "Test" w nazwie, ponieważ kolejnych kroków publikowania pakietu widocznego publicznie (chociaż jest mało prawdopodobne, każda osoba, która zostanie rzeczywiście używane).
    >
    > Jeśli spróbujesz opublikować pakiet o nazwie, która już istnieje, zostanie wyświetlony błąd.

1. Opcjonalnie: Aby wyświetlić właściwości bezpośrednio w pliku projektu, kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań i wybierz **Edytuj AppLogger.csproj**.

## <a name="run-the-pack-command"></a>Uruchom polecenie pakietu

1. Ustaw dla konfiguracji **wersji**.

1. Kliknij prawym przyciskiem myszy projekt w **Eksploratora rozwiązań** i wybierz **pakietu** polecenia:

    ![Polecenie pakietu NuGet w menu kontekstowym projektu programu Visual Studio](media/qs_create-vs-02-pack-command.png)

1. Program Visual Studio tworzy projekt i tworzy `.nupkg` pliku. Sprawdź **dane wyjściowe** szczegółowe informacje w oknie (podobnie jak poniżej), który zawiera ścieżkę do pliku pakietu. Należy też zauważyć, że skompilowany zestaw znajduje się w `bin\Release\netstandard2.0` befits jako element docelowy .NET 2.0 standardowa.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a>Opcja alternatywny: pakiet przy użyciu programu MSBuild

Przy użyciu dyskietki **pakietu** polecenia menu, NuGet 4.x+ i obsługuje MSBuild 15.1 + `pack` docelowych, jeśli projekt zawiera dane niezbędne pakietu:

```cli
msbuild /t:pack /p:Configuration=Release
```

Następnie można znaleźć pakietu w `bin\Release` folderu.

Aby uzyskać dodatkowe opcje z `msbuild /t:pack`, zobacz [NuGet pakietu i ich przywracania docelowych elementów MSBuild](../reference/msbuild-targets.md#pack-target).

## <a name="publish-the-package"></a>Publikowanie pakietu

Po utworzeniu `.nupkg` pliku opublikowaniu go za pomocą nuget.org `nuget.exe` interfejsu wiersza polecenia lub `dotnet.exe` CLI wraz z kluczem interfejsu API z nuget.org.

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Uzyskanie klucza interfejsu API

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>Publikowanie za pomocą wypychania nuget

Ten krok jest to alternatywa dla użycia `dotnet.exe`.

1. Zmień folder zawierający `.nupkg` pliku...

1. Uruchom następujące polecenie, określając nazwę pakietu i zamianę klucza wartość klucza interfejsu API:

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe wyświetla wyniki procesu publikowania:

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

Zobacz [wypychania nuget](../tools/cli-ref-push.md).

### <a name="publish-with-dotnet-nuget-push"></a>Publikowanie za pomocą wypychania nuget dotnet

Ten krok jest to alternatywa dla użycia `nuget.exe`.

[!INCLUDE[publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Publikowanie błędów

[!INCLUDE[publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Zarządzanie opublikowanego pakietu

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>Tematy pokrewne

- [Tworzenie pakietu](../create-packages/creating-a-package.md)
- [Publikowanie pakietu](../create-packages/publish-a-package.md)
- [Obsługuje wiele platform docelowych](../create-packages/supporting-multiple-target-frameworks.md)
- [Przechowywanie wersji pakietów](../reference/package-versioning.md)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
- [Dokumentacja biblioteki standardowej .NET](/dotnet/articles/standard/library)
- [Eksportowanie do platformy .NET Core z .NET Framework](/dotnet/articles/core/porting/index)