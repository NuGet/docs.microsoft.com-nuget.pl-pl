#### <a name="windows"></a>Windows

1. Odwiedź stronę [nuget.org/downloads](https://nuget.org/downloads) i wybierz polecenie NuGet 3.3 albo nowszej (2.8.6 nie jest zgodny z platformy Mono). Najnowszą wersję zawsze jest zalecana i 4.1.0+ jest wymagana do publikowania pakietów nuget.org.
1. Każda wersja jest `nuget.exe` pliku bezpośrednio. Poinstruuj przeglądarkę, aby zapisać plik w wybranym folderze. Plik jest *nie* wiadomość Instalatora; nie znajdziesz już niczego po uruchomieniu bezpośrednio z przeglądarki.
1. Dodaj folder, w którym została umieszczona `nuget.exe` do zmiennej środowiskowej PATH, aby użyć narzędzia interfejsu wiersza polecenia z dowolnego miejsca.

#### <a name="macoslinux"></a>macOS/Linux

Zachowania mogą się nieco różnić przez funkcję dystrybucji systemu operacyjnego.

1. Zainstaluj [Mono 4.4.2 lub nowszej](http://www.mono-project.com/docs/getting-started/install/).

1. Wykonaj następujące polecenie w wierszu polecenia powłoki:

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. Tworzenie aliasu, dodając poniższy skrypt do pliku odpowiednią dla Twojego systemu operacyjnego (zazwyczaj `~/.bash_aliases` lub `~/.bash_profile`):

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. Załaduj ponownie powłoki.  Przetestuj instalację, wprowadzając `nuget` bez parametrów. Interfejs wiersza polecenia NuGet pomocy powinna być wyświetlana.
