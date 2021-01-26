---
title: Instalowanie i używanie pakietu NuGet w programie Visual Studio
description: Samouczek instruktażowy dotyczący procesu instalowania i używania pakietu NuGet w projekcie programu Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 55f6a64d90ce8ca628d1ac5c68f8133872a214e0
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775527"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a>Szybki Start: Instalowanie i używanie pakietu w programie Visual Studio (tylko system Windows)

Pakiety NuGet zawierają kod wielokrotnego użytku, który inni deweloperzy udostępnili do użycia w projektach. Zobacz, [co to jest NuGet?](../What-is-NuGet.md) w tle. Pakiety są instalowane w projekcie programu Visual Studio za pomocą Menedżera pakietów NuGet, [konsoli Menedżera pakietów](../consume-packages/install-use-packages-powershell.md)lub [interfejsu wiersza polecenia dotnet](install-and-use-a-package-using-the-dotnet-cli.md). W tym artykule przedstawiono proces przy użyciu popularnego [Newtonsoft.Js](https://www.nuget.org/packages/Newtonsoft.Json/) pakietu i projektu Windows Presentation Foundation (WPF). Ten sam proces ma zastosowanie do dowolnego innego projektu .NET lub .NET Core.

Po zainstalowaniu programu zapoznaj się z pakietem w kodzie, `using <namespace>` gdzie \<namespace\> jest specyficzny dla używanego pakietu. Po wprowadzeniu odwołania można wywołać pakiet za pomocą jego interfejsu API.

> [!Tip]
> **Zacznij od NuGet.org**: przeglądanie *NuGet.org* polega na tym, że deweloperzy platformy .NET zwykle wyszukują składniki, których mogą ponownie używać w swoich aplikacjach. Możesz przeszukiwać *NuGet.org* bezpośrednio lub znajdować i instalować pakiety w programie Visual Studio, jak pokazano w tym artykule. Aby uzyskać ogólne informacje, zobacz [Znajdź i Oceń pakiety NuGet](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Wymagania wstępne

- Program Visual Studio 2019 z obciążeniem programistycznym dla programu .NET Desktop.

Wersję 2019 Community można zainstalować bezpłatnie z usługi [VisualStudio.com](https://www.visualstudio.com/) lub korzystać z wersji Professional lub Enterprise.

Jeśli używasz Visual Studio dla komputerów Mac, zobacz [Instalowanie i używanie pakietu w programie Visual Studio dla komputerów Mac](install-and-use-a-package-in-visual-studio-mac.md).

## <a name="create-a-project"></a>Tworzenie projektu

Pakiety NuGet można zainstalować w dowolnym projekcie .NET, pod warunkiem, że pakiet obsługuje tę samą platformę docelową co projekt.

W tym instruktażu należy użyć prostej aplikacji WPF. Utwórz projekt w programie Visual Studio przy użyciu **pliku**  >  **Nowy projekt**, wpisz **.NET** w polu wyszukiwania, a następnie wybierz **aplikację WPF (.NET Framework)**. Kliknij przycisk **Dalej**. Zaakceptuj wartości domyślne dla **struktury** po wyświetleniu monitu.

Program Visual Studio tworzy projekt, który zostanie otwarty w Eksplorator rozwiązań.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Dodaj Newtonsoft.Jsw pakiecie NuGet

Aby zainstalować pakiet, można użyć Menedżera pakietów NuGet lub konsoli Menedżera pakietów. Podczas instalacji pakietu NuGet rejestruje zależność w pliku projektu lub `packages.config` pliku (w zależności od formatu projektu). Aby uzyskać więcej informacji, zobacz [Omówienie użycia pakietu i przepływ pracy](../consume-packages/Overview-and-Workflow.md).

### <a name="nuget-package-manager"></a>Menedżer pakietów NuGet

1. W Eksplorator rozwiązań kliknij prawym przyciskiem myszy pozycję **odwołania** i wybierz polecenie **Zarządzaj pakietami NuGet**.

    ![Polecenie zarządzania pakietami NuGet dla odwołań do projektu](media/QS_Use-02-ManageNuGetPackages.png)

1. Wybierz pozycję "nuget.org" jako **Źródło pakietu**, wybierz kartę **Przeglądaj** , wyszukaj ciąg **Newtonsoft.Json**, zaznacz ten pakiet na liście, a następnie wybierz pozycję **Zainstaluj**:

    ![Lokalizowanie Newtonsoft.Jsw pakiecie](media/QS_Use-03-NewtonsoftJson.png)

    Aby uzyskać więcej informacji na temat Menedżera pakietów NuGet, zobacz [Instalowanie pakietów i zarządzanie nimi za pomocą programu Visual Studio](../consume-packages/install-use-packages-visual-studio.md).

1. Zaakceptuj wszelkie zapytanie licencji.

1. (Tylko w programie Visual Studio 2017) Jeśli zostanie wyświetlony monit o wybranie formatu zarządzania pakietami, wybierz pozycję **PackageReference w pliku projektu**:

    ![Wybieranie formatu zarządzania pakietami](media/QS_Use-03b-SelectFormat.png)

1. Jeśli zostanie wyświetlony monit o przejrzenie zmian, wybierz **przycisk OK**.

### <a name="package-manager-console"></a>Konsola menedżera pakietów

1. Wybierz kolejno pozycje **Narzędzia**  >  **Menedżer pakietów NuGet**  >  polecenie **konsola Menedżera pakietów** .

1. Po otwarciu konsoli Sprawdź, czy na liście rozwijanej **Projekt domyślny** znajduje się projekt, w którym ma zostać zainstalowany pakiet. Jeśli w rozwiązaniu istnieje pojedynczy projekt, jest on już zaznaczony.

    ![Wybierz projekt pakietu](media/QS_Use-08-Console1.png)

1. Wprowadź polecenie `Install-Package Newtonsoft.Json` (zobacz [install-package](../reference/ps-reference/ps-ref-install-package.md)). W oknie konsoli są wyświetlane dane wyjściowe polecenia. Błędy zwykle wskazują, że pakiet nie jest zgodny z platformą docelową projektu.

   Aby uzyskać więcej informacji na temat konsoli Menedżera pakietów, zobacz [Instalowanie pakietów i zarządzanie nimi za pomocą konsoli Menedżera pakietów](../consume-packages/install-use-packages-powershell.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Używanie Newtonsoft.Jsw interfejsie API w aplikacji

Za pomocą Newtonsoft.Jsw pakiecie w projekcie można wywołać `JsonConvert.SerializeObject` metodę, aby przekonwertować obiekt na ciąg czytelny dla człowieka.

1. Otwórz `MainWindow.xaml` i Zastąp istniejący `Grid` element następującym:

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Otwórz `MainWindow.xaml.cs` plik (znajdujący się w Eksplorator rozwiązań pod `MainWindow.xaml` węzłem) i Wstaw następujący kod wewnątrz `MainWindow` klasy:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@microsoft.com",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };
        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        TextBlock.Text = json;
    }
    ```

1. Mimo że dodano Newtonsoft.Jspakietu do projektu, czerwone zygzaki pojawiają się w obszarze `JsonConvert` , ponieważ potrzebujesz `using` instrukcji w górnej części pliku kodu:

    ```cs
    using Newtonsoft.Json;
    ```

1. Skompiluj i uruchom aplikację, naciskając klawisz F5 lub wybierając pozycję **Debuguj**  >  **Rozpocznij debugowanie**:

    ![Początkowe dane wyjściowe aplikacji WPF](media/QS_Use-06-AppStart.png)

1. Wybierz przycisk na przycisku, aby zobaczyć zawartość elementu TextBlock zamienionego na jakiś tekst JSON:

    ![Dane wyjściowe aplikacji WPF po wybraniu przycisku](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a>Pokrewne wideo

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

Znajdź więcej filmów wideo NuGet w witrynie [Channel 9](https://channel9.msdn.com/Series/NuGet-101) i [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="next-steps"></a>Następne kroki

Gratulacje z myślą o instalowaniu i używaniu pierwszego pakietu NuGet!

> [!div class="nextstepaction"]
> [Instalowanie pakietów i zarządzanie nimi za pomocą programu Visual Studio](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [Instalowanie pakietów i zarządzanie nimi przy użyciu konsoli Menedżera pakietów](../consume-packages/install-use-packages-powershell.md)

Aby poznać więcej informacji o tym, że pakiet NuGet jest oferowany, wybierz poniższe linki.

- [Omówienie użycia pakietu i przepływ pracy](../consume-packages/overview-and-workflow.md)
- [Znajdowanie i wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md)
- [Odwołania do pakietu w plikach projektu](../consume-packages/package-references-in-project-files.md)
