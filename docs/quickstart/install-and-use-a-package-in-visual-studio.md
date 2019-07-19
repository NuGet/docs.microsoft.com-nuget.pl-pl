---
title: Przewodnik wprowadzający do używania pakietów NuGet z poziomu programu Visual Studio
description: Samouczek instruktażowy dotyczący procesu instalowania i używania pakietu NuGet w projekcie programu Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: deedc251b605b5b58659d3b70e1ca01b19c72865
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317571"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a>Szybki start: Instalowanie i używanie pakietu w programie Visual Studio

Pakiety NuGet zawierają kod wielokrotnego użytku, który inni deweloperzy udostępnili do użycia w projektach. Zobacz, [co to jest NuGet?](../What-is-NuGet.md) w tle. Pakiety są instalowane w projekcie programu Visual Studio za pomocą interfejsu użytkownika Menedżera pakietów lub konsoli Menedżera pakietów. W tym artykule przedstawiono proces przy użyciu popularnego pakietu [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) i projektu platforma uniwersalna systemu Windows (platformy UWP). Ten sam proces ma zastosowanie do dowolnego innego projektu .NET lub .NET Core.

Po zainstalowaniu programu zapoznaj się z pakietem w `using <namespace>` kodzie \<,\> gdzie przestrzeń nazw jest specyficzna dla używanego pakietu. Po wprowadzeniu odwołania można wywołać pakiet za pomocą jego interfejsu API.

> [!Tip]
> **Zacznij od NuGet.org**: Nuget.org przeglądania polega na tym, że deweloperzy platformy .NET zwykle wyszukują składniki, których mogą ponownie używać w swoich aplikacjach. Możesz przeszukiwać nuget.org bezpośrednio lub znajdować i instalować pakiety w programie Visual Studio, jak pokazano w tym artykule.

## <a name="prerequisites"></a>Wymagania wstępne

- Program Visual Studio 2017 z obciążeniem programowanie platforma uniwersalna systemu Windows lub
- Program Visual Studio 2015 Update 3 z narzędziami dla aplikacji uniwersalnych systemu Windows.

Wersję 2017 Community można zainstalować bezpłatnie z usługi [VisualStudio.com](https://www.visualstudio.com/) lub korzystać z wersji Professional lub Enterprise.

Jeśli używasz Visual Studio dla komputerów Mac, zobacz [Dołącz pakiet NuGet do projektu](/visualstudio/mac/nuget-walkthrough).

## <a name="create-a-project"></a>Tworzenie projektu

Pakiety NuGet można zainstalować w dowolnym projekcie .NET, pod warunkiem, że pakiet obsługuje tę samą platformę docelową co projekt.

W tym instruktażu należy użyć prostej aplikacji uniwersalnej systemu Windows (platformy UWP). Utwórz projekt w programie Visual Studio przy użyciu **pliku > nowy projekt...** i wybierz pozycję **Windows Universal > Blank (aplikacja uniwersalna systemu Windows)** . Po wyświetleniu monitu zaakceptuj wartości domyślne wersji docelowej i wersji minimalnej.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Dodawanie pakietu NuGet Newtonsoft. JSON

Aby zainstalować pakiet, można użyć interfejsu użytkownika Menedżera pakietów lub konsoli Menedżera pakietów. Podczas instalacji pakietu NuGet rejestruje zależność w pliku projektu lub `packages.config` pliku. Aby uzyskać więcej informacji, zobacz [Omówienie użycia pakietu i przepływ pracy](../consume-packages/Overview-and-Workflow.md).

### <a name="package-manager-ui"></a>Interfejs użytkownika menedżera pakietów

1. W Eksplorator rozwiązań kliknij prawym przyciskiem myszy pozycję **odwołania** i wybierz polecenie **Zarządzaj pakietami NuGet**.

    ![Polecenie zarządzania pakietami NuGet dla odwołań do projektu](media/QS_Use-02-ManageNuGetPackages.png)

1. Wybierz pozycję "nuget.org" jako **Źródło pakietu**, wybierz kartę **Przeglądaj** , wyszukaj ciąg **Newtonsoft. JSON**, wybierz ten pakiet z listy, a następnie wybierz pozycję **Zainstaluj**:

    ![Lokalizowanie pakietu Newtonsoft. JSON](media/QS_Use-03-NewtonsoftJson.png)

1. Zaakceptuj wszelkie zapytanie licencji.

1. (Visual Studio 2017) Jeśli zostanie wyświetlony monit o wybranie formatu zarządzania pakietami, wybierz pozycję **PackageReference w pliku projektu**:

    ![Wybieranie formatu zarządzania pakietami](media/QS_Use-03b-SelectFormat.png)

1. Jeśli zostanie wyświetlony monit o przejrzenie zmian, wybierz **przycisk OK**.

### <a name="package-manager-console"></a>Konsola menedżera pakietów

1. Wybierz **narzędzia > Menedżer pakietów NuGet > menu konsoli Menedżera pakietów** .

1. Po otwarciu konsoli Sprawdź, czy na liście rozwijanej **Projekt domyślny** znajduje się projekt, w którym ma zostać zainstalowany pakiet. Jeśli w rozwiązaniu istnieje pojedynczy projekt, jest on już zaznaczony.

    ![Lokalizowanie pakietu Newtonsoft. JSON](media/QS_Use-08-Console1.png)

1. Wprowadź polecenie `Install-Package Newtonsoft.Json` (zobacz [install-package](../reference/ps-reference/ps-ref-install-package.md)). W oknie konsoli są wyświetlane dane wyjściowe polecenia. Błędy zwykle wskazują, że pakiet nie jest zgodny z platformą docelową projektu.

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Korzystanie z interfejsu API Newtonsoft. JSON w aplikacji

Za pomocą pakietu Newtonsoft. JSON w projekcie można wywołać `JsonConvert.SerializeObject` metodę, aby przekonwertować obiekt na ciąg czytelny dla człowieka.

1. Otwórz `MainPage.xaml` i Zastąp istniejący `Grid` element następującym:

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Otwórz plik (znajdujący się w Eksplorator rozwiązań `MainPage.xaml` pod węzłem) i Wstaw następujący kod wewnątrz `MainPage` konstruktora: `MainPage.xaml.cs`

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

1. Mimo że dodano pakiet Newtonsoft. JSON do projektu, czerwone zygzaki pojawiają się w obszarze `JsonConvert` , ponieważ `using` potrzebujesz instrukcji w górnej części pliku kodu:

    ```cs
    using Newtonsoft.Json;
    ```

1. Skompiluj i uruchom aplikację, naciskając klawisz F5 lub wybierając pozycję **debuguj > Rozpocznij debugowanie**:

    ![Początkowe dane wyjściowe aplikacji platformy UWP](media/QS_Use-06-AppStart.png)

1. Wybierz przycisk na przycisku, aby zobaczyć zawartość elementu TextBlock zamienionego na jakiś tekst JSON:

    ![Dane wyjściowe aplikacji platformy UWP po wybraniu przycisku](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a>Pokrewne artykuły:

- [Omówienie użycia pakietu i przepływ pracy](../consume-packages/overview-and-workflow.md)
- [Znajdowanie i wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md)
- [Typowe konfiguracje narzędzia NuGet](../consume-packages/configuring-nuget-behavior.md)
