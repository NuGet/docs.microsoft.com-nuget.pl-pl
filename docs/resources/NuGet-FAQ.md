---
title: Często zadawane pytania dotyczące narzędzia NuGet
description: Często zadawane pytania i odpowiedzi dotyczące korzystania z narzędzia NuGet w wierszu polecenia i w programie Visual Studio
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 937a0083ca47ba5668059736a7e99f7ca88e8908
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622619"
---
# <a name="nuget-frequently-asked-questions"></a>Często zadawane pytania dotyczące narzędzia NuGet

Często zadawane pytania dotyczące usługi NuGet.org, takie jak NuGet.org accounts, zobacz [często zadawane pytania](../nuget-org/nuget-org-faq.md).

**Co jest wymagane do uruchomienia narzędzia NuGet?**

Wszystkie informacje o interfejsie użytkownika i narzędziach wiersza polecenia są dostępne w [przewodniku instalacji](../install-nuget-client-tools.md).

**Czy pakiet NuGet obsługuje mono?**

Narzędzie wiersza polecenia, `nuget.exe` kompiluje i uruchamia się w programie mono 3.2 + i może tworzyć pakiety w mono.

Chociaż `nuget.exe` działa w pełni w systemie Windows, istnieją znane problemy w systemach Linux i OS X. Zobacz problemy z programem [mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) w serwisie GitHub.

[Klient graficzny](https://github.com/mrward/monodevelop-nuget-addin) jest dostępny jako dodatek dla narzędzia MonoDevelop.

**Jak określić, co pakiet zawiera i czy jest stabilny i przydatny dla mojej aplikacji?**

Podstawowym źródłem informacji o pakiecie jest jego strona aukcji w witrynie nuget.org (lub innego prywatnego źródła). Każda Strona pakietu w witrynie nuget.org zawiera opis pakietu, jego historię wersji oraz dane statystyczne użycia. Sekcja **informacje** na stronie pakiet zawiera również link do witryny sieci Web projektu, gdzie zazwyczaj znajdziesz wiele przykładów i innych dokumentów, które ułatwiają zapoznanie się z używanym pakietem.

Aby uzyskać więcej informacji, zobacz [Znajdowanie i wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md).

## <a name="nuget-in-visual-studio"></a>Pakiet NuGet w programie Visual Studio

**Jak program NuGet jest obsługiwany w różnych produktach Visual Studio?**

- Program Visual Studio w systemie Windows obsługuje [interfejs użytkownika Menedżera pakietów](../consume-packages/install-use-packages-visual-studio.md) i [konsolę Menedżera pakietów](../consume-packages/install-use-packages-powershell.md).
- Visual Studio dla komputerów Mac ma wbudowane funkcje NuGet, zgodnie z opisem w temacie [zawierającym pakiet NuGet w projekcie](/visualstudio/mac/nuget-walkthrough).
- Visual Studio Code (wszystkie platformy) nie ma żadnej bezpośredniej integracji z pakietem NuGet. Użyj [interfejsu wiersza polecenia NuGet](../reference/nuget-exe-cli-reference.md) lub [interfejsu wiersza polecenia dotnet](../reference/dotnet-commands.md).
- Usługa Azure DevOps udostępnia [krok kompilacji służący do przywracania pakietów NuGet](/vsts/build-release/tasks/package/nuget). Możesz również [hostować prywatne źródła pakietów NuGet na platformie Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).

**Jak mogę sprawdzić dokładną wersję zainstalowanych narzędzi NuGet?**

W programie Visual Studio Użyj **> pomocy dotyczącej Microsoft Visual Studio** polecenia i sprawdź wersję wyświetlaną obok pozycji **Menedżer pakietów NuGet**.

Alternatywnie można uruchomić konsolę Menedżera pakietów (**narzędzia > Menedżera pakietów NuGet > konsoli Menedżera pakietów**) i wprowadzić polecenie, `$host` Aby wyświetlić informacje o pakiecie NuGet, w tym wersję.

**Jakie języki programowania są obsługiwane przez pakiet NuGet?**

Pakiet NuGet zazwyczaj działa w przypadku języków .NET i jest przeznaczony do przenoszenia bibliotek .NET do projektu. Ponieważ obsługuje ona również narzędzia MSBuild i automatyzację programu Visual Studio w niektórych typach projektów, obsługuje również inne projekty i Języki w różnych stopniach.

Najnowsza wersja NuGet obsługuje języki C#, Visual Basic, F #, WiX i C++.

**Jakie szablony projektów są obsługiwane przez pakiet NuGet?**

Pakiet NuGet ma pełną obsługę wielu szablonów projektów, takich jak Windows, Web, Cloud, SharePoint, WIX i tak dalej.

**Jak mogę pakiety aktualizacji, które są częścią szablonów programu Visual Studio?**

Przejdź do karty **aktualizacje** w interfejsie użytkownika Menedżera pakietów i wybierz pozycję **Aktualizuj wszystko**lub Użyj [ `Update-Package` polecenia](../reference/ps-reference/ps-ref-update-package.md) z konsoli Menedżera pakietów.

Aby zaktualizować sam szablon, musisz ręcznie zaktualizować repozytorium szablonów. Zapoznaj się z [blogiem](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) dotyczącym Xavier. Należy pamiętać, że jest to wykonywane na własne ryzyko, ponieważ ręczne aktualizacje mogą uszkodzić szablon, jeśli Najnowsza wersja wszystkich zależności nie jest zgodna ze sobą.

**Czy mogę używać narzędzia NuGet poza programem Visual Studio?**

Tak, pakiet NuGet działa bezpośrednio z wiersza polecenia. Zobacz [Przewodnik instalacji](../install-nuget-client-tools.md) i [Dokumentacja interfejsu wiersza polecenia](../reference/nuget-exe-cli-reference.md).

## <a name="nuget-command-line"></a>Wiersz polecenia NuGet

**Jak mogę pobrać najnowszej wersji narzędzia wiersza polecenia NuGet?**

Zobacz [Przewodnik instalacji](../install-nuget-client-tools.md). Aby sprawdzić bieżącą zainstalowaną wersję narzędzia, użyj programu `nuget help` .

**Jaka jest licencja na nuget.exe?**

Możesz ponownie dystrybuować nuget.exe w ramach licencji MIT. Użytkownik jest odpowiedzialny za aktualizowanie i obsługę dowolnych kopii nuget.exe, które chcesz ponownie dystrybuować.

**Czy jest możliwe rozszerzenie narzędzia wiersza polecenia NuGet?**

Tak, możliwe jest dodanie poleceń niestandardowych do `nuget.exe` , zgodnie z opisem w [wpisie Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>Konsola Menedżera pakietów NuGet (Visual Studio w systemie Windows)

**Jak mogę uzyskać dostęp do obiektu DTE w konsoli Menedżera pakietów?**

Obiekt najwyższego poziomu w modelu obiektów automatyzacji programu Visual Studio jest nazywany obiektem DTE (środowisko narzędzi programistycznych). Konsola zapewnia tę wartość za pomocą zmiennej o nazwie `$DTE` . Aby uzyskać więcej informacji, zobacz [Omówienie modelu automatyzacji](/visualstudio/extensibility/internals/automation-model-overview) w dokumentacji rozszerzalności programu Visual Studio.

**Próbujemy rzutować zmienną $DTE na typ DTE2, ale otrzymuję błąd: nie można skonwertować wartości "EnvDTE. DTEClass" typu "EnvDTE. DTEClass" na typ "EnvDTE80. DTE2". Co jest nie tak?**

Jest to znany problem związany z współdziałaniem programu PowerShell z obiektem COM. Spróbuj wykonać następujące czynności:

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface` jest funkcją pomocnika dodaną przez hosta NuGet programu PowerShell.

## <a name="creating-and-publishing-packages"></a>Tworzenie i publikowanie pakietów

**Jak mogę wyświetlić mój pakiet w kanale informacyjnym?**

Zobacz [Tworzenie i publikowanie pakietu](../quickstart/create-and-publish-a-package.md).

**Mam wiele wersji mojej biblioteki, które są przeznaczone dla różnych wersji .NET Framework. Jak mogę utworzyć pojedynczy pakiet, który go obsługuje?**

Zobacz [Obsługa wielu .NET Framework wersji i profilów](../create-packages/supporting-multiple-target-frameworks.md).

**Jak mogę skonfigurować własne repozytorium lub źródło danych?**

Zobacz [Omówienie pakietów hostingu](../hosting-packages/overview.md).

**Jak mogę przekazać pakiety do mojego źródła danych NuGet zbiorczo?**

Zobacz [zbiorcze publikowanie pakietów NuGet](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).

## <a name="working-with-packages"></a>Praca z pakietami

**Czy jest możliwe zainstalowanie pakietów NuGet bez połączenia z Internetem?**

Tak, zobacz wpis w blogu Scott Hanselman, [jak uzyskać dostęp do narzędzia NuGet, gdy NuGet.org nie działa (lub na płaszczyźnie)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (Hanselman.com).

**Jak mogę zainstalować pakiety w innej lokalizacji z folderu pakietów domyślnych?**

Ustaw [`repositoryPath`](../reference/nuget-config-file.md#config-section) ustawienie `Nuget.Config` przy użyciu `nuget config -set repositoryPath=<path>` .

**Jak mogę unikać dodawania folderu pakietów NuGet do kontroli źródła?**

Ustaw wartość [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) w `Nuget.Config` na `true` . Ten klucz działa na poziomie rozwiązania i dlatego należy go dodać do `$(Solutiondir)\.nuget\Nuget.Config` pliku. Włączenie przywracania pakietów w programie Visual Studio powoduje automatyczne utworzenie tego pliku.

**Jak mogę wyłączyć Przywracanie pakietu?**

Zobacz [Włączanie i wyłączanie przywracania pakietów](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).

**Dlaczego otrzymuję "nie można rozpoznać błędu zależności" podczas instalowania pakietu lokalnego z zależnościami zdalnymi?**

W przypadku instalowania pakietu lokalnego w projekcie należy wybrać **wszystkie** źródła. Agreguje wszystkie źródła danych zamiast używać tylko jednego. Przyczyną tego błędu jest to, że użytkownicy lokalnego repozytorium często chcą uniknąć przypadkowego zainstalowania pakietu zdalnego ze względu na zasady korporacyjne.

**Mam wiele projektów w tym samym folderze, jak mogę używać oddzielnych plików packages.config dla każdego projektu?**

W większości projektów, w których oddzielne projekty znajdują się w oddzielnych folderach, nie jest to problem, ponieważ program NuGet identyfikuje `packages.config` pliki w każdym projekcie. W przypadku programu NuGet 3.3 + i wielu projektów w tym samym folderze można wstawić nazwę projektu do `packages.config` nazwy pliku, użyj wzorca `packages.{project-name}.config` , a NuGet używa tego pliku.

Nie jest to problem występujący podczas korzystania z programu PackageReference, ponieważ każdy plik projektu zawiera własną listę zależności.

**Nie widzę nuget.org na liście repozytoriów, jak to zrobić?**

- Dodaj `https://api.nuget.org/v3/index.json` do listy źródeł lub
- Usuń `%appdata%\.nuget\NuGet.Config` System (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) i pozwól, aby pakiet NuGet został utworzony ponownie.
