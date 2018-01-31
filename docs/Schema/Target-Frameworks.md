---
title: "Docelowa odwołania struktury programu NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/11/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "NuGet docelowy framework odwołuje się do identyfikacji i izolowanie składników zależnych od framework pakietu."
keywords: Pakiet NuGet przeznaczonych dla, .NET framework cele, wersje programu .NET framework
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: c69ff6efca2dcc4a5c1242277f537012e9f4610f
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="target-frameworks"></a>Docelowych platform

NuGet używa odwołań platformy docelowej w różnych miejscach w szczególności identyfikacji i izolowanie składników zależnych od framework pakietu:

- [.nuspec manifest](../schema/nuspec.md): pakietu można określić różne pakiety, które mają zostać uwzględnione w projekcie, w zależności od platformy docelowej projektu.
- [Nazwa folderu .nupkg](../create-packages/creating-a-package.md#from-a-convention-based-working-directory): folderów w pakiecie `lib` folder może być nazwany zgodnie z platformy docelowej, z których każdy zawiera bibliotek DLL i innej zawartości, które są odpowiednie dla tej struktury.
- [Packages.config](../schema/packages-config.md): `targetframework` atrybut zależności określa wariant pakiet do zainstalowania.

> [!Note]
> Kod źródłowy klienta NuGet, który oblicza w poniższej tabeli znajduje się w następujących lokalizacjach:
> - Obsługiwane nazwy framework: [FrameworkConstants.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/FrameworkConstants.cs)
> - Pierwszeństwo Framework i mapowania: [DefaultFrameworkMappings.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/DefaultFrameworkMappings.cs)

## <a name="supported-frameworks"></a>Obsługiwane platformy

Struktury jest zwykle przywoływany przez moniker platformy docelowej krótka lub TFM. W programie .NET Standard dotyczy to również jest uogólnione w celu *TxM* umożliwia jedno odwołanie do wielu platform.

Klienci NuGet obsługuje platform w poniższej tabeli. Odpowiedniki są wyświetlane w nawiasach []. Należy pamiętać, że niektóre narzędzi, takich jak `dotnet`, mogą używać odmiany canonical TFMs w niektórych plików. Na przykład `dotnet pack` używa `.NETCoreApp2.0` w `.nuspec` pliku zamiast `netcoreapp2.0`. Różnych narzędzi klienta NuGet poprawnie obsłużyć tych różnych wersji, ale zawsze należy używać canonical TFMs podczas edytowania plików bezpośrednio.

| Nazwa           | Skrót | TFMs/TxMs |
| -------------  | ------------ | --------- |
|.NET Framework  | NET          | net11     |
|                |              | net20     |
|                |              | net35     |
|                |              | net40     |
|                |              | net403    |
|                |              | net45      |
|                |              | net451     |
|                |              | net452     |
|                |              | net46      |
|                |              | net461     |
|                |              | net462     |
|Microsoft Store (Sklep Windows) | netcore      | netcore [netcore45] |
|                |              | netcore45 [win, Windows 8] |
|                |              | netcore451 [win81] |
|                |              | netcore50 |
|.NET MicroFramework | netmf    | netmf |
|Windows         | win          | Windows [win8, netcore45] |
| | | Windows 8 [netcore45, win] |
| | | win81 [netcore451] |
| | | Windows 10 (platforma nie obsługuje systemu Windows 10) |
Silverlight | sl | sl4 |
| | | sl5 |
Windows Phone (SL) | WP | WP [wp7] |
| | | wp7 |
| | | wp75 |
| | | wp8 |
| | | wp81 |
Windows Phone (UWP) | | wpa81 |
Platforma uniwersalna systemu Windows | uap | uap [uap10.0] |
| | | uap10.0 |
.NET standard | krótkich nazw netstandard | netstandard1.0 |
| | | netstandard1.1 |
| | | netstandard1.2 |
| | | netstandard1.3 |
| | | netstandard1.4 |
| | | netstandard1.5 |
| | | netstandard1.6 |
| | | netstandard2.0 |
Aplikacja .NET core | netcoreapp | netcoreapp1.0 |
| | | netcoreapp1.1 |
| | | netcoreapp2.0 |
tizen | tizen | tizen3 |
| | | tizen4 |

## <a name="deprecated-frameworks"></a>Przestarzałe struktur
Następujące struktury są przestarzałe. Pakietów przeznaczonych dla tych platform należy zmigrować do wskazanej zastępcze.

| Przestarzałe framework | Zastąpienie
| --- | ---
| aspnet50 | netcoreapp |
| aspnetcore50 |
| dnxcore50 |
| dnx |
| dnx45 |
| dnx451 |
| dnx452 |
| DotNet | krótkich nazw netstandard |
| dotnet50 | |
| dotnet51 | |
| dotnet52 | |
| dotnet53 | |
| dotnet54 | |
| dotnet55 | |
| dotnet56 | |
| winrt | win |

## <a name="precedence"></a>Pierwszeństwo

Liczba struktur są powiązane z i zgodne ze sobą, ale nie jest równorzędny musi:

| Framework | Można użyć |
| --- | --- |
| uap (platformy uniwersalnej systemu Windows) | win81 |
| | wpa81 |
| | netcore50 |
| win (Microsoft Store) | winrt |
| | | winrt45 |

## <a name="net-platform-standard"></a>Standard platformy Asp.net

[Platformy .NET Standard](https://github.com/dotnet/corefx/blob/master/Documentation/architecture/net-platform-standard.md) upraszcza odwołania między struktur zgodnego pliku binarnego, dzięki czemu framework pojedynczym elementem docelowym odwołać kombinacji innych. (W tle, zobacz [Elementarz .NET](/dotnet/articles/standard/index).)

[NuGet pobrania najbliższej Framework narzędzia](https://aka.ms/s2m3th) symuluje NuGet używa do wybrania framework jedną z wielu zasobów framework dostępne w pakiecie na platformę projektu na podstawie.

`dotnet` Serii monikerów powinien być używany w NuGet 3.3 i starszych wersji; `netstandard` składni moniker powinien być używany w v3.4 i nowszych.

## <a name="portable-class-libraries"></a>Biblioteki klas przenośnych

> [!Warning]
> **Nie zaleca się PCLs**. PCLs są obsługiwane, autorzy pakietu należy zamiast tego obsługuje krótkich nazw netstandard. Dla platformy .NET Standard jest rozwój PCLs i reprezentuje przenośność binarnego na platformach przy użyciu pojedynczego krótkiej nazwy statyczne, takie jak, takich jak elementy nie jest związane *przenośnych-+ b + c* monikerów.

Aby zdefiniować docelowe środowisko, które odwołuje się do wielu podrzędnych docelowych platform `portable` użyj słowa kluczowego używany do prefiksu lista platform do którego istnieje odwołanie. Unikaj, łącznie z sztucznie dodatkowy platform, które nie są bezpośrednio kompilowane przed ponieważ może spowodować niezamierzone skutki uboczne w tych środowisk.

Dodatkowe struktury zdefiniowane przez osoby trzecie zapewniają zgodność z innych środowiskach, które są dostępne w ten sposób. Ponadto są dostępne do odwołania te kombinacje pokrewne struktury jako numery profilu skrócona `Profile#`, ale nie jest zalecanym rozwiązaniem używać te liczby, ponieważ zmniejsza czytelność folderów i `.nuspec`.

| Profil # | Struktury | Pełna nazwa | .NET standard |
 --- | --- | --- | ---
 Profile2 | .NETFramework 4.0 | portable-net40+win8+sl4+wp7 |
 | | Windows 8.0 | |
 | | Silverlight 4.0 |
 | | WindowsPhone 7.0|
 Profile3 | .NETFramework 4.0 | portable-net40+sl4
 | | Silverlight 4.0 |
 Profile4 | .NETFramework 4.5 | portable-net45+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile5 | .NETFramework 4.0 | portable-net40+win8
 | | Windows 8.0 |
 Profile6 | .NETFramework 4.0.3 | portable-net403+win8
 | | Windows 8.0 |
 Profile7 | .NETFramework 4.5 | portable-net45+win8 | netstandard1.1
 | | Windows 8.0 |
 Profile14 | .NETFramework 4.0 | portable-net40+sl5
 | | Silverlight 5.0 |
 Profile18 | .NETFramework 4.0.3 | portable-net403+sl4
 | | Silverlight 4.0 |
 Profile19 | .NETFramework 4.0.3 | portable-net403+sl5
 | | Silverlight 5.0 |
 Profile23 | .NETFramework 4.5 | portable-net45+sl4
 | | Silverlight 4.0 |
 Profile24 | .NETFramework 4.5 | portable-net45+sl5
 | | Silverlight 5.0 |
 Profile31 | Windows 8.1 | portable-win81+wp81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 Profile32 | Windows 8.1 | portable-win81+wpa81 | netstandard1.2
 | | WindowsPhone 8.1 (UWP) |
 Profile36 | .NETFramework 4.0 | portable-net40+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile37 | .NETFramework 4.0 | portable-net40+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile41 | .NETFramework 4.0.3 | portable-net403+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile42 | .NETFramework 4.0.3 | portable-net403+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile44 | .NETFramework 4.5.1 | portable-net451+win81 | netstandard1.2
 | | Windows 8.1 |
 Profile46 | .NETFramework 4.5 | portable-net45+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile47 | .NETFramework 4.5 | portable-net45+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile49 | .NETFramework 4.5 | portable-net45+wp8 | netstandard1.0
 | | WindowsPhone 8.0 (SL) |
 Profile78 | .NETFramework 4.5 | portable-net45+win8+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile84 | WindowsPhone 8.1 | portable-wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (UWP) |
 Profile88 | .NETFramework 4.0 | portable-net40+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile92 | .NETFramework 4.0 | portable-net40+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile95 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile96 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile102 | .NETFramework 4.0.3 | portable-net403+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile104 | .NETFramework 4.5 | portable-net45+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile111 | .NETFramework 4.5 | portable-net45+win8+wpa81 | netstandard1.1
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile136 | .NETFramework 4.0 | portable-net40+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile143 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile147 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile151 | NETFramework 4.5.1 | portable-net451+win81+wpa81 | netstandard1.2
 | | Windows 8.1 |
 | | WindowsPhone 8.1 (UWP) |
 Profile154 | .NETFramework 4.5 | portable-net45+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile157 | Windows 8.1 | portable-win81+wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 | | WindowsPhone 8.1 (UWP) |
 Profile158 | .NETFramework 4.5 | portable-net45+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile225 | .NETFramework 4.0 | portable-net40+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile240 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile255 | .NETFramework 4.5 | portable-net45+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile259 | .NETFramework 4.5 | portable-net45+win8+wpa81+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile328 | .NETFramework 4.0 | portable-net40+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile336 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile344 | .NETFramework 4.5 | portable-net45+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |

Ponadto pakiety NuGet przeznaczonych dla platformy Xamarin mogą korzystać z dodatkowych struktury zdefiniowane Xamarin. Zobacz [pakietów NuGet tworzenie xamarin](https://developer.xamarin.com/guides/cross-platform/advanced/nuget/).

| Nazwa | Opis | .NET standard |
| --- | --- | ---
| monoandroid | Obsługa mono system operacyjny Android | netstandard1.4 |
| monotouch | Mono obsługę systemu iOS | netstandard1.4 |
| monomac | Mono pomocy technicznej dla systemu OS x | netstandard1.4 |
| xamarinios | Obsługa platformy Xamarin dla systemu iOS | netstandard1.4 |
| xamarinmac | Obsługuje xamarin dla komputerów Mac | netstandard1.4 |
| xamarinpsthree | Obsługa platformy Xamarin w Playstation 3 | netstandard1.4 |
| xamarinpsfour | Obsługa platformy Xamarin w Playstation 4 | netstandard1.4 |
| xamarinpsvita | Obsługa platformy Xamarin w PS Vita | netstandard1.4 |
| xamarinwatchos | Xamarin dla systemu operacyjnego czujki | netstandard1.4 |
| xamarintvos | Xamarin dla systemu operacyjnego TV | netstandard1.4 |
| xamarinxboxthreesixty | Xamarin dla konsoli XBox 360 | netstandard1.4 |
| xamarinxboxone | Xamarin dla konsoli XBox One | netstandard1.4 |

> [!Note]
> Podwyższenie Stephen utworzył narzędzie, które wyświetla listę obsługiwanych PCLs, które można znaleźć na jego post, [Framework profilów w programie .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html).
