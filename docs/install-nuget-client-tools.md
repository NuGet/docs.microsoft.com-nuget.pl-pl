---
title: Instalowanie narzędzi klienta NuGet
description: Wskazówki dotyczące instalacji narzędzi klienta dotnet i nuget interfejsy wiersza polecenia (CLI) i Menedżer pakietów dla programu Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 04/09/2018
ms.topic: quickstart
ms.openlocfilehash: f136295cd46dd11a153b5f9c25a685a5a8dbd45a
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818124"
---
# <a name="installing-nuget-client-tools"></a>Instalowanie narzędzi klienta NuGet

> **Wyszukiwanie, aby zainstalować pakiet? Zobacz [sposobów, aby zainstalować pakietów NuGet](consume-packages/ways-to-install-a-package.md).**

Aby pracować z NuGet, jako pakiet klienta lub twórcą, można użyć [narzędzi interfejsu wiersza polecenia (CLI)](#cli-tools) oraz [funkcji NuGet w programie Visual Studio](#visual-studio). W tym artykule krótko opisano możliwości różnych narzędzi, jak zainstalować i ich porównawczych [dostępność funkcji](#feature-availability). Aby rozpocząć pracę, aby korzystać z pakietów przy użyciu narzędzia NuGet, zobacz [instalacji i używania pakietu (.NET interfejsu wiersza polecenia)](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) i [instalacji i używania pakietu (Visual Studio)](quickstart/install-and-use-a-package-in-visual-studio.md). Aby rozpocząć tworzenie pakietów NuGet, zobacz [tworzenie i publikowanie pakietu NET Standard (dotnet interfejsu wiersza polecenia)](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) i [tworzenie i publikowanie pakietu NET Standard (Visual Studio)](quickstart/create-and-publish-a-package-using-visual-studio.md).

| Narzędzie&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Opis | Pobierz&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | Dołączone do zestawu SDK .NET Core i udostępnia podstawowe funkcje NuGet na wszystkich platformach. | [Oprogramowanie .NET core SDK](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | Zawiera wszystkie funkcje NuGet w systemie Windows, zawiera większość funkcji po Mac i Linux, gdy uruchomiona w ramach Mono. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | W systemie Windows zapewnia możliwości NuGet za pomocą interfejsu użytkownika Menedżera pakietów i konsoli Menedżera pakietów; dołączone. Obciążenia związane z sieci. Dla komputerów Mac udostępnia pewne funkcje za pośrednictwem interfejsu użytkownika. W programie Visual Studio Code NuGet funkcje są realizowane za pośrednictwem rozszerzenia. | [Visual Studio 2017](https://www.visualstudio.com/downloads/) |

[Interfejsu wiersza polecenia programu MSBuild](reference/msbuild-targets.md) udostępnia możliwość przywracania i tworzenia pakietów, która jest szczególnie przydatna na serwerach kompilacji. Program MSBuild nie jest uniwersalny narzędzia do pracy z programem NuGet.

## <a name="cli-tools"></a>Narzędzi interfejsu wiersza polecenia

Są dwa narzędzia interfejsu wiersza polecenia NuGet `dotnet.exe` i `nuget.exe`. Zobacz [dostępność funkcji](#feature-availability) porównanie.

### <a name="dotnetexe-cli"></a>DotNet.exe interfejsu wiersza polecenia

.NET Core 2.0 interfejsu wiersza polecenia, `dotnet.exe`, działa na wszystkich platformach (z systemem Windows, Mac i Linux) i zapewnia podstawowe funkcje NuGet, takie jak instalowanie, przywracania i publikowania pakietów. `dotnet` zapewnia integrację bezpośrednio z plikami projektu platformy .NET Core (takie jak `.csproj`), co jest przydatne w większości przypadków. `dotnet` również jest oparty bezpośrednio na różnych platformach i nie wymagają zainstalowania Mono.

Instalacja:

- Na komputerach deweloperów zainstalować [.NET Core SDK](https://aka.ms/dotnetcoregs).
- Serwery kompilacji, postępuj zgodnie z instrukcjami [przy użyciu programu .NET Core SDK i narzędzi w ciągłej integracji](/dotnet/core/tools/using-ci-with-cli).

Aby uzyskać więcej informacji, zobacz [.NET Core interfejsu wiersza polecenia narzędzia](/dotnet/core/tools/index?tabs=netcore2x#tabpanel_fXL5YCOYDa_netcore2x).

### <a name="nugetexe-cli"></a>nuget.exe interfejsu wiersza polecenia

Interfejsu wiersza polecenia NuGet `nuget.exe`, to narzędzie wiersza polecenia dla systemu Windows, który zawiera wszystkie funkcje NuGet; można go również uruchomić na systemu Mac OS x i Linux przy użyciu [Mono](http://www.mono-project.com/docs/getting-started/install/) z pewnymi ograniczeniami. W odróżnieniu od `dotnet`, `nuget.exe` interfejsu wiersza polecenia nie ma wpływu na pliki projektu i nie powoduje aktualizacji `packages.config` podczas instalowania pakietów.

Instalacja:

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> Użyj `nuget update -self` w systemie Windows, aby zaktualizować istniejące nuget.exe do najnowszej wersji.

> [!Note]
> Zalecane najnowszej interfejsu wiersza polecenia NuGet jest zawsze dostępna w `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe`. Do celów zgodności ze starszymi systemami ciągłej integracji, poprzedniego adresu URL `https://nuget.org/nuget.exe` obecnie udostępnia [przestarzałe 2.8.6 interfejsu wiersza polecenia narzędzia](https://github.com/NuGet/NuGetGallery/issues/5381).

## <a name="visual-studio"></a>Visual Studio

- Visual Studio Code: NuGet możliwości są dostępne za pośrednictwem rozszerzenia portalu marketplace, lub użyj `dotnet.exe` lub `nuget.exe` narzędzi interfejsu wiersza polecenia.

- Visual Studio dla komputerów Mac: pewnych funkcji NuGet są tworzone bezpośrednio. Zobacz [pakietu w tym NuGet w projekcie](/visualstudio/mac/nuget-walkthrough) przewodnik. Dla innych funkcji, należy użyć `dotnet.exe` lub `nuget.exe` narzędzi interfejsu wiersza polecenia.

- Visual Studio w systemie Windows: **Menedżera pakietów NuGet** jest dołączana do programu Visual Studio 2012 i nowszych. Menedżer pakietów zawiera [interfejsu użytkownika Menedżera pakietów](tools/package-manager-ui.md) i [Konsola Menedżera pakietów](tools/package-manager-console.md), za pomocą którego można wykonać większość operacji NuGet.
  - Instalator programu Visual Studio 2017 obejmuje Menedżera pakietów NuGet z dowolnym obciążeniu używającego .NET. Aby zainstalować oddzielnie lub sprawdź, czy jest zainstalowany Menedżer pakietów, uruchom Instalatora programu Visual Studio 2017 i zaznacz opcję w obszarze **pojedynczych składników > narzędzia Code > Menedżera pakietów NuGet**.
  - Interfejs użytkownika Menedżera pakietów i konsoli są unikatowe dla programu Visual Studio w systemie Windows. Nie są obecnie dostępne w programie Visual Studio dla komputerów Mac.
  - Program Visual Studio nie ma automatycznie `nuget.exe` interfejsu wiersza polecenia, które należy zainstalować osobno, zgodnie z wcześniejszym opisem.
  - Konsola Menedżera pakietów polecenia działa tylko w programie Visual Studio w systemie Windows i nie działają w innych środowiskach programu PowerShell.
  - Dla programu Visual Studio 2010 i starszych wersji należy zainstalować rozszerzenie "NuGet pakietu Manager dla programu Visual Studio".
  - Rozszerzenia NuGet dla programu Visual Studio 2013 i 2015 można również pobrać z [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).
  - Jeśli chcesz nadchodzących funkcji NuGet w wersji zapoznawczej, zainstaluj [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), który działa side-by-side z stabilne wersje programu Visual Studio. Zgłaszanie problemów lub udostępniać pomysły dotyczące wersji zapoznawczych, otwórz problemu na [repozytorium NuGet GitHub](https://github.com/Nuget/Home/issues).

## <a name="feature-availability"></a>Dostępność funkcji

| Funkcja | DotNet interfejsu wiersza polecenia | nuget interfejsu wiersza polecenia (system Windows) | nuget interfejsu wiersza polecenia (Mono) | Visual Studio (z systemem Windows) | Visual Studio for Mac |
| --- | --- | --- | --- | --- | --- |
| Pakiety wyszukiwania |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Instalowanie/Odinstalowywanie pakietów | &#10004;(1) | &#10004;(2) | &#10004; | &#10004; | &#10004; |
| Pakiety aktualizacji | &#10004; | &#10004; | | &#10004; | &#10004; |
| Przywracanie pakietów | &#10004; | &#10004; | &#10004;(3) | &#10004; | &#10004; |
| Zarządzanie źródła pakietu (źródła) | | &#10004; | &#10004; | &#10004; | &#10004; |
| Zarządzaj pakietami na źródło | &#10004;(1) | &#10004; | &#10004; | | |
| Klucze interfejsu API zestawu dla źródła danych | | &#10004; | &#10004; | | |
| Utwórz packages(4) | &#10004; | &#10004; | &#10004;(5) | &#10004; | |
| Publikowanie pakietów | &#10004;(1) | &#10004; | &#10004; | &#10004; |  |
| Replikowanie pakietów |  | &#10004; | &#10004; | | |
| Zarządzanie *globalnej pakietu* i pamięci podręcznej folderów | &#10004; | &#10004; | &#10004; | | |
| Zarządzanie konfiguracją NuGet | | &#10004; | &#10004; | | |

(1) pakiety na tylko nuget.org

(2) nie ma wpływu na pliki projektu; Użyj `dotnet.exe` zamiast tego.

(3) działa tylko z `packages.config` pliku, a nie z rozwiązaniem (`.sln`) plików.

(4) różne funkcje zaawansowane pakietu są dostępne za pośrednictwem interfejsu wiersza polecenia, tylko wtedy, gdy nie są one reprezentowane w narzędzia interfejsu użytkownika programu Visual Studio.

(5) współpracuje z `.nuspec` plików, ale nie pliki projektu.

### <a name="related-topics"></a>Tematy pokrewne

- [Polecenia dotnet](tools/dotnet-commands.md)
- [Odwołanie do interfejsu wiersza polecenia NuGet](tools/nuget-exe-cli-reference.md)
- [Informacje o interfejsie użytkownika Menedżera pakietów](tools/package-manager-ui.md)
- [Odwołanie do konsoli Menedżera pakietów](tools/package-manager-console.md)
- [Dokumentacja programu PowerShell konsoli Menedżera pakietów](tools/powershell-reference.md)
- [Tworzenie pakietu](create-packages/creating-a-package.md)
- [Publikowania pakietu](create-packages/publish-a-package.md)

Deweloperów pracujących w systemie Windows można też eksplorować [Explorer pakietu NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), open source, autonomiczne narzędzie, aby wizualnie eksplorować, tworzyć i edytować pakietów NuGet. Bardzo pomocne jest na przykład wprowadzania zmian eksperymentalne Struktura pakietu bez ponownie skompilować pakietu.
