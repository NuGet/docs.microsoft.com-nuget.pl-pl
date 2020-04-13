---
title: Rozwiązywanie problemów z przywracaniem pakietu NuGet w programie Visual Studio
description: Opis typowych błędów przywracania NuGet w programie Visual Studio i jak je rozwiązać.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: a1f9f1d03e9a6e58466fa92426bd655d5e8ed83d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "68860623"
---
# <a name="troubleshooting-package-restore-errors"></a>Rozwiązywanie problemów z błędami przywracania pakietu

W tym artykule koncentruje się na typowych błędów podczas przywracania pakietów i kroki, aby je rozwiązać. 

Narzędzie Package Restore próbuje zainstalować wszystkie zależności pakietów do prawidłowego stanu odpowiadającego odwołaniom do pakietu w pliku projektu (*.csproj*) lub pliku *packages.config.* (W programie Visual Studio odwołania są wyświetlane w Eksploratorze rozwiązań w obszarze **zależności \ NuGet** lub węźle **Odwołania).** Aby wykonać wymagane kroki w celu przywrócenia pakietów, zobacz [Przywracanie pakietów](../consume-packages/package-restore.md#restore-packages). Jeśli odwołania do pakietu w pliku projektu *(csproj)* lub pliku *packages.config* są niepoprawne (nie pasują do żądanego stanu po przywróceniu pakietu), należy zainstalować lub zaktualizować pakiety zamiast przywracania pakietu.

Jeśli instrukcje w tym miejscu nie działają dla Ciebie, [zgłoś problem na GitHub,](https://github.com/NuGet/docs.microsoft.com-nuget/issues) abyśmy mogli dokładniej zbadać twój scenariusz. Nie używaj "Czy ta strona jest pomocna?" kontroli, która może pojawić się na tej stronie, ponieważ nie daje nam możliwości skontaktowania się z Tobą w celu uzyskania więcej informacji.

## <a name="quick-solution-for-visual-studio-users"></a>Szybkie rozwiązanie dla użytkowników programu Visual Studio

Jeśli używasz programu Visual Studio, najpierw włącz przywracanie pakietu w następujący sposób. W przeciwnym razie przejdź do sekcji, które następują.

1. Wybierz polecenie menu **Narzędzia > Menedżera pakietów NuGet > Ustawienia Menedżera pakietów.**
1. Ustaw obie opcje w obszarze **Przywracanie pakietu**.
1. Kliknij przycisk **OK**.
1. Zbuduj swój projekt ponownie.

![Włącz przywracanie pakietu NuGet w narzędziu/opcjach](../consume-packages/media/restore-01-autorestoreoptions.png)

Te ustawienia można również `NuGet.config` zmienić w pliku; patrz sekcja [zgody.](#consent) Jeśli projekt jest starszy projekt, który używa msbuild zintegrowane przywracanie pakietu, może być konieczne [migracji](package-restore.md#migrate-to-automatic-package-restore-visual-studio) do automatycznego przywracania pakietu.

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>Ten projekt odwołuje się do pakietów NuGet, których brakuje na tym komputerze

Pełny komunikat o błędzie:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

Ten błąd występuje podczas próby utworzenia projektu, który zawiera odwołania do jednego lub więcej pakietów NuGet, ale te pakiety nie są obecnie zainstalowane na komputerze lub w projekcie.

- Podczas korzystania z formatu zarządzania [PackageReference](package-references-in-project-files.md) błąd oznacza, że pakiet nie jest zainstalowany w folderze *pakietów globalnych,* zgodnie z opisem w [sprawie Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](managing-the-global-packages-and-cache-folders.md).
- Podczas korzystania z [packages.config,](../reference/packages-config.md)błąd oznacza, że `packages` pakiet nie jest zainstalowany w folderze w katalogu głównym rozwiązania.

Ta sytuacja często występuje po uzyskaniu kodu źródłowego projektu z kontroli źródła lub innego pobrania. Pakiety są zazwyczaj pomijane w kontroli źródła lub pobiera, ponieważ można je przywrócić z kanałów pakietowych, takich jak nuget.org (patrz [Pakiety i kontrola źródła).](Packages-and-Source-Control.md) Włączenie ich w przeciwnym razie nadęłoby repozytorium lub stworzyłoby niepotrzebnie duże pliki .zip.

Błąd może również się zdarzyć, jeśli plik projektu zawiera ścieżki bezwzględne do lokalizacji pakietów i przenieść projekt.

Aby przywrócić pakiety, użyj jednej z następujących metod:

- Jeśli plik projektu został przeniesiony, edytuj plik bezpośrednio, aby zaktualizować odwołania do pakietu.
- [Visual Studio](package-restore.md#restore-using-visual-studio) [(automatyczne przywracanie](package-restore.md#restore-packages-automatically-using-visual-studio) lub [ręczne przywracanie)](package-restore.md#restore-packages-manually-using-visual-studio)
- [Interfejs wiersza polecenia dotnet](package-restore.md#restore-using-the-dotnet-cli)
- [Interfejs wiersza polecenia nuget.exe](package-restore.md#restore-using-the-nugetexe-cli)
- [MSBuild](package-restore.md#restore-using-msbuild)
- [Azure Pipelines](package-restore.md#restore-using-azure-pipelines)
- [Azure DevOps Server](package-restore.md#restore-using-azure-devops-server)

Po pomyślnym przywróceniu pakiet powinien znajdować się w folderze *pakietów globalnych.* W przypadku projektów przy użyciu PackageReference `obj/project.assets.json` przywracanie należy ponownie utworzyć plik; w przypadku `packages.config`projektów korzystających z pakietu `packages` powinien pojawić się w folderze projektu. Projekt powinien teraz pomyślnie zbudować. Jeśli nie, [zgłaś problem na GitHub,](https://github.com/NuGet/docs.microsoft.com-nuget/issues) abyśmy mogli z Tobą śledzić.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Nie znaleziono pliku zasobów project.assets.json

Pełny komunikat o błędzie:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

Plik `project.assets.json` przechowuje wykres zależności projektu podczas korzystania z formatu zarządzania PackageReference, który jest używany, aby upewnić się, że wszystkie niezbędne pakiety są zainstalowane na komputerze. Ponieważ ten plik jest generowany dynamicznie za pomocą przywracania pakietu, zazwyczaj nie jest dodawany do kontroli źródła. W rezultacie ten błąd występuje podczas tworzenia projektu `msbuild` za pomocą narzędzia, takiego jak to nie automatycznie przywraca pakiety.

W takim przypadku `msbuild -t:restore` uruchom, a następnie `msbuild`, lub użyj `dotnet build` (który automatycznie przywraca pakiety). Można również użyć dowolnej z metod przywracania pakietu w [poprzedniej sekcji](#missing).

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>Jeden lub więcej pakietów NuGet musi zostać przywrócony, ale nie może być, ponieważ zgoda nie została udzielona

Pełny komunikat o błędzie:

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

Ten błąd wskazuje, że przywracanie pakietu jest wyłączone w konfiguracji NuGet.

Odpowiednie ustawienia w programie Visual Studio można zmienić w sposób opisany wcześniej w obszarze [Szybkie rozwiązanie dla użytkowników programu Visual Studio.](#quick-solution-for-visual-studio-users)

Można również edytować te ustawienia `nuget.config` bezpośrednio w `%AppData%\NuGet\NuGet.Config` odpowiednim pliku `~/.nuget/NuGet/NuGet.Config` (zazwyczaj w systemie Windows i mac/linux). Upewnij `enabled` się, `automatic` że `packageRestore` klawisze i w obszarze są ustawione na True:

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
> Jeśli `packageRestore` ustawienia są edytowane `nuget.config`bezpośrednio w programie , uruchom ponownie program Visual Studio, aby okno dialogowe opcji wyświetlał bieżące wartości.

## <a name="other-potential-conditions"></a>Inne potencjalne warunki

- Mogą wystąpić błędy kompilacji z powodu brakujących plików, z komunikatem informującym o użyciu przywracania NuGet, aby je pobrać. Jednak uruchomienie przywracania może powiedzieć: "Wszystkie pakiety są już zainstalowane i nie ma nic do przywrócenia." W takim przypadku `packages` usuń folder `packages.config`(podczas `obj/project.assets.json` korzystania) lub plik (podczas korzystania z PackageReference) i uruchom przywracanie ponownie. Jeśli błąd nadal występuje, `nuget locals all -clear` `dotnet locals all --clear` użyj lub z wiersza polecenia, aby wyczyścić *globalne pakiety* i foldery pamięci podręcznej, zgodnie z opisem w [temacie Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](managing-the-global-packages-and-cache-folders.md).

- Podczas uzyskiwania projektu z kontroli źródła, foldery projektu mogą być ustawione na tylko do odczytu. Zmień uprawnienia do folderu i spróbuj przywrócić pakiety ponownie.

- Być może używasz starej wersji NuGet. Sprawdź [nuget.org/downloads,](https://www.nuget.org/downloads) czy dostępne są najnowsze zalecane wersje. Dla programu Visual Studio 2015 zaleca się 3.6.0.

Jeśli napotkasz inne problemy, [zgładź problem do GitHub,](https://github.com/NuGet/docs.microsoft.com-nuget/issues) abyśmy mogli uzyskać więcej szczegółów od Ciebie.
