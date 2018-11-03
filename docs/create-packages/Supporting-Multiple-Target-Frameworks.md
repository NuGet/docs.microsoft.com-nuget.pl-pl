---
title: Wielowersyjność kodu dla pakietów NuGet
description: Opis różnych metod pod kątem wiele wersji .NET Framework z w obrębie jednego pakietu NuGet.
author: karann-msft
ms.author: karann
ms.date: 09/27/2017
ms.topic: conceptual
ms.openlocfilehash: c59839240935e2a6c590dea3adf623313f79f02f
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981148"
---
# <a name="supporting-multiple-net-framework-versions"></a>Obsługiwanie wielu wersji programu .NET framework

*Dla projektów .NET Core za pomocą narzędzia NuGet 4.0 +, zobacz [NuGet pakowanie i przywrócić jako elementów docelowych MSBuild](../reference/msbuild-targets.md) szczegółowe informacje na temat określania wartości docelowej dla wielu.*

Wiele bibliotek docelowej określonej wersji programu .NET Framework. Na przykład Niewykluczone, że jedna wersja biblioteki, które są specyficzne dla platformy uniwersalnej systemu Windows, a inna wersja, która korzysta z funkcji .NET Framework 4.6.

Aby uwzględnić w efekcie NuGet obsługuje wprowadzanie wielu wersji tej samej biblioteki w jednym pakiecie, korzystając z oparty na Konwencji pracy katalogu metody opisanej w [Tworzenie pakietu](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).

## <a name="framework-version-folder-structure"></a>Struktura folderów wersji Framework

Podczas tworzenia pakietu zawierającego tylko jedna wersja biblioteki lub docelowej wielu platform, zawsze tworzyć podfoldery `lib` przy użyciu różnych framework uwzględniana wielkość liter nazwy przy użyciu następującej konwencji:

    lib\{framework name}[{version}]

Aby uzyskać pełną listę obsługiwanych nazw, zobacz [odwoływać się do platform docelowych](../reference/target-frameworks.md#supported-frameworks).

Nigdy nie powinny mieć wersję biblioteki, która nie jest przeznaczone do struktury i umieszczone bezpośrednio w katalogu głównym `lib` folderu. (Ta funkcja była obsługiwana tylko w przypadku `packages.config`). Ten sposób będzie dzięki bibliotece zgodny z dowolnej platformy docelowej i zezwolenie na można zainstalować w dowolnym miejscu, prawdopodobnie skutkuje nieoczekiwane błędy. Dodawanie zestawów w katalogu głównym (takie jak `lib\abc.dll`) lub jego podfolderach (takie jak `lib\abc\abc.dll`) jest przestarzały i jest ignorowana, gdy przy użyciu formatu PackagesReference.

Na przykład następującą strukturę folderów obsługuje cztery wersji zestawu, które są specyficzne dla framework:

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

Aby łatwo dołączyć te pliki, podczas tworzenia pakietu, należy użyć cyklicznej `**` symbolu wieloznacznego w `<files>` części Twojej `.nuspec`:

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a>Foldery architektury

W przypadku architektury zestawów, czyli oddzielne zestawy, których platformą docelową ARM, x 86 i x64, trzeba je umieścić w folderze o nazwie `runtimes` w podfolderach o nazwie `{platform}-{architecture}\lib\{framework}` lub `{platform}-{architecture}\native`. Na przykład następującą strukturę folderów może pomieścić natywnych i zarządzanych bibliotek DLL, przeznaczonych dla systemu Windows 10 i `uap10.0` framework:

    \runtimes
        \win10-arm
            \native
            \lib\uap10.0
        \win10-x86
            \native
            \lib\uap10.0
        \win10-x64
            \native
            \lib\uap10.0

Te zestawy będą dostępne tylko w czasie wykonywania, więc jeśli chcesz zapewnić odpowiednie także następnie zestawu czasu kompilacji `AnyCPU` zestawu w `/ref{tfm}` folderu. 

Należy pamiętać, NuGet zawsze wybiera te zasoby kompilacji lub środowisko uruchomieniowe z jednego folderu tak w przypadku niektórych zasoby zgodne z `/ref` następnie `/lib` zostanie zignorowana, aby dodać zestawy kompilacji. Podobnie jeśli istnieją pewne zasoby zgodna z `/runtime` , a następnie również `/lib` zostanie zignorowane dla środowiska uruchomieniowego.

Zobacz [tworzenie pakietów platformy UWP](../guides/create-uwp-packages.md) przykład odwołuje się do tych plików w `.nuspec` manifestu.

Zobacz też [pakowania składnika aplikacji Sklepu Windows za pomocą NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a>Zgodne wersje zestawów i platformy docelowej w projekcie

Podczas instalowania pakietu, który ma wiele wersji zestawu NuGet próbuje dopasować nazwę framework zestawu za pomocą platformy docelowej projektu.

Jeśli nie zostanie znalezione dopasowanie, NuGet kopiuje zestawu dla najwyższa wersja, która jest mniejsza lub równa platformy docelowej projektu, jeśli jest dostępny. Jeśli zestawy zgodna, nie zostanie znaleziony, NuGet zwraca odpowiedni komunikat o błędzie.

Na przykład rozważmy następującą strukturę folderów w pakiecie:

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

Podczas instalowania tego pakietu w projekcie, który jest przeznaczony dla .NET Framework 4.6, NuGet instaluje zestaw w `net45` folderu, ponieważ jest to najnowsza wersja dostępna o rozmiarze mniejszym niż 4.6.

Jeśli projekt jest przeznaczony dla platformy .NET Framework 4.6.1, z drugiej strony, NuGet instaluje zestaw w `net461` folderu.

Jeśli projekt jest przeznaczony dla .NET framework 4.0 i starszych, NuGet zgłasza odpowiedni komunikat o błędzie dla nie wyszukuje zgodny zestawu.

## <a name="grouping-assemblies-by-framework-version"></a>Zestawy są grupowane według framework w wersji

NuGet kopiuje zestawy z tylko jedna biblioteka folder w pakiecie. Na przykład załóżmy, że pakiet ma następującą strukturę folderów:

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

Gdy pakiet jest zainstalowany w projekcie, który jest przeznaczony dla .NET Framework 4.5, `MyAssembly.dll` (w wersji 2.0) to zestaw tylko zainstalowane. `MyAssembly.Core.dll` (w wersji 1.0) nie jest zainstalowany, ponieważ nie znajduje się w `net45` folderu. NuGet zachowuje się w ten sposób, ponieważ `MyAssembly.Core.dll` może mieć scalonego w wersji 2.0 programu `MyAssembly.dll`.

Jeśli chcesz `MyAssembly.Core.dll` konieczności instalowania programu .NET Framework 4.5, Umieść kopię w `net45` folderu.

## <a name="grouping-assemblies-by-framework-profile"></a>Zestawy grupowania w ramach profilu

NuGet obsługuje także przeznaczonych dla profilu określonego framework, dodając kreską i nazwę profilu w celu folderu.

    lib\{framework name}-{profile}

Profile obsługiwane są następujące:

- `client`: Profil klienta
- `full`: Pełny profil
- `wp`: Windows Phone
- `cf`: Compact Framework

## <a name="determining-which-nuget-target-to-use"></a>Określenie, która docelowa NuGet do użycia

Gdy bibliotek tworzenia pakietów przeznaczonych dla biblioteki klas przenośnych może być trudne do określenia docelowej NuGet, które należy używać w nazwach folderów i `.nuspec` pliku, zwłaszcza, jeśli jest to obsługiwane tylko podzbiór PCL. Następujące zasoby zewnętrzne pomoże Ci w tym:

- [Profile Framework na platformie .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)
- [Przenośne biblioteki klas profile](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Tabela wyliczania ich równoważne cele NuGet i profile PCL
- [Przenośne biblioteki klas profilów narzędzia](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): narzędzie wiersza polecenia umożliwiające określanie PCL profile dostępna w systemie

## <a name="content-files-and-powershell-scripts"></a>Pliki zawartości i skryptów programu PowerShell

> [!Warning]
> Modyfikowalne pliki zawartości i wykonywanie skryptu są dostępne z `packages.config` formatowania tylko; zostały zaniechane w innych formatach i nie powinna być używana dla żadnych nowych pakietów.

Za pomocą `packages.config`zawartości, pliki i skrypty programu PowerShell można grupować według platformy docelowej przy użyciu tych samych konwencji folder wewnątrz `content` i `tools` folderów. Na przykład:

    \content
        \net46
            \MyContent.txt
        \net461
            \MyContent461.txt
        \uap
            \MyUWPContent.html
        \netcore
    \tools
        init.ps1
        \net46
            install.ps1
            uninstall.ps1
        \uap
            install.ps1
            uninstall.ps1

Jeśli folder struktury jest puste, NuGet nie jest dodawanie odwołań do zestawów lub plików zawartości i uruchamiaj skrypty programu PowerShell dla tej struktury.

> [!Note]
> Ponieważ `init.ps1` jest wykonywany w rozwiązaniu poziomu i nie jest zależny od projektu musi zostać umieszczony bezpośrednio pod `tools` folderu. Jest on ignorowany, jeśli umieszczony w folderze framework.
