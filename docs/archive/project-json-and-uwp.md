---
title: Plik project.json NuGet w projektach platformy uniwersalnej systemu Windows
description: Opis sposobu używania pliku project.json do śledzenia zależności NuGet w projektach platformy uniwersalnej Windows (UWP).
author: karann-msft
ms.author: karann
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: ac3c137dd0ba50571737093eef11c8ab0ef932b2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548667"
---
# <a name="projectjson-and-uwp"></a>Plik Project.JSON i platformy uniwersalnej systemu Windows

> [!Important]
> Ta zawartość jest przestarzały. Projekty powinny używać albo `packages.config` lub PackageReference podzielony na fragmenty.

W tym dokumencie opisano strukturę pakietu, która używa funkcji NuGet 3 + (Visual Studio 2015 i nowszych). `minClientVersion` Właściwości usługi `.nuspec` może służyć do stanu wymagane funkcje opisane w tym miejscu, ustawiając go na 3.1.

## <a name="adding-uwp-support-to-an-existing-package"></a>Dodawanie obsługi platformy uniwersalnej systemu Windows do istniejącego pakietu

Jeśli masz istniejący pakiet, i chcesz dodać obsługę aplikacji platformy uniwersalnej systemu Windows, nie należy do przyjęcia format pakowania, opisane w tym miejscu. Należy przyjąć tego formatu, jeśli potrzebujesz funkcji, w tym artykule opisano i jest gotowa do pracy tylko w przypadku klientów, które zostały zaktualizowane do wersji 3 + klienta programu NuGet.

## <a name="i-already-target-netcore45"></a>Czy mogę wskazać już netcore45

Jeśli platformą docelową jest `netcore45` i nie trzeba korzystać z funkcji w tym miejscu, jest wymagana żadna akcja. `netcore45` pakiety mogą być używane przez aplikacje platformy uniwersalnej systemu Windows.

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a>Chcę móc korzystać z określonych interfejsów API systemu Windows 10

W takim przypadku należy dodać `uap10.0` docelowe moniker struktury (TFM lub TxM) do pakietu. Utwórz nowy folder w pakiecie i dodać zestaw, który został wcześniej skompilowany do pracy z systemem Windows 10 do tego folderu.

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a>Nie potrzebuję określonych interfejsów API systemu Windows 10, ale ma nowe funkcje platformy .NET lub nie został jeszcze netcore45

W takim przypadku należy dodać `dotnet` TxM do pakietu. W przeciwieństwie do innych TxMs `dotnet` nie sugeruje się udzielenia, powierzchni lub platformy. Jest o pakietu działa na dowolnej platformie, które zależności działają w treści. Podczas tworzenia pakietu o `dotnet` TxM, najprawdopodobniej będzie mieć wiele więcej zależności TxM określonych w swojej `.nuspec`, jak należy zdefiniować pakietów BCL, na przykład `System.Text`, `System.Xml`itp. Lokalizacje, które te zależności pracować nad definiują, gdzie działa pakiet.

### <a name="how-do-i-find-out-my-dependencies"></a>Jak sprawdzić zależności

Istnieją dwa sposoby, aby ustalić którym zależności, aby wyświetlić listę:

1. Użyj [Generator zależności NuSpec](https://github.com/onovotny/ReferenceGenerator) **firm 3** narzędzia. Narzędzie automatyzuje proces i aktualizacji usługi `.nuspec` plików za pomocą pakietów zależnych podczas kompilacji. Jest on dostępny za pośrednictwem pakietu NuGet, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).

1. (Sposób) Użyj `ILDasm` Przyjrzyj się Twoje `.dll` aby zobaczyć, jakie zestawy są rzeczywiście potrzebne w czasie wykonywania. Następnie określ pakiet NuGet, które każdy pochodzą z.

Zobacz [ `project.json` ](project-json.md) tematu, aby uzyskać szczegółowe informacje na temat funkcji, które pomagają w utworzeniu pakietu, który obsługuje `dotnet` TxM.

> [!Important]
> Jeśli pakiet jest przeznaczony do pracy z projektów PCL, zalecamy tworzenie `dotnet` folderu, w celu uniknięcia ostrzeżeń i potencjalnych problemów ze zgodnością.

## <a name="directory-structure"></a>Struktura katalogów

Pakiety NuGet, używając następującego formatu mają następujące dobrze znany folder i zachowania:

| Folder | Zachowania |
| --- | --- |
| Kompilacja | Zawiera program MSBuild cele i pliki właściwości w tym folderze są zintegrowane inaczej w projekcie, ale w przeciwnym razie nie nastąpiła żadna zmiana. |
| Narzędzia | `install.ps1` i `uninstall.ps1` nie są uruchamiane. `init.ps1` działa jak zawsze ma. |
| Zawartość | Zawartość nie jest kopiowana automatycznie do projektu użytkownika. Obsługa zawartości uwzględnianie w projekcie jest planowana w nowszej wersji. |
| lib | W przypadku wielu pakietów `lib` działa tak samo w NuGet 2.x, ale z rozszerzone opcje nazwy, jakie może być używany wewnątrz go i lepiej logiki dla pobrania poprawne podfolder, podczas korzystania z pakietów. Jednakże gdy jest używana w połączeniu z `ref`, `lib` folder zawiera zestawy, które implementują podatny na atak obszar zdefiniowany przez zestawy w `ref` folderu. |
| REF | `ref` jest opcjonalny folder zawierający zestawy .NET, definiując publicznie powierzchni (typy i metody publiczne) do kompilowanie z użyciem aplikacji. Zestawy znajdujące się w tym folderze może nie mają implementacji, czysto służą one do definiowania powierzchni dla kompilatora. Jeśli nie ma pakietu `ref` folder, a następnie `lib` jest zestaw odwołania i zestawu implementacji. |
| środowiska uruchomieniowe | `runtimes` jest opcjonalny folder zawierający kod określonego systemu operacyjnego, takich jak architektura procesora CPU i określonych lub w inny sposób zależny od platformy plików binarnych systemu operacyjnego. |

## <a name="msbuild-targets-and-props-files-in-packages"></a>Program MSBuild cele i pliki właściwości w pakietach

Pakiety NuGet może zawierać `.targets` i `.props` pliki, które są importowane do każdego projektu MSBuild, który pakiet jest zainstalowany w. W pakiecie NuGet 2.x, stało się przez wstrzykiwanie `<Import>` instrukcje do `.csproj` plików, NuGet 3.0 nie ma określonych "Instalacja z projektem" akcji. Zamiast tego proces przywracania pakietów zapisuje dwa pliki `[projectname].nuget.props` i `[projectname].NuGet.targets`.

Program MSBuild wie, aby wyszukać te dwa pliki i automatycznie importuje, na początku i pod koniec procesu kompilacji projektu. Zapewnia to zachowanie bardzo podobne do narzędzia NuGet 2.x, ale z jedną główną różnicą: *nie jest zagwarantowana kolejność plików celów/arkuszy właściwości w tym przypadku*. Jednak program MSBuild umożliwiają kolejność elementów docelowych, za pośrednictwem `BeforeTargets` i `AfterTargets` atrybuty `<Target>` definicji (zobacz [Target — Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).

## <a name="lib-and-ref"></a>Biblioteki i Ref

Zachowanie `lib` folderu nie zmieniły się znacznie w wersji NuGet 3. Jednak wszystkie zestawy muszą znajdować się w podfolderach o nazwie po TxM i nie będzie można umieścić bezpośrednio pod `lib` folderu. TxM nazywa się to platforma, która powinna działać w przypadku danego elementu zawartości w pakiecie. Logicznie te stanowią rozszerzenie z monikerów Framework docelowych (TFM) np. `net45`, `net46`, `netcore50`, i `dnxcore50` należą do nich TxMs (zobacz [platform docelowych](../reference/target-frameworks.md). TxM mogą odwoływać się do struktury (TFM) oraz innych obszarów specyficzne dla platformy. Na przykład TxM platformy uniwersalnej systemu Windows (`uap10.0`) reprezentuje obszar powierzchni .NET, a także Windows podatny na atak obszar dla aplikacji platformy uniwersalnej systemu Windows.

Przykład struktury lib:

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

`lib` Folder zawiera zestawy, które są używane w czasie wykonywania. Większość pakietów folder w węźle `lib` dla każdego obiektu docelowego TxMs to wszystko, co jest wymagane.

## <a name="ref"></a>REF

Czasami są przypadki użycia innego zestawu podczas kompilacji (do tego dzisiaj zestawy referencyjne platformy .NET). Dla tych przypadków użycia folder najwyższego poziomu o nazwie `ref` (skrót od "zestawy odwołań").

Większość autorom pakietów nie wymagają `ref` folderu. Jest to przydatne w przypadku pakietów, które muszą zapewnić spójny obszar powierzchni dla IntelliSense i kompilacja, ale następnie różne implementacje dla różnych TxMs. Największe przypadek użycia są `System.*` pakietów oferowanych w ramach wysyłki platformy .NET Core dla narzędzia NuGet. Te pakiety mają różne implementacje, które są trwa unified według spójny zbiór zestawów odwołania.

Mechanicznie zestawy zawarte w `ref` folderu są zestawy odwołania są przekazywane do kompilator. Dla osób, które były używane csc.exe są zestawy, firma Microsoft kończy się sukcesem [opcji/Reference C#](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) przełącznika.

Struktura `ref` folderu jest taka sama jak `lib`, na przykład:

    └───MyImageProcessingLib
         ├───lib
         │   ├───net40
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   ├───net451
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   └───win81
         │           MyImageProcessingLibrary.dll
         │
         └───ref
             ├───net40
             │       MyImageProcessingLibrary.dll
             │
             └───portable-net451-win81
                     MyImageProcessingLibrary.dll

W tym przykładzie zestawów w `ref` katalogów wszystkie będzie taka sama.

## <a name="runtimes"></a>środowiska uruchomieniowe

Folder środowiska uruchomieniowe zawiera zestawów i bibliotek natywnych wymagane do uruchamiania na określonych "runtimes", które są zazwyczaj definiowane przez architekturę systemu operacyjnego i procesora CPU. Te środowiska uruchomieniowe są identyfikowane za pomocą [identyfikatorów środowiska uruchomieniowego (RID)](/dotnet/core/rid-catalog) takich jak `win`, `win-x86`, `win7-x86`, `win8-64`itp.

## <a name="native-helpers-to-use-platform-specific-apis"></a>Natywne pomocników użycia interfejsów API specyficznych dla platformy

Poniższy przykład pokazuje czysto zarządzaną implementację dla różnych platform, które używa pomocników natywnych w systemie Windows 8, gdzie może wywołać do natywnych interfejsów API systemu Windows 8 określonego pakietu.

    └───MyLibrary
         ├───lib
         │   └───net40
         │           MyLibrary.dll
         │
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net40
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyNativeLibrary.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net40
                 │           MyLibrary.dll
                 │
                 └───native
                         MyNativeLibrary.dll

Biorąc pod uwagę powyższe pakietu się zdarzyć następujących czynności:

- Kiedy nie w systemie Windows 8 `lib/net40/MyLibrary.dll` zestaw jest używany.

- Gdy w systemie Windows 8 `runtimes/win8-<architecture>/lib/MyLibrary.dll` jest używany i `native/MyNativeHelper.dll` jest kopiowany do wyjściowego kompilacji.

W powyższym przykładzie `lib/net40` zestaw jest tylko kod zarządzany, podczas gdy zestawy znajdujące się w folderze środowiska uruchomieniowe będzie p/invoke do zestawu macierzystego pomocnika do wywoływania interfejsów API specyficznych dla systemu Windows 8.

Tylko jeden `lib` folderu jest nigdy nie zostać pobrane, więc w przypadku określonego folderu środowiska uruchomieniowego jest wybierany za pośrednictwem określonego bez środowiska uruchomieniowego `lib`. Folder macierzysty to dodatek, jeśli taki istnieje, jest kopiowany do danych wyjściowych kompilacji.

## <a name="managed-wrapper"></a>Zarządzana otoka

Innym sposobem użycia środowiska uruchomieniowe jest na potrzeby wysłania pakietu, który jest całkowicie zarządzana otoka za pośrednictwem natywnych zestawów. W tym scenariuszu utworzysz pakietu, jak pokazano poniżej:

    └───MyLibrary
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net451
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyImplementation.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net451
                 │           MyLibrary.dll
                 │
                 └───native
                         MyImplementation.dll

W tym przypadku istnieje nie najwyższego poziomu `lib` folderze, w tym folderze, co tam się bez wdrażania tego pakietu, który nie jest zależny od odpowiedniego natywny zestaw. Jeśli zestaw zarządzany `MyLibrary.dll`, została dokładnie takie same w obu przypadkach firma Microsoft może umieścić go w najwyższego poziomu `lib` folderu, ale ponieważ brak natywny zestaw nie powoduje pakietu niepowodzenie instalacji, jeśli została zainstalowana na platformie, nie były win x86 lub win x64, a następnie lib najwyższego poziomu będzie używana, ale nie natywny zestaw zostałoby skopiowanych.

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a>Tworzenie pakietów NuGet, 2 i NuGet 3

Jeśli chcesz utworzyć pakiet, który może być zużyte przez projektów przy użyciu `packages.config` również jako pakiety przy użyciu `project.json` następnie następujących warunków:

- REF i środowisk wykonawczych pracować tylko NuGet 3. Są one zarówno ignorowane przez NuGet 2.

- Nie można polegać na `install.ps1` lub `uninstall.ps1` funkcji. Wykonaj te pliki, korzystając z `packages.config`, ale są ignorowane z `project.json`. Więc pakietu musi być możliwe bez ich uruchamiania. `init.ps1` wciąż działa na NuGet 3.

- Cele i właściwości instalacji jest inny, dlatego upewnij się, że pakiet działa zgodnie z oczekiwaniami na obu komputerach klienckich.

- Podkatalogi lib musi być TxM NuGet 3. Nie można umieścić bibliotek w katalogu głównym `lib` folderu.

- Zawartość nie jest kopiowana automatycznie za pomocą NuGet 3. Konsumentów pakietu można kopiować pliki, samodzielnie lub użyj narzędzia, takiego jak modułu uruchamiającego zadania do zautomatyzowania kopiowania plików.

- Przekształcenia pliku źródłowego i konfiguracji nie są uruchamiane przez NuGet 3.

Jeśli są obsługiwane NuGet 2 i 3 wówczas `minClientVersion` powinno być najniższą wersją klienta NuGet 2, który pracuje pakietu. W przypadku istniejącego pakietu nie powinna wymagać zmiany.
