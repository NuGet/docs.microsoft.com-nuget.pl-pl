---
title: Tworzenie i publikowanie .NET Standard Pakiet NuGet — Visual Studio w systemie Windows
description: Samouczek instruktażowy dotyczący tworzenia i publikowania pakietu .NET Standard NuGet przy użyciu programu Visual Studio w systemie Windows.
author: karann-msft
ms.author: karann
ms.date: 08/16/2019
ms.topic: quickstart
ms.openlocfilehash: 32dcc1d233154463e2950b1ce46554b1cb89956e
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231295"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>Szybki Start: Tworzenie i publikowanie pakietu NuGet przy użyciu programu Visual Studio (.NET Standard, tylko w systemie Windows)

Jest to prosty proces tworzenia pakietu NuGet z biblioteki klas .NET Standard w programie Visual Studio w systemie Windows, a następnie opublikowania jej w celu nuget.org za pomocą narzędzia interfejsu wiersza polecenia.

> [!Note]
> Jeśli używasz Visual Studio dla komputerów Mac, zapoznaj się z [informacjami](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) na temat tworzenia pakietu NuGet lub Użyj [narzędzi interfejsu wiersza polecenia dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).

## <a name="prerequisites"></a>Wymagania wstępne

1. Zainstaluj dowolną wersję programu Visual Studio 2019 z [VisualStudio.com](https://www.visualstudio.com/) z użyciem obciążenia związanego z platformą .NET Core.

1. Zainstaluj interfejs wiersza polecenia `dotnet`, jeśli nie jest jeszcze zainstalowany.

   W przypadku interfejsu wiersza polecenia `dotnet`, rozpoczynając od programu Visual Studio 2017, interfejs wiersza polecenia `dotnet` jest automatycznie instalowany z dowolnymi obciążeniami związanymi z platformą .NET Core. W przeciwnym razie zainstaluj [zestaw .NET Core SDK](https://www.microsoft.com/net/download/) , aby uzyskać `dotnet` interfejsu wiersza polecenia. Interfejs wiersza polecenia `dotnet` jest wymagany dla projektów .NET Standard, które używają [formatu stylu zestawu SDK](../resources/check-project-format.md) (atrybut zestawu SDK). Domyślny szablon biblioteki klas .NET Standard w programie Visual Studio 2017 lub nowszym, który jest używany w tym artykule, używa atrybutu SDK.
   
   > [!Important]
   > Jeśli pracujesz z projektem w stylu innym niż zestaw SDK, postępuj zgodnie z procedurami w temacie [Tworzenie i publikowanie pakietu .NET Framework (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) , aby zamiast tego utworzyć i opublikować pakiet. W tym artykule zaleca się używanie interfejsu wiersza polecenia `dotnet`. Chociaż można opublikować dowolny pakiet NuGet przy użyciu interfejsu wiersza polecenia `nuget.exe`, niektóre kroki opisane w tym artykule są specyficzne dla projektów w stylu zestawu SDK i interfejsu wiersza polecenia dotnet. Interfejs wiersza polecenia NuGet. exe jest używany dla [projektów typu non-SDK](../resources/check-project-format.md) (zwykle .NET Framework).

1. [Zarejestruj się, aby korzystać z bezpłatnego konta w usłudze NuGet.org](../nuget-org/individual-accounts.md#add-a-new-individual-account) , jeśli jeszcze go nie masz. Utworzenie nowego konta spowoduje wysłanie wiadomości e-mail z potwierdzeniem. Musisz potwierdzić konto, aby można było przekazać pakiet.

## <a name="create-a-class-library-project"></a>Tworzenie projektu biblioteki klas

Można użyć istniejącego projektu biblioteki klas .NET Standard dla kodu, który ma zostać spakowany, lub utworzyć prosty jeden w następujący sposób:

1. W programie Visual Studio wybierz pozycję **plik > nowy > projekt**, rozwiń **węzeł C# .NET standard > wizualizacji** , wybierz szablon "Biblioteka klas (.NET standard)", nazwij projekt AppLogger i kliknij przycisk **OK**.

   > [!Tip]
   > O ile nie istnieje powód, aby wybrać inny sposób, .NET Standard jest preferowanym celem dla pakietów NuGet, ponieważ zapewnia zgodność z najszerszym zakresem zużywanych projektów.

1. Kliknij prawym przyciskiem myszy plik projektu powstały i wybierz pozycję **kompilacja** , aby upewnić się, że projekt został utworzony prawidłowo. Biblioteka DLL znajduje się w folderze debugowania (lub zwolnij, jeśli zostanie utworzona ta konfiguracja).

Oczywiście w rzeczywistym pakiecie NuGet zaimplementowano wiele przydatnych funkcji, z którymi inne mogą tworzyć aplikacje. W tym instruktażu nie można jednak napisać żadnego dodatkowego kodu, ponieważ biblioteka klas z szablonu jest wystarczająca do utworzenia pakietu. Nadal, jeśli chcesz, aby w pakiecie był jakiś kod funkcjonalny, użyj następujących czynności:

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

## <a name="configure-package-properties"></a>Konfigurowanie właściwości pakietu

1. Kliknij prawym przyciskiem myszy projekt w Eksplorator rozwiązań i wybierz polecenie **Właściwości** menu, a następnie wybierz kartę **pakiet** .

   Karta **pakiet** jest wyświetlana tylko dla projektów w stylu zestawu SDK w programie Visual Studio, zwykle .NET Standard lub projektów biblioteki klas platformy .NET Core; Jeśli obiektem docelowym jest projekt o stylu innym niż zestaw SDK (zazwyczaj .NET Framework), należy [przeprowadzić migrację projektu](../consume-packages/migrate-packages-config-to-package-reference.md) lub zobaczyć opcję [Utwórz i Opublikuj pakiet .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) , aby uzyskać instrukcje krok po kroku.

    ![Właściwości pakietu NuGet w projekcie programu Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > W przypadku pakietów przeznaczonych do użycia publicznego należy zwrócić szczególną uwagę na właściwości **Tagi** , ponieważ Tagi ułatwiają innym znalezienie pakietu i zrozumienie jego działania.

1. Nadaj pakietowi unikatowy identyfikator i Wypełnij wszystkie inne żądane właściwości. Aby uzyskać mapowanie właściwości programu MSBuild (projekt w stylu zestawu SDK) na właściwości w elemencie *. nuspec*, zobacz temat [targets Pack](../reference/msbuild-targets.md#pack-target). Opisy właściwości można znaleźć w [dokumentacji pliku. nuspec](../reference/nuspec.md). Wszystkie właściwości w tym miejscu należy do manifestu `.nuspec`, który program Visual Studio tworzy dla projektu.

    > [!Important]
    > Należy nadać pakietowi identyfikator, który jest unikatowy w obrębie nuget.org lub dowolnego hosta, który jest używany. W tym instruktażu Zalecamy uwzględnienie "przykładowego" lub "testowego" w nazwie, jak w późniejszym kroku publikowania sprawia, że pakiet jest widoczny publicznie (chociaż prawdopodobnie nikt się nie używa).
    >
    > Jeśli spróbujesz opublikować pakiet o nazwie, która już istnieje, zostanie wyświetlony komunikat o błędzie.

1. Obowiązkowe Aby wyświetlić właściwości bezpośrednio w pliku projektu, kliknij prawym przyciskiem myszy projekt w Eksplorator rozwiązań i wybierz polecenie **Edytuj AppLogger. csproj**.

   Ta opcja jest dostępna tylko w programie Visual Studio 2017 dla projektów, które używają atrybutu stylu zestawu SDK. W przeciwnym razie kliknij prawym przyciskiem myszy projekt i wybierz polecenie **Zwolnij projekt**. Następnie kliknij prawym przyciskiem myszy niezaładowanego projektu i wybierz polecenie **Edytuj AppLogger. csproj**.

## <a name="run-the-pack-command"></a>Uruchom pakiet polecenie

1. Skonfiguruj konfigurację do **wydania**.

1. Kliknij prawym przyciskiem myszy projekt w **Eksplorator rozwiązań** i wybierz polecenie **pakiet** :

    ![Polecenie pakietu NuGet w menu kontekstowym projektu programu Visual Studio](media/qs_create-vs-02-pack-command.png)

    Jeśli nie widzisz polecenia **Pack** , projekt nie jest prawdopodobnie projektem w stylu zestawu SDK i musisz użyć interfejsu wiersza polecenia `nuget.exe`. [Wykonaj migrację projektu](../consume-packages/migrate-packages-config-to-package-reference.md) i użyj interfejsu wiersza polecenia `dotnet` lub zobacz [Tworzenie i publikowanie pakietu .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) , aby uzyskać instrukcje krok po kroku.

1. Program Visual Studio kompiluje projekt i tworzy plik `.nupkg`. Przejrzyj okno **dane wyjściowe** , aby uzyskać szczegółowe informacje (podobne do następujących), które zawiera ścieżkę do pliku pakietu. Należy również pamiętać, że skompilowany zestaw jest w `bin\Release\netstandard2.0` jako befits 2,0 .NET Standard celu.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="optional-generate-package-on-build"></a>Obowiązkowe Generuj pakiet podczas kompilacji

Program Visual Studio można skonfigurować tak, aby automatycznie generował pakiet NuGet podczas kompilowania projektu.

1. W Eksplorator rozwiązań kliknij prawym przyciskiem myszy projekt i wybierz polecenie **Właściwości**.

2. Na karcie **pakiet** wybierz pozycję **Generuj pakiet NuGet podczas kompilacji**.

   ![Automatycznie Generuj pakiet podczas kompilacji](media/qs_create-vs-05-generate-on-build.png)

> [!NOTE]
> Po automatycznym wygenerowaniu pakietu czas do spakowania zwiększa czas kompilacji projektu.

### <a name="optional-pack-with-msbuild"></a>(Opcjonalnie) pakiet z użyciem programu MSBuild

Jako alternatywa dla użycia polecenia menu **pakiet** NuGet 4. x + i MSBuild 15.1 + obsługuje obiekt docelowy `pack`, gdy projekt zawiera niezbędne dane pakietu. Otwórz wiersz polecenia, przejdź do folderu projektu i uruchom następujące polecenie. (Zazwyczaj chcesz uruchomić "wiersz polecenia dla deweloperów dla programu Visual Studio" z menu Start, ponieważ zostanie on skonfigurowany ze wszystkimi niezbędnymi ścieżkami dla programu MSBuild).

Aby uzyskać więcej informacji, zobacz [Tworzenie pakietu przy użyciu programu MSBuild](../create-packages/creating-a-package-msbuild.md).

## <a name="publish-the-package"></a>Publikowanie pakietu

Gdy masz plik `.nupkg`, opublikujesz go w usłudze nuget.org przy użyciu interfejsu wiersza polecenia `nuget.exe` lub interfejsu wiersza polecenia `dotnet.exe` oraz z kluczem interfejsu API uzyskanym z nuget.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Pozyskiwanie klucza interfejsu API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-the-dotnet-cli-or-nugetexe-cli"></a>Publikowanie za pomocą interfejsu wiersza polecenia dotnet lub NuGet. exe

Wybierz kartę Narzędzia interfejsu wiersza polecenia, **interfejs wiersza polecenia platformy .NET Core** (interfejs wiersza polecenia dotnet) lub **NuGet** (interfejs wiersza polecenia NuGet. exe).

# <a name="net-core-cli"></a>[.NET Core CLI](#tab/netcore-cli)

Ten krok jest zalecaną alternatywą dla korzystania z `nuget.exe`.

Przed opublikowaniem pakietu należy najpierw otworzyć wiersz polecenia.

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

# <a name="nuget"></a>[NuGet](#tab/nuget)

Ten krok stanowi alternatywę dla korzystania z `dotnet.exe`.

1. Otwórz wiersz polecenia i przejdź do folderu zawierającego plik `.nupkg`.

1. Uruchom następujące polecenie, określając nazwę pakietu (unikatowy identyfikator pakietu) i zastępując kluczową wartość kluczem interfejsu API:

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. NuGet. exe wyświetla wyniki procesu publikowania:

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

Zobacz [wypychanie NuGet](../reference/cli-reference/cli-ref-push.md).

---

### <a name="publish-errors"></a>Błędy publikowania

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Zarządzanie opublikowanym pakietem

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a>Dodawanie pliku Readme i innych plików

Aby bezpośrednio określić pliki do dołączenia do pakietu, należy edytować plik projektu i użyć właściwości `content`:

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

Będzie to zawierać plik o nazwie `readme.txt` w katalogu głównym pakietu. Program Visual Studio Wyświetla zawartość tego pliku jako zwykły tekst bezpośrednio po zainstalowaniu pakietu bezpośrednio. (Pliki Readme nie są wyświetlane dla pakietów zainstalowanych jako zależności). Na przykład poniżej przedstawiono sposób wyświetlania pliku Readme dla pakietu HtmlAgilityPack:

![Wyświetlanie pliku Readme dla pakietu NuGet podczas instalacji](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> Jedynie dodanie pliku Readme. txt w katalogu głównym projektu nie spowoduje uwzględnienia go w pakiecie wynikowym.

## <a name="related-video"></a>Pokrewne wideo

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-Visual-Studio-4-of-5/player]

Znajdź więcej filmów wideo NuGet w witrynie [Channel 9](https://channel9.msdn.com/Series/NuGet-101) i [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="related-topics"></a>Powiązane tematy

- [Tworzenie pakietu](../create-packages/creating-a-package-dotnet-cli.md)
- [Publikowanie pakietu](../nuget-org/publish-a-package.md)
- [Pakiety wersji wstępnej](../create-packages/Prerelease-Packages.md)
- [Obsługa wielu platform docelowych](../create-packages/multiple-target-frameworks-project-file.md)
- [Przechowywanie wersji pakietów](../concepts/package-versioning.md)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
- [Dokumentacja biblioteki .NET Standard](/dotnet/articles/standard/library)
- [Przenoszenie do programu .NET Core z .NET Framework](/dotnet/articles/core/porting/index)
