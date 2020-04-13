---
title: Instalowanie narzędzi klienckich NuGet
description: Wskazówki dotyczące instalowania narzędzi klienckich, interfejsów wiersza polecenia dotnet i nuget (CLI) oraz Menedżera pakietów dla programu Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: quickstart
ms.openlocfilehash: 2769f0ef0373b26eedb4bac6242fee0e814310c5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428822"
---
# <a name="install-nuget-client-tools"></a>Instalowanie narzędzi klienta programu NuGet

> **Chcesz zainstalować pakiet? Zobacz [sposoby instalowania pakietów NuGet](consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).**

Aby pracować z NuGet, jako konsument pakietu lub twórca, można użyć narzędzi interfejsu wiersza polecenia (CLI), a także funkcji NuGet w programie Visual Studio. W tym artykule pokrótce opisano możliwości różnych narzędzi, sposób ich instalowania i ich [dostępność funkcji porównawczych.](#feature-availability) Aby rozpocząć korzystanie z pakietu NuGet do korzystania z pakietów, zobacz [Instalowanie i używanie pakietu (dotnet CLI)](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) oraz [Instalowanie i używanie pakietu (Visual Studio)](quickstart/install-and-use-a-package-in-visual-studio.md). Aby rozpocząć tworzenie pakietów NuGet, zobacz [Tworzenie i publikowanie pakietu NET Standard (dotnet CLI)](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) oraz [Tworzenie i publikowanie pakietu NET Standard (Visual Studio).](quickstart/create-and-publish-a-package-using-visual-studio.md)

| Narzędzie&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Opis | Pobierz&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [plik dotnet.exe](#dotnetexe-cli) | Narzędzie INTERFEJSU WIERSZA dla bibliotek .NET Core i .NET Standard oraz dla każdego [projektu w stylu zestawu SDK,](resources/check-project-format.md) takiego jak ten przeznaczony dla platformy .NET Framework. Dołączony do .NET Core SDK i zapewnia podstawowe funkcje NuGet na wszystkich platformach. (Począwszy od programu Visual Studio 2017, dotnet interfejsu wiersza polecenia jest automatycznie instalowany z dowolnymi obciążeniami związanymi z rdzeniem .NET.)| [Zestaw SDK dla platformy .NET Core](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | Narzędzie interfejsu wiersza polecenia dla bibliotek programu .NET Framework i dla każdego [projektu w stylu innego niż SDK,](resources/check-project-format.md) takiego jak ten przeznaczony dla bibliotek .NET Standard. Zapewnia wszystkie funkcje NuGet w systemie Windows, zapewnia większość funkcji na komputerach Mac i Linux podczas uruchamiania w obszarze Mono. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Program Visual Studio](#visual-studio) | W systemie Windows **Menedżer pakietów NuGet** jest dołączony do programu Visual Studio 2012 i nowszych. Visual Studio udostępnia [interfejs użytkownika Menedżera pakietów](consume-packages/install-use-packages-visual-studio.md) i [konsoli Menedżera pakietów](consume-packages/install-use-packages-powershell.md), za pośrednictwem którego można uruchomić większość operacji NuGet. | [Program Visual Studio](https://www.visualstudio.com/downloads/) |
| [Visual Studio dla komputerów Mac](/visualstudio/mac/nuget-walkthrough) | Na komputerze Mac niektóre funkcje NuGet są wbudowane bezpośrednio. Konsola Menedżera pakietów nie jest obecnie dostępna. Aby uzyskać inne możliwości, `nuget.exe` użyj narzędzi lub interfejsu wiersza `dotnet.exe` polecenia.  | [Visual Studio dla komputerów Mac](https://visualstudio.microsoft.com/vs/mac/) |
| [Visual Studio Code](https://code.visualstudio.com/docs) | W systemie Windows, Mac lub Linux funkcje NuGet są dostępne `dotnet.exe` `nuget.exe` za pośrednictwem rozszerzeń portalu Marketplace lub narzędzi interfejsu wiersza polecenia. | [Visual Studio Code](https://code.visualstudio.com/Download/)|

[NARZĘDZIE SIECI INSTALACYJNE MSBuild](reference/msbuild-targets.md) zapewnia również możliwość przywracania i tworzenia pakietów, co jest przydatne przede wszystkim na serwerach kompilacji. MSBuild nie jest narzędziem ogólnego przeznaczenia do pracy z NuGet.

Polecenia konsoli Menedżera pakietów działają tylko w programie Visual Studio w systemie Windows i nie działają w innych środowiskach programu PowerShell.

## <a name="visual-studio"></a>Visual Studio
### <a name="install-on-visual-studio-2017-and-newer"></a>Instalowanie w programie Visual Studio 2017 i nowszych
Począwszy od programu Visual Studio 2017 instalator zawiera Menedżera pakietów NuGet z dowolnym obciążeniem, które wykorzystuje .NET. Aby zainstalować oddzielnie lub sprawdzić, czy Menedżer pakietów jest zainstalowany, uruchom instalator programu Visual Studio i zaznacz opcję w obszarze **Narzędzia poszczególnych składników > Kod > Menedżer pakietów NuGet**.

### <a name="install-on-visual-studio-2015-and-older"></a>Instalowanie w programie Visual Studio 2015 i starszych
Rozszerzenia NuGet dla programu Visual Studio 2013 i 2015 można pobrać z programu [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).

W programie Visual Studio 2010 i wcześniejszych zainstaluj rozszerzenie "Menedżer pakietów NuGet dla programu Visual Studio". Uwaga: jeśli nie widzisz rozszerzenia na pierwszej stronie wyników wyszukiwania, spróbuj zmienić menu rozwijane Sortuj według na "Większość pobrań" lub sortowanie alfabetyczne.

## <a name="cli-tools"></a>Narzędzia cli
Można użyć interfejsu `dotnet` wiersza `nuget.exe` polecenia lub interfejsu wiersza polecenia do obsługi funkcji NuGet w IDE. Plik `dotnet` wiersza polecenia jest instalowany z niektórymi obciążeniami programu Visual Studio, takimi jak .NET Core. Wiersz `nuget.exe` polecenia musi być zainstalowany oddzielnie, jak opisano wcześniej.

Dwa narzędzia NuGet `dotnet.exe` CLI `nuget.exe`są i . Zobacz [dostępność funkcji](#feature-availability) dla porównania.

* Aby kierować na obiekt .NET Core lub .NET Standard, użyj interfejsu wiersza polecenia dotnet. Cli `dotnet` jest wymagane dla formatu projektu w stylu SDK, który używa [atrybutu SDK](/dotnet/core/tools/csproj#additions).
* Aby kierować .NET Framework (tylko projekt w stylu `nuget.exe` nieskładki), należy użyć interfejsu wiersza polecenia. Jeśli projekt jest migrowany z `packages.config` do PackageReference, użyj dotnet INTERFEJSU WIERSZA POLECENIA.

### <a name="dotnetexe-cli"></a>interfejsu wiersza polecenia dotnet.exe

Interfejs wiersza polecenia .NET Core `dotnet.exe`2.0, działa na wszystkich platformach (Windows, Mac i Linux) i udostępnia podstawowe funkcje NuGet, takie jak instalowanie, przywracanie i publikowanie pakietów. `dotnet`zapewnia bezpośrednią integrację z plikami `.csproj`projektu .NET Core (na przykład), co jest pomocne w większości scenariuszy. `dotnet`jest również zbudowany bezpośrednio dla każdej platformy i nie wymaga zainstalowania Mono.

Instalacja:

- Na komputerach deweloperów zainstaluj zestaw [SDK rdzenia .NET](https://aka.ms/dotnetcoregs). Począwszy od programu Visual Studio 2017, dotnet interfejsu wiersza polecenia jest automatycznie instalowany z dowolnego .NET Core obciążeń związanych.
- W przypadku serwerów kompilacji postępuj zgodnie z instrukcjami [dotyczącymi korzystania z zestawu .NET Core SDK i narzędzi w trybie ciągłej integracji](/dotnet/core/tools/using-ci-with-cli).

Aby dowiedzieć się, jak używać podstawowych poleceń z dotnet CLI, zobacz [Instalowanie i używanie pakietów przy użyciu interfejsu wiersza polecenia dotnet](consume-packages/install-use-packages-dotnet-cli.md).

### <a name="nugetexe-cli"></a>Interfejs wiersza polecenia nuget.exe

Cli, `nuget.exe` `nuget.exe`, jest narzędziem wiersza polecenia dla systemu Windows, który zapewnia wszystkie możliwości NuGet; może być również uruchamiany na Mac OSX i Linux przy użyciu [Mono](https://www.mono-project.com/docs/getting-started/install/) z pewnymi ograniczeniami.

Aby dowiedzieć się, jak `nuget.exe` używać podstawowych poleceń z wierszem polecenia, zobacz [Instalowanie i używanie pakietów przy użyciu pliku wiersza polecenia nuget.exe](consume-packages/install-use-packages-nuget-cli.md).

Instalacja:

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> Użyj `nuget update -self` w systemie Windows, aby zaktualizować istniejący program nuget.exe do najnowszej wersji.

> [!Note]
> Najnowsza zalecana funkcja NuGet `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe`CLI jest zawsze dostępna w pliku . Dla celów zgodności ze starszymi systemami ciągłej `https://nuget.org/nuget.exe` integracji, poprzedni adres URL, obecnie zapewnia [przestarzałe narzędzie 2.8.6 CLI](https://github.com/NuGet/NuGetGallery/issues/5381).

## <a name="feature-availability"></a>Dostępność funkcji

| Funkcja | Interfejs wiersza polecenia dotnet | nuget CLI (Windows) | nuget CLI (Mono) | Visual Studio (Windows) | Visual Studio for Mac |
| --- | --- | --- | --- | --- | --- |
| Wyszukiwanie pakietów |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Instalowanie/odinstalowywanie pakietów | &#10004; | &#10004; ust. | &#10004; | &#10004; | &#10004; |
| Aktualizuj pakiety | &#10004; | &#10004; | | &#10004; | &#10004; |
| Przywracanie pakietów | &#10004; | &#10004; | &#10004; ust. | &#10004; | &#10004; |
| Zarządzanie źródłami pakietów (źródłami) | | &#10004; | &#10004; | &#10004; | &#10004; |
| Zarządzanie pakietami w kanale informacyjnym | &#10004; | &#10004; | &#10004; | | |
| Ustawianie klawiszy INTERFEJSU API dla kanałów informacyjnych | | &#10004; | &#10004; | | |
| Tworzenie pakietów(3) | &#10004; | &#10004; | &#10004;(4) | &#10004; | |
| Publikowanie pakietów | &#10004; | &#10004; | &#10004; | &#10004; |  |
| Replikowanie pakietów |  | &#10004; | &#10004; | | |
| Zarządzanie folderami *pakietów globalnych* i pamięci podręcznej | &#10004; | &#10004; | &#10004; | | |
| Zarządzanie konfiguracją NuGet | | &#10004; | &#10004; | | |

(1) Nie ma wpływu na pliki projektu; zamiast `dotnet.exe` tego użyć.

(2) Działa `packages.config` tylko z plikami, a nie z plikami rozwiązania (`.sln`).

(3) Różne zaawansowane funkcje pakietu są dostępne za pośrednictwem interfejsu wiersza polecenia tylko wtedy, gdy nie są reprezentowane w narzędziach interfejsu użytkownika programu Visual Studio.

(4) Współpracuje `.nuspec` z plikami, ale nie z plikami projektu.

## <a name="upcoming-features"></a>Nadchodzące funkcje
Jeśli chcesz wyświetlić podgląd nadchodzących funkcji NuGet, zainstaluj [program Visual Studio Preview](https://www.visualstudio.com/vs/preview/), który działa obok siebie ze stabilnymi wersjami programu Visual Studio. Aby zgłosić problemy lub udostępnić pomysły dotyczące wersji zapoznawców, otwórz problem w [repozytorium NuGet GitHub](https://github.com/Nuget/Home/issues).

### <a name="related-topics"></a>Powiązane tematy

- [Instalowanie pakietów i zarządzanie nimi przy użyciu programu Visual Studio](consume-packages/install-use-packages-visual-studio.md)
- [Instalowanie pakietów i zarządzanie nimi przy użyciu programu PowerShell](consume-packages/install-use-packages-powershell.md)
- [Instalowanie pakietów i zarządzanie nimi przy użyciu dotnet CLI](consume-packages/install-use-packages-dotnet-cli.md)
- [Instalowanie pakietów i zarządzanie nimi przy użyciu pliku wiersza polecenia nuget.exe](consume-packages/install-use-packages-nuget-cli.md)
- [Odwołanie do konsoli PowerShell menedżera pakietów](reference/powershell-reference.md)
- [Tworzenie pakietu](create-packages/creating-a-package.md)
- [Publikowanie pakietu](nuget-org/publish-a-package.md)

Deweloperzy pracujący w systemie Windows mogą również eksplorować [Eksplorator pakietów NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), autonomiczne narzędzie typu open source do wizualnego eksplorowania, tworzenia i edytowania pakietów NuGet. Jest to bardzo pomocne, na przykład, aby wprowadzić eksperymentalne zmiany w strukturze pakietu bez przebudowy pakietu.
