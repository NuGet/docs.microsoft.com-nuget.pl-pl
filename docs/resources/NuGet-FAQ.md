---
title: NuGet Często zadawane pytania
description: Typowe pytania i odpowiedzi dotyczące używania programu NuGet w wierszu polecenia i programie Visual Studio
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 8cc990e0c9eed07c59c8dffb04d104be47051736
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "69999940"
---
# <a name="nuget-frequently-asked-questions"></a>NuGet często zadawane pytania

W przypadku często zadawanych pytań dotyczących NuGet.org, takich jak NuGet.org pytania dotyczące konta, zobacz [NuGet.org często zadawane pytania](../nuget-org/nuget-org-faq.md).

**Co jest wymagane do uruchomienia NuGet?**

Wszystkie informacje dotyczące zarówno interfejsu użytkownika, jak i narzędzi wiersza polecenia są dostępne w [przewodniku instalacji](../install-nuget-client-tools.md).

**Czy NuGet obsługuje mono?**

Narzędzie wiersza polecenia `nuget.exe`, buduje i działa w obszarze Mono 3.2+ i może tworzyć pakiety w mono.

Chociaż `nuget.exe` działa w pełni w systemie Windows, istnieją znane problemy w systemie Linux i OS X. Zapoznaj się z [problemami mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) w usłudze GitHub.

[Klient graficzny](https://github.com/mrward/monodevelop-nuget-addin) jest dostępny jako dodatek dla MonoDevelop.

**Jak mogę ustalić, co zawiera pakiet i czy jest stabilny i przydatny dla mojej aplikacji?**

Głównym źródłem nauki o pakiecie jest jego strona z listą w nuget.org (lub innym prywatnym pliku danych). Każda strona pakietu na nuget.org zawiera opis pakietu, jego historię wersji i statystyki użycia. Sekcja **Informacje** na stronie pakietu zawiera również łącze do witryny sieci Web projektu, w której zazwyczaj znajduje się wiele przykładów i innej dokumentacji, która pomoże Ci dowiedzieć się, jak pakiet jest używany.

Aby uzyskać więcej informacji, zobacz [Znajdowanie i wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md).

## <a name="nuget-in-visual-studio"></a>NuGet w programie Visual Studio

**Jak jest obsługiwany program NuGet w różnych produktach programu Visual Studio?**

- Program Visual Studio w systemie Windows obsługuje [interfejs użytkownika Menedżera pakietów](../consume-packages/install-use-packages-visual-studio.md) i [konsolę Menedżera pakietów](../consume-packages/install-use-packages-powershell.md).
- Visual Studio dla komputerów Mac ma wbudowane funkcje NuGet, zgodnie z opisem w [including pakietu NuGet w projekcie.](/visualstudio/mac/nuget-walkthrough)
- Visual Studio Code (wszystkie platformy) nie ma żadnej bezpośredniej integracji NuGet. Użyj [interfejsu wiersza polecenia NuGet](../reference/nuget-exe-cli-reference.md) lub [dotnet CLI](../reference/dotnet-commands.md).
- Usługa Azure DevOps udostępnia [krok kompilacji w celu przywrócenia pakietów NuGet.](/vsts/build-release/tasks/package/nuget) Można również [hostować prywatne źródła danych pakietu NuGet w usłudze Azure DevOps.](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish)

**Jak sprawdzić dokładną wersję zainstalowanych narzędzi NuGet?**

W programie Visual Studio użyj polecenia **Pomoc > Informacje o programie Microsoft Visual Studio** i przyjrzyj się wersji wyświetlanej obok Menedżera **pakietów NuGet**.

Alternatywnie uruchom konsolę Menedżera**pakietów (Narzędzia > Menedżer pakietów NuGet > konsoli Menedżera pakietów)** i wprowadź, `$host` aby wyświetlić informacje o NuGet, w tym wersję.

**Jakie języki programowania są obsługiwane przez NuGet?**

NuGet zazwyczaj działa dla języków platformy .NET i jest przeznaczony do wprowadzenia bibliotek platformy .NET do projektu. Ponieważ obsługuje również automatyzacji MSBuild i Visual Studio w niektórych typach projektów, obsługuje również inne projekty i języki w różnym stopniu.

Najnowsza wersja NuGet obsługuje C#, Visual Basic, F#, WiX i C++.

**Jakie szablony projektów są obsługiwane przez NuGet?**

NuGet ma pełną obsługę różnych szablonów projektów, takich jak Windows, Web, Chmura, SharePoint, Wix i tak dalej.

**Jak zaktualizować pakiety, które są częścią szablonów programu Visual Studio?**

Przejdź do karty **Aktualizacje** w interfejsie użytkownika Menedżera pakietów i wybierz pozycję **Aktualizuj wszystko**lub użyj [ `Update-Package` polecenia](../reference/ps-reference/ps-ref-update-package.md) z konsoli Menedżera pakietów.

Aby zaktualizować sam szablon, należy ręcznie zaktualizować repozytorium szablonów. Zobacz [blog Xavier Decoster](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) na ten temat. Należy zauważyć, że odbywa się to na własne ryzyko, ponieważ ręczne aktualizacje mogą uszkodzić szablon, jeśli najnowsza wersja wszystkich zależności nie są ze sobą zgodne.

**Czy można używać NuGet poza programem Visual Studio?**

Tak, NuGet działa bezpośrednio z wiersza polecenia. Zobacz [przewodnik instalacji](../install-nuget-client-tools.md) i [odwołanie do interfejsu wiersza polecenia](../reference/nuget-exe-cli-reference.md).

## <a name="nuget-command-line"></a>Wiersz polecenia NuGet

**Jak uzyskać najnowszą wersję narzędzia wiersza polecenia NuGet?**

Zobacz [przewodnik instalacji](../install-nuget-client-tools.md). Aby sprawdzić aktualną zainstalowaną wersję `nuget help`narzędzia, użyj programu .

**Co to jest licencja dla nuget.exe?**

Możesz redystrybuować nuget.exe zgodnie z warunkami licencji MIT. Użytkownik jest odpowiedzialny za aktualizowanie i obsługę wszelkich kopii pliku nuget.exe, które użytkownik zdecyduje się rozpowszechniać.

**Czy możliwe jest rozszerzenie narzędzia wiersza polecenia NuGet?**

Tak, możliwe jest dodanie niestandardowych `nuget.exe`poleceń do , jak opisano w [poście Roba Reynolda.](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx)

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>Konsola Menedżera pakietów NuGet (program Visual Studio w systemie Windows)

**Jak uzyskać dostęp do obiektu DTE w konsoli Menedżera pakietów?**

Obiekt najwyższego poziomu w modelu obiektów automatyzacji programu Visual Studio nosi nazwę obiektu DTE (Development Tools Environment). Konsola zapewnia to za `$DTE`pośrednictwem zmiennej o nazwie . Aby uzyskać więcej informacji, zobacz [Omówienie modelu automatyzacji](/visualstudio/extensibility/internals/automation-model-overview) w dokumentacji programu Visual Studio rozszerzalności.

**Próbuję rzutować zmienną $DTE na typ DTE2, ale pojawia się błąd: Nie można przekonwertować wartości "EnvDTE.DTEClass" typu "EnvDTE.DTEClass" na typ "EnvDTE80.DTE2". Co jest nie tak?**

Jest to znany problem z tym, jak program PowerShell współdziała z obiektem COM. Spróbuj wykonać następujące kroki:

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface`jest funkcją pomocnika dodaną przez hosta programu NuGet PowerShell.

## <a name="creating-and-publishing-packages"></a>Tworzenie i publikowanie pakietów

**Jak wyświetlić listę paczki w pliku danych?**

Zobacz [Tworzenie i publikowanie pakietu](../quickstart/create-and-publish-a-package.md).

**Mam wiele wersji mojej biblioteki, które są przeznaczone dla różnych wersji programu .NET Framework. Jak utworzyć pojedynczy pakiet, który obsługuje ten pakiet?**

Zobacz [Obsługa wielu wersji i profili programu .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).

**Jak skonfigurować własne repozytorium lub kanał informacyjny?**

Zobacz [omówienie pakietów hostingowych](../hosting-packages/overview.md).

**Jak zbiorczo przesyłać pakiety do mojego kanału NuGet?**

Zobacz [zbiorcze publikowanie pakietów NuGet](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).

## <a name="working-with-packages"></a>Praca z pakietami

**Jaka jest różnica między pakietem na poziomie projektu a pakietem na poziomie rozwiązania?**

Pakiet na poziomie rozwiązania (NuGet 3.x+) jest instalowany tylko raz w rozwiązaniu i jest następnie dostępny dla wszystkich projektów w rozwiązaniu. Pakiet na poziomie projektu jest zainstalowany w każdym projekcie, który go używa. Pakiet na poziomie rozwiązania może również zainstalować nowe polecenia, które mogą być wywoływane z poziomu konsoli Menedżera pakietów.

**Czy możliwe jest zainstalowanie pakietów NuGet bez połączenia z Internetem?**

Tak, zobacz Scott Hanselman's Blog post [Jak uzyskać dostęp NuGet, gdy nuget.org jest w dół (lub jesteś w samolocie)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).

**Jak zainstalować pakiety w innej lokalizacji niż folder pakietów domyślnych?**

Ustaw [`repositoryPath`](../reference/nuget-config-file.md#config-section) ustawienie `Nuget.Config` w `nuget config -set repositoryPath=<path>`użyciu .

**Jak uniknąć dodawania folderu Pakiety NuGet do kontroli źródła?**

Ustaw [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) w `Nuget.Config` `true`. Ten klucz działa na poziomie rozwiązania i dlatego `$(Solutiondir)\.nuget\Nuget.Config` należy dodać do pliku. Włączenie przywracania pakietu z programu Visual Studio automatycznie tworzy ten plik.

**Jak wyłączyć przywracanie pakietu?**

Zobacz [Włączanie i wyłączanie przywracania pakietu](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).

**Dlaczego podczas instalowania pakietu lokalnego z zależnościami zdalnymi jest "Nie można rozwiązać błędu zależności"?**

Należy wybrać **wszystkie** źródła podczas instalowania pakietu lokalnego w projekcie. Spowoduje to agregację wszystkich kanałów, a nie tylko jeden. Powodem pojawia się ten błąd jest to, że użytkownicy lokalnego repozytorium często chcą uniknąć przypadkowego zainstalowania pakietu zdalnego z powodu firmowej zasady.

**Mam wiele projektów w tym samym folderze, jak mogę używać oddzielnych plików packages.config dla każdego projektu?**

W większości projektów, w których oddzielne projekty znajdują się w oddzielnych `packages.config` folderach, nie jest to problem, ponieważ NuGet identyfikuje pliki w każdym projekcie. Z NuGet 3.3+ i wiele projektów w tym samym folderze, `packages.config` można wstawić nazwę `packages.{project-name}.config`projektu do nazw plików użyć wzorca i NuGet używa tego pliku.

Nie jest to problem podczas korzystania z PackageReference, ponieważ każdy plik projektu zawiera własną listę zależności.

**Nie widzę nuget.org na mojej liście repozytoriów, jak mogę go odzyskać?**

- Dodaj `https://api.nuget.org/v3/index.json` do listy źródeł lub
- Usuń `%appdata%\.nuget\NuGet.Config` (Windows) `~/.nuget/NuGet/NuGet.Config` lub (Mac/Linux) i pozwól NuGet odtworzyć go.
