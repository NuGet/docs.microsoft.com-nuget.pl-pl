---
title: Omówienie i przepływ pracy korzystania z pakietów NuGet
description: Omówienie procesu zużywania pakietów NuGet w projekcie z linkami do innych określonych części procesu.
author: JonDouglas
ms.author: jodou
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: d1d6df3bcc36d8a78fcee97099b301c9ffc440d9
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323638"
---
# <a name="package-consumption-workflow"></a>Przepływ pracy użycia pakietów

Między nuget.org prywatnymi i prywatnymi galeriami pakietów, które organizacja może ustanowić, możesz znaleźć dziesiątki tysięcy wysoce przydatnych pakietów do użycia w aplikacjach i usługach. Jednak niezależnie od źródła, korzystanie z pakietu jest w tym samym ogólnym przepływie pracy.

![Przepływ przechodzący do źródła pakietu, znajdowania pakietu, instalowania go w projekcie, a następnie dodawania instrukcji using i wywołań do interfejsu API pakietu](media/Overview-01-GeneralFlow.png)

\*_Visual Studio tylko `dotnet.exe` i . Polecenie `nuget install` nie modyfikuje plików projektu ani `packages.config` pliku. Wpisy muszą być zarządzane ręcznie._

Aby uzyskać więcej informacji, zobacz [Znajdowanie i wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md) oraz Co się [dzieje po zainstalowaniu pakietu?](../concepts/package-installation-process.md).

NuGet zapamiętuje tożsamość i numer wersji każdego zainstalowanego pakietu, rejestrując go w pliku projektu (przy użyciu [funkcji PackageReference](../consume-packages/package-references-in-project-files.md)) lub , w zależności od typu projektu i wersji [`packages.config`](../reference/packages-config.md) pakietu NuGet. W przypadku pakietu NuGet 4.0+, preferowany jest packageReference, chociaż można to Visual Studio za pomocą interfejsu [Menedżer pakietów użytkownika.](install-use-packages-visual-studio.md) W każdym przypadku możesz w dowolnym momencie zajrzeć do odpowiedniego pliku, aby wyświetlić pełną listę zależności dla projektu.

> [!Tip]
> Warto zawsze sprawdzać licencję dla każdego pakietu, który ma być w tym oprogramowaniu. Na nuget.org stronie opisu każdego pakietu znajduje się **link** Informacje o licencji. Jeśli pakiet nie zawiera postanowień licencyjnych, skontaktuj się bezpośrednio z właścicielem pakietu przy użyciu linku **Skontaktuj** się z właścicielami na stronie pakietu. Firma Microsoft nie udziela Licencjobiorcy licencji na własność intelektualną od zewnętrznych dostawców pakietów i nie jest odpowiedzialna za informacje udostępniane przez osoby trzecie.

Podczas instalowania pakietów pakiet NuGet zwykle sprawdza, czy pakiet jest już dostępny w jego pamięci podręcznej. Tę pamięć podręczną można wyczyścić ręcznie z wiersza polecenia zgodnie z opisem w tece [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej.](../consume-packages/managing-the-global-packages-and-cache-folders.md)

Program NuGet zapewnia również zgodność platform docelowych obsługiwanych przez pakiet z projektem. Jeśli pakiet nie zawiera zgodnych zestawów, nuGet wyświetla błąd. Zobacz [Rozwiązywanie problemów z niezgodnymi pakietami](../concepts/dependency-resolution.md#resolving-incompatible-package-errors).

Podczas dodawania kodu projektu do repozytorium źródłowego zazwyczaj nie dołącza się pakietów NuGet. Osoby, które później sklonują repozytorium lub w inny sposób uzyskają projekt, w tym agentów kompilacji w systemach takich jak Visual Studio Team Services, muszą przywrócić niezbędne pakiety przed uruchomieniem kompilacji:

![Przepływ przywracania pakietów NuGet przez klonowanie repozytorium i używanie polecenia przywracania](media/Overview-02-RestoreFlow.png)

[Przywracanie pakietu](../consume-packages/package-restore.md) używa informacji w pliku projektu lub `packages.config` do ponownego zainstalowania wszystkich zależności. Należy pamiętać, że istnieją różnice w tym procesie, zgodnie z opisem w [rozwiązywaniu zależności](../concepts/dependency-resolution.md). Ponadto na powyższym diagramie nie pokazano polecenia przywracania dla konsoli programu Menedżer pakietów, ponieważ jeśli używasz konsoli programu , jesteś już w kontekście programu Visual Studio, który zazwyczaj automatycznie przywraca pakiety i udostępnia polecenie na poziomie rozwiązania, jak pokazano.

Czasami konieczne jest ponowne zainstalowanie pakietów, które są już zawarte w projekcie, co może również spowodować ponowne zainstalowanie zależności. Można to łatwo zrobić za pomocą `nuget reinstall` polecenia lub konsoli Menedżer pakietów NuGet. Aby uzyskać szczegółowe informacje, zobacz [Ponowne instalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md).

Na koniec zachowanie programu NuGet jest oparte na `NuGet.Config` plikach. Wiele plików może służyć do scentralizować niektóre ustawienia na różnych poziomach, jak wyjaśniono w konfigurowanie [zachowania NuGet](../consume-packages/configuring-nuget-behavior.md).

## <a name="ways-to-install-a-nuget-package"></a>Sposoby instalowania pakietu NuGet

Pakiety NuGet są pobierane i instalowane przy użyciu dowolnej z metod z poniższej tabeli.

| Narzędzie | Platformy | Opis |
| --- | --- | --- |
| [Interfejs wiersza polecenia dotnet](install-use-packages-dotnet-cli.md) | Wszystko | Narzędzie interfejsu wiersza polecenia dla platformy .NET Core .NET Standard bibliotek i projektów w stylu zestawu SDK, które są .NET Framework (zobacz [atrybut zestawu SDK](/dotnet/core/tools/csproj#additions)). Pobiera pakiet identyfikowany przez \<package_name\> i dodaje odwołanie do pliku projektu. Pobiera również i instaluje zależności. |
| Visual Studio | Windows i Mac | Udostępnia interfejs użytkownika, za pomocą którego można przeglądać, wybierać i instalować pakiety oraz ich zależności w projekcie z określonego źródła pakietu. Dodaje odwołania do zainstalowanych pakietów do pliku projektu.<ul><li>[Instalowanie pakietów i zarządzanie nimi przy użyciu Visual Studio](install-use-packages-visual-studio.md)</li><li>[Łącznie z pakietem NuGet w projekcie (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| [Konsola menedżera pakietów (Visual Studio)](install-use-packages-powershell.md) | Tylko Windows | Pobiera i instaluje pakiet identyfikowany przez z wybranego źródła do określonego projektu w rozwiązaniu, a następnie dodaje \<package_name\> odwołanie do pliku projektu. Pobiera również i instaluje zależności. |
| [Interfejs wiersza polecenia nuget.exe](install-use-packages-nuget-cli.md) | Wszystko | Narzędzie interfejsu wiersza polecenia dla .NET Framework i projektów innych niż w stylu zestawu SDK, które są .NET Standard biblioteki. Pobiera pakiet zidentyfikowany przez i rozwija jego zawartość do folderu w bieżącym katalogu; może również pobrać wszystkie \<package_name\> pakiety wymienione w `packages.config` pliku. Ponadto pobiera i instaluje zależności, ale nie wprowadza żadnych zmian w plikach projektu lub `packages.config` . |
