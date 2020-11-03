---
title: Wiele elementów docelowych dla pakietów NuGet
description: Opis różnych metod ukierunkowanych na wiele wersji .NET Framework z jednego pakietu NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 7c0da38ab4059b89c9693ecbece2bc8ed1a775ec
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237948"
---
# <a name="support-multiple-net-versions"></a>Obsługa wielu wersji platformy .NET

Wiele bibliotek jest przeznaczonych dla określonej wersji .NET Framework. Na przykład może istnieć jedna wersja biblioteki, która jest specyficzna dla platformy UWP, oraz inna wersja, która wykorzystuje funkcje w .NET Framework 4,6. Aby to umożliwić, pakiet NuGet obsługuje umieszczanie wielu wersji tej samej biblioteki w jednym pakiecie.

W tym artykule opisano układ pakietu NuGet, bez względu na to, w jaki sposób jest tworzony pakiet lub zestawy (to oznacza, że układ jest taki sam, niezależnie od tego, czy jest używany wiele plików *csproj.* *.nuspec* *.csproj* W przypadku projektu w stylu zestawu SDK [elementy docelowe pakietu](../reference/msbuild-targets.md) NuGet wiedzą, w jaki sposób pakiet musi być layed i automatyzuje umieszczanie zestawów w poprawnych folderach lib i tworzenie grup zależności dla każdej platformy docelowej (TFM). Aby uzyskać szczegółowe instrukcje, zobacz [Obsługa wielu wersji .NET Framework w pliku projektu](multiple-target-frameworks-project-file.md).

Należy ręcznie określić pakiet, zgodnie z opisem w tym artykule w przypadku korzystania z metody katalogu roboczego opartej na Konwencji opisanej w temacie [Tworzenie pakietu](../create-packages/creating-a-package.md#from-a-convention-based-working-directory). W przypadku projektu w stylu zestawu SDK zaleca się metodę zautomatyzowaną, ale można również ręcznie określić układ pakietu zgodnie z opisem w tym artykule.

## <a name="framework-version-folder-structure"></a>Struktura folderu wersji struktury

Podczas kompilowania pakietu zawierającego tylko jedną wersję biblioteki lub docelową wiele struktur, należy zawsze tworzyć podfoldery w ramach `lib` różnych nazw struktur uwzględniających wielkość liter w następującej konwencji:

    lib\{framework name}[{version}]

Aby uzyskać pełną listę obsługiwanych nazw, zobacz [Dokumentacja platformy docelowej](../reference/target-frameworks.md#supported-frameworks).

Nigdy nie należy mieć wersji biblioteki, która nie jest specyficzna dla struktury i umieszczona bezpośrednio w `lib` folderze głównym. (Ta funkcja była obsługiwana tylko w systemie `packages.config` ). Dzięki temu biblioteka będzie zgodna z żadną platformą docelową i będzie można ją zainstalować w dowolnym miejscu, co może spowodować nieoczekiwane błędy w czasie wykonywania. Dodawanie zestawów w folderze głównym (takim jak `lib\abc.dll` ) lub podfolderach (takich jak `lib\abc\abc.dll` ) zostało zaniechane i jest ignorowane w przypadku używania formatu PackagesReference.

Na przykład następująca struktura folderów obsługuje cztery wersje zestawu, który jest specyficzny dla platformy:

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

Aby łatwo uwzględnić wszystkie te pliki podczas kompilowania pakietu, użyj cyklicznego `**` symbolu wieloznacznego w `<files>` sekcji `.nuspec` :

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a>Foldery specyficzne dla architektury

W przypadku zestawów specyficznych dla architektury, czyli oddzielnych zestawów przeznaczonych dla ARM, x86 i x64, należy umieścić je w folderze o nazwie `runtimes` w podfolderach o nazwie `{platform}-{architecture}\lib\{framework}` lub `{platform}-{architecture}\native` . Na przykład następująca struktura folderów będzie obsługiwać natywne i zarządzane biblioteki DLL przeznaczone dla systemu Windows 10 i `uap10.0` platformy:

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

Te zestawy będą dostępne tylko w czasie wykonywania, dlatego jeśli chcesz podać odpowiedni zestaw czasu kompilacji, a następnie `AnyCPU` zestaw w `/ref/{tfm}` folderze. 

Należy pamiętać, że pakiet NuGet zawsze wybiera te zasoby kompilacji lub środowiska uruchomieniowego z jednego folderu, więc jeśli istnieją pewne zgodne zasoby z tej wersji, `/ref` `/lib` zostaną zignorowane w celu dodania zestawów czasu kompilacji. Podobnie, jeśli istnieją pewne zgodne zasoby, `/runtimes` również `/lib` zostaną zignorowane w środowisku uruchomieniowym.

Zobacz [Tworzenie pakietów platformy UWP](../guides/create-uwp-packages.md) na przykład odwoływania się do tych plików w `.nuspec` manifeście.

Zobacz też artykuł [pakowanie składnika aplikacji ze sklepu Windows za pomocą narzędzia NuGet](/archive/blogs/mim/packaging-a-windows-store-apps-component-with-nuget-part-2)

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a>Dopasowanie wersji zestawu i platformy docelowej w projekcie

Gdy narzędzie NuGet zainstaluje pakiet z wieloma wersjami zestawu, próbuje dopasować nazwę platformy do zestawu przy użyciu platformy docelowej projektu.

Jeśli dopasowanie nie zostanie znalezione, pakiet NuGet kopiuje zestaw dla najwyższej wersji, która jest mniejsza lub równa docelowej platformy projektu, jeśli jest dostępna. Jeśli nie odnaleziono zgodnego zestawu, pakiet NuGet zwróci odpowiedni komunikat o błędzie.

Rozważmy na przykład następującą strukturę folderów w pakiecie:

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

Podczas instalowania tego pakietu w projekcie, który jest przeznaczony dla .NET Framework 4,6, pakiet NuGet instaluje zestaw w `net45` folderze, ponieważ jest to najwyższa dostępna wersja, która jest mniejsza lub równa 4,6.

Jeśli projekt jest przeznaczony .NET Framework 4.6.1, z drugiej strony pakiet NuGet instaluje zestaw w `net461` folderze.

Jeśli projekt jest przeznaczony dla programu .NET Framework 4,0 i jego wcześniejszych wersji, pakiet NuGet zgłasza odpowiedni komunikat o błędzie, aby nie znaleźć zgodnego zestawu.

## <a name="grouping-assemblies-by-framework-version"></a>Grupowanie zestawów według wersji struktury

Pakiet NuGet kopiuje zestawy tylko z jednego folderu biblioteki w pakiecie. Załóżmy na przykład, że pakiet ma następującą strukturę folderów:

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

Gdy pakiet jest zainstalowany w projekcie, który jest przeznaczony dla .NET Framework 4,5, `MyAssembly.dll` (v 2.0) jest jedynym zainstalowanym zestawem. `MyAssembly.Core.dll` (wersja 1.0) nie jest zainstalowana, ponieważ nie znajduje się ona w `net45` folderze. Pakiet NuGet działa w ten sposób `MyAssembly.Core.dll` , ponieważ mógł zostać scalony w wersji 2,0 programu `MyAssembly.dll` .

Jeśli chcesz `MyAssembly.Core.dll` zainstalować program dla .NET Framework 4,5, Umieść kopię w `net45` folderze.

## <a name="grouping-assemblies-by-framework-profile"></a>Grupowanie zestawów według profilu struktury

Pakiet NuGet obsługuje również określanie konkretnego profilu struktury przez dołączenie kreski i nazwy profilu do końca folderu.

    lib\{framework name}-{profile}

Obsługiwane są następujące profile:

- `client`: Profil klienta
- `full`: Pełny profil
- `wp`: Windows Phone
- `cf`: Compact Framework

## <a name="declaring-dependencies-advanced"></a>Deklarowanie zależności (Zaawansowane)

Podczas pakowania pliku projektu, pakiet NuGet próbuje automatycznie wygenerować zależności od projektu. Informacje przedstawione w tej sekcji dotyczące używania pliku *. nuspec* do deklarowania zależności są zwykle wymagane tylko w przypadku zaawansowanych scenariuszy.

*(Wersja 2.0 +)* Zależności pakietu można zadeklarować w elemencie *. nuspec* odpowiadającym platformie docelowej projektu docelowego za pomocą `<group>` elementów w obrębie `<dependencies>` elementu. Aby uzyskać więcej informacji, zobacz [zależności elementu](../reference/nuspec.md#dependencies-element).

Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej `<dependency>` elementów. Te zależności są instalowane razem, gdy struktura docelowa jest zgodna z profilem struktury projektu. Zobacz [Platformy docelowe](../reference/target-frameworks.md) dla dokładnych identyfikatorów platformy.

Zalecamy używanie jednej grupy na potrzeby monikera platformy docelowej (TFM) dla plików w *bibliotekach lib/* i *ref/* foldery.

W poniższym przykładzie przedstawiono różne odmiany `<group>` elementu:

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

## <a name="determining-which-nuget-target-to-use"></a>Ustalanie, który obiekt docelowy NuGet ma być używany

W przypadku bibliotek opakowaniowych przeznaczonych dla przenośnej biblioteki klas może być to konieczne, aby określić, który obiekt docelowy NuGet ma być używany w nazwach folderów i `.nuspec` pliku, szczególnie w przypadku określania tylko podzestawu PCL. Następujące zasoby zewnętrzne pomogą Ci:

- [Profile struktury w programie .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)
- [Profile biblioteki klas przenośnych](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): tabele wyliczające profile PCL i ich równoważne cele NuGet
- [Narzędzie profilów biblioteki klas przenośnych](https://github.com/StephenCleary/PortableLibraryProfiles) (GitHub.com): Narzędzie wiersza polecenia służące do określania profilów PCL dostępnych w systemie.

## <a name="content-files-and-powershell-scripts"></a>Pliki zawartości i skrypty programu PowerShell

> [!Warning]
> Modyfikowalne pliki zawartości i wykonywanie skryptów są dostępne `packages.config` tylko w formacie. są one przestarzałe ze wszystkimi innymi formatami i nie powinny być używane dla żadnych nowych pakietów.

W programie `packages.config` pliki zawartości i skrypty programu PowerShell mogą być pogrupowane według platformy docelowej przy użyciu tej samej Konwencji folderów w `content` `tools` folderach i. Przykład:

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

Jeśli folder struktury pozostanie pusty, pakiet NuGet nie dodaje odwołań do zestawu ani plików zawartości ani nie uruchamia skryptów programu PowerShell dla tej struktury.

> [!Note]
> Ponieważ `init.ps1` jest wykonywany na poziomie rozwiązania i nie zależy od projektu, musi być umieszczony bezpośrednio w `tools` folderze. Ta wartość jest ignorowana, jeśli jest umieszczona w folderze struktury.