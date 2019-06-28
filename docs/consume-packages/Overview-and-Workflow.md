---
title: Omówienie i przepływ pracy za pomocą pakietów NuGet
description: Przegląd procesu korzystanie z pakietów NuGet w projekcie, wraz z łączami do innych określonych części procesu.
author: karann-msft
ms.author: karann
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: eeae62a09a9f405d27cd113ff586393f6305ba47
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426710"
---
# <a name="package-consumption-workflow"></a>Przepływ pracy zużyciu pakietu

Między nuget.org i galerie prywatne pakietu, które Twoja organizacja może ustanowić można znaleźć dziesiątki tysięcy pakietów bardzo przydatna do użycia w aplikacji i usług. Jednak niezależnie od źródła, korzystanie z pakietu poniżej tego samego ogólnego przepływu pracy.

![Przepływ do źródła pakietu, znajdowanie pakietu, zamontowany w projekcie, a następnie dodanie przy użyciu instrukcji i wywołania interfejsu API pakietu](media/Overview-01-GeneralFlow.png)

\* _Program Visual Studio i `dotnet.exe` tylko. `nuget install` Polecenie nie powoduje modyfikacji plików projektu lub `packages.config` pliku; wpisów, które muszą być zarządzane ręcznie._

Aby uzyskać więcej informacji, zobacz [Znajdowanie i Wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md) i [co się stanie, gdy jest zainstalowany pakiet?](../concepts/package-installation-process.md).

NuGet są przechowywane tożsamości i numeru wersji każdego zainstalowanego pakietu nagrywanie, albo w pliku projektu (przy użyciu [PackageReference](../consume-packages/package-references-in-project-files.md)) lub [ `packages.config` ](../reference/packages-config.md), w zależności od typu projektu i Wersja pakietu nuget. Nuget 4.0 +, PackageReference jest preferowane, mimo że jest to można skonfigurować w programie Visual Studio za pośrednictwem [interfejs użytkownika Menedżera pakietów](../tools/package-manager-ui.md). W każdym przypadku można przeglądać odpowiedniego pliku w dowolnym momencie, aby zobaczyć pełną listę zależności dla Twojego projektu.

> [!Tip]
> Zaleca się do Zawsze sprawdzaj licencję dla każdego pakietu, który ma być używany w oprogramowaniu. W witrynie nuget.org, możesz znaleźć **informacji o licencji** łącza w prawej części strony opis każdego pakietu. Jeśli pakiet nie określa postanowienia licencyjne, skontaktuj się z właścicielem pakietu bezpośrednio przy użyciu **skontaktuj się z właścicielami** łącze na stronie pakiet. Microsoft nie licencji jakiejkolwiek własności intelektualnej dla Ciebie od dostawców pakietów innych firm, a nie jest odpowiedzialny za otrzymane od innych firm.

Podczas instalowania pakietów, NuGet zwykle sprawdza, jeśli pakiet jest już dostępna z pamięci podręcznej. Można ręcznie wyczyścić tę pamięć podręczną z wiersza polecenia, zgodnie z opisem na [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).

NuGet sprawia, że czy platform docelowych, obsługiwany przez pakiet są zgodne z projektem. Jeśli pakiet nie zawiera zgodne zestawy, NuGet wyświetla komunikat o błędzie. Zobacz [Rozwiązywanie błędów niezgodny pakiet](dependency-resolution.md#resolving-incompatible-package-errors).

Podczas dodawania projektu kodu do repozytorium źródłowego, zazwyczaj nie podasz pakietów NuGet. Tych, którzy później sklonować repozytorium lub inny sposób uzyskać projektu, w tym agentów kompilacji w systemach, takich jak Visual Studio Team Services, należy przywrócić niezbędne pakiety przed uruchomieniem kompilacji:

![Przepływ przywracania pakietów NuGet, klonowanie repozytorium i za pomocą polecenia restore](media/Overview-02-RestoreFlow.png)

[Przywracanie pakietu](../consume-packages/package-restore.md) korzysta z informacji w pliku projektu lub `packages.config` ponowną instalację wszystkich zależności. Należy pamiętać, że istnieją różnice w procesie związane, zgodnie z opisem w [rozpoznawania zależności](../consume-packages/dependency-resolution.md). Ponadto na powyższym diagramie nie są wyświetlane polecenia restore dla konsoli Menedżera pakietów, ponieważ w przypadku za pomocą konsoli użytkownik jest już w kontekście programu Visual Studio, która zwykle automatycznie przywraca pakietów oraz udostępnia polecenia poziomie rozwiązania jako wyświetlane.

Czasami zachodzi konieczność ponownej instalacji pakietów, które znajdują się już w projekcie może również ponownie zainstalować zależności. Jest to łatwo zrobić za pomocą `nuget reinstall` polecenia lub konsoli Menedżera pakietów NuGet. Aby uzyskać więcej informacji, zobacz [ponowne zainstalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md).

Na koniec zachowanie NuGet jest wymuszany przez `Nuget.Config` plików. Wiele plików można scentralizować pewnych ustawień na różnych poziomach, zgodnie z objaśnieniem w [Konfigurowanie zachowania pakietu NuGet](../consume-packages/configuring-nuget-behavior.md).

## <a name="ways-to-install-a-nuget-package"></a>Sposoby, aby zainstalować pakiet NuGet

Pakiety NuGet zostaną pobrane i zainstalowane przy użyciu dowolnej z metod w poniższej tabeli.

| Narzędzie | Opis |
| --- | --- |
| [DotNet.exe interfejsu wiersza polecenia](install-use-packages-dotnet-cli.md) | (Wszystkie platformy) Narzędzie interfejsu wiersza polecenia dla biblioteki .NET Core i .NET Standard, a dla zestawu SDK stylu projektów środowiska .NET Framework (zobacz [atrybutu zestawu SDK](/dotnet/core/tools/csproj#additions)). Pobiera pakiet identyfikowane przez \<nazwa_pakietu\> i dodaje odwołanie do pliku projektu. Ponadto umożliwia pobranie i zainstalowanie zależności. |
| Visual Studio | (Windows i Mac) Udostępnia interfejs użytkownika, za pomocą którego można przeglądać, wybierz i zainstalować pakiety i ich zależności do projektu ze źródła określonego pakietu. Dodaje odwołania do pakietów zainstalowanych w pliku projektu.<ul><li>[Instalowanie i zarządzanie pakietami za pomocą programu Visual Studio](../tools/package-manager-ui.md)</li><li>[Dołączanie pakietu NuGet w projekcie (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| [Program PowerShell w programie Visual Studio](../tools/package-manager-console.md) | (Tylko Windows) Pobiera i instaluje pakiet identyfikowane przez \<nazwa_pakietu\> z wybranego źródła do określonego projektu w rozwiązaniu, a następnie dodaje odwołanie do pliku projektu. Ponadto umożliwia pobranie i zainstalowanie zależności. |
| [Interfejs wiersza polecenia nuget.exe](install-use-packages-dotnet-cli.md) | (Wszystkie platformy) Narzędzie interfejsu wiersza polecenia do bibliotek .NET Framework i projektów innych stylu zestawu SDK, przeznaczonych dla biblioteki .NET Standard. Pobiera pakiet identyfikowane przez \<nazwa_pakietu\> i zwiększa jego zawartość do folderu w bieżącym katalogu; można także pobrać wszystkie pakiety wymienione w `packages.config` pliku. Również umożliwia pobranie i zainstalowanie zależności, ale nie wprowadza żadnych zmian w plikach projektu lub `packages.config`. |
