---
title: Rozwiązywanie problemów z przywracaniem pakietów NuGet w Visual Studio
description: Opis typowych błędów przywracania nuGet w Visual Studio i sposoby ich rozwiązywania.
author: JonDouglas
ms.author: jodou
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: 0bd14104695a15d2e4c65a13b271143809c4ba8a
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323625"
---
# <a name="troubleshooting-package-restore-errors"></a>Rozwiązywanie problemów z błędami przywracania pakietów

Ten artykuł koncentruje się na typowych błędach podczas przywracania pakietów i krokach ich rozwiązywania. 

Przywracanie pakietu próbuje zainstalować wszystkie zależności pakietu do prawidłowego stanu zgodnego z odwołaniami do pakietu w pliku projektu *(csproj)* lub w *packages.config* pliku. (W Visual Studio odwołania są wyświetlane w Eksplorator rozwiązań w obszarze **Zależności \ NuGet** lub w **węźle Odwołania).** Aby wykonać kroki wymagane do przywrócenia pakietów, zobacz [Przywracanie pakietów](../consume-packages/package-restore.md#restore-packages). Jeśli odwołania do pakietu w pliku projektu *(csproj)* lub w pliku *packages.config* są nieprawidłowe (nie są zgodne z żądanym stanem po przywróceniu pakietu), należy zainstalować lub zaktualizować pakiety zamiast korzystać z funkcji przywracania pakietów.

Jeśli instrukcje w tym miejscu nie działają, prosimy o slicie problemu w usłudze [GitHub,](https://github.com/NuGet/docs.microsoft.com-nuget/issues) abyśmy dokładniej zbadali Twój scenariusz. Nie używaj strony "Czy ta strona jest pomocna?" możesz kontrolować, która może pojawić się na tej stronie, ponieważ nie daje nam możliwości skontaktowania się z Tobą w celu uzyskać więcej informacji.

## <a name="quick-solution-for-visual-studio-users"></a>Szybkie rozwiązanie dla Visual Studio użytkowników

Jeśli używasz usługi Visual Studio najpierw włącz przywracanie pakietu w następujący sposób. W przeciwnym razie przejdź do kolejnych sekcji.

1. Wybierz polecenie **menu Narzędzia > NuGet Menedżer pakietów > Menedżer pakietów Ustawienia.**
1. Ustaw obie opcje w obszarze **Przywracanie pakietu.**
1. Wybierz przycisk **OK**.
1. Skompilowanie projektu ponownie.

![Włączanie przywracania pakietów NuGet w narzędziu/opcjach](../consume-packages/media/restore-01-autorestoreoptions.png)

Te ustawienia można również zmienić w `NuGet.Config` pliku. Zobacz [sekcję wyrażania](#consent) zgody. Jeśli projekt jest starszym projektem, który używa przywracania pakietów zintegrowanych z programem MSBuild, może być konieczne przeprowadzenie [migracji](package-restore.md#migrate-to-automatic-package-restore-visual-studio) do automatycznego przywracania pakietu.

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>Ten projekt odwołuje się do pakietów NuGet, których brakuje na tym komputerze

Pełny komunikat o błędzie:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

Ten błąd występuje podczas próby skompilowania projektu zawierającego odwołania do co najmniej jednego pakietu NuGet, ale te pakiety nie są obecnie zainstalowane na komputerze ani w projekcie.

- W przypadku korzystania z formatu [zarządzania PackageReference](package-references-in-project-files.md) ten błąd może być pozostawiony po migracji [](/nuget/resources/nuget-faq#working-with-packages) z packages.config do packageReference i musi zostać ręcznie usunięty z pliku projektu.
- W przypadku [packages.config](../reference/packages-config.md)błąd oznacza, że pakiet nie jest zainstalowany w `packages` folderze w katalogu głównym rozwiązania.

Taka sytuacja często występuje, gdy uzyskujesz kod źródłowy projektu z kontroli źródła lub innego pliku do pobrania. Pakiety są zwykle pomijane podczas kontroli źródła lub pobierania, ponieważ można je przywrócić ze źródeł danych pakietów, takich jak nuget.org (zobacz [Pakiety i kontrola źródła).](Packages-and-Source-Control.md) W przeciwnym razie ich uwzględnienie wywłaszczyłoby repozytorium lub niepotrzebnie duże pliki .zip plików.

Ten błąd może również wystąpić, jeśli plik projektu zawiera ścieżki bezwzględne do lokalizacji pakietu i przeniesiesz projekt.

Aby przywrócić pakiety, użyj jednej z następujących metod:

- Jeśli plik projektu został przeniesiony, edytuj go bezpośrednio, aby zaktualizować odwołania do pakietu.
- [Visual Studio](package-restore.md#restore-using-visual-studio) [(przywracanie automatyczne lub](package-restore.md#restore-packages-automatically-using-visual-studio) przywracanie [ręczne)](package-restore.md#restore-packages-manually-using-visual-studio)
- [Interfejs wiersza polecenia dotnet](package-restore.md#restore-using-the-dotnet-cli)
- [Interfejs wiersza polecenia nuget.exe](package-restore.md#restore-using-the-nugetexe-cli)
- [MSBuild](package-restore.md#restore-using-msbuild)
- [Azure Pipelines](package-restore.md#restore-using-azure-pipelines)
- [Azure DevOps Server](package-restore.md#restore-using-azure-devops-server)

Po pomyślnym przywróceniu pakiet powinien być obecny w *folderze global-packages.* W przypadku projektów korzystających z funkcji PackageReference przywracanie powinno ponownie utworzyć plik. W przypadku projektów korzystających z funkcji pakiet powinien pojawić się w `obj/project.assets.json` `packages.config` `packages` folderze projektu. Projekt powinien teraz zostać pomyślnie skompilowany. Jeśli tak nie [jest, w usłudze GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) należy utworzyć plik problemu, abyśmy z To użytkownikiem nas obserwowali.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Plik zasobów project.assets.jsnie znaleziono

Pełny komunikat o błędzie:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

Plik zachowuje wykres zależności projektu w przypadku korzystania z formatu zarządzania PackageReference, który służy do upewnienia się, że wszystkie niezbędne pakiety są `project.assets.json` zainstalowane na komputerze. Ponieważ ten plik jest generowany dynamicznie za pomocą przywracania pakietu, zazwyczaj nie jest dodawany do kontroli źródła. W związku z tym ten błąd występuje podczas budowania projektu za pomocą narzędzia takiego jak , które `msbuild` nie przywraca automatycznie pakietów.

W takim przypadku uruchom , `msbuild -t:restore` a następnie , lub użyj funkcji `msbuild` `dotnet build` (co spowoduje automatyczne przywrócenie pakietów). Możesz również użyć dowolnej metody przywracania pakietów z [poprzedniej sekcji](#missing).

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>Co najmniej jeden pakiet NuGet musi zostać przywrócony, ale nie można go przywrócić, ponieważ nie udzielono zgody

Pełny komunikat o błędzie:

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

Ten błąd wskazuje, że przywracanie pakietu jest wyłączone w konfiguracji nuGet.

Odpowiednie ustawienia można zmienić w programie Visual Studio jak opisano wcześniej w obszarze Szybkie [rozwiązanie dla Visual Studio użytkowników.](#quick-solution-for-visual-studio-users)

Te ustawienia można również edytować bezpośrednio w odpowiednich plikach (zazwyczaj w systemie `nuget.config` `%AppData%\NuGet\NuGet.Config` Windows i na `~/.nuget/NuGet/NuGet.Config` komputerach Mac/Linux). Upewnij się, `enabled` że klucze i w obszarze są ustawione na wartość `automatic` `packageRestore` True:

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
> Jeśli edytujesz ustawienia bezpośrednio w programie , uruchom Visual Studio, aby w oknie dialogowym opcji `packageRestore` `nuget.config` wyświetlane są bieżące wartości.

## <a name="other-potential-conditions"></a>Inne potencjalne warunki

- Mogą wystąpić błędy kompilacji z powodu braku plików z komunikatem o użyciu przywracania NuGet w celu ich pobrania. Jednak uruchomienie przywracania może powiedzieć "Wszystkie pakiety są już zainstalowane i nie ma nic do przywrócenia". W takim przypadku usuń folder (w przypadku używania funkcji ) lub pliku (w przypadku korzystania z `packages` `packages.config` `obj/project.assets.json` packageReference) i uruchom przywracanie ponownie. Jeśli błąd będzie nadal występował, użyj polecenia lub z wiersza polecenia, aby wyczyścić globalne pakiety i foldery pamięci podręcznej zgodnie z opisem w tece Zarządzanie globalnymi pakietami i folderami `nuget locals all -clear` `dotnet nuget locals all --clear` pamięci [podręcznej](managing-the-global-packages-and-cache-folders.md). 

- Podczas uzyskiwania projektu z kontroli źródła foldery projektu mogą być ustawione na tylko do odczytu. Zmień uprawnienia folderu i spróbuj ponownie przywrócić pakiety.

- Być może używasz starej wersji pakietu NuGet. Sprawdź [nuget.org/downloads](https://www.nuget.org/downloads) najnowsze zalecane wersje. W Visual Studio 2015 r. zalecamy korzystanie z 3.6.0.

Jeśli napotkasz inne problemy, [zamów problem w usłudze GitHub,](https://github.com/NuGet/docs.microsoft.com-nuget/issues) aby uzyskać więcej szczegółów od Ciebie.
