Instalowanie pakietu odbywa się na trzy sposoby:

| Metoda | Opis | Tematy pomocy |
| --- | --- | --- |
| nuget.exe interfejsu wiersza polecenia:`nuget install <package_name>` | Pobiera pakiet identyfikowane przez \<nazwa_pakietu\> i rozwija jego zawartość do folderu w bieżącym katalogu. Jeśli nie określono żadnych pakietów, zainstaluje wszystkie pakiety wymienione w projekcie `packages.config` pliku. Nie zmian do plików projektu. Zależności również są pobierane i rozwinięty. | [Odwołanie do interfejsu wiersza polecenia](../tools/nuget-exe-CLI-Reference.md) |
| Konsola Menedżera pakietów (Visual Studio):`Install-Package <package_name>` | Pobiera i instaluje pakiet do bieżącego projektu, a następnie aktualizacji pliku projektu, aby wyświetlić listę pakietu jako zależność. | [Przewodnik konsoli Menedżera pakietów](../tools/Package-Manager-Console.md) |
| Interfejs użytkownika Menedżera pakietów (Visual Studio) | Udostępnia interfejs, za pomocą którego można wybrać, wybierz i zainstaluj pakiety do projektu. Aktualizuje plik projektu, aby wyświetlić listę pakietu jako zależność. | [Informacje o interfejsie użytkownika Menedżera pakietów](../tools/Package-Manager-UI.md) |