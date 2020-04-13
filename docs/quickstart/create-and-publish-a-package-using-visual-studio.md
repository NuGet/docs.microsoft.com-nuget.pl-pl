---
title: Tworzenie i publikowanie standardowego pakietu NuGet platformy .NET — visual studio w systemie Windows
description: Samouczek instruktażowy dotyczący tworzenia i publikowania pakietu NuGet standard .NET przy użyciu programu Visual Studio w systemie Windows.
author: karann-msft
ms.author: karann
ms.date: 08/16/2019
ms.topic: quickstart
ms.openlocfilehash: 32dcc1d233154463e2950b1ce46554b1cb89956e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429032"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>Szybki start: tworzenie i publikowanie pakietu NuGet przy użyciu programu Visual Studio (.NET Standard, tylko system Windows)

Jest to prosty proces, aby utworzyć pakiet NuGet z biblioteki klas standardowych platformy .NET w programie Visual Studio w systemie Windows, a następnie opublikować go do nuget.org przy użyciu narzędzia interfejsu wiersza polecenia.

> [!Note]
> Jeśli używasz programu Visual Studio dla komputerów Mac, zapoznaj się z [tymi informacjami](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) dotyczącymi tworzenia pakietu NuGet lub użyj [narzędzi dotnet CLI.](create-and-publish-a-package-using-the-dotnet-cli.md)

## <a name="prerequisites"></a>Wymagania wstępne

1. Zainstaluj dowolną wersję programu Visual Studio 2019 z [visualstudio.com](https://www.visualstudio.com/) z obciążeniem związanym z rdzeniem .NET.

1. Jeśli nie jest jeszcze zainstalowany, `dotnet` zainstaluj cli.

   W `dotnet` przypadku interfejsu wiersza polecenia, począwszy `dotnet` od programu Visual Studio 2017, interfejsu wiersza polecenia jest automatycznie instalowany z dowolnymi obciążeniami powiązanymi z rdzeniem .NET. W przeciwnym razie zainstaluj [pakiet SDK rdzenia .NET,](https://www.microsoft.com/net/download/) aby uzyskać `dotnet` plik CLI. Cli `dotnet` jest wymagane dla projektów .NET Standard, które używają [formatu SDK stylu](../resources/check-project-format.md) (atrybut SDK). Domyślny szablon biblioteki klas .NET Standard w programie Visual Studio 2017 i nowszym, który jest używany w tym artykule, używa atrybutu SDK.
   
   > [!Important]
   > Jeśli pracujesz z projektem w stylu nie-SDK, postępuj zgodnie z procedurami w [Tworzenie i publikowanie pakietu .NET Framework (Visual Studio),](create-and-publish-a-package-using-visual-studio-net-framework.md) aby zamiast tego utworzyć i opublikować pakiet. W tym artykule zaleca się `dotnet` wiersza polecenia. Chociaż można opublikować dowolny pakiet `nuget.exe` NuGet przy użyciu interfejsu wiersza polecenia, niektóre kroki w tym artykule są specyficzne dla projektów w stylu zestawu SDK i interfejsu wiersza polecenia dotnet. Nuget.exe CLI jest używany dla [projektów w stylu innych niż SDK](../resources/check-project-format.md) (zazwyczaj .NET Framework).

1. [Zarejestruj się na darmowe konto w nuget.org](../nuget-org/individual-accounts.md#add-a-new-individual-account) jeśli jeszcze go nie masz. Utworzenie nowego konta wysyła wiadomość e-mail z potwierdzeniem. Musisz potwierdzić konto, zanim będzie można przesłać pakiet.

## <a name="create-a-class-library-project"></a>Tworzenie projektu biblioteki klas

Można użyć istniejącego projektu biblioteki klas standardowych platformy .NET dla kodu, który chcesz spakować, lub utworzyć prosty w następujący sposób:

1. W programie Visual Studio wybierz polecenie **Plik > nowy projekt >**, rozwiń węzeł Visual **C# > .NET Standard,** wybierz szablon "Biblioteka klas (.NET Standard)" , nazwij projekt AppLogger i kliknij przycisk **OK**.

   > [!Tip]
   > Jeśli nie masz powodu, aby wybrać inaczej, .NET Standard jest preferowanym obiektem docelowym dla pakietów NuGet, ponieważ zapewnia zgodność z najszerszym zakresem projektów zużywających.

1. Kliknij prawym przyciskiem myszy wynikowy plik projektu i wybierz **polecenie Build,** aby upewnić się, że projekt został prawidłowo utworzony. Biblioteka DLL znajduje się w folderze debugowania (lub Release, jeśli zamiast tego skompilujesz tę konfigurację).

W ramach prawdziwego pakietu NuGet, oczywiście, można zaimplementować wiele przydatnych funkcji, za pomocą których inni mogą tworzyć aplikacje. W tym instruktażu jednak nie będzie pisać żadnego dodatkowego kodu, ponieważ biblioteka klas z szablonu jest wystarczająca do utworzenia pakietu. Mimo to, jeśli chcesz jakiś kod funkcjonalny dla pakietu, użyj następujących czynności:

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

1. Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań, a następnie wybierz polecenie menu **Właściwości,** a następnie wybierz kartę **Pakiet.**

   Karta **Pakiet** jest wyświetlana tylko dla projektów w stylu zestawu SDK w programie Visual Studio, zazwyczaj w projektach biblioteki klas .NET Standard lub .NET Core; jeśli są przeznaczone dla projektu w stylu innego niż SDK (zazwyczaj .NET Framework), albo [migracji projektu](../consume-packages/migrate-packages-config-to-package-reference.md) lub zobacz Tworzenie [i publikowanie pakietu .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) zamiast instrukcji krok po kroku.

    ![Właściwości pakietu NuGet w projekcie programu Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > W przypadku pakietów przeznaczonych do użytku publicznego należy zwrócić szczególną uwagę na właściwość **Tagi,** ponieważ tagi pomagają innym znaleźć pakiet i zrozumieć, co robi.

1. Nadaj pakietowi unikatowy identyfikator i wypełnij inne żądane właściwości. Aby uzyskać mapowanie właściwości MSBuild (projekt w stylu zestawu SDK) do właściwości w *.nuspec*, zobacz [pack targets](../reference/msbuild-targets.md#pack-target). Opisy właściwości można znaleźć w [pliku .nuspec .](../reference/nuspec.md) Wszystkie właściwości w tym miejscu `.nuspec` przejść do manifestu, który visual studio tworzy dla projektu.

    > [!Important]
    > Należy nadać pakietowi identyfikator, który jest unikatowy w nuget.org lub niezależnie od hosta, którego używasz. W tym instruktażu zalecamy dołączenie "Przykład" lub "Test" w nazwie, ponieważ późniejszy krok publikowania powoduje, że pakiet jest publicznie widoczny (choć jest mało prawdopodobne, aby ktoś go faktycznie używał).
    >
    > Jeśli spróbujesz opublikować pakiet o nazwie, która już istnieje, zostanie wyświetlony błąd.

1. (Opcjonalnie) Aby wyświetlić właściwości bezpośrednio w pliku projektu, kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań i wybierz polecenie **Edytuj plik AppLogger.csproj**.

   Ta opcja jest dostępna tylko od programu Visual Studio 2017 dla projektów korzystających z atrybutu w stylu SDK. W przeciwnym razie kliknij prawym przyciskiem myszy projekt i wybierz polecenie **Zwolnij projekt**. Następnie kliknij prawym przyciskiem myszy niezaładowany projekt i wybierz polecenie **Edytuj plik AppLogger.csproj**.

## <a name="run-the-pack-command"></a>Uruchamianie polecenia pack

1. Ustaw konfigurację na **Zwolnij**.

1. Kliknij prawym przyciskiem myszy projekt w **Eksploratorze rozwiązań** i wybierz polecenie **Pack:**

    ![Polecenie NuGet pack w menu kontekstowym projektu programu Visual Studio](media/qs_create-vs-02-pack-command.png)

    Jeśli nie widzisz polecenia **Pack,** projekt prawdopodobnie nie jest projektem w stylu zestawu `nuget.exe` SDK i musisz użyć interfejsu wiersza polecenia. Migracji [projektu](../consume-packages/migrate-packages-config-to-package-reference.md) i użyj `dotnet` interfejsu wiersza polecenia lub zobacz Tworzenie i [publikowanie pakietu .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) zamiast instrukcji krok po kroku.

1. Visual Studio tworzy projekt i `.nupkg` tworzy plik. Sprawdź **dane wyjściowe,** aby uzyskać szczegółowe informacje (podobne do poniższych), który zawiera ścieżkę do pliku pakietu. Należy również zauważyć, że `bin\Release\netstandard2.0` zestaw zbudowany jest w jak przystało na .NET Standard 2.0 cel.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="optional-generate-package-on-build"></a>(Opcjonalnie) Generowanie pakietu na kompilacji

Program Visual Studio można skonfigurować do automatycznego generowania pakietu NuGet podczas tworzenia projektu.

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt i wybierz polecenie **Właściwości**.

2. Na karcie **Pakiet** wybierz pozycję **Generuj pakiet NuGet na kompilacji**.

   ![Automatyczne generowanie pakietu na kompilacji](media/qs_create-vs-05-generate-on-build.png)

> [!NOTE]
> Po automatycznym wygenerowaniu pakietu czas do spakowania zwiększa czas kompilacji dla projektu.

### <a name="optional-pack-with-msbuild"></a>(Opcjonalnie) opakowanie z MSBuild

Jako alternatywa przy użyciu polecenia menu **Pack,** NuGet 4.x+ i MSBuild `pack` 15.1+ obsługuje miejsce docelowe, gdy projekt zawiera niezbędne dane pakietu. Otwórz wiersz polecenia, przejdź do folderu projektu i uruchom następujące polecenie. (Zazwyczaj chcesz uruchomić "Developer Command Prompt for Visual Studio" z menu Start, ponieważ zostanie skonfigurowany ze wszystkimi niezbędnymi ścieżkami dla msbuild.)

Aby uzyskać więcej informacji, zobacz [Tworzenie pakietu przy użyciu programu MSBuild](../create-packages/creating-a-package-msbuild.md).

## <a name="publish-the-package"></a>Publikowanie pakietu

Po opublikowaniu `.nupkg` pliku można go opublikować w celu `nuget.exe` nuget.org przy `dotnet.exe` użyciu interfejsu wiersza polecenia lub interfejsu wiersza polecenia wraz z kluczem interfejsu API uzyskanym z nuget.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Uzyskaj klucz interfejsu API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-the-dotnet-cli-or-nugetexe-cli"></a>Publikowanie za pomocą interfejsu wiersza polecenia dotnet lub nuget.exe CLI

Wybierz kartę dla narzędzia interfejsu wiersza polecenia, interfejsu **.NET Core CLI** (dotnet CLI) lub **NuGet** (nuget.exe CLI).

# <a name="net-core-cli"></a>[Interfejs wiersza polecenia platformy .NET Core](#tab/netcore-cli)

Ten krok jest zalecaną `nuget.exe`alternatywą dla używania programu .

Przed opublikowaniem pakietu należy najpierw otworzyć wiersz polecenia.

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

# <a name="nuget"></a>[Nuget](#tab/nuget)

Ten krok jest alternatywą dla korzystania z programu `dotnet.exe`.

1. Otwórz wiersz polecenia i zmień folder `.nupkg` zawierający plik.

1. Uruchom następujące polecenie, określając nazwę pakietu (unikatowy identyfikator pakietu) i zastępując wartość klucza kluczem interfejsu API:

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

Zobacz [nuget push](../reference/cli-reference/cli-ref-push.md).

---

### <a name="publish-errors"></a>Błędy publikowania

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Zarządzanie opublikowanym pakietem

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a>Dodawanie pliku readme i innych plików

Aby bezpośrednio określić pliki do uwzględnienia w pakiecie, `content` edytuj plik projektu i użyj właściwości:

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

Będzie to obejmować `readme.txt` plik o nazwie w katalogu głównym pakietu. Visual Studio wyświetla zawartość tego pliku jako zwykły tekst natychmiast po zainstalowaniu pakietu bezpośrednio. (Pliki Readme nie są wyświetlane dla pakietów zainstalowanych jako zależności). Na przykład, oto jak readme dla pakietu HtmlAgilityPack pojawia się:

![Wyświetlanie pliku readme dla pakietu NuGet po instalacji](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> Samo dodanie pliku readme.txt w katalogu głównym projektu nie spowoduje, że zostanie on uwzględniony w pakiecie wynikowym.

## <a name="related-video"></a>Podobne wideo

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-Visual-Studio-4-of-5/player]

Znajdź więcej filmów NuGet na [Channel 9](https://channel9.msdn.com/Series/NuGet-101) i [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="related-topics"></a>Powiązane tematy

- [Tworzenie pakietu](../create-packages/creating-a-package-dotnet-cli.md)
- [Publikowanie pakietu](../nuget-org/publish-a-package.md)
- [Pakiety w wersji wstępnej](../create-packages/Prerelease-Packages.md)
- [Obsługa wielu platform docelowych](../create-packages/multiple-target-frameworks-project-file.md)
- [Przechowywanie wersji pakietów](../concepts/package-versioning.md)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
- [Dokumentacja biblioteki standardowej platformy .NET](/dotnet/articles/standard/library)
- [Przenoszenie do rdzenia net z platformy .NET Framework](/dotnet/articles/core/porting/index)
