---
ms.openlocfilehash: 5197447531288a8b071354dbeb3a3ae02f7cce09
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610533"
---
#### <a name="windows"></a>Windows

> [!Note]
> Pakiet NuGet. exe 5,0 i nowsze wymagają .NET Framework 4.7.2 lub nowszego do wykonania.

1. Odwiedź stronę [NuGet.org/downloads](https://nuget.org/downloads) i wybierz opcję NuGet 3,3 lub nowszą (2.8.6 nie jest zgodna z programem mono). Najnowsza wersja jest zawsze zalecana, a 4.1.0 + jest wymagana do publikowania pakietów w nuget.org.
1. Każdy plik jest pobierany bezpośrednio `nuget.exe`. Poinstruuj przeglądarkę, aby zapisywał plik w wybranym folderze. Ten plik *nie* jest instalatorem; nie zobaczysz niczego, jeśli uruchomisz go bezpośrednio z przeglądarki.
1. Dodaj folder, w którym zostały umieszczone `nuget.exe` do zmiennej środowiskowej PATH, aby użyć narzędzia interfejsu wiersza polecenia z dowolnego miejsca.

#### <a name="macoslinux"></a>macOS/Linux

Zachowania mogą się nieco różnić w zależności od dystrybucji systemu operacyjnego.

1. Zainstaluj [mono lub nowszy](https://www.mono-project.com/docs/getting-started/install/).

1. Wykonaj następujące polecenie w wierszu polecenia powłoki:

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. Utwórz alias, dodając następujący skrypt do odpowiedniego pliku dla systemu operacyjnego (zwykle `~/.bash_aliases` lub `~/.bash_profile`):

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. Załaduj ponownie powłokę.  Przetestuj instalację, wprowadzając `nuget` bez parametrów. Pomoc interfejsu wiersza polecenia NuGet powinna zostać wyświetlona.
