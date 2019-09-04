---
title: Instalowanie i używanie pakietu NuGet w programie Visual Studio dla komputerów Mac
description: Samouczek instruktażowy dotyczący procesu instalowania i używania pakietu NuGet w projekcie Visual Studio dla komputerów Mac.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/03/2019
ms.locfileid: "70238526"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a>Szybki start: Instalowanie i używanie pakietu w Visual Studio dla komputerów Mac

Pakiety NuGet zawierają kod wielokrotnego użytku, który inni deweloperzy udostępnili do użycia w projektach. Zobacz, [co to jest NuGet?](../What-is-NuGet.md) w tle. Pakiety są instalowane w projekcie Visual Studio dla komputerów Mac przy użyciu Menedżera pakietów NuGet. W tym artykule przedstawiono proces przy użyciu popularnego pakietu [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) i projektu konsoli .NET Core. Ten sam proces ma zastosowanie do dowolnego innego projektu Xamarin lub .NET Core.

Po zainstalowaniu programu zapoznaj się z pakietem w `using <namespace>` kodzie \<,\> gdzie przestrzeń nazw jest specyficzna dla używanego pakietu. Po wprowadzeniu odwołania można wywołać pakiet za pomocą jego interfejsu API.

> [!Tip]
> **Zacznij od NuGet.org**: *NuGet.org* przeglądania polega na tym, że deweloperzy platformy .NET zwykle wyszukują składniki, których mogą ponownie używać w swoich aplikacjach. Możesz przeszukiwać *NuGet.org* bezpośrednio lub znajdować i instalować pakiety w programie Visual Studio, jak pokazano w tym artykule. Aby uzyskać ogólne informacje, zobacz [Znajdź i Oceń pakiety NuGet](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Wymagania wstępne

- Program Visual Studio 2019 dla komputerów Mac.

Wersję 2019 Community można zainstalować bezpłatnie z usługi [VisualStudio.com](https://www.visualstudio.com/) lub korzystać z wersji Professional lub Enterprise.

Jeśli używasz programu Visual Studio w systemie Windows, zobacz [Instalowanie i używanie pakietu w programie Visual Studio (tylko system Windows)](install-and-use-a-package-in-visual-studio.md).

## <a name="create-a-project"></a>Tworzenie projektu

Pakiety NuGet można zainstalować w dowolnym projekcie .NET, pod warunkiem, że pakiet obsługuje tę samą platformę docelową co projekt.

W tym instruktażu należy użyć prostej aplikacji konsolowej platformy .NET Core. Utwórz projekt w Visual Studio dla komputerów Mac przy użyciu **pliku > nowe rozwiązanie...** , wybierz **aplikację .NET Core > Application > szablon aplikacji konsolowej** . Kliknij przycisk **Dalej**. Po wyświetleniu monitu zaakceptuj wartości domyślne dla **platformy docelowej** .

Program Visual Studio tworzy projekt, który zostanie otwarty w Eksplorator rozwiązań.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Dodawanie pakietu NuGet Newtonsoft. JSON

Aby zainstalować pakiet, należy użyć Menedżera pakietów NuGet. Podczas instalacji pakietu NuGet rejestruje zależność w pliku projektu lub `packages.config` pliku (w zależności od formatu projektu). Aby uzyskać więcej informacji, zobacz [Omówienie użycia pakietu i przepływ pracy](../consume-packages/Overview-and-Workflow.md).

### <a name="nuget-package-manager"></a>Menedżer pakietów NuGet

1. W Eksplorator rozwiązań kliknij prawym przyciskiem myszy pozycję **zależności** i wybierz polecenie **Dodaj pakiety..** ..

    ![Polecenie zarządzania pakietami NuGet dla odwołań do projektu](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. Wybierz pozycję "nuget.org" jako **Źródło pakietu** w lewym górnym rogu okna dialogowego, a następnie wyszukaj ciąg **Newtonsoft. JSON**, wybierz ten pakiet z listy, a następnie wybierz pozycję **Dodaj pakiety...** :

    ![Lokalizowanie pakietu Newtonsoft. JSON](media/QS_Use_Mac-03-NewtonsoftJson.png)

    Aby uzyskać więcej informacji na temat Menedżera pakietów NuGet, zobacz [Instalowanie pakietów i zarządzanie nimi za pomocą Visual Studio dla komputerów Mac](../consume-packages/install-use-packages-visual-studio.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Korzystanie z interfejsu API Newtonsoft. JSON w aplikacji

Za pomocą pakietu Newtonsoft. JSON w projekcie można wywołać `JsonConvert.SerializeObject` metodę, aby przekonwertować obiekt na ciąg czytelny dla człowieka.

1. `Program.cs` Otwórz plik (znajdujący się w okienko rozwiązania) i Zastąp zawartość pliku następującym kodem:

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

1. Skompiluj i uruchom aplikację, wybierając pozycję **Uruchom, > rozpocząć debugowanie**:

1. Po uruchomieniu aplikacji zobaczysz serializowane dane wyjściowe JSON wyświetlane w konsoli programu:

  ![Dane wyjściowe aplikacji konsolowej](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a>Następne kroki
Gratulacje z myślą o instalowaniu i używaniu pierwszego pakietu NuGet!

> [!div class="nextstepaction"]
> [Instalowanie pakietów i zarządzanie nimi przy użyciu Visual Studio dla komputerów Mac](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

Aby poznać więcej informacji o tym, że pakiet NuGet jest oferowany, wybierz poniższe linki.

- [Omówienie użycia pakietu i przepływ pracy](../consume-packages/overview-and-workflow.md)
- [Odwołania do pakietu w plikach projektu](../consume-packages/package-references-in-project-files.md)
