---
title: Instalowanie narzędzi klienta programu NuGet
description: Wskazówki na temat instalowania narzędzi klienckich, dotnet, jak i nuget interfejsów z wierszem polecenia (CLI) i Menedżer pakietów dla programu Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: quickstart
ms.openlocfilehash: 6e3011493b7b89bc43cd9a267aea7fd32d668cec
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426569"
---
# <a name="install-nuget-client-tools"></a>Instalowanie narzędzi klienta programu NuGet

> **Wyszukiwanie, aby zainstalować pakiet? Zobacz [sposobów instalowania pakietów NuGet](consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).**

Aby pracować z pakietów NuGet jako konsument pakietu lub twórcą, można użyć narzędzi interfejsu wiersza polecenia (CLI), a także funkcje NuGet w programie Visual Studio. W tym artykule krótko opisano możliwości różnych narzędzi, jak zainstalować, a ich porównawczej [dostępność funkcji](#feature-availability). Aby rozpocząć korzystanie z pakietów za pomocą narzędzia NuGet, zobacz [instalacji i używania pakietu (interfejs wiersza polecenia platformy .NET)](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) i [instalacji i używania pakietu (Visual Studio)](quickstart/install-and-use-a-package-in-visual-studio.md). Aby rozpocząć tworzenie pakietów NuGet, zobacz [tworzenie i publikowanie pakietu platformy .NET Standard (interfejs wiersza polecenia platformy dotnet)](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) i [tworzenie i publikowanie pakietu platformy .NET Standard (Visual Studio)](quickstart/create-and-publish-a-package-using-visual-studio.md).

| Narzędzie&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Opis | Pobierz&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | Narzędzie interfejsu wiersza polecenia dla biblioteki .NET Core i .NET Standard, a dla każdego projektu zestawu SDK stylu taki, który jest przeznaczony dla .NET Framework (zobacz [atrybutu zestawu SDK](/dotnet/core/tools/csproj#additions)). Dołączone do zestawu SDK programu .NET Core i zapewnia podstawowe funkcje NuGet na wszystkich platformach. | [Zestaw SDK dla platformy .NET core](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | Narzędzie interfejsu wiersza polecenia dla biblioteki .NET Framework i projektów innych stylu zestawu SDK, przeznaczonych dla biblioteki .NET Standard. Zawiera wszystkie funkcje NuGet na Windows elastycznego, wyświetla większości funkcji na komputerach Mac i Linux, w przypadku uruchomienia w Mono. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | W Windows zapewnia możliwości NuGet za pomocą interfejsu użytkownika Menedżera pakietów i konsoli Menedżera pakietów; dołączone. Obciążenia związane z sieci. Na komputerze Mac udostępnia pewne funkcje za pośrednictwem interfejsu użytkownika. W programie Visual Studio Code funkcji NuGet są dostarczane za pośrednictwem rozszerzeń. | [Visual Studio 2017](https://www.visualstudio.com/downloads/) |

[Interfejsu wiersza polecenia MSBuild](reference/msbuild-targets.md) udostępnia możliwość przywracania i tworzenia pakietów, co przydaje się głównie na serwerach kompilacji. Program MSBuild nie jest narzędziem ogólnego przeznaczenia do pracy z NuGet.

## <a name="cli-tools"></a>Narzędzia interfejsu wiersza polecenia

Są dwa narzędzia interfejsu wiersza polecenia NuGet `dotnet.exe` i `nuget.exe`. Zobacz [dostępność funkcji](#feature-availability) dla porównania.

* Aby skierować je do platformy .NET Core lub .NET Standard, należy użyć wiersz polecenia dotnet. Wiersz polecenia dotnet jest wymagany do formatu projektu zestawu SDK stylu, który używa [atrybutu zestawu SDK](/dotnet/core/tools/csproj#additions).
* Do obiektu docelowego .NET Framework (tylko projekt się w stylu zestawu SDK), użyj `nuget.exe CLI`. Jeśli projekt jest migracja do `packages.config`, użyj wiersz polecenia dotnet.

### <a name="dotnetexe-cli"></a>DotNet.exe interfejsu wiersza polecenia

.NET Core 2.0 CLI `dotnet.exe`, działa na wszystkich platformach (Windows, Mac i Linux) i zapewnia podstawowe funkcje NuGet, takich jak instalowanie, przywracania i publikowania pakietów. `dotnet` zapewnia bezpośrednią integrację z pliki projektów .NET Core (takie jak `.csproj`), co jest przydatne w większości scenariuszy. `dotnet` jest również wbudowane bezpośrednio dla każdej platformy i nie wymaga zainstalowania platformy Mono.

Instalacja:

- Na komputerach deweloperów jest instalowany [zestawu .NET Core SDK](https://aka.ms/dotnetcoregs).
- W przypadku serwerów kompilacji, postępuj zgodnie z instrukcjami [przy użyciu zestawu .NET Core SDK i narzędzi ciągłej integracji](/dotnet/core/tools/using-ci-with-cli).

Aby dowiedzieć się, jak podstawowe polecenia za pomocą interfejsu wiersza polecenia platformy dotnet, zobacz [Instalowanie i używanie pakietów przy użyciu interfejsu wiersza polecenia platformy dotnet](consume-packages/install-use-packages-dotnet-cli.md).

### <a name="nugetexe-cli"></a>Interfejs wiersza polecenia nuget.exe

`nuget.exe` Interfejsu wiersza polecenia, `nuget.exe`, to narzędzie wiersza polecenia dla Windows, który zawiera wszystkie funkcje NuGet; może również działać w systemie Mac OSX i Linux przy użyciu [Mono](http://www.mono-project.com/docs/getting-started/install/) z pewnymi ograniczeniami.

Instalacja:

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> Użyj `nuget update -self` na Windows, aby zaktualizować istniejące nuget.exe do najnowszej wersji.

Aby dowiedzieć się, jak użyć podstawowa poleceń z `nuget.exe` interfejsu wiersza polecenia, zobacz [Instalowanie i używanie pakietów przy użyciu interfejsu wiersza polecenia nuget.exe](consume-packages/install-use-packages-nuget-cli.md).

> [!Note]
> Najnowsze zalecane, interfejs wiersza polecenia NuGet jest zawsze dostępne pod adresem `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe`. Dla celów zgodności ze starszymi systemami ciągłej integracji, poprzedniego adresu URL `https://nuget.org/nuget.exe` udostępnia obecnie [przestarzałe 2.8.6 narzędzie interfejsu wiersza polecenia](https://github.com/NuGet/NuGetGallery/issues/5381).

## <a name="visual-studio"></a>Visual Studio

- Visual Studio Code: NuGet możliwości są dostępne za pośrednictwem rozszerzeń z witryny marketplace lub użyj `dotnet.exe` lub `nuget.exe` narzędzi interfejsu wiersza polecenia.

- Visual Studio dla komputerów Mac: pewnych funkcji NuGet są wbudowane bezpośrednio. Zobacz [pakietu w tym NuGet w projekcie](/visualstudio/mac/nuget-walkthrough) przewodnik. W przypadku innych funkcji, użyj `dotnet.exe` lub `nuget.exe` narzędzi interfejsu wiersza polecenia.

- Visual Studio on Windows: **Menedżera pakietów NuGet** jest dołączone do programu Visual Studio 2012 i nowszych wersjach. Program Visual Studio udostępnia [interfejs użytkownika Menedżera pakietów](tools/package-manager-ui.md) i [Konsola Menedżera pakietów](tools/package-manager-console.md), za pomocą którego można uruchomić większość operacji NuGet.
  - Począwszy od programu Visual Studio 2017, Instalator zawiera Menedżer pakietów NuGet za pomocą dowolnego obciążenia, która używa .NET. Aby zainstalować niezależnie lub sprawdź, czy jest zainstalowany Menedżer pakietów, uruchom Instalatora programu Visual Studio i zaznacz opcję w obszarze **poszczególne składniki > Kod Narzędzia > Menedżer pakietów NuGet**.
  - Interfejs użytkownika Menedżera pakietów i konsoli są unikatowe dla programu Visual Studio w Windows. Nie są obecnie dostępne w programie Visual Studio dla komputerów Mac.
  - Narzędzie interfejsu wiersza polecenia jest wymagany do obsługi funkcji NuGet w środowisku IDE. Można użyć dowolnego `dotnet` interfejsu wiersza polecenia lub `nuget.exe` interfejsu wiersza polecenia. `dotnet` Interfejsu wiersza polecenia został zainstalowany przy użyciu niektórych obciążeń programu Visual Studio, takich jak .NET Core. `nuget.exe` Interfejsu wiersza polecenia musi być zainstalowany oddzielnie, zgodnie z wcześniejszym opisem.
  - Konsola Menedżera pakietów polecenia działają tylko w programie Visual Studio na Windows, a nie przeszkadzają inne środowiska PowerShell.
  - Dla programu Visual Studio 2010 i starszych należy zainstalować rozszerzenie "NuGet pakietu Menedżera for Visual Studio".
  - Rozszerzenia NuGet dla programu Visual Studio 2013 i 2015 można również pobrać z [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).
  - Jeśli chcesz nadchodzące funkcje NuGet w wersji zapoznawczej, należy zainstalować [Visual Studio 2017 w wersji zapoznawczej](https://www.visualstudio.com/vs/preview/), która działa side-by-side przy użyciu stabilnej wersji programu Visual Studio. Aby zgłosić problemy lub Podziel się pomysłami dotyczącym wersji zapoznawczych, otwórz problem w [repozytorium NuGet GitHub](https://github.com/Nuget/Home/issues).

## <a name="feature-availability"></a>Dostępność funkcji

| Funkcja | Wiersz polecenia DotNet | nuget interfejsu wiersza polecenia platformy (Windows) | nuget interfejsu wiersza polecenia (Mono) | Visual Studio (Windows) | Visual Studio for Mac |
| --- | --- | --- | --- | --- | --- |
| Wyszukaj pakiety |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Instalowanie/Odinstalowywanie pakietów | &#10004; | &#10004;(1) | &#10004; | &#10004; | &#10004; |
| Aktualizowanie pakietów | &#10004; | &#10004; | | &#10004; | &#10004; |
| Przywracanie pakietów | &#10004; | &#10004; | &#10004;(2) | &#10004; | &#10004; |
| Zarządzanie źródłami pakietów (źródła) | | &#10004; | &#10004; | &#10004; | &#10004; |
| Zarządzanie pakietami na źródło danych | &#10004; | &#10004; | &#10004; | | |
| Zestaw kluczy interfejsu API dla źródeł danych | | &#10004; | &#10004; | | |
| Utwórz packages(3) | &#10004; | &#10004; | &#10004;(4) | &#10004; | |
| Publikowanie pakietów | &#10004; | &#10004; | &#10004; | &#10004; |  |
| Replikowanie pakietów |  | &#10004; | &#10004; | | |
| Zarządzanie *globalny pakiet* i foldery w pamięci podręcznej | &#10004; | &#10004; | &#10004; | | |
| Zarządzanie konfiguracją NuGet | | &#10004; | &#10004; | | |

(1) nie wpływa na pliki projektu; Użyj `dotnet.exe` zamiast tego.

(2) działa tylko w przypadku `packages.config` pliku, a nie z rozwiązania (`.sln`) plików.

(3) różne funkcje zaawansowane pakietu są dostępne za pośrednictwem interfejsu wiersza polecenia, tylko wtedy, gdy nie są one reprezentowane w interfejsie użytkownika Visual Studio tools.

(4) współpracuje z `.nuspec` plików, ale nie z plików projektu.

### <a name="related-topics"></a>Tematy pokrewne

- [Instalowanie i zarządzanie pakietami za pomocą programu Visual Studio](tools/package-manager-ui.md)
- [Instalowanie i zarządzania pakietami przy użyciu programu PowerShell](tools/package-manager-console.md)
- [Instalowanie i zarządzanie pakietami za pomocą interfejsu wiersza polecenia platformy dotnet](consume-packages/install-use-packages-dotnet-cli.md)
- [Instalowanie i zarządzanie pakietami za pomocą interfejsu wiersza polecenia nuget.exe](consume-packages/install-use-packages-nuget-cli.md)
- [Dokumentacja programu PowerShell z konsoli Menedżera pakietów](tools/powershell-reference.md)
- [Tworzenie pakietu](create-packages/creating-a-package.md)
- [Publikowanie pakietu](nuget-org/publish-a-package.md)

Deweloperzy pracujący nad Windows też mogą zapoznać się z [Eksplorator pakietów NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), typu open source, autonomiczne narzędzie wizualnie eksplorować, tworzyć i edytować pakietów NuGet. Bardzo pomocne jest na przykład zmiany eksperymentalne do struktury pakietu bez odbudowywania pakietu.
