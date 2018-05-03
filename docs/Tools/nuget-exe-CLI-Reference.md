---
title: Odwołanie do NuGet interfejsu wiersza polecenia (CLI)
description: Indeks wiersza polecenia dla nuget.exe interfejsu wiersza polecenia
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: ed91a31505ab1de9447cdbeb87c8ad08f7ba56d8
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-cli-reference"></a>Odwołanie do interfejsu wiersza polecenia NuGet

NuGet interfejsu wiersza polecenia (CLI), `nuget.exe`, zapewnia pełny zakres funkcji NuGet, aby zainstalować, tworzenie, publikowanie i zarządzanie pakietami bez wprowadzania żadnych zmian w plikach projektu.

Aby użyć dowolnego polecenia, Otwórz okno poleceń lub powłoki bash, a następnie uruchom `nuget` następuje polecenia i odpowiednie opcje, takie jak `nuget help pack` (Aby wyświetlić Pomoc dla polecenia pakietu).

Ta dokumentacja odzwierciedla najnowszą wersję interfejsu wiersza polecenia NuGet. Uzyskać dokładne szczegółów dla danej wersji, którego używasz, uruchom `nuget help` dla żądanego polecenia.

## <a name="installing-nugetexe"></a>Instalowanie nuget.exe

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> Aby udostępnić interfejsu wiersza polecenia NuGet w konsoli Menedżera pakietów w programie Visual Studio, zobacz [przy użyciu nuget.exe interfejsu wiersza polecenia w konsoli](package-manager-console.md#using-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Dostępność

Zobacz [dostępność funkcji](../install-nuget-client-tools.md#feature-availability) dokładne szczegółowe informacje.

- Wszystkie polecenia są dostępne w systemie Windows.
- Wszystkie polecenia pracy z systemem Mono oprócz wskazanych dla nuget.exe `pack`, `restore`, i `update`.
- `pack`, `restore`, `delete`, `locals`, I `push` polecenia są również dostępne na Mac i Linux za pomocą dotnet interfejsu wiersza polecenia.

## <a name="commands-and-applicability"></a>Polecenia i zastosowania

Dostępne polecenia i zastosowanie do tworzenia pakietu, użycie pakietu i/lub publikowania pakietu na hoście:

| Typowe polecenia | Odpowiednich ról | Wersja narzędzia NuGet | Opis |
| --- | --- | --- | --- |
| [pakiet](cli-ref-pack.md) | Tworzenie | 2.7+ | Tworzy pakiet NuGet z `.nuspec` lub pliku projektu. Podczas uruchamiania na Mono, tworzenie pakietu z pliku projektu nie jest obsługiwane. |
| [push](cli-ref-push.md) | Publikowanie | Wszystkie | Publikuje pakiet do źródła pakietu. |
| [config](cli-ref-config.md) | Wszystkie | Wszystkie | Pobiera lub ustawia wartości konfiguracji NuGet. |
| [help lub ?](cli-ref-help.md) | Wszystkie | Wszystkie | Wyświetla Pomoc informacje i pomoc dla polecenia. |
| [locals](cli-ref-locals.md) | Zużycie | 3.3+ | Wyświetla lokalizacje *globalne pakiety*, *pamięci podręcznej http*, i *temp* folderów i czyści zawartość tych folderów. |
| [restore](cli-ref-restore.md) | Zużycie | 2.7+ | Przywraca wszystkie pakiety odwołuje się formatu używanego pakietu zarządzania. W przypadku uruchamiania na Mono, przywracanie pakietów przy użyciu formatu PackageReference nie jest obsługiwana. |
| [setapikey](cli-ref-setapikey.md) | Publikowanie i zużycia | Wszystkie | Zapisuje klucz interfejsu API dla danego pakietu źródła, kiedy źródła pakietu wymaga klucza dostępu. |
| [spec](cli-ref-spec.md) | Tworzenie | Wszystkie | Generuje `.nuspec` plików przy użyciu tokenów, jeżeli generuje plik z projektu programu Visual Studio. |

| Dodatkowej poleceń | Odpowiednich ról | Wersja narzędzia NuGet | Opis |
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | Publikowanie | 3.3+ | Dodaje pakiet ze źródłem pakietu innego niż HTTP za pomocą układu hierarchicznej. Dla źródeł protokołu HTTP, użyj *wypychania*. |
| [delete](cli-ref-delete.md) | Publikowanie | Wszystkie | Usuwa lub unlists pakietu ze źródła pakietu. |
| [init](cli-ref-init.md) | Tworzenie | 3.3+ | Dodaje pakiety z folderu do źródła pakietu w układzie hierarchicznej. |
| [install](cli-ref-install.md) | Zużycie | Wszystkie | Instaluje a pakietu do bieżącego projektu, ale nie modyfikować projektów lub plików. |
| [list](cli-ref-list.md) | Użycie prawdopodobnie publikowania | Wszystkie | Przedstawia pakiety z danego źródła. |
| [mirror](cli-ref-mirror.md) | Publikowanie | Przestarzałe w wersji 3.2 + | Odzwierciedla pakiet i jego zależności ze źródła do repozytorium docelowej. |
| [sources](cli-ref-sources.md) | Zużycie, publikowania | Wszystkie | Zarządza źródła pakietów w plikach konfiguracji. |
| [update](cli-ref-update.md) | Zużycie | Wszystkie | Pakiety projektu aktualizacji do najnowszej wersji. Nie jest obsługiwane podczas uruchamiania na Mono. |

Inne polecenia należy używać różnych [zmiennych środowiskowych](cli-ref-environment-variables.md).

Polecenia interfejsu wiersza polecenia NuGet w odpowiednich ról:

| Rola | Polecenia |
| --- | --- |
| Zużycie | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| Tworzenie | `config`, `help`, `init`, `pack`, `spec` |
| Publikowanie | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Deweloperzy związane tylko z korzystanie z pakietów, tylko konieczne na przykład zrozumienie tego podzbioru polecenia NuGet.

> [!Note]
> Nazwy opcji polecenia jest rozróżniana wielkość liter. Opcje, które zostały uznane za przestarzałe nie znajdują się w niniejszej dokumentacji, takich jak `NoPrompt` (zastępuje `NonInteractive`) i `Verbose` (zastępuje `Verbosity`).
