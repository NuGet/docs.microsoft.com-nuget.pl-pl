#### <a name="windows"></a><span data-ttu-id="fce1c-101">Windows</span><span class="sxs-lookup"><span data-stu-id="fce1c-101">Windows</span></span>

1. <span data-ttu-id="fce1c-102">Odwiedź stronę [nuget.org/downloads](https://nuget.org/downloads) i wybierz polecenie NuGet 3.3 albo nowszej (2.8.6 nie jest zgodny z platformy Mono).</span><span class="sxs-lookup"><span data-stu-id="fce1c-102">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="fce1c-103">Najnowszą wersję zawsze jest zalecana i 4.1.0+ jest wymagana do publikowania pakietów nuget.org.</span><span class="sxs-lookup"><span data-stu-id="fce1c-103">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
1. <span data-ttu-id="fce1c-104">Każda wersja jest `nuget.exe` pliku bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="fce1c-104">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="fce1c-105">Poinstruuj przeglądarkę, aby zapisać plik w wybranym folderze.</span><span class="sxs-lookup"><span data-stu-id="fce1c-105">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="fce1c-106">Plik jest *nie* wiadomość Instalatora; nie znajdziesz już niczego po uruchomieniu bezpośrednio z przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="fce1c-106">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
1. <span data-ttu-id="fce1c-107">Dodaj folder, w którym została umieszczona `nuget.exe` do zmiennej środowiskowej PATH, aby użyć narzędzia interfejsu wiersza polecenia z dowolnego miejsca.</span><span class="sxs-lookup"><span data-stu-id="fce1c-107">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="fce1c-108">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="fce1c-108">macOS/Linux</span></span>

<span data-ttu-id="fce1c-109">Zachowania mogą się nieco różnić przez funkcję dystrybucji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="fce1c-109">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="fce1c-110">Zainstaluj [Mono 4.4.2 lub nowszej](http://www.mono-project.com/docs/getting-started/install/).</span><span class="sxs-lookup"><span data-stu-id="fce1c-110">Install [Mono 4.4.2 or later](http://www.mono-project.com/docs/getting-started/install/).</span></span>

1. <span data-ttu-id="fce1c-111">Wykonaj następujące polecenie w wierszu polecenia powłoki:</span><span class="sxs-lookup"><span data-stu-id="fce1c-111">Execute the following command at a shell prompt:</span></span>

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. <span data-ttu-id="fce1c-112">Tworzenie aliasu, dodając poniższy skrypt do pliku odpowiednią dla Twojego systemu operacyjnego (zazwyczaj `~/.bash_aliases` lub `~/.bash_profile`):</span><span class="sxs-lookup"><span data-stu-id="fce1c-112">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. <span data-ttu-id="fce1c-113">Załaduj ponownie powłoki.</span><span class="sxs-lookup"><span data-stu-id="fce1c-113">Reload the shell.</span></span>  <span data-ttu-id="fce1c-114">Przetestuj instalację, wprowadzając `nuget` bez parametrów.</span><span class="sxs-lookup"><span data-stu-id="fce1c-114">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="fce1c-115">Interfejs wiersza polecenia NuGet pomocy powinna być wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="fce1c-115">NuGet CLI help should display.</span></span>
