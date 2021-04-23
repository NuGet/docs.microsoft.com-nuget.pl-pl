---
title: Informacje o platformach docelowych dla programu NuGet
description: Odwołania do docelowej struktury NuGet identyfikują i izolują składniki zależne od struktury pakietu.
author: JonDouglas
ms.author: jodou
ms.date: 12/11/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: d7f91880096b5cbdca7447f7838634ff099c3c4c
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901723"
---
# <a name="target-frameworks"></a>Platformy docelowe

Program NuGet używa odwołań do platform docelowych w różnych miejscach, aby identyfikować i izolować składniki zależne od struktury pakietu:

- [plik projektu:](../create-packages/multiple-target-frameworks-project-file.md)w przypadku projektów w stylu zestawu SDK plik *csproj* zawiera odwołania do platformy docelowej.
- [Manifest nuspec: pakiet](../reference/nuspec.md)może wskazywać odrębne pakiety, które mają zostać uwzględnione w projekcie, w zależności od struktury docelowej projektu.
- [Nazwa folderu .nupkg:](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)foldery wewnątrz folderu pakietu mogą być nazwane zgodnie z platformą docelową, z których każdy zawiera biblioteki DLL i inną zawartość odpowiednią dla `lib` tej struktury.
- [packages.config: ](../reference/packages-config.md)atrybut zależności określa `targetframework` wariant pakietu do zainstalowania.

> [!Note]
> NuGet obsługuje wszystkie nowoczesne struktury docelowe .NET:
> - Aby uzyskać listę najnowszych platform docelowych, zobacz dokumentację Platformy docelowe w projektach w [stylu zestawu SDK.](/dotnet/standard/frameworks)

## <a name="supported-frameworks"></a>Obsługiwane struktury

Do struktury zwykle odwołuje się krótka podwzorca struktury docelowej lub program TFM. W .NET Standard jest to również uogólnione do *TxM,* aby umożliwić pojedyncze odwołanie do wielu platform.

> [!Note]
> Kod źródłowy klienta NuGet, który oblicza poniższe tabele, znajduje się w następujących lokalizacjach:
> - Obsługiwane nazwy platform: [FrameworkConstants.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/FrameworkConstants.cs)
> - Pierwszeństwo i mapowanie struktury: [DefaultFrameworkMappings.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/DefaultFrameworkMappings.cs)

Klienci NuGet obsługują struktury w poniższej tabeli. Odpowiedniki są wyświetlane w nawiasach kwadratowych []. Należy pamiętać, że niektóre narzędzia, takie jak , mogą używać odmian kanonicznych `dotnet` TFM w niektórych plikach. Na przykład `dotnet pack` używa w  `.NETCoreApp2.0` pliku, a `.nuspec` nie `netcoreapp2.0` . Różne narzędzia klienta NuGet prawidłowo obsługują te odmiany, ale podczas bezpośredniego edytowania plików należy zawsze używać kanonicznych narzędzi TFM.

| Nazwa | Skrót | TfMs/TxMs |
| ------------- | ------------ | --------- |
|.NET Framework | net | net11 |
| | | net20 |
| | | net35 |
| | | net40 |
| | | net403 |
| | | net45 |
| | | net451 |
| | | net452 |
| | | net46 |
| | | net461 |
| | | net462 |
| | | net47 |
| | | net471 |
| | | net472 |
| | | net48 |
|Microsoft Store (Sklep Windows) | netcore | netcore [netcore45] |
| | | netcore45 [win, win8] |
| | | netcore451 [win81] |
| | | netcore50 |
|.NET MicroFramework | netmf | netmf |
|Windows | Wygrać | win [win8, netcore45] |
| | | win8 [netcore45, win] |
| | | win81 [netcore451] |
| | | win10 (nie jest obsługiwane przez Windows 10 Platform) |
Silverlight | Sl | sl4 |
| | | sl5 |
Windows Phone (SL) | Wp | wp [wp7] |
| | | wp7 |
| | | wp75 |
| | | wp8 |
| | | wp81 |
Windows Phone (UWP) | | wpa81 |
Platforma uniwersalna systemu Windows | Uap | uap [uap10.0] |
| | | uap10.0 |
| | | uap10.0.xxxxx (gdzie 10.0.xxxxx to minimalna wersja aplikacji zużywanej na platformie docelowej) |
.NET Standard | netstandard | netstandard1.0 |
| | | netstandard1.1 |
| | | netstandard1.2 |
| | | netstandard1.3 |
| | | netstandard1.4 |
| | | netstandard1.5 |
| | | netstandard1.6 |
| | | netstandard2.0 |
| | | netstandard2.1 |
.NET 5+ (i .NET Core) | netcoreapp | netcoreapp1.0 |
| | | netcoreapp1.1 |
| | | netcoreapp2.0 |
| | | netcoreapp2.1 |
| | | netcoreapp2.2 |
| | | netcoreapp3.0 |
| | | netcoreapp3.1 |
| | net | net5.0 |
| | | net6.0 |
Tizen | tizen | tizen3 |
| | | tizen4 |

## <a name="deprecated-frameworks"></a>Przestarzałe struktury

Następujące struktury są przestarzałe. Pakiety przeznaczone dla tych platform powinny być migrowane do wskazanych zamian.

| Przestarzała framework | Funkcja zastępująca
| --- | ---
| aspnet50 | netcoreapp |
| aspnetcore50 |
| dnxcore50 |
| Dnx |
| dnx45 |
| dnx451 |
| dnx452 |
| dotnet | netstandard |
| dotnet50 | |
| dotnet51 | |
| dotnet52 | |
| dotnet53 | |
| dotnet54 | |
| dotnet55 | |
| dotnet56 | |
| Winrt | Wygrać |

## <a name="precedence"></a>Pierwszeństwo

Wiele platform jest powiązanych ze sobą i ze sobą zgodnych, ale niekoniecznie równoważnych:

| Framework | Można użyć |
| -- | --- |
| uap (platforma uniwersalna systemu Windows) | win81 |
| | wpa81 |
| | netcore50 |
| win (Microsoft Store) | Winrt |
| | |

## <a name="net-standard"></a>NET Standard

[.NET Standard](/dotnet/standard/net-standard) odwołań między platformami zgodnymi z plikami binarnymi, umożliwiając pojedynczej platformie docelowej odwołanie się do kombinacji innych. (Aby uzyskać podstawowe informacje, zobacz [.NET Primer](/dotnet/articles/standard/index)).)

Narzędzie [NuGet Get Nearest Framework Tool](https://aka.ms/s2m3th) symuluje to, czego używa pakiet NuGet, aby wybrać jedną platformę z wielu dostępnych zasobów struktury w pakiecie na podstawie struktury projektu.

Seria monikerów powinna być używana w programie NuGet 3.3 i starszych wersjach. Składnia monikera powinna być używana w wersji `dotnet` `netstandard` 3.4 i nowszych.

## <a name="portable-class-libraries"></a>Biblioteki klas przenośnych

> [!Warning]
> **Nie zaleca się stosowanialsów PCL.** Mimo że adresy PCL są obsługiwane, autorzy pakietów powinni zamiast tego obsługiwać netstandard. Platforma .NET Standard to ewolucja bibliotek PCL, która reprezentuje przenośność binarną na różnych platformach przy użyciu jednej monikera, która nie jest powiązana z biblioteką statyczną, na przykład monikery *portable-a+b+c.*

Aby zdefiniować platformę docelową, która odwołuje się do wielu platform obiektów docelowych podrzędnych, należy użyć słowa kluczowego służącego do poprzedzania listy przywołynych `portable` platform. Unikaj sztucznej kompilacji dodatkowych platform, które nie są bezpośrednio kompilowane, ponieważ może to prowadzić do niezamierzonych efektów ubocznych w tych platformach.

Dodatkowe struktury zdefiniowane przez inne firmy zapewniają zgodność z innymi środowiskami, które są dostępne w ten sposób. Ponadto istnieją skrócone numery profilów, które mogą odwoływać się do tych kombinacji powiązanych platform jako , ale nie jest to zalecane, aby używać tych liczb, ponieważ zmniejsza to czytelność folderów i `Profile#` `.nuspec` .

| Proﬁl # | Struktury | Imię i nazwisko | .NET Standard |
 --- | --- | --- | ---
 Profil2 | . NETFramework 4.0 | portable-net40+win8+sl4+wp7 |
 | | Windows 8.0 | |
 | | Silverlight 4.0 |
 | | WindowsPhone 7.0|
 Profil3 | . NETFramework 4.0 | portable-net40+sl4
 | | Silverlight 4.0 |
 Profil4 | . NETFramework 4.5 | portable-net45+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profil5 | . NETFramework 4.0 | portable-net40+win8
 | | Windows 8.0 |
 Profil6 | . NETFramework 4.0.3 | portable-net403+win8
 | | Windows 8.0 |
 Profil7 | . NETFramework 4.5 | portable-net45+win8 | netstandard1.1
 | | Windows 8.0 |
 Profil14 | . NETFramework 4.0 | portable-net40+sl5
 | | Silverlight 5.0 |
 Profil18 | . NETFramework 4.0.3 | portable-net403+sl4
 | | Silverlight 4.0 |
 Profil19 | . NETFramework 4.0.3 | portable-net403+sl5
 | | Silverlight 5.0 |
 Profil23 | . NETFramework 4.5 | portable-net45+sl4
 | | Silverlight 4.0 |
 Profil24 | . NETFramework 4.5 | portable-net45+sl5
 | | Silverlight 5.0 |
 Profil31 | Windows 8.1 | portable-win81+wp81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 Profil32 | Windows 8.1 | portable-win81+wpa81 | netstandard1.2
 | | WindowsPhone 8.1 (UWP) |
 Profil36 | . NETFramework 4.0 | portable-net40+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profil37 | . NETFramework 4.0 | portable-net40+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profil41 | . NETFramework 4.0.3 | portable-net403+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profil42 | . NETFramework 4.0.3 | portable-net403+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profil44 | . NETFramework 4.5.1 | portable-net451+win81 | netstandard1.2
 | | Windows 8.1 |
 Profil46 | . NETFramework 4.5 | portable-net45+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profil47 | . NETFramework 4.5 | portable-net45+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profil49 | . NETFramework 4.5 | portable-net45+wp8 | netstandard1.0
 | | WindowsPhone 8.0 (SL) |
 Profile78 | . NETFramework 4.5 | portable-net45+win8+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profil84 | WindowsPhone 8.1 | portable-wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (UWP) |
 Profil88 | . NETFramework 4.0 | portable-net40+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profil92 | . NETFramework 4.0 | portable-net40+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profil95 | . NETFramework 4.0.3 | portable-net403+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profil96 | . NETFramework 4.0.3 | portable-net403+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profil102 | . NETFramework 4.0.3 | portable-net403+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profil104 | . NETFramework 4.5 | portable-net45+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profil111 | . NETFramework 4.5 | portable-net45+win8+wpa81 | netstandard1.1
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profil136 | . NETFramework 4.0 | portable-net40+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profil143 | . NETFramework 4.0.3 | portable-net403+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profil147 | . NETFramework 4.0.3 | portable-net403+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profil151 | NETFramework 4.5.1 | portable-net451+win81+wpa81 | netstandard1.2
 | | Windows 8.1 |
 | | WindowsPhone 8.1 (UWP) |
 Profil154 | . NETFramework 4.5 | portable-net45+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profil157 | Windows 8.1 | portable-win81+wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 | | WindowsPhone 8.1 (UWP) |
 Profil158 | . NETFramework 4.5 | portable-net45+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profil225 | . NETFramework 4.0 | portable-net40+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profil240 | . NETFramework 4.0.3 | portable-net403+sl5+win8+wpa8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profil255 | . NETFramework 4.5 | portable-net45+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profil259 | . NETFramework 4.5 | portable-net45+win8+wpa81+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profil328 | . NETFramework 4.0 | portable-net40+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profil336 | . NETFramework 4.0.3 | portable-net403+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profil344 | . NETFramework 4.5 | portable-net45+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |

Ponadto pakiety NuGet przeznaczone dla platformy Xamarin mogą używać dodatkowych platform zdefiniowanych przez platformę Xamarin. Zobacz Creating NuGet packages for Xamarin (Tworzenie pakietów [NuGet dla platformy Xamarin).](https://developer.xamarin.com/guides/cross-platform/advanced/nuget/)

| Nazwa | Opis | .NET Standard |
| --- | --- | ---
| monoandroid | Obsługa mono dla systemu operacyjnego Android | netstandard1.4 |
| monotouch | Obsługa mono dla systemu iOS | netstandard1.4 |
| monomac | Obsługa mono dla systemu OSX | netstandard1.4 |
| xamarinios | Obsługa platformy Xamarin dla systemu iOS | netstandard1.4 |
| xamarinmac | Obsługa platformy Xamarin dla komputerów Mac | netstandard1.4 |
| xamarinpsthree | Obsługa platformy Xamarin na platformie Playstation 3 | netstandard1.4 |
| xamarinpsfour | Obsługa platformy Xamarin na platformie Playstation 4 | netstandard1.4 |
| xamarinps nie | Obsługa platformy Xamarin w programie PS Vita | netstandard1.4 |
| xamarinwatchos | Xamarin for Watch OS | netstandard1.4 |
| xamarintvos | Xamarin dla systemu operacyjnego TV | netstandard1.4 |
| xamarinxboxthreesixty | Xamarin dla XBox 360 | netstandard1.4 |
| xamarinxboxone | Xamarin for XBox One | netstandard1.4 |

> [!Note]
> Stephen Cleary utworzył narzędzie, które wyświetla listę obsługiwanych list PCL, które można znaleźć w jego wpisie Profile [framework na platformie .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html).
