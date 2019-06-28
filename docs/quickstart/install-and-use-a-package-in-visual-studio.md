---
title: Przewodnik wprowadzający do korzystania z pakietów NuGet z poziomu programu Visual Studio
description: Samouczek wskazówki dotyczące procesu o instalowaniu i używaniu pakietu NuGet w projekcie programu Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 014b316ea03b45584406c313d46b96ad36340124
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426232"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a>Szybki start: Instalowanie i używanie pakietu w programie Visual Studio

Pakiety NuGet zawierają kodu wielokrotnego użytku, które inni deweloperzy zapewnić dostępność do użycia w projektach. Zobacz [co to jest NuGet?](../What-is-NuGet.md) w tle. Pakiety są instalowane w projekcie programu Visual Studio za pomocą interfejsu użytkownika Menedżera pakietów lub konsoli Menedżera pakietów. W tym artykule przedstawiono proces, korzystając z popularnych [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) pakietu i projektu uniwersalnej platformy Windows (UWP). Ten sam proces ma zastosowanie do innych projektów .NET lub .NET Core.

Po zakończeniu instalacji można znaleźć pakietu w kodzie za pomocą `using <namespace>` gdzie \<przestrzeni nazw\> jest właściwa dla pakietu jest używany. Gdy odniesienia, można wywołać pakiet za pośrednictwem jego interfejsu API.

> [!Tip]
> **Rozpoczynać nuget.org**: Przeglądanie nuget.org znajduje się, jak .NET deweloperzy zazwyczaj znajdują składników ponownego wykorzystania w swoich aplikacjach. Można wyszukać nuget.org bezpośrednio lub znaleźć i zainstalować pakiety w programie Visual Studio, jak pokazano w tym artykule.

## <a name="prerequisites"></a>Wymagania wstępne

- Program Visual Studio 2017 z obciążeniem programowanie uniwersalnej platformy Windows, lub
- Visual Studio 2015 Update 3 za pomocą narzędzia Tools for Universal Windows Apps.

Wersja Community 2017 można zainstalować bezpłatnie z [visualstudio.com](https://www.visualstudio.com/) lub użyj Professional lub Enterprise Edition.

Jeśli używasz programu Visual Studio dla komputerów Mac, zobacz [obejmują pakiet NuGet w projekcie](/visualstudio/mac/nuget-walkthrough).

## <a name="create-a-project"></a>Tworzenie projektu

Do każdego projektu .NET można zainstalować pakietów NuGet, pod warunkiem, że pakiet obsługuje platformę docelową tego samego jako projekt.

W ramach tego przewodnika należy użyć prostej aplikacji Universal Windows (UWP). Tworzenie projektu w programie Visual Studio przy użyciu **Plik > Nowy projekt...**  i wybierając polecenie **Windows Universal > Pusta aplikacja (Windows Universal)** . Zaakceptuj wartości domyślne dla wersji docelowej i wersję minimalną po wyświetleniu monitu.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Dodaj pakiet Newtonsoft.Json NuGet

Aby zainstalować pakiet, można użyć interfejsu użytkownika Menedżera pakietów lub konsoli Menedżera pakietów. Podczas instalowania pakietu NuGet rejestruje zależność w jednym pliku projektu lub `packages.config` pliku. Aby uzyskać więcej informacji, zobacz [pakietu zużycie omówienie i przepływ pracy](../consume-packages/Overview-and-Workflow.md).

### <a name="package-manager-ui"></a>Interfejs użytkownika menedżera pakietów

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **odwołania** i wybierz polecenie **Zarządzaj pakietami NuGet**.

    ![Zarządzanie pakietami NuGet polecenia dla odwołania do projektu](media/QS_Use-02-ManageNuGetPackages.png)

1. Wybierz pozycję "nuget.org" jako **źródła pakietu**, wybierz opcję **Przeglądaj** kartę, wyszukaj **Newtonsoft.Json**, a następnie wybierz pakiet z listy i wybierz  **Zainstaluj**:

    ![Lokalizowanie pakiet Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. Zaakceptuj wszystkie monity licencji.

1. (Visual Studio 2017) Jeśli zostanie wyświetlony monit, aby wybrać format pakiet zarządzania, wybierz opcję **packagereference v souboru projektu**:

    ![Wybieranie formatu zarządzania pakietów](media/QS_Use-03b-SelectFormat.png)

1. W przypadku wyświetlenia monitu o przegląd zmian dokonanych wybierz **OK**.

### <a name="package-manager-console"></a>Konsola menedżera pakietów

1. Wybierz **Narzędzia > Menedżer pakietów NuGet > Konsola Menedżera pakietów** polecenia menu.

1. Po otwarciu konsoli, sprawdź, czy **projekt domyślny** listy rozwijanej pokazuje projektu, do którego chcesz zainstalować pakiet. Jeśli masz jednego projektu w rozwiązaniu, jest już wybrany.

    ![Lokalizowanie pakiet Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. Wprowadź polecenie `Install-Package Newtonsoft.Json` (zobacz [Install-Package](../tools/ps-ref-install-package.md)). W oknie konsoli wyświetlane dane wyjściowe polecenia. Błędy zazwyczaj wskazują, że pakiet nie jest zgodny z platforma docelowa projektu.

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Użyj pakietu Newtonsoft.Json interfejsu API w aplikacji

Przy użyciu pakietu Newtonsoft.Json w projekcie, można wywołać jej `JsonConvert.SerializeObject` metodę, aby przekonwertować obiekt na ciąg czytelny dla człowieka.

1. Otwórz `MainPage.xaml` , zastępując istniejącą `Grid` element następującym kodem:

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Otwórz `MainPage.xaml.cs` pliku (znajdujący się w oknie Eksploratora rozwiązań pod `MainPage.xaml` węzła) i Wstaw następujący kod wewnątrz `MainPage` Konstruktor:

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

1. Mimo że pakietu Newtonsoft.Json jest dodawany do projektu, czerwone faliste linie pojawia się w obszarze `JsonConvert` ponieważ będzie potrzebny `using` instrukcji na górze pliku kodu:

    ```cs
    using Newtonsoft.Json;
    ```

1. Skompilować i uruchomić aplikację, naciskając klawisz F5 lub wybierając **Debuguj > Rozpocznij debugowanie**:

    ![Początkowe dane wyjściowe aplikacji platformy uniwersalnej systemu Windows](media/QS_Use-06-AppStart.png)

1. Wybierz przycisk, aby wyświetlić zawartość TextBlock zastąpiony tekst JSON:

    ![Dane wyjściowe aplikacji platformy uniwersalnej systemu Windows po wybraniu przycisku](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a>Pokrewne artykuły:

- [Omówienie i przepływ pracy zużycia pakietu](../consume-packages/overview-and-workflow.md)
- [Instalowanie i zarządzanie pakietami za pomocą programu Visual Studio](../tools/package-manager-ui.md)
- [Znajdowanie i wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md)
- [Typowe konfiguracje NuGet](../consume-packages/configuring-nuget-behavior.md)
