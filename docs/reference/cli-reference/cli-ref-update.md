---
title: Polecenie aktualizacji interfejsu wiersza polecenia nuGet
description: Odwołanie do polecenia nuget.exe update
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 5f244e4cf15ca7afa0e6318a8c20d464ff75bd8e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323651"
---
# <a name="update-command-nuget-cli"></a>Polecenie update (interfejs wiersza polecenia nuGet)

**Dotyczy: zużycie** pakietu &bullet; **Obsługiwane wersje:** wszystkie

Aktualizuje wszystkie pakiety w projekcie (przy użyciu `packages.config` ) do ich najnowszych dostępnych wersji. Zaleca się uruchomienie ["przywracania"](cli-ref-restore.md) przed uruchomieniem . `update` (Aby zaktualizować pojedynczy pakiet, użyj bez określania numeru wersji, w takim przypadku [`nuget install`](cli-ref-install.md) nuGet instaluje najnowszą wersję).

Uwaga: `update` nie działa z interfejsem wiersza polecenia uruchomionym w programie Mono (Mac OSX lub Linux) ani w przypadku korzystania z formatu PackageReference.

Polecenie `update` aktualizuje również odwołania do zestawu w pliku projektu, o ile te odwołania już istnieją. Jeśli zaktualizowany pakiet ma dodany zestaw, nowe odwołanie nie *jest dodawane.* Nowe zależności pakietów również nie mają dodanych odwołań do zestawu. Aby uwzględnić te operacje w ramach aktualizacji, zaktualizuj pakiet w programie Visual Studio użyciu interfejsu Menedżer pakietów użytkownika lub Menedżer pakietów konsoli programu .

To polecenie może również służyć do aktualizowania nuget.exe za pomocą *-self* flag.

## <a name="usage"></a>Użycie

```cli
nuget update <configPath> [options]
```

gdzie `<configPath>` identyfikuje plik rozwiązania lub , który wyświetla listę zależności `packages.config` projektu.

## <a name="options"></a>Opcje

- **`-ConfigFile`**

  Plik konfiguracji NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  Określa wersję pakietów zależności do użycia, która może być jedną z następujących czynności:<br/><ul><li>*Najniższa* (domyślna): najniższa wersja</li><li>*HighestPatch:* wersja z najniższą wersją główną, najmniejszą poprawką pomocniczą, najwyższą poprawką</li><li>*HighestMinor:* wersja z najniższą wersją główną, najwyższą poprawką pomocniczą i najwyższą</li><li>*Najwyższa:* najwyższa wersja</li><li>*Ignoruj:* nie będą używane żadne pakiety zależności</li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  Określa domyślną akcję, gdy plik z pakietu już istnieje w projekcie docelowym. Ustawienie na wartość `Overwrite` powoduje, że pliki są zawsze zastępowane. Ustaw na , `Ignore` aby pominąć pliki.

  Akcja, domyślna, będzie monitować o każdy plik powodujące konflikt, chyba że zostanie podany lub, co będzie `PromptUser` stosowane do wszystkich pozostałych `OverwriteAll` `IgnoreAll` plików.

- **`-ForceEnglishOutput`**

  *(3.5+)* Wymusza nuget.exe uruchamiania przy użyciu niezmiennej kultury opartej na języku angielskim.

- **`-?|-help`**

  Wyświetla informacje pomocy dotyczące polecenia.

- **`-Id`**

  Określa listę identyfikatorów pakietów do zaktualizowania.

- **`-MSBuildPath`**

  *(4.0+)* Określa ścieżkę msBuild do użycia z poleceniem, pierwszeństwo przed `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3.2+)* Określa wersję programu MSBuild, która ma być używana z tym poleceniem. Obsługiwane wartości to 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9. Domyślnie jest wybierany program MSBuild w ścieżce. W przeciwnym razie domyślnie jest wybierana najwyższa zainstalowana wersja programu MSBuild.

- **`-NonInteractive`**

  Pomija monity o wprowadzenie danych przez użytkownika lub potwierdzenia.

- **`-PreRelease`**

  Umożliwia aktualizowanie do wersji wstępnych. Ta flaga nie jest wymagana w przypadku aktualizowania pakietów wstępnych, które są już zainstalowane.

- **`-RepositoryPath`**

  Określa folder lokalny, w którym są instalowane pakiety.

- **`-Safe`**

  Określa, że zostaną zainstalowane tylko aktualizacje z najwyższą wersją dostępną w tej samej wersji główna i pomocnicza, co zainstalowany pakiet.

- **`-Self`**

  Aktualizacje `nuget.exe` do najnowszej wersji. `-Source` można użyć, jednak wszystkie inne argumenty są ignorowane. Jeśli nie podano źródła, sprawdza aktualizacje `nuget.org` niezależnie od `NuGet.Config` ustawień.

- **`-Source`**

  Określa listę źródeł pakietów (jako adresy URL) do użycia na użytek aktualizacji. Jeśli polecenie zostanie pominięte, użyje źródeł podanych w plikach konfiguracji. Zobacz [Typowe konfiguracje NuGet.](../../consume-packages/configuring-nuget-behavior.md)

- **`-Verbosity [normal|quiet|detailed]`**

  Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (ustawienie domyślne), `quiet` lub `detailed` .

- **`-Version`**

  Gdy jest używany z jednym identyfikatorem pakietu, określa wersję pakietu do zaktualizowania.

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
