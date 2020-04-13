---
title: Omówienie i przepływ pracy przy użyciu pakietów NuGet
description: Omówienie procesu korzystania z pakietów NuGet w projekcie, z łączami do innych określonych części procesu.
author: karann-msft
ms.author: karann
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: ddd1d163e18ed4ce1e7cbf41ed152acc40c1c423
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428885"
---
# <a name="package-consumption-workflow"></a>Przepływ pracy zużycia pakietów

Między nuget.org i prywatnymi galeriami pakietów, które może ustanowić organizacja, można znaleźć dziesiątki tysięcy bardzo przydatnych pakietów do użycia w aplikacjach i usługach. Ale niezależnie od źródła, korzystanie z pakietu następuje tego samego ogólnego przepływu pracy.

![Przepływ przechodzenia do źródła pakietu, znajdowania pakietu, instalowania go w projekcie, a następnie dodawania instrukcji using i wywołania interfejsu API pakietu](media/Overview-01-GeneralFlow.png)

\*_Visual Studio `dotnet.exe` i tylko. Polecenie `nuget install` nie modyfikuje plików `packages.config` projektu ani pliku; wpisów muszą być zarządzane ręcznie._

Aby uzyskać więcej informacji, zobacz [Znajdowanie i wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md) i [Co się stanie, gdy pakiet jest zainstalowany?](../concepts/package-installation-process.md).

NuGet zapamiętuje tożsamość i numer wersji każdego zainstalowanego pakietu, zapisując go [`packages.config`](../reference/packages-config.md)w pliku projektu (przy użyciu [PackageReference)](../consume-packages/package-references-in-project-files.md)lub , w zależności od typu projektu i wersji NuGet. Z NuGet 4.0+, PackageReference jest preferowane, chociaż jest to konfigurowalne w programie Visual Studio za pośrednictwem [interfejsu użytkownika Menedżera pakietów.](install-use-packages-visual-studio.md) W każdym przypadku można szukać w odpowiednim pliku w dowolnym momencie, aby wyświetlić pełną listę zależności dla projektu.

> [!Tip]
> Rozsądne jest, aby zawsze sprawdzić licencję dla każdego pakietu, który zamierzasz używać w oprogramowaniu. Na nuget.org po prawej stronie strony opisu każdego pakietu znajduje się łącze **Informacje o licencji.** Jeśli pakiet nie określa postanowień licencyjnych, skontaktuj się z właścicielem pakietu bezpośrednio za pomocą łącza **Skontaktuj się z właścicielami** na stronie pakietu. Firma Microsoft nie udziela licencji na żadne prawa własności intelektualnej od zewnętrznych dostawców pakietów i nie ponosi odpowiedzialności za informacje dostarczone przez osoby trzecie.

Podczas instalowania pakietów, NuGet zazwyczaj sprawdza, czy pakiet jest już dostępny z jego pamięci podręcznej. Tę pamięć podręczną można usunąć ręcznie z wiersza polecenia, zgodnie z opisem w temacie [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).

NuGet również upewnia się, że struktury docelowe obsługiwane przez pakiet są zgodne z projektem. Jeśli pakiet nie zawiera zgodnych zestawów, NuGet wyświetla błąd. Zobacz [Rozwiązywanie niezgodnych błędów pakietu](../concepts/dependency-resolution.md#resolving-incompatible-package-errors).

Podczas dodawania kodu projektu do repozytorium źródłowego zazwyczaj nie zawierają pakietów NuGet. Ci, którzy później sklonować repozytorium lub w inny sposób uzyskać projekt, w tym agentów kompilacji w systemach takich jak Visual Studio Team Services, należy przywrócić niezbędne pakiety przed uruchomieniem kompilacji:

![Przepływ przywracania pakietów NuGet przez klonowanie repozytorium i używanie polecenia przywracania](media/Overview-02-RestoreFlow.png)

[Narzędzie Przywracanie pakietu](../consume-packages/package-restore.md) używa informacji `packages.config` w pliku projektu lub ponownej instalacji wszystkich zależności. Należy zauważyć, że istnieją różnice w procesie, zgodnie z opisem w [rozpoznawaniu zależności](../concepts/dependency-resolution.md). Ponadto na powyższym diagramie nie pokazano polecenia przywracania konsoli Menedżera pakietów, ponieważ jeśli korzystasz z konsoli, jesteś już w kontekście programu Visual Studio, który zazwyczaj automatycznie przywraca pakiety i udostępnia polecenie na poziomie rozwiązania, jak pokazano.

Od czasu do czasu konieczne jest ponowne zainstalowanie pakietów, które są już uwzględnione w projekcie, które mogą również ponownie zainstalować zależności. Jest to łatwe do `nuget reinstall` wykonania za pomocą polecenia lub konsoli Menedżera pakietów NuGet. Aby uzyskać szczegółowe informacje, zobacz [Ponowne instalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md).

Na koniec zachowanie NuGet jest `Nuget.Config` napędzany przez pliki. Wiele plików może służyć do scentralizowania niektórych ustawień na różnych poziomach, jak wyjaśniono w [konfiguracji zachowania NuGet](../consume-packages/configuring-nuget-behavior.md).

## <a name="ways-to-install-a-nuget-package"></a>Sposoby instalowania pakietu NuGet

Pakiety NuGet są pobierane i instalowane przy użyciu dowolnej z metod w poniższej tabeli.

| Narzędzie | Opis |
| --- | --- |
| [interfejsu wiersza polecenia dotnet.exe](install-use-packages-dotnet-cli.md) | (Wszystkie platformy) Narzędzie INTERFEJSU WIERSZA dla bibliotek .NET Core i .NET Standard oraz dla projektów w stylu zestawu SDK przeznaczonych dla programu .NET Framework (zobacz [atrybut SDK](/dotnet/core/tools/csproj#additions)). Pobiera pakiet identyfikowany \<przez\> package_name i dodaje odwołanie do pliku projektu. Pobiera również i instaluje zależności. |
| Visual Studio | (Windows i Mac) Udostępnia interfejs użytkownika, za pomocą którego można przeglądać, wybierać i instalować pakiety i ich zależności w projekcie z określonego źródła pakietu. Dodaje odwołania do zainstalowanych pakietów do pliku projektu.<ul><li>[Instalowanie pakietów i zarządzanie nimi przy użyciu programu Visual Studio](install-use-packages-visual-studio.md)</li><li>[Dołączanie pakietu NuGet do projektu (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| [Konsola menedżera pakietów (Visual Studio)](install-use-packages-powershell.md) | (tylko system Windows) Pobiera i instaluje pakiet \<zidentyfikowany przez\> package_name z wybranego źródła do określonego projektu w rozwiązaniu, a następnie dodaje odwołanie do pliku projektu. Pobiera również i instaluje zależności. |
| [Interfejs wiersza polecenia nuget.exe](install-use-packages-nuget-cli.md) | (Wszystkie platformy) Narzędzie INTERFEJSU WIERSZA dla bibliotek programu .NET Framework i projektów w stylu innych niż SDK przeznaczonych dla bibliotek .NET Standard. Pobiera pakiet identyfikowany \<przez package_name\> i rozszerza jego zawartość do folderu w bieżącym katalogu; można również pobrać wszystkie pakiety wymienione w `packages.config` pliku. Pobiera również i instaluje zależności, ale nie `packages.config`wprowadza żadnych zmian w plikach projektu lub . |
