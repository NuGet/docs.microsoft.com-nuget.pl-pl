---
ms.openlocfilehash: 5197447531288a8b071354dbeb3a3ae02f7cce09
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610533"
---
#### <a name="windows"></a><span data-ttu-id="e5176-101">Windows</span><span class="sxs-lookup"><span data-stu-id="e5176-101">Windows</span></span>

> [!Note]
> <span data-ttu-id="e5176-102">NuGet.exe 5.0 i nowsze wymagają .NET Framework 4.7.2 lub nowsze do wykonania.</span><span class="sxs-lookup"><span data-stu-id="e5176-102">NuGet.exe 5.0 and later require .NET Framework 4.7.2 or later to execute.</span></span>

1. <span data-ttu-id="e5176-103">Odwiedź [nuget.org/downloads](https://nuget.org/downloads) i wybierz NuGet 3.3 lub nowszą (2.8.6 nie jest kompatybilny z Mono).</span><span class="sxs-lookup"><span data-stu-id="e5176-103">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="e5176-104">Najnowsza wersja jest zawsze zalecana, a 4.1.0+ jest wymagane do publikowania pakietów, aby nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e5176-104">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
1. <span data-ttu-id="e5176-105">Każde pobranie `nuget.exe` jest plikiem bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="e5176-105">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="e5176-106">Poinstruuj przeglądarkę, aby zapisać plik w wybranym folderze.</span><span class="sxs-lookup"><span data-stu-id="e5176-106">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="e5176-107">Plik *nie* jest instalatorem; nie zobaczysz niczego, jeśli uruchomisz go bezpośrednio z przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="e5176-107">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
1. <span data-ttu-id="e5176-108">Dodaj folder, w `nuget.exe` którym został umieszczony do zmiennej środowiskowej PATH, aby używać narzędzia cli z dowolnego miejsca.</span><span class="sxs-lookup"><span data-stu-id="e5176-108">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="e5176-109">system macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="e5176-109">macOS/Linux</span></span>

<span data-ttu-id="e5176-110">Zachowania mogą się nieznacznie różnić w zależności od rozkładu systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="e5176-110">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="e5176-111">Zainstaluj [Mono 4.4.2 lub nowsze](https://www.mono-project.com/docs/getting-started/install/).</span><span class="sxs-lookup"><span data-stu-id="e5176-111">Install [Mono 4.4.2 or later](https://www.mono-project.com/docs/getting-started/install/).</span></span>

1. <span data-ttu-id="e5176-112">Wykonaj następujące polecenie w wierszu powłoki:</span><span class="sxs-lookup"><span data-stu-id="e5176-112">Execute the following command at a shell prompt:</span></span>

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. <span data-ttu-id="e5176-113">Utwórz alias, dodając następujący skrypt do odpowiedniego pliku dla `~/.bash_aliases` `~/.bash_profile`systemu operacyjnego (zazwyczaj lub):</span><span class="sxs-lookup"><span data-stu-id="e5176-113">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. <span data-ttu-id="e5176-114">Przeładuj powłokę.</span><span class="sxs-lookup"><span data-stu-id="e5176-114">Reload the shell.</span></span>  <span data-ttu-id="e5176-115">Przetestuj instalację, `nuget` wprowadzając bez parametrów.</span><span class="sxs-lookup"><span data-stu-id="e5176-115">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="e5176-116">Pomoc NuGet CLI powinna być wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="e5176-116">NuGet CLI help should display.</span></span>
