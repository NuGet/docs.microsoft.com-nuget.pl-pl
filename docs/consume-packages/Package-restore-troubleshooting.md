---
title: Rozwiązywanie problemów z przywracaniem pakietów NuGet w programie Visual Studio
description: Opis typowych błędów przywracania NuGet w programie Visual Studio i sposoby ich rozwiązywania.
author: JonDouglas
ms.author: jodou
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: f1c7c4ce2872e18b1ed35ccbf3355a6192ab4a9c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775027"
---
# <a name="troubleshooting-package-restore-errors"></a>Rozwiązywanie problemów z błędami przywracania pakietu

Ten artykuł koncentruje się na typowych błędach podczas przywracania pakietów i kroków w celu ich rozwiązania. 

Przywracanie pakietu próbuje zainstalować wszystkie zależności pakietów do poprawnego stanu pasującego do odwołania do pakietu w pliku projektu (*. csproj*) lub pliku *packages.config* . (W programie Visual Studio odwołania pojawiają się w Eksplorator rozwiązań w obszarze **zależności \ NuGet** lub węzeł **odwołania** ). Aby wykonać kroki wymagane do przywrócenia pakietów, zobacz [przywracanie pakietów](../consume-packages/package-restore.md#restore-packages). Jeśli odwołania do pakietu w pliku projektu (*. csproj*) lub pliku *packages.config* są niepoprawne (nie są zgodne z żądanym stanem po przywróceniu pakietu), należy zainstalować lub zaktualizować pakiety zamiast korzystać z przywracania pakietu.

Jeśli instrukcje tego nie zadziałały, należy [rozwiązać problem w usłudze GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) , aby dokładniej przeanalizować scenariusz. Nie używaj "czy ta strona jest pomocna?" kontrolka, która może pojawić się na tej stronie, ponieważ nie daje nam możliwości skontaktowania się z Tobą w celu uzyskania dodatkowych informacji.

## <a name="quick-solution-for-visual-studio-users"></a>Szybkie rozwiązanie dla użytkowników programu Visual Studio

Jeśli używasz programu Visual Studio, najpierw włącz przywracanie pakietu w następujący sposób. W przeciwnym razie przejdź do kolejnych sekcji.

1. Wybierz polecenie **narzędzia > Menedżer pakietów NuGet > menu Ustawienia Menedżera pakietów** .
1. Ustaw obie opcje w obszarze **przywracanie pakietu**.
1. Wybierz przycisk **OK**.
1. Ponownie skompiluj projekt.

![Włącz przywracanie pakietu NuGet w narzędziu/opcjach](../consume-packages/media/restore-01-autorestoreoptions.png)

Te ustawienia można także zmienić w `NuGet.config` pliku; zapoznaj się z sekcją [zgody](#consent) . Jeśli projekt jest starszym projektem, który używa przywracania pakietu programu MSBuild, może być konieczne przeprowadzenie [migracji](package-restore.md#migrate-to-automatic-package-restore-visual-studio) do automatycznego przywracania pakietów.

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>Ten projekt odwołuje się do pakietów NuGet, których brakuje na tym komputerze

Pełny komunikat o błędzie:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

Ten błąd występuje podczas próby skompilowania projektu, który zawiera odwołania do co najmniej jednego pakietu NuGet, ale te pakiety nie są obecnie zainstalowane na komputerze ani w projekcie.

- W przypadku korzystania z formatu [PackageReference](package-references-in-project-files.md) Management ten błąd może być pozostały z packages.config do PackageReference migracji i musi zostać [ręcznie usunięty](../resources/NuGet-FAQ.md#working-with-packages) z pliku projektu.
- W przypadku korzystania z [packages.config](../reference/packages-config.md)błąd oznacza, że pakiet nie jest zainstalowany w `packages` folderze w katalogu głównym rozwiązania.

Ta sytuacja często występuje, gdy uzyskujesz kod źródłowy projektu z kontroli źródła lub innego pobierania. Pakiety są zwykle pomijane na podstawie kontroli źródła lub pobierania, ponieważ można je przywrócić ze źródeł danych pakietu, takich jak nuget.org (zobacz [pakiety i kontrola źródła](Packages-and-Source-Control.md)). Dołączenie ich w inny sposób przeładowanie repozytorium lub tworzenie niepotrzebnych dużych plików. zip.

Ten błąd może również wystąpić, jeśli plik projektu zawiera bezwzględne ścieżki do lokalizacji pakietów i przeniesiesz projekt.

Aby przywrócić pakiety, użyj jednej z następujących metod:

- Jeśli plik projektu został przeniesiony, edytuj go bezpośrednio, aby zaktualizować odwołania do pakietu.
- [Visual Studio](package-restore.md#restore-using-visual-studio) ([automatyczne przywracanie](package-restore.md#restore-packages-automatically-using-visual-studio) lub [przywracanie ręczne](package-restore.md#restore-packages-manually-using-visual-studio))
- [Interfejs wiersza polecenia dotnet](package-restore.md#restore-using-the-dotnet-cli)
- [Interfejs wiersza polecenia nuget.exe](package-restore.md#restore-using-the-nugetexe-cli)
- [MSBuild](package-restore.md#restore-using-msbuild)
- [Azure Pipelines](package-restore.md#restore-using-azure-pipelines)
- [Azure DevOps Server](package-restore.md#restore-using-azure-devops-server)

Po pomyślnym przywróceniu pakiet powinien znajdować się w folderze *Global-Packages* . W przypadku projektów korzystających z programu PackageReference przywracanie powinno odtworzyć `obj/project.assets.json` plik. w przypadku projektów używających `packages.config` pakiet powinien pojawić się w `packages` folderze projektu. Projekt powinien teraz zostać pomyślnie skompilowany. Jeśli nie, Zastąp [problem w usłudze GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) , dzięki czemu będziemy mogli z nich skorzystać.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Nie znaleziono pliku zasobów project.assets.js

Pełny komunikat o błędzie:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

`project.assets.json`Plik utrzymuje wykres zależności projektu przy użyciu formatu zarządzania PackageReference, który jest używany do upewnienia się, że wszystkie wymagane pakiety są zainstalowane na komputerze. Ponieważ ten plik jest generowany dynamicznie przez Przywracanie pakietów, zazwyczaj nie jest dodawany do kontroli źródła. W związku z tym ten błąd występuje podczas kompilowania projektu za pomocą narzędzia, takiego jak `msbuild` nie przywraca automatycznie pakietów.

W takim przypadku należy uruchomić `msbuild -t:restore` `msbuild` polecenie, a następnie użyć `dotnet build` (które automatycznie przywraca pakiety). Można również użyć dowolnej z metod przywracania pakietów w [poprzedniej sekcji](#missing).

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>Należy przywrócić co najmniej jeden pakiet NuGet, ale nie można go z powodu braku zgody

Pełny komunikat o błędzie:

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

Ten błąd wskazuje, że przywracanie pakietu jest wyłączone w konfiguracji programu NuGet.

Można zmienić odpowiednie ustawienia w programie Visual Studio zgodnie z wcześniejszym opisem w sekcji [szybkie rozwiązanie dla użytkowników programu Visual Studio](#quick-solution-for-visual-studio-users).

Te ustawienia można również edytować bezpośrednio w odpowiednim `nuget.config` pliku (zazwyczaj `%AppData%\NuGet\NuGet.Config` w systemach Windows i `~/.nuget/NuGet/NuGet.Config` Mac/Linux). Upewnij się, `enabled` że `automatic` klucze i w obszarze `packageRestore` są ustawione na wartość true:

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
> Jeśli edytujesz `packageRestore` Ustawienia bezpośrednio w programie `nuget.config` , uruchom ponownie program Visual Studio, aby okno dialogowe Opcje pokazywało bieżące wartości.

## <a name="other-potential-conditions"></a>Inne potencjalne warunki

- Błędy kompilacji mogą wystąpić z powodu braku plików, a komunikat informujący o konieczności użycia przywracania NuGet do pobrania. Jednak uruchomienie przywracania może powiedzieć, "wszystkie pakiety są już zainstalowane i nie ma niczego do przywrócenia". W takim przypadku Usuń `packages` folder (w przypadku używania `packages.config` ) lub `obj/project.assets.json` plik (w przypadku korzystania z programu PackageReference) i ponownie uruchom przywracanie. Jeśli błąd nadal występuje, użyj `nuget locals all -clear` lub `dotnet nuget locals all --clear` z wiersza polecenia, aby wyczyścić foldery *globalne-Packages* i pamięci podręcznej zgodnie z opisem w temacie [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](managing-the-global-packages-and-cache-folders.md).

- Podczas uzyskiwania projektu z kontroli źródła foldery projektu mogą być ustawione na tylko do odczytu. Zmień uprawnienia folderu i spróbuj ponownie przywrócić pakiety.

- Być może używasz starej wersji programu NuGet. Sprawdź [NuGet.org/downloads](https://www.nuget.org/downloads) z najnowszymi zalecanymi wersjami. W przypadku programu Visual Studio 2015 zalecamy 3.6.0.

Jeśli napotkasz inne problemy, zapoznaj [się z problemem w serwisie GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) , aby uzyskać więcej szczegółowych informacji.
