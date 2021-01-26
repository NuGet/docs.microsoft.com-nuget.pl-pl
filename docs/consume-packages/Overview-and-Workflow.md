---
title: Omówienie i przepływ pracy z użyciem pakietów NuGet
description: Przegląd procesu zużywania pakietów NuGet w projekcie z linkami do innych określonych części procesu.
author: JonDouglas
ms.author: jodou
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: 5f1856940a988e0585c29ccfd581d823e4f69921
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775067"
---
# <a name="package-consumption-workflow"></a>Przepływ pracy zużycia pakietów

Między nuget.org i prywatnymi galeriami pakietów, które organizacja może ustalić, można znaleźć dziesiątki tysięcy wysoce przydatnych pakietów do użycia w aplikacjach i usługach. Bez względu na to, że pakiet korzystający z pakietu jest zgodny z tym samym ogólnym przepływem pracy.

![Przepływ do źródła pakietów, wyszukiwanie pakietu, instalowanie go w projekcie, Dodawanie instrukcji using i wywołań do interfejsu API pakietu](media/Overview-01-GeneralFlow.png)

\*_Visual Studio i `dotnet.exe` tylko. `nuget install`Polecenie nie modyfikuje plików projektu lub `packages.config` pliku; wpisy muszą być zarządzane ręcznie._

Aby uzyskać więcej informacji, zobacz [Znajdowanie i wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md) oraz [to, co się dzieje po zainstalowaniu pakietu?](../concepts/package-installation-process.md).

Pakiet NuGet zapamiętuje tożsamość i numer wersji każdego z zainstalowanych pakietów, rejestrując go w pliku projektu (przy użyciu [PackageReference](../consume-packages/package-references-in-project-files.md)) lub [`packages.config`](../reference/packages-config.md) , w zależności od typu projektu i używanej wersji programu NuGet. W przypadku programu NuGet 4.0 + PackageReference jest preferowany, chociaż można go skonfigurować w programie Visual Studio za pomocą [interfejsu użytkownika Menedżera pakietów](install-use-packages-visual-studio.md). W każdym przypadku można w dowolnym momencie wyszukać odpowiedni plik, aby wyświetlić pełną listę zależności dla projektu.

> [!Tip]
> Należy zawsze sprawdzić licencję dla każdego pakietu, którego zamierzasz używać w oprogramowaniu. W witrynie nuget.org znajdziesz link **informacji o licencji** po prawej stronie strony opisu każdego pakietu. Jeśli pakiet nie określa postanowień licencyjnych, skontaktuj się z właścicielem pakietu bezpośrednio, korzystając z linku **właściciele kontaktu** na stronie pakiet. Firma Microsoft nie udziela licencji jakiejkolwiek własności intelektualnej od dostawców pakietów innych firm i nie ponosi odpowiedzialności za informacje udostępniane przez strony trzecie.

Podczas instalowania pakietów NuGet zwykle sprawdza, czy pakiet jest już dostępny w jego pamięci podręcznej. Możesz ręcznie wyczyścić tę pamięć podręczną z poziomu wiersza polecenia, zgodnie z opisem w temacie [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).

Pakiet NuGet gwarantuje również, że Platformy docelowe obsługiwane przez ten element są zgodne z projektem. Jeśli pakiet nie zawiera zgodnych zestawów, program NuGet wyświetli błąd. Zobacz [Rozwiązywanie niezgodnych błędów pakietów](../concepts/dependency-resolution.md#resolving-incompatible-package-errors).

W przypadku dodawania kodu projektu do repozytorium źródłowego zazwyczaj nie są uwzględniane pakiety NuGet. Osoby, które później sklonują repozytorium lub pozyskają projekt, w tym agentów kompilacji w systemach, takich jak Visual Studio Team Services, muszą przywrócić wymagane pakiety przed uruchomieniem kompilacji:

![Przepływ przywracania pakietów NuGet przez klonowanie repozytorium i użycie polecenia Restore](media/Overview-02-RestoreFlow.png)

[Przywracanie pakietu](../consume-packages/package-restore.md) używa informacji w pliku projektu lub `packages.config` do ponownego zainstalowania wszystkich zależności. Należy zauważyć, że występują różnice w procesie, zgodnie z opisem w temacie [rozpoznawanie zależności](../concepts/dependency-resolution.md). Ponadto na powyższym diagramie nie jest wyświetlane polecenie Restore dla konsoli Menedżera pakietów, ponieważ jeśli masz już konsolę programu Visual Studio, która zwykle przywraca pakiety automatycznie i udostępnia polecenie na poziomie rozwiązania, jak pokazano.

Czasami konieczne jest ponowne zainstalowanie pakietów, które już znajdują się w projekcie, co może również ponownie zainstalować zależności. Można to łatwo zrobić przy użyciu `nuget reinstall` polecenia lub konsoli Menedżera pakietów NuGet. Aby uzyskać szczegółowe informacje, zobacz [ponowne instalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md).

Na koniec zachowanie narzędzia NuGet jest zależne od `Nuget.Config` plików. Wiele plików może służyć do scentralizowania niektórych ustawień na różnych poziomach, jak wyjaśniono w temacie [Konfigurowanie zachowania NuGet](../consume-packages/configuring-nuget-behavior.md).

## <a name="ways-to-install-a-nuget-package"></a>Sposoby instalacji pakietu NuGet

Pakiety NuGet są pobierane i instalowane przy użyciu dowolnej metody z poniższej tabeli.

| Narzędzie | Opis |
| --- | --- |
| [ INTERFEJS WIERSZA POLECENIAdotnet.exe](install-use-packages-dotnet-cli.md) | (Wszystkie platformy) Narzędzie interfejsu wiersza polecenia dla bibliotek .NET Core i .NET Standard oraz dla projektów w stylu zestawu SDK, które są przeznaczone dla .NET Framework (zobacz [atrybut zestawu SDK](/dotnet/core/tools/csproj#additions)). Pobiera pakiet identyfikowany przez \<package_name\> i dodaje odwołanie do pliku projektu. Program również pobiera i instaluje zależności. |
| Visual Studio | (Systemy Windows i Mac) Udostępnia interfejs użytkownika, za pomocą którego można przeglądać, wybierać i instalować pakiety oraz ich zależności w projekcie z określonego źródła pakietu. Dodaje odwołania do zainstalowanych pakietów do pliku projektu.<ul><li>[Instalowanie pakietów i zarządzanie nimi za pomocą programu Visual Studio](install-use-packages-visual-studio.md)</li><li>[Dołączanie pakietu NuGet w projekcie (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| [Konsola menedżera pakietów (Visual Studio)](install-use-packages-powershell.md) | (Tylko system Windows) Pobiera i instaluje pakiet identyfikowany przez \<package_name\> z wybranego źródła w określonym projekcie w rozwiązaniu, a następnie dodaje odwołanie do pliku projektu. Program również pobiera i instaluje zależności. |
| [Interfejs wiersza polecenia nuget.exe](install-use-packages-nuget-cli.md) | (Wszystkie platformy) Narzędzie interfejsu wiersza polecenia dla bibliotek .NET Framework i projektów spoza zestawu SDK, które są przeznaczone dla .NET Standard bibliotek. Pobiera pakiet identyfikowany przez program \<package_name\> i rozszerza jego zawartość do folderu w bieżącym katalogu. można również pobrać wszystkie pakiety wymienione w `packages.config` pliku. Program również pobiera i instaluje zależności, ale nie wprowadza zmian w plikach projektu ani `packages.config` . |
