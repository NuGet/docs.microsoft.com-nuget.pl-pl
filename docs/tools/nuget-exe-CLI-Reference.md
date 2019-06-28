---
title: Dokumentacja interfejsu wiersza polecenia (CLI) NuGet
description: Indeks wiersza polecenia nuget.exe interfejsu wiersza polecenia
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: a257dbbd9d56b5989e050ed4096d096cd1036184
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426023"
---
# <a name="nuget-cli-reference"></a>Dokumentacja interfejsu wiersza polecenia NuGet

NuGet interfejsu wiersza polecenia (CLI), `nuget.exe`, oferuje pełny zakres funkcji NuGet do zainstalowania, tworzenie, publikowanie i zarządzanie pakietami bez wprowadzania żadnych zmian w plikach projektu.

Aby użyć dowolnego polecenia, Otwórz okno polecenia lub powłokę bash, a następnie uruchom `nuget` następuje poleceń i odpowiednie opcje, takie jak `nuget help pack` (Aby wyświetlić Pomoc dotyczącą polecenia dodatkiem Service pack).

Ta dokumentacja zawiera najnowszą wersję interfejsu wiersza polecenia NuGet. Aby uzyskać szczegółowymi informacjami na temat dla danej wersji, którego używasz, uruchom `nuget help` dla żądanego polecenia.

Aby dowiedzieć się, jak użyć podstawowa poleceń z `nuget.exe` interfejsu wiersza polecenia, zobacz [Instalowanie i używanie pakietów przy użyciu interfejsu wiersza polecenia nuget.exe](../consume-packages/install-use-packages-nuget-cli.md).

## <a name="installing-nugetexe"></a>Instalowanie nuget.exe

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> Aby udostępnić interfejs wiersza polecenia NuGet w konsoli Menedżera pakietów w programie Visual Studio, zobacz [przy użyciu nuget.exe interfejsu wiersza polecenia w konsoli](package-manager-console.md#using-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Dostępność

Zobacz [dostępność funkcji](../install-nuget-client-tools.md#feature-availability) dla szczegółowymi informacjami na temat.

- Wszystkie polecenia są dostępne w Windows.
- Wszystkie polecenia pracować nuget.exe systemem platformy Mono, z wyjątkiem sytuacji, gdy należy określić `pack`, `restore`, i `update`.
- `pack`, `restore`, `delete`, `locals`, I `push` polecenia są również dostępne na komputerach Mac i Linux za pomocą interfejsu wiersza polecenia platformy dotnet.

## <a name="commands-and-applicability"></a>Polecenia i możliwości zastosowania

Dostępne polecenia i ma zastosowanie do tworzenia pakietów, użycie pakietu i/lub opublikować pakiet do hosta:

| Typowe polecenia | Odpowiednich ról | NuGet w wersji | Opis |
| --- | --- | --- | --- |
| [pakiet](cli-ref-pack.md) | Tworzenie | 2.7+ | Tworzy pakiet NuGet z `.nuspec` lub pliku projektu. Podczas uruchamiania na platformy Mono, tworzenie pakietu z pliku projektu nie jest obsługiwana. |
| [push](cli-ref-push.md) | Publikowanie | Wszystkie | Publikuje pakiet do źródła pakietu. |
| [config](cli-ref-config.md) | Wszystkie | Wszystkie | Pobiera lub ustawia wartości konfiguracji NuGet. |
| [help or ?](cli-ref-help.md) | Wszystkie | Wszystkie | Wyświetla Pomoc informacje lub pomoc dla polecenia. |
| [locals](cli-ref-locals.md) | Zużycie | 3.3+ | Wyświetla lokalizacje *globalnymi pakietami*, *pamięci podręcznej http*, i *temp* foldery i czyści zawartość tych folderów. |
| [restore](cli-ref-restore.md) | Zużycie | 2.7+ | Przywraca wszystkie pakiety, które odwołuje się formatu używanego pakietu zarządzania. Podczas uruchamiania na platformy Mono, przywracanie pakietów przy użyciu formatu PackageReference nie jest obsługiwana. |
| [setapikey](cli-ref-setapikey.md) | Publikowanie i użycia | Wszystkie | Zapisuje klucz interfejsu API dla danego pakietu źródła, podczas tego źródła pakietów wymaga klucza dostępu. |
| [spec](cli-ref-spec.md) | Tworzenie | Wszystkie | Generuje `.nuspec` plików, przy użyciu tokenów, jeśli generuje plik z projektu programu Visual Studio. |

| Dodatkowych poleceń | Odpowiednich ról | NuGet w wersji | Opis |
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | Publikowanie | 3.3+ | Dodaje pakiet do źródła pakietu protokołu HTTP przy użyciu układzie hierarchicznym. W przypadku źródła HTTP, użyj *wypychania*. |
| [delete](cli-ref-delete.md) | Publikowanie | Wszystkie | Usuwa lub unlists pakietu ze źródła pakietu. |
| [init](cli-ref-init.md) | Tworzenie | 3.3+ | Dodaje pakiety z folderu do źródła pakietu przy użyciu układzie hierarchicznym. |
| [install](cli-ref-install.md) | Zużycie | Wszystkie | Instaluje pakiet do bieżącego projektu, ale nie modyfikować projekty lub odwoływać się do plików. |
| [list](cli-ref-list.md) | Zużycie, może być publikowania | Wszystkie | Wyświetla pakiety z danego źródła. |
| [mirror](cli-ref-mirror.md) | Publikowanie | Przestarzałe w 3.2 + | Odzwierciedla pakietu oraz jego zależności ze źródła do repozytorium docelowego. |
| [sources](cli-ref-sources.md) | Zużycie, publikowanie | Wszystkie | Zarządza źródłami pakietów w plikach konfiguracji. |
| [update](cli-ref-update.md) | Zużycie | Wszystkie | Aktualizacje pakietów projektu do najnowszej dostępnej wersji. Nieobsługiwane w przypadku uruchomienia w Mono. |

Różne polecenia należy używać różnych [zmienne środowiskowe](cli-ref-environment-variables.md).

Polecenia interfejsu wiersza polecenia NuGet w odpowiednich ról:

| Rola | Polecenia |
| --- | --- |
| Zużycie | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| Tworzenie | `config`, `help`, `init`, `pack`, `spec` |
| Publikowanie | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Deweloperów zainteresowanych tylko w przypadku używania pakietów, na przykład, należy tylko informacje o tego podzbioru polecenia NuGet.

> [!Note]
> Nazwy opcji polecenia jest rozróżniana wielkość liter. Opcje, które zostały zaniechane nie są uwzględnione w to odwołanie, takich jak `NoPrompt` (zastępuje `NonInteractive`) i `Verbose` (zastępuje `Verbosity`).
