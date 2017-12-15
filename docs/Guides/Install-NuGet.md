---
title: "Instalowanie narzędzi klienta NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: "Wskazówki na temat instalowania narzędzi klienta, interfejsu wiersza polecenia (CLI) i Menedżer pakietów dla programu Visual Studio."
keywords: "nuget.exe interfejsu wiersza polecenia narzędzia klienta NuGet, Menedżer pakietów NuGet, konsoli Menedżera pakietów NuGet, NuGet dla programu Visual Studio, NuGet w wersji beta kanału"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b1abb30458c9ebfb0ffb28be254efd9709a9627f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="installing-nuget-client-tools"></a>Instalowanie narzędzi klienta NuGet

> [!Tip]
> **Wyszukiwanie, aby zainstalować pakiet? Zobacz [Szybki Start - Użyj pakietu](../Quickstart/Use-a-Package.md).**

Istnieją dwa podstawowe narzędzia ułatwiających tworzenie, publikowanie i korzystać z pakietów NuGet:

1. [ **Interfejsu wiersza polecenia NuGet** ](#nuget-cli) to narzędzie wiersza polecenia dla systemu Windows, który zawiera wszystkie funkcje NuGet; może również być uruchomione na systemu Mac OS x i Linux za pomocą Mono lub za pośrednictwem interfejsu wiersza polecenia platformy .NET Core (`dotnet`).
1. [ **Menedżera pakietów NuGet w programie Visual Studio** ](#nuget-package-manager-in-visual-studio) (tylko system Windows) jest narzędziem do graficznego interfejsu użytkownika dla zarządzania pakietów i obejmuje konsolę programu PowerShell, za pomocą których można użyć pewnych poleceń NuGet bezpośrednio z poziomu programu Visual Studio. Interfejs użytkownika Menedżera pakietów i konsoli są dołączone do programu Visual Studio (w systemie Windows), 2012 lub nowszy i może zostać zainstalowany ręcznie w przypadku wcześniejszych wersji.

    Program Visual Studio dla komputerów Mac możliwości NuGet są wbudowane bezpośrednio. Zobacz [pakietu w tym NuGet w projekcie](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough) przewodnik.

    Visual Studio Code obecnie nie ma żadnych wbudowana obsługa NuGet. Użyj interfejsu wiersza polecenia NuGet lub [dotnet interfejsu wiersza polecenia](../Tools/dotnet-Commands.md).

Interfejs wiersza polecenia NuGet i Package Manager obsługuje następujące operacje:

- Pakiety wyszukiwania
- Instalowanie pakietów
- Pakiety aktualizacji
- Odinstalowania pakietów
- Przywracanie pakietów (tylko w Menedżerze pakietów interfejsu użytkownika)
- Zarządzaj źródłami NuGet

Następujące funkcje są obsługiwane tylko w przypadku interfejsu wiersza polecenia NuGet:

- Zarządzaj pakietami (nuget.org lub prywatnej źródła danych)
- Tworzenie pakietów 
- Publikowanie pakietów
- Zarządzanie pliku Nuget.Config.
- Zarządzanie pamięcią podręczną NuGet
- Replikowanie pakietu

> [!Note]
> Kolejnym narzędziem dobrej jest [Explorer pakietu NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), open source, autonomiczne narzędzie, aby wizualnie eksplorować, tworzyć i edytować pakietów NuGet. Bardzo przydatne, jest na przykład zmienić eksperymentalne Struktura pakietu bez konieczności Skompiluj ponownie pakiet zawsze.
> Obsługujący wiele platform [interfejsu wiersza polecenia platformy .NET Core](https://docs.microsoft.com/dotnet/articles/core/tools/index#installation) łańcuch narzędzi, używany do tworzenia aplikacji platformy .NET Core obsługuje kilka polecenia NuGet, takich jak usuwanie, zmienne lokalne, wypychania, pakietu i przywracania. 

## <a name="nuget-cli"></a>Interfejs wiersza polecenia NuGet

Interfejs wiersza polecenia NuGet zapewnia dostęp do wszystkich funkcji NuGet i mogą być uruchamiane w systemach Windows, Mac OS x i Linux, zgodnie z opisem w poniższych sekcjach.

### <a name="windows"></a>Windows

**Pobieranie bezpośrednie:**

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> Nuget 1.4 +, można użyć `nuget update -self` aktualizacji z istniejących nuget.exe do najnowszej wersji.

**Inne metody:**

- **Chocolatey**: Zainstaluj [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey pakietu przy użyciu [Chocolatey](http://chocolatey.org) klienta. 

    ```ps
    choco install nuget.commandline
    ```

- **Visual Studio**: Zainstaluj [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) pakietu w konsoli Menedżera pakietów w programie Visual Studio.

    > [!Note]
    > **Dla użytkowników 2.x NuGet**: ze względu na istotne zmiany wprowadzone w NuGet 3.2 [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) trwania stanu stabilnego punktów do najnowszej wersji 2.x NuGet, aby zapobiec systemów ciągłej integracji z potencjalnie przerywanie.

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a>Mac OS x i Linux

W systemie Mac OS x i Linux istnieją dwa sposoby uruchamiania interfejsu wiersza polecenia NuGet:

- Zainstaluj [.NET Core SDK](https://www.microsoft.com/net/download/core), która obejmuje podstawowych możliwości NuGet. Pliki do pobrania znajdują się na [github.com/dotnet/cli](https://github.com/dotnet/cli). Jeśli potrzebujesz możliwości na pełniejsze, następnie użyć opcji drugi poniżej do użycia `nuget.exe` z Mono.

- Zainstaluj [Mono](http://www.mono-project.com/docs/getting-started/install/) , a następnie użyj `nuget.exe` pliku wykonywalnego wiersza polecenia dla systemu Windows (w wersji 3.2 i nowszej) z [nuget.org/downloads](https://nuget.org/downloads). Systemem NuGet Mono podlega następującym ograniczeniom:

    - Przetestowany pod kątem pracy polecenia:
        - Konfiguracji
        - Usuń
        - Pomoc
        - Zainstaluj
        - list
        - Push
        - setApiKey
        - Źródeł
        - Specyfikacja

    - Częściowo pracy polecenia:
        - pakiet: współpracuje z `.nuspec` plików, ale nie pliki projektu.
        - Przywróć: współpracuje z `packages.config` i `project.json` plików, ale nie z rozwiązania (`.sln`) plików.

    - Polecenia, które nie są obsługiwane:
        - Aktualizacja

### <a name="related-topics"></a>Tematy pokrewne

- [Odwołanie do interfejsu wiersza polecenia NuGet](../tools/nuget-exe-cli-reference.md)
- [Tworzenie pakietu](../create-packages/creating-a-package.md)
- [Publikowania pakietu](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a>Menedżer pakietów NuGet w programie Visual Studio

Menedżer pakietów NuGet jest zawarte we wszystkich wersjach programu Visual Studio w systemie Windows 2012 lub nowszym. Obejmuje on interfejsu użytkownika Menedżera pakietów ([odwołania](../tools/package-manager-ui.md)), a konsola Menedżera pakietów, za pomocą którego można uzyskać dostępu do narzędzi, które pochodzą z niektórych pakietów ([odwołania](../tools/package-manager-console.md)).

Instalator programu Visual Studio 2017 obejmuje Menedżera pakietów NuGet z dowolnym obciążeniu używającego .NET. Aby zainstalować oddzielnie lub sprawdź, czy jest zainstalowany Menedżer pakietów, uruchom Instalatora programu Visual Studio 2017 i zaznacz opcję w obszarze **pojedynczych składników > narzędzia Code > Menedżera pakietów NuGet**.

> [!Note]
> Wymaga konsoli [PowerShell 2.0](http://support.microsoft.com/kb/968929), który już będzie zainstalowanego w systemach Windows 7 lub nowszy i Windows Server 2008 R2 lub nowszej.
>
> Konsola Menedżera pakietów polecenia również działać tylko w programie Visual Studio w systemie Windows. Za pomocą interfejsu wiersza polecenia NuGet poza tym środowiskiem, łącznie z programem Visual Studio for Mac i Visual Studio Code.

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a>Instalacja Menedżera pakietów dla programu Visual Studio 2010 i starszych wersji

*Te kroki nie są niezbędne dla programu Visual Studio 2012 lub nowszym, które już zawierają Menedżera pakietów.*

1. W programie Visual Studio 2010 i starszych wersji, kliknij przycisk **Narzędzia > rozszerzenia i aktualizacje**.
1. Przejdź do **Online**, następnie wyszukaj "NuGet pakietu Manager dla programu Visual Studio" i kliknij przycisk **Pobierz**.
1. W oknie dialogowym Instalatora, kliknij przycisk **zainstalować**.
1. Po zakończeniu instalacji uruchom ponownie program Visual Studio.

> [!Tip]
> Jeśli nie można użyć **rozszerzenia i aktualizacje** okna dialogowego w programie Visual Studio (na przykład zablokowanych przez serwer proxy), możesz pobrać rozszerzeń dla programu Visual Studio 2013 i 2015 bezpośrednio na [https://dist.nuget.org/ index.HTML](https://dist.nuget.org/index.html).

### <a name="updating-the-package-manager"></a>Aktualizowanie Menedżera pakietów

Dla programu Visual Studio 2015 Update 2 lub nowszego oraz Package Manager zostanie automatycznie zaktualizowany do najnowszej wersji stabilnej.

Dla programu Visual Studio 2015 Update 1 i starszych wersji, wybierz **Narzędzia > rozszerzenia i aktualizacje** polecenia, a następnie kliknij polecenie **aktualizacje** kartę, aby zobaczyć, czy dostępna jest nowa wersja Menedżera pakietów.  

### <a name="nuget-previews"></a>Podglądy NuGet

Jeśli chcesz nadchodzących funkcji NuGet w wersji zapoznawczej, zainstaluj [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), który działa side-by-side z stabilne wersje programu Visual Studio.

Należy pamiętać, że kanał poprzedniej wersji Beta NuGet (`https://dotnet.myget.org/F/nuget-beta/vsix/`) dla programu Visual Studio 2015 nie jest już używana.

Zgłaszanie problemów z dowolną wersją systemu NuGet lub Podziel się pomysłami, należy otworzyć na problemu [repozytorium NuGet GitHub](https://github.com/Nuget/Home).

### <a name="related-topics"></a>Tematy pokrewne

- [Informacje o interfejsie użytkownika Menedżera pakietów](../tools/package-manager-ui.md)
- [Odwołanie do konsoli Menedżera pakietów](../tools/package-manager-console.md)
- [Dokumentacja programu PowerShell konsoli Menedżera pakietów](../tools/powershell-reference.md)