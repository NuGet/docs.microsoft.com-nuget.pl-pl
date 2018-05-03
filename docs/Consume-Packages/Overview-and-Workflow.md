---
title: Omówienie i przepływ pracy za pomocą pakietów NuGet
description: Omówienie procesu eksploatującego pakietów NuGet w projekcie, wraz z łączami do innych części określonego procesu.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: 765b48b474aee17415f53491514bf6e9d50af010
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="package-consumption-workflow"></a>Przepływ pracy zużycie pakietu

Między nuget.org i prywatnej pakietu galerii, które organizacja może ustanawiać można znaleźć dziesiątki tysięcy bardzo przydatne pakietów do użycia w aplikacji i usług. Ale niezależnie od tego źródła, korzystających z pakietu następuje tego samego ogólnego przepływu pracy.

![Przepływ przechodząc do źródła pakietu, znajdowanie pakietu, instalując je w projekcie, a następnie dodawanie przy użyciu instrukcji i wywołania interfejsu API pakietu](media/Overview-01-GeneralFlow.png)

\* _Program Visual Studio i dotnet.ex "tylko. Polecenie install nuget nie modyfikuje pliki projektu lub pliku packages.config; wpisy muszą być zarządzane ręcznie._

Aby uzyskać szczegółowe informacje, zobacz [wyszukiwanie i Wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md) i [różne sposoby, można zainstalować pakietu NuGet](ways-to-install-a-package.md).

NuGet pamięta tożsamości oraz numeru wersji każdego zainstalowanego pakietu nagrywania albo [ `packages.config` ](../reference/packages-config.md) lub pliku projektu (przy użyciu [PackageReference](../consume-packages/package-references-in-project-files.md)), w zależności od typu projektu i wersja programu NuGet. Nuget 4.0 +, PackageReference jest preferowana, ale jest to można skonfigurować w programie Visual Studio za pomocą [opcji interfejsu użytkownika Menedżera pakietów](../tools/package-manager-ui.md). W każdym przypadku można przeglądać odpowiedniego pliku w dowolnym momencie, aby zobaczyć pełną listę zależności dla projektu.

> [!Tip]
> Zaleca się sprawdzać licencja na każdy pakiet, który ma być używany w oprogramowaniu. Na nuget.org, możesz znaleźć **informacje dotyczące licencji** łącza w prawej części strony opis każdego pakietu. Jeśli pakiet nie określa postanowienia licencyjne, skontaktuj się z właścicielem pakietu bezpośrednio za pomocą **skontaktuj się z właścicieli** łącze na stronie pakiet. Microsoft nie licencji jakiejkolwiek własności intelektualnej użytkownikowi od innych dostawców pakietu i nie jest odpowiedzialny za informacji dostarczonych przez strony trzecie.

Podczas instalowania pakietów, NuGet zwykle sprawdza, czy pakiet jest już dostępne z pamięci podręcznej. Można ręcznie wyczyścić tę pamięć podręczną z wiersza polecenia, zgodnie z opisem na [Zarządzanie globalne pakietów i foldery pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).

NuGet również zapewnia, że docelowych platform obsługiwanych przez pakiet są zgodne z projektem. Jeśli pakiet zawiera zestawy zgodne, NuGet jest wyświetlany błąd. Zobacz [rozwiązywaniu problemów z błędami niezgodnych pakietu](dependency-resolution.md#resolving-incompatible-package-errors).

Podczas dodawania kodu projektu do repozytorium źródłowe, zwykle nie uwzględniono pakietów NuGet. Tych osób, które później sklonować repozytorium lub inny sposób uzyskać projektu, w tym agentów kompilacji w systemach, takich jak Visual Studio Team Services, musisz przywrócić niezbędne pakiety przed uruchomieniem kompilacji:

![Trwa przywracanie pakietów NuGet w klonowania repozytorium, a następnie użyć polecenia restore przepływu](media/Overview-02-RestoreFlow.png)

[Przywracanie pakietów](../consume-packages/package-restore.md) używa tych informacji w pliku projektu lub `packages.config` ponownie zainstalować wszystkie zależności. Należy pamiętać, że istnieją różnice w procesie związane, zgodnie z opisem w [rozpoznawania zależności](../consume-packages/dependency-resolution.md). Ponadto na powyższym diagramie nie są wyświetlane polecenia restore dla konsoli Menedżera pakietów, ponieważ jest z konsoli, użytkownik jest już w kontekście programu Visual Studio, co zwykle automatycznie przywraca pakietów i zapewnia polecenie rozwiązanie na poziomie, jak pokazano .

Czasami zachodzi konieczność ponownie zainstaluj pakiety, które znajdują się już w projekcie, mogą również ponownie zainstalować zależności. Jest to łatwo zrobić przy użyciu `nuget reinstall` polecenia lub konsoli Menedżera pakietów NuGet. Aby uzyskać więcej informacji, zobacz [ponowne zainstalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md).

Na koniec zachowanie NuGet jest wymuszany przez `Nuget.Config` plików. Wiele plików może służyć do scentralizowanie pewnych ustawień na różnych poziomach, zgodnie z objaśnieniem w [Konfigurowanie zachowania NuGet](../consume-packages/configuring-nuget-behavior.md).

Owocnej pracy z produktywne kodowanie dzięki funkcjom pakietów NuGet
