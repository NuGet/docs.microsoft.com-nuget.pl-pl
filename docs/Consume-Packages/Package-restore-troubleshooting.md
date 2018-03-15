---
title: "Rozwiązywanie problemów z pakietu NuGet przywracania w programie Visual Studio | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Opis wspólnej NuGet Przywracanie błędy w Visual Studio i sposoby ich rozwiązywania."
keywords: "Przywracanie pakietu NuGet, przywracanie pakietów, rozwiązywania problemów, rozwiązywanie problemów"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8efaed497a596921af3c73ab919831c73bf598e0
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/15/2018
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

Ten błąd występuje przystąpieniem do tworzenia projektu, który zawiera odwołania do co najmniej jednego pakietu NuGet, ale pakiety nie są obecnie buforowane w projekcie. (Pakiety są buforowane w `packages` folder w katalogu głównym rozwiązanie, jeśli projekt używa `packages.config`, lub `obj/project.assets.json` plik, jeśli projekt używa formatu PackageReference.)

Taka sytuacja często występuje, gdy uzyskać kod źródłowy projektu z kontroli źródła lub innego pobierania. Pakiety są zwykle pominięto z kontroli źródła lub pliki do pobrania, ponieważ pliki mogą zostać przywrócone z pakietu źródeł danych, takich jak nuget.org (zobacz [pakietów i kontroli źródła](Packages-and-Source-Control.md)). Włączenie ich w przeciwnym razie będzie wybrzuszanie repozytorium lub Utwórz plików zip niepotrzebnie.

Użyj jednej z następujących metod w celu przywrócenia pakietów:

- W programie Visual Studio, Włącz Przywracanie pakietu po wybraniu **Narzędzia > Menedżera pakietów NuGet > Ustawienia Menedżera pakietów** polecenia menu, ustawianie obu opcji w obszarze **przywracania pakietów**i wybierając  **OK**. Następnie ponownie skompiluj rozwiązanie.
- Projekty platformy .NET Core, uruchom `dotnet restore` lub `dotnet build` (automatycznie uruchamia przywracania).
- W wierszu polecenia Uruchom `nuget restore` (z wyjątkiem projektów utworzonych za pomocą `dotnet`, w którym to przypadku użycia `dotnet restore`).
- W wierszu polecenia z projektami przy użyciu formatu PackageReference Uruchom `msbuild /t:restore`.

Po pomyślnym przywracania, powinna zostać wyświetlona albo `packages` folder (przy użyciu `packages.config`) lub `obj/project.assets.json` plików (w przypadku używania PackageReference). Projekt powinien teraz kompilacji pomyślnie. Jeśli nie, [pliku problemu w serwisie GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) , firma Microsoft możesz skomunikować się z Tobą.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Nie można odnaleźć project.assets.json pliku zasobów

Pełny komunikat:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

Ten błąd występuje z powodów zgodnie z objaśnieniem w [poprzedniej sekcji](#missing), i ma takie same środki zaradcze. Na przykład uruchomiona `msbuild` na .NET Core projektu został uzyskany z kontroli źródła nie będzie automatycznie przywrócić pakiety. W takim przypadku uruchom `msbuild /t:restore` następuje `msbuild`, lub użyj `dotnet build` (co spowoduje przywrócenie pakietów automatycznie).

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

Należy pamiętać, że po zmodyfikowaniu `packageRestore` ustawienia bezpośrednio w `nuget.config`, uruchom ponownie program Visual Studio, opcje — Okno dialogowe zawiera bieżące wartości.

## <a name="other-potential-conditions"></a>Inne potencjalne warunki

- Mogą wystąpić błędy kompilacji z powodu braku plików z komunikat z informacją, użyj polecenia NuGet restore, aby je pobrać. Jednak Uruchamianie przywracania może powiedzieć "wszystkie pakiety są już zainstalowane i nie ma niczego do przywrócenia." W takim przypadku usuń `packages` folder (przy użyciu `packages.config`) lub `obj/project.assets.json` plików (w przypadku używania PackageReference) i uruchom ponownie przywracania.

- Podczas uzyskiwania projektu z kontroli źródła, folderów projektu może być równa tylko do odczytu. Zmień uprawnienia do folderu i spróbuj ponownie przywrócić pakiety.

- Korzystasz z starsza wersja programu NuGet. Sprawdź [nuget.org/downloads](https://www.nuget.org/downloads) najnowsze zalecane wersji. Dla programu Visual Studio 2015 zaleca się 3.6.0.

Jeśli występują inne problemy [pliku problemu w serwisie GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) , możemy więcej informacji można uzyskać od użytkownika.