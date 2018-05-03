---
title: Rozwiązywanie problemów z Przywracanie pakietu NuGet w programie Visual Studio
description: Opis wspólnej NuGet Przywracanie błędy w Visual Studio i sposoby ich rozwiązywania.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: c552941c896d1a7136310c0a8bc6755d5974809a
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="troubleshooting-package-restore-errors"></a>Rozwiązywanie problemów z błędami przywracania pakietu

Ten artykuł dotyczy typowe błędy podczas przywracania pakietów i sposobów ich rozwiązywania. Aby uzyskać szczegółowe informacje dotyczące przywracania pakietów, zobacz [Przywracanie pakietu](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

Jeśli poniższe instrukcje nie działają, [Zgłoś problem w usłudze GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) tak, aby firma Microsoft bada danego scenariusza bardziej dokładnie. Nie używaj "warto tę stronę?" formant, który może występować na tej stronie, ponieważ go nie dają nam możliwość się z Tobą, aby uzyskać więcej informacji.

## <a name="quick-solution-for-visual-studio-users"></a>Szybkie rozwiązanie dla użytkowników programu Visual Studio

Jeśli używasz programu Visual Studio, najpierw włączyć Przywracanie pakietu w następujący sposób. W przeciwnym razie nadal w kolejnych sekcjach.

1. Wybierz **Narzędzia > Menedżera pakietów NuGet > Ustawienia Menedżera pakietów** polecenia menu.
1. Ustaw obie opcje w obszarze **przywracania pakietów**.
1. Wybierz **OK**.
1. Skompiluj projekt ponownie.

![Włącz Przywracanie pakietu NuGet w narzędzia/Opcje](../consume-packages/media/restore-01-autorestoreoptions.png)

Te ustawienia można zmienić w Twojej `NuGet.config` pliku; zobacz [zgody](#consent) sekcji.

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>Ten projekt zawiera odwołania do pakietów NuGet Brak na tym komputerze

Pełny komunikat:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

Ten błąd występuje przystąpieniem do tworzenia projektu, który zawiera odwołania do co najmniej jednego pakietu NuGet, ale pakiety nie są obecnie zainstalowane na komputerze lub w projekcie.

- Podczas korzystania z formatu zarządzania PackageReference, błąd oznacza, że pakiet nie jest zainstalowany w *globalne pakiety* folderu zgodnie z opisem na zgodnie z opisem na [Zarządzanie globalne pakietów i pamięci podręcznej folderów](managing-the-global-packages-and-cache-folders.md).
- Korzystając z `packages.config`, ten błąd oznacza, że pakiet nie jest zainstalowany w `packages` folder w katalogu głównym rozwiązania.

Taka sytuacja często występuje, gdy uzyskać kod źródłowy projektu z kontroli źródła lub innego pobierania. Pakiety są zwykle pominięto z kontroli źródła lub pliki do pobrania, ponieważ pliki mogą zostać przywrócone z pakietu źródeł danych, takich jak nuget.org (zobacz [pakietów i kontroli źródła](Packages-and-Source-Control.md)). Włączenie ich w przeciwnym razie będzie wybrzuszanie repozytorium lub Utwórz plików zip niepotrzebnie.

Użyj jednej z następujących metod w celu przywrócenia pakietów:

- W programie Visual Studio, Włącz Przywracanie pakietu po wybraniu **Narzędzia > Menedżera pakietów NuGet > Ustawienia Menedżera pakietów** polecenia menu, ustawianie obu opcji w obszarze **przywracania pakietów**i wybierając  **OK**. Następnie ponownie skompiluj rozwiązanie.
- Projekty platformy .NET Core, uruchom `dotnet restore` lub `dotnet build` (automatycznie uruchamia przywracania).
- W wierszu polecenia Uruchom `nuget restore` (z wyjątkiem projektów utworzonych za pomocą `dotnet`, w którym to przypadku użycia `dotnet restore`).
- W wierszu polecenia z projektami przy użyciu formatu PackageReference Uruchom `msbuild /t:restore`.

Po przywróceniu pomyślnie, powinien znajdować się w pakiecie *globalne pakiety* folderu. W przypadku projektów przy użyciu PackageReference przywracania należy ponownie utworzyć `obj/project.assets.json` pliku; dla projektów przy użyciu `packages.config`, pakiet powinien zostać wyświetlony w projekcie `packages` folderu. Projekt powinien teraz kompilacji pomyślnie. Jeśli nie, [pliku problemu w serwisie GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) , firma Microsoft możesz skomunikować się z Tobą.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Nie można odnaleźć project.assets.json pliku zasobów

Pełny komunikat:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

`project.assets.json` Pliku przechowuje wykresu zależności projektu, gdy w formacie PackageReference zarządzania, który jest używany, aby upewnić się, że wszystkie niezbędne pakiety są zainstalowane na komputerze. Ponieważ ten plik jest generowany dynamicznie za pośrednictwem Przywracanie pakietu, zwykle nie został dodany do kontroli źródła. W związku z tym, że ten błąd występuje podczas kompilowania projektu za pomocą narzędzia, takie jak `msbuild` który nie automatycznie przywrócić pakiety.

W takim przypadku uruchom `msbuild /t:restore` następuje `msbuild`, lub użyj `dotnet build` (co spowoduje przywrócenie pakietów automatycznie). Można również użyć dowolnej z metod przywracania pakietu w [poprzedniej sekcji](#missing).

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>Konieczne jest przywrócenie co najmniej jednego pakietu NuGet, ale nie może być, ponieważ nie udzielono zgody

Pełny komunikat:

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

Ten błąd wskazuje, że to, że Przywracanie pakietu jest wyłączone w konfiguracji programu NuGet.

Można zmienić odpowiednich ustawień w programie Visual Studio, jak opisano wcześniej w [szybkie rozwiązanie dla użytkowników programu Visual Studio](#quick-solution-for-visual-studio-users).

Można również edytować tych ustawień bezpośrednio w odpowiednich `nuget.config` pliku (zazwyczaj `%AppData%\NuGet\NuGet.Config` w systemie Windows i `~/.nuget/NuGet/NuGet.Config` na system Mac/Linux). Upewnij się, że `enabled` i `automatic` kluczy w obszarze `packageRestore` są ustawione na wartość True:

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> Po zmodyfikowaniu `packageRestore` ustawienia bezpośrednio w `nuget.config`, uruchom ponownie program Visual Studio, opcje — Okno dialogowe zawiera bieżące wartości.

## <a name="other-potential-conditions"></a>Inne potencjalne warunki

- Mogą wystąpić błędy kompilacji z powodu braku plików z komunikat z informacją, użyj polecenia NuGet restore, aby je pobrać. Jednak Uruchamianie przywracania może powiedzieć "wszystkie pakiety są już zainstalowane i nie ma niczego do przywrócenia." W takim przypadku usuń `packages` folder (przy użyciu `packages.config`) lub `obj/project.assets.json` plików (w przypadku używania PackageReference) i uruchom ponownie przywracania. Jeśli błąd będzie nadal występować, użyj `nuget locals all -clear` lub `dotnet locals all --clear` z poziomu wiersza polecenia, aby wyczyścić *globalne pakiety* i pamięci podręcznej folderów, zgodnie z opisem na [Zarządzanie globalne pakietów i pamięci podręcznej folderów](managing-the-global-packages-and-cache-folders.md).

- Podczas uzyskiwania projektu z kontroli źródła, folderów projektu może być równa tylko do odczytu. Zmień uprawnienia do folderu i spróbuj ponownie przywrócić pakiety.

- Korzystasz z starsza wersja programu NuGet. Sprawdź [nuget.org/downloads](https://www.nuget.org/downloads) najnowsze zalecane wersji. Dla programu Visual Studio 2015 zaleca się 3.6.0.

Jeśli występują inne problemy [pliku problemu w serwisie GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) , możemy więcej informacji można uzyskać od użytkownika.