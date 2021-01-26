---
title: project.jsNuGet dla pliku z projektami platformy UWP
description: Opis sposobu, w jaki project.jsw pliku jest używany do śledzenia zależności NuGet w projektach platforma uniwersalna systemu Windows (platformy UWP).
author: JonDouglas
ms.author: jodou
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: 30e2272aafb5d2ea8d932e3cb0209d97c30b3209
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773804"
---
# <a name="projectjson-and-uwp"></a>Plik project.json i platforma UWP

> [!Important]
> Ta zawartość jest przestarzała. Projekty powinny używać `packages.config` formatów lub PackageReference.

W tym dokumencie opisano strukturę pakietu, która wykorzystuje funkcje programu NuGet 3 + (Visual Studio 2015 i nowsze). `minClientVersion`Właściwość użytkownika `.nuspec` może być używana w celu ustalenia, czy są wymagane funkcje opisane w tym miejscu przez ustawienie go na 3,1.

## <a name="adding-uwp-support-to-an-existing-package"></a>Dodawanie obsługi platformy UWP do istniejącego pakietu

Jeśli masz istniejący pakiet i chcesz dodać obsługę aplikacji platformy UWP, nie musisz przyjąć formatu pakietu opisanego tutaj. Ten format należy zastosować tylko w przypadku, gdy wymagane są funkcje, które opisuje i które są dostępne tylko dla klientów zaktualizowanych do wersji 3 + klienta NuGet.

## <a name="i-already-target-netcore45"></a>Mam już element docelowy netcore45

Jeśli masz już miejsce docelowe `netcore45` i nie musisz korzystać z tych funkcji, nie trzeba wykonywać żadnych czynności. `netcore45` pakiety mogą być używane przez aplikacje platformy UWP.

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a>Chcę skorzystać z interfejsów API specyficznych dla systemu Windows 10

W takim przypadku należy dodać `uap10.0` moniker platformy docelowej (TFM lub TxM) do pakietu. Utwórz nowy folder w pakiecie i Dodaj zestaw, który został skompilowany do pracy z systemem Windows 10 do tego folderu.

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a>Nie potrzebuję interfejsów API specyficznych dla systemu Windows 10, ale potrzebujesz nowych funkcji platformy .NET lub nie masz już netcore45

W takim przypadku należy dodać `dotnet` TxM do pakietu. W przeciwieństwie do innych TxMs, `dotnet` nie oznacza obszaru powierzchni lub platformy. Jest stwierdzany, że pakiet działa na dowolnej platformie, na której działają zależności. Podczas kompilowania pakietu przy użyciu `dotnet` TxM istnieje wiele bardziej TxMych zależności określonych w programie `.nuspec` , ponieważ trzeba zdefiniować pakiety BCL, od których zależy, na przykład `System.Text` `System.Xml` itd. Lokalizacje, w których te zależności działają, definiują, gdzie działa pakiet.

### <a name="how-do-i-find-out-my-dependencies"></a>Jak mogę sprawdzić moje zależności

Istnieją dwa sposoby określania zależności do wyświetlenia:

1. Użyj narzędzia **innej firmy** dla [generatora zależności NuSpec](https://github.com/onovotny/ReferenceGenerator) . Narzędzie automatyzuje proces i aktualizuje `.nuspec` plik przy użyciu zależnych pakietów podczas kompilacji. Jest on dostępny za pośrednictwem pakietu NuGet [NuSpec. ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).

1. (W sposób twardy) Użyj `ILDasm` , aby `.dll` sprawdzić, jakie zestawy są rzeczywiście potrzebne w czasie wykonywania. Następnie ustal, z jakim pakietem NuGet pochodzą.

Zobacz [`project.json`](project-json.md) temat, aby uzyskać szczegółowe informacje na temat funkcji, które ułatwiają tworzenie pakietu, który obsługuje `dotnet` TxM.

> [!Important]
> Jeśli pakiet jest przeznaczony do pracy z projektami PCL, zdecydowanie zalecamy utworzenie `dotnet` folderu, aby uniknąć ostrzeżeń i potencjalnych problemów ze zgodnością.

## <a name="directory-structure"></a>Struktura katalogów

Pakiety NuGet używające tego formatu mają następujący dobrze znany folder i zachowania:

| Folder | Zachowania |
| --- | --- |
| Kompilacja | Zawiera elementy docelowe programu MSBuild i pliki props w tym folderze są zintegrowane w inny sposób w projekcie, ale w przeciwnym razie zmiany nie są zmieniane. |
| Narzędzia | `install.ps1` i `uninstall.ps1` nie są uruchamiane. `init.ps1` działa jak zawsze. |
| Zawartość | Zawartość nie jest automatycznie kopiowana do projektu użytkownika. Obsługa uwzględniania zawartości w projekcie jest planowana dla późniejszej wersji. |
| Lib | W przypadku wielu pakietów `lib` działa tak samo jak w programie NuGet 2. x, ale z rozwiniętymi opcjami dotyczącymi nazw, które mogą być używane wewnątrz niego, i lepsza logika do wybierania poprawnego podfolderu podczas korzystania z pakietów. Jednak w przypadku użycia w połączeniu z programem `ref` `lib` folder zawiera zestawy implementujące obszar powierzchni zdefiniowany przez zestawy w `ref` folderze. |
| Umieszczone | `ref` jest opcjonalnym folderem zawierającym zestawy .NET definiujące publiczną (typy publiczne i metody) dla aplikacji do skompilowania. Zestawy w tym folderze mogą nie mieć implementacji, są one wyłącznie używane do definiowania obszaru powierzchni dla kompilatora. Jeśli pakiet nie ma `ref` folderu, to `lib` zarówno zestaw odwołania, jak i zestaw implementacji. |
| Runtime | `runtimes` jest folderem opcjonalnym, który zawiera kod specyficzny dla systemu operacyjnego, taki jak architektura procesora CPU i dane binarne zależne od platformy lub w inny sposób. |

## <a name="msbuild-targets-and-props-files-in-packages"></a>Elementy docelowe programu MSBuild i pliki props w pakietach

Pakiety NuGet mogą zawierać `.targets` i `.props` pliki, które są importowane do dowolnego projektu programu MSBuild, do którego pakiet jest instalowany. W programie NuGet 2. x zostało to zrobione przez wstrzyknięcie `<Import>` instrukcji do `.csproj` pliku, w programie NuGet 3,0 nie ma określonego działania "Instalacja do projektu". Zamiast tego proces przywracania pakietu zapisuje dwa pliki `[projectname].nuget.props` i `[projectname].NuGet.targets` .

Program MSBuild wie o tych dwóch plikach i automatycznie importuje je blisko początku i blisko końca procesu tworzenia projektu. Zapewnia to bardzo podobne zachowanie do programu NuGet 2. x, ale z jedną istotną różnicą: *w tym przypadku nie ma gwarantowanej kolejności plików Target/props*. Jednak program MSBuild zapewnia sposoby porządkowania obiektów docelowych za pomocą `BeforeTargets` atrybutów i `AfterTargets` `<Target>` definicji (patrz [element Target)](/visualstudio/msbuild/target-element-msbuild).

## <a name="lib-and-ref"></a>Lib i ref

Zachowanie `lib` folderu nie zmienia się znacząco w programie NuGet v3. Jednak wszystkie zestawy muszą znajdować się w podfolderach o nazwie po TxM i nie mogą być umieszczane bezpośrednio w `lib` folderze. TxM to nazwa platformy, dla której ma być wykonane działanie danego elementu zawartości w pakiecie. Logicznie są to rozszerzenia monikerów platformy docelowej (TFM), np.,, `net45` `net46` `netcore50` i `dnxcore50` to wszystkie przykłady TxMs (zobacz [Platformy docelowe](../reference/target-frameworks.md). TxM może odwoływać się do struktury (TFM), a także innych obszarów powierzchni związanych z platformą. Na przykład platformy UWP TxM ( `uap10.0` ) reprezentuje obszar powierzchni .NET, a także obszar powierzchniowy systemu Windows dla aplikacji platformy UWP.

Przykładowa struktura lib:

```
lib
├───net40
│       MyLibrary.dll
└───wp81
        MyLibrary.dll
```

`lib`Folder zawiera zestawy, które są używane w czasie wykonywania. W przypadku większości pakietów wymagany jest folder w ramach `lib` każdego elementu docelowego TxMs.

## <a name="ref"></a>Umieszczone

Czasami istnieją przypadki, w których podczas kompilacji należy użyć innego zestawu (zestawy odwołań platformy .NET to dzisiaj). W tych przypadkach należy użyć folderu najwyższego poziomu o nazwie `ref` (krótkie dla "zestawów odwołań").

Większość autorów pakietów nie wymaga `ref` folderu. Jest to przydatne w przypadku pakietów, które wymagają zapewnienia spójnego obszaru powierzchni do kompilowania i IntelliSense, a następnie mają różne implementacje dla różnych TxMs. Największym przypadkiem użycia są `System.*` pakiety, które są tworzone w ramach wysyłki platformy .NET Core w pakiecie NuGet. Te pakiety mają różne implementacje, które są ujednolicone przez spójny zestaw zestawów referencyjnych.

W sposób mechaniczny zestawy dołączone do tego `ref` folderu są zestawami odwołań, które są przesyłane do kompilatora. Dla osób, które zostały użyte csc.exe są to zestawy przekazywane do przełącznika [opcji/Reference języka C#](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) .

Struktura `ref` folderu jest taka sama jak `lib` na przykład:

```
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
```

W tym przykładzie zestawy w `ref` katalogach powinny być identyczne.

## <a name="runtimes"></a>Runtime

Folder środowiska uruchomieniowe zawiera zestawy i natywne biblioteki wymagane do uruchamiania w określonych "środowiskach uruchomieniowych", które są zwykle zdefiniowane przez system operacyjny i architekturę procesora CPU. Te środowiska uruchomieniowe są identyfikowane przy użyciu [identyfikatorów środowiska uruchomieniowego (RID)](/dotnet/core/rid-catalog) , takich jak `win` ,, `win-x86` `win7-x86` , `win8-64` itd.

## <a name="native-helpers-to-use-platform-specific-apis"></a>Natywni pomocnicy korzystający z interfejsów API specyficznych dla platformy

W poniższym przykładzie przedstawiono pakiet, który ma czysto zarządzaną implementację kilku platform, ale używa natywnych pomocników w systemie Windows 8, gdzie może wywoływać interfejsy natywne interfejsów API dla systemu Windows 8.

```
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
```

Powyższym pakietem zachodzą następujące kwestie:

- Gdy nie ma w systemie Windows 8, `lib/net40/MyLibrary.dll` używany jest zestaw.

- W przypadku systemu Windows 8 `runtimes/win8-<architecture>/lib/MyLibrary.dll` jest używany i `native/MyNativeHelper.dll` jest kopiowany do danych wyjściowych kompilacji.

W powyższym przykładzie `lib/net40` zestaw jest czystym kodem zarządzanym, podczas gdy zestawy w folderze Runtimes są p/Invoke do natywnego zestawu pomocnika, aby wywoływać interfejsy API specyficzne dla systemu Windows 8.

Tylko jeden `lib` folder jest kiedykolwiek wybierany, więc jeśli istnieje folder specyficzny dla środowiska uruchomieniowego, który jest wybierany przez niezależny od środowiska uruchomieniowego `lib` . Folder macierzysty jest dodatkiem, jeśli istnieje, jest kopiowany do danych wyjściowych kompilacji.

## <a name="managed-wrapper"></a>Otoka zarządzana

Innym sposobem użycia środowiska uruchomieniowego jest dostarczenie pakietu, który jest całkowicie zarządzanym otoką w zestawie natywnym. W tym scenariuszu utworzysz pakiet podobny do następującego:

```
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
```

W takim przypadku nie ma folderu najwyższego poziomu, ponieważ ten folder nie ma `lib` implementacji tego pakietu, który nie bazuje na odpowiednim zestawie macierzystym. Jeśli zarządzany zestaw, `MyLibrary.dll` ,, był dokładnie taki sam w obu tych przypadkach, można go umieścić w folderze najwyższego poziomu `lib` , ale ponieważ brak zestawu natywnego nie powoduje, że instalacja pakietu nie powiedzie się, jeśli został on zainstalowany na platformie, która nie powiodła się — x86 lub win-x64, zostanie użyta Biblioteka najwyższego poziomu, ale nie będzie można skopiować zestawu natywnego.

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a>Tworzenie pakietów dla programu NuGet 2 i NuGet 3

Jeśli chcesz utworzyć pakiet, który może być używany przez projekty, a `packages.config` także pakiety przy użyciu następujących warunków `project.json` :

- Odwołania i środowiska uruchomieniowe działają tylko na serwerze NuGet 3. Są one ignorowane przez program NuGet 2.

- Nie można polegać na `install.ps1` lub `uninstall.ps1` funkcji. Te pliki są wykonywane przy użyciu `packages.config` , ale są ignorowane w programie `project.json` . Aby pakiet był gotowy do użytku bez ich działania. `init.ps1` nadal działa w programie NuGet 3.

- Instalacja elementów docelowych i właściwości jest inna, dlatego należy się upewnić, że pakiet działa zgodnie z oczekiwaniami na obu klientach.

- Podkatalogi biblioteki lib muszą być TxM w programie NuGet 3. Biblioteki nie mogą być umieszczane w katalogu głównym `lib` folderu.

- Zawartość nie jest kopiowana automatycznie z pakietem NuGet 3. Odbiorcy pakietu mogą skopiować same pliki lub użyć narzędzia, takiego jak moduł uruchamiający zadania, aby zautomatyzować kopiowanie plików.

- Przekształcenia plików źródłowych i konfiguracji nie są uruchamiane przez pakiet NuGet 3.

Jeśli obsługujesz program NuGet 2 i 3, `minClientVersion` powinna to być najniższa wersja klienta NuGet 2, na którym działa pakiet. W przypadku istniejącego pakietu nie trzeba zmieniać.
