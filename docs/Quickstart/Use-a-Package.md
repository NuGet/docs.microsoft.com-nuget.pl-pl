---
title: "Przewodnik wprowadzający do korzystania z pakietów NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/04/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Samouczek wskazówki dotyczące procesu instalacji i przy użyciu pakietu NuGet w projekcie."
keywords: "instalowania NuGet użycia pakietu NuGet, instalowanie pakietów NuGet, odwołania do pakietu NuGet, za pomocą pakietów NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 897419d1e49f12d54fbb996a2462e06e32933e65
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/31/2018
---
# <a name="install-and-use-a-package"></a>Zainstaluj i użyj pakietu

Pakiety NuGet to jednostki do ponownego użycia kodu, który inni deweloperzy udostępnić użytkownikowi do użycia w projektach. Zobacz [co to jest NuGet?](../What-is-NuGet.md) w tle.

[!INCLUDE [install-methods](../includes/install-methods.md)]

Po zakończeniu instalacji można znaleźć pakietu w kodzie z `using <namespace>` gdzie \<przestrzeni nazw\> jest przeznaczony dla pakietu używasz. Po odniesienia, można wywołać pakietu za pośrednictwem jej interfejsu API.

W pozostałej części tego tematu, który przeprowadzi Cię przez proces instalowania popularnego przy użyciu interfejsu użytkownika Menedżera pakietów [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) pakiet w projekcie systemu Windows platformy Uniwersalnej. Następnie pokaże przykładem przy użyciu pakietu. Podobne przepływu pracy są używane inne pakiety NuGet.

- [Zainstaluj wymagania wstępne](#install-pre-requisites)
- [Tworzenie projektu](#create-a-project)
- [Dodaj pakiet Newtonsoft.Json NuGet](#add-the-newtonsoftjson-nuget-package)
- [Użyj Newtonsoft.Json interfejsu API w aplikacji](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> **Rozpoczynać nuget.org**: Instalowanie pakietów z nuget.org to typowe przepływ pracy deweloperów platformy .NET Użyj, aby znaleźć mogą używać składników we własnych aplikacjach. Może zawsze wyszukiwania nuget.org bezpośrednio lub znajdować i instalować pakiety w programie Visual Studio, jak pokazano w tym temacie.

## <a name="install-pre-requisites"></a>Zainstaluj wymagania wstępne

Ten samouczek wymaga programu Visual Studio 2015 Update 3 z narzędzia dla uniwersalnych aplikacji systemu Windows lub programu Visual Studio 2017 z obciążeniem rozwoju platformy uniwersalnej systemu Windows. Jeśli masz już zainstalowanego programu Visual Studio, można uruchomić Instalatora ponownie, aby dodać narzędzia platformy uniwersalnej systemu Windows.

Można zainstalować Community edition bezpłatnie z [visualstudio.com](https://www.visualstudio.com/) lub użyj Professional lub Enterprise Edition. 

## <a name="create-a-project"></a>Tworzenie projektu

Aby zainstalować pakiet NuGet, należy niektóre rodzaju. Na podstawie NET projektu programu Visual Studio. W ramach tego przewodnika, można użyć prostej aplikacji Windows Presentation Foundation (WPF) lub platformy uniwersalnej systemu Windows (UWP):

- WPF (Windows 7 +), wybierz **Plik > Nowy > Projekt**, rozwiń węzeł **Visual C#**, wybierz pozycję **klasycznego pulpitu systemu Windows > WPF aplikacji (.NET Framework)**i wybierz **OK**.
- Dla platformy uniwersalnej systemu Windows (Windows 10), użyj **uniwersalnych systemu Windows > Pusta aplikacja (uniwersalna systemu Windows)** zamiast tego. Zaakceptuj wartości domyślne dla wersji docelowej i minimalna wersja po wyświetleniu monitu.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Dodaj pakiet Newtonsoft.Json NuGet

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **odwołania** i wybierz polecenie **Zarządzaj pakietami NuGet**.

    ![Zarządzanie pakietami NuGet polecenia dla odwołania do projektu](media/QS_Use-02-ManageNuGetPackages.png)

1. Wybierz polecenie "nuget.org" jako **źródła pakietu**, wybierz pozycję **Przeglądaj** karcie, wyszukaj **Newtonsoft.Json**, wybierz z listy tego pakietu i wybierz  **Zainstaluj**:

    ![Lokalizowanie pakiet Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. Jeśli zostanie wyświetlony monit, aby wybrać format pakietu zarządzania, wybierz między PackageReference (zalecane) i `packages.config`:

    ![Wybieranie formatu odwołanie do pakietu](media/QS_Use-03b-SelectFormat.png)

1. Jeśli zostanie wyświetlony monit o przegląd zmian dokonanych, wybierz **OK**.

1. Kliknij prawym przyciskiem myszy rozwiązanie w Eksploratorze rozwiązań i wybierz **Kompiluj rozwiązanie**. Spowoduje to przywrócenie żadnych pakietów NuGet wymienionych w obszarze **odwołania**. Aby uzyskać więcej informacji, zobacz [przywracania pakietów](../consume-packages/package-restore.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Użyj Newtonsoft.Json interfejsu API w aplikacji

Przy użyciu pakietu Newtonsoft.Json w projekcie, można wywołać jej `JsonConvert.SerializeObject` metodę, aby przekonwertować obiekt na ciąg zrozumiałą dla użytkownika.

1. Otwórz `MainWindow.xaml` (WPF) lub `MainPage.xaml` (UWP) i Zastąp istniejące `Grid` element z następujących czynności:

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Rozwiń węzeł `MainWindow.xaml` (WPF) lub `MainPage.xaml` węzła (UWP) w Eksploratorze rozwiązań Otwórz `.cs` pliku i Wstaw następujący kod w `MainWindow` lub `MainPage` klasy po konstruktora:

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

1. Nawet jeśli pakiet Newtonsoft.Json dodane do projektu, red zygzaki jest wyświetlany w obszarze `JsonConvert` ponieważ potrzebne `using` instrukcji. Umieść kursor nad podkreślony `JsonConvert` i zobaczysz żarówka wraz z opcją **Pokaż potencjalne rozwiązania**:

    ![Żarówka z możliwości Pokaż poprawki polecenia](media/QS_Use-04-ShowPotentialFixes.png)


1. Polecenie **Pokaż potencjalne rozwiązania** (lub żarówka) i wybierz pierwszy sugerowanej poprawki, `using Newtonsoft.Json;`. Spowoduje to dodanie wiersza niezbędne do początku pliku.

    ![Żarówka nadanie opcję, aby dodać using — instrukcja](media/QS_Use-05-AddUsing.png)

1. Skompilować i uruchomić aplikację, naciskając klawisz F5 lub wybranie **Debuguj > Rozpocznij debugowanie** (UWP pokazane; WPF przypomina):

    ![Początkowe dane wyjściowe aplikacji platformy uniwersalnej systemu Windows](media/QS_Use-06-AppStart.png)

1. Wybierz przycisk, aby wyświetlić zawartość obiektu TextBlock zastąpione tekst JSON:

    ![Dane wyjściowe aplikacji platformy uniwersalnej systemu Windows po wybraniu przycisku](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a>Tematy pokrewne

- [Omówienie i przepływ pracy zużycia pakietu](../consume-packages/overview-and-workflow.md)
- [Wyszukiwanie i Wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md)
- [Konfigurowanie zachowania programu NuGet](../consume-packages/configuring-nuget-behavior.md)
