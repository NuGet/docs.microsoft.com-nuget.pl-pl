---
title: Instalowanie narzędzi klienta NuGet
description: Wskazówki dotyczące instalowania narzędzi klienckich, poleceń dotnet i NuGet (CLI) oraz Menedżera pakietów dla programu Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/20/2019
ms.topic: quickstart
ms.openlocfilehash: 0e3938fc1ac748285ba26541a7d4e907c9a64156
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775895"
---
# <a name="install-nuget-client-tools"></a>Instalowanie narzędzi klienta programu NuGet

> **Chcesz zainstalować pakiet? Zobacz [sposoby instalowania pakietów NuGet](consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).**

Aby współpracować z pakietem NuGet jako odbiorca lub twórca pakietu, można użyć narzędzi interfejsu wiersza polecenia (CLI), a także funkcji NuGet w programie Visual Studio. W tym artykule krótko opisano możliwości różnych narzędzi, sposób ich instalacji oraz [dostępność funkcji](#feature-availability)porównawczych. Aby rozpocząć korzystanie z narzędzia NuGet do korzystania z pakietów, zobacz [Instalowanie i używanie pakietu (interfejsu wiersza polecenia dotnet)](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) oraz [Instalowanie i używanie pakietu (Visual Studio)](quickstart/install-and-use-a-package-in-visual-studio.md). Aby rozpocząć tworzenie pakietów NuGet, zobacz [Tworzenie i publikowanie pakietu platformy .NET Standard (interfejsu wiersza polecenia dotnet)](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) oraz [Tworzenie i publikowanie pakietu platformy .NET Standard (Visual Studio)](quickstart/create-and-publish-a-package-using-visual-studio.md).

| Narzędziem&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Opis | Przesłać&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | Narzędzie interfejsu wiersza polecenia dla bibliotek .NET Core i .NET Standard oraz dla dowolnego [projektu w stylu zestawu SDK](resources/check-project-format.md) , takiego jak jeden obiekt docelowy .NET Framework. Uwzględniono w zestaw .NET Core SDK i udostępnia podstawowe funkcje NuGet na wszystkich platformach. (Począwszy od programu Visual Studio 2017, interfejs wiersza polecenia dotnet jest automatycznie instalowany z dowolnymi obciążeniami związanymi z platformą .NET Core).| [Zestaw .NET Core SDK](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | Narzędzie interfejsu wiersza polecenia dla bibliotek .NET Framework i dla dowolnego [projektu typu innego niż zestaw SDK](resources/check-project-format.md) , takiego jak ten, który jest przeznaczony dla bibliotek .NET Standard. Zapewnia wszystkie możliwości programu NuGet w systemie Windows, zapewnia większość funkcji w systemach Mac i Linux, gdy działa w ramach programu mono. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | W systemie Windows **Menedżer pakietów NuGet** jest dołączony do programu Visual Studio 2012 lub nowszego. Program Visual Studio udostępnia [interfejs użytkownika Menedżera pakietów](consume-packages/install-use-packages-visual-studio.md) i [konsolę Menedżera pakietów](consume-packages/install-use-packages-powershell.md), za pomocą którego można uruchamiać większość operacji NuGet. | [Visual Studio](https://www.visualstudio.com/downloads/) |
| [Visual Studio dla komputerów Mac](/visualstudio/mac/nuget-walkthrough) | Na komputerach Mac niektóre funkcje NuGet są wbudowane bezpośrednio. Konsola Menedżera pakietów nie jest obecnie dostępna. Aby uzyskać inne możliwości, użyj `dotnet.exe` `nuget.exe` narzędzi lub interfejsu wiersza polecenia.  | [Visual Studio dla komputerów Mac](https://visualstudio.microsoft.com/vs/mac/) |
| [Visual Studio Code](https://code.visualstudio.com/docs) | W systemie Windows, Mac lub Linux funkcje NuGet są dostępne za pomocą rozszerzeń witryny Marketplace lub `dotnet.exe` `nuget.exe` narzędzi interfejsu wiersza polecenia. | [Visual Studio Code](https://code.visualstudio.com/Download/)|

[Interfejs wiersza polecenia programu MSBuild](reference/msbuild-targets.md) oferuje również możliwość przywracania i tworzenia pakietów, co jest szczególnie przydatne na serwerach kompilacji. MSBuild nie jest narzędziem ogólnego przeznaczenia do pracy z pakietem NuGet.

Polecenia konsoli Menedżera pakietów działają tylko w programie Visual Studio w systemie Windows i nie działają w innych środowiskach programu PowerShell.

## <a name="visual-studio"></a>Visual Studio
### <a name="install-on-visual-studio-2017-and-newer"></a>Zainstaluj w programie Visual Studio 2017 i nowszym
Począwszy od programu Visual Studio 2017, Instalator zawiera Menedżera pakietów NuGet z dowolnym obciążeniem, które wykorzystuje platformę .NET. Aby przeprowadzić instalację osobno lub sprawdzić, czy Menedżer pakietów jest zainstalowany, uruchom Instalatora programu Visual Studio i zaznacz opcję w obszarze **poszczególne składniki > narzędzia kodu > Menedżera pakietów NuGet**.

### <a name="install-on-visual-studio-2015-and-older"></a>Zainstaluj w programie Visual Studio 2015 i starszych wersjach
Rozszerzenia NuGet dla Visual Studio 2013 i 2015 można pobrać z programu [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) .

W przypadku programu Visual Studio 2010 i starszych wersji Zainstaluj rozszerzenie "NuGet Package Manager for Visual Studio". Uwaga Jeśli rozszerzenie nie jest widoczne na pierwszej stronie wyników wyszukiwania, spróbuj zmienić sortowanie według listy rozwijanej na "większość plików do pobrania" lub Sortuj alfabetycznie.

## <a name="cli-tools"></a>Narzędzia interfejsu wiersza polecenia
`dotnet`Do obsługi funkcji NuGet w środowisku IDE można użyć interfejsu wiersza polecenia lub `nuget.exe` interfejsu wiersza polecenia. `dotnet`Interfejs wiersza polecenia jest instalowany z niektórymi obciążeniami programu Visual Studio, takimi jak .NET Core. `nuget.exe`Interfejs wiersza polecenia należy zainstalować osobno zgodnie z wcześniejszym opisem.

Dwa narzędzia interfejsu wiersza polecenia NuGet to `dotnet.exe` i `nuget.exe` . Zobacz [dostępność funkcji](#feature-availability) dla porównania.

* Aby określić obiekt docelowy .NET Core lub .NET Standard, użyj interfejsu wiersza polecenia dotnet. `dotnet`Interfejs wiersza polecenia jest wymagany dla formatu projektu w stylu zestawu SDK, który używa [atrybutu SDK](/dotnet/core/tools/csproj#additions).
* Aby określić docelową .NET Framework (tylko projekt typu non-SDK), użyj `nuget.exe` interfejsu wiersza polecenia. Jeśli projekt jest migrowany z `packages.config` do PackageReference, użyj interfejsu wiersza polecenia dotnet.

### <a name="dotnetexe-cli"></a>INTERFEJS WIERSZA POLECENIA dotnet.exe

Interfejs wiersza polecenia platformy .NET Core 2,0, `dotnet.exe` , działa na wszystkich platformach (Windows, Mac i Linux) i udostępnia podstawowe funkcje NuGet, takie jak instalowanie, przywracanie i publikowanie pakietów. `dotnet` zapewnia bezpośrednią integrację z plikami projektu programu .NET Core (takimi jak `.csproj` ), które są przydatne w większości scenariuszy. `dotnet` Program jest również zbudowany bezpośrednio dla każdej platformy i nie wymaga instalacji programu mono.

Instalacja:

- Na komputerach deweloperskich zainstaluj [zestaw .NET Core SDK](https://aka.ms/dotnetcoregs). Począwszy od programu Visual Studio 2017, interfejs wiersza polecenia dotnet jest automatycznie instalowany z dowolnymi obciążeniami związanymi z platformą .NET Core.
- W przypadku serwerów kompilacji postępuj zgodnie z instrukcjami dotyczącymi [używania zestaw .NET Core SDK i narzędzi w ciągłej integracji](/dotnet/core/tools/using-ci-with-cli).

Aby dowiedzieć się, jak używać podstawowych poleceń z interfejsem wiersza polecenia dotnet, zobacz [Instalowanie i używanie pakietów przy użyciu interfejsu wiersza polecenia dotnet](consume-packages/install-use-packages-dotnet-cli.md).

### <a name="nugetexe-cli"></a>Interfejs wiersza polecenia nuget.exe

`nuget.exe`Interfejs wiersza `nuget.exe` polecenia,, jest narzędziowym wierszem poleceń dla systemu Windows, który zapewnia wszystkie możliwości NuGet. można go również uruchomić w systemach Mac OSX i Linux przy użyciu narzędzia [mono](https://www.mono-project.com/docs/getting-started/install/) z pewnymi ograniczeniami.

Aby dowiedzieć się, jak używać podstawowych poleceń za pomocą `nuget.exe` interfejsu wiersza polecenia, zobacz [Instalowanie i używanie pakietów przy użyciu interfejsu wiersza polecenia nuget.exe](consume-packages/install-use-packages-nuget-cli.md).

Instalacja:

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> Użyj `nuget update -self` w systemie Windows, aby zaktualizować istniejące nuget.exe do najnowszej wersji.

> [!Note]
> Najnowsza zalecana wersja interfejsu wiersza polecenia NuGet jest zawsze dostępna pod adresem `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe` . W celu zapewnienia zgodności ze starszymi systemami ciągłej integracji, poprzedni adres URL, `https://nuget.org/nuget.exe` obecnie zapewnia [przestarzałe narzędzie interfejsu wiersza polecenia 2.8.6](https://github.com/NuGet/NuGetGallery/issues/5381).

## <a name="feature-availability"></a>Dostępność funkcji

| Cechy | Interfejs wiersza polecenia dotnet | Interfejs wiersza polecenia NuGet (Windows) | Interfejs wiersza polecenia NuGet (mono) | Visual Studio (Windows) | Visual Studio dla komputerów Mac |
| --- | --- | --- | --- | --- | --- |
| Wyszukaj pakiety |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Instalowanie/Odinstalowywanie pakietów | &#10004; | &#10004; (1) | &#10004; | &#10004; | &#10004; |
| Pakiety aktualizacji | &#10004; | &#10004; | | &#10004; | &#10004; |
| Przywracanie pakietów | &#10004; | &#10004; | &#10004; (2) | &#10004; | &#10004; |
| Zarządzanie źródłami pakietów (źródła) | | &#10004; | &#10004; | &#10004; | &#10004; |
| Zarządzanie pakietami w kanale informacyjnym | &#10004; | &#10004; | &#10004; | | |
| Ustawianie kluczy interfejsu API dla kanałów informacyjnych | | &#10004; | &#10004; | | |
| Utwórz pakiety (3) | &#10004; | &#10004; | &#10004; (4) | &#10004; | |
| Publikowanie pakietów | &#10004; | &#10004; | &#10004; | &#10004; |  |
| Replikuj pakiety |  | &#10004; | &#10004; | | |
| Zarządzanie folderami *globalnymi i pakietami* pamięci podręcznej | &#10004; | &#10004; | &#10004; | | |
| Zarządzanie konfiguracją NuGet | | &#10004; | &#10004; | | |

(1) nie ma wpływu na pliki projektu; Użyj `dotnet.exe` zamiast tego.

(2) działa tylko z `packages.config` plikiem, a nie z plikami rozwiązania ( `.sln` ).

(3) różne zaawansowane funkcje pakietu są dostępne za pomocą interfejsu wiersza polecenia tylko wtedy, gdy nie są one reprezentowane w narzędziach interfejsu użytkownika programu Visual Studio.

(4) współpracuje z `.nuspec` plikami, ale nie z plikami projektu.

## <a name="upcoming-features"></a>Nadchodzące funkcje
Jeśli chcesz przejrzeć nadchodzące funkcje NuGet, zainstaluj [program Visual Studio Preview](https://www.visualstudio.com/vs/preview/), który działa obok siebie w stabilnych wersjach programu Visual Studio. Aby zgłosić problemy lub udostępnić pomysły dotyczące wersji zapoznawczych, Otwórz problem w [repozytorium GitHub programu NuGet](https://github.com/Nuget/Home/issues).

### <a name="related-topics"></a>Powiązane tematy

- [Instalowanie pakietów i zarządzanie nimi za pomocą programu Visual Studio](consume-packages/install-use-packages-visual-studio.md)
- [Instalowanie pakietów i zarządzanie nimi przy użyciu programu PowerShell](consume-packages/install-use-packages-powershell.md)
- [Instalowanie pakietów i zarządzanie nimi przy użyciu interfejsu wiersza polecenia dotnet](consume-packages/install-use-packages-dotnet-cli.md)
- [Instalowanie pakietów i zarządzanie nimi przy użyciu interfejsu wiersza polecenia nuget.exe](consume-packages/install-use-packages-nuget-cli.md)
- [Dokumentacja programu PowerShell konsoli Menedżera pakietów](reference/powershell-reference.md)
- [Tworzenie pakietu](create-packages/creating-a-package.md)
- [Publikowanie pakietu](nuget-org/publish-a-package.md)

Deweloperzy pracujący w systemie Windows mogą również zapoznać się z [Eksploratorem pakietów NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)— autonomicznym narzędziem do wizualizacji, tworzenia i edytowania pakietów NuGet. Jest to bardzo przydatne, na przykład, aby wprowadzać eksperymentalne zmiany struktury pakietu bez ponownego kompilowania pakietu.
