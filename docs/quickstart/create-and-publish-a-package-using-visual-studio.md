---
title: Tworzenie i publikowanie pakietu platformy .NET Standard, za pomocą programu Visual Studio na Windows
description: Samouczek wskazówki na temat tworzenia i publikowania pakietu NuGet programu .NET Standard za pomocą programu Visual Studio 2017 na Windows.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/18/2018
ms.topic: quickstart
ms.openlocfilehash: af6e6e015f2e4adccd99171abb37e7291551351c
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794102"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>Szybki Start: Tworzenie i publikowanie pakietu NuGet za pomocą programu Visual Studio (.NET Standard, tylko Windows)

Jest to prosty proces, aby utworzyć pakiet NuGet z standardowe biblioteki klas .NET w programie Visual Studio na Windows, a następnie opublikować go w witrynie nuget.org, za pomocą narzędzia interfejsu wiersza polecenia.

> [!Note]
> Ten przewodnik Szybki Start ma zastosowanie do programu Visual Studio 2017 for Windows tylko. Visual Studio dla komputerów Mac nie ma możliwości opisane w tym miejscu. Użyj [narzędzi interfejsu wiersza polecenia dotnet](create-and-publish-a-package-using-the-dotnet-cli.md) zamiast tego.

## <a name="prerequisites"></a>Wymagania wstępne

1. Instalowania dowolnej wersji programu Visual Studio 2017 z [visualstudio.com](https://www.visualstudio.com/) ze wszystkimi. Obciążenie związane z sieci. Po zainstalowaniu obciążenia platformy .NET, Visual Studio 2017 zawiera automatycznie możliwości NuGet.

1. Zainstaluj `nuget.exe` interfejsu wiersza polecenia, pobierając go z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), zapisywania, który `.exe` pliku do odpowiedniego folderu i dodawanie folderu do zmiennej środowiskowej PATH.

    Alternatywnie Jeśli masz [zestawu .NET Core SDK](https://www.microsoft.com/net/download/) zainstalowany, możesz użyć `dotnet` interfejsu wiersza polecenia.

1. [Zarejestruj, aby utworzyć bezpłatne konto w witrynie nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Jeśli nie masz jeszcze takiego. Tworzenie nowego konta wysyła wiadomość e-mail z potwierdzeniem. Aby można było przekazać pakiet, należy potwierdzić konto.

## <a name="create-a-class-library-project"></a>Utwórz projekt biblioteki klas

Można użyć istniejącego projektu Biblioteka klas programu .NET Standard dla kodu, który ma być pakietu lub Utwórz proste w następujący sposób:

1. W programie Visual Studio, wybierz **Plik > Nowy > Projekt**, rozwiń węzeł **Visual C# > .NET Standard** węzła, wybierz szablon "Biblioteka klas (.NET Standard)", nazwij projekt AppLogger i kliknij **OK**.

1. Kliknij prawym przyciskiem myszy, wynikowy plik projektu, a następnie wybierz pozycję **kompilacji** się upewnić, że projekt został utworzony prawidłowo. Biblioteka DLL znajduje się w folderze debugowania (lub wydania, jeśli tworzysz tę konfigurację zamiast).

W ciągu rzeczywistą pakietu NuGet oczywiście, możesz zaimplementować wiele przydatnych funkcji, które inne osoby mogą tworzyć aplikacje. W tym przewodniku jednak nie będzie pisania żadnego dodatkowego kodu ponieważ biblioteki klas na podstawie tego szablonu jest wystarczające, aby utworzyć pakiet. Jednak jeśli chcesz funkcjonalności kodu dla pakietu, użyj następującego polecenia:

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
> Chyba że istnieje powód, aby wybrać inny sposób, .NET Standard jest preferowany cel pakiety NuGet, ponieważ zapewnia zgodność z szeroką gamą wykorzystywanie projektów.

## <a name="configure-package-properties"></a>Konfigurowanie właściwości pakietu

1. Wybierz **projektu > właściwości** menu polecenia, a następnie wybierz **pakietu** kartę. ( **Pakietu** karta jest wyświetlana tylko dla projektów biblioteki klas .NET Standard; jeśli są przeznaczone dla .NET Framework, zobacz [tworzenie i publikowanie pakietu platformy .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) zamiast tego. Jeśli nie pojawia się dla projektu .NET Standard, konieczne może być aktualizacja programu Visual Studio 2017 do najnowszej wersji.)

    ![Właściwości pakietu NuGet w projekcie programu Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > Pakiety utworzone do użytku publicznego, należy zwrócić szczególną uwagę na **tagi** właściwości, jak tagi pomóc innym odnaleźć pakietu i zrozumieć, co robi.

1. Nadaj Unikatowy identyfikator pakietu i podaj żądane właściwości. Aby uzyskać opis różnych właściwości, zobacz [odwołanie do pliku .nuspec](../reference/nuspec.md). Wszystkie właściwości, w tym miejscu są przekazywane do `.nuspec` manifest przez program Visual Studio dla projektu.

    > [!Important]
    > Musisz nadać pakietu, identyfikator, który jest unikatowa w obrębie nuget.org, lub niezależnie od rodzaju hoście jest używany. W ramach tego przewodnika firma Microsoft zaleca, tym "Próbny" lub "Test" w nazwie późniejszym etapie publikowania uwidocznić pakietu publicznie (choć jest mało prawdopodobne, każda osoba będzie faktycznie używać).
    >
    > Jeśli spróbujesz opublikować pakietu o nazwie, która już istnieje, zostanie wyświetlony błąd.

1. Opcjonalnie: Aby wyświetlić właściwości bezpośrednio w pliku projektu, kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań i wybierz **Edytuj AppLogger.csproj**.

## <a name="run-the-pack-command"></a>Uruchom polecenie pakietu

1. Ustaw konfigurację **wersji**.

1. Kliknij prawym przyciskiem myszy projekt w **Eksploratora rozwiązań** i wybierz **pakiet** polecenia:

    ![Polecenie pakietu NuGet w menu kontekstowym projektu programu Visual Studio](media/qs_create-vs-02-pack-command.png)

1. Program Visual Studio tworzy projekt i tworzy `.nupkg` pliku. Sprawdź **dane wyjściowe** okno Szczegóły (podobne do następujących), który zawiera ścieżkę do pliku pakietu. Należy zauważyć, że skompilowany zestaw znajduje się w `bin\Release\netstandard2.0` befits jako obiektu docelowego .NET Standard 2.0.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a>Alternatywna opcja: pakiet za pomocą narzędzia MSBuild

Jako alternatywnego za pomocą **pakiet** polecenia menu, NuGet 4.x+ i obsługuje program MSBuild 15.1 + `pack` docelowy, jeśli projekt zawiera dane niezbędne pakietu. Otwórz wiersz polecenia, przejdź do folderu projektu i uruchom następujące polecenie. (Zazwyczaj należy start "Developer wiersz polecenia dla programu Visual Studio" z Start menu, co będzie można skonfigurować wszystkie niezbędne ścieżki programu MSBuild.)

```cli
msbuild /t:pack /p:Configuration=Release
```

Następnie można znaleźć pakietu w `bin\Release` folderu.

Aby uzyskać dodatkowe opcje z `msbuild /t:pack`, zobacz [NuGet pakowanie i przywrócić jako elementów docelowych MSBuild](../reference/msbuild-targets.md#pack-target).

## <a name="publish-the-package"></a>Publikowanie pakietu

Po utworzeniu `.nupkg` pliku opublikujesz go w witrynie nuget.org, za pomocą `nuget.exe` interfejsu wiersza polecenia lub `dotnet.exe` interfejsu wiersza polecenia oraz klucza interfejsu API uzyskanych z repozytorium nuget.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Uzyskiwanie klucza interfejsu API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>Publikowanie za pomocą wypychania nuget

Ten krok jest alternatywa dla użycia `dotnet.exe`.

1. Zmień folder zawierający `.nupkg` pliku.

1. Uruchom następujące polecenie, określając nazwę pakietu i zastępując wartość klucza swój klucz interfejsu API:

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe wyświetla wyniki proces publikowania:

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

Zobacz [wypychania nuget](../tools/cli-ref-push.md).

### <a name="publish-with-dotnet-nuget-push"></a>Publikowanie za pomocą polecenia dotnet nuget wypychania

Ten krok jest alternatywa dla użycia `nuget.exe`.

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Publikowanie błędy

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Zarządzanie opublikowany pakiet

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a>Dodawanie pliku readme i inne pliki

Aby bezpośrednio określić pliki do dołączenia w pakiecie, Edytuj plik projektu i użyj `content` właściwości:

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

To będzie zawierać plik o nazwie `readme.txt` w katalogu głównym pakietu. Visual Studio Wyświetla zawartość tego pliku jako zwykły tekst od razu po zainstalowaniu pakietu bezpośrednio. (Pliki Readme nie są wyświetlane dla pakietów zainstalowanych jako zależności). Na przykład poniżej przedstawiono sposób wyświetlania pliku readme pakietu HtmlAgilityPack:

![Wyświetlanie pliku readme podczas instalacji pakietu NuGet](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> Jedynie Dodawanie readme.txt w katalogu głównym projektu nie spowoduje jego ona dołączana do pakietu wynikowego.

## <a name="related-topics"></a>Tematy pokrewne

- [Utwórz pakiet](../create-packages/creating-a-package.md)
- [Publikowanie pakietu](../create-packages/publish-a-package.md)
- [Pakiety w wersji wstępnej](../create-packages/Prerelease-Packages.md)
- [Obsługa wielu platform docelowych](../create-packages/supporting-multiple-target-frameworks.md)
- [Przechowywanie wersji pakietów](../reference/package-versioning.md)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
- [Dokumentacja .NET biblioteki standardowej](/dotnet/articles/standard/library)
- [Eksportowanie do programu .NET Core z .NET Framework](/dotnet/articles/core/porting/index)
