---
title: NuGet — często zadawane pytania
description: Typowe pytania i odpowiedzi dla za pomocą narzędzia NuGet w wierszu polecenia i w programie Visual Studio
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9842e1d729d029ad987c1944afd10f2696030b3b
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426832"
---
# <a name="nuget-frequently-asked-questions"></a>NuGet — często zadawane pytania

**Co to jest wymagane do uruchamiania NuGet?**

Wszystkie informacje dotyczące narzędzia wiersza polecenia i interfejsu użytkownika jest dostępna w [Przewodnik instalacji](../install-nuget-client-tools.md).

**NuGet obsługuje platformy Mono?**

Narzędzie wiersza polecenia `nuget.exe`, kompilacji i uruchamiana Mono 3.2 + i mogą tworzyć pakiety w rozwiązaniu Mono.

Mimo że `nuget.exe` działa całkowicie w Windows, występują znane problemy w systemie Linux i OS X. zobacz [wystawia Mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) w witrynie GitHub.

A [graficzny klient](https://github.com/mrward/monodevelop-nuget-addin) jest dostępna jako dodatek do programu MonoDevelop.

**Jak sprawdzić, co zawiera pakiet i czy jest stabilna i użyteczna dla mojej aplikacji?**

Podstawowym źródłem szkoleniowe dotyczące pakietu jest jego strony w witrynie nuget.org (lub innej prywatnej źródła danych). Każda strona pakietu w witrynie nuget.org zawiera opis pakietu, jego Historia wersji i statystyki użycia. **Informacje** sekcji na stronie pakiet zawiera również link do witryny sieci web projektu, w którym można zwykle znaleźć wiele przykładów i inne dokumenty, aby ułatwić Ci poznanie sposobu używania pakietu.

Aby uzyskać więcej informacji, zobacz [Znajdowanie i Wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md).

## <a name="nuget-in-visual-studio"></a>NuGet w programie Visual Studio

**Jak NuGet jest obsługiwane w różnych produktów Visual Studio?**

- Program Visual Studio w Windows obsługuje [interfejs użytkownika Menedżera pakietów](../tools/package-manager-ui.md) i [Konsola Menedżera pakietów](../tools/package-manager-console.md).
- Program Visual Studio dla komputerów Mac ma wbudowanych funkcji NuGet, zgodnie z opisem na [pakietu w tym NuGet w projekcie](/visualstudio/mac/nuget-walkthrough).
- Visual Studio Code (wszystkie platformy) nie ma żadnych bezpośrednią integrację z NuGet. Użyj [interfejs wiersza polecenia NuGet](../tools/nuget-exe-cli-reference.md) lub [wiersz polecenia dotnet](../tools/dotnet-commands.md).
- Azure DevOps zapewnia [krok kompilacji, aby przywrócić pakiety NuGet](/vsts/build-release/tasks/package/nuget). Możesz również [hosta prywatnego pakietu NuGet kanałów informacyjnych w DevOps platformy Azure](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).

**Jak sprawdzić wersję narzędzia NuGet, które są zainstalowane?**

W programie Visual Studio, należy użyć **Pomoc > Microsoft Visual Studio** polecenia i przyjrzyj się wersja wyświetlany obok pozycji **Menedżera pakietów NuGet**.

Alternatywnie Uruchom konsolę Menedżera pakietów (**Narzędzia > Menedżer pakietów NuGet > Konsola Menedżera pakietów**) i wprowadź `$host` Aby wyświetlić informacje o tym w wersji NuGet.

**Jakich języków programowania są obsługiwane przez NuGet?**

NuGet zwykle działa w przypadku języków .NET i jest przeznaczona do bibliotek .NET do projektu. Ponieważ w niektórych typach projektów są również obsługuje automatyzacji programu MSBuild i Visual Studio, obsługuje ona również innych projektów i języki różnym stopniu.

Obsługuje najnowszej wersji pakietu NuGet C#, Visual Basic F#, WiX i C++.

**Szablony projektów, które są obsługiwane przez NuGet?**

NuGet ma pełną pomoc techniczną dla różnych szablonów projektu, takich jak Windows, sieci Web, chmury, SharePoint, Wix i tak dalej.

**Jak zaktualizować pakiety, które są częścią szablony programu Visual Studio?**

Przejdź do **aktualizacje** w Interfejsie użytkownika Menedżera pakietów, a wybierz pozycję **Aktualizuj wszystkie**, lub użyj [ `Update-Package` polecenia](../tools/ps-ref-update-package.md) z konsoli Menedżera pakietów.

Aby zaktualizować samego szablonu, musisz ręcznie zaktualizować repozytorium szablonów. Zobacz [blog Xavier Decoster](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) na ten temat. Należy to zrobić na własne ryzyko, należy pamiętać, ponieważ ręczne aktualizacje może spowodować uszkodzenie szablonu, jeśli najnowszą wersję wszystkich zależności nie są ze sobą zgodne.

**Można użyć NuGet poza programem Visual Studio?**

Tak, NuGet współpracuje bezpośrednio z poziomu wiersza polecenia. Zobacz [Przewodnik instalacji](../install-nuget-client-tools.md) i [dokumentacja interfejsu wiersza polecenia](../tools/nuget-exe-cli-reference.md).

## <a name="nuget-command-line"></a>Wiersz polecenia NuGet

**Jak uzyskać najnowszą wersję narzędzia wiersza polecenia NuGet?**

Zobacz [Przewodnik instalacji](../install-nuget-client-tools.md).

**Co to jest licencja na nuget.exe?**

Możesz wykonać ponowną dystrybucję nuget.exe zgodnie z warunkami licencji MIT. Odpowiedzialność za aktualizacji i obsługi wszystkich kopii nuget.exe, który chcesz ponownie rozesłać.

**Czy jest możliwe rozszerzenie narzędzia wiersza polecenia NuGet?**

Tak, istnieje możliwość dodawania niestandardowych poleceń do `nuget.exe`, zgodnie z opisem w [wpis Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>Konsola Menedżera pakietów NuGet (Visual Studio Windows)

**Jak uzyskać dostęp do obiektu DTE w konsoli Menedżera pakietów?**

Obiekt najwyższego poziomu w modelu obiektu automatyzacji programu Visual Studio nosi nazwę obiektu DTE (środowisko programistyczne narzędzia). Konsolę te elementy są dostępne za pośrednictwem zmiennej o nazwie `$DTE`. Aby uzyskać więcej informacji, zobacz [omówienie modelu automatyzacji](/visualstudio/extensibility/internals/automation-model-overview) w dokumentacji rozszerzeń programu Visual Studio.

**Próbie rzutowania $DTE zmienną typu DTE2, ale pojawia się błąd: Nie można przekonwertować wartości "EnvDTE.DTEClass" typu "EnvDTE.DTEClass" na typ "EnvDTE80.DTE2". Co jest nie tak?**

Jest to znany problem dotyczący współdziałania programu PowerShell za pomocą obiektu COM. Spróbuj wykonać następujące czynności:

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface` czy funkcji pomocnika, która jest dodawany przez hosta NuGet w programie PowerShell.

## <a name="creating-and-publishing-packages"></a>Tworzenie i publikowanie pakietów

**Jak wyświetlić listę Mój pakiet w źródle danych?**

Zobacz [tworzenie i publikowanie pakietu](../quickstart/create-and-publish-a-package.md).

**Mam wiele wersji biblioteki, przeznaczonych dla różnych wersji programu .NET Framework. Jak utworzyć jeden pakiet, który obsługuje tę funkcję?**

Zobacz [obsługujące wiele wersje programu .NET Framework i profile](../create-packages/supporting-multiple-target-frameworks.md).

**Jak skonfigurować własnego repozytorium lub źródło danych?**

Zobacz [hostingu — Omówienie pakietów](../hosting-packages/overview.md).

**Jak przesłać pakiety do mojego NuGet źródła danych w trybie zbiorczym**

Zobacz [zbiorczo publikowania pakietów NuGet](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).

## <a name="working-with-packages"></a>Praca z pakietami

**Jaka jest różnica między pakietem na poziomie projektu i pakietu poziomie rozwiązania?**

Pakiet poziomie rozwiązania (NuGet 3.x+) zostanie zainstalowana tylko raz w rozwiązaniu i jest dostępna dla wszystkich projektów w rozwiązaniu. Pakiet na poziomie projektu jest zainstalowany w każdym projekcie, który korzysta z niego. Pakiet poziomie rozwiązania może również zainstalować nowe polecenia, które mogą być wywoływane z poziomu konsoli Menedżera pakietów.

**Czy istnieje możliwość zainstalowania pakietów NuGet bez łączności z Internetem?**

Tak, zobacz wpis w blogu Scotta Hanselmana [jak uzyskać dostęp do NuGet, kiedy nuget.org znajduje się w dół (lub jesteś na płaszczyźnie)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).

**Jak zainstalować pakiety w innym miejscu niż domyślny folder pakietów?**

Ustaw [ `repositoryPath` ](../reference/nuget-config-file.md#config-section) w `Nuget.Config` przy użyciu `nuget config -set repositoryPath=<path>`.

**Jak uniknąć Dodawanie folderu pakiety NuGet do kontroli źródła**

Ustaw [ `disableSourceControlIntegration` ](../reference/nuget-config-file.md#solution-section) w `Nuget.Config` do `true`. Ta działa klucza w rozwiązaniu poziomie i w związku z tym konieczne będzie dodanie do `$(Solutiondir)\.nuget\Nuget.Config` pliku. Włączanie przywracania pakietów w programie Visual Studio automatycznie tworzy ten plik.

**Jak wyłączyć Przywracanie pakietu**

Zobacz [Włączanie i wyłączanie Przywracanie pakietu](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

**Dlaczego otrzymuję "Nie można rozwiązać błąd zależności" podczas instalowania pakietu lokalnego przy użyciu zależności zdalnych?**

Musisz wybrać **wszystkie** źródła podczas instalowania pakietu lokalnego do projektu. To agreguje wszystkie źródła danych zamiast przy użyciu tylko jednego. Przyczyna tego błędu pojawia się jest, czy użytkownicy lokalnego repozytorium często chcą uniknąć przypadkowego instalowania zdalnego pakietu ze względu na firmowe zasady.

**Mam wiele projektów w tym samym folderze, jak korzystać z pliku packages.config oddzielnych plików dla każdego projektu?**

W większości projektów, w którym oddzielnych projektów znajdować się w oddzielnych folderów, nie jest to problem jak NuGet identyfikuje `packages.config` plików w każdym projekcie. Nuget 3.3 + i jest wiele projektów w tym samym folderze, można wstawiać Nazwa projektu do `packages.config` nazw plików, użyj wzorca `packages.{project-name}.config`, i NuGet korzysta z tego pliku.

To nie jest wystąpił problem podczas korzystania z funkcji PackageReference, ponieważ każdy plik projektu zawiera swój własny listę zależności.

**Nuget.org nie jest widoczny w listy moich repozytoriów, jak uzyskać go ponownie?**

- Dodaj `https://api.nuget.org/v3/index.json` do listy źródeł, lub
- Usuń `%appdata%\.nuget\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) i pozwolić NuGet, utwórz go ponownie.