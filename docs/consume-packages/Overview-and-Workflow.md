---
title: Omówienie i przepływ pracy za pomocą pakietów NuGet
description: Przegląd procesu korzystanie z pakietów NuGet w projekcie, wraz z łączami do innych określonych części procesu.
author: karann-msft
ms.author: karann
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: 5f52b00e0c45882fb7a4bd1c1a80022192f3be6b
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580249"
---
# <a name="package-consumption-workflow"></a>Przepływ pracy zużyciu pakietu

Między nuget.org i galerie prywatne pakietu, które Twoja organizacja może ustanowić można znaleźć dziesiątki tysięcy pakietów bardzo przydatna do użycia w aplikacji i usług. Jednak niezależnie od źródła, korzystanie z pakietu poniżej tego samego ogólnego przepływu pracy.

![Przepływ do źródła pakietu, znajdowanie pakietu, zamontowany w projekcie, a następnie dodanie przy użyciu instrukcji i wywołania interfejsu API pakietu](media/Overview-01-GeneralFlow.png)

\* _Program Visual Studio i `dotnet.exe` tylko. `nuget install` Polecenie nie powoduje modyfikacji plików projektu lub `packages.config` pliku; wpisów, które muszą być zarządzane ręcznie._

Aby uzyskać więcej informacji, zobacz [Znajdowanie i Wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md) i [różne sposoby, aby zainstalować pakiet NuGet](ways-to-install-a-package.md).

NuGet są przechowywane tożsamości i numeru wersji każdego zainstalowanego pakietu nagrywanie, albo [ `packages.config` ](../reference/packages-config.md) lub pliku projektu (przy użyciu [PackageReference](../consume-packages/package-references-in-project-files.md)), w zależności od typu projektu i Wersja pakietu nuget. Nuget 4.0 +, PackageReference jest preferowane, mimo że jest to można skonfigurować w programie Visual Studio za pośrednictwem [opcje interfejsu użytkownika Menedżera pakietów](../tools/package-manager-ui.md). W każdym przypadku można przeglądać odpowiedniego pliku w dowolnym momencie, aby zobaczyć pełną listę zależności dla Twojego projektu.

> [!Tip]
> Zaleca się do Zawsze sprawdzaj licencję dla każdego pakietu, który ma być używany w oprogramowaniu. W witrynie nuget.org, możesz znaleźć **informacji o licencji** łącza w prawej części strony opis każdego pakietu. Jeśli pakiet nie określa postanowienia licencyjne, skontaktuj się z właścicielem pakietu bezpośrednio przy użyciu **skontaktuj się z właścicielami** łącze na stronie pakiet. Microsoft nie licencji jakiejkolwiek własności intelektualnej dla Ciebie od dostawców pakietów innych firm, a nie jest odpowiedzialny za otrzymane od innych firm.

Podczas instalowania pakietów, NuGet zwykle sprawdza, jeśli pakiet jest już dostępna z pamięci podręcznej. Można ręcznie wyczyścić tę pamięć podręczną z wiersza polecenia, zgodnie z opisem na [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).

NuGet sprawia, że czy platform docelowych, obsługiwany przez pakiet są zgodne z projektem. Jeśli pakiet nie zawiera zgodne zestawy, NuGet wyświetla komunikat o błędzie. Zobacz [Rozwiązywanie błędów niezgodny pakiet](dependency-resolution.md#resolving-incompatible-package-errors).

Podczas dodawania projektu kodu do repozytorium źródłowego, zazwyczaj nie podasz pakietów NuGet. Tych, którzy później sklonować repozytorium lub inny sposób uzyskać projektu, w tym agentów kompilacji w systemach, takich jak Visual Studio Team Services, należy przywrócić niezbędne pakiety przed uruchomieniem kompilacji:

![Przepływ przywracania pakietów NuGet, klonowanie repozytorium i za pomocą polecenia restore](media/Overview-02-RestoreFlow.png)

[Przywracanie pakietu](../consume-packages/package-restore.md) korzysta z informacji w pliku projektu lub `packages.config` ponowną instalację wszystkich zależności. Należy pamiętać, że istnieją różnice w procesie związane, zgodnie z opisem w [rozpoznawania zależności](../consume-packages/dependency-resolution.md). Ponadto na powyższym diagramie nie są wyświetlane polecenia restore dla konsoli Menedżera pakietów, ponieważ jesteś za pomocą konsoli, użytkownik jest już w kontekście programu Visual Studio, co zwykle automatycznie przywraca pakietów i zapewnia polecenie poziomie rozwiązania, jak pokazano .

Czasami zachodzi konieczność ponownej instalacji pakietów, które znajdują się już w projekcie może również ponownie zainstalować zależności. Jest to łatwo zrobić za pomocą `nuget reinstall` polecenia lub konsoli Menedżera pakietów NuGet. Aby uzyskać więcej informacji, zobacz [ponowne zainstalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md).

Na koniec zachowanie NuGet jest wymuszany przez `Nuget.Config` plików. Wiele plików można scentralizować pewnych ustawień na różnych poziomach, zgodnie z objaśnieniem w [Konfigurowanie zachowania pakietu NuGet](../consume-packages/configuring-nuget-behavior.md).

Korzystaj z usługi produktywne kodowanie dzięki pakiety NuGet!
