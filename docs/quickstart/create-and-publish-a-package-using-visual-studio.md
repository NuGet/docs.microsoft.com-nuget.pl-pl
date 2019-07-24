---
title: Tworzenie i publikowanie pakietu .NET Standard NuGet przy użyciu programu Visual Studio w systemie Windows
description: Samouczek instruktażowy dotyczący tworzenia i publikowania pakietu .NET Standard NuGet przy użyciu programu Visual Studio w systemie Windows.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: quickstart
ms.openlocfilehash: 86e71460094de9b799384db83456a68db57647af
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419922"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>Szybki start: Tworzenie i publikowanie pakietu NuGet przy użyciu programu Visual Studio (.NET Standard, tylko w systemie Windows)

Jest to prosty proces tworzenia pakietu NuGet z biblioteki klas .NET Standard w programie Visual Studio w systemie Windows, a następnie opublikowania jej w celu nuget.org za pomocą narzędzia interfejsu wiersza polecenia.

> [!Note]
> Jeśli używasz Visual Studio dla komputerów Mac, zapoznaj się z [informacjami](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) na temat tworzenia pakietu NuGet lub Użyj [narzędzi interfejsu wiersza polecenia dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).

## <a name="prerequisites"></a>Wymagania wstępne

1. Zainstaluj dowolną wersję programu Visual Studio 2017 lub nowszą z [VisualStudio.com](https://www.visualstudio.com/) przy użyciu obciążenia związanego z platformą .NET Core.

1. Jeśli nie jest jeszcze zainstalowana, zainstaluj `dotnet` interfejs wiersza polecenia.

   W przypadku `dotnet` interfejsu wiersza polecenia, rozpoczynając od programu Visual Studio 2017, interfejs wiersza polecenia jest automatycznie instalowany z dowolnymi obciążeniami związanymi z platformą .NET Core. `dotnet` W przeciwnym razie zainstaluj [zestaw .NET Core SDK](https://www.microsoft.com/net/download/) , aby uzyskać `dotnet` interfejs wiersza polecenia. Interfejs wiersza polecenia jest wymagany dla projektów .NET Standard, które używają [formatu stylu zestawu SDK](../resources/check-project-format.md) (atrybut zestawu SDK). `dotnet` Domyślny szablon biblioteki klas w programie Visual Studio 2017 lub nowszym, który jest używany w tym artykule, używa atrybutu SDK.
   
   > [!Important]
   > W tym artykule `dotnet` zaleca się używanie interfejsu wiersza polecenia. Chociaż można opublikować dowolny pakiet NuGet przy użyciu `nuget.exe` interfejsu wiersza polecenia, niektóre kroki opisane w tym artykule są specyficzne dla projektów w stylu zestawu SDK i interfejsu wiersza polecenia dotnet. Interfejs wiersza polecenia NuGet. exe jest używany dla [projektów typu non-SDK](../resources/check-project-format.md) (zwykle .NET Framework). Jeśli pracujesz z projektem w stylu innym niż zestaw SDK, postępuj zgodnie z procedurami w temacie [Tworzenie i publikowanie pakietu .NET Framework (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) , aby utworzyć i opublikować pakiet.

1. [Zarejestruj się, aby korzystać z bezpłatnego konta w usłudze NuGet.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) , jeśli jeszcze go nie masz. Utworzenie nowego konta spowoduje wysłanie wiadomości e-mail z potwierdzeniem. Musisz potwierdzić konto, aby można było przekazać pakiet.

## <a name="create-a-class-library-project"></a>Tworzenie projektu biblioteki klas

Można użyć istniejącego projektu biblioteki klas .NET Standard dla kodu, który ma zostać spakowany, lub utworzyć prosty jeden w następujący sposób:

1. W programie Visual Studio wybierz pozycję **plik > nowy > projekt**, rozwiń **węzeł C# .NET standard > wizualizacji** , wybierz szablon "Biblioteka klas (.NET standard)", nazwij projekt AppLogger i kliknij przycisk **OK**.

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

> [!Tip]
> O ile nie istnieje powód, aby wybrać inny sposób, .NET Standard jest preferowanym celem dla pakietów NuGet, ponieważ zapewnia zgodność z najszerszym zakresem zużywanych projektów.

## <a name="configure-package-properties"></a>Konfigurowanie właściwości pakietu

1. Kliknij prawym przyciskiem myszy projekt w Eksplorator rozwiązań i wybierz polecenie **Właściwości** menu, a następnie wybierz kartę **pakiet** .

   Karta **pakiet** jest wyświetlana tylko dla projektów w stylu zestawu SDK w programie Visual Studio, zwykle .NET Standard lub projektów biblioteki klas platformy .NET Core; Jeśli obiektem docelowym jest projekt o stylu innym niż zestaw SDK (zwykle .NET Framework), należy [przeprowadzić migrację projektu](../reference/migrate-packages-config-to-package-reference.md) i użyć `dotnet` interfejsu wiersza polecenia lub zobaczyć [Tworzenie i publikowanie pakietu .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) lub zobaczyć [, jak utworzyć i opublikować pakiet .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) Zamiast tego instrukcje krok po kroku.

    ![Właściwości pakietu NuGet w projekcie programu Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > W przypadku pakietów przeznaczonych do użycia publicznego należy zwrócić szczególną uwagę na właściwości **Tagi** , ponieważ Tagi ułatwiają innym znalezienie pakietu i zrozumienie jego działania.

1. Nadaj pakietowi unikatowy identyfikator i Wypełnij wszystkie inne żądane właściwości. Opis różnych właściwości można znaleźć w [dokumentacji pliku. nuspec](../reference/nuspec.md). Wszystkie właściwości w tym miejscu należy `.nuspec` do manifestu, który program Visual Studio tworzy dla projektu.

    > [!Important]
    > Należy nadać pakietowi identyfikator, który jest unikatowy w obrębie nuget.org lub dowolnego hosta, który jest używany. W tym instruktażu Zalecamy uwzględnienie "przykładowego" lub "testowego" w nazwie, jak w późniejszym kroku publikowania sprawia, że pakiet jest widoczny publicznie (chociaż prawdopodobnie nikt się nie używa).
    >
    > Jeśli spróbujesz opublikować pakiet o nazwie, która już istnieje, zostanie wyświetlony komunikat o błędzie.

1. Opcjonalne: Aby wyświetlić właściwości bezpośrednio w pliku projektu, kliknij prawym przyciskiem myszy projekt w Eksplorator rozwiązań i wybierz polecenie **Edytuj AppLogger. csproj**.

   Ta opcja jest dostępna tylko w programie Visual Studio 2017 dla projektów, które używają atrybutu stylu zestawu SDK. W przeciwnym razie kliknij prawym przyciskiem myszy projekt i wybierz polecenie **Zwolnij projekt**. Następnie kliknij prawym przyciskiem myszy niezaładowanego projektu i wybierz polecenie **Edytuj AppLogger. csproj**.

## <a name="run-the-pack-command"></a>Uruchom pakiet polecenie

1. Skonfiguruj konfigurację do **wydania**.

1. Kliknij prawym przyciskiem myszy projekt w **Eksplorator rozwiązań** i wybierz polecenie **pakiet** :

    ![Polecenie pakietu NuGet w menu kontekstowym projektu programu Visual Studio](media/qs_create-vs-02-pack-command.png)

    Jeśli nie widzisz polecenia **Pack** , projekt prawdopodobnie nie jest projektem w `nuget.exe` stylu zestawu SDK i musisz użyć interfejsu wiersza polecenia. Aby uzyskać instrukcje krok po kroku `dotnet` , należy [przeprowadzić migrację projektu](../reference/migrate-packages-config-to-package-reference.md) i użyć interfejsu wiersza polecenia lub zobaczyć, [jak utworzyć i opublikować pakiet .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) .

1. Program Visual Studio kompiluje projekt i tworzy `.nupkg` plik. Przejrzyj okno **dane wyjściowe** , aby uzyskać szczegółowe informacje (podobne do następujących), które zawiera ścieżkę do pliku pakietu. Należy również pamiętać, że skompilowany zestaw jest `bin\Release\netstandard2.0` w befits .NET Standard 2,0.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a>Opcja alternatywna: pakiet z programem MSBuild

Jako alternatywa dla użycia polecenia menu **pakiet** NuGet 4. x + i MSBuild 15.1 + obsługuje `pack` obiekt docelowy, gdy projekt zawiera niezbędne dane pakietu. Otwórz wiersz polecenia, przejdź do folderu projektu i uruchom następujące polecenie. (Zazwyczaj chcesz uruchomić "wiersz polecenia dla deweloperów dla programu Visual Studio" z menu Start, ponieważ zostanie on skonfigurowany ze wszystkimi niezbędnymi ścieżkami dla programu MSBuild).

```cli
msbuild -t:pack -p:Configuration=Release
```

Pakiet można następnie znaleźć w `bin\Release` folderze.

Aby uzyskać dodatkowe opcje `msbuild -t:pack`w programie, zobacz [pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild](../reference/msbuild-targets.md#pack-target).

## <a name="publish-the-package"></a>Publikowanie pakietu

`nuget.exe` `dotnet.exe` Po utworzeniu `.nupkg` pliku opublikuj go w usłudze NuGet.org przy użyciu interfejsu wiersza polecenia lub interfejsu wiersza polecenia oraz klucza API uzyskanego z NuGet.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Pozyskiwanie klucza interfejsu API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a>Publikowanie przy użyciu wypychania NuGet programu dotnet (interfejs wiersza polecenia dotnet)

Ten krok jest zalecaną alternatywą dla `nuget.exe`korzystania z programu.

Przed opublikowaniem pakietu należy najpierw otworzyć wiersz polecenia.

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a>Publikowanie przy użyciu wypychania NuGet (interfejs wiersza polecenia NuGet. exe)

Ten krok jest alternatywą dla korzystania `dotnet.exe`z programu.

1. Otwórz wiersz polecenia i przejdź do folderu zawierającego `.nupkg` plik.

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

### <a name="publish-errors"></a>Błędy publikowania

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Zarządzanie opublikowanym pakietem

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a>Dodawanie pliku Readme i innych plików

Aby bezpośrednio określić pliki do dołączenia do pakietu, należy edytować plik projektu i użyć `content` właściwości:

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

## <a name="related-topics"></a>Tematy pokrewne

- [Tworzenie pakietu](../create-packages/creating-a-package.md)
- [Publikowanie pakietu](../nuget-org/publish-a-package.md)
- [Pakiety wersji wstępnej](../create-packages/Prerelease-Packages.md)
- [Obsługa wielu platform docelowych](../create-packages/multiple-target-frameworks-project-file.md)
- [Przechowywanie wersji pakietów](../reference/package-versioning.md)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
- [Dokumentacja biblioteki .NET Standard](/dotnet/articles/standard/library)
- [Przenoszenie do programu .NET Core z .NET Framework](/dotnet/articles/core/porting/index)
