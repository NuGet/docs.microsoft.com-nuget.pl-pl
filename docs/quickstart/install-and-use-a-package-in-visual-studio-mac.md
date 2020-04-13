---
title: Instalowanie i używanie pakietu NuGet w programie Visual Studio dla komputerów Mac
description: Samouczek instruktażowy na temat procesu instalowania i używania pakietu NuGet w projekcie programu Visual Studio dla komputerów Mac.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "70238526"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a>Szybki start: instalowanie i używanie pakietu w programie Visual Studio dla komputerów Mac

Pakiety NuGet zawierają kod wielokrotnego użytku, który inni deweloperzy udostępniają do użycia w projektach. Zobacz [Co to jest NuGet?](../What-is-NuGet.md) w tle. Pakiety są instalowane w projekcie programu Visual Studio dla komputerów Mac przy użyciu Menedżera pakietów NuGet. W tym artykule przedstawiono proces przy użyciu popularnego pakietu [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) i projektu konsoli .NET Core. Ten sam proces dotyczy każdego innego projektu platformy Xamarin lub .NET Core.

Po zainstalowaniu należy zapoznać `using <namespace>` się \<z\> pakietem w kodzie, w którym obszar nazw jest specyficzny dla używanego pakietu. Po nawiązaniu odwołania można wywołać pakiet za pośrednictwem jego interfejsu API.

> [!Tip]
> **Zacznij od nuget.org:** Przeglądanie *nuget.org* to sposób, w jaki deweloperzy platformy .NET zazwyczaj znajdują składniki, których mogą ponownie wykorzystać we własnych aplikacjach. Można wyszukiwać *nuget.org* bezpośrednio lub znaleźć i zainstalować pakiety w programie Visual Studio, jak pokazano w tym artykule. Aby uzyskać ogólne informacje, zobacz [Znajdowanie i ocenianie pakietów NuGet](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Wymagania wstępne

- Visual Studio 2019 dla komputerów Mac.

Wersję społeczności 2019 można zainstalować bezpłatnie w [visualstudio.com](https://www.visualstudio.com/) lub korzystać z wersji Professional lub Enterprise.

Jeśli używasz programu Visual Studio w systemie Windows, zobacz [Instalowanie i używanie pakietu w programie Visual Studio (tylko dla systemu Windows)](install-and-use-a-package-in-visual-studio.md).

## <a name="create-a-project"></a>Tworzenie projektu

Pakiety NuGet można zainstalować w dowolnym projekcie .NET, pod warunkiem, że pakiet obsługuje taką samą platformę docelową jak projekt.

W tym instruktażu należy użyć prostej aplikacji konsoli .NET Core Console. Utwórz projekt w programie Visual Studio dla komputerów Mac przy użyciu **> nowego rozwiązania plików...**, wybierz szablon **aplikacji konsoli .NET Core > App > Console.** Kliknij przycisk **Dalej**. Zaakceptuj wartości domyślne dla **platformy docelowej** po wyświetleniu monitu.

Visual Studio tworzy projekt, który otwiera się w Eksploratorze rozwiązań.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Dodaj pakiet Newtonsoft.Json NuGet

Aby zainstalować pakiet, należy użyć Menedżera pakietów NuGet. Po zainstalowaniu pakietu NuGet rejestruje zależność w pliku projektu `packages.config` lub pliku (w zależności od formatu projektu). Aby uzyskać więcej informacji, zobacz [Omówienie zużycia pakietów i przepływ pracy](../consume-packages/Overview-and-Workflow.md).

### <a name="nuget-package-manager"></a>Menedżer pakietów NuGet

1. W Eksploratorze **rozwiązań** kliknij prawym przyciskiem myszy pozycję Zależności i wybierz polecenie **Dodaj pakiety...**.

    ![Zarządzanie poleceniem NuGet Packages dla odwołań do projektu](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. Wybierz "nuget.org" jako **źródło pakietu** w lewym górnym rogu okna dialogowego i wyszukaj **plik Newtonsoft.Json**, wybierz ten pakiet na liście i wybierz pozycję **Dodaj pakiety...**:

    ![Lokalizowanie pakietu Newtonsoft.Json](media/QS_Use_Mac-03-NewtonsoftJson.png)

    Aby uzyskać więcej informacji na temat Menedżera pakietów NuGet, zobacz [Instalowanie pakietów i zarządzanie nimi przy użyciu programu Visual Studio dla komputerów Mac](../consume-packages/install-use-packages-visual-studio.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Korzystanie z interfejsu API Newtonsoft.Json w aplikacji

Za pomocą pakietu Newtonsoft.Json w projekcie `JsonConvert.SerializeObject` można wywołać jego metodę konwersji obiektu na ciąg czytelny dla człowieka.

1. Otwórz `Program.cs` plik (znajdujący się w panelu rozwiązania) i zastąp zawartość pliku następującym kodem:

    ```cs
    using System;
    using Newtonsoft.Json;

    namespace NuGetDemo
    {
        public class Account
        {
            public string Name { get; set; }
            public string Email { get; set; }
            public DateTime DOB { get; set; }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                Account account = new Account()
                {
                    Name = "Joe Doe",
                    Email = "joe@test.com",
                    DOB = new DateTime(1976, 3, 24)
                };
                string json = JsonConvert.SerializeObject(account);
                Console.WriteLine(json);
            }
        }
    }
    ```

1. Tworzenie i uruchamianie aplikacji przez wybranie **opcji Uruchom > Rozpocznij debugowanie:**

1. Po uruchomieniu aplikacji w konsoli pojawi się serializowane dane wyjściowe JSON:

  ![Dane wyjściowe aplikacji Console](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a>Następne kroki
Gratulujemy instalacji i korzystania z pierwszego pakietu NuGet!

> [!div class="nextstepaction"]
> [Instalowanie pakietów i zarządzanie nimi przy użyciu programu Visual Studio dla komputerów Mac](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

Aby dowiedzieć się więcej, że NuGet ma do zaoferowania, wybierz poniższe łącza.

- [Omówienie i przepływ pracy zużycia pakietów](../consume-packages/overview-and-workflow.md)
- [Odwołania do pakietu w plikach projektu](../consume-packages/package-references-in-project-files.md)
