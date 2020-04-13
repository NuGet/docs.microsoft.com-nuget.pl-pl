---
ms.openlocfilehash: 5197447531288a8b071354dbeb3a3ae02f7cce09
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610533"
---
#### <a name="windows"></a>Windows

> [!Note]
> NuGet.exe 5.0 i nowsze wymagają .NET Framework 4.7.2 lub nowsze do wykonania.

1. Odwiedź [nuget.org/downloads](https://nuget.org/downloads) i wybierz NuGet 3.3 lub nowszą (2.8.6 nie jest kompatybilny z Mono). Najnowsza wersja jest zawsze zalecana, a 4.1.0+ jest wymagane do publikowania pakietów, aby nuget.org.
1. Każde pobranie `nuget.exe` jest plikiem bezpośrednio. Poinstruuj przeglądarkę, aby zapisać plik w wybranym folderze. Plik *nie* jest instalatorem; nie zobaczysz niczego, jeśli uruchomisz go bezpośrednio z przeglądarki.
1. Dodaj folder, w `nuget.exe` którym został umieszczony do zmiennej środowiskowej PATH, aby używać narzędzia cli z dowolnego miejsca.

#### <a name="macoslinux"></a>system macOS/Linux

Zachowania mogą się nieznacznie różnić w zależności od rozkładu systemu operacyjnego.

1. Zainstaluj [Mono 4.4.2 lub nowsze](https://www.mono-project.com/docs/getting-started/install/).

1. Wykonaj następujące polecenie w wierszu powłoki:

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. Utwórz alias, dodając następujący skrypt do odpowiedniego pliku dla `~/.bash_aliases` `~/.bash_profile`systemu operacyjnego (zazwyczaj lub):

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. Przeładuj powłokę.  Przetestuj instalację, `nuget` wprowadzając bez parametrów. Pomoc NuGet CLI powinna być wyświetlana.
