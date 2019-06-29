---
title: Rozwiązywanie problemów z przywracania pakietów NuGet w programie Visual Studio
description: Opis typowych NuGet przywrócić błędów w Visual Studio oraz ze sposobem rozwiązać ten problem.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: 3be8d1dad6552db2fc04b2f324145ac7ce86acb2
ms.sourcegitcommit: b9a134a6e10d7d8502613f389f7d5f9b9e206ec8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467772"
---
# <a name="troubleshooting-package-restore-errors"></a>Rozwiązywanie problemów z błędami Przywracanie pakietu

Ten artykuł koncentruje się na typowych błędów podczas przywracania pakietów i kroki, aby je rozwiązać. Aby uzyskać szczegółowe informacje dotyczące przywracania pakietów, zobacz [Przywracanie pakietu](../consume-packages/package-restore.md#enable-and-disable-package-restore).

Jeśli podanych tutaj instrukcji nie działają, [Zgłoś problem w serwisie GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) tak, aby firma Microsoft bardziej dokładnie sprawdź danego scenariusza. Nie używaj "czy ta strona jest pomocna?" Kontrolka, która może pojawić się na tej stronie, ponieważ jej nie umożliwiają nam się z Tobą, aby uzyskać więcej informacji.

## <a name="quick-solution-for-visual-studio-users"></a>Szybkie rozwiązanie dla użytkowników programu Visual Studio

Jeśli używasz programu Visual Studio, najpierw włączyć przywracania pakietów w następujący sposób. W przeciwnym razie przejdź do kolejnych sekcjach.

1. Wybierz **Narzędzia > Menedżer pakietów NuGet > Ustawienia Menedżera pakietów** polecenia menu.
1. Ustaw obie opcje, w obszarze **Przywracanie pakietów**.
1. Kliknij przycisk **OK**.
1. Ponownie skompiluj projekt.

![Włączanie przywracania pakietów NuGet w narzędzia/Opcje](../consume-packages/media/restore-01-autorestoreoptions.png)

Te ustawienia można zmienić w swojej `NuGet.config` pliku; zobacz [zgody](#consent) sekcji.

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>Ten projekt przywołuje pakiety NuGet, których brakuje na tym komputerze

Komunikat o błędzie ukończone:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

Ten błąd występuje podczas próby skompilowania projektu, który zawiera odwołania do co najmniej jednego pakietu NuGet, ale te pakiety nie są obecnie zainstalowane na komputerze lub w projekcie.

- Korzystając z formatu zarządzania PackageReference, ten błąd oznacza, że pakiet nie jest zainstalowana w *globalnymi pakietami* folderu zgodnie z opisem na [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](managing-the-global-packages-and-cache-folders.md).
- Korzystając z `packages.config`, ten błąd oznacza, że pakiet nie jest zainstalowany w `packages` folder w katalogu głównym rozwiązania.

Ta sytuacja występuje często, gdy uzyskać kod źródłowy projektu z kontroli źródła lub innego pobierania. Pakiety zazwyczaj zostały pominięte w kontroli źródła lub pliki do pobrania, ponieważ pliki mogą zostać przywrócone z pakietu pakietami, takie jak nuget.org (zobacz [pakiety i kontrola źródła](Packages-and-Source-Control.md)). Uwzględniając je w przeciwnym razie będzie wybrzuszanie repozytorium lub utworzyć pliki zip niepotrzebnie.

Ten błąd może też być plik projektu zawiera ścieżki bezwzględnej do lokalizacji pakietu, a następnie przenieść projektu.

Do przywrócenia pakietów, użyj jednej z następujących metod:

- Jeśli po przeniesieniu pliku projektu, należy edytować plik bezpośrednio, aby zaktualizować odwołania do pakietu.
- W programie Visual Studio, należy włączyć Przywracanie pakietu, wybierając **Narzędzia > Menedżer pakietów NuGet > Ustawienia Menedżera pakietów** polecenia menu, ustawianie obu opcji w obszarze **Przywracanie pakietów**i wybierając polecenie  **OK**. Następnie ponownie skompiluj rozwiązanie.
- Dla projektów .NET Core, uruchom `dotnet restore` lub `dotnet build` (który automatycznie uruchamia przywracania).
- W wierszu polecenia Uruchom `nuget restore` (z wyjątkiem projekty utworzone za pomocą `dotnet`, w którym to przypadku użycia `dotnet restore`).
- W wierszu polecenia z projektami przy użyciu formatu PackageReference Uruchom `msbuild -t:restore`.

Po pomyślnie przeprowadzić przywrócenie, muszą znajdować się w pakiecie *globalnymi pakietami* folderu. W przypadku projektów przy użyciu funkcji PackageReference przywracania należy ponownie utworzyć `obj/project.assets.json` pliku; dla projektów przy użyciu `packages.config`, pakiet powinien pojawić się w projekcie `packages` folderu. Projekt teraz powinien być kompilowany pomyślnie. W przeciwnym razie [pliku wystąpił problem w serwisie GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) , dzięki czemu możemy wykonać kolejne czynności z Tobą.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Zasoby plików nie można odnaleźć project.assets.json

Komunikat o błędzie ukończone:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

`project.assets.json` Pliku przechowuje wykres zależności projektu, gdy w formacie PackageReference zarządzania, który jest używany, aby upewnić się, że wszystkie niezbędne pakiety są instalowane na komputerze. Ponieważ ten plik jest generowany dynamicznie za pośrednictwem Przywracanie pakietu, nie został zazwyczaj dodany do kontroli źródła. W wyniku ten błąd występuje podczas kompilowania projektu za pomocą narzędzia, takie jak `msbuild` , nie automatycznie przywraca pakietów.

W takim przypadku uruchom `msbuild -t:restore` następuje `msbuild`, lub użyj `dotnet build` (przywraca pakietów automatycznie). Można również użyć dowolnej z metod przywracania pakietów w [poprzedniej sekcji](#missing).

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>Co najmniej jednego pakietu NuGet, muszą zostać przywrócone, ale nie może być, ponieważ nie udzielono zgody

Komunikat o błędzie ukończone:

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

Ten błąd oznacza, że Przywracanie pakietu jest wyłączone w konfiguracji NuGet.

Można zmienić ustawienia mające zastosowanie w programie Visual Studio, zgodnie z wcześniejszym opisem w obszarze [szybkie rozwiązanie dla użytkowników programu Visual Studio](#quick-solution-for-visual-studio-users).

Można również edytować te ustawienia bezpośrednio w odpowiednią `nuget.config` pliku (zazwyczaj `%AppData%\NuGet\NuGet.Config` na Windows i `~/.nuget/NuGet/NuGet.Config` w systemie Mac/Linux). Upewnij się, że `enabled` i `automatic` klucze w ramach `packageRestore` są ustawione na wartość True:

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
> Jeśli edytujesz `packageRestore` ustawienia bezpośrednio w `nuget.config`, uruchom ponownie program Visual Studio, okno dialogowe Opcje Pokazuje bieżące wartości.

## <a name="other-potential-conditions"></a>Inne warunki potencjalnych

- Komunikat informujący o tym, pobierz je za pomocą Przywracanie pakietów NuGet, mogą wystąpić błędy kompilacji z powodu brakujących plików. Jednak Uruchamianie przywracania może powiedzieć "wszystkie pakiety są już zainstalowane i nie ma nic do przywrócenia". W takim przypadku usuń `packages` folder (przy użyciu `packages.config`) lub `obj/project.assets.json` pliku (w przypadku używania funkcji PackageReference) i uruchom ponownie przywracania. Jeśli ten błąd będzie nadal występował, należy użyć `nuget locals all -clear` lub `dotnet locals all --clear` z poziomu wiersza polecenia, aby wyczyścić *globalnymi pakietami* i foldery pamięci podręcznej, zgodnie z opisem na [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](managing-the-global-packages-and-cache-folders.md).

- Podczas uzyskiwania projektu z kontroli źródła, folderów projektu może być ustawiona na tylko do odczytu. Zmień uprawnienia do folderu i spróbuj ponownie przywracania pakietów.

- Używasz starszej wersji pakietu nuget. Sprawdź [nuget.org/downloads](https://www.nuget.org/downloads) najnowsze zalecanych wersji. Dla programu Visual Studio 2015 firma Microsoft zaleca 3.6.0.

Jeśli wystąpią problemy z innymi [pliku wystąpił problem w serwisie GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) Aby uzyskać więcej szczegółowych informacji ze strony użytkownika.
