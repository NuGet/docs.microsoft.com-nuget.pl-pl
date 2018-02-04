---
title: Projekty platformy UWP pliku project.json NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Opis sposobu pliku project.json jest używane do śledzenia zależności NuGet w projektach systemu Windows platformy Uniwersalnej."
keywords: "Zależności NuGet, NuGet i platformy uniwersalnej systemu Windows, platformy uniwersalnej systemu Windows i project.json, plik project.json NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f1ec086d6404c441ca5ad53028af2265a2344905
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/01/2018
---
# <a name="projectjson-and-uwp"></a>pliku Project.JSON i platformy uniwersalnej systemu Windows

> [!Important]
> Ta zawartość jest przestarzały. Projekty powinny używać albo `packages.config` lub PackageReference formatów.

W tym dokumencie opisano strukturę pakietu, która wykorzystuje funkcje programu NuGet 3 + (Visual Studio 2015 i nowsze). `minClientVersion` Właściwości użytkownika `.nuspec` może służyć do stanu, aby wymagać funkcje opisane w tym miejscu, ustawiając go na 3.1.

## <a name="adding-uwp-support-to-an-existing-package"></a>Dodawanie obsługi platformy uniwersalnej systemu Windows do istniejącego pakietu

Jeśli masz istniejący pakiet i chcesz dodać obsługę aplikacji platformy uniwersalnej systemu Windows, nie muszą przyjęcie format pakowania opisane w tym miejscu. Należy przyjąć tego formatu, jeśli wymagane funkcje, w tym artykule opisano i chcesz pracować tylko z klientami, które zostały zaktualizowane w wersji 3 + klienta NuGet.

## <a name="i-already-target-netcore45"></a>Mogę wskazać już netcore45

W przypadku skierowania `netcore45` już i nie trzeba korzystać z funkcji w tym miejscu, nie jest potrzebne nie działanie. `netcore45`pakiety mogą być używane przez aplikacje platformy uniwersalnej systemu Windows.

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a>Chcę korzystać z określonych interfejsów API systemu Windows 10

W takim przypadku należy dodać `uap10.0` target framework moniker (TFM lub TxM) do pakietu. Utwórz nowy folder do pakietu, a następnie dodaj zestawu, który został skompilowany do pracy z systemem Windows 10 do tego folderu.

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a>Nie potrzebuję poszczególnych interfejsów API systemu Windows 10, ale ma nowe funkcje platformy .NET lub nie został jeszcze netcore45

W takim przypadku należy dodać `dotnet` TxM do pakietu. W odróżnieniu od innych TxMs `dotnet` nie wiąże się z powierzchni ani platformy. Jest informujący pakietu działa na dowolnej platformie, która pracuje zależności. Podczas tworzenia pakietu z `dotnet` TxM, najprawdopodobniej będzie zależnościami dużo więcej TxM określonych Twojej `.nuspec`, musisz zdefiniować pakiety BCL możesz zależne, takie `System.Text`, `System.Xml`itp. Lokalizacje, które działają tych zależności w zdefiniuj, gdzie działa pakietu.

### <a name="how-do-i-find-out-my-dependencies"></a>Jak sprawdzić Moje zależności

Istnieją dwa sposoby, aby dowiedzieć się, które zależności, aby wyświetlić listę:

1. Użyj [Generator zależności NuSpec](https://github.com/onovotny/ReferenceGenerator) **3 strona** narzędzia. Narzędzie automatyzuje proces i aktualizacji programu `.nuspec` pliku z pakietów zależnych podczas kompilacji. Jest dostępna za pośrednictwem pakietu NuGet, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).

1. (Sposób twarde) Użyj `ILDasm` spojrzeć na Twojej `.dll` aby zobaczyć, jakie zestawy są faktycznie wymagane w czasie wykonywania. Następnie określ pakietu NuGet, które mają pochodzić z.

Zobacz [ `project.json` ](project-json.md) tematu, aby uzyskać szczegółowe informacje na funkcje, które ułatwiają tworzenie pakietu, który obsługuje `dotnet` TxM.

> [!Important]
> Jeśli pakiet jest przeznaczony do pracy z projektami PCL, zalecamy tworzenie `dotnet` folderu, aby uniknąć ostrzeżenia i potencjalnych problemów ze zgodnością.

## <a name="directory-structure"></a>Struktura katalogów

Pakiety NuGet, w tym formacie mają następujące dobrze znany folder i zachowania:

| Folder | Zachowania |
| --- | --- |
| Kompilacja | Zawiera MSBuild cele i pliki właściwości w tym folderze są zintegrowane z inną nazwę projektu, ale w przeciwnym razie nie została zmieniona. |
| Narzędzia | `install.ps1`i `uninstall.ps1` nie są uruchamiane. `init.ps1`działa jako zawsze ma. |
| Zawartość | Zawartość nie jest kopiowana automatycznie do użytkownika projektu. Obsługa zawartości uwzględnienie w projekcie jest planowane w nowszej wersji. |
| Lib | Wiele pakietów `lib` działa tak samo w NuGet 2.x, ale bez opcji rozwinięte jakie nazwy może być używany w go i lepsze logiki dla pobrania poprawne podfolderu w przypadku uzyskiwania dostępu do pakietów. Jednak w przypadku używania w połączeniu z `ref`, `lib` folder zawiera zestawy, które implementuje powierzchni zdefiniowane przez zestawy w `ref` folderu. |
| REF | `ref`jest opcjonalny folder zawierający zestawy .NET Definiowanie publicznego powierzchni (typy publiczne i metody) do kompilacji dla aplikacji. Zestawy w tym folderze może mieć żadnej implementacji, czysto są one używane do definiowania powierzchni dla kompilatora. Jeśli nie ma pakietu `ref` folder, a następnie `lib` jest odwołanie do zestawu i zestawu implementacji. |
| środowisk uruchomieniowych | `runtimes`jest opcjonalny folder zawierający kod określonego systemu operacyjnego, takie jak architektura Procesora i systemu operacyjnego określonego lub w inny sposób zależny od platformy plików binarnych. |

## <a name="msbuild-targets-and-props-files-in-packages"></a>MSBuild cele i pliki właściwości w pakiety

Pakiety NuGet mogą zawierać `.targets` i `.props` pliki, które są importowane do żadnego projektu MSBuild zainstalowanego pakietu do. W NuGet 2.x, to był przez wstrzykiwanie `<Import>` instrukcje do `.csproj` pliku, w NuGet 3.0 istnieje akcja określonych "Instalacja do projektu". Zamiast tego proces przywracania pakietu zapisuje dwa pliki `[projectname].nuget.props` i `[projectname].NuGet.targets`.

MSBuild zna do wyszukania tych plików i automatycznie importowane na początku i pod koniec procesu tworzenia projektu. Zapewnia to bardzo podobnie do NuGet 2.x, ale z jedną główną różnicą: *istnieje w tym przypadku nie gwarantuje kolejność plików celów/arkuszy właściwości*. Jednak MSBuild udostępniają sposoby kolejności docelowych za pośrednictwem `BeforeTargets` i `AfterTargets` atrybuty `<Target>` definicji (zobacz [Target — Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).

## <a name="lib-and-ref"></a>Lib i Ref

Zachowanie `lib` folderu nie zmieniła się znacznie w NuGet w wersji 3. Jednak wszystkie zestawy muszą się znajdować w podfoldery o nazwie po TxM i nie można umieścić bezpośrednio pod `lib` folderu. TxM jest nazwą platformy, który ma działać w przypadku danej zawartości w pakiecie. Logicznie rozszerzenia elementu docelowego Framework monikerów (TFM) są to np. `net45`, `net46`, `netcore50`, i `dnxcore50` należą do nich TxMs (zobacz [docelowych platform](../reference/target-frameworks.md). TxM mogą odwoływać się do struktury (TFM) oraz innych obszarach powierzchni specyficzne dla platformy. Na przykład TxM platformy uniwersalnej systemu Windows (`uap10.0`) reprezentuje powierzchni .NET, a także powierzchni systemu Windows dla aplikacji platformy uniwersalnej systemu Windows.

Przykład struktury lib:

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

`lib` Folder zawiera zestawy, które są używane w czasie wykonywania. Większość pakietów folderu `lib` dla każdego elementu docelowego TxMs to wszystko, co jest wymagane.

## <a name="ref"></a>REF

Czasami istnieją przypadki, w których należy używać innym zestawie podczas kompilacji (.NET zestawów odwołań do tego dzisiaj). Dla tych przypadków użycia folder najwyższego poziomu o nazwie `ref` (skrót od "zestawów odwołań").

Większość autorów pakietu nie wymagają `ref` folderu. Jest to przydatne w przypadku pakietów, które należy zapewnić spójne powierzchni IntelliSense i kompilacji, ale następnie inną implementację dla różnych TxMs. Przypadek użycia największych są `System.*` pakietów oferowanych w ramach wysyłanie .NET Core na NuGet. Te pakiety mają różne implementacje, które są trwa unified spójny zestaw zestawy ref.

Mechanicznie zestawy zawarte w `ref` znajdują się zestawy referencyjne przekazywany do kompilatora. Dla tych osób, które zostały użyte csc.exe są zestawy, możemy przekazywane do [opcji/Reference C#](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) przełącznika.

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

W tym przykładzie zestawów w `ref` katalogów wszystkie będą identyczne.

## <a name="runtimes"></a>środowisk uruchomieniowych

Folder środowisk uruchomieniowych zawiera zestawy i natywnych bibliotek wymaganych do uruchomienia na określonym "środowisk uruchomieniowych", które są zazwyczaj definiowane przez architekturę systemu operacyjnego i procesora CPU. Te programy obsługi są identyfikowane za pomocą [identyfikatorów środowiska uruchomieniowego (RID)](/dotnet/core/rid-catalog) takich jak `win`, `win-x86`, `win7-x86`, `win8-64`itp.

## <a name="native-light-up"></a>Natywny światła w górę

W poniższym przykładzie przedstawiono czysto zarządzaną implementację dla różnych platform, które używa pomocników macierzystego w systemie Windows 8, gdzie może wywołać do natywnych interfejsów API systemu Windows 8 określonego pakietu.

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

Podany pakiet powyżej stanie następujących czynności:

- Kiedy nie w systemie Windows 8 `lib/net40/MyLibrary.dll` zestaw jest używany.

- Gdy w systemie Windows 8 `runtimes/win8-<architecture>/lib/MyLibrary.dll` jest używany i `native/MyNativeHelper.dll` jest kopiowany do danych wyjściowych kompilacji.

W powyższym przykładzie `lib/net40` zestaw jest wyłącznie kod zarządzany, podczas gdy zestawów w folderze środowisk uruchomieniowych będzie p/invoke do zestawu macierzystego pomocnika do wywoływania interfejsów API specyficzne dla systemu Windows 8.

Tylko jeden `lib` folder jest kiedykolwiek zostać pobrane, więc jeśli istnieje folder określonego środowiska uruchomieniowego jest wybierany przez konkretnego z systemem innym niż środowisko uruchomieniowe `lib`. Folder macierzysty jest dodatku, jeśli taka istnieje jest kopiowany do danych wyjściowych kompilacji.

## <a name="managed-wrapper"></a>Zarządzany otok

Innym sposobem użycia środowisk uruchomieniowych jest na potrzeby wysłania pakietu, który jest wyłącznie zarządzany otok za pośrednictwem natywnych zestawów. W tym scenariuszu należy utworzyć pakiet podobne do poniższych:

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

W takim przypadku istnieje nie najwyższego poziomu `lib` folderze, w tym folderze, ponieważ wystąpiły jest żadnej implementacji tego pakietu, które nie korzystają z odpowiedniego zestawu macierzystego. Jeśli zestaw zarządzany `MyLibrary.dll`, została dokładnie taka sama w obu przypadkach firma Microsoft może umieść ją w najwyższego poziomu `lib` folderu, ale ponieważ brak natywny zestaw nie powoduje pakietu niepowodzenie instalacji, jeśli została zainstalowana na platformie który następnie lib najwyższego poziomu, które mają być używane, ale nie natywny zestaw jest kopiowany były x86 Windows lub Windows x64.

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a>Tworzenie pakietów NuGet 2 i NuGet 3

Jeśli chcesz utworzyć pakiet, który może być zużyte przez projektów przy użyciu `packages.config` również jako pakietów przy użyciu `project.json` następnie następujących warunków:

- REF i środowisk uruchomieniowych tylko pracy nad NuGet 3. Są one zarówno ignorowane przez NuGet 2.

- Nie należy polegać na `install.ps1` lub `uninstall.ps1` funkcji. Wykonanie tych plików przy użyciu `packages.config`, ale są ignorowane z `project.json`. Dlatego pakietu musi być możliwe bez ich uruchamiania. `init.ps1`nadal działa na NuGet 3.

- Cele i właściwości instalacji jest inny, dlatego należy upewnić się, że pakiet działa zgodnie z oczekiwaniami na obu komputerach klienckich.

- Podkatalogi lib musi być TxM w NuGet 3. Nie można umieścić bibliotek w katalogu głównym `lib` folderu.

- Zawartość nie jest kopiowana automatycznie z NuGet 3. Konsumentów pakietu można skopiować same pliki lub zautomatyzować kopiowania plików za pomocą narzędzia, takiego jak modułu uruchamiającego zadania.

- Transformacje pliku źródłowego i konfiguracji nie są uruchamiane przez NuGet 3.

Jeśli są obsługiwane NuGet 2 i 3, a następnie z `minClientVersion` powinny być najniższy wersji klienta NuGet 2, który pracuje pakietu. W przypadku istniejącego pakietu nie powinna wymagać zmiany.