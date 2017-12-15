---
title: "Omówienie i przepływ pracy za pomocą pakietów NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3c60f920-457d-4f43-9efe-210c514e5242
description: "Omówienie procesu eksploatującego pakietów NuGet w projekcie, wraz z łączami do innych części określonego procesu."
keywords: "Użycie pakietu NuGet, omówienie zużycia NuGet, przepływ pracy zużycia NuGet, przepływu pracy przez pakiet, omówienie zużycie pakietu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c48351cb6fed0ac94bd437d9443811f46c032bd0
ms.sourcegitcommit: 122bf7ce308365ea45da018b0768f0536de76a1f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="package-consumption-workflow"></a>Przepływ pracy zużycie pakietu

Między nuget.org i prywatnej pakietu galerii, które organizacja może ustanawiać można znaleźć dziesiątki tysięcy bardzo przydatne pakietów do użycia w aplikacji i usług. Ale niezależnie od tego źródła, korzystających z pakietu następuje tego samego ogólnego przepływu pracy w sposób przedstawiony poniżej. Aby uzyskać więcej informacji, zobacz [wyszukiwanie i Wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md) i [Użyj szybkiego startu pakiet](../quickstart/use-a-package.md).

![Przepływ przechodząc do źródła pakietu, znajdowanie pakietu, instalując je w projekcie, a następnie dodawanie przy użyciu instrukcji i wywołania interfejsu API pakietu](media/Overview-01-GeneralFlow.png)

\*_z wyjątkiem z `nuget install` z wiersza polecenia, w którym to przypadku należy edytować konfigurację pliki ręcznie. Zobacz [zainstalować poleceń](../tools/cli-ref-install.md)._

NuGet pamięta tożsamości oraz numeru wersji każdego zainstalowanego pakietu nagrywania albo `packages.config`, plik projektu lub `project.json` pliku w katalogu głównym projektu, w zależności od używanej wersji programu NuGet i typ projektu. Nuget 4.0 + [przechowywanie zależności w pliku projektu](../consume-packages/package-references-in-project-files.md) jest ustawieniem domyślnym (z wyjątkiem projekty platformy UWP przeznaczonych dla systemu Windows 10 RS1). W każdym przypadku można przeglądać odpowiedniego pliku w dowolnym momencie, aby zobaczyć pełną listę zależności dla projektu.

> [!Tip]
> Zaleca się sprawdzać licencja na każdy pakiet, który ma być używany w oprogramowaniu. Znajdziesz nuget.org, **informacje dotyczące licencji** łącza w prawej części strony opis każdego pakietu. Jeśli pakiet nie określa postanowienia licencyjne, skontaktuj się z właścicielem pakietu bezpośrednio za pomocą **skontaktuj się z właścicieli** łącze na stronie pakiet. Microsoft nie licencji jakiejkolwiek własności intelektualnej użytkownikowi od innych dostawców pakietu i nie jest odpowiedzialny za informacji dostarczonych przez strony trzecie.

Podczas instalowania pakietów, NuGet zwykle sprawdza, czy pakiet jest już dostępne z pamięci podręcznej. Można ręcznie wyczyścić tę pamięć podręczną z wiersza polecenia, zgodnie z opisem na [Zarządzanie pamięci podręcznej NuGet](../consume-packages/managing-the-nuget-cache.md).

NuGet również zapewnia, że docelowych platform obsługiwanych przez pakiet są zgodne z projektem. Jeśli pakiet zawiera zestawy zgodne, NuGet otrzymasz komunikat o błędzie. Zobacz [rozwiązywaniu problemów z błędami niezgodnych pakietu](dependency-resolution.md#resolving-incompatible-package-errors).

Podczas dodawania kodu projektu do repozytorium źródłowe, zwykle nie uwzględniono pakietów NuGet. Osób, które później Klonuj repozytorium, w tym agentów kompilacji w systemach, takich jak Visual Studio Team Services, musisz przywrócić niezbędne pakiety przed uruchomieniem kompilacji:

![Trwa przywracanie pakietów NuGet w klonowania repozytorium, a następnie użyć polecenia restore przepływu](media/Overview-02-RestoreFlow.png)

[Przywracanie pakietów](../consume-packages/package-restore.md) używa tych informacji w pliku projektu `packages.config`, `project.json` ponownie zainstalować wszystkie zależności. Należy pamiętać, że istnieją różnice w procesie związane, zgodnie z opisem w [rozpoznawania zależności](../consume-packages/dependency-resolution.md).

Czasami zachodzi konieczność ponownie zainstaluj pakiety, które znajdują się już w projekcie, mogą również ponownie zainstalować zależności. Jest to łatwo zrobić przy użyciu `reinstall` polecenia za pomocą wiersza polecenia NuGet lub konsoli Menedżera pakietów NuGet. Aby uzyskać więcej informacji, zobacz [ponowne zainstalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md).

Na koniec zachowanie NuGet jest wymuszany przez `Nuget.Config` plików konfiguracyjnych. Wiele plików może służyć do scentralizowanie pewnych ustawień na różnych poziomach, zgodnie z objaśnieniem w [Konfigurowanie zachowania NuGet](../consume-packages/configuring-nuget-behavior.md).

Owocnej pracy z produktywne kodowanie dzięki funkcjom pakietów NuGet
