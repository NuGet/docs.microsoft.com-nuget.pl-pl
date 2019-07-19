---
title: Dokumentacja interfejsu wiersza polecenia NuGet (CLI)
description: Indeks odwołania w wierszu polecenia dla interfejsu CLI programu NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: 52aa2c533a8b67ae10455888a34a7ac9767fd0e3
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328244"
---
# <a name="nuget-cli-reference"></a>Dokumentacja interfejsu wiersza polecenia NuGet

Interfejs wiersza polecenia NuGet (CLI) `nuget.exe`, zapewnia pełen zakres funkcji NuGet do instalowania, tworzenia, publikowania i zarządzania pakietami bez wprowadzania żadnych zmian w plikach projektu.

Aby użyć dowolnego polecenia, Otwórz okno polecenia lub powłokę bash, a następnie `nuget` Uruchom polecenie i odpowiednie opcje, takie jak `nuget help pack` (aby wyświetlić pomoc dotyczącą polecenia pakiet).

Ta dokumentacja odzwierciedla najnowszą wersję interfejsu wiersza polecenia NuGet. Aby uzyskać dokładne informacje dotyczące dowolnej używanej wersji, uruchom `nuget help` polecenie dla żądanego polecenia.

Aby dowiedzieć się, jak używać podstawowych poleceń `nuget.exe` za pomocą interfejsu wiersza polecenia, zobacz [Instalowanie i używanie pakietów przy użyciu interfejsu wiersza polecenia NuGet. exe](../consume-packages/install-use-packages-nuget-cli.md).

## <a name="installing-nugetexe"></a>Instalowanie NuGet. exe

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> Aby udostępnić interfejs wiersza polecenia NuGet w konsoli Menedżera pakietów w programie Visual Studio, zobacz [Używanie interfejsu wiersza polecenia NuGet. exe w konsoli programu](../consume-packages/install-use-packages-powershell.md#use-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Dostępność

Szczegółowe informacje można znaleźć w temacie [dostępność funkcji](../install-nuget-client-tools.md#feature-availability) .

- Wszystkie polecenia są dostępne w systemie Windows.
- Wszystkie polecenia pracują z pakietem NuGet. exe działającym na platformie `pack`mono `restore`, z wyjątkiem sytuacji, w których wskazano dla, i `update`.
- `pack`Polecenia, `restore`, ,`delete` isą`push` również dostępne na komputerach Mac i w systemie Linux za pomocą interfejsu wiersza polecenia dotnet `locals`.

## <a name="commands-and-applicability"></a>Polecenia i możliwość zastosowania

Dostępne polecenia i możliwość zastosowania do tworzenia pakietów, użycia pakietów i/lub publikowania pakietu na hoście:

| Typowe polecenia | Odpowiednie role | Wersja programu NuGet | Opis |
| --- | --- | --- | --- |
| [pakiet](cli-reference/cli-ref-pack.md) | Tworzenie | 2.7+ | Tworzy pakiet NuGet z `.nuspec` pliku projektu lub. W przypadku uruchamiania w systemie mono Tworzenie pakietu z pliku projektu nie jest obsługiwane. |
| [push](cli-reference/cli-ref-push.md) | Publikowanie | Wszystkie | Publikuje pakiet w źródle pakietu. |
| [config](cli-reference/cli-ref-config.md) | Wszystkie | Wszystkie | Pobiera lub ustawia wartości konfiguracji NuGet. |
| [help or ?](cli-reference/cli-ref-help.md) | Wszystkie | Wszystkie | Wyświetla informacje pomocy lub pomoc dla polecenia. |
| [locals](cli-reference/cli-ref-locals.md) | Zużycie | 3.3+ | Wyświetla listę lokalizacji *globalnych pakietów*, *pamięci podręcznej protokołu HTTP*i folderów *tymczasowych* i czyści zawartość tych folderów. |
| [restore](cli-reference/cli-ref-restore.md) | Zużycie | 2.7+ | Przywraca wszystkie pakiety, do których odwołuje się używany format zarządzania pakietami. W przypadku uruchamiania w systemie mono przywracanie pakietów przy użyciu formatu PackageReference nie jest obsługiwane. |
| [setapikey](cli-reference/cli-ref-setapikey.md) | Publikowanie, użycie | Wszystkie | Zapisuje klucz interfejsu API dla danego źródła pakietu, gdy źródło tego pakietu wymaga klucza dostępu. |
| [spec](cli-reference/cli-ref-spec.md) | Tworzenie | Wszystkie | `.nuspec` Generuje plik, używając tokenów, jeśli generuje plik z projektu programu Visual Studio. |

| Polecenia pomocnicze | Odpowiednie role | Wersja programu NuGet | Opis |
| --- | --- | --- | --- |
| [add](cli-reference/cli-ref-add.md) | Publikowanie | 3.3+ | Dodaje pakiet do źródła pakietów innego niż HTTP przy użyciu układu hierarchicznego. W przypadku źródeł HTTP Użyj *polecenia push*. |
| [delete](cli-reference/cli-ref-delete.md) | Publikowanie | Wszystkie | Usuwa pakiet ze źródła pakietu. |
| [init](cli-reference/cli-ref-init.md) | Tworzenie | 3.3+ | Dodaje pakiety z folderu do źródła pakietu przy użyciu układu hierarchicznego. |
| [install](cli-reference/cli-ref-install.md) | Zużycie | Wszystkie | Instaluje pakiet w bieżącym projekcie, ale nie modyfikuje projektów ani plików referencyjnych. |
| [list](cli-reference/cli-ref-list.md) | Użycie, prawdopodobnie publikowanie | Wszystkie | Wyświetla pakiety z danego źródła. |
| [mirror](cli-reference/cli-ref-mirror.md) | Publikowanie | Przestarzałe w 3.2 + | Odzwierciedla pakiet i jego zależności ze źródła do repozytorium docelowego. |
| [sources](cli-reference/cli-ref-sources.md) | Użycie, publikowanie | Wszystkie | Zarządza źródłami pakietów w plikach konfiguracji. |
| [update](cli-reference/cli-ref-update.md) | Zużycie | Wszystkie | Aktualizuje pakiety projektu do najnowszej dostępnej wersji. Nieobsługiwane w przypadku uruchamiania na mono. |

Różne polecenia wykorzystują różne [zmienne środowiskowe](cli-reference/cli-ref-environment-variables.md).

Poleceń interfejsu wiersza polecenia NuGet według odpowiednich ról:

| Role | Polecenia |
| --- | --- |
| Zużycie | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| Tworzenie | `config`, `help`, `init`, `pack`, `spec` |
| Publikowanie | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Deweloperzy zainteresowani tylko pakietem pakietów, na przykład potrzebują jedynie zrozumienia podzestawu poleceń NuGet.

> [!Note]
> W nazwach opcji poleceń nie jest rozróżniana wielkość liter. Opcje, które są przestarzałe, nie zostały uwzględnione w tym odwołaniu `NoPrompt` , np. `NonInteractive`(zastąpione przez) `Verbosity`i `Verbose` (zastąpione przez).
