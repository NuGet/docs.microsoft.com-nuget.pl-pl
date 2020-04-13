---
title: Instalowanie i używanie pakietu NuGet w programie Visual Studio
description: Samouczek instruktażowy na temat procesu instalowania i używania pakietu NuGet w projekcie programu Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 10bc34653d294cf70b5c91ce79a79cf6532fba1b
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "80147490"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a>Szybki start: instalowanie i używanie pakietu w programie Visual Studio (tylko w systemie Windows)

Pakiety NuGet zawierają kod wielokrotnego użytku, który inni deweloperzy udostępniają do użycia w projektach. Zobacz [Co to jest NuGet?](../What-is-NuGet.md) w tle. Pakiety są instalowane w projekcie programu Visual Studio przy użyciu Menedżera pakietów NuGet, [konsoli Menedżera pakietów](../consume-packages/install-use-packages-powershell)lub [interfejsu wiersza polecenia dotnet.](install-and-use-a-package-using-the-dotnet-cli.md) W tym artykule przedstawiono proces przy użyciu popularnego pakietu [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) i projektu Windows Presentation Foundation (WPF). Ten sam proces dotyczy każdego innego projektu .NET lub .NET Core.

Po zainstalowaniu należy zapoznać `using <namespace>` się \<z\> pakietem w kodzie, w którym obszar nazw jest specyficzny dla używanego pakietu. Po nawiązaniu odwołania można wywołać pakiet za pośrednictwem jego interfejsu API.

> [!Tip]
> **Zacznij od nuget.org:** Przeglądanie *nuget.org* to sposób, w jaki deweloperzy platformy .NET zazwyczaj znajdują składniki, których mogą ponownie wykorzystać we własnych aplikacjach. Można wyszukiwać *nuget.org* bezpośrednio lub znaleźć i zainstalować pakiety w programie Visual Studio, jak pokazano w tym artykule. Aby uzyskać ogólne informacje, zobacz [Znajdowanie i ocenianie pakietów NuGet](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Wymagania wstępne

- Visual Studio 2019 z obciążeniem .NET desktop development.

Wersję społeczności 2019 można zainstalować bezpłatnie w [visualstudio.com](https://www.visualstudio.com/) lub korzystać z wersji Professional lub Enterprise.

Jeśli używasz programu Visual Studio dla komputerów Mac, zobacz [Instalowanie i używanie pakietu w programie Visual Studio dla komputerów Mac](install-and-use-a-package-in-visual-studio-mac.md).

## <a name="create-a-project"></a>Tworzenie projektu

Pakiety NuGet można zainstalować w dowolnym projekcie .NET, pod warunkiem, że pakiet obsługuje taką samą platformę docelową jak projekt.

W tym instruktażu należy użyć prostej aplikacji WPF. Utwórz projekt w programie Visual Studio przy użyciu **programu File** > **New Project**, wpisując pozycję **.NET** w polu wyszukiwania, a następnie wybierając **aplikację WPF (.NET Framework).** Kliknij przycisk **Dalej**. Zaakceptuj wartości domyślne dla **programu Framework** po wyświetleniu monitu.

Visual Studio tworzy projekt, który otwiera się w Eksploratorze rozwiązań.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Dodaj pakiet Newtonsoft.Json NuGet

Aby zainstalować pakiet, można użyć Menedżera pakietów NuGet lub konsoli Menedżera pakietów. Po zainstalowaniu pakietu NuGet rejestruje zależność w pliku projektu `packages.config` lub pliku (w zależności od formatu projektu). Aby uzyskać więcej informacji, zobacz [Omówienie zużycia pakietów i przepływ pracy](../consume-packages/Overview-and-Workflow.md).

### <a name="nuget-package-manager"></a>Menedżer pakietów NuGet

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **pozycję Odwołania** i wybierz polecenie **Zarządzaj pakietami NuGet**.

    ![Zarządzanie poleceniem NuGet Packages dla odwołań do projektu](media/QS_Use-02-ManageNuGetPackages.png)

1. Wybierz "nuget.org" jako **źródło pakietu**, wybierz kartę **Przeglądaj,** wyszukaj **newtonsoft.Json**, wybierz ten pakiet na liście i wybierz pozycję **Zainstaluj:**

    ![Lokalizowanie pakietu Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

    Jeśli chcesz uzyskać więcej informacji na temat Menedżera pakietów NuGet, zobacz [Instalowanie pakietów i zarządzanie nimi przy użyciu programu Visual Studio](../consume-packages/install-use-packages-visual-studio.md).

1. Zaakceptuj wszelkie monity licencyjne.

1. (Tylko program Visual Studio 2017) Jeśli zostanie wyświetlony monit o wybranie formatu zarządzania pakietami, wybierz pozycję **PackageReference w pliku projektu:**

    ![Wybieranie formatu zarządzania pakietami](media/QS_Use-03b-SelectFormat.png)

1. Jeśli zostanie wyświetlony monit o przejrzenie zmian, wybierz przycisk **OK**.

### <a name="package-manager-console"></a>Konsola menedżera pakietów

1. Wybierz polecenie menu Konsola**Konsoli Menedżera pakietów** Menedżera **pakietów** >  > Narzędzia**NuGet.**

1. Po otwarciu konsoli sprawdź, czy lista rozwijana **Domyślny projekt** zawiera projekt, w którym chcesz zainstalować pakiet. Jeśli masz jeden projekt w rozwiązaniu, jest już zaznaczone.

    ![Lokalizowanie pakietu Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. Wprowadź polecenie `Install-Package Newtonsoft.Json` (patrz [Install-Package](../reference/ps-reference/ps-ref-install-package.md)). W oknie konsoli jest wyświetlane dane wyjściowe dla polecenia. Błędy zazwyczaj wskazują, że pakiet nie jest zgodny z platformą docelową projektu.

   Aby uzyskać więcej informacji na temat Konsoli Menedżera pakietów, zobacz [Instalowanie pakietów i zarządzanie nimi przy użyciu konsoli Menedżera pakietów](../consume-packages/install-use-packages-powershell.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Korzystanie z interfejsu API Newtonsoft.Json w aplikacji

Za pomocą pakietu Newtonsoft.Json w projekcie `JsonConvert.SerializeObject` można wywołać jego metodę konwersji obiektu na ciąg czytelny dla człowieka.

1. Otwórz `MainWindow.xaml` i zastąp istniejący `Grid` element następującymi elementami:

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Otwórz `MainWindow.xaml.cs` plik (znajdujący się `MainWindow.xaml` w Eksploratorze rozwiązań `MainWindow` pod węzłem) i wstaw następujący kod wewnątrz klasy:

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

1. Mimo że dodano pakiet Newtonsoft.Json do projektu, czerwony squiggles pojawia się pod, `JsonConvert` ponieważ potrzebujesz `using` instrukcji w górnej części pliku kodu:

    ```cs
    using Newtonsoft.Json;
    ```

1. Tworzenie i uruchamianie aplikacji przez naciśnięcie klawisza F5 lub wybranie **debugowania debugowania** > **startowego:**

    ![Wstępne dane wyjściowe aplikacji WPF](media/QS_Use-06-AppStart.png)

1. Wybierz na przycisku, aby zobaczyć zawartość TextBlock zastąpione niektóre JSON tekst:

    ![Dane wyjściowe aplikacji WPF po wybraniu przycisku](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a>Podobne wideo

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

Znajdź więcej filmów NuGet na [Channel 9](https://channel9.msdn.com/Series/NuGet-101) i [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="next-steps"></a>Następne kroki

Gratulujemy instalacji i korzystania z pierwszego pakietu NuGet!

> [!div class="nextstepaction"]
> [Instalowanie pakietów i zarządzanie nimi przy użyciu programu Visual Studio](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [Instalowanie pakietów i zarządzanie nimi przy użyciu Konsoli Menedżera pakietów](../consume-packages/install-use-packages-powershell.md)

Aby dowiedzieć się więcej, że NuGet ma do zaoferowania, wybierz poniższe łącza.

- [Omówienie i przepływ pracy zużycia pakietów](../consume-packages/overview-and-workflow.md)
- [Znajdowanie i wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md)
- [Odwołania do pakietu w plikach projektu](../consume-packages/package-references-in-project-files.md)
