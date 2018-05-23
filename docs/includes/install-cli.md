#### <a name="windows"></a>Windows

1. Odwiedź stronę [nuget.org/downloads](https://nuget.org/downloads) i wybierz NuGet 3.3 lub nowszej (2.8.6 nie jest zgodny z Mono). Zaleca się zawsze najnowszą wersję, a 4.1.0+ jest wymagana do publikowania pakietów nuget.org.
1. Każda wersja jest `nuget.exe` pliku bezpośrednio. Poinstruuj przeglądarkę, aby zapisać plik w folderze wybranych przez użytkownika. Plik jest *nie* usługi Instalatora; nie znajdziesz już niczego po uruchomieniu bezpośrednio z przeglądarki.
1. Dodaj folder, w którym została umieszczona `nuget.exe` Twojego zmiennej środowiskowej ŚCIEŻKA korzystać z narzędzia interfejsu wiersza polecenia z dowolnego miejsca.

#### <a name="macoslinux"></a>macOS/Linux

Zachowania mogą się nieco różnić przy dystrybucji systemu operacyjnego.

1. Zainstaluj [Mono 4.4.2 lub nowszym](http://www.mono-project.com/docs/getting-started/install/).

1. Uruchom następujące polecenie w wierszu polecenia powłoki:

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. Utwórz alias, dodając następujący skrypt do odpowiedniego pliku dla Twojego systemu operacyjnego (zazwyczaj `~/.bash_aliases` lub `~/.bash_profile`):

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. Załaduj ponownie powłoki.  Testowanie instalacji wprowadzając `nuget` bez parametrów. Interfejs wiersza polecenia NuGet pomocy powinien być wyświetlany.
