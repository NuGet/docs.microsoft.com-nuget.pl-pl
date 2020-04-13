---
title: Plik NuGet project.json z projektami platformy uniwersalnej systemuśpiłnie
description: Opis sposobu, w jaki plik project.json jest używany do śledzenia zależności NuGet w projektach platformy uniwersalnej systemu Windows (UWP).
author: karann-msft
ms.author: karann
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: ac3c137dd0ba50571737093eef11c8ab0ef932b2
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "64494372"
---
# <a name="projectjson-and-uwp"></a>Plik project.json i platforma UWP

> [!Important]
> Ta zawartość jest przestarzała. Projekty powinny używać `packages.config` formatów lub PackageReference.

W tym dokumencie opisano strukturę pakietu, który wykorzystuje funkcje w NuGet 3+ (Visual Studio 2015 i nowsze). Właściwość `minClientVersion` użytkownika `.nuspec` może służyć do określania, że wymagane są funkcje opisane w tym miejscu, ustawiając ją na 3.1.

## <a name="adding-uwp-support-to-an-existing-package"></a>Dodawanie pomocy technicznej platformy uniwersalnej systemu i platformy uniwersalnej do istniejącego pakietu

Jeśli masz istniejący pakiet i chcesz dodać obsługę aplikacji platformy uniwersalnej systemuśpiłka, nie musisz przyjmować formatu opakowania opisanego w tym miejscu. Wystarczy przyjąć ten format tylko wtedy, gdy wymagane funkcje, które opisuje i są chętni do pracy tylko z klientami, które zostały zaktualizowane do wersji 3 + klienta NuGet.

## <a name="i-already-target-netcore45"></a>Ja już cel netcore45

Jeśli już `netcore45` kierujesz reklamy i nie musisz korzystać z funkcji w tym miejscu, nie jest potrzebne żadne działanie. `netcore45`pakiety mogą być używane przez aplikacje platformy uniwersalnej systemuśpiłnie.

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a>Chcę skorzystać z interfejsów API specyficznych dla systemu Windows 10

W takim przypadku należy `uap10.0` dodać moniker struktury docelowej (TFM lub TxM) do pakietu. Utwórz nowy folder w pakiecie i dodaj zestaw, który został skompilowany do pracy z systemem Windows 10 do tego folderu.

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a>Nie potrzebuję specyficznych interfejsów API systemu Windows 10, ale chcę nowych funkcji .NET lub nie mam już netcore45

W takim przypadku należy `dotnet` dodać TxM do pakietu. W przeciwieństwie do innych `dotnet` TxM, nie oznacza powierzchni lub platformy. Jest to stwierdzające, że pakiet działa na dowolnej platformie, na którym działają zależności. Podczas tworzenia pakietu `dotnet` z TxM, prawdopodobnie masz o wiele więcej zależności specyficznych dla TxM w , `.nuspec`jak trzeba `System.Text` `System.Xml`zdefiniować pakiety BCL, na których polegasz, takie , itp. Lokalizacje, które działają te zależności na zdefiniować, gdzie działa pakiet.

### <a name="how-do-i-find-out-my-dependencies"></a>Jak sprawdzić moje zależności

Istnieją dwa sposoby, aby dowiedzieć się, które zależności do listy:

1. Użyj narzędzia [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) **3rd party.** Narzędzie automatyzuje proces `.nuspec` i aktualizuje plik za pomocą pakietów zależnych na kompilacji. Jest on dostępny za pośrednictwem pakietu NuGet, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).

1. (Trudna droga) Użyj, `ILDasm` aby `.dll` spojrzeć na swoje, aby zobaczyć, jakie zestawy są rzeczywiście potrzebne w czasie wykonywania. Następnie należy określić, który pakiet NuGet, z którego pochodzą.

Zobacz [`project.json`](project-json.md) temat, aby uzyskać szczegółowe informacje na temat funkcji, które pomagają w tworzeniu pakietu, który obsługuje `dotnet` TxM.

> [!Important]
> Jeśli pakiet jest przeznaczony do pracy z projektami PCL, zdecydowanie zaleca się utworzenie folderu, `dotnet` aby uniknąć ostrzeżeń i potencjalnych problemów ze zgodnością.

## <a name="directory-structure"></a>Struktura katalogów

Pakiety NuGet przy użyciu tego formatu mają następujący dobrze znany folder i zachowania:

| Folder | Zachowania |
| --- | --- |
| Kompilacja | Zawiera obiekty docelowe MSBuild i rekwizyty pliki w tym folderze są zintegrowane inaczej do projektu, ale w przeciwnym razie nie ma żadnych zmian. |
| Narzędzia | `install.ps1`i `uninstall.ps1` nie są uruchamiane. `init.ps1`działa jak zawsze. |
| Zawartość | Zawartość nie jest automatycznie kopiowana do projektu użytkownika. Wsparcie dla dołączania zawartości w projekcie jest planowane w nowszej wersji. |
| Lib | Dla wielu `lib` pakietów działa tak samo jak w NuGet 2.x, ale z rozszerzonymi opcjami dla tego, jakie nazwy mogą być używane wewnątrz niego i lepszą logiką do wybierania poprawnego podfolderu podczas korzystania z pakietów. Jednak w połączeniu z `ref`folderem `lib` zawiera zestawy, które implementują powierzchnię zdefiniowaną przez zestawy w folderze. `ref` |
| Ref | `ref`jest opcjonalnym folderem, który zawiera zestawy .NET definiujące powierzchnię publiczną (typy publiczne i metody) dla aplikacji do skompilowania. Zestawy w tym folderze może mieć żadnej implementacji, są one używane wyłącznie do definiowania powierzchni dla kompilatora. Jeśli pakiet nie `ref` ma folderu, `lib` to jest zarówno zestaw odwołania i zestawu implementacji. |
| Środowiska wykonawcze | `runtimes`to opcjonalny folder zawierający kod specyficzny dla systemu operacyjnego, taki jak architektura procesora i pliki binarne specyficzne dla systemu operacyjnego lub w inny sposób zależne od platformy. |

## <a name="msbuild-targets-and-props-files-in-packages"></a>MSBuild cele i rekwizyty plików w pakietach

Pakiety NuGet `.targets` `.props` mogą zawierać i pliki, które są importowane do dowolnego projektu MSBuild, w którym pakiet jest zainstalowany. W NuGet 2.x zostało to `<Import>` zrobione przez `.csproj` wstrzykiwanie instrukcji do pliku, w NuGet 3.0 nie ma żadnych konkretnych akcji "instalacja do projektu". Zamiast tego proces przywracania pakietu `[projectname].nuget.props` `[projectname].NuGet.targets`zapisuje dwa pliki i .

MSBuild wie, aby wyszukać te dwa pliki i automatycznie importuje je na początku i pod koniec procesu kompilacji projektu. Zapewnia to bardzo podobne zachowanie do NuGet 2.x, ale z jedną istotną różnicą: *nie ma gwarantowanej kolejności docelowych / rekwizytów plików w tym przypadku*. Jednak MSBuild zapewnia sposoby zamawiania `BeforeTargets` `AfterTargets` obiektów docelowych za pomocą i atrybutów `<Target>` definicji (zobacz Element [docelowy (MSBuild)](/visualstudio/msbuild/target-element-msbuild).

## <a name="lib-and-ref"></a>Lib i ref

Zachowanie folderu `lib` nie uległo znacznej zmianie w nuget v3. Jednak wszystkie zestawy muszą znajdować się w podfolderach nazwanych po TxM i `lib` nie mogą być już umieszczane bezpośrednio pod folderem. TxM to nazwa platformy, dla których dany zasób w pakiecie ma działać. Logicznie rzecz biorąc, są to rozszerzenie docelowego monikers framework `net45` `net46`(TFM) `netcore50` `dnxcore50` [np.](../reference/target-frameworks.md) TxM może odnosić się do struktury (TFM), jak również innych obszarów powierzchni specyficznych dla platformy. Na przykład uwp TxM (`uap10.0`) reprezentuje obszar powierzchni .NET, a także powierzchni systemu Windows dla aplikacji platformy uniwersalnej systemu Windows.

Przykładowa struktura lib:

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

Folder `lib` zawiera zestawy, które są używane w czasie wykonywania. Dla większości pakietów `lib` folder w ramach dla każdego z docelowych TxMs jest wszystko, co jest wymagane.

## <a name="ref"></a>Ref

Czasami zdarzają się przypadki, w których podczas kompilacji powinien być używany inny zestaw (zestawy odwołań.NET). W takich przypadkach należy użyć folderu najwyższego poziomu o nazwie `ref` (skrót od "Zestawy odwołań").

Większość autorów pakietów `ref` nie wymaga tego folderu. Jest to przydatne dla pakietów, które muszą zapewnić spójną powierzchnię kompilacji i IntelliSense, ale następnie mają inną implementację dla różnych TxM. Największym przypadkiem użycia tego `System.*` są pakiety, które są produkowane w ramach wysyłki .NET Core na NuGet. Te pakiety mają różne implementacje, które są ujednolicone przez spójny zestaw zestawów ref.

Mechanicznie zestawy zawarte w folderze `ref` są zestawami odwołań przekazywanymi do kompilatora. Dla tych z Was, którzy korzystali z csc.exe są zestawy jesteśmy przekazywania do [C# / reference przełącznik opcji.](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option)

Struktura folderu `ref` jest taka `lib`sama jak na przykład:

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

W tym przykładzie zestawy `ref` w katalogach będą identyczne.

## <a name="runtimes"></a>Środowiska wykonawcze

Folder runtimes zawiera zestawy i biblioteki macierzyste wymagane do uruchamiania w określonych "środowiskach uruchomieniowych", które są zazwyczaj definiowane przez system operacyjny i architekturę procesora. Te środowiska wykonawcze są identyfikowane przy użyciu [identyfikatorów środowiska uruchomieniowego (RID),](/dotnet/core/rid-catalog) `win`takich jak `win-x86`, , `win7-x86`, `win8-64`itp.

## <a name="native-helpers-to-use-platform-specific-apis"></a>Natywni pomocnicy do korzystania z interfejsów API specyficznych dla platformy

W poniższym przykładzie pokazano pakiet, który ma czysto zarządzaną implementację dla kilku platform, ale używa natywnych pomocników w systemie Windows 8, gdzie można wywołać natywne interfejsy API specyficzne dla systemu Windows 8.

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

Biorąc pod uwagę powyższy pakiet, dzieją się następujące rzeczy:

- Gdy nie ma w `lib/net40/MyLibrary.dll` systemie Windows 8, używany jest zestaw.

- Gdy w systemie `runtimes/win8-<architecture>/lib/MyLibrary.dll` Windows 8 `native/MyNativeHelper.dll` jest używany i jest kopiowany do danych wyjściowych kompilacji.

W powyższym `lib/net40` przykładzie zestaw jest czysto zarządzany kod, podczas gdy zestawy w folderze runtimes będzie p/invoke do natywnego zestawu pomocnika do wywołania interfejsów API specyficznych dla systemu Windows 8.

Tylko jeden `lib` folder jest kiedykolwiek pobierany, więc jeśli istnieje folder specyficzny dla środowiska wykonawczego, jest on wybrany przez niepodejmować specyficznego dla `lib`środowiska wykonawczego. Folder macierzysty jest addytywny, jeśli istnieje, jest kopiowany do danych wyjściowych kompilacji.

## <a name="managed-wrapper"></a>Otoka zarządzana

Innym sposobem użycia środowisk uruchomieniowych jest wysłanie pakietu, który jest czysto otoką zarządzaną przez natywny zestaw. W tym scenariuszu można utworzyć pakiet, podobnie jak następujące:

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

W takim przypadku nie ma `lib` żadnego folderu najwyższego poziomu, ponieważ nie ma implementacji tego pakietu, który nie polega na odpowiednim zestawie macierzystym. Jeśli zarządzanyzespoł, `MyLibrary.dll`, był dokładnie taki sam w obu tych `lib` przypadkach, to możemy umieścić go w folderze najwyższego poziomu, ale ponieważ brak natywnego zestawu nie powoduje, że pakiet nie może zainstalować, jeśli został zainstalowany na platformie, która nie była win-x86 lub win-x64 następnie lib najwyższego poziomu będzie używany, ale nie natywnyzezeszes będzie kopiowany.

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a>Tworzenie pakietów dla NuGet 2 i NuGet 3

Jeśli chcesz utworzyć pakiet, który może być `packages.config` używany przez projekty `project.json` przy użyciu, a także pakiety przy użyciu następnie stosuje się następujące:

- Ref i runtimes działają tylko na NuGet 3. Oba są ignorowane przez NuGet 2.

- Nie można `install.ps1` polegać na lub `uninstall.ps1` do działania. Pliki te są `packages.config`wykonywane podczas korzystania `project.json`z programu , ale są ignorowane za pomocą programu . Więc pakiet musi być użyteczny bez ich uruchamiania. `init.ps1`nadal działa na NuGet 3.

- Obiekty docelowe i props instalacji jest inna, więc upewnij się, że pakiet działa zgodnie z oczekiwaniami na obu klientach.

- Podkatalogi lib musi być TxM w NuGet 3. Nie można umieszczać bibliotek w `lib` katalogu głównym folderu.

- Zawartość nie jest kopiowana automatycznie za pomocą nuget 3. Konsumenci pakietu mogą samodzielnie kopiować pliki lub używać narzędzia, takiego jak narzędzie, aby zautomatyzować kopiowanie plików.

- Transformacje plików źródłowych i konfiguracyjnych nie są uruchamiane przez nuget 3.

Jeśli obsługujesz NuGet 2 i 3 następnie `minClientVersion` powinny być najniższą wersję klienta NuGet 2, że pakiet działa na. W przypadku istniejącego pakietu nie należy go zmieniać.
