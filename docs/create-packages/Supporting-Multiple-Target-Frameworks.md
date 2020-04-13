---
title: Wielokierunkowe dla pakietów NuGet
description: Opis różnych metod do docelowych wielu wersji programu .NET Framework z jednego pakietu NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 34f7c6132ba6050e20114642932ccf29a5ec088d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429011"
---
# <a name="support-multiple-net-versions"></a>Obsługa wielu wersji platformy .NET

Wiele bibliotek jest przeznaczone dla określonej wersji programu .NET Framework. Na przykład może mieć jedną wersję biblioteki, która jest specyficzna dla platformy uniwersalnej systemu i innej wersji, która korzysta z funkcji w .NET Framework 4.6. Aby to uwzględnić, NuGet obsługuje umieszczanie wielu wersji tej samej biblioteki w jednym pakiecie.

W tym artykule opisano układ pakietu NuGet, niezależnie od sposobu zbudowania pakietu lub zestawów (oznacza to, że układ jest taki sam, czy przy użyciu wielu plików *csproj* w stylu innych niż SDK i niestandardowego pliku *nuspec,* czy pojedynczego wielokierunkowego zestawu SDK w stylu *csproj*). W przypadku projektu w stylu zestawu SDK [obiekty docelowe pakietu](../reference/msbuild-targets.md) NuGet pack wie, jak pakiet musi być rozłożony i automatyzuje umieszczanie zestawów w odpowiednich folderach lib i tworzenie grup zależności dla każdej struktury docelowej (TFM). Aby uzyskać szczegółowe instrukcje, zobacz [Obsługa wielu wersji programu .NET Framework w pliku projektu](multiple-target-frameworks-project-file.md).

Należy ręcznie rozłożyć pakiet zgodnie z opisem w tym artykule podczas korzystania z metody katalogu roboczego opartego na konwencji [opisanej](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)w temacie Tworzenie pakietu . W przypadku projektu w stylu zestawu SDK zalecana jest metoda zautomatyzowana, ale można również ręcznie rozłożyć pakiet zgodnie z opisem w tym artykule.

## <a name="framework-version-folder-structure"></a>Struktura folderów wersji frameworka

Podczas tworzenia pakietu, który zawiera tylko jedną wersję biblioteki lub docelowe `lib` wiele struktur, zawsze należy wykonać podfoldery w ramach przy użyciu różnych nazw struktury z uwzględnieniem wielkości liter z następującą konwencją:

    lib\{framework name}[{version}]

Aby uzyskać pełną listę obsługiwanych nazw, zobacz [odwołanie do ram docelowych](../reference/target-frameworks.md#supported-frameworks).

Nigdy nie należy mieć wersji biblioteki, która nie jest specyficzna dla struktury i umieszczona bezpośrednio w folderze głównym. `lib` (Ta funkcja była obsługiwana `packages.config`tylko z ). W ten sposób sprawi, że biblioteka będzie zgodna z dowolną platformą docelową i pozwoli na zainstalowanie jej w dowolnym miejscu, co prawdopodobnie spowoduje nieoczekiwane błędy środowiska uruchomieniowego. Dodawanie zestawów w folderze `lib\abc.dll`głównym (na przykład) `lib\abc\abc.dll`lub podfolderach (takich jak ) zostało przestarzałe i jest ignorowane podczas korzystania z formatu PackagesReference.

Na przykład następująca struktura folderów obsługuje cztery wersje zestawu, które są specyficzne dla struktury:

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

Aby łatwo dołączyć wszystkie te pliki podczas tworzenia pakietu, użyj `<files>` cyklicznego `.nuspec` `**` symbolu wieloznacznego w sekcji :

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a>Foldery specyficzne dla architektury

Jeśli masz zestawy specyficzne dla architektury, czyli oddzielne zestawy docelowe ARM, x86 i x64, `runtimes` należy umieścić je `{platform}-{architecture}\lib\{framework}` w `{platform}-{architecture}\native`folderze o nazwie w podfolderach o nazwie lub . Na przykład następująca struktura folderów będzie uwzględniać zarówno natywne, `uap10.0` jak i zarządzane biblioteki DLL przeznaczone dla systemu Windows 10 i strukturę:

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

Te zestawy będą dostępne tylko w czasie wykonywania, więc jeśli chcesz podać odpowiedni `AnyCPU` zestaw `/ref/{tfm}` czasu kompilacji, a następnie mają zestaw w folderze. 

Należy pamiętać, NuGet zawsze wybiera te zasoby kompilacji lub środowiska uruchomieniowego z `/ref` `/lib` jednego folderu, więc jeśli istnieją pewne zgodne zasoby od tego czasu zostaną zignorowane, aby dodać zestawy w czasie kompilacji. Podobnie, jeśli istnieją pewne zgodne `/runtimes` zasoby `/lib` od tego czasu również zostaną zignorowane dla środowiska wykonawczego.

Zobacz [Tworzenie pakietów platformy uniwersalnej](../guides/create-uwp-packages.md) systemu i `.nuspec` platformy uniwersalnej systemu, aby uzyskać przykład odwoływania się do tych plików w manifeście.

Zobacz [też: Pakowanie składnika aplikacji ze Sklepu Windows za pomocą usługi NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a>Pasujące wersje zestawu i struktura docelowa w projekcie

Gdy NuGet instaluje pakiet, który ma wiele wersji zestawu, próbuje dopasować nazwę struktury zestawu z ramą docelową projektu.

Jeśli dopasowanie nie zostanie znalezione, NuGet kopiuje zestaw dla najwyższej wersji, która jest mniejsza lub równa platformie docelowej projektu, jeśli jest dostępna. Jeśli nie znaleziono zgodnego zestawu, NuGet zwraca odpowiedni komunikat o błędzie.

Rozważmy na przykład następującą strukturę folderów w pakiecie:

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

Podczas instalowania tego pakietu w projekcie, który jest przeznaczony dla platformy .NET `net45` Framework 4.6, NuGet instaluje zestaw w folderze, ponieważ jest to najwyższa dostępna wersja, która jest mniejsza lub równa 4.6.

Jeśli projekt jest przeznaczony dla platformy .NET Framework 4.6.1, z `net461` drugiej strony NuGet instaluje zestaw w folderze.

Jeśli projekt jest przeznaczony dla platformy .NET framework 4.0 i wcześniejszych, NuGet zgłasza odpowiedni komunikat o błędzie, aby nie znaleźć zgodnego zestawu.

## <a name="grouping-assemblies-by-framework-version"></a>Grupowanie zestawów według wersji framework

NuGet kopiuje zestawy tylko z jednego folderu biblioteki w pakiecie. Załóżmy na przykład, że pakiet ma następującą strukturę folderów:

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

Gdy pakiet jest zainstalowany w projekcie, który jest przeznaczony `MyAssembly.dll` dla platformy .NET Framework 4.5(v2.0) jest jedynym zainstalowanym zestawem. `MyAssembly.Core.dll`(wersja 1.0) nie jest zainstalowany, ponieważ `net45` nie jest wymieniony w folderze. NuGet zachowuje się `MyAssembly.Core.dll` w ten sposób, ponieważ może być `MyAssembly.dll`scalony w wersji 2.0 .

Jeśli chcesz `MyAssembly.Core.dll` zostać zainstalowany dla programu .NET Framework 4.5, umieść kopię w folderze. `net45`

## <a name="grouping-assemblies-by-framework-profile"></a>Grupowanie zestawów według profilu struktury

NuGet obsługuje również kierowanie określonego profilu struktury przez dołączenie kreski i nazwę profilu na końcu folderu.

    lib\{framework name}-{profile}

Obsługiwane profile są następujące:

- `client`: Profil klienta
- `full`: Pełny profil
- `wp`: Windows Phone
- `cf`: Kompaktowa struktura

## <a name="declaring-dependencies-advanced"></a>Deklarowanie zależności (zaawansowane)

Podczas pakowania pliku projektu NuGet próbuje automatycznie wygenerować zależności od projektu. Informacje w tej sekcji dotyczące używania pliku *nuspec* do deklarowania zależności jest zazwyczaj konieczne tylko w przypadku zaawansowanych scenariuszy.

*(Wersja 2.0+)* Można zadeklarować zależności pakietu w *.nuspec* odpowiadające platformie `<group>` docelowej `<dependencies>` projektu docelowego przy użyciu elementów w elemencie. Aby uzyskać więcej informacji, zobacz [element zależności](../reference/nuspec.md#dependencies-element).

Każda grupa ma atrybut `targetFramework` o nazwie `<dependency>` i zawiera zero lub więcej elementów. Te zależności są instalowane razem, gdy struktura docelowa jest zgodna z profilem framework projektu. Zobacz [struktury docelowe](../reference/target-frameworks.md) dla dokładnych identyfikatorów struktury.

Zalecamy użycie jednej grupy na moniker ram docelowych (TFM) dla plików w folderach *lib/* i *ref/.*

Poniższy przykład pokazuje różne `<group>` odmiany elementu:

```xml
<dependencies>

    <group targetFramework="net472">
        <dependency id="jQuery" version="1.10.2" />
        <dependency id="WebActivatorEx" version="2.2.0" />
    </group>

    <group targetFramework="net20">
    </group>

</dependencies>
```

## <a name="determining-which-nuget-target-to-use"></a>Określanie, który obiekt docelowy NuGet ma być używany

Podczas pakowania bibliotek docelowych biblioteki klas przenośnych może być trudne do określenia, który `.nuspec` obiekt docelowy NuGet należy użyć w nazwach folderów i pliku, zwłaszcza jeśli kierowanie tylko podzbiór PCL. Pomogą Ci w tym następujące zasoby zewnętrzne:

- [Profile frameworka w .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)
- [Profile przenośnej biblioteki klas](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): tabela wyliczająca profile PCL i ich równoważne obiekty docelowe NuGet
- [Narzędzie Profile Portable Class Library](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): narzędzie wiersza polecenia do określania profili PCL dostępnych w systemie

## <a name="content-files-and-powershell-scripts"></a>Pliki zawartości i skrypty programu PowerShell

> [!Warning]
> Pliki modyfikowalne zawartości i `packages.config` wykonywanie skryptów są dostępne tylko w formacie; są przestarzałe ze wszystkimi innymi formatami i nie powinny być używane dla żadnych nowych pakietów.

Z `packages.config`, pliki zawartości i skrypty programu PowerShell mogą być pogrupowane według struktury docelowej przy użyciu tej samej konwencji folderów `content` wewnątrz folderów i `tools` folderów. Przykład:

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

Jeśli folder framework pozostaje pusty, NuGet nie dodaje odwołań do zestawu lub plików zawartości ani nie uruchamia skryptów programu PowerShell dla tej struktury.

> [!Note]
> Ponieważ `init.ps1` jest wykonywany na poziomie rozwiązania i nie zależy od projektu, musi być umieszczony bezpośrednio pod folderem. `tools` Jest ignorowana, jeśli jest umieszczana w folderze framework.
