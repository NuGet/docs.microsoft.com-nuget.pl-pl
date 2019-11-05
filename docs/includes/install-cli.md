---
ms.openlocfilehash: 5197447531288a8b071354dbeb3a3ae02f7cce09
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610533"
---
#### <a name="windows"></a><span data-ttu-id="36490-101">Windows</span><span class="sxs-lookup"><span data-stu-id="36490-101">Windows</span></span>

> [!Note]
> <span data-ttu-id="36490-102">Pakiet NuGet. exe 5,0 i nowsze wymagają .NET Framework 4.7.2 lub nowszego do wykonania.</span><span class="sxs-lookup"><span data-stu-id="36490-102">NuGet.exe 5.0 and later require .NET Framework 4.7.2 or later to execute.</span></span>

1. <span data-ttu-id="36490-103">Odwiedź stronę [NuGet.org/downloads](https://nuget.org/downloads) i wybierz opcję NuGet 3,3 lub nowszą (2.8.6 nie jest zgodna z programem mono).</span><span class="sxs-lookup"><span data-stu-id="36490-103">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="36490-104">Najnowsza wersja jest zawsze zalecana, a 4.1.0 + jest wymagana do publikowania pakietów w nuget.org.</span><span class="sxs-lookup"><span data-stu-id="36490-104">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
1. <span data-ttu-id="36490-105">Każdy plik jest pobierany bezpośrednio `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="36490-105">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="36490-106">Poinstruuj przeglądarkę, aby zapisywał plik w wybranym folderze.</span><span class="sxs-lookup"><span data-stu-id="36490-106">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="36490-107">Ten plik *nie* jest instalatorem; nie zobaczysz niczego, jeśli uruchomisz go bezpośrednio z przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="36490-107">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
1. <span data-ttu-id="36490-108">Dodaj folder, w którym zostały umieszczone `nuget.exe` do zmiennej środowiskowej PATH, aby użyć narzędzia interfejsu wiersza polecenia z dowolnego miejsca.</span><span class="sxs-lookup"><span data-stu-id="36490-108">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="36490-109">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="36490-109">macOS/Linux</span></span>

<span data-ttu-id="36490-110">Zachowania mogą się nieco różnić w zależności od dystrybucji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="36490-110">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="36490-111">Zainstaluj [mono lub nowszy](https://www.mono-project.com/docs/getting-started/install/).</span><span class="sxs-lookup"><span data-stu-id="36490-111">Install [Mono 4.4.2 or later](https://www.mono-project.com/docs/getting-started/install/).</span></span>

1. <span data-ttu-id="36490-112">Wykonaj następujące polecenie w wierszu polecenia powłoki:</span><span class="sxs-lookup"><span data-stu-id="36490-112">Execute the following command at a shell prompt:</span></span>

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. <span data-ttu-id="36490-113">Utwórz alias, dodając następujący skrypt do odpowiedniego pliku dla systemu operacyjnego (zwykle `~/.bash_aliases` lub `~/.bash_profile`):</span><span class="sxs-lookup"><span data-stu-id="36490-113">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. <span data-ttu-id="36490-114">Załaduj ponownie powłokę.</span><span class="sxs-lookup"><span data-stu-id="36490-114">Reload the shell.</span></span>  <span data-ttu-id="36490-115">Przetestuj instalację, wprowadzając `nuget` bez parametrów.</span><span class="sxs-lookup"><span data-stu-id="36490-115">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="36490-116">Pomoc interfejsu wiersza polecenia NuGet powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="36490-116">NuGet CLI help should display.</span></span>
