---
ms.openlocfilehash: 1f65939493cf423a76c024607264acee6c7e9050
ms.sourcegitcommit: ef08f376688f0191a8d3d873b6a4386afd799373
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/28/2019
ms.locfileid: "66271594"
---
#### <a name="windows"></a><span data-ttu-id="15677-101">Windows</span><span class="sxs-lookup"><span data-stu-id="15677-101">Windows</span></span>

> [!Note]
> <span data-ttu-id="15677-102">NuGet.exe 5.0 lub nowszy wymaga .NET Framework 4.7.2 lub nowszej, aby wykonać.</span><span class="sxs-lookup"><span data-stu-id="15677-102">NuGet.exe 5.0 and later require .NET Framework 4.7.2 or later to execute.</span></span>

1. <span data-ttu-id="15677-103">Odwiedź stronę [nuget.org/downloads](https://nuget.org/downloads) i wybierz polecenie NuGet 3.3 albo nowszej (2.8.6 nie jest zgodny z platformy Mono).</span><span class="sxs-lookup"><span data-stu-id="15677-103">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="15677-104">Najnowszą wersję zawsze jest zalecana i 4.1.0+ jest wymagana do publikowania pakietów nuget.org.</span><span class="sxs-lookup"><span data-stu-id="15677-104">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
1. <span data-ttu-id="15677-105">Każda wersja jest `nuget.exe` pliku bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="15677-105">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="15677-106">Poinstruuj przeglądarkę, aby zapisać plik w wybranym folderze.</span><span class="sxs-lookup"><span data-stu-id="15677-106">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="15677-107">Plik jest *nie* wiadomość Instalatora; nie znajdziesz już niczego po uruchomieniu bezpośrednio z przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="15677-107">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
1. <span data-ttu-id="15677-108">Dodaj folder, w którym została umieszczona `nuget.exe` do zmiennej środowiskowej PATH, aby użyć narzędzia interfejsu wiersza polecenia z dowolnego miejsca.</span><span class="sxs-lookup"><span data-stu-id="15677-108">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="15677-109">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="15677-109">macOS/Linux</span></span>

<span data-ttu-id="15677-110">Zachowania mogą się nieco różnić przez funkcję dystrybucji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="15677-110">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="15677-111">Zainstaluj [Mono 4.4.2 lub nowszej](http://www.mono-project.com/docs/getting-started/install/).</span><span class="sxs-lookup"><span data-stu-id="15677-111">Install [Mono 4.4.2 or later](http://www.mono-project.com/docs/getting-started/install/).</span></span>

1. <span data-ttu-id="15677-112">Wykonaj następujące polecenie w wierszu polecenia powłoki:</span><span class="sxs-lookup"><span data-stu-id="15677-112">Execute the following command at a shell prompt:</span></span>

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. <span data-ttu-id="15677-113">Tworzenie aliasu, dodając poniższy skrypt do pliku odpowiednią dla Twojego systemu operacyjnego (zazwyczaj `~/.bash_aliases` lub `~/.bash_profile`):</span><span class="sxs-lookup"><span data-stu-id="15677-113">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. <span data-ttu-id="15677-114">Załaduj ponownie powłoki.</span><span class="sxs-lookup"><span data-stu-id="15677-114">Reload the shell.</span></span>  <span data-ttu-id="15677-115">Przetestuj instalację, wprowadzając `nuget` bez parametrów.</span><span class="sxs-lookup"><span data-stu-id="15677-115">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="15677-116">Interfejs wiersza polecenia NuGet pomocy powinna być wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="15677-116">NuGet CLI help should display.</span></span>
