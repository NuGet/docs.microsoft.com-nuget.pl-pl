---
title: Dokumentacja interfejsu wiersza polecenia (CLI) NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d777c424-0cf3-4bc0-8abd-7ca16c22192b
description: Indeks wiersza polecenia dla nuget.exe interfejsu wiersza polecenia
keywords: "Indeks odwołań nuget.exe, interfejsu wiersza polecenia nuget.exe, nuget.exe interfejsu wiersza polecenia, polecenia nuget"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3d1c3585d8bbf4c9bd9b50c8167e860594a42055
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-cli-reference"></a>Odwołanie do interfejsu wiersza polecenia NuGet

NuGet interfejsu wiersza polecenia (CLI), `nuget.exe`, zapewnia pełny zakres funkcji NuGet, aby zainstalować, tworzenie, publikowanie i zarządzanie pakietami bez wprowadzania żadnych zmian w plikach projektu.

Aby użyć dowolnego polecenia, Otwórz okno poleceń lub powłoki bash, a następnie uruchom `nuget` następuje polecenia i odpowiednie opcje, takie jak `nuget help pack` (Aby wyświetlić Pomoc dla polecenia pakietu).

## <a name="installing-nugetexe"></a>Instalowanie nuget.exe

[!INCLUDE[install-cli](../includes/install-cli.md)]

## <a name="availability"></a>Dostępność

- Wszystkie polecenia są dostępne w systemie Windows.
- Wszystkie polecenia pracy z [nuget.exe systemem Mono](../guides/install-nuget.md#mac-osx-and-linux) z wyjątkiem określić `pack`, `restore`, i `update`.
- `pack`, `restore`, `delete`, `locals`, I `push` polecenia są również dostępne na Mac i Linux za pomocą [dotnet interfejsu wiersza polecenia](dotnet-Commands.md). 

## <a name="commands-and-applicability"></a>Polecenia i zastosowania

Dostępne polecenia i zastosowanie do tworzenia pakietu, użycie pakietu i/lub publikowania pakietu na hoście:

| Typowe polecenia | Odpowiednich ról | Wersja narzędzia NuGet | Opis | 
| --- | --- | --- | --- |
| [pakiet](cli-ref-pack.md) | Tworzenie | 2.7+ | Tworzy pakiet NuGet z `.nuspec` lub pliku projektu. Podczas uruchamiania na Mono, tworzenie pakietu z pliku projektu nie jest obsługiwane. |
| [wypychania](cli-ref-push.md) | Publikowanie | Wszystkie | Publikuje pakiet do źródła pakietu. |
| [konfiguracji](cli-ref-config.md) | Wszystkie | Wszystkie | Pobiera lub ustawia wartości konfiguracji NuGet. |
| [Pomoc lub?](cli-ref-help.md) | Wszystkie | Wszystkie | Wyświetla Pomoc informacje i pomoc dla polecenia. |
| [Zmienne lokalne](cli-ref-locals.md) | Zużycie | 3.3+ | Usuwa listy pakietów w różnych pamięci podręcznych lub w folderze pakietów globalnych lub identyfikuje te foldery. |
| [Przywracanie](cli-ref-restore.md) | Zużycie | 2.7+ | Przywraca wszystkie pakiety odwołuje się format odwołania pakietu w użyciu. W przypadku uruchamiania na Mono, przywracanie pakietów przy użyciu formatu PackageReference nie jest obsługiwana. | 
| [setapikey](cli-ref-setapikey.md) | Publikowanie i zużycia | Wszystkie | Zapisuje klucz interfejsu API dla danego pakietu źródła, kiedy źródła pakietu wymaga klucza dostępu. |
| [Specyfikacja](cli-ref-spec.md) | Tworzenie | Wszystkie | Generuje `.nuspec` plików przy użyciu tokenów, jeżeli generuje plik z projektu programu Visual Studio. |


| Dodatkowej poleceń | Odpowiednich ról | Wersja narzędzia NuGet | Opis | 
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | Publikowanie | 3.3+ | Dodaje pakiet ze źródłem pakietu innego niż HTTP za pomocą układu hierarchicznej. Dla źródeł protokołu HTTP, użyj *wypychania*. |
| [Usuń](cli-ref-delete.md) | Publikowanie | Wszystkie | Usuwa lub unlists pakietu ze źródła pakietu. |
| [init](cli-ref-init.md) | Tworzenie | 3.3+ | Dodaje pakiety z folderu do źródła pakietu w układzie hierarchicznej. |
| [Zainstaluj](cli-ref-install.md) | Zużycie | Wszystkie | Instaluje a pakietu do bieżącego projektu, ale nie modyfikować projektów lub plików. |
| [Lista](cli-ref-list.md) | Użycie prawdopodobnie publikowania | Wszystkie | Przedstawia pakiety z danego źródła. |
| [dublowany](cli-ref-mirror.md) | Publikowanie | Przestarzałe w wersji 3.2 + | Odzwierciedla pakiet i jego zależności ze źródła do repozytorium docelowej. |
| [źródeł](cli-ref-sources.md) | Zużycie, publikowania | Wszystkie | Zarządza źródła pakietów w plikach konfiguracji. |
| [Aktualizacja](cli-ref-update.md) | Zużycie | Wszystkie | Pakiety projektu aktualizacji do najnowszej wersji. Nie jest obsługiwane podczas uruchamiania na Mono. |

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
